---
title: "OVER 절 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OVER_TSQL
- OVER
dev_langs:
- TSQL
helpviewer_keywords:
- order of rowsets [SQL Server]
- rowsets [SQL Server], windowing
- window function
- partitions [SQL Server], rowsets
- clauses [SQL Server], OVER
- rowsets [SQL Server], partitioning
- rowsets [SQL Server], ordering
- OVER clause
ms.assetid: ddcef3a6-0341-43e0-ae73-630484b7b398
caps.latest.revision: 75
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: db58418025c1659d42c4f1b76a06af8b08ff2ea6
ms.openlocfilehash: 9e6dad4cbd3e3b64b35f859986b4b7b9928babd5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/06/2017

---
# <a name="select---over-clause-transact-sql"></a>선택-OVER 절 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  관련 창 함수를 적용하기 전에 행 집합의 분할과 순서를 결정합니다. 즉, OVER 절은 쿼리 결과 집합 내의 창 또는 사용자 지정 행 집합을 정의합니다. 그런 다음 창 함수가 창의 각 행에 대한 값을 계산합니다. OVER 절에 함수를 사용하여 이동 평균, 누적 집계, 누계 또는 그룹 결과당 상위 N개 결과 등의 집계된 값을 계산할 수 있습니다.  
  
-   [순위 함수](../../t-sql/functions/ranking-functions-transact-sql.md)  
  
-   [집계 함수](../../t-sql/functions/aggregate-functions-transact-sql.md)  
  
-   [분석 함수](../../t-sql/functions/analytic-functions-transact-sql.md)  
  
-   [NEXT VALUE FOR 함수](../../t-sql/functions/next-value-for-transact-sql.md)  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Database, and Azure SQL Data Warehouse  
  
OVER (   
       [ <PARTITION BY clause> ]  
       [ <ORDER BY clause> ]   
       [ <ROW or RANGE clause> ]  
      )  
  
<PARTITION BY clause> ::=  
PARTITION BY value_expression , ... [ n ]  
  
<ORDER BY clause> ::=  
ORDER BY order_by_expression  
    [ COLLATE collation_name ]   
    [ ASC | DESC ]   
    [ ,...n ]  
  
<ROW or RANGE clause> ::=  
{ ROWS | RANGE } <window frame extent>  
  
<window frame extent> ::=   
{   <window frame preceding>  
  | <window frame between>  
}  
<window frame between> ::=   
  BETWEEN <window frame bound> AND <window frame bound>  
  
<window frame bound> ::=   
{   <window frame preceding>  
  | <window frame following>  
}  
  
<window frame preceding> ::=   
{  
    UNBOUNDED PRECEDING  
  | <unsigned_value_specification> PRECEDING  
  | CURRENT ROW  
}  
  
<window frame following> ::=   
{  
    UNBOUNDED FOLLOWING  
  | <unsigned_value_specification> FOLLOWING  
  | CURRENT ROW  
}  
  
<unsigned value specification> ::=   
{  <unsigned integer literal> }  
  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
