---
title: GROUP BY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GROUP
- CUBE
- ROLLUP
- GROUPING_SETS_TSQL
- GROUP BY
- GROUPING SETS
- GROUP_BY_TSQL
- GROUP_TSQL
- CUBE_TSQL
- ROLLUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GROUP BY clause, about GROUP BY clause
- dividing tables into groups
- GROUPING SETS
- GROUP BY clause
- table groups [SQL Server]
- groups [SQL Server], tables divided into groups
- summary values [SQL Server]
ms.assetid: 40075914-6385-4692-b4a5-62fe44ae6cb6
caps.latest.revision: 80
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 47f0a4be2697714c9fa41c632337c5da7863510d
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="select---group-by--transact-sql"></a>SELECT - GROUP BY- Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

대개 각 그룹에서 하나 이상의 집계를 수행하기 위해 쿼리 결과를 행 그룹으로 분할하는 SELECT 문의 절입니다. SELECT 문은 그룹마다 하나의 행을 반환합니다.  
  
## <a name="syntax"></a>구문  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
```  
-- Syntax for SQL Server and Azure SQL Database   
-- ISO-Compliant Syntax  
  
GROUP BY {
      column-expression  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
    | GROUPING SETS ( <grouping_set> [ ,...n ]  )  
    | () --calculates the grand total 
} [ ,...n ] 
 
<group_by_expression> ::=  
      column-expression  
    | ( column-expression [ ,...n ] )    
   
<grouping_set> ::=  
      () --calculates the grand total  
    | <grouping_set_item>  
    | ( <grouping_set_item> [ ,...n ] )  
  
<grouping_set_item> ::=  
      <group_by_expression>  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
  

-- For backward compatibility only.
-- Non-ISO-Compliant Syntax for SQL Server and Azure SQL Database 
  
GROUP BY 
      [ ALL ] column-expression [ ,...n ] 
    | column-expression [ ,...n ] [ WITH { CUBE | ROLLUP } ]   

```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
GROUP BY {
      column-name [ WITH (DISTRIBUTED_AGG) ]  
    | column-expression
} [ ,...n ]

```  
  
## <a name="arguments"></a>인수 
 
### <a name="column-expression"></a>*column-expression*  
열 또는 열에 대한 비집계 계산을 지정합니다. 이 열은 테이블, 파생 테이블 또는 뷰에 속할 수 있습니다. 열은 SELECT 문의 FROM 절에 나타나야 하지만, SELECT 목록에는 나타나지 않아도 됩니다. 

유효한 식은 [식](~/t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.    

열은 SELECT 문의 FROM 절에 나타나야 하지만, SELECT 목록에는 나타나지 않아도 됩니다. 그러나 \<select> 목록의 모든 비집계 식에 있는 각 테이블 또는 뷰의 열은 GROUP BY 목록에 포함되어야 합니다.  
  
다음 문이 허용됩니다.  
  
    ```  
    SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA, ColumnB;  
    SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA, ColumnB;  
    SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    SELECT ColumnA + ColumnB + constant FROM T GROUP BY ColumnA, ColumnB;  
    ```  
  
다음 문이 허용되지 않습니다.  
  
    ```  
    SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    SELECT ColumnA + constant + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    ```  
열 식에 포함될 수 없는 항목은 다음과 같습니다.

- SELECT 목록에 정의된 열 별칭. FROM 절에 정의된 파생 테이블에 대한 열 별칭은 사용할 수 있습니다.
- **text**, **ntext** 또는 **image** 형식의 열. 그러나 text, ntext 또는 image 형식의 열은 유효한 데이터 형식의 값을 반환하는 함수의 인수로 사용할 수 있습니다. 예를 들어 식은 SUBSTRING () 및 CAST ()를 사용할 수 있습니다. 이는 HAVING 절의 식에도 적용됩니다.
- xml 데이터 형식 메서드. xml 데이터 형식 메서드를 사용하는 사용자 정의 함수는 포함할 수 있습니다. xml 데이터 형식 메서드를 사용하는 계산 열은 포함할 수 있습니다. 
- 하위 쿼리 144 오류가 반환됩니다. 
- 인덱싱된 뷰의 열. 
 
### <a name="group-by-column-expression--n-"></a>GROUP BY *column-expression* [ ,...n ] 

하나 이상의 열 식의 목록에 있는 값에 따라 SELECT 문 결과를 그룹화합니다. 

예를 들어 이 쿼리는 Country, Region 및 Sales에 대한 열이 포함된 Sales 테이블을 만듭니다. 네 개의 행을 삽입하고, 이러한 행 중 두 행에는 Country 및 Region에 대해 일치하는 값이 있습니다.  

```
CREATE TABLE Sales ( Country varchar(50), Region varchar(50), Sales int );

