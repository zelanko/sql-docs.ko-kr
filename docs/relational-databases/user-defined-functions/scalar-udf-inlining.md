---
title: Microsoft SQL Server의 스칼라 UDF 인라인 처리 | Microsoft Docs
description: 스칼라 UDF 인라인 처리 기능은 SQL Server(SQL Server 2019부터)에서 스칼라 UDF를 호출하는 쿼리의 성능을 향상하기 위한 것입니다.
ms.custom: ''
ms.date: 03/17/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: s-r-k
ms.author: karam
monikerRange: = azuresqldb-current || >= sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 79608c96e56a7f70d10aaa4b897db837bdf03acc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79486552"
---
# <a name="scalar-udf-inlining"></a>스칼라 UDF 인라인 처리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [지능형 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md) 기능 모음의 기능인 스칼라 UDF 인라인 처리를 소개합니다. 이 기능은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQLv15](../../includes/sssqlv15-md.md)]부터)에서 스칼라 UDF를 호출하는 쿼리의 성능을 향상합니다.

## <a name="t-sql-scalar-user-defined-functions"></a>T-SQL 스칼라 사용자 정의 함수
[!INCLUDE[tsql](../../includes/tsql-md.md)]로 구현되며 단일 데이터 값을 반환하는 UDF(사용자 정의 함수)를 T-SQL 스칼라 사용자 정의 함수라고 합니다. T-SQL UDF는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리에서 코드 재사용과 모듈화를 구현하는 세련된 방법입니다. 일부 계산(예: 복잡한 비즈니스 규칙)은 명령적 UDF 형태에서 더 표현하기 쉽습니다. UDF는 복잡한 SQL 쿼리를 작성하기 위한 전문 지식 없이도 복잡한 논리를 구축하는 데 도움이 됩니다.

## <a name="performance-of-scalar-udfs"></a>스칼라 UDF 성능
스칼라 UDF의 성능이 저하되는 이유는 일반적으로 다음과 같습니다.

- **반복 호출:** UDF가 튜플 정규화마다 한 번씩 반복적인 방식으로 호출됩니다. 이렇게 하면 함수 호출로 인해 반복적인 컨텍스트 전환에 따른 추가 비용이 발생합니다. 특히 해당 정의에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 실행하는 UDF에는 심각한 영향이 있습니다.

- **비용 부족:** 최적화 중에는 관계형 연산자에만 비용을 지불하고 스칼라 연산자는 지불하지 않습니다. 스칼라 UDF 도입 이전에는 보통 다른 스칼라 연산자가 더 저렴했고 비용이 필요하지 않았습니다. 스칼라 작업에 소규모 CPU 비용만 추가되면 충분했습니다. 실제 비용이 큰데 적게 표시되는 시나리오가 있습니다.

- **실행 해석:** UDF는 명령문 단위로 실행되는 명령문 일괄 처리로 평가됩니다. 각 문 자체가 컴파일되며 컴파일된 계획은 캐시됩니다. 이 캐싱 전략에서는 다시 컴파일하지 않고 각각의 문이 격리 실행되므로 시간을 상당 수준 절약할 수 있습니다. 교차 문 최적화는 수행되지 않습니다.

- **직렬 실행:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 UDF를 호출하는 쿼리 내부 병렬 처리가 허용되지 않습니다. 

## <a name="automatic-inlining-of-scalar-udfs"></a>스칼라 UDF의 자동 인라인 처리
스칼라 UDF 인라인 처리 기능의 목표는 UDF 실행이 주요 병목 현상이 되는 T-SQL 스칼라 UDF를 호출하는 쿼리 성능을 높이는 것입니다.

이 새 기능을 통해 스칼라 UDF는 자동으로 스칼라 식이나 스칼라 하위 쿼리로 변환되며 호출하는 쿼리에서 UDF 연산자 대신 대체됩니다. 그런 다음, 이 식 및 하위 쿼리가 최적화됩니다. 따라서 쿼리 계획에는 이제 사용자 정의 함수 연산자가 없으나 그 영향은 계획의 보기나 인라인 TVF 등에서 확인할 수 있습니다.

### <a name="example-1---single-statement-scalar-udf"></a>예제 1 - 단일 문 스칼라 UDF
다음 쿼리를 살펴보세요.

