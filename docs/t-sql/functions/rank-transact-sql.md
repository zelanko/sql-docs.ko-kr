---
title: RANK(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RANK
- RANK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row ranking [SQL Server]
- tied rows [SQL Server]
- ranking rows
- RANK function [Transact-SQL]
ms.assetid: 2d96f6d2-5db7-4b3c-a63e-213c58e4af55
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1aa1ab1466776af502249c43d005af896827de85
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003759"
---
# <a name="rank-transact-sql"></a>RANK(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

결과 집합의 파티션 내에 있는 각 행의 순위를 반환합니다. 요청한 행의 순위는 해당 행 앞에 있는 행의 순위에 1을 더한 값입니다.  

ROW_NUMBER와 RANK는 유사합니다. ROW_NUMBER는 모든 행을 순차적으로 번호 지정합니다.(예: 1, 2, 3, 4, 5) RANK는 순위 동률(예: 1, 2, 2, 4, 5)에 대해 동일한 숫자 값을 제공합니다.   
  
> [!NOTE]
> RANK는 쿼리를 실행할 때 계산되는 임시 값입니다. 테이블의 숫자를 유지하려면 [IDENTITY 속성](../../t-sql/statements/create-table-transact-sql-identity-property.md) 및 [SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md)를 참조하세요. 
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
RANK ( ) OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
## <a name="arguments"></a>인수  
 OVER **(** [ _partition\_by\_clause_ ] _order\_by\_clause_ **)**  
 *partition_by_clause*는 FROM 절이 생성한 결과 집합을 함수가 적용되는 파티션으로 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. _order\_by\_clause_는 함수를 적용하기 전에 데이터의 순서를 결정합니다. *order_by_clause*가 필요합니다. OVER 절의 \<rows or range clause/>는 RANK 함수에 지정할 수 없습니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.  
  
## <a name="return-types"></a>반환 형식  
 **bigint**  
  
## <a name="remarks"></a>설명  
 하나의 순위에 둘 이상의 행이 결합되면 결합된 각 행은 동일한 순위를 갖게 됩니다. 예를 들어 성과가 가장 좋은 두 명의 판매 직원이 같은 SalesYTD 값을 갖는 경우 둘 다 1로 순위가 지정됩니다. 다음으로 높은 SalesYTD를 갖는 판매 직원은 더 높은 순위를 가진 행이 두 개이기 때문에 3위로 순위가 지정됩니다. 따라서 RANK 함수는 항상 연속적인 정수를 반환하지는 않습니다.  
  
 전체 쿼리에 사용되는 정렬 순서는 행이 결과 집합에 표시되는 순서를 결정합니다.  
  
 RANK는 비결정적입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
  
### <a name="a-ranking-rows-within-a-partition"></a>A. 파티션 내의 행 순위 지정  
 다음 예에서는 재고 수량을 기준으로 지정한 인벤토리 위치의 제품에 순위를 부여합니다. 결과 집합은 `LocationID`를 기준으로 분할되고 `Quantity`를 기준으로 논리적으로 정렬됩니다. 제품 494와 495는 수량이 동일합니다. 두 제품은 서로 연결되어 있으므로 동일하게 순위 1이 부여됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT i.ProductID, p.Name, i.LocationID, i.Quantity  
    ,RANK() OVER   
    (PARTITION BY i.LocationID ORDER BY i.Quantity DESC) AS Rank  
FROM Production.ProductInventory AS i   
INNER JOIN Production.Product AS p   
    ON i.ProductID = p.ProductID  
WHERE i.LocationID BETWEEN 3 AND 4  
ORDER BY i.LocationID;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```sql  
  
ProductID   Name                   LocationID   Quantity Rank  
----------- ---------------------- ------------ -------- ----  
494         Paint - Silver         3            49       1  
495         Paint - Blue           3            49       1  
493         Paint - Red            3            41       3  
496         Paint - Yellow         3            30       4  
492         Paint - Black          3            17       5  
495         Paint - Blue           4            35       1  
496         Paint - Yellow         4            25       2  
493         Paint - Red            4            24       3  
492         Paint - Black          4            14       4  
494         Paint - Silver         4            12       5  
 (10 row(s) affected)  
```  
  
### <a name="b-ranking-all-rows-in-a-result-set"></a>B. 결과 집합의 모든 행 순위 지정  
 다음 예제에서는 연봉이 상위 10위권에 들어가는 직원을 반환합니다. PARTITION BY 절을 지정하지 않았으므로 결과 집합의 모든 행에 RANK 함수가 적용되었습니다.  
  
```sql  
USE AdventureWorks2012  
SELECT TOP(10) BusinessEntityID, Rate,   
       RANK() OVER (ORDER BY Rate DESC) AS RankBySalary  
FROM HumanResources.EmployeePayHistory AS eph1  
WHERE RateChangeDate = (SELECT MAX(RateChangeDate)   
                        FROM HumanResources.EmployeePayHistory AS eph2  
                        WHERE eph1.BusinessEntityID = eph2.BusinessEntityID)  
ORDER BY BusinessEntityID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```sql  
BusinessEntityID Rate                  RankBySalary  
---------------- --------------------- --------------------  
1                125.50                1  
2                63.4615               4  
3                43.2692               8  
4                29.8462               19  
5                32.6923               16  
6                32.6923               16  
7                50.4808               6  
8                40.8654               10  
9                40.8654               10  
10               42.4808               9  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-ranking-rows-within-a-partition"></a>C: 파티션 내의 행 순위 지정  
 다음 예는 총 판매액에 따라 각 영업 지역에서 영업 담당자의 순위를 매깁니다. 행 집합은 `SalesTerritoryGroup`별로 분할되며 `SalesAmountQuota`를 기준으로 정렬됩니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryRegion,  
    RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```sql
LastName          TotalSales     SalesTerritoryRegion  RankResult
----------------  -------------  -------------------  --------
Tsoflias          1687000.0000   Australia            1
Saraiva           7098000.0000   Canada               1
Vargas            4365000.0000   Canada               2
Carson            12198000.0000  Central              1
Varkey Chudukatil 5557000.0000   France               1
Valdez            2287000.0000   Germany              1
Blythe            11162000.0000  Northeast            1
Campbell          4025000.0000   Northwest            1
Ansman-Wolfe      3551000.0000   Northwest            2
Mensa-Annan       2753000.0000   Northwest            3
Reiter            8541000.0000   Southeast            1
Mitchell          11786000.0000  Southwest            1
Ito               7804000.0000   Southwest            2
Pak               10514000.0000  United Kingdom       1
```  
  
## <a name="see-also"></a>참고 항목  
 [DENSE_RANK&#40;Transact-SQL&#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [ROW_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/row-number-transact-sql.md)   
 [NTILE&#40;Transact-SQL&#41;](../../t-sql/functions/ntile-transact-sql.md)   
 [순위 함수&#40;Transact-SQL&#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  