INSERT INTO sales VALUES (N'Canada', N'Alberta', 100);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 200);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 300);
INSERT INTO sales VALUES (N'United States', N'Montana', 100);
```
Sales 테이블에 포함된 행은 다음과 같습니다.

| Country | Region | Sales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | British Columbia | 200 |
| Canada | British Columbia | 300 |
| United States | Montana | 100 |

다음 쿼리에서는 Country 및 Region을 그룹화하고, 값의 각 조합에 대한 집계 합계를 반환합니다.  
 
``` 
SELECT Country, Region, SUM(sales) AS TotalSales
FROM Sales
GROUP BY Country, Region;
```
Country 및 Region에 대한 값의 조합이 3개이므로 쿼리 결과에는 3개의 행이 있습니다. Canada와 British Columbia에 대한 TotalSales는 두 행의 합계입니다. 

| Country | Region | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | British Columbia | 500 |
| United States | Montana | 100 |

### <a name="group-by-rollup"></a>GROUP BY ROLLUP

열 식의 각 조합에 대한 그룹을 만듭니다. 또한 결과를 부분합 및 총합계로 "롤업"합니다. 이렇게 하려면 오른쪽에서 왼쪽으로 이동하여 그룹 및 집계를 만드는 열 식의 수를 줄입니다. 

열 순서는 ROLLUP 출력에 영향을 주며, 결과 집합의 행 수에도 영향을 줄 수 있습니다.  

예를 들어 `GROUP BY ROLLUP (col1, col2, col3, col4)`은 다음 목록에 있는 열 식의 각 조합에 대한 그룹을 만듭니다.  

- col1, col2, col3, col4 
- col1, col2, col3, NULL
- col1, col2, NULL, NULL
- col1, NULL, NULL, NULL
- NULL, NULL, NULL, NULL -- 총합계입니다.

이전 예제의 테이블을 사용하면 이 코드에서 단순 GROUP BY 대신 GROUP BY ROLLUP 작업을 실행합니다.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region);
```

쿼리 결과에는 ROLLUP이 없는 단순 GROUP BY와 동일한 집계가 있습니다. 또한 Country의 각 값에 대한 부분합을 만듭니다. 마지막으로 모든 행에 대한 총합계를 제공합니다. 결과는 다음과 같습니다.

| Country | Region | TotalSales |
| :------ | :----- | ---------: |
| Canada | Alberta | 100 |
| Canada | British Columbia | 500 |
| Canada | NULL | 600 |
| United States | Montana | 100 |
| United States | NULL | 100 |
| NULL | NULL | 700 |

### <a name="group-by-cube--"></a>GROUP BY CUBE ( )  

GROUP BY CUBE는 가능한 모든 열 조합에 대한 그룹을 만듭니다. GROUP BY CUBE (a, b)의 경우 결과에는 (a, b), (NULL, b), (a, NULL) 및 (NULL, NULL)의 고유 값에 대한 그룹이 있습니다.

다음 코드에서는 이전 예제의 표를 사용하여 Country 및 Region에 대한 GROUP BY CUBE 작업을 실행합니다. 

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

쿼리 결과에는 (Country, Region), (NULL, Region), (Country, NULL) 및 (NULL, NULL)의 고유 값에 대한 그룹이 있습니다. 결과는 다음과 같습니다.

| Country | Region | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| NULL | Alberta | 100 |
| Canada | British Columbia | 500 |
| NULL | British Columbia | 500 |
| United States | Montana | 100 |
| NULL | Montana | 100 |
| NULL | NULL | 700
| Canada | NULL | 600 |
| United States | NULL | 100 |
   
 ### <a name="group-by-grouping-sets--"></a>GROUP BY GROUPING SETS ( )  
 
GROUPING SETS 옵션은 여러 GROUP BY 절을 하나의 GROUP BY 절로 결합하는 기능을 제공합니다. 결과는 지정한 그룹의 UNION ALL에 해당합니다. 

