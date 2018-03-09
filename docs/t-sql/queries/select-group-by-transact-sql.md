---
title: GROUP BY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5e99efe49620003de40659dd4bfd959dacef986c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="select---group-by--transact-sql"></a>선택-그룹 BY-TRANSACT-SQL
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

각 그룹에 하나 이상의 집계를 수행 하기 위해 일반적으로 행 그룹으로 쿼리 결과 분할 하는 SELECT 문 절. SELECT 문은 그룹 마다 하나의 행을 반환 합니다.  
  
## <a name="syntax"></a>구문  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
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
열에는 열 또는 비 집계 계산을 지정합니다. 이 열은 테이블, 파생된 테이블 또는 뷰에 속할 수 있습니다. 열 SELECT 문의 FROM 절에 표시 되어야 하지만 SELECT 목록에 표시 하는 데 필요 하지 않습니다. 

유효한 식에 대 한 참조 [식](~/t-sql/language-elements/expressions-transact-sql.md)합니다.    

열 SELECT 문의 FROM 절에 표시 되어야 하지만 SELECT 목록에 표시 하는 데 필요 하지 않습니다. 그러나 각 테이블 또는 열에 있는 모든 비 집계 식에서 볼 수는 \<선택 > 목록 GROUP BY 목록에 포함 되어야 합니다.  
  
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
열 식을 포함할 수 없습니다.

- SELECT 목록에 정의 된 열 별칭입니다. FROM 절에 정의 된 파생된 테이블에 대 한 열 별칭을 사용할 수 있습니다.
- 형식의 열 **텍스트**, **ntext**, 또는 **이미지**합니다. 그러나 올바른 데이터 형식의 값을 반환 하는 함수에 인수로 text, ntext 또는 image 열을 사용할 수 있습니다. 예를 들어, substring ()와 CAST () 사용할 수 있습니다. HAVING 절에서는 식에도 적용 됩니다.
- xml 데이터 형식 메서드를 사용 합니다. Xml 데이터 형식 메서드를 사용 하는 사용자 정의 함수를 포함할 수 있습니다. Xml 데이터 형식 메서드를 사용 하는 계산된 열을 포함할 수 있습니다. 
- 하위 쿼리 144 오류가 반환 됩니다. 
- 인덱싱된 뷰에서 열입니다. 
 
### <a name="group-by-column-expression--n-"></a>GROUP BY *열 식을* [,...n] 

하나 이상의 열 식의 목록에서 값에 따라 SELECT 문의 결과 그룹화합니다. 

예를 들어이 쿼리 국가, 지역 및 판매에 대 한 열이 있는 Sales 테이블을 만듭니다. 4 개의 행을 삽입 하 고 국가 및 지역에 대 한 일치 하는 값이 있는 행의 두 합니다.  

```
CREATE TABLE Sales ( Country varchar(50), Region varchar(50), Sales int );

INSERT INTO sales VALUES (N'Canada', N'Alberta', 100);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 200);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 300);
INSERT INTO sales VALUES (N'United States', N'Montana', 100);
```
Sales 테이블에이 행을이 포함 되어 있습니다.

| Country | Region | Sales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | 브리티시 콜롬비아 | 200 |
| Canada | 브리티시 콜롬비아 | 300 |
| United States | 몬테나 | 100 |

이 다음 쿼리는 국가 및 지역 그룹화 하 고 값의 각 조합에 대 한 집계 합계를 반환 합니다.  
 
``` 
SELECT Country, Region, SUM(sales) AS TotalSales
FROM Sales
GROUP BY Country, Region;
```
쿼리 결과 행이 세 국가 및 지역에 대 한 값을 3 조합 있기 때문입니다. 캐나다 및 브리티시 콜롬비아에 대 한 TotalSales 두 행의 합계입니다. 

| Country | Region | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | 브리티시 콜롬비아 | 500 |
| United States | 몬테나 | 100 |

### <a name="group-by-rollup"></a>그룹 롤업

열 식의 각 조합에 대 한 그룹을 만듭니다. 또한 것 "12" 결과 부분합 및 총합계를 합니다. 이 수행 하려면 오른쪽에서 그룹 및는 aggregation(s) 생성 하는 열 식의 수를 줄이거나 왼쪽으로 이동 합니다. 

열 순서 롤업 출력 미치며 결과 집합의 행 수에 영향을 줄 수 있습니다.  

예를 들어 `GROUP BY ROLLUP (col1, col2, col3, col4)` 다음 목록의 열 식의 각 조합에 대 한 그룹을 만듭니다.  

