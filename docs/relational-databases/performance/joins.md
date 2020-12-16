---
title: 조인(SQL Server) | Microsoft Docs
description: SQL Server에서 사용하는 조인 작업의 유형에 대해 알아봅니다. SQL Server는 조인 작업을 사용하여 세로 테이블 분할 또는 열 형식 스토리지를 지원합니다.
ms.custom: ''
ms.date: 07/19/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- HASH join
- NESTED LOOPS join
- MERGE join
- ADAPTIVE join
- joins [SQL Server], about joins
- join hints [SQL Server]
ms.assetid: bfc97632-c14c-4768-9dc5-a9c512f4b2bd
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f85260ea8ba17e6d4ceef4f07eded1c20775ea4d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463284"
---
# <a name="joins-sql-server"></a>조인(SQL Server)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 메모리 내 정렬 및 해시 조인 기술을 사용하여 정렬, 교집합, 합집합 및 차집합 연산을 수행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이러한 유형의 쿼리 계획을 사용하여 수직 테이블 분할을 지원합니다.   

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문에서 결정한 논리적 조인 작업을 구현합니다.
-   내부 조인
-   왼쪽 우선 외부 조인
-   오른쪽 우선 외부 조인
-   완전 외부 조인
-   크로스 조인

> [!NOTE]
> 조인 구문에 대한 자세한 내용은 [FROM 절과 JOIN, APPLY, PIVOT(Transact-SQL)](../../t-sql/queries/from-transact-sql.md)을 참조하세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 논리적 조인 작업을 수행하는 네 가지 유형의 물리적 조인 작업을 채택합니다.    
-   중첩 루프 조인     
-   병합 조인   
-   해시 조인   
-   적응 조인([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터)

## <a name="join-fundamentals"></a><a name="fundamentals"></a> 조인 기본 사항
조인을 사용하면 테이블 간의 논리적 관계를 기준으로 둘 이상의 테이블에서 데이터를 검색할 수 있습니다. 조인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 특정 테이블의 데이터를 사용하여 다른 테이블의 행을 선택하는 방법을 나타냅니다.    

조인 조건은 다음과 같이 쿼리에서 두 테이블의 관계를 정의합니다.    
-   조인에 사용될 각 테이블에서 열을 지정합니다. 일반적으로 조인 조건은 한 테이블에서 외래 키를 지정하고 다른 테이블에서 이와 관련된 키를 지정합니다.    
-   열에서 값을 비교할 때 사용할 논리 연산자(예: =, <>)를 지정합니다.   

조인은 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문을 사용하여 논리적으로 표현됩니다.
-   INNER JOIN
-   LEFT [ OUTER ] JOIN
-   RIGHT [ OUTER ] JOIN
-   FULL [ OUTER ] JOIN
-   CROSS JOIN

**내부 조인** 은 `FROM` 또는 `WHERE` 절에서 지정할 수 있습니다. **외부 조인** 및 **크로스 조인** 은 `FROM` 절에서만 지정할 수 있습니다. `WHERE` 및 `HAVING` 검색 조건과 결합된 조인 조건은 `FROM` 절에서 참조되는 기본 테이블에서 선택된 행을 제어합니다.    

`FROM` 절에 조인 조건을 지정하면 `WHERE` 절에 지정할 수 있는 다른 검색 조건과 구분하기 쉬우므로 적합한 조인 지정 방법입니다. 간단한 ISO `FROM` 절의 조인 구문은 다음과 같습니다.

```
FROM first_table < join_type > second_table [ ON ( join_condition ) ]
```

*join_type* 는 어떤 유형의 조인을 실행할지 지정합니다. 조인 유형에는 내부 조인, 외부 조인, 크로스 조인이 있습니다. *join_condition* 은 조인된 행의 각 쌍에 대해 평가할 조건자를 정의합니다. 다음은 `FROM` 절 조인 사양의 예제입니다.

```sql
FROM Purchasing.ProductVendor INNER JOIN Purchasing.Vendor
     ON ( ProductVendor.BusinessEntityID = Vendor.BusinessEntityID )
```

다음은 위의 조인을 사용하는 간단한 `SELECT` 문입니다.

```sql
SELECT ProductID, Purchasing.Vendor.BusinessEntityID, Name
FROM Purchasing.ProductVendor INNER JOIN Purchasing.Vendor
    ON (Purchasing.ProductVendor.BusinessEntityID = Purchasing.Vendor.BusinessEntityID)
WHERE StandardPrice > $10
  AND Name LIKE N'F%'
GO
```

위의 `SELECT` 문은 회사 이름이 F로 시작하고 제품 가격이 $10 이상인 회사에서 공급되는 부품 조합에 대해 제품과 공급업체 정보를 반환합니다.   

하나의 쿼리에서 여러 테이블이 참조될 경우 모든 열 참조는 명확해야 합니다. 위의 예제에서 `ProductVendor` 및 `Vendor` 테이블에 모두 `BusinessEntityID`라는 열이 있습니다. 쿼리에서 참조되는 둘 이상의 테이블 간에 중복된 열 이름이 있으면 테이블 이름으로 한정해야 합니다. 예제에서 `Vendor` 열에 대한 모든 참조는 한정됩니다.   

쿼리에 사용된 둘 이상의 테이블에서 열 이름이 중복되지 않을 경우 해당 열에 대한 참조를 테이블 이름으로 한정할 필요가 없습니다. 위의 예에도 이러한 열이 포함되어 있습니다. 이러한 `SELECT` 절은 각 열을 제공하는 테이블을 나타내지 않기 때문에 이해하기 어려울 수도 있습니다. 모든 열이 테이블 이름으로 한정되면 쿼리의 가독성이 향상됩니다. 테이블 별칭을 사용하면 가독성이 더욱 향상되며 특히 테이블 이름을 데이터베이스 이름과 소유자 이름으로 한정해야 할 경우 그러합니다. 다음은 가독성 향상을 위해 테이블 별칭이 할당되고 열이 테이블 별칭으로 한정된 것을 제외하면 위 예와 동일합니다.

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv 
INNER JOIN Purchasing.Vendor AS v
    ON (pv.BusinessEntityID = v.BusinessEntityID)
WHERE StandardPrice > $10
    AND Name LIKE N'F%';
```

위의 예제는 일반적으로 사용되는 방법대로 조인 조건을 `FROM` 절에 지정했습니다. 다음은 동일한 조인 조건을 `WHERE` 절에 지정한 쿼리입니다.

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv, Purchasing.Vendor AS v
WHERE pv.BusinessEntityID=v.BusinessEntityID
    AND StandardPrice > $10
    AND Name LIKE N'F%';
```

조인의 `SELECT` 목록은 조인된 테이블의 모든 열이나 이러한 열의 하위 집합을 참조할 수 있습니다. 모든 테이블의 열을 조인에 포함하는 데 `SELECT` 목록은 필요하지 않습니다. 예를 들면 세 개의 테이블 조인에서 한 테이블만 사용하여 다른 한 테이블을 세 번째 테이블과 연결하고 중간 테이블의 열은 선택 목록에서 참조되지 않아도 됩니다. 이를 **anti semi join** 이라고도 합니다.  

조인 조건에는 일반적으로 같음 연산자(=)를 사용하지만 다른 조건자처럼 기타 비교 연산자나 관계 연산자를 지정할 수 있습니다. 자세한 내용은 [Comparison Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md) 및 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)를 참조하세요.  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 조인을 처리할 때 쿼리 최적화 프로그램은 여러 가지 가능한 방법 중 가장 효율적인 방법을 선택합니다. 여기에는 가장 효율적인 유형의 물리적 조인 선택, 테이블이 조인되는 순서, **semi join** 및 **anti semi join** 과 같이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문으로 직접 표현할 수 없는 논리적 조인 작업 유형 사용이 포함됩니다. 다양한 조인의 물리적 실행에서는 다양한 최적화가 사용될 수 있으므로 이에 대해 신뢰할 수 있는 예측은 수행할 수 없습니다. semi join 및 anti semi join에 대한 자세한 내용은 [실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)를 확인하세요.  