예를 들어 `GROUP BY ROLLUP (Country, Region)`과 `GROUP BY GROUPING SETS ( ROLLUP (Country, Region) )`는 동일한 결과를 반환합니다. 

GROUPING SETS에 둘 이상의 요소가 있는 경우 결과는 요소의 합집합입니다. 다음 예제에서는 Country 및 Region에 대한 ROLLUP 및 CUBE 결과의 합집합을 반환합니다.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( ROLLUP (Country, Region), CUBE (Country, Region) );
```

결과는 두 GROUP BY 문의 합집합을 반환하는 다음 쿼리와 동일합니다.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region)
UNION ALL
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region)
;
```

SQL은 GROUPING SETS 목록에 대해 생성된 중복 그룹을 통합하지 않습니다. 예를 들어 `GROUP BY ( (), CUBE (Country, Region) )`에서 두 요소는 모두 총합계에 대한 행을 반환하고, 두 행이 모두 결과에 나열됩니다. 

 ### <a name="group-by-"></a>GROUP BY ()  
총합계를 생성하는 빈 그룹을 지정합니다. 이는 GROUPING SET의 요소 중 하나로 유용합니다. 예를 들어 다음 명령문은 각 국가에 대한 총 판매액을 제공한 다음, 모든 국가에 대한 총 판매액을 제공합니다.

```
SELECT Country, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( Country, () );
```

### <a name="group-by--all--column-expression--n-"></a>GROUP BY [ ALL ] column-expression [ ,...n ] 

적용 대상: SQL Server 및 Azure SQL Database

참고: 이 구문은 이전 버전과의 호환성을 위해서만 제공됩니다. 이후 버전에서는 제거됩니다. 새 개발 작업에서는 이 구문을 사용하지 말고, 현재 이 구문을 사용하는 응용 프로그램을 수정하세요.

WHERE 절의 검색 조건에 맞는지 여부에 관계없이 결과에 모든 그룹을 포함하도록 지정합니다. 검색 조건에 맞지 않는 그룹은 집계에서 NULL을 가집니다. 

GROUP BY ALL:
- 쿼리에 WHERE 절이 있는 경우 원격 테이블을 액세스하는 쿼리에는 지원되지 않습니다.
- FILESTREAM 특성이 있는 열에서 실패합니다.
  
### <a name="with-distributedagg"></a>WITH (DISTRIBUTED_AGG)
적용 대상: Azure SQL Data Warehouse 및 병렬 데이터 웨어하우스

DISTRIBUTED_AGG 쿼리 힌트는 집계를 수행하기 전에 MPP(Massively Parallel Processing) 시스템에서 특정 열에 테이블을 다시 배포하도록 합니다. GROUP BY 절에 있는 하나의 열만 DISTRIBUTED_AGG 쿼리 힌트를 가질 수 있습니다. 쿼리가 완료되면 다시 배포된 테이블이 삭제됩니다. 원래 테이블은 변경되지 않습니다.  

참고: DISTRIBUTED_AGG 쿼리 힌트는 이전 버전의 병렬 데이터 웨어하우스와의 호환성을 위해 제공되며, 대부분의 쿼리에 대한 성능이 향상되지 않습니다. 기본적으로 MPP는 집계 성능을 향상시키기 위해 이미 필요에 따라 데이터를 다시 배포합니다. 
  
## <a name="general-remarks"></a>일반적인 주의 사항

### <a name="how-group-by-interacts-with-the-select-statement"></a>GROUP BY와 SELECT 문이 상호 작용하는 방법
SELECT 목록:
- 벡터 집계. 집계 함수가 SELECT 목록에 포함되어 있으면 GROUP BY는 각 그룹에 대한 요약 값을 계산합니다. 이를 벡터 집계라고 합니다. 
- Distinct 집계. AVG (DISTINCT *column_name*), COUNT (DISTINCT *column_name*) 및 SUM (DISTINCT *column_name*) 집계 함수에서 ROLLUP, CUBE 및 GROUPING SETS를 지원합니다.
  
WHERE 절:
- SQL에서 그룹화 작업을 수행하기 전에 WHERE 절의 조건에 맞지 않은 행을 제거합니다.  
  