```sql
SELECT L_SHIPDATE, O_SHIPPRIORITY, SUM (L_EXTENDEDPRICE *(1 - L_DISCOUNT)) 
FROM LINEITEM
INNER JOIN ORDERS
  ON O_ORDERKEY = L_ORDERKEY 
GROUP BY L_SHIPDATE, O_SHIPPRIORITY ORDER BY L_SHIPDATE;
```

이 쿼리는 품목의 할인 가격 합계를 계산하고 출고일과 출고 우선 순위에 따라 그룹화된 결과를 표시합니다. `L_EXTENDEDPRICE *(1 - L_DISCOUNT)` 식은 특정 품목에 대한 할인 가격을 위한 수식입니다. 이러한 수식은 모듈 및 재사용의 장점을 활용할 수 있는 함수로 추출될 수 있습니다.

```sql
CREATE FUNCTION dbo.discount_price(@price DECIMAL(12,2), @discount DECIMAL(12,2)) 
RETURNS DECIMAL (12,2) AS
BEGIN
  RETURN @price * (1 - @discount);
END
```

이제 쿼리를 수정하여 이 UDF를 호출할 수 있습니다.

```sql
SELECT L_SHIPDATE, O_SHIPPRIORITY, SUM (dbo.discount_price(L_EXTENDEDPRICE, L_DISCOUNT)) 
FROM LINEITEM
INNER JOIN ORDERS
  ON O_ORDERKEY = L_ORDERKEY 
GROUP BY L_SHIPDATE, O_SHIPPRIORITY ORDER BY L_SHIPDATE
```

앞서 개략적으로 설명한 이유로 인해 UDF가 있는 쿼리는 성능이 떨어집니다. 이제 스칼라 UDF 인라인 처리를 통해 UDF 본문의 스칼라 식을 쿼리에서 직접 대체합니다. 이 쿼리를 실행한 결과는 아래 표에 있습니다.

| 쿼리: | UDF 없는 쿼리 | UDF 있는 쿼리(인라인 처리 없음) | 스칼라 UDF 인라인 처리가 있는 쿼리 | 
| --- | --- | --- | --- |
| 실행 시간: | 1.6초 | 29분 11초 | 1.6초 |

이러한 수치는 10GB CCI 데이터베이스(TPC-H 스키마 사용), 이중 프로세서 탑재 머신(12코어)에서 실행, 96GB RAM, SSD 지원을 기반으로 합니다. 이 값에는 콜드 프로시저 캐시 및 버퍼 풀을 통한 컴파일 및 실행 시간이 포함됩니다. 기본 구성을 사용했으며 다른 인덱스는 만들지 않았습니다.

### <a name="example-2---multi-statement-scalar-udf"></a>예제 2 - 다중 문 스칼라 UDF
변수 할당, 조건 분기 등과 같이 여러 T-SQL 문을 통해 구현되는 스칼라 UDF도 인라인 처리가 가능합니다. 다음 스칼라 UDF는 고객 키가 주어지면 해당 고객에 대한 서비스 범주를 결정합니다. SQL 쿼리를 사용하여 고객이 수행한 모든 주문의 총 가격을 먼저 계산하여 범주에 도달합니다. 그런 다음, `IF (...) ELSE` 논리를 사용하여 총 가격을 기준으로 범주를 결정합니다.

```sql
CREATE OR ALTER FUNCTION dbo.customer_category(@ckey INT) 
RETURNS CHAR(10) AS
BEGIN
  DECLARE @total_price DECIMAL(18,2);
  DECLARE @category CHAR(10);

  SELECT @total_price = SUM(O_TOTALPRICE) FROM ORDERS WHERE O_CUSTKEY = @ckey;

  IF @total_price < 500000
    SET @category = 'REGULAR';
  ELSE IF @total_price < 1000000
    SET @category = 'GOLD';
  ELSE 
    SET @category = 'PLATINUM';

  RETURN @category;
END
```

이제 이 UDF를 호출하는 쿼리를 고려해 보겠습니다.

```sql
SELECT C_NAME, dbo.customer_category(C_CUSTKEY) FROM CUSTOMER;
```

[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]에서 이 쿼리의 실행 계획(호환성 수준 140 및 그 이전)은 다음과 같습니다.

![인라인 처리 없는 쿼리 계획](./media/query-plan-without-udf-inlining.png)

계획에서 보듯이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 간단한 전략을 택하고 있습니다. 즉 `CUSTOMER` 테이블의 모든 튜플에 대해 UDF를 호출하고 결과를 출력합니다. 이 전략은 단순하고 비효율적입니다. 인라인 처리가 있으면 이런 UDF가 해당하는 스칼라 하위 쿼리로 변환되며 호출하는 쿼리에서 UDF 대신 대체됩니다.