조인 조건에 사용된 열의 이름이나 데이터 형식은 반드시 동일하지 않아도 됩니다. 그러나 데이터 형식이 다를 경우 서로 호환이 가능하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 암시적으로 변환할 수 있는 형식이어야 합니다. 데이터 형식을 암시적으로 변환할 수 없을 경우 조인 조건은 `CAST` 함수를 사용하여 데이터 형식을 명시적으로 변환해야 합니다. 암시적 및 명시적 데이터 변환에 대한 자세한 내용은 [데이터 형식 변환&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)을 참조하세요.    

조인을 사용하는 대부분의 쿼리는 하위 쿼리(다른 쿼리 내에 중첩된 쿼리)를 사용하여 다시 작성할 수 있으며 대부분의 하위 쿼리는 조인으로 다시 작성할 수 있습니다. 하위 쿼리에 대한 자세한 내용은 [Subqueries](../../relational-databases/performance/subqueries.md)를 참조하세요.   

> [!NOTE]
> ntext, text 또는 image 열에서는 테이블을 직접 조인할 수 없습니다. 하지만 ntext, text 또는 image 열에서 `SUBSTRING`을 사용하여 테이블을 간접적으로 조인할 수 있습니다.    
> 예를 들어 `SELECT * FROM t1 JOIN t2 ON SUBSTRING(t1.textcolumn, 1, 20) = SUBSTRING(t2.textcolumn, 1, 20)`은 t1 및 t2 테이블에 있는 각 텍스트 열의 처음 20자에 두 개의 테이블 내부 조인을 수행합니다.   
> 또한 두 테이블의 ntext 또는 text 열을 비교할 수 있는 다른 방법으로는 `WHERE` 절로 열의 길이를 비교하는 것입니다. 예:`WHERE DATALENGTH(p1.pr_info) = DATALENGTH(p2.pr_info)`