OVER ( [ PARTITION BY value_expression ] [ order_by_clause ] )  
```  
  
## <a name="arguments"></a>인수  
 PARTITION BY  
 쿼리 결과 집합을 파티션으로 분할합니다. 창 함수는 각 파티션에 별도로 적용되므로 각 파티션에 대해 계산이 다시 시작됩니다.  
  
 *value_expression*  
 행 집합을 분할하는 데 사용하는 열을 지정합니다. *value_expression* FROM 절을 통해 사용 가능한 열만 참조할 수 있습니다. *value_expression* 식이나 select 목록에 별칭을 참조할 수 없습니다. *value_expression* 열 식, 스칼라 하위 쿼리, 스칼라 함수 또는 사용자 정의 변수 될 수 있습니다.  
  
 \<ORDER BY 절 >  
 결과 집합의 각 파티션 내에서 행의 논리적 순서를 정의합니다. 즉, 창 functioncalculation이 수행되는 논리적 순서를 지정합니다.  
  
 *order_by_expression*  
 정렬할 열 또는 식을 지정합니다. *order_by_expression* FROM 절을 통해 사용 가능한 열만 참조할 수 있습니다. 열 이름이나 별칭을 나타내기 위해 정수를 지정할 수는 없습니다.  
  
 COLLATE *데이터 정렬 이름*  
 에 지정 된 데이터 정렬에 따라 ORDER BY 작업을 수행 하도록 지정 *데이터 정렬 이름*합니다. *데이터 정렬 이름* Windows 데이터 정렬 이름이 나 SQL 데이터 정렬 이름이 될 수 있습니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요. COLLATE 형식의 열에만 적용 가능 **char**, **varchar**, **nchar**, 및 **nvarchar**합니다.  
  
 **ASC** | DESC  
 지정된 열의 값이 오름차순으로 정렬되는지 내림차순으로 정렬되는지를 지정합니다. ASC가 기본 정렬 순서입니다. Null 값은 가능한 가장 작은 값으로 취급됩니다.  
  
 ROWS | RANGE  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
 파티션 내의 시작점 및 끝점을 지정하여 파티션 내의 행을 추가로 제한합니다. 이 작업은 논리적 연결이나 물리적 연결을 통해 현재 행을 기준으로 한 행 범위를 지정하여 수행됩니다. 물리적 연결은 ROWS 절을 사용하여 수행됩니다.  
  
 ROWS 절은 현재 행 이전 또는 다음의 고정 행 수를 지정하여 파티션 내의 행 수를 제한합니다. 또한 RANGE 절은 현재 행의 값을 기준으로 행 범위를 지정하여 파티션 내의 행 수를 논리적으로 제한합니다. 이전 및 다음 행은 ORDER BY 절의 순서에 따라 정의됩니다. 창 프레임 "RANGE … CURRENT ROW … " 현재 행으로 ORDER BY 식에 동일한 값을 가진 모든 행을 포함 합니다. 예를 들어 ROWS BETWEEN 2 PRECEDING AND CURRENT ROW는 함수가 작동하는 행의 창 크기가 앞의 두 행과 현재 행을 포함하여 모두 세 개의 행임을 의미합니다.  
  
> [!NOTE]  
>  ROWS 또는 RANGE에는 ORDER BY 절을 지정해야 합니다. ORDER BY에 여러 개의 순서 식이 포함되어 있는 경우 CURRENT ROW FOR RANGE는 현재 행을 확인할 때 ORDER BY 목록의 모든 열을 고려합니다.  
  
 UNBOUNDED PRECEDING  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 창이 파티션의 첫 번째 행에서 시작되도록 지정합니다. UNBOUNDED PRECEDING은 창 시작 지점으로만 지정할 수 있습니다.  
  
 \<value 부호 없음 > PRECEDING  
 지정 된 \<value 부호 없음 > 행 또는 현재 행 앞에 값의 수를 나타냅니다. RANGE에는 이 인수를 지정할 수 없습니다.  
  
 CURRENT ROW  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
 창이 현재 행(ROWS와 함께 사용될 경우) 또는 현재 값(RANGE와 함께 사용될 경우)에서 시작되거나 끝나도록 지정합니다. CURRENT ROW는 시작 지점 및 끝 지점 모두로 지정할 수 있습니다.  
  
 사이의 \<바인딩된 창 프레임 > AND \<바인딩된 창 프레임 >  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
 ROWS 또는 RANGE와 함께 사용되어 창의 하한(시작) 및 상한(끝) 지점을 지정합니다. \<창 프레임 바인딩된 > 경계 시작 지점 정의 및 \<바인딩된 창 프레임 > 경계 끝점을 정의 합니다. 상한은 하한보다 작을 수 없습니다.  
  
 UNBOUNDED FOLLOWING  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
 창이 파티션의 마지막 행에서 끝나도록 지정합니다. UNBOUNDED FOLLOWING은 창 끝 지점으로만 지정할 수 있습니다. 예를 들어 RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING은 현재 행에서 시작하고 파티션의 마지막 행에서 끝나는 창을 정의합니다.  
  
 \<value 부호 없음 > 다음  
 지정 된 \<value 서명 되지 않은 > 행 또는 값에 따라 현재 행의 수를 나타냅니다. 때 \<value 서명 되지 않은 > 다음 창 시작 지점으로 지정 된, 끝점 이어야 합니다 \<value 서명 되지 않은 > 다음 합니다. 예를 들어 ROWS BETWEEN 2 FOLLOWING AND 10 FOLLOWING은 현재 행 다음의 두 번째 행에서 시작하고 현재 행 다음의 열 번째 행에서 끝나는 창을 정의합니다. RANGE에는 이 인수를 지정할 수 없습니다.  
  
 부호 없는 정수 리터럴  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 현재 행 이전 또는 다음의 행 또는 값 수를 지정하는 양의 정수 리터럴(0 포함)입니다. 이 인수는 ROWS에만 지정할 수 있습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 단일 쿼리의 단일 FROM 절에서 둘 이상의 창 함수를 사용할 수 있습니다. 각 함수의 OVER 절은 분할 및 순서에서 달라질 수 있습니다.  
  
 PARTITION BY를 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. 
 
### <a name="important"></a>중요!

ROWS/RANGE는 지정 하는 경우 및 \<이전 창 프레임 >에 사용 되 \<창 프레임 크기 > (짧은 구문)이이 사양은 창 프레임 경계 시작 지점에 사용 되 고 CURRENT ROW는 경계 끝에 사용 됩니다 점입니다. 예를 들어 “ROWS 5 PRECEDING”은 “ROWS BETWEEN 5 PRECEDING AND CURRENT ROW”와 같습니다.  
  
> [!NOTE]
> ORDER BY를 지정하지 않을 경우 전체 파티션이 창 프레임에 사용됩니다. 이는 ORDER BY 절이 필요하지 않은 함수에만 적용됩니다. ROWS/RANGE는 지정하지 않았지만 ORDER BY를 지정한 경우 RANGE UNBOUNDED PRECEDING AND CURRENT ROW가 창 프레임의 기본값으로 사용됩니다. 이는 선택적 ROWS/RANGE 사양을 허용할 수 있는 함수에만 적용됩니다. 예를 들어 순위 함수는 ROWS/RANGE를 허용할 수 없으므로 ORDER BY가 있고 ROWS/RANGE가 없더라도 이 창 프레임은 적용되지 않습니다.  
    
## <a name="limitations-and-restrictions"></a>제한 사항  
 OVER 절은 CHECKSUM 집계 함수와 함께 사용할 수 없습니다.  
  
 범위는 함께 사용할 수 없습니다 \<value 서명 되지 않은 > PRECEDING 또는 \<value 서명 되지 않은 > 다음 합니다.  
  
 OVER 절과 함께 사용 하는 순위, 집계 또는 분석 함수에 따라 \<ORDER BY 절 > 및/또는 \<ROWS 및 RANGE 절 > 지원 되지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-over-clause-with-the-rownumber-function"></a>1. OVER 절에 ROW_NUMBER 함수 사용  
 다음 예에서는 OVER 절에 ROW_NUMBER 함수를 사용하여 파티션 내의 각 행에 대한 행 번호를 표시하는 방법을 보여 줍니다. OVER 절에 지정된 ORDER BY 절은 각 파티션의 행을 `SalesYTD` 열을 기준으로 정렬합니다. SELECT 문의 ORDER BY 절은 전체 쿼리 결과 집합이 반환되는 순서를 결정합니다.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
SELECT ROW_NUMBER() OVER(PARTITION BY PostalCode ORDER BY SalesYTD DESC) AS "Row Number",   
    p.LastName, s.SalesYTD, a.PostalCode  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0  
ORDER BY PostalCode;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Row Number      LastName                SalesYTD              PostalCode 
 --------------- ----------------------- --------------------- ---------- 
 1               Mitchell                4251368.5497          98027 
 2               Blythe                  3763178.1787          98027 
 3               Carson                  3189418.3662          98027 
 4               Reiter                  2315185.611           98027 
 5               Vargas                  1453719.4653          98027  
 6               Ansman-Wolfe            1352577.1325          98027  
 1               Pak                     4116871.2277          98055  
 2               Varkey Chudukatil       3121616.3202          98055  
 3               Saraiva                 2604540.7172          98055  
 4               Ito                     2458535.6169          98055  
 5               Valdez                  1827066.7118          98055  
 6               Mensa-Annan             1576562.1966          98055  
 7               Campbell                1573012.9383          98055  
 8               Tsoflias                1421810.9242          98055
 ```  
  
