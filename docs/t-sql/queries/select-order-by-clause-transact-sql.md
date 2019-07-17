---
title: ORDER BY 절(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ORDER_TSQL
- BY
- ORDER_BY_TSQL
- BY_TSQL
- ORDER
- ORDER BY
dev_langs:
- TSQL
helpviewer_keywords:
- ad-hoc query paging
- OFFSET clause
- SELECT statement [SQL Server], FETCH clause
- clauses [SQL Server], ORDER BY
- SELECT statement [SQL Server], limiting the rows returned
- data [SQL Server], limiting the rows returned
- data [SQL Server], ad-hoc query paging
- sort orders [SQL Server]
- SELECT statement [SQL Server], OFFSET clause
- ORDER BY clause [Transact-SQL]
- LIMIT
- limiting result sets
- SELECT statement [SQL Server], ORDER BY clause
- query paging
- data [SQL Server], sorting
- limiting data returned in a query
- sort orders [SQL Server], ORDER BY clause
- FETCH clause
ms.assetid: bb394abe-cae6-4905-b5c6-8daaded77742
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c08e29c5d1fba184739e2bb0e33718f766c32655
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62708174"
---
# <a name="select---order-by-clause-transact-sql"></a>SELECT - ORDER BY 절(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 쿼리에서 반환되는 데이터를 정렬합니다. 이 절을 사용하여 다음을 수행할 수 있습니다.  
  
-   쿼리 결과 집합을 지정한 열 목록별로 정렬하고 필요한 경우 반환되는 행을 지정한 범위로 제한합니다. ORDER BY 절을 지정하지 않으면 결과 집합에서 행이 반환되는 순서가 보장되지 않습니다.  
  
-   [순위 함수](../../t-sql/functions/ranking-functions-transact-sql.md) 값이 결과 집합에 적용되는 순서를 결정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!NOTE]  
>  ORDER BY는 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]의 SELECT/INTO 또는 CREATE TABLE AS SELECT (CTAS) 문에서 지원되지 않습니다.

## <a name="syntax"></a>구문  
  
```sql  
-- Syntax for SQL Server and Azure SQL Database  
  
ORDER BY order_by_expression  
    [ COLLATE collation_name ]   
    [ ASC | DESC ]   
    [ ,...n ]   
[ <offset_fetch> ]  
  
<offset_fetch> ::=  
{   
    OFFSET { integer_constant | offset_row_count_expression } { ROW | ROWS }  
    [  
      FETCH { FIRST | NEXT } {integer_constant | fetch_row_count_expression } { ROW | ROWS } ONLY  
    ]  
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[ ORDER BY   
    {  
    order_by_expression   
    [ ASC | DESC ]   
    } [ ,...n ]   
]   
```  
  
## <a name="arguments"></a>인수  
 *order_by_expression*  
 쿼리 결과 집합을 정렬할 열 또는 식을 지정합니다. 열 정렬은 이름이나 열 별칭으로 지정되거나 SELECT 목록에 있는 열의 위치를 나타내는 음수가 아닌 정수로 지정될 수 있습니다.  
  
 여러 개의 열 정렬을 지정할 수 있습니다. 열 이름은 고유해야 합니다. ORDER BY 절에서 열 정렬의 순서가 정렬된 결과 집합의 구성 방식을 정의합니다. 즉, 결과 집합은 첫 번째 열을 기준으로 정렬된 다음 이 정렬된 목록이 두 번째 열을 기준으로 정렬되는 식으로 정렬됩니다.  
  
 ORDER BY 절에서 참조하는 열 이름은 선택 목록의 열이나 열 별칭 또는 정확하게 FROM 절에서 지정한 테이블에 정의된 열과 같아야 합니다. ORDER BY 절이 선택 목록에서 열 별칭을 참조하는 경우 열 별칭을 독립 실행형으로 사용해야 하며, 예를 들어 ORDER BY 절의 일부 식으로 사용하지 않아야 합니다.
 