HAVING 절:
- SQL에서 having 절을 사용하여 결과 집합의 그룹을 필터링합니다. 
  
ORDER BY 절:
- ORDER BY 절을 사용하여 결과 집합의 순서를 지정합니다. GROUP BY 절은 결과 집합의 순서를 지정하지 않습니다. 
  
NULL 값:
- 그룹화 열에 NULL 값이 포함된 경우 모든 NULL 값이 동일한 것으로 간주되어 단일 그룹으로 수집됩니다.   
  
## <a name="limitations-and-restrictions"></a>제한 사항

적용 대상: SQL Server(2008부터) 및 Azure SQL Data Warehouse

### <a name="maximum-capacity"></a>최대 용량

ROLLUP, CUBE 또는 GROUPING SETS를 사용하는 GROUP BY 절의 경우 식의 최대 수는 32개입니다. 그룹의 최대 수는 4,096(2<sup>12</sup>)개입니다. GROUP BY 절에 4,096개가 넘는 그룹이 있으므로 다음 예제에서는 실패합니다.  
 
-   다음 예제에서는 4,097(2<sup>12</sup> + 1)개의 그룹화 집합을 생성하지만 실패합니다.  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), b )  
    ```  
  
-   다음 예제에서는 4,097(2<sup>12</sup> + 1)개의 그룹을 생성하지만 실패합니다. `CUBE ()` 그룹화 집합과 `()` 그룹화 집합 모두 총합계 행을 생성하고 중복된 그룹화 집합은 제거되지 않습니다.  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), ())  
    ```  

-   다음 예제에서는 이전 버전과 호환되는 구문을 사용합니다. 8,192(2<sup>13</sup>)개의 그룹화 집합을 생성하지만 실패합니다.  
  
    ```  
    GROUP BY CUBE (a1, ..., a13)   
    GROUP BY a1, ..., a13 WITH CUBE   
    ```    
    CUBE 또는 ROLLUP이 포함되지 않고 이전 버전과 호환되는 GROUP BY 절의 경우, 항목 별 그룹 수는 GROUP BY 열 크기, 집계 열 및 쿼리에 포함된 집계 값으로 제한됩니다. 이 제한은 중간 작업 테이블이 중간 쿼리 결과를 보유하는 데 필요한 8,060바이트 제한을 기준으로 책정됩니다. CUBE 또는 ROLLUP이 지정될 경우 최대 12개의 그룹화 식이 허용됩니다.

### <a name="support-for-iso-and-ansi-sql-2006-group-by-features"></a>ISO 및 ANSI SQL-2006 GROUP BY 기능 지원

GROUP BY 절은 SQL-2006 표준에 포함된 모든 GROUP BY 기능을 지원하지만, 다음과 같은 구문 예외가 있습니다.  
  
-   명시적 GROUPING SETS 목록의 일부가 아닌 그룹화 집합을 GROUP BY 절에 사용할 수 없습니다. 예를 들어 `GROUP BY Column1, (Column2, ...ColumnN`)은 표준에서 허용되지만, Transact-SQL에서는 허용되지 않습니다.  Transact-SQL은 의미상 동일한 `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))` 및 `GROUP BY Column1, Column2, ... ColumnN`을 지원합니다. 이러한 예는 이전 `GROUP BY` 예와 기능적으로 동일합니다. 이는 `GROUP BY Column1, (Column2, ...ColumnN`)이 의미상 동일하지 않은 `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))`로 잘못 해석될 수 있는 가능성을 방지하기 위한 것입니다.  
  
-   그룹화 집합은 그룹화 집합 내에 사용할 수 없습니다. 예를 들어 `GROUP BY GROUPING SETS (A1, A2,…An, GROUPING SETS (C1, C2, ...Cn))`는 SQL-2006 표준에서 허용되지만, Transact-SQL에서는 허용되지 않습니다. Transact-SQL은 `GROUP BY GROUPING SETS( A1, A2,...An, C1, C2, ...Cn )` 또는 `GROUP BY GROUPING SETS( (A1), (A2), ... (An), (C1), (C2), ... (Cn) )`를 허용합니다. 이는 의미상 첫 번째 GROUP BY 예제와 동일하며 더 명확한 구문을 사용합니다.  
  