## <a name="understanding-nested-loops-joins"></a><a name="nested_loops"></a> 중첩 루프 조인 이해
한 조인 입력은 작고(행이 10개 미만) 다른 조인 입력은 아주 크며 조인 열에 인덱스가 지정된 경우에는 I/O와 비교 작업이 가장 적은 인덱스 중첩 루프 조인이 가장 빠른 조인 연산입니다. 

*중첩 반복* 이라고도 하는 중첩 루프 조인은 조인 입력 한 개를 외부 입력 테이블(그래픽 실행 계획에서 최상위 입력으로 표시됨)로 사용하고 한 개는 내부(최하위) 입력 테이블로 사용합니다. 외부 루프는 외부 입력 테이블에서 한 번에 한 행씩 입력받아 처리합니다. 각 외부 행에 대해 실행되는 내부 루프는 외부 테이블의 행과 일치하는 내부 입력 테이블의 행을 검색합니다.   

가장 간단하게 전체 테이블 또는 인덱스를 검색하는 경우를 *원시 중첩 루프 조인* 이라고 합니다. 검색에서 인덱스를 사용하는 경우에는 *인덱스 중첩 루프 조인* 이라고 합니다. 인덱스가 쿼리 계획의 일부로 작성되고 쿼리 완료와 동시에 삭제되는 경우에는 *임시 인덱스 중첩 루프 조인* 이라고 합니다. 어떤 방식을 사용할 것인지는 쿼리 최적화 프로그램에 의해 고려됩니다.   

외부 입력은 작고 내부 입력은 크며 미리 인덱스가 정해져 있는 경우 중첩 루프 조인이 상당히 효과적입니다. 작은 행 집합에만 영향을 주는 일반적인 소규모 트랜잭션의 경우 인덱스 중첩 루프 조인이 병합 조인이나 해시 조인보다 훨씬 우수합니다. 그러나 크기가 큰 쿼리에서는 중첩 루프 조인이 최적의 선택이 아닌 경우도 많습니다.    

중첩 루프의 조인 연산자의 OPTIMIZED 특성이 **True** 로 설정되면 최적화된 중첩 루프(또는 일괄 처리 정렬)가 내부 쪽 테이블이 클 때 평행화 여부에 상관없이 I/O를 최소화하는 데 사용됨을 의미합니다. 정렬 자체가 숨겨진 작업임을 고려하면, 지정된 계획에서 이 최적화의 존재는 실행 계획을 분석할 때 아주 명백하지 않을 수 있습니다. 그러나 OPTIMIZED 특성에 대한 계획 XML을 살펴보면, 이는 중첩 루프 조인이 I/O 성능을 향상시키기 위해 입력 행을 다시 정렬하려고 함을 나타냅니다.

