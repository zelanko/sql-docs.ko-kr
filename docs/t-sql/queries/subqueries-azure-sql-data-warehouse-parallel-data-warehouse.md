---
title: "하위 쿼리 (Azure SQL 데이터 웨어하우스, 병렬 데이터 웨어하우스) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e8ebd60-1936-48c9-b2b9-e099c8269fcf
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b30ff820d9a9003a1832c8b4226adf20072fceb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="subqueries-azure-sql-data-warehouse-parallel-data-warehouse"></a>하위 쿼리 (Azure SQL 데이터 웨어하우스, 병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  이 항목의 하위 쿼리를 사용 하 여 예제가 나와 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.  
  
 SELECT 문에서 참조 [select&#40; Transact SQL &#41;](../../t-sql/queries/select-transact-sql.md)  
  
## <a name="contents"></a>내용  
  
-   [기본 사항](#Basics)  
  
-   [예: SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스](#Examples)  
  
##  <a name="Basics"></a>기본 사항  
 하위 쿼리  
 하위 쿼리는 SELECT, INSERT, UPDATE, DELETE 문이나 다른 하위 쿼리 내부에 중첩된 쿼리입니다. 내부 쿼리 또는 내부 선택이 호출 또한 됩니다.  
  
 외부 쿼리  
 하위 쿼리를 포함 하는 문입니다. 이 외부 select을 라고도 합니다.  
  
 상관된 하위 쿼리  
 외부 쿼리의 테이블을 참조 하는 하위 쿼리.  
  
##  <a name="Examples"></a>예: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 이 섹션에서는 지원 되는 하위 쿼리의 예제를 제공 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.  
  
### <a name="a-top-and-order-by-in-a-subquery"></a>1. TOP 및 하위 쿼리에서 ORDER BY  
  
```  
SELECT * FROM tblA  
WHERE col1 IN  
    (SELECT TOP 100 col1 FROM tblB ORDER BY col1);  
  
```  
  
### <a name="b-having-clause-with-a-correlated-subquery"></a>2. HAVING 절의 상관된 하위 쿼리 사용  
  
```  
SELECT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
GROUP BY dm.EmployeeKey, dm.FirstName, dm.LastName  
HAVING 5000 <=   
(SELECT sum(OrderQuantity)  
FROM FactResellerSales AS frs  
WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
  
```  
  
### <a name="c-correlated-subqueries-with-analytics"></a>3. 분석을 상관된 하위 쿼리  
  
```  
SELECT * FROM ReplA AS A   
WHERE A.ID IN   
    (SELECT sum(B.ID2) OVER() FROM ReplB AS B WHERE A.ID2 = B.ID);  
```  
  
### <a name="d-correlated-union-statements-in-a-subquery"></a>4. 하위 쿼리에 union 상관 관계가 지정 된 문  
  
```  
SELECT * FROM RA   
WHERE EXISTS   
    (SELECT 1 FROM RB WHERE RB.b1 = RA.a1   
     UNION ALL SELECT 1 FROM RC);  
```  
  
### <a name="e-join-predicates-in-a-subquery"></a>5. 하위 쿼리에 이러한  
  
```  
SELECT * FROM RA INNER JOIN RB   
    ON RA.a1 = (SELECT COUNT(*) FROM RC);  
```  
  
### <a name="f-correlated-join-predicates-in-a-subquery"></a>6. 하위 쿼리에 상관 관계가 지정 된 조인 조건자  
  
```  
SELECT * FROM RA   
    WHERE RA.a2 IN   
    (SELECT 1 FROM RB INNER JOIN RC ON RA.a1=RB.b1+RC.c1);  
```  
  
### <a name="g-correlated-subselects-as-data-sources"></a>7. 데이터 원본으로 상관 관계가 지정 된 하위 select  
  
```  
SELECT * FROM RA   
    WHERE 3 = (SELECT COUNT(*)   
        FROM (SELECT b1 FROM RB WHERE RB.b1 = RA.a1) X);  
```  
  
### <a name="h-correlated-subqueries-in-the-data-values--used-with-aggregates"></a>8. 집계 된 데이터 값에 상관된 하위 쿼리  
  
```  
SELECT Rb.b1, (SELECT RA.a1 FROM RA WHERE RB.b1 = RA.a1) FROM RB GROUP BY RB.b1;  
```  
  
### <a name="i-using-in-with-a-correlated-subquery"></a>9. 상관된 하위 쿼리를 사용 하 여 사용 하 여  
 다음 예에서는 상관 또는 반복 하위 쿼리에 `IN`을 사용합니다. 이것은 외부 쿼리에 따라 해당 값이 달라지는 쿼리입니다. 내부 쿼리를 반복적으로 실행할 각 행에 대해 한 번씩을 선택할 수는 외부 쿼리에 의해 합니다. 인스턴스 하나를 검색 하는이 쿼리는 `EmployeeKey` 는 각 직원의 성과 이름을 붙인는 `OrderQuantity` 에 `FactResellerSales` 테이블은 `5` 및 직원 id 번호에서 일치 하는 것에 대 한는 `DimEmployee` 및 `FactResellerSales` 테이블입니다.  
  
```  
SELECT DISTINCT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
WHERE 5 IN   
    (SELECT OrderQuantity  
    FROM FactResellerSales AS frs  
    WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
```  
  
### <a name="j-using-exists-versus-in-with-a-subquery"></a>10. 하위 쿼리와 함께 in 및 EXISTS를 사용 하 여  
 다음 예제에서는 의미가 동일한 사용 간의 차이 설명 하는 쿼리는 `EXISTS` 키워드 및 `IN` 키워드입니다. 제품 하위 범주는 각 제품 이름의 인스턴스 하나를 검색 하는 하위 쿼리의 예에 모두 `Road Bikes`합니다. `ProductSubcategoryKey`간에 일치는 `DimProduct` 및 `DimProductSubcategory` 테이블입니다.  
  
```  
SELECT DISTINCT EnglishProductName  
FROM DimProduct AS dp   
WHERE EXISTS  
    (SELECT *  
     FROM DimProductSubcategory AS dps   
     WHERE dp.ProductSubcategoryKey = dps.ProductSubcategoryKey  
           AND dps.EnglishProductSubcategoryName = 'Road Bikes')  
ORDER BY EnglishProductName;  
```  
  
 또는  
  
```  
SELECT DISTINCT EnglishProductName  
FROM DimProduct AS dp   
WHERE dp.ProductSubcategoryKey IN  
    (SELECT ProductSubcategoryKey  
     FROM DimProductSubcategory   
     WHERE EnglishProductSubcategoryName = 'Road Bikes')  
ORDER BY EnglishProductName;  
```  
  
### <a name="k-using-multiple-correlated-subqueries"></a>11. 여러 개의 상관된 하위 쿼리를 사용 하 여  
 다음 예에서는 두 개의 상관 하위 쿼리를 사용하여 특정 제품을 판매한 직원의 이름을 찾습니다.  
  
```  
SELECT DISTINCT LastName, FirstName, e.EmployeeKey  
FROM DimEmployee e JOIN FactResellerSales s ON e.EmployeeKey = s.EmployeeKey  
WHERE ProductKey IN  
(SELECT ProductKey FROM DimProduct WHERE ProductSubcategoryKey IN  
(SELECT ProductSubcategoryKey FROM DimProductSubcategory   
 WHERE EnglishProductSubcategoryName LIKE '%Bikes'))  
ORDER BY LastName  
;  
  
```  
  
  
