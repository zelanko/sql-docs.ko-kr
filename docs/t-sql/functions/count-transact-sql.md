---
title: COUNT (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COUNT_TSQL
- COUNT
dev_langs:
- TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT function
- totals [SQL Server]
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT function [Transact-SQL]
ms.assetid: 28d39da6-bc2e-46c7-858c-b1721c938830
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: e2d11d2cc57d275e952ff371ddf99c34dcae323d
ms.contentlocale: ko-kr
ms.lasthandoff: 10/05/2017

---
# <a name="count-transact-sql"></a>COUNT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

그룹의 항목 개수를 반환합니다. Count는 [COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md) 함수입니다. 두 함수 간의 유일한 차이점은 반환 값뿐입니다. COUNT는 항상 반환는 **int** 데이터 값을 입력 합니다. COUNT_BIG은 항상 반환 된 **bigint** 데이터 값을 입력 합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
-- Syntax for SQL Server and Azure SQL Database  
  
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )   
    [ OVER (   
        [ partition_by_clause ]   
        [ order_by_clause ]   
        [ ROW_or_RANGE_clause ]  
    ) ]  
```  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregation Function Syntax  
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )  

-- Analytic Function Syntax  
COUNT ( { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>인수  
**ALL**  
모든 값에 집계 함수를 적용합니다. 기본값은 ALL입니다.
  
DISTINCT  
Null이 아닌 고유한 값의 개수만 반환하도록 지정합니다.
  
*expression*  
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 제외한 모든 형식의 **텍스트**, **이미지**, 또는 **ntext**합니다. 집계 함수와 하위 쿼리는 허용되지 않습니다.
  
\*  
테이블 행의 전체 개수를 반환할 때 모든 행이 포함되도록 지정합니다. COUNT (\*) 매개 변수가 없으며 DISTINCT와 함께 사용할 수 없습니다. COUNT (\*) 필요 하지 않습니다는 *식* 매개 변수 이므로 기본적으로 사용 하지 않는 특정 열에 대 한 정보입니다. COUNT(*)는 지정한 테이블에서 중복 행을 포함한 행의 개수를 반환합니다. 각 행은 개별적으로 계산되며 Null 값을 가진 행도 포함됩니다.
  
통해 **(** [ *partition_by_clause* ] [ *order_by_clause* ] [ *ROW_or_RANGE_clause* ] **)**  
*partition_by_clause* 함수가 적용 되는 파티션으로 FROM 절에서 생성 한 결과 집합을 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. *order_by_clause* 작업이 수행 되는 논리적 순서를 결정 합니다. 자세한 내용은 참조 [OVER 절 &#40; Transact SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>반환 형식
 **int**  
  
## <a name="remarks"></a>주의  
COUNT(*)는 그룹에 포함된 항목 개수를 반환합니다. 여기에는 NULL 값과 중복 항목이 포함됩니다.
  
COUNT (모든 *식*) 평가 *식* 그룹의 각 행에 대해 null이 아닌 값의 수를 반환 합니다.
  
COUNT (DISTINCT *식*) 평가 *식* 그룹의 각 행에 대해 null이 아닌 값의 수를 반환 합니다.
  
반환 값이 2^31-1보다 큰 경우 COUNT에서 오류가 발생합니다. 이 때는 COUNT 대신 COUNT_BIG을 사용하세요.
  
COUNT는 OVER 및 ORDER BY 절 없이 사용되는 경우 결정적 함수이고, OVER 및 ORDER BY 절과 함께 지정되는 경우 비결정적 함수입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.
  
## <a name="examples"></a>예  
  
### <a name="a-using-count-and-distinct"></a>1. COUNT 및 DISTINCT 사용  
다음 예에서는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]에서 근무하는 직원이 가질 수 있는 고유한 직함의 수를 나열하는 방법을 보여 줍니다.
  
```sql
SELECT COUNT(DISTINCT Title)  
FROM HumanResources.Employee;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
67  
  
(1 row(s) affected)
```
  
### <a name="b-using-count"></a>2. COUNT(*) 사용  
다음 예에서는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]에서 근무하는 전체 직원의 수를 구하는 방법을 보여 줍니다.
  
```sql
SELECT COUNT(*)  
FROM HumanResources.Employee;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
290  
  
(1 row(s) affected)
```
  
### <a name="c-using-count-with-other-aggregates"></a>3. COUNT(*)와 다른 집계 사용  
다음 예에서는 SELECT 목록에서 `COUNT(*)`를 다른 집계 함수와 결합할 수 있음을 보여 줍니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.
  
```sql
SELECT COUNT(*), AVG(Bonus)  
FROM Sales.SalesPerson  
WHERE SalesQuota > 25000;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
----------- ---------------------
14            3472.1428
  
