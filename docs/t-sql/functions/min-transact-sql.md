---
title: MIN (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MIN
- MIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MIN function [Transact-SQL]
- minimum values [SQL Server]
- values [SQL Server], minimum
ms.assetid: 56cf6ec5-34f5-47e3-a402-7129039d4429
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: eff0ef5388cd1f26053187a3ac06847214f3abf0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="min-transact-sql"></a>MIN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  식의 최소값을 반환합니다. 가 올 수 있습니다는 [OVER 절](../../t-sql/queries/select-over-clause-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
    
MIN ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregation Function Syntax  
MIN ( [ ALL | DISTINCT ] expression )  
  
-- Aggregation Function Syntax   
MIN ( expression ) OVER ( [ <partition_by_clause> ] [ <order_by_clause> ] )  
```  
  
## <a name="arguments"></a>인수  
 **ALL**  
 모든 값에 집계 함수를 적용합니다. 기본값은 ALL입니다.  
  
 DISTINCT  
 각 고유 값을 고려하도록 지정합니다. DISTINCT는 MIN에서는 의미가 없으며 ISO 호환성을 위해서만 제공됩니다.  
  
 *expression*  
 상수, 열 이름 또는 함수이며 산술, 비트 및 문자열 연산자의 조합입니다. MIN은 함께 사용할 수 있습니다 **숫자**, **char**, **varchar**, **uniqueidentifier**, 또는 **datetime** 열, 익숙하지 않습니다 **비트** 열입니다. 집계 함수와 하위 쿼리는 허용되지 않습니다.  
  
 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.  
  
 통해 **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* 함수가 적용 되는 파티션으로 FROM 절에서 생성 한 결과 집합을 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. *order_by_clause* 작업이 수행 되는 논리적 순서를 결정 합니다. *order_by_clause* 가 필요 합니다. 자세한 내용은 참조 [OVER 절 &#40; Transact SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>반환 형식  
 반환 값과 동일 *식*합니다.  
  
## <a name="remarks"></a>주의  
 MIN은 모든 Null 값을 무시합니다.  
  
 문자 데이터 열에서 MIN은 정렬 순서에서 가장 낮은 값을 찾습니다.  
  
 MIN은 OVER 및 ORDER BY 절 없이 사용되는 경우 결정적 함수이고, OVER 및 ORDER BY 절과 함께 지정되는 경우 비결정적 함수입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-example"></a>1. 간단한 예  
 다음 예에서는 가장 낮은(최소) 세율이 반환됩니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```  
SELECT MIN(TaxRate)  
FROM Sales.SalesTaxRate;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 -------------------
  
 5.00
  
 (1 row(s) affected)
 ```  
  
### <a name="b-using-the-over-clause"></a>2. OVER 절 사용  
 다음 예에서는 OVER 절과 함께 MIN, MAX, AVG 및 COUNT 함수를 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `HumanResources.Department` 테이블에서 각 부서에 대한 집계 값을 제공합니다.  
  
```  
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
  
```  
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
  
### <a name="c-using-min"></a>3. MIN을 사용 하 여  
 다음 예제에서는 MIN 집계 함수를 사용 하 여 지정된 된 판매 주문 집합의 가장 저렴 하다 (최소) 제품의 가격을 반환 하 합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT MIN(UnitPrice)  
FROM dbo.FactResellerSales   
WHERE SalesOrderNumber IN (N'SO43659', N'SO43660', N'SO43664');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------  
 5.1865
 ```  
  
### <a name="d-using-min-with-over"></a>4. OVER MIN 사용  
 다음 예에서는 각 판매 주문에서 가장 저렴 하다 제품의 가격을 반환 하려면 MIN OVER() 분석 함수를 사용 합니다. 결과 집합으로 분할 되는 `SalesOrderID` 열입니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT MIN(UnitPrice) OVER(PARTITION BY SalesOrderNumber) AS LeastExpensiveProduct,  
       SalesOrderNumber  
FROM dbo.FactResellerSales    
WHERE SalesOrderNumber IN (N'SO43659', N'SO43660', N'SO43664')  
ORDER BY SalesOrderNumber;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LeastExpensiveProduct SalesOrderID  
--------------------- ----------  
5.1865                SO43659  
419.4589              SO43660  
28.8404               SO43664
```  
  
## <a name="see-also"></a>관련 항목:  
 [집계 함수 &#40; Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [최대 &#40; Transact SQL &#41;](../../t-sql/functions/max-transact-sql.md)   
 [절 &#40; 조치 Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  