- col1, col2, col3, col4 
- col1, col2, col3, NULL
- col1, col2, NULL, NULL
- col1, NULL, NULL, NULL
- 이 총합계 NULL, NULL, NULL, NULL-

이 코드에서는 이전 예제의 테이블을 사용 하는 단순 GROUP BY 대신 GROUP BY ROLLUP 작업을 실행 합니다.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region);
```

쿼리 결과는 단순 GROUP BY 롤업을 없이으로 동일한 집계. 또한 Country의 각 값에 대 한 부분합을 만듭니다. 마지막으로 모든 행에 대 한 총합계를 제공 합니다. 결과 다음과 같습니다.

| Country | Region | TotalSales |
| :------ | :----- | ---------: |
| Canada | Alberta | 100 |
| Canada | 브리티시 콜롬비아 | 500 |
| Canada | NULL | 600 |
| United States | 몬테나 | 100 |
| United States | NULL | 100 |
| NULL | NULL | 700 |

### <a name="group-by-cube--"></a>GROUP BY CUBE)  

GROUP BY CUBE 열의 모든 가능한 조합에 대 한 그룹을 만듭니다. GROUP BY CUBE (a, b)에 대 한 결과 고유 값에 대 한 그룹 (a, b)의 (NULL, b) (a, NULL) 및 (NULL, NULL).

이전 예제에 나오는 표를 사용 하 여이 코드는 국가 및 지역에 대 한 GROUP BY CUBE 작업이 실행 됩니다. 

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

쿼리 결과는 (Country, Region)의 고유 값에 대 한 그룹 (NULL, 지역), (Country, NULL) 및 (NULL, NULL). 결과 다음과 같습니다.

| Country | Region | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| NULL | Alberta | 100 |
| Canada | 브리티시 콜롬비아 | 500 |
| NULL | 브리티시 콜롬비아 | 500 |
| United States | 몬테나 | 100 |
| NULL | 몬테나 | 100 |
| NULL | NULL | 700
| Canada | NULL | 600 |
| United States | NULL | 100 |
   
 ### <a name="group-by-grouping-sets--"></a>집합 ()를 그룹화 하 여 그룹  
 
GROUPING SETS 옵션 하나의 GROUP BY 절에 여러 GROUP BY 절을 결합 하는 기능을 제공 합니다. 결과는 지정한 그룹의 UNION ALL에 해당합니다. 

예를 들어 `GROUP BY ROLLUP (Country, Region)` 및 `GROUP BY GROUPING SETS ( ROLLUP (Country, Region) )` 동일한 결과 반환 합니다. 

GROUPING SETS에 요소가 둘 이상 있는 경우 결과 요소의 합집합입니다. 이 예에서는 국가 및 지역에 대 한 ROLLUP 및 CUBE 결과의 합집합을 반환 합니다.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( ROLLUP (Country, Region), CUBE (Country, Region) );
```

결과 두 개의 GROUP BY 문의 합집합을 반환 하는이 쿼리와와 동일 합니다.

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

SQL은 GROUPING SETS 목록에 대해 생성 된 중복 그룹을 통합 하지 않습니다. 예를 들어, `GROUP BY ( (), CUBE (Country, Region) )`두 요소에 대 한 총합계 행을 반환 하 고 두 행을 결과에 표시 됩니다. 

 ### <a name="group-by-"></a>GROUP BY ()  
총합계를 생성 하는 빈 그룹을 지정 합니다. GROUPING SET의 요소 중 하나로 유용합니다. 예를 들어이 문에 각 국가 대 한 총 판매액을 제공 하 고 모든 국가 grand total를 제공 합니다.

```
SELECT Country, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( Country, () );
```

### <a name="group-by--all--column-expression--n-"></a>열-식을 GROUP BY [ALL] [,...n] 

적용 대상: SQL Server 및 Azure SQL 데이터베이스

참고:이 구문은 이전 버전과 호환성을 위해서만 위해 제공 됩니다. 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 구문을 사용 하지 마십시오 하 고 현재이 구문을 사용 하는 응용 프로그램은 수정 하세요.

WHERE 절의 검색 조건에 맞는지 여부에 관계 없이 결과에 모든 그룹을 포함 하도록 지정 합니다. 검색 조건과 일치 하지 않는 그룹의 집계에 대 한 NULL 값을 가집니다. 

모든 그룹:
- 쿼리에서 WHERE 절도이 원격 테이블에 액세스 하는 쿼리에서 지원 되지 않습니다.
- FILESTREAM 특성이 있는 열에 실패 합니다.
  
### <a name="with-distributedagg"></a>(DISTRIBUTED_AGG) 사용
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스

