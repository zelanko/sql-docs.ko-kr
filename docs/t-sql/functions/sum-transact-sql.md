---
title: SUM(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SUM
- SUM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], sum of all
- SUM function [Transact-SQL]
- values [SQL Server]
- summation [SQL Server]
- expressions [SQL Server], sum of all values
- DISTINCT keyword
- totals [SQL Server], SUM
- summary values [SQL Server]
ms.assetid: 9af94d0f-55d4-428f-a840-ec530160f379
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6c2f972e93de85e39b2f2e6910cbe9149e69501c
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37789064"
---
# <a name="sum-transact-sql"></a>SUM(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  식의 모든 값 또는 DISTINCT 값의 합계를 반환합니다. SUM은 숫자 열에서만 사용할 수 있습니다. Null 값은 무시됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SUM ( [ ALL | DISTINCT ] expression )
   [ OVER ( [ partition_by_clause ] order_by_clause ) ]
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SUM ( [ ALL | DISTINCT ] expression )  
```  
  
## <a name="arguments"></a>인수  
 ALL  
 모든 값에 집계 함수를 적용합니다. 기본값은 ALL입니다.  
  
 DISTINCT  
 SUM이 고유한 값의 합계를 반환하도록 지정합니다.  
  
 *expression*  
 상수, 열 또는 함수이며 산술, 비트 및 문자열 연산자의 조합입니다. *expression*은 **bit** 데이터 형식을 제외한 정확한 수치 또는 근사치 데이터 형식 범주의 식입니다. 집계 함수와 하위 쿼리는 허용되지 않습니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.  
  
 OVER **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause*는 FROM 절이 생성한 결과 집합을 함수가 적용되는 파티션으로 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. *order_by_clause*는 작업이 수행되는 논리적 순서를 결정합니다. *order_by_clause*가 필요합니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.  
  
## <a name="return-types"></a>반환 형식  
 가장 정확한 *expression* 데이터 형식에서 모든 *expression* 값의 합계를 반환합니다.  
  
|식 결과|반환 형식|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**ssNoversion**|**int**|  
|**bigint**|**bigint**|  
|**decimal** 범주(p, s)|**decimal(38, s)**|  
|**money** 및 **smallmoney** 범주|**money**|  
|**float** 및 **real** 범주|**float**|  
  
## <a name="remarks"></a>Remarks  
 SUM은 OVER 및 ORDER BY 절 없이 사용되는 경우 결정적 함수이고, OVER 및 ORDER BY 절과 함께 지정되는 경우 비결정적 함수입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-sum-to-return-summary-data"></a>1. SUM을 사용하여 요약 데이터 반환  
 다음 예에서는 SUM 함수를 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 요약 데이터를 반환하는 방법을 보여 줍니다.  
  
```  
SELECT Color, SUM(ListPrice), SUM(StandardCost)  
FROM Production.Product  
WHERE Color IS NOT NULL   
    AND ListPrice != 0.00   
    AND Name LIKE 'Mountain%'  
GROUP BY Color  
ORDER BY Color;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Color
--------------- --------------------- ---------------------
Black           27404.84              5214.9616
Silver          26462.84              14665.6792
White           19.00                 6.7926