-   GROUP BY [ALL/DISTINCT]는 열 식이 포함된 단순 GROUP BY 절에서만 허용됩니다. GROUPING SETS, ROLLUP, CUBE, WITH CUBE 또는 WITH ROLLUP 구조에서는 허용되지 않습니다. ALL은 기본값이며 암시적입니다. 또한 이전 버전과 호환되는 구문에서도 허용됩니다.
  
### <a name="comparison-of-supported-group-by-features"></a>지원되는 GROUP BY 기능 비교  
 다음 표에서는 SQL 버전 및 데이터베이스 호환성 수준에 따라 지원되는 GROUP BY 기능에 대해 설명합니다.  
  
|기능|SQL Server Integration Services|SQL Server 호환성 수준 100 이상|SQL Server 2008 이상(호환성 수준 90).|  
|-------------|-------------------------------------|--------------------------------------------------|-----------------------------------------------------------|  
|DISTINCT 집계|WITH CUBE 또는 WITH ROLLUP에 대해 지원되지 않습니다.|WITH CUBE, WITH ROLLUP, GROUPING SETS, CUBE 또는 ROLLUP에 대해 지원됩니다.|호환성 수준 100과 같습니다.|  
|GROUP BY 절에서 이름이 CUBE 또는 ROLLUP인 사용자 정의 함수|**dbo.cube(***arg1***,***...argN***)** 또는 **dbo.rollup(***arg1***,**...*argN***)** 사용자 정의 함수가 GROUP BY 절에 허용됩니다.<br /><br /> 예: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|**dbo.cube (***arg1***,**...argN **)** 또는 **dbo.rollup(** arg1 **,***...argN***)** 사용자 정의 함수는 GROUP BY 절에 허용되지 않습니다.<br /><br /> 예: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`<br /><br /> "'cube'&#124;'rollup' 키워드 근처의 구문이 잘못되었습니다."라는 오류 메시지가 반환됩니다.<br /><br /> 이 문제를 방지하려면 `dbo.cube`를 `[dbo].[cube]`로 바꾸거나 `dbo.rollup`을 `[dbo].[rollup]`으로 바꿉니다.<br /><br /> 허용되는 예제: `SELECT SUM (x) FROM T  GROUP BY [dbo].[cube](y);`|**dbo.cube (***arg1***,***...argN*) 또는 **dbo.rollup(***arg1***,***...argN***)** 사용자 정의 함수가 GROUP BY 절에 허용됩니다.<br /><br /> 예: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|  
|GROUPING SETS|지원되지 않음|지원됨|지원됨|  
|CUBE|지원되지 않음|지원됨|지원되지 않음|  
|ROLLUP|지원되지 않음|지원됨|지원되지 않음|  
|GROUP BY ()와 같은 총합계|지원되지 않음|지원됨|지원됨|  
|GROUPING_ID 함수|지원되지 않음|지원됨|지원됨|  
|GROUPING 함수|지원됨|지원됨|지원됨|  
|WITH CUBE|지원됨|지원됨|지원됨|  
|WITH ROLLUP|지원됨|지원됨|지원됨|  
|WITH CUBE 또는 WITH ROLLUP "중복된" 그룹화 제거|지원됨|지원됨|지원됨| 
 
  
## <a name="examples"></a>예  
  
### <a name="a-use-a-simple-group-by-clause"></a>1. 단순 GROUP BY 절 사용  
 다음 예에서는 `SalesOrderID` 테이블의 각 `SalesOrderDetail`에 대한 합계를 계산합니다. 이 예제에서는 AdventureWorks를 사용합니다.  
  
```  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail AS sod  
GROUP BY SalesOrderID  
ORDER BY SalesOrderID;  
```  
  
### <a name="b-use-a-group-by-clause-with-multiple-tables"></a>2. 여러 테이블이 포함된 GROUP BY 절 사용  
 다음 예에서는 `City` 테이블에 조인된 `Address` 테이블에서 각 `EmployeeAddress`에 대한 직원 수를 검색합니다. 이 예제에서는 AdventureWorks를 사용합니다. 
  
```  
SELECT a.City, COUNT(bea.AddressID) EmployeeCount  
FROM Person.BusinessEntityAddress AS bea   
    INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
