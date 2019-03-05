---
title: SELECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SELECT_TSQL
- SELECT
dev_langs:
- TSQL
helpviewer_keywords:
- retrieving rows
- SELECT statement [SQL Server]
- SELECT statement [SQL Server], about SELECT statement
- row retrieval [SQL Server], SELECT statement
- DML [SQL Server], SELECT statement
- data manipulation language [SQL Server], SELECT statement
- row retrieval [SQL Server]
- queries [SQL Server], results
ms.assetid: dc85caea-54d1-49af-b166-f3aa2f3a93d0
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b92d260901efdec91add2d785774bfd826c8b46
ms.sourcegitcommit: 670082cb47f7d3d82e987b549b6f8e3a8968b5db
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57334690"
---
# <a name="select-transact-sql"></a>SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스에서 행을 검색하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 하나 이상의 테이블에서 하나 이상의 행 또는 열을 선택할 수 있도록 합니다. SELECT 문의 전체 구문은 복잡하지만 주요 절은 다음과 같이 요약할 수 있습니다.  
  
[ WITH { [ XMLNAMESPACES ,] [ \<common_table_expression> ] } ]
  
 SELECT *select_list* [ INTO *new_table* ]  
  
 [ FROM *table_source* ] [ WHERE *search_condition* ]  
  
 [ GROUP BY *group_by_expression* ]  
  
 [ HAVING *search_condition* ]  
  
 [ ORDER BY *order_expression* [ ASC | DESC ] ]  
  
 UNION, EXCEPT 및 INTERSECT 연산자는 쿼리 간에 결과를 비교하거나 하나의 결과 집합으로 결합하는 데 사용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
<SELECT statement> ::=    
    [ WITH { [ XMLNAMESPACES ,] [ <common_table_expression> [,...n] ] } ]  
    <query_expression>   
    [ ORDER BY { order_by_expression | column_position [ ASC | DESC ] }   
  [ ,...n ] ]   
    [ <FOR Clause>]   
    [ OPTION ( <query_hint> [ ,...n ] ) ]   
<query_expression> ::=   
    { <query_specification> | ( <query_expression> ) }   
    [  { UNION [ ALL ] | EXCEPT | INTERSECT }  
        <query_specification> | ( <query_expression> ) [...n ] ]   