DISTRIBUTED_AGG 쿼리 힌트를 사용 하는 집계를 수행 하기 전에 특정 열에 테이블 다시 배포 하는 방대한 병렬 처리 (MPP) 시스템을 강제로 수행 합니다. GROUP BY 절에 열이 하나만 DISTRIBUTED_AGG 쿼리 힌트를 가질 수 있습니다. 쿼리를 완료 한 후에 재배포 테이블을 삭제 합니다. 원래 테이블이 변경 되지 않습니다.  

참고: DISTRIBUTED_AGG 쿼리 힌트를 위해 제공 되며 이전 버전과 병렬 데이터 웨어하우스 이전 버전과 호환성에 대 한 대부분의 쿼리 성능이 향상 되지 않습니다. 기본적으로 MPP 집계에 대 한 성능 향상을 위해 필요에 따라 데이터 이미 재배포 합니다. 
  
## <a name="general-remarks"></a>일반적인 주의 사항

### <a name="how-group-by-interacts-with-the-select-statement"></a>GROUP BY와 상호 작용 방법 SELECT 문
선택 목록:
- 벡터 집계 합니다. 집계 함수는 SELECT 목록에 포함 된, GROUP BY 각 그룹에 대 한 요약 값을 계산 합니다. 이를 벡터 집계라고 합니다. 
- Distinct 집계 합니다. 집계 AVG (DISTINCT *column_name*), COUNT (DISTINCT *column_name*), 및 SUM (DISTINCT *column_name*)은 ROLLUP, CUBE 및 GROUPING SETS에서 지원 합니다.
  
WHERE 절:
- SQL은 그룹화 작업이 수행 되기 전에 WHERE 절 조건을 충족 하지 않는 행을 제거 합니다.  
  
HAVING 절:
- SQL 사용 having 절은 결과 집합의 그룹을 필터링 합니다. 
  
ORDER BY 절:
- ORDER BY 절을 사용하여 결과 집합의 순서를 지정합니다. GROUP BY 절은 결과 집합의 순서를 지정하지 않습니다. 
  
NULL 값:
- 그룹화 열에 NULL 값이 있으면 모든 NULL 값은 같은 것으로 간주 하 고 단일 그룹으로 수집 합니다.   
  
## <a name="limitations-and-restrictions"></a>제한 사항

적용 대상: SQL Server (2008부터 시작) 및 Azure SQL 데이터 웨어하우스

### <a name="maximum-capacity"></a>최대 용량

GROUP by ROLLUP, CUBE 또는 GROUPING SETS를 사용 하는, 최대 식 수는 32입니다. 그룹의 최대 수는 4096 (2<sup>12</sup>). 다음 예에는 GROUP BY 절에는 4, 096 개 이상의 그룹에 있기 때문에 실패 합니다.  
 
-   다음 예에서는 4097 (2<sup>12</sup> + 1) 집합을 그룹화 하 고 실패 합니다.  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), b )  
    ```  
  
-   다음 예에서는 4097 (2<sup>12</sup> + 1)를 그룹화 하 고 실패 합니다. `CUBE ()` 그룹화 집합과 `()` 그룹화 집합 모두 총합계 행을 생성하고 중복된 그룹화 집합은 제거되지 않습니다.  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), ())  
    ```  

-   이 예제에서는 이전 버전과 호환 되는 구문을 사용 합니다. 생성 8192 (2<sup>13</sup>) 집합을 그룹화 하 고 실패 합니다.  
  
    ```  
    GROUP BY CUBE (a1, ..., a13)   
    GROUP BY a1, ..., a13 WITH CUBE   
    ```    
    절을 위해 이전 버전과 호환 GROUP BY CUBE 또는 ROLLUP을 포함 하지 않는 항목으로 그룹의 수는 GROUP BY 열 크기를 집계 된 열에 의해 제한 됩니다와 집계 값에 쿼리 합니다. 이 제한은 중간 작업 테이블이 중간 쿼리 결과를 보유하는 데 필요한 8,060바이트 제한을 기준으로 책정됩니다. CUBE 또는 ROLLUP이 지정될 경우 최대 12개의 그룹화 식이 허용됩니다.

### <a name="support-for-iso-and-ansi-sql-2006-group-by-features"></a>ISO 및 ANSI SQL-2006 GROUP BY 기능 지원

GROUP BY 절에서는 모든 GROUP BY 기능에는 다음과 같은 구문 예외가 sql-2006 표준에 포함 된 지원 합니다.  
  
