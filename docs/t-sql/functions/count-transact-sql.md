---
description: COUNT(Transact-SQL)
title: COUNT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a5b660c4b55f01f794a07e19374a4c6a8ba38bfb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88311109"
---
# <a name="count-transact-sql"></a>COUNT(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 함수는 그룹에 있는 항목의 수를 반환합니다. `COUNT`은 [COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md) 함수처럼 작동합니다. 이러한 함수는 해당 반환 값의 데이터 형식만이 다릅니다. `COUNT`은 항상 **int** 데이터 형식 값을 반환합니다. `COUNT_BIG`은 항상 **bigint** 데이터 형식 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql

-- Aggregation Function Syntax  
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )  

-- Analytic Function Syntax  
COUNT ( [ ALL ]  { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
**ALL**  
모든 값에 집계 함수를 적용합니다. ALL은 기본값으로 사용됩니다.
  
DISTINCT  
`COUNT`이 Null이 아닌 고유한 값의 수를 반환하도록 지정합니다.
  
*expression*  
**image**, **ntext** 또는 **text**를 제외한 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. `COUNT`이 식에서 집계 함수 또는 하위 쿼리를 지원하지 않습니다.
  
\*  
`COUNT`이 반환할 총 테이블 행 개수를 결정하는 모든 행을 계산해야 한다고 지정합니다. `COUNT(*)`에는 매개 변수가 없으며 DISTINCT의 사용을 지원하지 않습니다. `COUNT(*)`은 특정 열에 대한 정보를 사용하지 않도록 정의되어 있으므로 *expression* 매개 변수가 필요하지 않습니다. `COUNT(*)`은 지정한 테이블에서 행의 수를 반환하고 중복 행을 유지합니다. 각 행은 개별적으로 계산되며 Null 값을 가진 행도 포함됩니다.
  
OVER **(** [ *partition_by_clause* ] [ *order_by_clause* ] [ *ROW_or_RANGE_clause* ] **)**  
*partition_by_clause*는 `FROM` 절이 생성한 결과 집합을 `COUNT` 함수가 적용되는 파티션으로 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. *order_by_clause*는 작업의 논리적 순서를 결정합니다. 자세한 내용은 [OVER 절 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요. 

## <a name="return-types"></a>반환 형식
 **int**  
  
## <a name="remarks"></a>설명  
COUNT(\*)는 그룹에 포함된 항목 개수를 반환합니다. 여기에는 NULL 값과 중복 항목이 포함됩니다.
  
COUNT(ALL *식*)은 그룹에 포함된 각 행의 *식*을 계산하여 Null이 아닌 값의 개수를 반환합니다.
  
COUNT(DISTINCT *식*)은 그룹에 포함된 각 행의 *식*을 계산하여 Null이 아닌 고유 값의 개수를 반환합니다.
  
2^31-1을 초과하는 반환 값의 경우 `COUNT`가 오류를 반환합니다. 이러한 경우 대신 `COUNT_BIG`를 사용합니다.
  
`COUNT`은 OVER 및 ORDER BY 절 ***없이*** 사용되는 경우 결정적 함수이고, OVER 및 ORDER BY 절과 ***함께*** 사용되는 경우 비결정적 함수입니다. 자세한 내용은 [결정적 및 비결정 함수](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)를 참조하세요.
  
## <a name="examples"></a>예제  
  
### <a name="a-using-count-and-distinct"></a>A. COUNT 및 DISTINCT 사용  
이 예제에서는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 직원이 보유할 수 있는 여러 직함의 수를 반환합니다.
  
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
  
### <a name="b-using-count"></a>B. COUNT(\*) 사용  
이 예제에서는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 직원의 총 수를 반환합니다.
  
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
  
### <a name="c-using-count-with-other-aggregates"></a>C. 다른 집계와 COUNT(\*) 사용  
이 예제에서는 `COUNT(*)`가 `SELECT` 목록의 다른 집계 함수로 작동하는 것을 보여줍니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.
  
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
  
### <a name="d-using-the-over-clause"></a>D. OVER 절 사용  
이 예제에서는 `OVER` 절에서 `MIN`, `MAX`, `AVG` 및 `COUNT` 함수를 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스 `HumanResources.Department` 테이블에서 각 부서에 대해 집계된 값을 반환합니다.
  
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
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-count-and-distinct"></a>E. COUNT 및 DISTINCT 사용  
이 예제에서는 특정 회사의 직원이 보유할 수 있는 여러 직함의 수를 반환합니다.
  
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
  
### <a name="f-using-count"></a>F. COUNT(\*) 사용  
이 예제에서는 `dbo.DimEmployee` 테이블에 있는 총 행 수를 반환합니다.
  
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
  
### <a name="g-using-count-with-other-aggregates"></a>G. 다른 집계와 COUNT(\*) 사용  
이 예제에서는 `COUNT(*)`를 `SELECT` 목록의 다른 집계 함수와 결합합니다. 그러면 연간 판매 할당량이 $500,000를 초과하는 영업 담당자의 수와 해당 영업 담당자의 평균 영업 할당량을 반환합니다.
  
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
  
### <a name="h-using-count-with-having"></a>H. HAVING과 함께 COUNT 사용  
이 예제에서는 `HAVING` 절과 함께 `COUNT`를 사용하여 각각 15명 이상의 직원이 있는 회사의 부서를 반환합니다.
  
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
  
### <a name="i-using-count-with-over"></a>9\. OVER와 함께 COUNT 사용  
이 예제에서는 `OVER` 절과 함께 `COUNT`를 사용하여 지정된 각 판매 주문에 포함된 제품의 수를 반환합니다.
  
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
[집계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/count-big-transact-sql.md)  
[OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  


