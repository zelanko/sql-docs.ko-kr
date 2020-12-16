---
description: PolyBase의 푸시다운 계산
title: PolyBase의 푸시다운 계산 | Microsoft Docs
dexcription: Enable pushdown computation to improve performance of queries on your Hadoop cluster. You can select a subset of rows/columns in an external table for pushdown.
ms.date: 11/17/2020
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016'
ms.openlocfilehash: 844ab3f2a13e2bd5a9e3ea26d41012a51e7329a4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97416617"
---
# <a name="pushdown-computations-in-polybase"></a>PolyBase의 푸시다운 계산

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

푸시다운 계산은 외부 데이터 원본의 쿼리 성능을 향상합니다. SQL Server 2016부터 Hadoop 외부 데이터 원본에 대한 푸시다운 계산을 사용할 수 있었습니다. SQL Server 2019에는 다른 형식의 외부 데이터 원본에 대한 푸시다운 계산이 도입되었습니다.

## <a name="enable-pushdown-computation"></a> 푸시다운 계산 사용

다음 문서에는 특정 형식의 외부 데이터 원본에 대한 푸시다운 계산 구성과 관련된 정보가 포함됩니다.

- [Hadoop에서 푸시다운 계산 사용](polybase-configure-hadoop.md#pushdown)
- [Oracle의 외부 데이터에 액세스하도록 PolyBase 구성](polybase-configure-oracle.md)
- [Teradata의 외부 데이터에 액세스하도록 PolyBase 구성](polybase-configure-teradata.md)
- [MongoDB의 외부 데이터에 액세스하도록 PolyBase 구성](polybase-configure-mongodb.md)
- [ODBC 제네릭 형식의 외부 데이터를 액세스하도록 PolyBase 구성](polybase-configure-odbc-generic.md)
- [SQL Server의 외부 데이터에 액세스하도록 PolyBase 구성](polybase-configure-sql-server.md)

## <a name="select-a-subset-of-rows"></a>행 하위 집합 선택

조건자 푸시다운을 사용하여 외부 테이블에서 행 하위 집합을 선택하는 쿼리의 성능을 향상시킬 수 있습니다.

이 예에서 SQL Server 2016은 Hadoop에서 `customer.account_balance < 200000` 조건자와 일치하는 행을 검색하는 맵 감소 작업을 시작합니다. 테이블의 모든 행을 검색하지 않고 쿼리가 성공적으로 완료될 수 있으므로 조건자 조건에 맞는 행만 SQL Server에 복사됩니다. 이렇게 하면 잔액 &lt; 200000인 고객 수가 계정 잔액 &gt;= 200000인 고객 수에 비해 작은 경우 상당한 시간이 절약되며 필요한 임시 스토리지 공간이 줄어듭니다.

```sql
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="select-a-subset-of-columns"></a>열 하위 집합 선택

조건자 푸시다운을 사용하여 외부 테이블에서 열 하위 집합을 선택하는 쿼리의 성능을 향상시킬 수 있습니다.

이 쿼리에서 SQL Server는 맵 감소 작업을 시작하여 customer.name과 customer.zip_code라는 두 열의 데이터만 SQL Server에 복사되도록 Hadoop의 구분된 텍스트 파일을 전처리합니다.

```sql
SELECT customer.name, customer.zip_code
FROM customer
WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>기본 식과 연산자에 대한 푸시다운

SQL Server는 조건자 푸시다운에 대해 다음과 같은 기본 식과 연산자를 허용합니다.

- 숫자, 날짜 및 시간 값에 대한 이진 비교 연산자(`<`, `>`, `=`, `!=`, `<>`, `>=`, `<=`)
- 산술 연산자(`+`, `-`, `*`, `/`, `%`)
- 논리 연산자(`AND`, `OR`)
- 단항 연산자(`NOT`, `IS NULL`, `IS NOT NULL`)

`BETWEEN`, `NOT`, `IN` 및 `LIKE` 연산자를 푸시다운할 수 있습니다. 실제 동작은 쿼리 최적화 프로그램에서 기본 관계형 연산자를 사용하는 일련의 문으로 다시 작성하는 방법에 따라 달라집니다.

이 예제의 쿼리에는 Hadoop에 푸시다운할 수 있는 여러 조건자가 있습니다. SQL Server는 Hadoop에 맵 감소 작업을 푸시하여 `customer.account_balance <= 200000` 조건자를 수행할 수 있습니다. `BETWEEN 92656 AND 92677` 식도 Hadoop에 푸시할 수 있는 이진 및 논리 연산으로 구성됩니다. `customer.account_balance AND customer.zipcode`의 논리적 **AND** 는 최종 식입니다.

이 조건자를 결합하면 맵 감소 작업에서 모든 WHERE 절을 수행할 수 있습니다. `SELECT` 조건에 맞는 데이터만 SQL Server에 다시 복사됩니다.

```sql
SELECT * FROM customer 
WHERE customer.account_balance <= 200000 
    AND customer.zipcode BETWEEN 92656 AND 92677
```

## <a name="examples"></a>예제

### <a name="force-pushdown"></a>강제 푸시다운

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

### <a name="disable-pushdown"></a>푸시다운 사용 안 함

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
```

## <a name="next-steps"></a>다음 단계

PolyBase에 대한 자세한 내용은 [PolyBase란?](polybase-guide.md)을 참조하세요.