-   명시적 GROUPING SETS 목록의 일부가 아닌 그룹화 집합을 GROUP BY 절에 사용할 수 없습니다. 예를 들어 `GROUP BY Column1, (Column2, ...ColumnN`) 표준에 있지만 TRANSACT-SQL에는 없는 허용 됩니다.  Transact SQL 지원 `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))` 및 `GROUP BY Column1, Column2, ... ColumnN`는 의미입니다. 이러한 예는 이전 `GROUP BY` 예와 기능적으로 동일합니다. 이 가능성을 방지 하기 위해는 하 `GROUP BY Column1, (Column2, ...ColumnN`)로 잘못 해석 될 수 `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))`, 의미상 동일 하지 않은 합니다.  
  
-   그룹화 집합은 그룹화 집합 내에 사용할 수 없습니다. 예를 들어 `GROUP BY GROUPING SETS (A1, A2,…An, GROUPING SETS (C1, C2, ...Cn))` TRANSACT-SQL 있지만 sql-2006 표준에 허용 됩니다. Transact SQL 허용 `GROUP BY GROUPING SETS( A1, A2,...An, C1, C2, ...Cn )` 또는 `GROUP BY GROUPING SETS( (A1), (A2), ... (An), (C1), (C2), ... (Cn) )`, 첫 번째 GROUP BY 예와 기능적 동일 하 고 보다 명확한 구문을 가질 수 있습니다.  
  
-   GROUP BY [ALL/DISTINCT]는 단순 GROUP BY 절에 열 식이 포함 된 개만 있습니다. GROUPING SETS, ROLLUP, CUBE, WITH CUBE 또는 WITH ROLLUP 구문과 허용 되지 않습니다. ALL은 기본값이며 암시적입니다. 또한 이전 버전과 호환 구문에서 허용 됩니다.
  
### <a name="comparison-of-supported-group-by-features"></a>지원되는 GROUP BY 기능 비교  
 다음 표에서 SQL 버전 및 데이터베이스 호환성 수준에 따라 지원 되는 GROUP BY 기능을 설명 합니다.  
  
|기능|SQL Server Integration Services|SQL Server 호환성 수준 100 이상|SQL Server 2008 이상(호환성 수준 90).|  
|-------------|-------------------------------------|--------------------------------------------------|-----------------------------------------------------------|  
|DISTINCT 집계|WITH CUBE 또는 WITH ROLLUP에 대해 지원되지 않습니다.|WITH CUBE, WITH ROLLUP, GROUPING SETS, CUBE 또는 ROLLUP에 대해 지원됩니다.|호환성 수준 100과 같습니다.|  
|GROUP BY 절에서 이름이 CUBE 또는 ROLLUP인 사용자 정의 함수|사용자 정의 함수 **dbo.cube (***arg1***,***...argN***)** 또는 **dbo.rollup (***arg1***,**... *argN * * *)* * GROUP by 절을 사용할 수 있습니다.<br /><br /> 예를 들어 `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|사용자 정의 함수 **dbo.cube (***arg1***,**...argN**)** 또는 **dbo.rollup (**arg1**,***...argN*** )** GROUP by 절은 허용 되지 않습니다.<br /><br /> 예를 들어 `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`<br /><br /> 다음과 같은 오류 메시지가 반환 됩니다: "'큐브의' 키워드 &#124; 근처의 구문이 잘못 되었습니다 ' 롤업 '. "<br /><br /> 이 문제를 방지하려면 `dbo.cube`를 `[dbo].[cube]`로 바꾸거나 `dbo.rollup`을 `[dbo].[rollup]`으로 바꿉니다.<br /><br /> 다음 예제는 허용 됩니다.`SELECT SUM (x) FROM T  GROUP BY [dbo].[cube](y);`|사용자 정의 함수 **dbo.cube (***arg1***, * * *...argN*) 또는 **dbo.rollup (***arg1***,***...argN***)**GROUP by 절을 사용할 수<br /><br /> 예를 들어 `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|  
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
 다음 예에서는 `SalesOrderID` 테이블의 각 `SalesOrderDetail`에 대한 합계를 계산합니다. 이 예제에서는 AdventureWorks를 사용 합니다.  
  
```  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail AS sod  
GROUP BY SalesOrderID  
ORDER BY SalesOrderID;  
```  
  
### <a name="b-use-a-group-by-clause-with-multiple-tables"></a>2. GROUP BY 절을 사용 하 여 여러 테이블을  
 다음 예에서는 `City` 테이블에 조인된 `Address` 테이블에서 각 `EmployeeAddress`에 대한 직원 수를 검색합니다. 이 예제에서는 AdventureWorks를 사용 합니다. 
  
