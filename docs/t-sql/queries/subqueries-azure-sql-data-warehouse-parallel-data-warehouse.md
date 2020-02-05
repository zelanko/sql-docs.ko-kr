---
title: 하위 쿼리
description: Azure SQL Data Warehouse 및 병렬 데이터 웨어하우스의 하위 쿼리
ms.custom: seo-lt-2019
titleSuffix: Azure SQL Data Warehouse
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 0e8ebd60-1936-48c9-b2b9-e099c8269fcf
author: shkale-msft
ms.author: shkale
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c8f60ee25f00c4b9ba4b7959a6447e11a0f549b1
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75244826"
---
# <a name="subqueries-azure-sql-data-warehouse-parallel-data-warehouse"></a>하위 쿼리(Azure SQL Data Warehouse, 병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  이 항목에는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 하위 쿼리를 사용한 예제가 나와 있습니다.  
  
 SELECT 문의 경우 [SELECT&#40;TRANSACT-SQL&#41;](../../t-sql/queries/select-transact-sql.md)을 참조하세요.  
  
## <a name="contents"></a>콘텐츠  
  
-   [기본 사항](#Basics)  
  
-   [예: SQL Data Warehouse 및 병렬 데이터 웨어하우스](#Examples)  
  
##  <a name="Basics"></a> 기본 사항  
 하위 쿼리  
 하위 쿼리는 SELECT, INSERT, UPDATE, DELETE 문이나 다른 하위 쿼리 내부에 중첩된 쿼리입니다. 또한 내부 쿼리 또는 내부 선택이 호출됩니다.  
  
 외부 쿼리  
 하위 쿼리를 포함하는 명령문입니다. 또한 외부 선택이 호출됩니다.  
  
 상호 관련된 하위 쿼리  
 외부 쿼리의 테이블을 참조하는 하위 쿼리입니다.  
  
##  <a name="Examples"></a> 예제: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 이 섹션에서는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 지원되는 하위 쿼리의 예제를 제공합니다.  
  
### <a name="a-top-and-order-by-in-a-subquery"></a>A. 하위 쿼리에서 TOP 및 ORDER BY  
  
```  
SELECT * FROM tblA  
WHERE col1 IN  
    (SELECT TOP 100 col1 FROM tblB ORDER BY col1);  
  
```  
  
### <a name="b-having-clause-with-a-correlated-subquery"></a>B. 상호 관련된 하위 쿼리가 있는 HAVING 절  
  
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
  
### <a name="c-correlated-subqueries-with-analytics"></a>C. 분석이 포함된 상호 관련된 하위 쿼리  
  
```  
SELECT * FROM ReplA AS A   
WHERE A.ID IN   
    (SELECT sum(B.ID2) OVER() FROM ReplB AS B WHERE A.ID2 = B.ID);  
```  
  
### <a name="d-correlated-union-statements-in-a-subquery"></a>D. 하위 쿼리의 상호 관련된 통합 문  
  
```  
SELECT * FROM RA   
WHERE EXISTS   
    (SELECT 1 FROM RB WHERE RB.b1 = RA.a1   
     UNION ALL SELECT 1 FROM RC);  
```  
  
### <a name="e-join-predicates-in-a-subquery"></a>E. 하위 쿼리의 조인 조건자  
  
```  
SELECT * FROM RA INNER JOIN RB   
    ON RA.a1 = (SELECT COUNT(*) FROM RC);  
```  
  
### <a name="f-correlated-join-predicates-in-a-subquery"></a>F. 하위 쿼리의 상호 관련된 조인 조건자  
  
```  
SELECT * FROM RA   
    WHERE RA.a2 IN   
    (SELECT 1 FROM RB INNER JOIN RC ON RA.a1=RB.b1+RC.c1);  
```  
  
### <a name="g-correlated-subselects-as-data-sources"></a>G. 데이터 원본으로 상호 관련된 하위 SELECT  
  
```  
SELECT * FROM RA   
    WHERE 3 = (SELECT COUNT(*)   
        FROM (SELECT b1 FROM RB WHERE RB.b1 = RA.a1) X);  
```  
  
### <a name="h-correlated-subqueries-in-the-data-values--used-with-aggregates"></a>H. 집계를 사용한 데이터 값의 상호 관련된 하위 쿼리  
  
```  
SELECT Rb.b1, (SELECT RA.a1 FROM RA WHERE RB.b1 = RA.a1) FROM RB GROUP BY RB.b1;  
```  
  
### <a name="i-using-in-with-a-correlated-subquery"></a>9\. 상호 관련된 하위 쿼리가 있는 IN 사용  
 다음 예에서는 상관 또는 반복 하위 쿼리에 `IN`을 사용합니다. 이것은 외부 쿼리에 따라 해당 값이 달라지는 쿼리입니다. 내부 쿼리는 외부 쿼리에서 선택한 각 행마다 한 번씩 반복적으로 실행됩니다. 이 `EmployeeKey` 테이블에서 `OrderQuantity`가 `FactResellerSales`이고 `5` 및 `DimEmployee` 테이블에서 직원 ID 번호가 일치하는 각 직원의 `FactResellerSales`와 이름 및 성의 인스턴스 하나를 검색합니다.  
  
```  
SELECT DISTINCT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
WHERE 5 IN   
    (SELECT OrderQuantity  
    FROM FactResellerSales AS frs  
    WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
```  
  
### <a name="j-using-exists-versus-in-with-a-subquery"></a>J. 하위 쿼리와 함께 EXISTS 대 IN 사용  
 다음 예에서는 기능상 동일한 쿼리를 보여 주고 `EXISTS` 키워드와 `IN` 키워드를 사용할 때의 차이점에 대해 설명합니다. 모두 제품 하위 범주가 `Road Bikes`인 각 제품 이름의 인스턴스 하나를 검색하는 하위 쿼리의 예입니다. `ProductSubcategoryKey`는 `DimProduct` 및 `DimProductSubcategory` 테이블 간에 일치합니다.  
  
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
  
### <a name="k-using-multiple-correlated-subqueries"></a>11. 여러 상호 관련된 하위 쿼리 사용  
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
  
  
