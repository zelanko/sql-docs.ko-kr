---
title: COALESCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COALESCE
- COALESCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], nonnull
- COALESCE function
- first nonnull expressions [SQL Server]
- nonnull expressions
ms.assetid: fafc0dba-f8a8-4aad-9b7f-908e34b74d88
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 085972109c9b19173e46c97cc5cef239a454dcb7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67950297"
---
# <a name="coalesce-transact-sql"></a>COALESCE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

인수를 순서대로 평가하고 처음으로 `NULL`이 아닌 첫 번째 식의 현재 값을 반환합니다. 예를 들어 `SELECT COALESCE(NULL, NULL, 'third_value', 'fourth_value');`는 세 번째 값이 Null이 아닌 첫 값이기 때문에 세 번째 값을 반환합니다. 
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
COALESCE ( expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>인수  
_expression_  
모든 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
## <a name="return-types"></a>반환 형식  
데이터 형식 우선 순위가 가장 높은 _식_의 데이터 형식을 반환합니다. 모든 식에서 Null을 허용하지 않으면 결과가 Null을 허용하지 않는 형식으로 처리됩니다.  
  
## <a name="remarks"></a>설명  
모든 인수가 `NULL`인 경우 `COALESCE`가 `NULL`를 반환합니다. Null 값 중 하나 이상이 `NULL` 형식이어야 합니다.  
  
## <a name="comparing-coalesce-and-case"></a>COALESCE 및 CASE 비교  
`COALESCE` 식은 `CASE` 식의 구문 바로 가기입니다.  즉, 쿼리 최적화 프로그램에서는 `COALESCE`(_expression1_, _...n_) 코드를 다음과 같은 `CASE` 식으로 다시 작성합니다.  
  
```sql  
CASE  
WHEN (expression1 IS NOT NULL) THEN expression1  
WHEN (expression2 IS NOT NULL) THEN expression2  
...  
ELSE expressionN  
END  
```  
  
입력 값(_expression1_, _expression2_, _expressionN_ 등)이 여러 번 평가 됩니다. 하위 쿼리가 포함된 값 식은 비결정적인 것으로 간주되어 하위 쿼리가 두 번 평가됩니다. 이 결과는 SQL 표준을 준수합니다. 어느 경우에든 첫 번째 평가와 예정된 평가 간에 서로 다른 결과가 반환될 수 있습니다.  
  
예를 들어 `COALESCE((subquery), 1)` 코드를 실행하면 하위 쿼리가 두 번 평가됩니다. 따라서 쿼리 격리 수준에 따라 다른 결과가 반환될 수 있습니다. 예를 들어 다중 사용자 환경의 `NULL` 격리 수준에서는 이 코드에서 `READ COMMITTED`을 반환할 수 있습니다. 일정한 결과가 반환되도록 하려면 `SNAPSHOT ISOLATION` 격리 수준을 사용하거나 `COALESCE` 함수로 `ISNULL`를 바꿔야 합니다. 또는 다음 예와 같이 하위 쿼리가 하위 선택 안에 들어가도록 쿼리를 다시 작성할 수 있습니다.  
  
```sql  
SELECT CASE WHEN x IS NOT NULL THEN x ELSE 1 END  
from  
(  
SELECT (SELECT Nullable FROM Demo WHERE SomeCol = 1) AS x  
) AS T;  
  
```  
  
## <a name="comparing-coalesce-and-isnull"></a>COALESCE 및 ISNULL 비교  
`ISNULL` 함수와 `COALESCE` 식은 용도는 비슷하지만 동작은 다를 수 있습니다.  
  
1.  `ISNULL`은 함수이므로 한 번만 평가됩니다.  위의 설명대로 `COALESCE` 식의 입력 값은 여러 번 평가될 수 있습니다.  
  
2.  결과 식의 데이터 형식 결정 방법이 다릅니다. `ISNULL`은 첫 번째 매개 변수의 데이터 형식을 사용하고 `COALESCE`는 `CASE` 식 규칙에 따라 우선 순위가 가장 높은 값의 데이터 형식을 반환합니다.  
  
3.  `ISNULL` 및 `COALESCE`는 결과 식에서의 NULL 허용 여부가 다릅니다. `ISNULL` 반환 값은 항상 Null을 허용하지 않는 것으로 간주(반환 값이 Null을 허용하지 않는 값이라고 가정)됩니다. 이와 반대로 Null이 아닌 매개 변수가 있는 `COALESCE`는 `NULL`로 간주합니다. 따라서 `ISNULL(NULL, 1)` 및 `COALESCE(NULL, 1)` 식은 같지만 Null 허용 여부 값이 다릅니다. 이 값을 사용하면 해당 식을 계산 열에서 사용하거나, 키 제약 조건을 만들거나, 다음 예에서와 같이 인덱싱이 가능하도록 스칼라 UDF 결정적 식의 반환 값을 만드는 경우 차이가 발생합니다.  
  
    ```sql  
    USE tempdb;  
    GO  
    -- This statement fails because the PRIMARY KEY cannot accept NULL values  
    -- and the nullability of the COALESCE expression for col2   
    -- evaluates to NULL.  
    CREATE TABLE #Demo   
    (   
    col1 integer NULL,   
    col2 AS COALESCE(col1, 0) PRIMARY KEY,   
    col3 AS ISNULL(col1, 0)   
    );   
  
    -- This statement succeeds because the nullability of the   
    -- ISNULL function evaluates AS NOT NULL.  
  
    CREATE TABLE #Demo   
    (   
    col1 integer NULL,   
    col2 AS COALESCE(col1, 0),   
    col3 AS ISNULL(col1, 0) PRIMARY KEY   
    );  
    ```  
  
4.  `ISNULL` 및 `COALESCE`에 대한 유효성 검사도 다릅니다. 예를 들어 `NULL`의 경우 데이터 형식을 직접 제공해야 하지만 `ISNULL`에 대한 **값은**int`COALESCE`로 변환됩니다.  
  
5.  `ISNULL`에는 다음 두 개의 매개 변수만 사용됩니다. 반대로, `COALESCE`가 사용하는 매개 변수의 수는 가변적입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-running-a-simple-example"></a>A. 간단한 예 실행  
다음 예에서는 `COALESCE`가 Null 이외의 값이 있는 첫 번째 열에서 데이터를 선택하는 방법을 보여 줍니다. 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
SELECT Name, Class, Color, ProductNumber,  
COALESCE(Class, Color, ProductNumber) AS FirstNotNull  
FROM Production.Product;  
```  
  
### <a name="b-running-a-complex-example"></a>B. 복잡한 예 실행  
다음 예에서는 `wages` 테이블에 직원의 연봉 정보에 대한 시급, 월급 및 커미션의 3개 열이 포함되어 있습니다. 그러나 각 직원은 이 중 한 종류의 급여만 받습니다. 모든 직원에게 지급된 총 급여액을 확인하려면 `COALESCE` 함수를 사용하여 `hourly_wage`, `salary`, `commission`에서 검색된 Null이 아닌 값만 포함시킵니다.  
  
```sql  
SET NOCOUNT ON;  
GO  
USE tempdb;  
IF OBJECT_ID('dbo.wages') IS NOT NULL  
    DROP TABLE wages;  
GO  
CREATE TABLE dbo.wages  
(  
    emp_id        tinyint   identity,  
    hourly_wage   decimal   NULL,  
    salary        decimal   NULL,  
    commission    decimal   NULL,  
    num_sales     tinyint   NULL  
);  
GO  
INSERT dbo.wages (hourly_wage, salary, commission, num_sales)  
VALUES  
    (10.00, NULL, NULL, NULL),  
    (20.00, NULL, NULL, NULL),  
    (30.00, NULL, NULL, NULL),  
    (40.00, NULL, NULL, NULL),  
    (NULL, 10000.00, NULL, NULL),  
    (NULL, 20000.00, NULL, NULL),  
    (NULL, 30000.00, NULL, NULL),  
    (NULL, 40000.00, NULL, NULL),  
    (NULL, NULL, 15000, 3),  
    (NULL, NULL, 25000, 2),  
    (NULL, NULL, 20000, 6),  
    (NULL, NULL, 14000, 4);  
GO  
SET NOCOUNT OFF;  
GO  
SELECT CAST(COALESCE(hourly_wage * 40 * 52,   
   salary,   
   commission * num_sales) AS money) AS 'Total Salary'   
FROM dbo.wages  
ORDER BY 'Total Salary';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```   
Total Salary  
------------  
10000.00  
20000.00  
20800.00  
30000.00  
40000.00  
41600.00  
45000.00  
50000.00  
56000.00  
62400.00  
83200.00  
120000.00  
  
(12 row(s) affected)
```  
  
### <a name="c-simple-example"></a>C: 간단한 예  
다음 예에서는 `COALESCE`가 Null 이외의 값이 있는 첫째 열에서 데이터를 선택하는 방법을 보여 줍니다. 이 예제에서는 `Products` 테이블이 이 데이터를 포함한다고 가정합니다.  
  
```  
Name         Color      ProductNumber  
------------ ---------- -------------  
Socks, Mens  NULL       PN1278  
Socks, Mens  Blue       PN1965  
NULL         White      PN9876
```  
 
이 후 다음 COALESCE 쿼리를 실행합니다.  
  
```sql  
SELECT Name, Color, ProductNumber, COALESCE(Color, ProductNumber) AS FirstNotNull   
FROM Products ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Name         Color      ProductNumber  FirstNotNull  
------------ ---------- -------------  ------------  
Socks, Mens  NULL       PN1278         PN1278  
Socks, Mens  Blue       PN1965         Blue  
NULL         White      PN9876         White
```  
  
첫 번째 행에서의 `FirstNotNull` 값은 `PN1278`가 아닌 `Socks, Mens`입니다. 예제에서 `Name` 열이 `COALESCE`에 대한 매개 변수로 지정되지 않았기 때문에 이와 같은 값이 사용됩니다.  
  
### <a name="d-complex-example"></a>D: 복잡한 예  
다음 예제에서는 `COALESCE`를 사용하여 세 열의 값을 비교하고 열에서 찾은 Null이 아닌 값만 반환합니다.  
  
```sql  
CREATE TABLE dbo.wages  
(  
    emp_id        tinyint   NULL,  
    hourly_wage   decimal   NULL,  
    salary        decimal   NULL,  
    commission    decimal   NULL,  
    num_sales     tinyint   NULL  
);  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (1, 10.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (2, 20.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (3, 30.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (4, 40.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (5, NULL, 10000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (6, NULL, 20000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (7, NULL, 30000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (8, NULL, 40000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (9, NULL, NULL, 15000, 3);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (10,NULL, NULL, 25000, 2);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (11, NULL, NULL, 20000, 6);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (12, NULL, NULL, 14000, 4);  
  
SELECT CAST(COALESCE(hourly_wage * 40 * 52,   
   salary,   
   commission * num_sales) AS decimal(10,2)) AS TotalSalary   
FROM dbo.wages  
ORDER BY TotalSalary;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Total Salary  
------------  
10000.00  
20000.00  
20800.00  
30000.00  
40000.00  
41600.00  
45000.00  
50000.00  
56000.00  
62400.00  
83200.00  
120000.00
```  
  
## <a name="see-also"></a>참고 항목  
[ISNULL &#40;Transact-SQL&#41;](../../t-sql/functions/isnull-transact-sql.md)   
[CASE&#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)  
  
  