```  
SELECT a.City, COUNT(bea.AddressID) EmployeeCount  
FROM Person.BusinessEntityAddress AS bea   
    INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
GROUP BY a.City  
ORDER BY a.City;  
```  
  
### <a name="c-use-a-group-by-clause-with-an-expression"></a>3. 식으로 GROUP BY 절을 사용 하 여  
 다음 예에서는 `DATEPART` 함수를 사용하여 각 연도별 총 판매액을 검색합니다. `SELECT` 목록과 `GROUP BY` 절 모두에 같은 식이 있어야 합니다.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
### <a name="d-use-a-group-by-clause-with-a-having-clause"></a>4. HAVING 절과 함께 GROUP BY 절을 사용 하 여  
 다음 예에서는 `HAVING` 절을 사용하여 `GROUP BY` 절에 생성된 그룹 중 결과 집합에 포함되어야 하는 그룹을 지정합니다.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
HAVING DATEPART(yyyy,OrderDate) >= N'2003'  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
## <a name="examples-sql-data-warehouse-and-parallel-data-warehouse"></a>예: SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스  
  
### <a name="e-basic-use-of-the-group-by-clause"></a>5. GROUP BY 절을 기본적으로 사용  
 다음 예제에서는 각 날짜에 모든 판매에 대 한 총 금액을 찾습니다. 모든 판매의 합계를 포함 하는 한 행은 각 날짜에 대해 반환 됩니다.  
  
```  
-- Uses AdventureWorksDW  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales FROM FactInternetSales  
GROUP BY OrderDateKey ORDER BY OrderDateKey;  
```  
  
### <a name="f-basic-use-of-the-distributedagg-hint"></a>6. DISTRIBUTED_AGG 힌트의 기본적인 사용  
 이 예제에서는 DISTRIBUTED_AGG 쿼리 힌트를 테이블에서 순서 섞기를 어플라이언스를 사용 하 여는 `CustomerKey` 집계를 수행 하기 전에 열입니다.  
  
```  
-- Uses AdventureWorksDW  
  
SELECT CustomerKey, SUM(SalesAmount) AS sas  
FROM FactInternetSales  
GROUP BY CustomerKey WITH (DISTRIBUTED_AGG)  
ORDER BY CustomerKey DESC;  
```  
  
### <a name="g-syntax-variations-for-group-by"></a>7. GROUP BY에 대 한 구문 변형  
 Select 목록에는 집계가 있는 경우 각 열은 select 목록에 GROUP BY 목록에 포함 되어야 합니다. Select 목록에 계산된 열 나열 될 수 있습니다 하지만 GROUP BY 목록에 필요 하지 않습니다. 다음은 구문이 올바른 SELECT 문의 예입니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName FROM DimCustomer GROUP BY LastName, FirstName;  
SELECT NumberCarsOwned FROM DimCustomer GROUP BY YearlyIncome, NumberCarsOwned;  
SELECT (SalesAmount + TaxAmt + Freight) AS TotalCost FROM FactInternetSales GROUP BY SalesAmount, TaxAmt, Freight;  
SELECT SalesAmount, SalesAmount*1.10 SalesTax FROM FactInternetSales GROUP BY SalesAmount;  
SELECT SalesAmount FROM FactInternetSales GROUP BY SalesAmount, SalesAmount*1.10;  
```  
  
### <a name="h-using-a-group-by-with-multiple-group-by-expressions"></a>8. GROUP BY를 사용 하 여 여러 GROUP BY 식  
 여러 사용 하 여 결과 그룹화 하는 다음 예제에서는 `GROUP BY` 조건입니다. 각 경우 `OrderDateKey` 하위 그룹으로 구분 되어야 하는 그룹 `DueDateKey`, 새로운 그룹화 결과 집합에 대해 정의 됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, DueDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSalesGROUP BY OrderDateKey, DueDateKey   
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-a-group-by-clause-with-a-having-clause"></a>9. HAVING 절과 함께 GROUP BY 절 사용  
 다음 예제에서는 `HAVING` 절에서 생성 된 그룹을 지정 하는 `GROUP BY` 결과 집합에 포함 되어야 하는 절. 주문 날짜가 2004 이상에서 해당 그룹에만 결과에 포함 됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING OrderDateKey > 20040000   
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [GROUPING_ID &#40; Transact SQL &#41;](~/t-sql/functions/grouping-id-transact-sql.md)   
 [그룹화 &#40; Transact SQL &#41;](~/t-sql/functions/grouping-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)   
 [SELECT 절 &#40; Transact SQL &#41;](~/t-sql/queries/select-clause-transact-sql.md)  
  
  