(3 row(s) affected)
 ```  
  
### <a name="b-using-the-over-clause"></a>2. OVER 절 사용  
 다음 예에서는 OVER 절과 함께 SUM 함수를 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `Sales.SalesPerson` 테이블에 있는 각 지역에 대해 연간 매출의 누적 합계를 구합니다. 데이터는 `TerritoryID`를 기준으로 분할되고 `SalesYTD`를 기준으로 논리적으로 정렬됩니다. 즉, SUM 함수는 판매 연도를 기준으로 각 지역에 대해 계산됩니다. `TerritoryID` 1의 경우 2005년도에 대한 두 개의 행이 있습니다. 이 두 행은 해당 연도의 두 영업 사원과 매출을 나타냅니다. 이 두 행의 누적 매출이 계산된 다음 2006년도 매출을 나타내는 세 번째 행이 계산에 포함됩니다.  
  
```  
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                           ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY TerritoryID,SalesYear;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           559,697.56           559,697.56  
287              NULL        2006        519,905.93           539,801.75           1,079,603.50  
285              NULL        2007        172,524.45           417,375.98           1,252,127.95  
283              1           2005        1,573,012.94         1,462,795.04         2,925,590.07  
280              1           2005        1,352,577.13         1,462,795.04         2,925,590.07  
284              1           2006        1,576,562.20         1,500,717.42         4,502,152.27  
275              2           2005        3,763,178.18         3,763,178.18         3,763,178.18  
277              3           2005        3,189,418.37         3,189,418.37         3,189,418.37  
276              4           2005        4,251,368.55         3,354,952.08         6,709,904.17  
281              4           2005        2,458,535.62         3,354,952.08         6,709,904.17  
  
(10 row(s) affected)  
  
```  
  
 이 예에서는 OVER 절에 PARTITION BY가 포함되어 있지 않습니다. 즉, 이 함수는 쿼리에서 반환된 모든 행에 적용됩니다. OVER 절에 지정된 ORDER BY 절은 SUM 함수가 적용되는 논리적 순서를 결정합니다. 이 쿼리는 WHERE 절에 지정된 모든 판매 지역의 연도별 누적 매출 총액을 반환합니다. SELECT 문에 지정된 ORDER BY 절은 쿼리의 행이 표시되는 순서를 결정합니다.  
  
```  
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY SalesYear;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           2,449,684.05         17,147,788.35  
275              2           2005        3,763,178.18         2,449,684.05         17,147,788.35  
276              4           2005        4,251,368.55         2,449,684.05         17,147,788.35  
277              3           2005        3,189,418.37         2,449,684.05         17,147,788.35  
280              1           2005        1,352,577.13         2,449,684.05         17,147,788.35  
281              4           2005        2,458,535.62         2,449,684.05         17,147,788.35  
283              1           2005        1,573,012.94         2,449,684.05         17,147,788.35  
284              1           2006        1,576,562.20         2,138,250.72         19,244,256.47  
287              NULL        2006        519,905.93           2,138,250.72         19,244,256.47  
285              NULL        2007        172,524.45           1,941,678.09         19,416,780.93  
(10 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-a-simple-sum-example"></a>3. 간단한 SUM 예  
 다음 예는 2003년 판매된 각 제품의 총 수를 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductKey, SUM(SalesAmount) AS TotalPerProduct  
FROM dbo.FactInternetSales  
WHERE OrderDateKey >= '20030101'   
      AND OrderDateKey < '20040101'  
GROUP BY ProductKey  
ORDER BY ProductKey;  
  
```  
  
 다음은 결과 집합의 일부입니다.  
  
 ```
ProductKey  TotalPerProduct
----------  ---------------
214         31421.0200
217         31176.0900
222         29986.4300
225          7956.1500
 ```
  
### <a name="d-calculating-group-totals-with-more-than-one-column"></a>4. 두 개 이상의 열에 대한 그룹 합계 계산  
 다음 예에서는 `ListPrice` 테이블에 나열된 각 색에 대한 `StandardCost` 및 `Product`의 합계를 계산합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT Color, SUM(ListPrice)AS TotalList,   
       SUM(StandardCost) AS TotalCost  
FROM dbo.DimProduct  
GROUP BY Color  
ORDER BY Color;  
```  
  
 결과 집합의 첫 번째 부분은 아래에 나와 있습니다.  
  
 ```
Color       TotalList      TotalCost
----------  -------------  --------------
Black       101295.7191    57490.5378
Blue         24082.9484    14772.0524
Grey           125.0000       51.5625
Multi          880.7468      526.4095
NA            3162.3564     1360.6185
 ```  
  
## <a name="see-also"></a>참고 항목  
 [집계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