```sql
SELECT SCHEMA_NAME(schema_id) AS SchemaName FROM sys.objects 
ORDER BY SchemaName; -- correct 
SELECT SCHEMA_NAME(schema_id) AS SchemaName FROM sys.objects 
ORDER BY SchemaName + ''; -- wrong
```
  
 COLLATE *collation_name*  
 테이블이나 뷰에 정의된 열의 데이터 정렬이 아니라 *collation_name*에 지정된 데이터 정렬에 따라 ORDER BY 작업을 수행하도록 지정합니다. *collation_name*으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요. COLLATE는 **char**, **varchar**, **nchar** 및 **nvarchar** 형식의 열에만 적용할 수 있습니다.  
  
 **ASC** | DESC  
 지정된 열의 값이 오름차순으로 정렬되는지 내림차순으로 정렬되는지를 지정합니다. ASC는 오름차순으로 정렬하고, DESC는 내림차순으로 정렬합니다. ASC가 기본 정렬 순서입니다. Null 값은 가능한 가장 작은 값으로 취급됩니다.  
  
 OFFSET { *integer_constant* | *offset_row_count_expression* } { ROW | ROWS }  
 쿼리 식에서 행을 반환하기 전에 건너뛸 행 수를 지정합니다. 값은 0보다 크거나 같은 정수 상수 또는 식일 수 있습니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 *offset_row_count_expression*은 변수, 매개 변수 또는 상수 스칼라 하위 쿼리일 수 있습니다. 하위 쿼리를 사용하는 경우 외부 쿼리 범위에 정의된 열을 참조할 수 없습니다. 즉, 외부 쿼리와 상관 관계를 만들 수 없습니다.  
  
 ROW와 ROWS는 ANSI 호환성을 위해 제공되는 동의어입니다.  
  
 쿼리 실행 계획에서 오프셋 행 수 값은 TOP 쿼리 연산자의 **Offset** 특성에 표시됩니다.  
  
 FETCH { FIRST | NEXT } { *integer_constant* | *fetch_row_count_expression* } { ROW | ROWS } ONLY  
 OFFSET 절을 처리한 후에 반환할 행 수를 지정합니다. 값은 1보다 크거나 같은 정수 상수 또는 식일 수 있습니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지  
  
 *fetch_row_count_expression*은 변수, 매개 변수 또는 상수 스칼라 하위 쿼리일 수 있습니다. 하위 쿼리를 사용하는 경우 외부 쿼리 범위에 정의된 열을 참조할 수 없습니다. 즉, 외부 쿼리와 상관 관계를 만들 수 없습니다.  
  
 FIRST와 NEXT는 ANSI 호환성을 위해 제공되는 동의어입니다.  
  
 ROW와 ROWS는 ANSI 호환성을 위해 제공되는 동의어입니다.  
  
 쿼리 실행 계획에서 오프셋 행 수 값은 TOP 쿼리 연산자의 **Rows** 또는 **Top** 특성에 표시됩니다.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 ORDER BY 절에서 정수를 지정하는 방식으로 SELECT 목록에 있는 열의 위치를 나타내지 않도록 해야 합니다. 예를 들어 `SELECT ProductID, Name FROM Production.Production ORDER BY 2`와 같은 문은 유효하지만 실제 열 이름을 지정하는 것에 비해 다른 사용자가 이해하기 어렵습니다. 또한 열 순서 변경 또는 새 열 추가와 같이 SELECT 목록을 변경하려면 예기치 않은 결과가 발생하지 않도록 ORDER BY 절을 수정해야 합니다.  
  
 SELECT TOP (*N*) 문에는 항상 ORDER BY 절을 사용합니다. 이 방법은 TOP의 영향을 받는 행을 예측 가능한 방식으로 나타내는 유일한 방법입니다. 자세한 내용은 [TOP&#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)을 참조하세요.  
  
## <a name="interoperability"></a>상호 운용성  
 ORDER BY 절을 SELECT…INTO 문과 함께 사용하여 다른 원본에서 행을 삽입한 경우 지정된 순서대로 행이 삽입된다는 보장은 없습니다.  
  
 뷰에서 OFFSET과 FETCH를 함께 사용하면 뷰의 updateability 속성이 변경되지 않습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 ORDER BY 절의 열 개수에는 제한이 없지만 ORDER BY 절에 지정된 열의 전체 크기는 8,060바이트를 초과할 수 없습니다.  
  
 **ntext**, **text**, **image**, **geography**, **geometry** 및 **xml** 형식의 열은 ORDER BY 절에서 사용할 수 없습니다.  
  
 *order_by_expression*이 순위 함수에 나타나는 경우 정수 또는 상수를 지정할 수 없습니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.  
  
 FROM 절에 테이블 이름이 별칭으로 지정되어 있는 경우에는 ORDER BY 절에서 별칭 이름만 사용하여 해당 열을 정규화할 수 있습니다.  
  
 SELECT 문에 다음 절 또는 연산자 중 하나가 있으면 ORDER BY 절에 지정된 열 이름 및 별칭을 SELECT 문에도 정의해야 합니다.  
  
-   UNION 연산자  
  
-   EXCEPT 연산자  
  
-   INTERSECT 연산자  
  
-   SELECT DISTINCT  
  
 또한 명령문에 UNION, EXCEPT 또는 INTERSECT 연산자가 포함되면, 첫 번째(왼쪽) 쿼리의 SELECT 목록에 열 이름 또는 열 별칭을 지정해야 합니다.  
  
 UNION, EXCEPT 또는 INTERSECT 연산자를 사용하는 쿼리에서는 문의 끝 부분에만 ORDER BY를 사용할 수 있습니다. 이 제한 사항은 UNION, EXCEPT 및 INTERSECT를 하위 쿼리가 아닌 최상위 수준 쿼리에서 지정하는 경우에만 적용됩니다. 뒷부분에 나오는 예 섹션을 참조하세요.  
  
 TOP 절 또는 OFFSET 및 FETCH 절을 함께 지정하지 않는 한 뷰, 인라인 함수, 파생 테이블 및 하위 쿼리에서 ORDER BY 절을 사용할 수 없습니다. 이러한 개체에서 ORDER BY 절을 사용하는 경우 이 절은 TOP 절 또는 OFFSET 및 FETCH 절에서 반환되는 행을 결정하기 위한 용도로만 사용됩니다. 쿼리 자체에 ORDER BY를 지정하지 않으면 ORDER BY 절은 이러한 구조에 대한 쿼리 시 정렬된 결과를 보장하지 않습니다.  
  
 인덱싱 뷰 또는 CHECK OPTION을 사용하여 정의된 뷰에서는 OFFSET 및 FETCH가 지원되지 않습니다.  
  
 OFFSET 및 FETCH는 TOP 및 ORDER BY를 허용하는 모든 쿼리에서 사용할 수 있지만 다음과 같은 제한 사항이 있습니다.  
  
-   OVER 절은 OFFSET 및 FETCH를 지원하지 않습니다.  
  
-   OFFSET 및 FETCH는 INSERT, UPDATE, MERGE 및 DELETE 문에서 직접 지정할 수 없지만 이러한 문에 정의된 하위 쿼리에서는 지정할 수 있습니다. 예를 들어 INSERT INTO SELECT 문의 경우 SELECT 문에서 OFFSET 및 FETCH를 지정할 수 있습니다.  
  
-   UNION, EXCEPT 또는 INTERSECT 연산자를 사용하는 쿼리에서는 쿼리 결과의 순서를 지정하는 마지막 쿼리에서만 OFFSET 및 FETCH를 지정할 수 있습니다.  
  
-   같은 쿼리 식(같은 쿼리 범위)에서 TOP을 OFFSET 및 FETCH와 결합할 수 없습니다.  
  
## <a name="using-offset-and-fetch-to-limit-the-rows-returned"></a>OFFSET 및 FETCH를 사용하여 반환되는 행 수 제한  
 TOP 절 대신 OFFSET 및 FETCH 절을 사용하여 쿼리 페이징 솔루션을 구현하고 클라이언트 응용 프로그램으로 보내는 행 수를 제한하는 것이 좋습니다.  
  
 OFFSET 및 FETCH를 페이징 솔루션으로 사용하려면 클라이언트 응용 프로그램에 반환되는 데이터의 각 "페이지"에 대해 쿼리를 한 번씩 실행해야 합니다. 예를 들어 행 수가 10개씩 증가하는 쿼리 결과를 반환하려면 1~10행을 반환하는 쿼리를 한 번 실행한 다음 11~20행을 반환하는 쿼리를 다시 실행하고 이런 식으로 계속 쿼리를 실행해야 합니다. 각 쿼리는 독립적이며 어떤 방식으로도 서로 관련이 없습니다. 즉, 쿼리가 한 번 실행되면 서버에 상태가 유지되는 커서와 달리 클라이언트 응용 프로그램에서 상태를 추적해야 합니다. OFFSET 및 FETCH를 사용한 쿼리 요청 간에 안정적인 결과를 얻으려면 다음 조건을 충족해야 합니다.  
  
1.  쿼리에 사용되는 기본 데이터가 변경되지 않아야 합니다. 즉, 쿼리와 연결된 행이 업데이트되지 않거나 페이지에 대한 모든 쿼리 요청이 스냅샷 또는 직렬화 가능 트랜잭션 격리를 사용하여 단일 트랜잭션에서 실행되어야 합니다. 이러한 트랜잭션 격리 수준에 대한 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요.  
  
2.  ORDER BY 절이 고유한 열 또는 열의 조합을 포함해야 합니다.  
  
 이 항목의 뒷부분에 나오는 예 섹션에서 "단일 트랜잭션에서 여러 쿼리 실행" 예를 참조하세요.  
  
 페이징 솔루션에 일관된 실행 계획이 중요한 경우 OFFSET 및 FETCH 매개 변수에 대한 OPTIMIZE FOR 쿼리 힌트를 사용하는 것이 좋습니다. 이 항목의 뒷부분에 나오는 예 섹션에서 "식을 사용하여 OFFSET 및 FETCH 값 지정"을 참조하세요. OPTIMIZE FOR에 대한 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
## <a name="examples"></a>예  
  
|범주|중요한 구문 요소|  
|--------------|------------------------------|  
|[기본 구문](#BasicSyntax)|ORDER BY|  
|[오름차순 또는 내림차순 지정](#SortOrder)|DESC • ASC|  
|[데이터 정렬 지정](#Collation)|COLLATE|  
|[조건부 순서 지정](#Case)|CASE 식|  
|[순위 함수에 ORDER BY 사용](#Rank)|순위 함수|  
|[반환되는 행 수 제한](#Offset)|OFFSET • FETCH|  
|[UNION, EXCEPT 및 INTERSECT가 포함된 ORDER BY 사용](#Union)|UNION|  
  
###  <a name="BasicSyntax"></a>기본 구문  
 이 섹션의 예에서는 최소 필수 구문을 사용하여 ORDER BY 절의 기본 기능을 보여 줍니다.  
  
#### <a name="a-specifying-a-single-column-defined-in-the-select-list"></a>1\. SELECT 목록에 정의된 단일 열 지정  
 다음 예에서는 숫자 열 `ProductID`를 기준으로 결과 집합을 정렬합니다. 특정 정렬 순서를 지정하지 않으므로 기본값(오름차순)이 사용됩니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name FROM Production.Product  
WHERE Name LIKE 'Lock Washer%'  
ORDER BY ProductID;  
```  
  
#### <a name="b-specifying-a-column-that-is-not-defined-in-the-select-list"></a>2\. SELECT 목록에 정의되지 않은 열 지정  
 다음 예에서는 SELECT 목록에 없지만 FROM 절에 지정된 테이블에 정의되어 있는 열을 기준으로 결과 집합을 정렬합니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
ORDER BY ListPrice;  
  
```  
  
#### <a name="c-specifying-an-alias-as-the-sort-column"></a>C. 별칭을 정렬 열로 지정  
 다음 예에서는 열 별칭 `SchemaName`을 정렬 순서 열로 지정합니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT name, SCHEMA_NAME(schema_id) AS SchemaName  
FROM sys.objects  
WHERE type = 'U'  
ORDER BY SchemaName;  
  
```  
  
#### <a name="d-specifying-an-expression-as-the-sort-column"></a>D. 식을 정렬 열로 지정  
 다음 예에서는 식을 정렬 열로 사용합니다. 이 식은 DATEPART 함수를 사용하여 직원이 고용된 연도별로 결과 집합을 정렬하도록 정의됩니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY DATEPART(year, HireDate);  
  
```  
  
###  <a name="SortOrder"></a> 오름차순 또는 내림차순 정렬 지정  
  
#### <a name="a-specifying-a-descending-order"></a>1\. 내림차순 지정  
 다음 예에서는 숫자 열 `ProductID`를 기준으로 내림차순으로 결과 집합을 정렬합니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name FROM Production.Product  
WHERE Name LIKE 'Lock Washer%'  
ORDER BY ProductID DESC;  
  
```  
  
#### <a name="b-specifying-an-ascending-order"></a>2\. 오름차순 지정  
 다음 예에서는 `Name` 열을 기준으로 오름차순으로 결과 집합을 정렬합니다. 문자가 숫자순이 아니라 사전순으로 정렬됩니다. 즉, 10이 2보다 먼저 옵니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name FROM Production.Product  
WHERE Name LIKE 'Lock Washer%'  
ORDER BY Name ASC ;  
  
```  
  
#### <a name="c-specifying-both-ascending-and-descending-order"></a>C. 오름차순과 내림차순 둘 다 지정  
 다음 예에서는 두 열을 기준으로 결과 집합을 정렬합니다. 쿼리 결과 집합은 먼저 `FirstName` 열을 기준으로 오름차순으로 정렬된 다음 `LastName` 열을 기준으로 내림차순으로 정렬됩니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT LastName, FirstName FROM Person.Person  
WHERE LastName LIKE 'R%'  
ORDER BY FirstName ASC, LastName DESC ;  
  
```  
  
###  <a name="Collation"></a> 데이터 정렬 지정  
 다음 예에서는 ORDER BY 절에서 데이터 정렬을 지정할 경우 쿼리 결과가 반환되는 순서가 어떻게 변경되는지를 보여 줍니다. 대/소문자 및 액센트를 구분하지 않는 데이터 정렬을 사용하여 정의된 열이 포함된 테이블이 만들어집니다. 다양한 대/소문자와 악센트가 있는 값을 삽입했습니다. ORDER BY 절에서 데이터 정렬을 지정하지 않았으므로 첫 번째 쿼리는 열의 데이터 정렬을 사용하여 값을 정렬합니다. 두 번째 쿼리에서는 ORDER BY 절에 대/소문자 구분 및 악센트 구분 데이터 정렬을 지정했으므로 행이 반환되는 순서가 변경됩니다.  
  
```sql
USE tempdb;  
GO  
CREATE TABLE #t1 (name nvarchar(15) COLLATE Latin1_General_CI_AI)  
GO  
INSERT INTO #t1 VALUES(N'Sánchez'),(N'Sanchez'),(N'sánchez'),(N'sanchez');  
  
-- This query uses the collation specified for the column 'name' for sorting.  
SELECT name  
FROM #t1  
ORDER BY name;  
-- This query uses the collation specified in the ORDER BY clause for sorting.  
SELECT name  
FROM #t1  
ORDER BY name COLLATE Latin1_General_CS_AS;  
  
```  
  
###  <a name="Case"></a> 조건부 순서 지정  
 다음 예제에서는 ORDER BY 절에 CASE 식을 사용하여 지정된 열 값에 따라 행의 정렬 순서를 조건부로 결정합니다. 첫 번째 예에서는 `SalariedFlag` 테이블의 `HumanResources.Employee` 열의 값이 계산됩니다. `SalariedFlag`가 1로 설정된 직원은 `BusinessEntityID` 순서에 따라 내림차순으로 반환됩니다. `SalariedFlag`가 0으로 설정된 직원은 `BusinessEntityID` 순서에 따라 오름차순으로 반환됩니다. 두 번째 예에서 결과 집합은 `TerritoryName` 열이 'United States'와 동일하면 `CountryRegionName` 열을 기준으로 정렬되고 그 외 다른 행에는 `CountryRegionName` 열을 기준으로 정렬됩니다.  
  
```sql
SELECT BusinessEntityID, SalariedFlag  
FROM HumanResources.Employee  
ORDER BY CASE SalariedFlag WHEN 1 THEN BusinessEntityID END DESC  
        ,CASE WHEN SalariedFlag = 0 THEN BusinessEntityID END;  
GO  
  
```  
  
```sql
SELECT BusinessEntityID, LastName, TerritoryName, CountryRegionName  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL  
ORDER BY CASE CountryRegionName WHEN 'United States' THEN TerritoryName  
         ELSE CountryRegionName END;  
  
```  
  
###  <a name="Rank"></a> 순위 함수에 ORDER BY 사용  
 다음 예에서는 순위 함수 ROW_NUMBER, RANK, DENSE_RANK 및 NTILE에 ORDER BY 절을 사용합니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,ROW_NUMBER() OVER (ORDER BY a.PostalCode) AS "Row Number"  
    ,RANK() OVER (ORDER BY a.PostalCode) AS "Rank"  
    ,DENSE_RANK() OVER (ORDER BY a.PostalCode) AS "Dense Rank"  
    ,NTILE(4) OVER (ORDER BY a.PostalCode) AS "Quartile"  
    ,s.SalesYTD, a.PostalCode  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL AND SalesYTD <> 0;  
  
```  
  
###  <a name="Offset"></a> 반환되는 행 수 제한  
 다음 예에서는 OFFSET 및 FETCH를 사용하여 쿼리에서 반환되는 행 수를 제한합니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지  
  
#### <a name="a-specifying-integer-constants-for-offset-and-fetch-values"></a>1\. 정수 상수를 사용하여 OFFSET 및 FETCH 값 지정  
 다음 예에서는 정수 상수를 OFFSET 및 FETCH 절의 값으로 지정합니다. 첫 번째 쿼리는 `DepartmentID` 열을 기준으로 정렬된 모든 행을 반환합니다. 이 쿼리에서 반환된 결과를 다음에 나오는 두 쿼리의 결과와 비교해 보세요. 다음 쿼리에서는 `OFFSET 5 ROWS` 절을 사용하여 처음 5개 행을 건너뛰고 나머지 행을 모두 반환합니다. 마지막 쿼리에서는 `OFFSET 0 ROWS` 절을 사용하여 첫 번째 행에서 시작한 다음 `FETCH NEXT 10 ROWS ONLY`를 사용하여 반환되는 행을 정렬된 결과 집합의 10개 행으로 제한합니다.  
  
```sql
USE AdventureWorks2012;  
GO  
-- Return all rows sorted by the column DepartmentID.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID;  
  
-- Skip the first 5 rows from the sorted result set and return all remaining rows.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID OFFSET 5 ROWS;  
  
-- Skip 0 rows and return only the first 10 rows from the sorted result set.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID   
    OFFSET 0 ROWS  
    FETCH NEXT 10 ROWS ONLY;  
  
```  
  
#### <a name="b-specifying-variables-for-offset-and-fetch-values"></a>2\. 변수를 사용하여 OFFSET 및 FETCH 값 지정  
 다음 예에서는 변수 `@StartingRowNumber` 및 `@FetchRows`를 선언하고 이러한 변수를 OFFSET 및 FETCH 절에 지정합니다.  
  
```sql
USE AdventureWorks2012;  
GO  
-- Specifying variables for OFFSET and FETCH values    
DECLARE @StartingRowNumber tinyint = 1  
      , @FetchRows tinyint = 8;  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber ROWS   
    FETCH NEXT @FetchRows ROWS ONLY;  
  
```  
  
#### <a name="c-specifying-expressions-for-offset-and-fetch-values"></a>C. 식을 사용하여 OFFSET 및 FETCH 값 지정  
 다음 예에서는 `@StartingRowNumber - 1` 식을 사용하여 OFFSET 값을 지정하고, `@EndingRowNumber - @StartingRowNumber + 1` 식을 사용하여 FETCH 값을 지정합니다. 또한 OPTIMIZE FOR 쿼리 힌트를 지정합니다. 이 힌트는 쿼리가 컴파일되고 최적화될 때 지역 변수에 대해 특정 값을 제공하는 데 사용될 수 있습니다. 해당 값은 쿼리 최적화 중에만 사용되고 쿼리 실행 중에는 사용되지 않습니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
```sql
USE AdventureWorks2012;  
GO  
  
-- Specifying expressions for OFFSET and FETCH values      
DECLARE @StartingRowNumber tinyint = 1  
      , @EndingRowNumber tinyint = 8;  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber - 1 ROWS   
    FETCH NEXT @EndingRowNumber - @StartingRowNumber + 1 ROWS ONLY  
OPTION ( OPTIMIZE FOR (@StartingRowNumber = 1, @EndingRowNumber = 20) );  
  
```  
  
#### <a name="d-specifying-a-constant-scalar-subquery-for-offset-and-fetch-values"></a>D. 상수 스칼라 하위 쿼리를 사용하여 OFFSET 및 FETCH 값 지정  
 다음 예에서는 상수 스칼라 하위 쿼리를 사용하여 FETCH 절의 값을 정의합니다. 이 하위 쿼리는 `PageSize` 테이블의 `dbo.AppSettings` 열에서 단일 값을 반환합니다.  
  
```sql
-- Specifying a constant scalar subquery  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.AppSettings (AppSettingID int NOT NULL, PageSize int NOT NULL);  
GO  
INSERT INTO dbo.AppSettings VALUES(1, 10);  
GO  
DECLARE @StartingRowNumber tinyint = 1;  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber ROWS   
    FETCH NEXT (SELECT PageSize FROM dbo.AppSettings WHERE AppSettingID = 1) ROWS ONLY;  
  
```  
  
#### <a name="e-running-multiple-queries-in-a-single-transaction"></a>E. 단일 트랜잭션에서 여러 쿼리 실행  
 다음 예에서는 쿼리의 모든 요청에서 안정적인 결과가 반환되도록 페이징 솔루션을 구현하는 한 가지 방법을 보여 줍니다. 쿼리는 스냅샷 격리 수준을 사용하여 단일 트랜잭션에서 실행되며, ORDER BY 절에 지정된 열이 열의 고유성을 보장합니다.  
  
```sql
USE AdventureWorks2012;  
GO  
  
-- Ensure the database can support the snapshot isolation level set for the query.  
IF (SELECT snapshot_isolation_state FROM sys.databases WHERE name = N'AdventureWorks2012') = 0  
    ALTER DATABASE AdventureWorks2012 SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
  
-- Set the transaction isolation level  to SNAPSHOT for this query.  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
  
-- Beging the transaction  
BEGIN TRANSACTION;  
GO  
-- Declare and set the variables for the OFFSET and FETCH values.  
DECLARE @StartingRowNumber int = 1  
      , @RowCountPerPage int = 3;  
  
-- Create the condition to stop the transaction after all rows have been returned.  
WHILE (SELECT COUNT(*) FROM HumanResources.Department) >= @StartingRowNumber  
BEGIN  
  
-- Run the query until the stop condition is met.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber - 1 ROWS   
    FETCH NEXT @RowCountPerPage ROWS ONLY;  
  
-- Increment @StartingRowNumber value.  
SET @StartingRowNumber = @StartingRowNumber + @RowCountPerPage;  
CONTINUE  
END;  
GO  
COMMIT TRANSACTION;  
GO  
  
```  
  
###  <a name="Union"></a> UNION, EXCEPT 및 INTERSECT가 포함된 ORDER BY 사용  
 쿼리에서 UNION, EXCEPT 또는 INTERSECT 연산자를 사용하는 경우 문의 끝 부분에 ORDER BY 절을 지정해야 하며 조합된 쿼리 결과가 정렬됩니다. 다음 예에서는 빨간색 또는 노란색 제품을 모두 반환하고 이 조합된 목록을 `ListPrice` 열을 기준으로 정렬합니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT Name, Color, ListPrice  
FROM Production.Product  
WHERE Color = 'Red'  
-- ORDER BY cannot be specified here.  
UNION ALL  
SELECT Name, Color, ListPrice  
FROM Production.Product  
WHERE Color = 'Yellow'  
ORDER BY ListPrice ASC;  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예제에서는 결과 집합을 숫자 `EmployeeKey` 열을 기준으로 오름차순으로 정렬하는 방법을 보여 줍니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY EmployeeKey;  
```  
  
 다음 예제에서는 결과 집합을 숫자 `EmployeeKey` 열을 기준으로 내림차순으로 정렬합니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY EmployeeKey DESC;  
```  
  
 다음 예제에서는 결과 집합을 `LastName` 열을 기준으로 정렬합니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY LastName;  
```  
  
 다음 예제에서는 두 열을 기준으로 정렬합니다. 이 쿼리는 먼저 `FirstName` 열을 기준으로 오름차순으로 정렬한 다음, 공통 `FirstName` 값을 `LastName` 열을 기준으로 내림차순으로 정렬합니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY LastName, FirstName;  
```  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [순위 함수&#40;Transact-SQL&#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [TOP&#40;Transact SQL&#41;](../../t-sql/queries/top-transact-sql.md)   
 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)   
 [EXCEPT and INTERSECT &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [UNION&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-union-transact-sql.md)   
 [CASE&#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)  
  
  