<query_specification> ::=   
SELECT [ ALL | DISTINCT ]   
    [TOP ( expression ) [PERCENT] [ WITH TIES ] ]   
    < select_list >   
    [ INTO new_table ]   
    [ FROM { <table_source> } [ ,...n ] ]   
    [ WHERE <search_condition> ]   
    [ <GROUP BY> ]   
    [ HAVING < search_condition > ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[ WITH <common_table_expression> [ ,...n ] ]  
SELECT <select_criteria>  
[;]  
  
<select_criteria> ::=  
    [ TOP ( top_expression ) ]   
    [ ALL | DISTINCT ]   
    { * | column_name | expression } [ ,...n ]   
    [ FROM { table_source } [ ,...n ] ]  
    [ WHERE <search_condition> ]   
    [ GROUP BY <group_by_clause> ]   
    [ HAVING <search_condition> ]   
    [ ORDER BY <order_by_expression> ]  
    [ OPTION ( <query_option> [ ,...n ] ) ]  
  
```  
  
## <a name="remarks"></a>Remarks  
 SELECT 문은 복잡하기 때문에 자세한 구문 요소와 인수가 다음과 같은 절로 표시됩니다.  
  
|||  
|-|-|  
|[WITH XMLNAMESPACES](../../t-sql/xml/with-xmlnamespaces.md)<br /><br /> [WITH common_table_expression](../../t-sql/queries/with-common-table-expression-transact-sql.md)|[HAVING](../../t-sql/queries/select-having-transact-sql.md)|  
|[SELECT 절](../../t-sql/queries/select-clause-transact-sql.md)|[UNION](../../t-sql/language-elements/set-operators-union-transact-sql.md)|  
|[INTO 절](../../t-sql/queries/select-into-clause-transact-sql.md)|[EXCEPT 및 INTERSECT](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)|  
|[FROM](../../t-sql/queries/from-transact-sql.md)|[ORDER BY](../../t-sql/queries/select-order-by-clause-transact-sql.md)|  
|[WHERE](../../t-sql/queries/where-transact-sql.md)|[FOR 절](../../t-sql/queries/select-for-clause-transact-sql.md)|  
|[GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md)|[OPTION 절](../../t-sql/queries/option-clause-transact-sql.md)|  
  
 SELECT 문에서 절의 순서는 매우 중요합니다. 선택 사항인 절은 생략할 수 있지만 이러한 절을 사용할 때는 적절한 순서로 표시해야 합니다.  
  
 사용자 정의 함수 내의 SELECT 문은 함수에서 로컬인 변수에 값을 할당하는 식이 문의 선택 목록에 포함된 경우에만 허용됩니다.  
  
 서버 이름 부분에 OPENDATASOURCE 함수를 사용하여 네 부분으로 구성한 이름은 SELECT 문에서 테이블 이름이 표시될 수 있는 곳이면 어디든 테이블 원본으로 사용할 수 있습니다. [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에는 네 부분으로 된 이름을 지정할 수 없습니다.  
  
 SELECT 문에는 원격 테이블과 관련된 몇몇 구문 제한이 적용됩니다.  
  
## <a name="logical-processing-order-of-the-select-statement"></a>SELECT 문의 논리적 처리 순서  
 다음 단계에서는 SELECT 문의 논리적 처리 순서(바인딩 순서)를 보여 줍니다. 이 순서에 따라 특정 단계에서 정의한 개체를 후속 단계의 절에 사용할 수 있는 시기가 결정됩니다. 예를 들어 쿼리 프로세스가 FROM 절에 정의된 테이블 또는 뷰에 바인딩(액세스)할 수 있는 경우 이러한 개체 및 해당 열을 모든 후속 단계에서 사용할 수 있습니다. 반면, SELECT 절은 8단계이므로 해당 절에서 정의된 열 별칭 또는 파생 열을 이전 절에서 참조할 수는 없습니다. 그러나 ORDER BY 절 등의 후속 절에서는 이러한 항목을 참조할 수 있습니다. 문의 실제 실행은 쿼리 프로세서를 통해 결정되며 순서는 이 목록과 다를 수 있습니다.  
  
1.  FROM  
2.  ON  
3.  JOIN  
4.  WHERE  
5.  GROUP BY  
6.  WITH CUBE 또는 WITH ROLLUP  
7.  HAVING  
8.  SELECT  
9. DISTINCT  
10. ORDER BY  
11. 맨 위로 이동  

> [!WARNING]
> 위의 순서는 일반적으로 맞습니다. 그러나 순서가 달라지는 특수한 경우가 있을 수 있습니다.
>
> 예를 들어 뷰에 클라스터형 인덱스가 있고 이 뷰가 일부 테이블 행을 제외하며 이 뷰의 SELECT 열 목록에서 *varchar* 데이터 형식을 *정수*로 바꾸는 CONVERT를 사용한다고 가정해 봅니다. 이런 상황에서 CONVERT는 WHERE 문이 실행되기 전에 실행될 수 있습니다. 물론 일반적이지 않습니다. 필요한 상황에서 다른 순서를 방지하기 위해 뷰를 수정하는 방법이 있는 경우가 종종 있습니다. 

## <a name="permissions"></a>Permissions  
 데이터를 선택하려면 테이블이나 뷰에 대한 **SELECT** 권한이 있어야 합니다. 이 권한은 스키마에 대한 **SELECT** 권한이나 테이블에 대한 **CONTROL** 권한과 같은 상위 범위에서 상속할 수 있습니다. 또는 **db_datareader** 또는 **db_owner** 고정 데이터베이스 역할이거나 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다. **SELECTINTO**를 사용하여 새 테이블을 만들려면 **CREATETABLE** 권한과 새 테이블을 소유하는 스키마에 대한 **ALTERSCHEMA** 권한이 둘 다 있어야 합니다.  
  
## <a name="examples"></a>예:   
다음 예에서는 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스를 사용합니다.
  
### <a name="a-using-select-to-retrieve-rows-and-columns"></a>1. SELECT를 사용하여 행 및 열 검색  
 이 섹션에서는 세 가지 코드 예를 보여 줍니다. 첫 번째 코드 예에서는 `DimEmployee` 테이블에서 모든 행(WHERE 절이 지정되지 않음) 및 모든 열(`*` 사용)을 반환합니다.  
  
```sql  
SELECT *  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
 이 다음 예제에서는 테이블 별칭을 사용하여 같은 결과를 냅니다.  
  
```sql  
SELECT e.*  
FROM DimEmployee AS e  
ORDER BY LastName;  
```  
  
 다음 예에서는 `AdventureWorksPDW2012` 데이터베이스의 `DimEmployee` 테이블에서 모든 행(WHERE 절이 지정되지 않음) 및 열의 하위 집합(`FirstName`, `LastName`, `StartDate`)을 반환합니다. 세 번째 열 머리글 이름이 `FirstDay`로 변경됩니다.  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
ORDER BY LastName;  
```  
  
 이 예제에서는 `EndDate`가 NULL이 아니며 `MaritalStatus`가 'M'(기혼)인 `DimEmployee`의 행만 반환합니다.  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
WHERE EndDate IS NOT NULL   
AND MaritalStatus = 'M'  
ORDER BY LastName;  
```  
  
### <a name="b-using-select-with-column-headings-and-calculations"></a>2. SELECT에 열 머리글 및 계산 사용  
 다음 예제에서는 `DimEmployee` 테이블의 모든 행을 반환하며 `BaseRate` 및 40시간 근무 주를 기준으로 각 직원의 총 급여를 계산합니다.  
  
```sql  
SELECT FirstName, LastName, BaseRate, BaseRate * 40 AS GrossPay  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
### <a name="c-using-distinct-with-select"></a>C. SELECT에 DISTINCT 사용  
 다음 예제에서는 `DISTINCT`를 사용하여 `DimEmployee` 테이블의 모든 고유한 이름 목록을 생성합니다.  
  
```sql  
SELECT DISTINCT Title  
FROM DimEmployee  
ORDER BY Title;  
```  
  
### <a name="d-using-group-by"></a>D. GROUP BY 사용  
 다음 예제에서는 일별 총 판매액을 모두 찾습니다.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
 `GROUP BY` 절을 사용했으므로 각 날짜에 대해 모든 판매의 합계를 포함하는 한 행만 반환됩니다.  
  
### <a name="e-using-group-by-with-multiple-groups"></a>E. GROUP BY에 여러 그룹 사용  
 다음 예제에서는 주문일과 프로모션 키별로 그룹화된 일별 총 인터넷 판매 합계와 평균 금액을 찾습니다.  
  
```sql  

SELECT OrderDateKey, PromotionKey, AVG(SalesAmount) AS AvgSales, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey, PromotionKey  
ORDER BY OrderDateKey;   
```  
  
### <a name="f-using-group-by-and-where"></a>F. GROUP BY 및 WHERE 사용  
 다음 예에서는 가격이 주문일이 2002년 8월 1일 이후인 행만 검색한 후 그 결과를 그룹화합니다.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
WHERE OrderDateKey > '20020801'  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="g-using-group-by-with-an-expression"></a>G. GROUP BY에 식 사용  
 다음 예에서는 식으로 그룹화를 수행합니다. 식에 집계 함수가 없는 경우 식으로 그룹화를 수행할 수 있습니다.  
  
```sql  
SELECT SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY (OrderDateKey * 10);  
```  
  
### <a name="h-using-group-by-with-order-by"></a>H. GROUP BY 및 ORDER BY 사용  
 다음 예제에서는 일별 판매 합계와 일별 주문을 찾습니다.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-the-having-clause"></a>9. HAVING 절 사용  
 이 쿼리에서는 `HAVING` 절을 사용하여 결과를 제한합니다.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
HAVING OrderDateKey > 20010000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>참고 항목  
 [SELECT Examples &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md)  
 [힌트 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)
  