(1 row(s) affected)
```
  
### <a name="d-using-the-over-clause"></a>4. OVER 절 사용  
다음 예에서는 OVER 절과 함께 MIN, MAX, AVG 및 COUNT 함수를 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `HumanResources.Department` 테이블에서 각 부서에 대한 집계 값을 제공합니다.
  
```sql
SELECT DISTINCT Name  
       , MIN(Rate) OVER (PARTITION BY edh.DepartmentID) AS MinSalary  
       , MAX(Rate) OVER (PARTITION BY edh.DepartmentID) AS MaxSalary  
       , AVG(Rate) OVER (PARTITION BY edh.DepartmentID) AS AvgSalary  
       ,COUNT(edh.BusinessEntityID) OVER (PARTITION BY edh.DepartmentID) AS EmployeesPerDept  
FROM HumanResources.EmployeePayHistory AS eph  
JOIN HumanResources.EmployeeDepartmentHistory AS edh  
     ON eph.BusinessEntityID = edh.BusinessEntityID  
JOIN HumanResources.Department AS d  
ON d.DepartmentID = edh.DepartmentID
WHERE edh.EndDate IS NULL  
ORDER BY Name;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Name                          MinSalary             MaxSalary             AvgSalary             EmployeesPerDept  
----------------------------- --------------------- --------------------- --------------------- ----------------  
Document Control              10.25                 17.7885               14.3884               5  
Engineering                   32.6923               63.4615               40.1442               6  
Executive                     39.06                 125.50                68.3034               4  
Facilities and Maintenance    9.25                  24.0385               13.0316               7  
Finance                       13.4615               43.2692               23.935                10  
Human Resources               13.9423               27.1394               18.0248               6  
Information Services          27.4038               50.4808               34.1586               10  
Marketing                     13.4615               37.50                 18.4318               11  
Production                    6.50                  84.1346               13.5537               195  
Production Control            8.62                  24.5192               16.7746               8  
Purchasing                    9.86                  30.00                 18.0202               14  
Quality Assurance             10.5769               28.8462               15.4647               6  
Research and Development      40.8654               50.4808               43.6731               4  
Sales                         23.0769               72.1154               29.9719               18  
Shipping and Receiving        9.00                  19.2308               10.8718               6  
Tool Design                   8.62                  29.8462               23.5054               6  
  
(16 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-count-and-distinct"></a>5. COUNT 및 DISTINCT 사용  
다음 예제에서는 특정 회사에서 근무 하는 직원이 보유할 수 있는 다른 타이틀 수를 나열 합니다.
  
```sql
USE ssawPDW;  
  
SELECT COUNT(DISTINCT Title)  
FROM dbo.DimEmployee;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
67
```  
  
### <a name="f-using-count"></a>6. COUNT(*) 사용  
에 있는 행의 총 수를 반환 하는 다음 예제는 `dbo.DimEmployee` 테이블입니다.
  
```sql
USE ssawPDW;  
  
SELECT COUNT(*)  
FROM dbo.DimEmployee;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-------------
296
```  
  
### <a name="g-using-count-with-other-aggregates"></a>7. COUNT(*)와 다른 집계 사용  
다음 예제에서는 결합 `COUNT(*)` SELECT 목록에 다른 집계 함수와 합니다. 쿼리는 500, 000 달러와 평균 판매 할당량 보다 큰 연간 판매 할당량이 있는 영업 담당자의 수를 반환합니다.
  
```sql
USE ssawPDW;  
  
SELECT COUNT(EmployeeKey) AS TotalCount, AVG(SalesAmountQuota) AS [Average Sales Quota]  
FROM dbo.FactSalesQuota  
WHERE SalesAmountQuota > 500000 AND CalendarYear = 2001;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
TotalCount  Average Sales Quota
----------  -------------------
10          683800.0000
```
  
### <a name="h-using-count-with-having"></a>8. HAVING 개수 사용  
다음 예에서는 HAVING 절과 함께 COUNT를 사용 하 여 15 개 이상의 직원이 있는 회사의 부서를 반환 합니다.
  
```sql
USE ssawPDW;  
  
SELECT DepartmentName,   
       COUNT(EmployeeKey)AS EmployeesInDept  
FROM dbo.DimEmployee  
GROUP BY DepartmentName  
HAVING COUNT(EmployeeKey) > 15;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
DepartmentName  EmployeesInDept
--------------  ---------------
Sales           18
Production      179
```
  
### <a name="i-using-count-with-over"></a>9. OVER 개수 사용  
다음 예에서는 OVER 절과 함께 COUNT를 사용 하 여 각각 지정 된 판매 주문에 포함 된 제품 수를 반환 합니다.
  
```sql
USE ssawPDW;  
  
SELECT DISTINCT COUNT(ProductKey) OVER(PARTITION BY SalesOrderNumber) AS ProductCount  
    ,SalesOrderNumber  
FROM dbo.FactInternetSales  
WHERE SalesOrderNumber IN (N'SO53115',N'SO55981');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
ProductCount   SalesOrderID`
------------   -----------------
3              SO53115
1              SO55981
```
  
## <a name="see-also"></a>참고 항목
[집계 함수 &#40; Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT_BIG &#40; Transact SQL &#41;](../../t-sql/functions/count-big-transact-sql.md)  
[절 &#40; 조치 Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  