### <a name="b-using-the-over-clause-with-aggregate-functions"></a>2. OVER 절에 집계 함수 사용  
 다음 예에서는 쿼리에서 반환된 모든 행에 대해 `OVER` 절에 집계 함수를 사용합니다. 이 예에서는 하위 쿼리를 사용하는 것보다 `OVER` 절을 사용하는 것이 집계 값을 파생시키는 데 더 효율적입니다.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
SELECT SalesOrderID, ProductID, OrderQty  
    ,SUM(OrderQty) OVER(PARTITION BY SalesOrderID) AS Total  
    ,AVG(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Avg"  
    ,COUNT(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Count"  
    ,MIN(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Min"  
    ,MAX(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Max"  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
SalesOrderID ProductID   OrderQty Total       Avg         Count       Min    Max  
------------ ----------- -------- ----------- ----------- ----------- ------ ------  
43659        776         1        26          2           12          1      6  
43659        777         3        26          2           12          1      6  
43659        778         1        26          2           12          1      6  
43659        771         1        26          2           12          1      6  
43659        772         1        26          2           12          1      6  
43659        773         2        26          2           12          1      6  
43659        774         1        26          2           12          1      6  
43659        714         3        26          2           12          1      6  
43659        716         1        26          2           12          1      6  
43659        709         6        26          2           12          1      6  
43659        712         2        26          2           12          1      6  
43659        711         4        26          2           12          1      6  
43664        772         1        14          1           8           1      4  
43664        775         4        14          1           8           1      4  
43664        714         1        14          1           8           1      4  
43664        716         1        14          1           8           1      4  
43664        777         2        14          1           8           1      4  
43664        771         3        14          1           8           1      4  
43664        773         1        14          1           8           1      4  
43664        778         1        14          1           8           1      4  
```  
  
 다음 예에서는 `OVER` 절에 계산된 값의 집계 함수를 사용하는 방법을 보여 줍니다.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
SELECT SalesOrderID, ProductID, OrderQty  
    ,SUM(OrderQty) OVER(PARTITION BY SalesOrderID) AS Total  
    ,CAST(1. * OrderQty / SUM(OrderQty) OVER(PARTITION BY SalesOrderID)   
        *100 AS DECIMAL(5,2))AS "Percent by ProductID"  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] 집계는 `SalesOrderID`로 계산되며 각 `Percent by ProductID`의 각 줄에 대해 `SalesOrderID`가 계산됩니다.  
  
```  
SalesOrderID ProductID   OrderQty Total       Percent by ProductID  
------------ ----------- -------- ----------- ---------------------------------------  
43659        776         1        26          3.85  
43659        777         3        26          11.54  
43659        778         1        26          3.85  
43659        771         1        26          3.85  
43659        772         1        26          3.85  
43659        773         2        26          7.69  
43659        774         1        26          3.85  
43659        714         3        26          11.54  
43659        716         1        26          3.85  
43659        709         6        26          23.08  
43659        712         2        26          7.69  
43659        711         4        26          15.38  
43664        772         1        14          7.14  
43664        775         4        14          28.57  
43664        714         1        14          7.14  
43664        716         1        14          7.14  
43664        777         2        14          14.29  
43664        771         3        14          21.4  
43664        773         1        14          7.14  
43664        778         1        14          7.14  
  
 (20 row(s) affected)  
```  
  
### <a name="c-producing-a-moving-average-and-cumulative-total"></a>3. 이동 평균 및 누적 합계 생성  
 다음 예에서는 OVER 절과 함께 AVG 및 SUM 함수를 사용하여 `Sales.SalesPerson` 테이블에 있는 각 지역에 대해 연간 매출의 이동 평균 및 누적 합계를 구합니다. 데이터는 `TerritoryID`를 기준으로 분할되고 `SalesYTD`를 기준으로 논리적으로 정렬됩니다. 즉, AVG 함수는 판매 연도를 기준으로 각 지역에 대해 계산됩니다. `TerritoryID` 1의 경우 2005년도에 대한 두 개의 행이 있습니다. 이 두 행은 해당 연도의 두 영업 사원과 매출을 나타냅니다. 이 두 행의 평균 매출이 계산된 다음 2006년도 매출을 나타내는 세 번째 행이 계산에 포함됩니다.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
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
  
 이 예에서는 OVER 절에 PARTITION BY가 포함되어 있지 않습니다. 즉, 이 함수는 쿼리에서 반환된 모든 행에 적용됩니다. OVER 절에 지정된 ORDER BY 절은 AVG 함수가 적용되는 논리적 순서를 결정합니다. 이 쿼리는 WHERE 절에 지정된 모든 판매 지역의 연도별 매출 이동 평균을 반환합니다. SELECT 문에 지정된 ORDER BY 절은 쿼리의 행이 표시되는 순서를 결정합니다.  
  
```t-sql  
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
  
### <a name="d-specifying-the-rows-clause"></a>4. ROWS 절 지정  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 다음 예에서는 ROWS 절을 사용 하 여 현재 행으로 행을 계산 하는 창을 정의 하 고 *N* (이 예제에서는 1 행)를 수행 하는 행의 번호입니다.  
  
```t-sql  
SELECT BusinessEntityID, TerritoryID   
    ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
    ,DATEPART(yy,ModifiedDate) AS SalesYear  
    ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                             ORDER BY DATEPART(yy,ModifiedDate)   
                                             ROWS BETWEEN CURRENT ROW AND 1 FOLLOWING ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYTD             SalesYear   CumulativeTotal  
---------------- ----------- -------------------- ----------- --------------------  
274              NULL        559,697.56           2005        1,079,603.50  
287              NULL        519,905.93           2006        692,430.38  
285              NULL        172,524.45           2007        172,524.45  
283              1           1,573,012.94         2005        2,925,590.07  
280              1           1,352,577.13         2005        2,929,139.33  
284              1           1,576,562.20         2006        1,576,562.20  
275              2           3,763,178.18         2005        3,763,178.18  
277              3           3,189,418.37         2005        3,189,418.37  
276              4           4,251,368.55         2005        6,709,904.17  
281              4           2,458,535.62         2005        2,458,535.62  
```  
  
 다음 예에서는 ROWS 절과 함께 UNBOUNDED PRECEDING을 지정합니다. 그 결과 창이 파티션의 첫 번째 행에서 시작됩니다.  
  
```t-sql  
SELECT BusinessEntityID, TerritoryID   
    ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
    ,DATEPART(yy,ModifiedDate) AS SalesYear  
    ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                             ORDER BY DATEPART(yy,ModifiedDate)   
                                             ROWS UNBOUNDED PRECEDING),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYTD             SalesYear   CumulativeTotal  
---------------- ----------- -------------------- ----------- --------------------  
274              NULL        559,697.56           2005        559,697.56  
287              NULL        519,905.93           2006        1,079,603.50  
285              NULL        172,524.45           2007        1,252,127.95  
283              1           1,573,012.94         2005        1,573,012.94  
280              1           1,352,577.13         2005        2,925,590.07  
284              1           1,576,562.20         2006        4,502,152.27  
275              2           3,763,178.18         2005        3,763,178.18  
277              3           3,189,418.37         2005        3,189,418.37  
276              4           4,251,368.55         2005        4,251,368.55  
281              4           2,458,535.62         2005        6,709,904.17  
  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-the-over-clause-with-the-rownumber-function"></a>5. OVER 절에 ROW_NUMBER 함수 사용  
 다음 예제에서는 할당 된 판매 할당량 한도에 따라 판매 담당자는 ROW_NUMBER를 반환 합니다.  
  
```t-sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(ORDER BY SUM(SalesAmountQuota) DESC) AS RowNumber,  
    FirstName, LastName,   
CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName;  
```  
  
 다음은 결과 집합의 일부입니다.  
  
 ```
 RowNumber  FirstName  LastName            SalesQuota  
 ---------  ---------  ------------------  -------------  
 1          Jillian    Carson              12,198,000.00  
 2          Linda      Mitchell            11,786,000.00  
 3          Michael    Blythe              11,162,000.00  
 4          Jae        Pak                 10,514,000.00  
 ```
 
### <a name="f-using-the-over-clause-with-aggregate-functions"></a>6. OVER 절에 집계 함수 사용  
 다음 예에서는 집계 함수에 OVER 절을 사용 하 여 보여 줍니다. 이 예에서는 OVER 절을 사용 하 여이 하위 쿼리를 사용 하 여 보다 효율적입니다.  
  
```t-sql  
-- Uses AdventureWorks  
  
SELECT SalesOrderNumber AS OrderNumber, ProductKey,   
       OrderQuantity AS Qty,   
       SUM(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Total,  
       AVG(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Avg,  
       COUNT(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Count,  
       MIN(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Min,  
       MAX(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Max  
FROM dbo.FactResellerSales   
WHERE SalesOrderNumber IN(N'SO43659',N'SO43664') AND  
      ProductKey LIKE '2%'  
ORDER BY SalesOrderNumber,ProductKey;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 OrderNumber  Product  Qty  Total  Avg  Count  Min  Max  
 -----------  -------  ---  -----  ---  -----  ---  ---  
 SO43659      218      6    16     3    5      1    6  
 SO43659      220      4    16     3    5      1    6  
 SO43659      223      2    16     3    5      1    6  
 SO43659      229      3    16     3    5      1    6  
 SO43659      235      1    16     3    5      1    6  
 SO43664      229      1     2     1    2      1    1  
 SO43664      235      1     2     1    2      1    1  
 ```
 
 다음 예에서는 OVER 절을 사용 하 여 계산된 된 값에 집계 함수를 보여 줍니다. 공지 여 계산 된 집계 `SalesOrderNumber` 의 각 줄에 대 한 총 판매 주문 백분율로 계산 됩니다 `SalesOrderNumber`합니다.  
  
```t-sql  
-- Uses AdventureWorks  
  
SELECT SalesOrderNumber AS OrderNumber, ProductKey AS Product,   
       OrderQuantity AS Qty,   
       SUM(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Total,  
       CAST(1. * OrderQuantity / SUM(OrderQuantity)   
        OVER(PARTITION BY SalesOrderNumber)   
            *100 AS DECIMAL(5,2)) AS PctByProduct  
FROM dbo.FactResellerSales   
WHERE SalesOrderNumber IN(N'SO43659',N'SO43664') AND  
      ProductKey LIKE '2%'  
ORDER BY SalesOrderNumber,ProductKey;  
```  
  
 이 결과 집합의 첫 번째 시작이 됩니다.  
  
 ```
 OrderNumber  Product  Qty  Total  PctByProduct  
 -----------  -------  ---  -----  ------------  
 SO43659      218      6    16     37.50  
 SO43659      220      4    16     25.00  
 SO43659      223      2    16     12.50  
 SO43659      229      2    16     18.75  
 ```
 
## <a name="see-also"></a>관련 항목:  
 [집계 함수 &#40; Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [분석 함수 &#40; Transact SQL &#41;](../../t-sql/functions/analytic-functions-transact-sql.md)   
 [Sqlmag.com, Itzik Ben Gan 여에 창 함수와 조치에 대 한 뛰어난 블로그 게시물](http://sqlmag.com/sql-server-2012/how-use-microsoft-sql-server-2012s-window-functions-part-1)  
  
  

