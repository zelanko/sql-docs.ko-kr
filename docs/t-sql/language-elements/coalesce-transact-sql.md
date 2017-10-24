---
title: COALESCE (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d597c347b0b608b69c5d435fbf58b2779d462a32
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="coalesce-transact-sql"></a>COALESCE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

인수를 순서 대로 평가 하 고 처음에 평가 되지 않는 첫 번째 식의 현재 값을 반환 `NULL`합니다. 예를 들어 `SELECT COALESCE(NULL, NULL, 'third_value', 'fourth_value');` 세 번째 값은 null이 아닌 첫 번째 값 때문에 세 번째 값을 반환 합니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
COALESCE ( expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 모든 종류의 합니다.  
  
## <a name="return-types"></a>반환 형식  
 데이터 형식을 반환 *식* 우선 순위가 가장 높은 데이터 형식입니다. 모든 식에서 Null을 허용하지 않으면 결과가 Null을 허용하지 않는 형식으로 처리됩니다.  
  
## <a name="remarks"></a>주의  
 모든 인수가 `NULL`, `COALESCE` 반환 `NULL`합니다. Null 값 중 하나 이상 형식화 된 해야 `NULL`합니다.  
  
## <a name="comparing-coalesce-and-case"></a>COALESCE 및 CASE 비교  
 `COALESCE` 식은 대 한 구문 바로 가기를 `CASE` 식입니다.  즉, 코드 `COALESCE`(*expression1*,*...n*)이 다음으로 쿼리 최적화 프로그램에서 다시 작성 `CASE` 식:  
  
 ```sql  
 CASE  
 WHEN (expression1 IS NOT NULL) THEN expression1  
 WHEN (expression2 IS NOT NULL) THEN expression2  
 ...  
 ELSE expressionN  
 END  
 ```  
  
 즉, 입력된 값 (*expression1*, *expression2*, *expressionN*등) 여러 번 평가 됩니다. 또한 SQL 표준에 따라 하위 쿼리가 포함된 값 식은 비결정적인 것으로 간주되어 하위 쿼리가 두 번 평가됩니다. 어느 경우에든 첫 번째 평가와 이후 평가 간에 서로 다른 결과가 반환될 수 있습니다.  
  
 예를 들어 `COALESCE((subquery), 1)` 코드를 실행하면 하위 쿼리가 두 번 평가됩니다. 따라서 쿼리 격리 수준에 따라 다른 결과가 반환될 수 있습니다. 예를 들어 코드 반환할 수 있습니다 `NULL` 아래는 `READ COMMITTED` 다중 사용자 환경에서 격리 수준입니다. 결과가 반환 되도록 하려면 사용 하 여는 `SNAPSHOT ISOLATION` 격리 수준 또는 교체 `COALESE` 와 `ISNULL` 함수입니다. 또는 다음 예제와 같이 하위 select 안에 들어가도록 쿼리를 다시 작성할 수 있습니다.  
  
```sql  
SELECT CASE WHEN x IS NOT NULL THEN x ELSE 1 END  
from  
(  
SELECT (SELECT Nullable FROM Demo WHERE SomeCol = 1) AS x  
) AS T;  
  
```  
  
## <a name="comparing-coalesce-and-isnull"></a>COALESCE 및 ISNULL 비교  
 `ISNULL` 함수 및 `COALESCE` 식은 용도 비슷하지만 하지만 다르게 동작할 수 있습니다.  
  
1.  때문에 `ISNULL` 는 함수를 한 번만 계산 됩니다.  입력 값에 대해 위에서 설명한 대로 `COALESCE` 식에 여러 번 계산 될 수 있습니다.  
  
2.  결과 식의 데이터 형식 결정 방법이 다릅니다. `ISNULL`첫 번째 매개 변수의 데이터 형식을 사용 하 여 `COALESCE` 뒤에 오는 `CASE` 및 식 규칙 우선 순위가 가장 높은 값의 데이터 형식을 반환 합니다.  
  
3.  결과 식의 null 허용 여부는에 대 한 다른 `ISNULL` 및 `COALESCE`합니다. `ISNULL` 반환 값은 항상 않은 것으로 간주 (반환 값은 null이 아닌 한 가정) NULLable 반면 `COALESCE` null이 아닌 매개 변수가 있는 것으로 간주 됩니다 `NULL`합니다. 따라서 식 `ISNULL(NULL, 1)` 및 `COALESCE(NULL, 1)`동일 하지만, null 허용 여부가 다른 값이 있습니다. 이 계산된 열에서는 이러한 식을 사용 하 여 키 제약 조건을 만들거나 하거나 결정적 스칼라 UDF의 반환 값을 다음 예제에 나와 있는 것 처럼 인덱싱할 수 있도록 하는 경우 달라를 집니다.  
  
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
  
4.  에 대 한 `ISNULL` 및 `COALESCE` 도 다릅니다. 예를 들어는 `NULL` 값에 대 한 `ISNULL` 변환할 **int** 반면에 대 한 `COALESCE`, 데이터 형식을 제공 해야 합니다.  
  
5.  `ISNULL`반면에 두 개의 매개 변수를 사용 `COALESCE` 가변 개수의 매개 변수를 사용 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-running-a-simple-example"></a>1. 간단한 예 실행  
 다음 예에서는 `COALESCE`가 Null 이외의 값이 있는 첫 번째 열에서 데이터를 선택하는 방법을 보여 줍니다. 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
SELECT Name, Class, Color, ProductNumber,  
COALESCE(Class, Color, ProductNumber) AS FirstNotNull  
FROM Production.Product;  
```  
  
### <a name="b-running-a-complex-example"></a>2. 복잡한 예 실행  
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
 다음 예제에서는 어떻게 `COALESCE` null이 아닌 값을 갖는 첫 번째 열에서 데이터를 선택 합니다. 이 예제에 대 한 가정 하 고 `Products` 이 데이터를 포함 하는 테이블:  
  
 ```  
 Name         Color      ProductNumber  
 ------------ ---------- -------------  
 Socks, Mens  NULL       PN1278  
 Socks, Mens  Blue       PN1965  
 NULL         White      PN9876
 ```  
  
 다음 다음 COALESCE 쿼리를 실행 했습니다.  
  
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
  
 첫 번째 행에서의 `FirstNotNull` 값은 `PN1278`이 아니라 `Socks, Mens`합니다. 때문에 이것이 `Name` 열에 대 한 매개 변수로 지정 하지 않은 `COALESCE` 예제에서입니다.  
  
### <a name="d-complex-example"></a>D: 복잡 한 예  
 다음 예제에서는 `COALESCE` 3 개의 열에 값을 비교 하는 열에 null이 아닌 값만 반환 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [ISNULL &#40; Transact SQL &#41;](../../t-sql/functions/isnull-transact-sql.md)   
 [CASE&#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)  
  
  