동일한 쿼리에 대해 인라인 처리된 UDF가 있는 계획은 다음과 같습니다.

![인라인 처리 있는 쿼리 계획](./media/query-plan-with-udf-inlining.png)

앞서 설명한 것처럼 쿼리 계획에는 이제 사용자 정의 함수 연산자가 없으나 그 영향은 계획의 보기나 인라인 TVF 등에서 확인할 수 있습니다. 위의 계획에서 몇 가지 주요 확인 사항은 다음과 같습니다.

-  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `CUSTOMER` 및 `ORDERS` 간의 암시적 조인을 추론하며 조인 연산자를 통해 명시적으로 설정했습니다.
-  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]도 암시적 `GROUP BY O_CUSTKEY on ORDERS`를 추론하며 IndexSpool + StreamAggregate를 사용하여 구현합니다.
-  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이제 모든 연산자에서 병렬 처리를 사용하고 있습니다.

UDF의 논리 복잡성에 따라 결과적인 쿼리 계획이 더 크고 복잡할 수도 있습니다. 여기서 보듯이 UDF 내 연산은 더 이상 블랙 박스가 아니므로 쿼리 최적화 프로그램이 해당 연산을 희생하고 최적화할 수 있습니다. 또한 UDF가 더 이상 계획에 없으므로 반복 UDF 호출이 함수 호출 과부하를 완전히 방지하는 계획으로 바뀝니다.

## <a name="inlineable-scalar-udfs-requirements"></a>인라인 처리 가능한 스칼라 UDF 요구 사항
<a name="requirements"></a> 다음 조건을 모두 만족하는 스칼라 T-SQL UDF를 인라인 처리할 수 있습니다.

- UDF는 다음 구문을 사용하여 작성됩니다.
    - `DECLARE`, `SET`: 변수 선언 및 할당.
    - `SELECT`: 단일/다중 변수 할당이 있는 SQL 쿼리<sup>1</sup>.
    - `IF`/`ELSE`: 임의 수준의 중첩이 있는 분기.
    - `RETURN`: 단일 또는 여러 return 문.
    - `UDF`: 중첩/재귀 함수 호출<sup>2</sup>.
    - 기타: 관계형 연산(예: `EXISTS`, `ISNULL`).
- UDF는 시간 종속적이거나(예: `GETDATE()`) 부작용이 있는<sup>3</sup>(예: `NEWSEQUENTIALID()`) 내장 함수를 호출하지 않습니다.
- UDF는 `EXECUTE AS CALLER` 절을 사용합니다(`EXECUTE AS` 절을 지정하지 않은 경우 기본 동작).
- UDF는 테이블 변수나 테이블 값 매개 변수를 참조하지 않습니다.
- 스칼라 UDF를 호출하는 쿼리는 `GROUP BY` 절에서 스칼라 UDF 호출을 참조하지 않습니다.
- `DISTINCT` 절을 사용한 선택 목록에서 스칼라 UDF를 호출하는 쿼리는 `ORDER BY` 절이 없습니다.
- UDF는 `ORDER BY` 절에서 사용되지 않습니다.
- UDF는 원시적으로 컴파일됩니다(호환성 지원).
- UDF는 계산된 열 또는 제약 조건 확인 정의에서 사용되지 않습니다.
- UDF는 사용자 정의 형식을 참조하지 않습니다.
- UDF에 추가되는 서명은 없습니다.
- UDF는 파티션 함수가 아닙니다.
- UDF에는 CTE(공용 테이블 식)에 대한 참조가 포함되지 않습니다.

<sup>1</sup> `SELECT`(변수 누적/집계 있음, 예: `SELECT @val += col1 FROM table1`)는 인라인 처리에 지원되지 않습니다.

<sup>2</sup> 재귀 UDF는 특정 깊이에만 인라인 처리됩니다.

<sup>3</sup> 현재 시스템 시간에 따라 결과가 달라지는 내장 함수는 시간 종속입니다. 부작용이 있는 함수의 예로 일부 내부 글로벌 상태를 업데이트할 수 있는 내장 함수를 들 수 있습니다. 이러한 함수는 내부 상태에 따라 호출될 때마다 다른 결과를 반환합니다.