## <a name="understanding-merge-joins"></a><a name="merge"></a> 병합 조인 이해
두 조인 입력이 작지는 않지만 해당 조인 열을 기준으로 정렬되는 경우(예: 정렬된 인덱스 검색으로 가져온 경우)에는 병합 조인이 가장 빠른 조인 연산입니다. 두 조인 입력이 모두 크고 비슷한 크기인 경우에는 사전 정렬이 포함된 병합 조인과 해시 조인이 비슷한 성능을 제공합니다. 그러나 두 입력의 크기가 서로 많이 다를 때는 해시 조인 연산이 더 빠른 경우가 많습니다.       

병합 조인에서는 두 입력이 모두 조인 조건자의 등가(ON) 절로 정의되는 병합 열에서 정렬되어야 합니다. 쿼리 최적화 프로그램은 일반적으로 인덱스를 검색하거나(인덱스가 적절한 열 집합에 있는 경우) 병합 조인 아래에 정렬 연산자를 배치합니다. 간혹 여러 개의 등가 절이 있는 경우도 있지만 사용 가능한 등가 절에서만 병합 열을 가져옵니다.    

각 입력이 정렬되므로 **Merge Join** 연산자는 각 입력으로부터 행을 가져와서 비교합니다. 예를 들어 내부 조인 작업에 대해서는 행이 동일한 경우 반환됩니다. 행이 동일하지 않으면 값이 더 낮은 행이 무시되고 해당 입력으로부터 다른 행을 가져옵니다. 모든 행이 처리될 때까지 이 과정이 반복됩니다.    

병합 조인 작업은 일반 또는 다 대 다 작업이 될 수 있습니다. 다 대 다 병합 조인에서는 임시 테이블을 사용하여 행을 저장합니다. 각 입력으로부터 중복 값이 있으면 그 중 하나의 입력을 다른 입력으로부터 각각의 중복이 처리될 때 중복의 시작 부분까지 되감아야 합니다.    

잔여 조건자가 있는 경우에는 병합 조건자에 부합되는 모든 행이 잔여 조건자를 평가하고 그 조건자에 부합되는 행만 반환됩니다.   

병합 조인 자체는 매우 빠르지만 정렬 작업이 필요한 경우에는 비용이 많이 드는 방법이 될 수 있습니다. 그러나 데이터 볼륨이 크고 원하는 데이터를 기존의 B-트리 인덱스로부터 미리 정렬된 상태로 가져올 수 있는 경우에는 주로 병합 조인이 사용 가능한 조인 알고리즘 중 가장 빠른 조인이 됩니다.    

## <a name="understanding-hash-joins"></a><a name="hash"></a> 해시 조인 이해
해시 조인은 크고 정렬되지 않았으며 인덱싱되지 않은 입력을 효율적으로 처리할 수 있습니다. 해시 조인이 복잡한 쿼리의 중간 결과에 유용한 이유는 다음과 같습니다.
-   디스크에 명시적으로 저장한 다음 인덱싱하지 않는 한 중간 결과는 인덱싱되지 않으며 쿼리 계획의 다음 작업을 위해 적절히 정렬되지 않는 경우가 많습니다.
-   쿼리 최적화 프로그램은 중간 결과 크기만을 예상합니다. 복잡한 쿼리에서는 예상이 크게 잘못될 수 있으므로 중간 결과를 처리하기 위한 알고리즘은 효율적이어야 할 뿐 아니라 중간 결과가 예상보다 훨씬 큰 것으로 확인되는 경우 적절히 하향 조정되어야 합니다.   

해시 조인을 사용하면 비정규화 사용을 줄일 수 있습니다. 비정규화는 대체로 중복(예: 일관성 없는 업데이트)의 위험에도 불구하고 조인 연산을 줄여 보다 나은 성능을 얻기 위해 사용됩니다. 해시 조인은 비정규화의 필요성을 줄여 줍니다. 해시 조인을 사용하면 별개의 파일 또는 인덱스에 있는 단일 테이블의 열 그룹을 나타내는 수직 분할이 물리적 데이터베이스 디자인에 유용한 옵션이 될 수 있습니다.     