GROUP BY a.City  
ORDER BY a.City;  
```  
  
### <a name="c-use-a-group-by-clause-with-an-expression"></a>3. 식이 포함된 GROUP BY 절 사용  
 다음 예에서는 `DATEPART` 함수를 사용하여 각 연도별 총 판매액을 검색합니다. `SELECT` 목록과 `GROUP BY` 절 모두에 같은 식이 있어야 합니다.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
### <a name="d-use-a-group-by-clause-with-a-having-clause"></a>4. HAVING 절이 포함된 GROUP BY 절 사용  
 다음 예에서는 `HAVING` 절을 사용하여 `GROUP BY` 절에 생성된 그룹 중 결과 집합에 포함되어야 하는 그룹을 지정합니다.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
HAVING DATEPART(yyyy,OrderDate) >= N'2003'  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
## <a name="examples-sql-data-warehouse-and-parallel-data-warehouse"></a>예제: SQL Data Warehouse 및 병렬 데이터 웨어하우스  
  
### <a name="e-basic-use-of-the-group-by-clause"></a>5. GROUP BY 절의 기본적인 사용  
 다음 예제에서는 일별 총 판매액을 모두 찾습니다. 일일 판매의 합계가 모두 포함된 하나의 행이 반환됩니다.  
  
```  
-- Uses AdventureWorksDW  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales FROM FactInternetSales  
GROUP BY OrderDateKey ORDER BY OrderDateKey;  
```  
  
### <a name="f-basic-use-of-the-distributedagg-hint"></a>6. DISTRIBUTED_AGG 힌트의 기본적인 사용  
 다음 예제에서는 집계를 수행하기 전에 DISTRIBUTED_AGG 쿼리 힌트를 사용하여 어플라이언스가 `CustomerKey` 열에 있는 테이블의 순서를 섞도록 합니다.  
  
```  
-- Uses AdventureWorksDW  
  
SELECT CustomerKey, SUM(SalesAmount) AS sas  
FROM FactInternetSales  
GROUP BY CustomerKey WITH (DISTRIBUTED_AGG)  
ORDER BY CustomerKey DESC;  
```  
  
### <a name="g-syntax-variations-for-group-by"></a>7. GROUP BY 구문 변형  
 선택 목록에 집계가 없는 경우 선택 목록의 각 열이 GROUP BY 목록에 포함되어야 합니다. 선택 목록의 계산 열은 GROUP BY 목록에 나열될 수 있지만 필수는 아닙니다. 다음은 구문상 유효한 SELECT 문의 예제입니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName FROM DimCustomer GROUP BY LastName, FirstName;  
SELECT NumberCarsOwned FROM DimCustomer GROUP BY YearlyIncome, NumberCarsOwned;  
SELECT (SalesAmount + TaxAmt + Freight) AS TotalCost FROM FactInternetSales GROUP BY SalesAmount, TaxAmt, Freight;  
SELECT SalesAmount, SalesAmount*1.10 SalesTax FROM FactInternetSales GROUP BY SalesAmount;  
SELECT SalesAmount FROM FactInternetSales GROUP BY SalesAmount, SalesAmount*1.10;  
```  
  
### <a name="h-using-a-group-by-with-multiple-group-by-expressions"></a>8. 여러 GROUP BY 식이 포함된 GROUP BY 사용  
 다음 예제에서는 여러 `GROUP BY` 조건을 사용하여 결과를 그룹화합니다. 각 `OrderDateKey` 그룹 내에서 `DueDateKey`로 구분할 수 있는 하위 그룹이 있는 경우 결과 집합에 대한 새 그룹화가 정의됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, DueDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSalesGROUP BY OrderDateKey, DueDateKey   
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-a-group-by-clause-with-a-having-clause"></a>9. HAVING 절과 함께 GROUP BY 절 사용  
 다음 예제에서는 `HAVING` 절을 사용하여 결과 집합에 포함되어야 하는 `GROUP BY` 절에 생성된 그룹을 지정합니다. 2004년 이후의 주문 날짜가 있는 그룹만 결과에 포함됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING OrderDateKey > 20040000   
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>참고 항목  
 [GROUPING_ID&#40;Transact-SQL&#41;](~/t-sql/functions/grouping-id-transact-sql.md)   
 [GROUPING&#40;Transact-SQL&#41;](~/t-sql/functions/grouping-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)   
 [SELECT 절&#40;Transact-SQL&#41;](~/t-sql/queries/select-clause-transact-sql.md)  
  
  




