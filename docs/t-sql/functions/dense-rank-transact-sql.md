---
title: DENSE_RANK (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DENSE_RANK_TSQL
- DENSE_RANK
dev_langs:
- TSQL
helpviewer_keywords:
- row ranking [SQL Server]
- DENSE_RANK function
- tied rows [SQL Server]
- ranking rows
ms.assetid: 03871fc6-9592-4016-b0b2-ff543f132b20
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4897ba682387179ad305657215afce9cde3e5a70
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="denserank-transact-sql"></a>DENSE_RANK(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  결과 집합 파티션 내 행의 순위를 순위 간격 없이 반환합니다. 행의 순위는 바로 앞 행의 순위에 1을 더한 것입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DENSE_RANK ( ) OVER ( [ <partition_by_clause> ] < order_by_clause > )  
```  
  
## <a name="arguments"></a>인수  
 \<partition_by_clause >  
 생성 한 결과 집합을 나눕니다는 [FROM](../../t-sql/queries/from-transact-sql.md) DENSE_RANK 함수가 적용 되는 절을으로 분할 합니다. PARTITION BY 구문은 참조 [OVER 절 &#40; Transact SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 \<order_by_clause >  
 DENSE_RANK 함수가 파티션 내의 행에 적용되는 순서를 결정합니다.  
  
## <a name="return-types"></a>반환 형식  
 **bigint**  
  
## <a name="remarks"></a>주의  
 같은 파티션에서 한 순위에 두 개 이상의 행이 연결된 경우 연결된 각 행에는 같은 순위가 지정됩니다. 예를 들어 성과가 가장 좋은 두 명의 판매 직원이 같은 SalesYTD 값을 갖는 경우 둘 다 1로 순위가 지정됩니다. 다음으로 높은 SalesYTD 값을 갖는 판매 직원이 순위 2로 지정됩니다. 이는 해당 행 앞에 오는 개별 행의 수보다 하나 더 큰 값입니다. 따라서 DENSE_RANK 함수가 반환하는 수는 간격 없이 항상 연속적인 순위를 갖게 됩니다.  
  
 전체 쿼리에 사용되는 정렬 순서는 결과에 나타나는 행의 순서를 결정합니다. 이는 순위 1로 지정된 행이 반드시 파티션에서 첫 번째 행일 필요는 없음을 의미합니다.  
  
 DENSE_RANK는 비결정적입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-ranking-rows-within-a-partition"></a>1. 파티션 내의 행 순위 지정  
 다음 예에서는 재고 수량을 기준으로 지정한 인벤토리 위치의 제품에 순위를 부여합니다. 결과 집합은 `LocationID`를 기준으로 분할되고 `Quantity`를 기준으로 논리적으로 정렬됩니다. 제품 494와 495는 수량이 동일합니다. 두 제품은 서로 연결되어 있으므로 동일하게 순위 1이 부여됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT i.ProductID, p.Name, i.LocationID, i.Quantity  
    ,DENSE_RANK() OVER   
    (PARTITION BY i.LocationID ORDER BY i.Quantity DESC) AS Rank  
FROM Production.ProductInventory AS i   
INNER JOIN Production.Product AS p   
    ON i.ProductID = p.ProductID  
WHERE i.LocationID BETWEEN 3 AND 4  
ORDER BY i.LocationID;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ProductID   Name                               LocationID Quantity Rank  
----------- ---------------------------------- ---------- -------- -----  
494         Paint - Silver                     3          49       1  
495         Paint - Blue                       3          49       1  
493         Paint - Red                        3          41       2  
496         Paint - Yellow                     3          30       3  
492         Paint - Black                      3          17       4  
495         Paint - Blue                       4          35       1  
496         Paint - Yellow                     4          25       2  
493         Paint - Red                        4          24       3  
492         Paint - Black                      4          14       4  
494         Paint - Silver                     4          12       5  
  
(10 row(s) affected)  
  
```  
  
### <a name="b-ranking-all-rows-in-a-result-set"></a>2. 결과 집합의 모든 행 순위 지정  
 다음 예제에서는 연봉이 상위 10위권에 들어가는 직원을 반환합니다. PARTITION BY 절을 지정하지 않았으므로 결과 집합의 모든 행에 DENSE_RANK 함수가 적용되었습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TOP(10) BusinessEntityID, Rate,   
       DENSE_RANK() OVER (ORDER BY Rate DESC) AS RankBySalary  
FROM HumanResources.EmployeePayHistory;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID Rate                  RankBySalary  
---------------- --------------------- --------------------  
1                125.50                1  
25               84.1346               2  
273              72.1154               3  
2                63.4615               4  
234              60.0962               5  
263              50.4808               6  
7                50.4808               6  
234              48.5577               7  
285              48.101                8  
274              48.101                8  
```  
  
## <a name="c-four-ranking-functions-used-in-the-same-query"></a>3. 같은 쿼리에서 사용 되는 4 개의 순위 함수  
 다음은 동일한 쿼리에 사용된 4가지 순위 함수를 보여 줍니다. 함수별 예에 대한 자세한 내용은 각 순위 함수를 참조하십시오.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,ROW_NUMBER() OVER (ORDER BY a.PostalCode) AS "Row Number"  
    ,RANK() OVER (ORDER BY a.PostalCode) AS Rank  
    ,DENSE_RANK() OVER (ORDER BY a.PostalCode) AS "Dense Rank"  
    ,NTILE(4) OVER (ORDER BY a.PostalCode) AS Quartile  
    ,s.SalesYTD  
    ,a.PostalCode  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL AND SalesYTD <> 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|FirstName|LastName|Row Number|Rank|Dense Rank|Quartile|SalesYTD|PostalCode|  
|---------------|--------------|----------------|----------|----------------|--------------|--------------|----------------|  
|Michael|Blythe|1.|1|1|1.|4557045.0459|98027|  
|Linda|Mitchell|2|1|1|1.|5200475.2313|98027|  
|Jillian|Carson|3|1|1|1.|3857163.6332|98027|  
|Garrett|Vargas|4|1|1|1.|1764938.9859|98027|  
|Tsvi|Reiter|5|1.|1|2|2811012.7151|98027|  
|Shu|Ito|6|6|2|2|3018725.4858|98055|  
|José|Saraiva|7|6|2|2|3189356.2465|98055|  
|David|Campbell|8|6|2|3|3587378.4257|98055|  
|Tete|Mensa-Annan|9|6|2|3|1931620.1835|98055|  
|Lynn|Tsoflias|10|6|2|3|1758385.926|98055|  
|Rachel|Valdez|11|6|2|4|2241204.0424|98055|  
|Jae|Pak|12|6|2|4|5015682.3752|98055|  
|Ranjit|Varkey Chudukatil|13|6|2|4|3827950.238|98055| 


## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-ranking-rows-within-a-partition"></a>D:에는 파티션 내의 행 순위 지정  
 다음 예에서는 순위 총 판매액에 따라 각 영업 지역에 영업 담당자를 지정 합니다. 행 집합은 `SalesTerritoryGroup`별로 분할되며 `SalesAmountQuota`를 기준으로 정렬됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryGroup,  
    DENSE_RANK() OVER (PARTITION BY SalesTerritoryGroup ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryGroup != N'NA'  
GROUP BY LastName,SalesTerritoryGroup;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
 LastName          TotalSales     SalesTerritoryGroup  RankResult  
----------------  -------------  -------------------  --------  
Pak               10514000.0000  Europe               1  
Varkey Chudukatil  5557000.0000  Europe               2  
Valdez             2287000.0000  Europe               3  
Carson            12198000.0000  North America        1  
Mitchell          11786000.0000  North America        2  
Blythe            11162000.0000  North America        3  
Reiter             8541000.0000  North America        4  
Ito                7804000.0000  North America        5  
Saraiva            7098000.0000  North America        6  
Vargas             4365000.0000  North America        7  
Campbell           4025000.0000  North America        8  
Ansman-Wolfe       3551000.0000  North America        9  
Mensa-Annan        2753000.0000  North America        10  
Tsoflias           1687000.0000  Pacific              1 
```  

## <a name="see-also"></a>관련 항목:  
 [순위 &#40; Transact SQL &#41;](../../t-sql/functions/rank-transact-sql.md)   
 [ROW_NUMBER &#40; Transact SQL &#41;](../../t-sql/functions/row-number-transact-sql.md)   
 [NTILE &#40; Transact SQL &#41;](../../t-sql/functions/ntile-transact-sql.md)   
 [순위 함수 &#40; Transact SQL &#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [함수](../../t-sql/functions/functions.md)  
  
  