해시 조인에는 **빌드** 입력 및 **프로브** 입력 등 두 가지 입력이 있습니다. 쿼리 최적화 프로그램은 두 가지 입력 중 작은 쪽이 빌드 입력이 될 수 있도록 이러한 역할을 할당합니다.    

해시 조인은 여러 가지 유형의 집합 일치 연산, 즉 내부 조인, 왼쪽, 오른쪽, 완전 외부 조인, 왼쪽 및 오른쪽 세미 조인, 교집합, 합집합, 차집합 등에 사용합니다. 또한, 해시 조인의 변형은 중복 요소 제거 및 그룹화(예: `SUM(salary) GROUP BY department`)를 수행할 수 있습니다. 이러한 수정에서는 빌드 및 검색 역할 모두에 대해 한 개의 입력만 사용합니다.   

다음 섹션에서는 인-메모리 해시 조인, 유예 해시 조인 및 재귀 해시 조인 등 여러 해시 조인 유형을 설명합니다.    

### <a name="in-memory-hash-join"></a><a name="inmem_hash"></a> 인-메모리 해시 조인
해시 조인은 먼저 전체 빌드 입력을 스캔하거나 계산한 다음 해시 테이블을 메모리에 작성합니다. 해시 키에 대해 계산된 해시 값에 따라 각 행이 해시 버킷에 삽입됩니다. 전체 빌드 입력이 사용 가능한 메모리보다 작으면 모든 행을 해시 테이블에 삽입할 수 있습니다. 이 빌드 단계 다음으로는 검색 단계가 이어집니다. 전체 검색 입력은 한 번에 한 행씩 스캔 또는 계산되며, 각 검색 행에 대해 해시 키 값이 계산되고 해당 해시 버킷이 스캔되며 일치하는 항목이 생성됩니다.    

### <a name="grace-hash-join"></a><a name="grace_hash"></a> 유예 해시 조인
빌드 입력이 메모리 크기에 맞지 않으면 해시 조인은 몇 개의 단계로 진행됩니다. 이것을 유예 해시 조인이라고 합니다. 각 단계마다 빌드 단계와 검색 단계가 있습니다. 처음에는 전체 빌드 및 검색 입력이 사용되며 해시 키에 대한 해시 함수를 사용하여 여러 파일로 분할됩니다. 해시 키에 대한 해시 함수를 사용하면 2개의 조인 레코드가 모두 동일한 파일 쌍에 있는 것이 보장됩니다. 따라서 2개의 큰 입력을 조인하는 태스크가 동일한 작업의 여러 개의 작은 인스턴스로 축소되었습니다. 그런 다음 해시 조인은 분할된 파일의 각 쌍에 적용됩니다.    

### <a name="recursive-hash-join"></a><a name="recursive_hash"></a> 재귀 해시 조인
빌드 입력이 너무 커서 표준 외부 병합에 대한 입력에 여러 개의 병합 수준이 필요한 경우에는 여러 개의 분할 단계와 여러 개의 분할 수준이 요구됩니다. 일부 파티션만 큰 경우에는 해당 파티션에서만 추가 분할 단계가 사용됩니다. 모든 분할 단계를 가능한 한 빠르게 유지하기 위해서는 단일 스레드가 여러 개의 디스크 드라이브를 사용 중인 상태로 유지할 수 있도록 대형의 비동기 I/O 작업이 사용됩니다.    

> [!NOTE]
> 빌드 입력이 사용 가능한 메모리보다 조금밖에 크지 않다면 인-메모리 해시 조인과 유예 해시 조인의 요소가 단일 단계에서 결합되어 하이브리드 해시 조인이 생성됩니다.   

최적화 중에 사용될 해시 조인을 확인하는 것이 항상 가능한 것은 아닙니다. 따라서 SQL Server는 빌드 입력의 크기에 따라 인-메모리 해시 조인을 사용하여 시작된 후 유예 해시 조인, 재귀 해시 조인으로 점차 전환됩니다.    