### <a name="checking-whether-or-not-a-udf-can-be-inlined"></a>UDF를 인라인 처리할 수 있는지 여부를 확인합니다.
모든 T-SQL 스칼라 UDF에 대해 [sys.sql_modules](../system-catalog-views/sys-sql-modules-transact-sql.md) 카탈로그 보기에는 UDF의 인라인 처리 가능 여부를 표시하는 `is_inlineable`이라는 속성이 포함되어 있습니다. 

> [!NOTE]
> `is_inlineable` 속성은 UDF 정의 내에 있는 구성에서 파생됩니다. UDF가 실제로 컴파일 타임에 인라인 처리가 가능한지 여부는 확인하지 않습니다. 자세한 내용은 아래의 [인라인 처리를 위한 조건](#requirements)을 참조하세요.

1 값은 인라인 처리 가능, 0은 그 반대를 나타냅니다. 이 속성은 모든 인라인 TVF에 대해 1 값을 갖습니다. 다른 모든 모듈에 대해서는 값이 0입니다.

스칼라 UDF를 인라인 처리할 수 있는 경우 항상 인라인 처리가 된다는 뜻은 아닙니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 UDF를 인라인 처리할지 여부를 결정합니다(쿼리 및 UDF별 기준). UDF를 인라인 처리할 수 없는 몇 가지 예는 다음과 같습니다.

-  UDF 정의가 수천 줄의 코드로 실행되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 이를 인라인 처리하지 않도록 선택할 수 있습니다. 
-  `GROUP BY` 절의 UDF 호출은 인라인 처리되지 않습니다. 스칼라 UDF를 참조하는 쿼리가 컴파일될 때 이 결정을 수행합니다.
-  UDF가 인증서로 서명된 경우 UDF를 만든 후에 서명을 추가하거나 삭제할 수 있으므로 스칼라 UDF를 참조하는 쿼리를 컴파일할 때 인라인으로 할지 여부를 결정합니다. 예를 들어 시스템 함수는 일반적으로 인증서로 서명됩니다. [sys.crypt_properties](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)를 사용하여 서명된 개체를 찾을 수 있습니다. 

   ```sql
   SELECT * 
   FROM sys.crypt_properties AS cp
   INNER JOIN sys.objects AS o ON cp.major_id = o.object_id;
   ```

### <a name="checking-whether-inlining-has-happened-or-not"></a>인라인 처리의 발생 여부 확인
모든 사전 조건을 충족하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 인라인 처리를 수행하기로 결정한 경우 UDF를 관계형 식으로 변환합니다. 쿼리 계획에서는 인라인 처리의 발생 여부를 확인하기 쉽습니다.

- 계획 xml에는 성공적으로 인라인 처리된 UDF에 대한 `<UserDefinedFunction>` xml 노드가 없습니다. 
- 특정 Xevent는 내보냅니다.

## <a name="enabling-scalar-udf-inlining"></a>스칼라 UDF 인라인 처리 사용
데이터베이스에 대해 호환성 수준 150을 사용하도록 설정하여 워크로드가 스칼라 UDF 인라인 처리에 자동으로 적합하도록 만들 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 설정할 수 있습니다. 다음은 그 예입니다.  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 150;
```

이와는 별도로 이 기능을 활용하기 위해 UDF나 쿼리에 다른 변경이 필요하지 않습니다.

## <a name="disabling-scalar-udf-inlining-without-changing-the-compatibility-level"></a>호환성 수준 변경 없이 스칼라 UDF 인라인 처리 사용 안 함
데이터베이스 호환성 수준 150 이상을 유지하면서 데이터베이스, 문 또는 UDF 범위에서 스칼라 UDF 인라인 처리를 사용하지 않게 설정할 수 있습니다. 데이터베이스 범위에서 스칼라 UDF 인라인 처리를 사용하지 않으려면 해당하는 데이터베이스의 컨텍스트 안에서 다음 명령문을 실행합니다. 

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF;
```

데이터베이스에 대해 스칼라 UDF 인라인 처리를 다시 사용하려면 해당하는 데이터베이스의 컨텍스트 안에서 다음 명령문을 실행합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = ON;
```

ON이면 이 설정은 [`sys.database_scoped_configurations`](../system-catalog-views/sys-database-scoped-configurations-transact-sql.md)에서 사용하는 것으로 표시됩니다. `DISABLE_TSQL_SCALAR_UDF_INLINING`을 `USE HINT` 쿼리 힌트로 지정하여 특정 쿼리에 대해 스칼라 UDF 인라인 처리를 사용하지 않게 설정할 수도 있습니다. 다음은 그 예입니다.

```sql
SELECT L_SHIPDATE, O_SHIPPRIORITY, SUM (dbo.discount_price(L_EXTENDEDPRICE, L_DISCOUNT)) 
FROM LINEITEM
INNER JOIN ORDERS
  ON O_ORDERKEY = L_ORDERKEY 
GROUP BY L_SHIPDATE, O_SHIPPRIORITY ORDER BY L_SHIPDATE
OPTION (USE HINT('DISABLE_TSQL_SCALAR_UDF_INLINING'));
```

`USE HINT` 쿼리 힌트는 데이터베이스 범위 구성 또는 호환성 수준 설정보다 우선합니다.

`CREATE FUNCTION` 또는 `ALTER FUNCTION` 문에서 INLINE 절을 사용하는 특정 UDF에서는 스칼라 UDF 인라인 처리를 사용하지 않도록 설정할 수 있습니다.
다음은 그 예입니다.

```sql
CREATE OR ALTER FUNCTION dbo.discount_price(@price DECIMAL(12,2), @discount DECIMAL(12,2))
RETURNS DECIMAL (12,2)
WITH INLINE = OFF
AS
BEGIN
    RETURN @price * (1 - @discount);
END;
```

위의 문이 실행된 후에는 이 UDF가 이를 호출하는 어떤 쿼리에도 인라인 처리되지 않습니다. 이 UDF에 인라인 처리를 다시 사용하려면 다음 명령문을 실행합니다.

```sql
CREATE OR ALTER FUNCTION dbo.discount_price(@price DECIMAL(12,2), @discount DECIMAL(12,2))
RETURNS DECIMAL (12,2)
WITH INLINE = ON
AS
BEGIN
    RETURN @price * (1 - @discount);
END
```

> [!NOTE]
> `INLINE` 절은 필수 항목이 아닙니다. `INLINE` 절을 지정하지 않으면 UDF가 인라인 처리 가능한지 여부에 따라 `ON`/`OFF`로 자동으로 설정됩니다. `INLINE = ON`이 지정되었지만 UDF가 인라인 처리에 해당하지 않는 것으로 확인되면 오류가 throw됩니다.

## <a name="important-notes"></a>중요 사항
이 문서에서 설명한 것처럼 스칼라 UDF 인라인 처리는 스칼라 UDF가 있는 쿼리를 동급 스칼라 하위 쿼리가 있는 쿼리로 변환합니다. 이 변환으로 인해 다음 시나리오에서는 일부 작동의 차이가 확인될 수 있습니다.

1. 인라인 처리가 동일한 쿼리 텍스트에 대해 다른 쿼리 해시를 초래합니다.
1. 이 전에 숨겨졌을 수 있는 UDF 내 문의 특정 경고(예: 0으로 나누기 등)가 인라인 처리로 인해 드러날 수 있습니다.
1. 인라인 처리에는 새 조인이 들어가므로 쿼리 수준 조인 힌트가 더 이상 유효하지 않을 수 있습니다. 로컬 조인 힌트를 대신 사용해야 합니다.
1. 인라인 스칼라 UDF를 참조하는 보기를 인덱싱할 수 없습니다. 이런 보기에 대해 인덱스를 만들려면 참조된 UDF에 대해 인라인 처리를 사용하지 않습니다.
1. UDF 인라인 처리에서 [동적 데이터 마스킹](../security/dynamic-data-masking.md)의 동작에 차이가 있을 수 있습니다. (UDF의 논리에 따라) 특정 상황에서는 인라인 처리가 w.r.t 마스킹 출력 열보다 더 보수적일 수 있습니다. UDF에서 참조하는 열이 출력 열이 아닌 시나리오에서는 마스킹되지 않습니다. 
1. UDF가 기본 제공 함수(예: `SCOPE_IDENTITY()`, `@@ROWCOUNT` 또는 `@@ERROR`)를 참조할 경우 기본 제공 함수에서 반환한 값이 인라인 처리에 따라 변경됩니다. 이 동작 변경은 인라인 처리가 UDF 내 문 범위를 변경하기 때문입니다.

## <a name="see-also"></a>참고 항목
[SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대한 성능 센터](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md)     
[실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)     
[조인](../../relational-databases/performance/joins.md)     
[지능형 쿼리 처리 시연](https://aka.ms/IQPDemos)      