2개의 입력 중 빌드 입력이 되어야 하는 작은 쪽을 쿼리 최적화 프로그램이 잘못 예측하는 경우에는 빌드 및 검색 역할이 동적으로 바뀝니다. 해시 조인은 작은 쪽의 오버플로 파일을 빌드 입력으로 사용하게 합니다. 이 기술을 역할 전환이라고 합니다. 역할 반전은 하나 이상의 해시 조인이 디스크에 "spill"된 경우 해시 조인 내에서 발생합니다.     

> [!NOTE]
> 역할 반전은 모든 쿼리 참고 또는 구조와 관계없이 발생합니다. 역할 반전은 쿼리 계획에 나타나지 않습니다. 역할 반전이 발생하면 사용자는 인식하지 못합니다.

### <a name="hash-bailout"></a><a name="hash_bailout"></a> 해시 재귀 한도 초과
해시 재귀 한도 초과라는 용어는 경우에 따라 유예 해시 조인 또는 재귀 해시 조인을 설명하는 데 사용됩니다.    

> [!NOTE]
> 재귀 해시 조인 또는 해시 재귀 한도 초과는 서버 성능을 저하시킵니다. 추적에서 해시 경고 이벤트가 많이 발견되면 조인되는 열의 통계를 업데이트하십시오.    

해시 재귀 한도 초과에 대한 자세한 내용은 [해시 경고 이벤트 클래스](../../relational-databases/event-classes/hash-warning-event-class.md)를 참조하세요.    

## <a name="understanding-adaptive-joins"></a><a name="adaptive"></a> 적응 조인 이해
[일괄 처리 모드](../../relational-databases/query-processing-architecture-guide.md#batch-mode-execution) 적응 조인을 사용하면 [해시 조인](#hash) 또는 [중첩 루프](#nested_loops) 조인 메서드 선택을 첫 번째 입력이 검사된 **후** 까지 지연할 수 있습니다. 적응 조인 연산자는 중첩된 루프 계획으로 전환할 시기를 결정하는 데 사용되는 임계값을 정의합니다. 따라서 쿼리 계획을 다시 컴파일하지 않고도 실행 중에 더 나은 조인 전략으로 동적으로 전환할 수 있습니다. 

> [!TIP]
> 작은 조인 입력 검색과 큰 조인 입력 검색 간에 자주 변동하는 워크로드가 이 기능에서 가장 큰 혜택을 받게 됩니다.

런타임은 다음 단계에 따라 결정됩니다.
-  중첩 루프 조인이 해시 조인보다 적합할 만큼 빌드 조인 입력의 행 수가 충분히 적으면 계획이 중첩 루프 알고리즘으로 전환됩니다.
-  빌드 조인 입력이 특정 행 수 임계값을 초과하면 전환이 발생하지 않으며 계획이 해시 조인을 계속 사용합니다.

다음 쿼리는 적응 조인 예제를 설명하기 위해 사용됩니다.

```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 360;
```

이 쿼리는 336개의 행을 반환합니다. [활성 쿼리 통계](../../relational-databases/performance/live-query-statistics.md)를 사용하도록 설정하면 다음 계획이 표시됩니다.

![쿼리 결과 336개 행](../../relational-databases/performance/media/4_AQPStats336Rows.png)

계획에서 다음을 확인합니다.
1. 해시 조인 빌드 단계에 대한 행을 제공하는 데 columnstore 인덱스 검색이 사용됩니다.
2. 새 적응 조인 연산자입니다. 이 연산자는 중첩된 루프 계획으로 전환할 시기를 결정하는 데 사용되는 임계값을 정의합니다. 이 예제에서 임계값은 78개 행입니다. &gt;= 78개 행이면 모두 해시 조인을 사용합니다. 임계값보다 작으면 중첩 루프 조인이 사용됩니다.
3. 쿼리에서 336개 행을 반환하기 때문에 임계값을 초과하므로 두 번째 분기가 표준 해시 조인 작업의 프로브 단계를 나타냅니다. 활성 쿼리 통계는 연산자를 통과하는 행(이 경우 "672/672")을 보여줍니다.
4. 마지막 분기는 임계값을 초과하지 않을 경우 중첩 루프 조인에서 사용하기 위한 Clustered Index Seek입니다. "0/336"개 행이 표시됩니다(분기가 사용되지 않음).

이제 계획과 동일한 쿼리를 비교합니다. 하지만 *Quantity* 값이 테이블에 행이 하나만 있는 경우
 
```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 361;
```
쿼리가 하나의 행을 반환합니다. 활성 쿼리 통계를 사용하도록 설정하면 다음 계획이 표시됩니다.

![쿼리 결과 하나의 행](../../relational-databases/performance/media/5_AQPStatsOneRow.png)

계획에서 다음을 확인합니다.
- 하나의 행이 반환되면 이제 Clustered Index Seek에 통과하는 행이 있습니다.
- 해시 조인 빌드 단계를 계속 진행하지 않았으므로 두 번째 분기를 통해 흐르는 행이 없습니다.

### <a name="adaptive-join-remarks"></a>적응 조인 설명
적응 조인은 동등한 인덱스 중첩된 루프 조인 계획보다 메모리 요구 사항이 더 높습니다. 중첩 루프가 해시 조인인 것처럼 추가 메모리가 요청됩니다. 동등한 중첩된 루프 스트리밍 조인에 비해 스탑앤고(stop-and-go) 작업으로서 빌드 단계에 대한 오버헤드도 있습니다. 빌드 입력의 행 수가 변동될 수 있는 시나리오에서 해당 추가 비용과 함께 유연성이 제공됩니다.

일괄 처리 모드 적응 조인은 문의 초기 실행에서 작동하며, 컴파일된 후에는 컴파일된 적응 조인 임계값과 외부 입력의 빌드 단계를 통과하는 런타임 행에 따라 연속 실행이 적응 상태로 유지됩니다.

적응 조인이 중첩된 루프 작업으로 전환하는 경우 해시 조인 빌드에서 이미 읽은 행이 사용됩니다. 연산자는 외부 참조 행을 다시 읽지 **않습니다**.

### <a name="tracking-adaptive-join-activity"></a>적응 조인 작업 추적
적응 조인 연산자에는 다음과 같은 계획 연산자 특성이 있습니다.

|계획 특성|Description|
|---|---|
|AdaptiveThresholdRows|해시 조인에서 중첩된 루프 조인으로 전환하는 데 사용되는 임계값을 보여 줍니다.|
|EstimatedJoinType|가능한 조인 형식입니다.|
|ActualJoinType|실제 계획에서 임계값에 따라 최종적으로 선택된 조인 알고리즘을 보여 줍니다.|

예상 계획은 정의된 적응 조인 임계값 및 예상 조인 형식과 함께 적응 조인 계획 모양을 보여줍니다.

> [!TIP]
> 쿼리 저장소는 일괄 처리 모드 적응 조인 계획을 캡처하고 강제로 적용할 수 있습니다.

### <a name="adaptive-join-eligible-statements"></a>적응 조인 적합한 문
논리 조인을 일괄 처리 모드 적응 조인에 적합하게 만드는 몇 가지 조건은 다음과 같습니다.
- 데이터베이스 호환성 수준이 140 이상입니다.
- 쿼리가 `SELECT` 문입니다(데이터 수정 문은 현재 적합하지 않음).
- 인덱싱된 중첩 루프 조인 또는 해시 조인 실제 알고리즘 둘 다에서 조인을 실행할 수 있습니다.
- 해시 조인은 쿼리 전체의 Columnstore 인덱스 현재 상태를 통해 사용하도록 설정되거나, 조인에서 직접 참조되는 Columnstore 인덱싱된 테이블을 통해 사용하도록 설정되거나, [rowstore의 일괄 처리 모드](./intelligent-query-processing.md#batch-mode-on-rowstore)를 사용하여 활성화되는 일괄 처리 모드를 사용합니다.
- 중첩 루프 조인 및 해시 조인의 생성된 대체 솔루션에 동일한 첫 번째 자식(외부 참조)이 있어야 합니다.

### <a name="adaptive-threshold-rows"></a>적응 임계값 행
다음 차트에서는 해시 조인 비용과 중첩 루프 조인 대안 비용 간의 교차 예를 보여줍니다. 이 교차 지점에서 결정되는 임계값에 따라 다시 조인 작업에 사용되는 실제 알고리즘이 결정됩니다.

![조인 임계값](../../relational-databases/performance/media/6_AQPJoinThreshold.png)

### <a name="disabling-adaptive-joins-without-changing-the-compatibility-level"></a>호환성 수준을 변경하지 않고 적응형 조인 비활성화
데이터베이스 호환성 수준 140 이상을 유지하면서 데이터베이스 또는 명령문 범위에서 적응형 조인을 비활성화할 수 있습니다.  
데이터베이스에서 발생하는 모든 쿼리 실행에 대한 적응형 조인을 비활성화하려면 해당 데이터베이스의 컨텍스트 내에서 다음을 실행합니다.

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = ON;

-- Azure SQL Database, SQL Server 2019 and higher
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ADAPTIVE_JOINS = OFF;
```

활성화될 경우 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)에서 이 설정이 enabled로 표시됩니다.
데이터베이스에서 발생하는 모든 쿼리 실행에 대한 적응형 조인을 재활성화하려면 해당 데이터베이스의 컨텍스트 내에서 다음을 실행합니다.

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = OFF;

-- Azure SQL Database, SQL Server 2019 and higher
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ADAPTIVE_JOINS = ON;
```

또한 `DISABLE_BATCH_MODE_ADAPTIVE_JOINS`를 [USE HINT 쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint)로 지정하여 특정 쿼리에 대한 적응형 조인을 비활성화할 수 있습니다. 예를 들면 다음과 같습니다.

```sql
SELECT s.CustomerID,
       s.CustomerName,
       sc.CustomerCategoryName
FROM Sales.Customers AS s
LEFT OUTER JOIN Sales.CustomerCategories AS sc
       ON s.CustomerCategoryID = sc.CustomerCategoryID
OPTION (USE HINT('DISABLE_BATCH_MODE_ADAPTIVE_JOINS')); 
```

> [!NOTE]
> USE HINT 쿼리 힌트는 데이터베이스 범위 구성 또는 추적 플래그 설정보다 우선합니다. 

## <a name="null-values-and-joins"></a><a name="nulls_joins"></a> Null 값 및 조인
조인되는 테이블의 열에 Null 값이 있을 경우 Null 값은 서로 일치하지 않습니다. 조인되는 테이블 중 한 테이블의 열에 있는 Null 값은 외부 조인을 사용해야만 반환됩니다(`WHERE` 절이 Null 값을 배제하지 않을 경우).     

다음 두 테이블에는 조인에 포함되는 열에 모두 NULL이 있습니다.     

```
table1                          table2
a           b                   c            d
-------     ------              -------      ------
      1        one                 NULL         two
   NULL      three                    4        four
      4      join4
```    

c 열에 대해 a 열의 값을 비교하는 조인은 NULL 값을 가진 열에서는 일치하는 행이 없습니다.

```sql
SELECT *
FROM table1 t1 JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```  

a 열과 c 열에서 값이 4인 한 행만 반환됩니다.

```
a           b      c           d      
----------- ------ ----------- ------ 
4           join4  4           four   

(1 row(s) affected)
```   

기본 테이블에서 반환되는 Null 값은 외부 조인에서 반환되는 Null 값과 구분하기가 어렵습니다. 예를 들어 다음 `SELECT` 문은 위의 두 테이블에 대해 왼쪽 우선 외부 조인을 수행합니다.   

```sql
SELECT *
FROM table1 t1 LEFT OUTER JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```   

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]   

```
a           b      c           d      
----------- ------ ----------- ------ 
NULL        three  NULL        NULL 
1           one    NULL        NULL 
4           join4  4           four   

(3 row(s) affected)
```   

위의 결과에서 데이터에 포함된 NULL과 조인 실패를 나타내는 NULL을 구분하기가 어렵습니다. 조인되는 데이터에 Null 값이 있으면 일반 조인을 사용하여 이를 결과에서 제외하는 것이 좋습니다.    

## <a name="see-also"></a>참고 항목  
[실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)     
[비교 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)    
[데이터 형식 변환&#40;Database Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
[Subqueries](../../relational-databases/performance/subqueries.md)      
[적응 조인](../../relational-databases/performance/intelligent-query-processing.md#batch-mode-adaptive-joins)    
[FROM 절과 JOIN, APPLY, PIVOT(Transact-SQL)](../../t-sql/queries/from-transact-sql.md)
