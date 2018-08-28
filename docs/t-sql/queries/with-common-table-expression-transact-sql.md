---
title: WITH common_table_expression(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- WITH common_table_expression
- WITH_TSQL
- WITH
- common table expression
dev_langs:
- TSQL
helpviewer_keywords:
- WITH common_table_expression clause
- CTEs
- hierarchical queries [SQL Server], WITH common_table_expression
- recursive CTEs [SQL Server]
- recursive queries [SQL Server]
- common table expressions
- MAXRECURSION hint
- clauses [SQL Server], WITH common_table_expression
ms.assetid: 27cfb819-3e8d-4274-8bbe-cbbe4d9c2e23
caps.latest.revision: 60
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a7b96ba58211ee48bd1fb61b25a79429d7b03fa9
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43067586"
---
# <a name="with-commontableexpression-transact-sql"></a>WITH common_table_expression(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  CTE(공통 테이블 식)라고도 하는 임시로 이름이 지정된 결과 집합을 지정합니다. CTE는 단순 쿼리에서 파생되며 SELECT, INSERT, UPDATE 또는 DELETE 문 하나의 실행 범위 내에서 정의됩니다. 이 절은 정의하는 SELECT 문의 일부로 CREATE VIEW 문 내에서도 사용할 수 있습니다. 공통 테이블 식은 자신에 대한 참조를 포함할 수 있으며 이를 재귀 공통 테이블 식이라 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
[ WITH <common_table_expression> [ ,...n ] ]  
  
<common_table_expression>::=  
    expression_name [ ( column_name [ ,...n ] ) ]  
    AS  
    ( CTE_query_definition )  
```  
  
## <a name="arguments"></a>인수  
 *expression_name*  
공통 테이블 식에 대한 유효한 식별자입니다. *expression_name*은 같은 WITH \<common_table_expression> 절에서 정의된 다른 공통 테이블 식의 이름과는 달라야 하지만 *expression_name*이 기본 테이블 또는 뷰의 이름과 같을 수 있습니다. 쿼리에서 *expression_name*에 대한 모든 참조는 기본 개체가 아니라 공통 테이블 식을 사용합니다.
  
 *column_name*  
 공통 테이블 식에서 열 이름을 지정합니다. 단일 CTE 정의 내에서는 중복 이름이 허용되지 않습니다. 지정한 열 이름 수는 반드시 *CTE_query_definition*의 결과 집합에 있는 열 수와 일치해야 합니다. 열 이름 목록은 쿼리 정의에 모든 결과 열에 대한 고유한 이름을 제공한 경우에만 선택 사항입니다.  
  
 *CTE_query_definition*  
 공통 테이블 식을 채울 결과 집합을 위한 SELECT 문을 지정합니다. *CTE_query_definition*의 SELECT 문은 CTE가 또 다른 CTE를 정의하지는 못한다는 점을 제외하고는 뷰를 만들 때와 동일한 요구 사항을 만족해야 합니다. 자세한 내용은 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)과 주의 섹션을 참조하세요.  
  
 *CTE_query_definition*이 두 개 이상 정의된 경우 UNION ALL, UNION, EXCEPT 또는 INTERSECT 등의 집합 연산자 중 하나를 사용하여 쿼리 정의에 조인해야 합니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="guidelines-for-creating-and-using-common-table-expressions"></a>공통 테이블 식 만들기 및 사용 지침  
 다음 지침은 비재귀 공통 테이블 식에 적용됩니다. 재귀 공통 테이블 식에 적용되는 지침은 다음에 나오는 "재귀 공통 테이블 식 정의 및 사용 지침"을 참조하세요.  
  
-   CTE 뒤에는 일부 또는 모든 CTE 열을 참조하는 SELECT, INSERT, UPDATE 또는 DELETE 문 하나가 있어야 합니다. 뷰의 SELECT 문 정의의 일부로 CREATE VIEW 문 내에 CTE를 지정할 수 있습니다.  
  
-   비재귀 CTE 내에 여러 개의 CTE 쿼리 정의를 정의할 수 있습니다. 이러한 정의는 UNION ALL, UNION, INTERSECT 또는 EXCEPT 등의 집합 연산자 중 하나를 사용하여 결합해야 합니다.  
  
-   CTE는 같은 WITH 절에서 자신 및 이전에 정의한 CTE를 참조할 수 있지만 전방 참조는 허용되지 않습니다.  
  
-   CTE에 둘 이상의 WITH 절을 지정할 수 없습니다. 예를 들어 *CTE_query_definition*이 하위 쿼리를 포함하는 경우 그 하위 쿼리는 또 다른 CTE를 정의하는 중첩 WITH 절을 포함할 수 없습니다.  
  
-   *CTE_query_definition*에는 다음 절을 사용할 수 없습니다.  
  
    -   ORDER BY(TOP 절을 지정하는 경우는 제외)  
  
    -   INTO  
  
    -   쿼리 힌트가 있는 OPTION 절  
  
    -   FOR BROWSE  
  
-   일괄 처리에 속한 문에 CTE를 사용할 때는 그 전의 문 다음에 반드시 세미콜론을 추가해야 합니다.  
  
-   CTE를 참조하는 쿼리를 사용하여 커서를 정의할 수 있습니다.  
  
-   CTE에서 원격 서버 상의 테이블을 참조할 수 있습니다.  
  
-   CTE를 실행할 때는 쿼리의 뷰를 참조하는 힌트와 마찬가지로 CTE를 참조하는 힌트가 CTE가 기본 테이블에 액세스할 때 발견되는 다른 힌트와 충돌을 일으킬 수 있습니다. 이러한 경우 쿼리에서 오류를 반환합니다.  
  
## <a name="guidelines-for-defining-and-using-recursive-common-table-expressions"></a>재귀 공통 테이블 식 정의 및 사용 지침  
 다음 지침은 재귀 공통 테이블 식 정의 작업에 적용됩니다.  
  
-   재귀 CTE 정의는 적어도 두 개의 CTE 쿼리 정의 즉, 하나의 앵커 멤버와 재귀 멤버를 포함해야 합니다. 앵커 멤버와 재귀 멤버를 여러 개 정의할 수 있지만 앵커 멤버 쿼리 정의는 모두 첫 번째 재귀 멤버 정의 앞에 와야 합니다. 모든 CTE 쿼리 정의는 CTE 자체를 참조하지 않는 한 앵커 멤버입니다.  
  
-   앵커 멤버는 UNION ALL, UNION, INTERSECT 또는 EXCEPT 등의 집합 연산자 중 하나를 사용하여 결합해야 합니다. UNION ALL은 여러 재귀 멤버를 결합할 때 마지막 앵커 멤버와 첫 번째 재귀 멤버 사이에서 허용되는 유일한 집합 연산자입니다.  
  
-   앵커 멤버 및 재귀 멤버에 있는 열의 수는 같아야 합니다.  
  
-   재귀 멤버에 있는 열의 데이터 형식은 앵커 멤버에 있는 해당 열의 데이터 형식과 반드시 같아야 합니다.  
  
-   재귀 멤버의 FROM 절은 CTE *expression_name*을 한 번만 참조해야 합니다.  
  
-   다음 항목은 재귀 멤버의 *CTE_query_definition*에서 허용되지 않습니다.  
  
    -   SELECT DISTINCT  
  
    -   GROUP BY  
  
    -   PIVOT(데이터베이스 호환성 수준이 110 이상인 경우. [SQL Server 2016 데이터베이스 엔진 기능의 주요 변경](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)을 참조합니다.)  
  
    -   HAVING  
  
    -   스칼라 집계  
  
    -   맨 위로 이동  
  
    -   LEFT, RIGHT, OUTER JOIN(INNER JOIN이 허용됨)  
  
    -   하위 쿼리  
  
    -   *CTE_query_definition* 내부의 CTE에 대한 재귀적 참조에 적용되는 힌트입니다.  
  
 다음 지침은 재귀 공통 테이블 식 사용 작업에 적용됩니다.  
  
-   재귀 CTE가 반환하는 모든 열은 참가하는 SELECT 문이 반환하는 열의 Null 허용 여부와는 상관없이 Null을 허용합니다.  
  
-   잘못 구성된 재귀적 CTE로 인해 무한 루프가 발생할 수 있습니다. 예를 들어 재귀 멤버 쿼리 정의가 부모 열과 자식 열 모두에 대해 동일한 값을 반환하면 무한 루프가 생성된 것입니다. 무한 루프를 막기 위해서는 INSERT, UPDATE, DELETE 또는 SELECT 문의 OPTION 절에서 MAXRECURSION 힌트와 0부터 32,767 사이의 값을 사용하여 특정 문에 허용되는 재귀 수준을 제한할 수 있습니다. 이 방법으로 루프를 발생시키는 코드 문제를 해결할 때까지 문의 실행을 제어할 수 있습니다. 서버 차원의 기본값은 100입니다. 0을 지정하면 제한이 적용되지 않습니다. 하나의 문에는 하나의 MAXRECURSION 값만 지정할 수 있습니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
-   재귀 공통 테이블 식을 포함한 뷰를 사용하여 데이터를 업데이트할 수 없습니다.  
  
-   CTE를 사용하여 쿼리에 커서를 정의할 수 있습니다. CTE는 커서의 결과 집합을 정의하는 *select_statement* 인수입니다. 재귀 CTE에는 빠른 정방향 전용 커서 및 정적(스냅숏) 커서만 사용할 수 있습니다. 재귀 CTE에 또 다른 커서 유형을 지정하는 경우 해당 커서 유형이 정적으로 변환됩니다.  
  
-   CTE에서 원격 서버 상의 테이블을 참조할 수 있습니다. CTE의 재귀 멤버에서 원격 서버를 참조하는 경우 로컬에서 반복적으로 테이블에 액세스할 수 있도록 각 원격 테이블을 위한 스풀이 생성됩니다. CTE 쿼리인 경우 쿼리 계획에 Index Spool/Lazy Spool이 표시되며 이 스풀은 추가 WITH STACK 조건자를 가집니다. 이는 재귀를 올바르게 수행하는 한 가지 방법입니다.  
  
-   CTE의 재귀 부분에 있는 분석 및 집계 함수는 현재 재귀 수준에 대한 집합에만 적용되며 CTE에 대한 집합에는 적용되지 않습니다. ROW_NUMBER와 같은 함수는 CTE의 재귀 부분에 전달된 전체 데이터 집합이 아니라 현재 재귀 수준에 의해 함수로 전달된 데이터 하위 집합에 대해서만 실행됩니다. 자세한 내용은 예제 K. 재귀 CTE에서 분석 함수 사용을 참조하세요.  
  
## <a name="features-and-limitations-of-common-table-expressions-in-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 공통 테이블 식의 기능과 제한  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 현재 CTE의 구현은 다음과 같은 기능과 제한이 있습니다.  
  
-   CTE는 **SELECT** 문에서 지정될 수 있습니다.  
  
-   CTE는 **CREATE VIEW** 문에서 지정될 수 있습니다.  
  
-   CTE는 **CREATE TABLE AS SELECT**(CTAS) 문에서 지정할 수 있습니다.  
  
-   CTE는 **CREATE REMOTE TABLE AS SELECT**(CRTAS) 문에서 지정할 수 있습니다.  
  
-   CTE는 **CREATE EXTERNAL TABLE AS SELECT**(CETAS) 문에서 지정할 수 있습니다.  
  
-   CTE에서 원격 테이블을 참조할 수 있습니다.  
  
-   CTE에서 외부 테이블을 참조할 수 있습니다.  
  
-   여러 CTE 쿼리 정의는 CTE 내에서 정의할 수 있습니다.  
  
-   CTE 다음에 단일 **SELECT** 문을 추가해야 합니다. **INSERT**, **UPDATE**, **DELETE** 및 **MERGE** 문은 지원하지 않습니다.  
  
-   자체(재귀 공통 테이블 식)에 대한 참조를 포함하는 공통 테이블 식은 지원하지 않습니다.  
  
-   CTE에 둘 이상의 **WITH** 절을 지정할 수 없습니다. 예를 들어 CTE_query_definition이 하위 쿼리를 포함하는 경우 그 하위 쿼리는 또 다른 CTE를 정의하는 중첩 **WITH** 절을 포함할 수 없습니다.  
  
-   **ORDER BY** 절은 **TOP** 절이 지정된 경우를 제외하고는 CTE_query_definition에서 사용할 수 없습니다.  
  
-   일괄 처리에 속한 문에 CTE를 사용할 때는 그 전의 문 다음에 반드시 세미콜론을 추가해야 합니다.  
  
-   CTE가 **sp_prepare**에서 준비한 문에 사용되는 경우 PDW에서 사용하는 다른 **SELECT**과 동일한 방식으로 작동합니다. 그러나 CTE가 **sp_prepare**에서 준비한 CETAS의 일부로서 사용되는 경우 그 동작은 바인딩이 **sp_prepare**에 대해 구현되는 방식 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 다른 PDW 문에서 지연될 수 있습니다. CTE를 참조하는 **SELECT** 문이 CTE에 존재하지 않는 잘못된 열을 사용하고 있는 경우 **sp_prepare**는 오류를 감지하지 않고 지나가지만 대신 오류는 **sp_execute** 동안 throw됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-simple-common-table-expression"></a>1. 간단한 공통 테이블 식 만들기  
 다음 예에서는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]에서 각 판매 담당자의 연간 총 판매 주문 수를 보여 줍니다.  
  
```  
  
-- Define the CTE expression name and column list.  
WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
AS  
-- Define the CTE query.  
(  
    SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
)  
-- Define the outer query referencing the CTE name.  
SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
FROM Sales_CTE  
GROUP BY SalesYear, SalesPersonID  
ORDER BY SalesPersonID, SalesYear;  
GO  
  
```  
  
### <a name="b-using-a-common-table-expression-to-limit-counts-and-report-averages"></a>2. 공통 테이블 식을 사용한 수 제한 및 평균 보고  
 다음 예에서는 판매 담당자의 모든 연도에 대한 평균 판매 주문 수를 보여 줍니다.  
  
```  
WITH Sales_CTE (SalesPersonID, NumberOfOrders)  
AS  
(  
    SELECT SalesPersonID, COUNT(*)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
    GROUP BY SalesPersonID  
)  
SELECT AVG(NumberOfOrders) AS "Average Sales Per Person"  
FROM Sales_CTE;  
GO  
```  
  
### <a name="c-using-multiple-cte-definitions-in-a-single-query"></a>3. 단일 쿼리에서 여러 CTE 정의 사용  
 다음 예에서는 단일 쿼리에서 둘 이상의 CTE를 정의하는 방법을 보여 줍니다. CTE 쿼리 정의를 구분하기 위해 쉼표가 사용되었습니다. 통화 형식에서 통화량을 표시하는 데 사용되는 FORMAT 함수는 SQL Server 2012 이상에서 사용할 수 있습니다.  
  
```  
  
WITH Sales_CTE (SalesPersonID, TotalSales, SalesYear)  
AS  
-- Define the first CTE query.  
(  
    SELECT SalesPersonID, SUM(TotalDue) AS TotalSales, YEAR(OrderDate) AS SalesYear  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
       GROUP BY SalesPersonID, YEAR(OrderDate)  
  
)  
,   -- Use a comma to separate multiple CTE definitions.  
  
-- Define the second CTE query, which returns sales quota data by year for each sales person.  
Sales_Quota_CTE (BusinessEntityID, SalesQuota, SalesQuotaYear)  
AS  
(  
       SELECT BusinessEntityID, SUM(SalesQuota)AS SalesQuota, YEAR(QuotaDate) AS SalesQuotaYear  
       FROM Sales.SalesPersonQuotaHistory  
       GROUP BY BusinessEntityID, YEAR(QuotaDate)  
)  
  
-- Define the outer query by referencing columns from both CTEs.  
SELECT SalesPersonID  
  , SalesYear  
  , FORMAT(TotalSales,'C','en-us') AS TotalSales  
  , SalesQuotaYear  
  , FORMAT (SalesQuota,'C','en-us') AS SalesQuota  
  , FORMAT (TotalSales -SalesQuota, 'C','en-us') AS Amt_Above_or_Below_Quota  
FROM Sales_CTE  
JOIN Sales_Quota_CTE ON Sales_Quota_CTE.BusinessEntityID = Sales_CTE.SalesPersonID  
                    AND Sales_CTE.SalesYear = Sales_Quota_CTE.SalesQuotaYear  
ORDER BY SalesPersonID, SalesYear;  
GO  
  
```  
  
 다음은 결과 집합의 일부입니다.  
  
```  
  
SalesPersonID SalesYear   TotalSales    SalesQuotaYear SalesQuota  Amt_Above_or_Below_Quota  
------------- ---------   -----------   -------------- ---------- ----------------------------------   
  
274           2005        $32,567.92    2005           $35,000.00  ($2,432.08)  
274           2006        $406,620.07   2006           $455,000.00 ($48,379.93)  
274           2007        $515,622.91   2007           $544,000.00 ($28,377.09)  
274           2008        $281,123.55   2008           $271,000.00  $10,123.55  
  
```  
  
### <a name="d-using-a-recursive-common-table-expression-to-display-multiple-levels-of-recursion"></a>4. 재귀 공통 테이블 식을 사용하여 여러 수준의 재귀 표시  
 다음 예에서는 관리자의 계층적 목록 및 이들에게 보고하는 직원을 보여 줍니다. `dbo.MyEmployees` 테이블을 만들고 채워 이 예를 시작합니다.  
  
```  
-- Create an Employee table.  
CREATE TABLE dbo.MyEmployees  
(  
EmployeeID smallint NOT NULL,  
FirstName nvarchar(30)  NOT NULL,  
LastName  nvarchar(40) NOT NULL,  
Title nvarchar(50) NOT NULL,  
DeptID smallint NOT NULL,  
ManagerID int NULL,  
 CONSTRAINT PK_EmployeeID PRIMARY KEY CLUSTERED (EmployeeID ASC)   
);  
-- Populate the table with values.  
INSERT INTO dbo.MyEmployees VALUES   
 (1, N'Ken', N'Sánchez', N'Chief Executive Officer',16,NULL)  
,(273, N'Brian', N'Welcker', N'Vice President of Sales',3,1)  
,(274, N'Stephen', N'Jiang', N'North American Sales Manager',3,273)  
,(275, N'Michael', N'Blythe', N'Sales Representative',3,274)  
,(276, N'Linda', N'Mitchell', N'Sales Representative',3,274)  
,(285, N'Syed', N'Abbas', N'Pacific Sales Manager',3,273)  
,(286, N'Lynn', N'Tsoflias', N'Sales Representative',3,285)  
,(16,  N'David',N'Bradley', N'Marketing Manager', 4, 273)  
,(23,  N'Mary', N'Gibson', N'Marketing Specialist', 4, 16);  
```  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(ManagerID, EmployeeID, Title, EmployeeLevel) AS   
(  
    SELECT ManagerID, EmployeeID, Title, 0 AS EmployeeLevel  
    FROM dbo.MyEmployees   
    WHERE ManagerID IS NULL  
    UNION ALL  
    SELECT e.ManagerID, e.EmployeeID, e.Title, EmployeeLevel + 1  
    FROM dbo.MyEmployees AS e  
        INNER JOIN DirectReports AS d  
        ON e.ManagerID = d.EmployeeID   
)  
SELECT ManagerID, EmployeeID, Title, EmployeeLevel   
FROM DirectReports  
ORDER BY ManagerID;  
GO  
```  
  
### <a name="e-using-a-recursive-common-table-expression-to-display-two-levels-of-recursion"></a>5. 재귀 공통 테이블 식을 사용하여 두 가지 수준의 재귀 표시  
 다음 예에서는 관리자와 그들에게 보고하는 직원을 보여 줍니다. 반환되는 수준은 2로 제한됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(ManagerID, EmployeeID, Title, EmployeeLevel) AS   
(  
    SELECT ManagerID, EmployeeID, Title, 0 AS EmployeeLevel  
    FROM dbo.MyEmployees   
    WHERE ManagerID IS NULL  
    UNION ALL  
    SELECT e.ManagerID, e.EmployeeID, e.Title, EmployeeLevel + 1  
    FROM dbo.MyEmployees AS e  
        INNER JOIN DirectReports AS d  
        ON e.ManagerID = d.EmployeeID   
)  
SELECT ManagerID, EmployeeID, Title, EmployeeLevel   
FROM DirectReports  
WHERE EmployeeLevel <= 2 ;  
GO  
  
```  
  
### <a name="f-using-a-recursive-common-table-expression-to-display-a-hierarchical-list"></a>6. 재귀 공통 테이블 식을 사용하여 계층적 목록 표시  
 다음 예에서는 4번 예를 바탕으로 관리자 및 직원의 이름과 각각의 직함을 추가하는 방법을 보여 줍니다. 관리자와 직원의 계층을 추가로 강조하기 위해 각 수준을 들여쓰기 했습니다.  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(Name, Title, EmployeeID, EmployeeLevel, Sort)  
AS (SELECT CONVERT(varchar(255), e.FirstName + ' ' + e.LastName),  
        e.Title,  
        e.EmployeeID,  
        1,  
        CONVERT(varchar(255), e.FirstName + ' ' + e.LastName)  
    FROM dbo.MyEmployees AS e  
    WHERE e.ManagerID IS NULL  
    UNION ALL  
    SELECT CONVERT(varchar(255), REPLICATE ('|    ' , EmployeeLevel) +  
        e.FirstName + ' ' + e.LastName),  
        e.Title,  
        e.EmployeeID,  
        EmployeeLevel + 1,  
        CONVERT (varchar(255), RTRIM(Sort) + '|    ' + FirstName + ' ' +   
                 LastName)  
    FROM dbo.MyEmployees AS e  
    JOIN DirectReports AS d ON e.ManagerID = d.EmployeeID  
    )  
SELECT EmployeeID, Name, Title, EmployeeLevel  
FROM DirectReports   
ORDER BY Sort;  
GO  
```  
  
### <a name="g-using-maxrecursion-to-cancel-a-statement"></a>7. MAXRECURSION을 사용하여 문 취소  
 잘못 구성된 재귀 CTE가 무한 루프에 진입하는 것을 방지하는 데 `MAXRECURSION`을 사용할 수 있습니다. 다음 예에서는 의도적으로 무한 루프를 만들고 `MAXRECURSION` 힌트를 사용하여 재귀 수준을 2로 제한하는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
--Creates an infinite loop  
WITH cte (EmployeeID, ManagerID, Title) as  
(  
    SELECT EmployeeID, ManagerID, Title  
    FROM dbo.MyEmployees  
    WHERE ManagerID IS NOT NULL  
  UNION ALL  
    SELECT cte.EmployeeID, cte.ManagerID, cte.Title  
    FROM cte   
    JOIN  dbo.MyEmployees AS e   
        ON cte.ManagerID = e.EmployeeID  
)  
--Uses MAXRECURSION to limit the recursive levels to 2  
SELECT EmployeeID, ManagerID, Title  
FROM cte  
OPTION (MAXRECURSION 2);  
GO  
```  
  
 코딩 오류를 교정한 다음에는 더 이상 MAXRECURSION이 필요하지 않습니다. 다음 예에서는 교정된 코드를 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
WITH cte (EmployeeID, ManagerID, Title)  
AS  
(  
    SELECT EmployeeID, ManagerID, Title  
    FROM dbo.MyEmployees  
    WHERE ManagerID IS NOT NULL  
  UNION ALL  
    SELECT  e.EmployeeID, e.ManagerID, e.Title  
    FROM dbo.MyEmployees AS e  
    JOIN cte ON e.ManagerID = cte.EmployeeID  
)  
SELECT EmployeeID, ManagerID, Title  
FROM cte;  
GO  
```  
  
### <a name="h-using-a-common-table-expression-to-selectively-step-through-a-recursive-relationship-in-a-select-statement"></a>8. 공통 테이블 식을 사용하여 SELECT 문에서 재귀적 관계를 선택적으로 단계별 진행  
 다음 예에서는 `ProductAssemblyID = 800`에 대해 자전거를 제작하는 데 필요한 부품과 구성 요소의 계층을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
SELECT AssemblyID, ComponentID, Name, PerAssemblyQty, EndDate,  
        ComponentLevel   
FROM Parts AS p  
    INNER JOIN Production.Product AS pr  
    ON p.ComponentID = pr.ProductID  
ORDER BY ComponentLevel, AssemblyID, ComponentID;  
GO  
```  
  
### <a name="i-using-a-recursive-cte-in-an-update-statement"></a>9. UPDATE 문에서 재귀 CTE 사용  
 다음 예에서는 제품 'Road-550-W Yellow, 44' `(ProductAssemblyID``800`를 제작하는 데 사용되는 모든 부품의 `PerAssemblyQty` 값을 업데이트합니다). 공통 테이블 식은 `ProductAssemblyID 800`을 제작하는 데 사용되는 부품 및 해당 부품을 만드는 데 사용되는 구성 요소 등의 계층적 목록을 반환합니다. 이렇게 공통 테이블 식이 반환한 행만 수정됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
UPDATE Production.BillOfMaterials  
SET PerAssemblyQty = c.PerAssemblyQty * 2  
FROM Production.BillOfMaterials AS c  
JOIN Parts AS d ON c.ProductAssemblyID = d.AssemblyID  
WHERE d.ComponentLevel = 0;  
```  
  
### <a name="j-using-multiple-anchor-and-recursive-members"></a>10. 여러 앵커 및 재귀 멤버 사용  
 다음 예에서는 지정된 인물의 모든 조상을 반환하기 위해 여러 개의 앵커 및 재귀 멤버를 사용하는 방법을 보여 줍니다. 이 예는 재귀 CTE가 반환한 가족 계보를 구성하기 위해 하나의 테이블을 만들고 값을 삽입합니다.  
  
```  
-- Genealogy table  
IF OBJECT_ID('dbo.Person','U') IS NOT NULL DROP TABLE dbo.Person;  
GO  
CREATE TABLE dbo.Person(ID int, Name varchar(30), Mother int, Father int);  
GO  
INSERT dbo.Person   
VALUES(1, 'Sue', NULL, NULL)  
      ,(2, 'Ed', NULL, NULL)  
      ,(3, 'Emma', 1, 2)  
      ,(4, 'Jack', 1, 2)  
      ,(5, 'Jane', NULL, NULL)  
      ,(6, 'Bonnie', 5, 4)  
      ,(7, 'Bill', 5, 4);  
GO  
-- Create the recursive CTE to find all of Bonnie's ancestors.  
WITH Generation (ID) AS  
(  
-- First anchor member returns Bonnie's mother.  
    SELECT Mother   
    FROM dbo.Person  
    WHERE Name = 'Bonnie'  
UNION  
-- Second anchor member returns Bonnie's father.  
    SELECT Father   
    FROM dbo.Person  
    WHERE Name = 'Bonnie'  
UNION ALL  
-- First recursive member returns male ancestors of the previous generation.  
    SELECT Person.Father  
    FROM Generation, Person  
    WHERE Generation.ID=Person.ID  
UNION ALL  
-- Second recursive member returns female ancestors of the previous generation.  
    SELECT Person.Mother  
    FROM Generation, dbo.Person  
    WHERE Generation.ID=Person.ID  
)  
SELECT Person.ID, Person.Name, Person.Mother, Person.Father  
FROM Generation, dbo.Person  
WHERE Generation.ID = Person.ID;  
GO  
```  
  
###  <a name="bkmkUsingAnalyticalFunctionsInARecursiveCTE"></a> K. 재귀 CTE에서 분석 함수 사용  
 다음 예에서는 CTE의 재귀 부분에서 분석 또는 집계 함수를 사용할 때 발생할 수 있는 문제를 보여 줍니다.  
  
```  
DECLARE @t1 TABLE (itmID int, itmIDComp int);  
INSERT @t1 VALUES (1,10), (2,10);   
  
DECLARE @t2 TABLE (itmID int, itmIDComp int);   
INSERT @t2 VALUES (3,10), (4,10);   
  
WITH vw AS  
 (  
    SELECT itmIDComp, itmID  
    FROM @t1  
  
    UNION ALL  
  
    SELECT itmIDComp, itmID  
    FROM @t2  
)   
,r AS  
 (  
    SELECT t.itmID AS itmIDComp  
           , NULL AS itmID  
           ,CAST(0 AS bigint) AS N  
           ,1 AS Lvl  
    FROM (SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4) AS t (itmID)   
  
UNION ALL  
  
SELECT t.itmIDComp  
    , t.itmID  
    , ROW_NUMBER() OVER(PARTITION BY t.itmIDComp ORDER BY t.itmIDComp, t.itmID) AS N  
    , Lvl + 1  
FROM r   
    JOIN vw AS t ON t.itmID = r.itmIDComp  
)   
  
SELECT Lvl, N FROM r;  
```  
  
 다음은 쿼리의 예상 결과입니다.  
  
```  
Lvl  N  
1    0  
1    0  
1    0  
1    0  
2    4  
2    3  
2    2  
2    1  
```  
  
 다음은 쿼리의 실제 결과입니다.  
  
```  
Lvl  N  
1    0  
1    0  
1    0  
1    0  
2    1  
2    1  
2    1  
2    1  
```  
  
 `N`은 CTE 재귀 부분의 각 패스에 대해 1을 반환하는데 그 이유는 해당 재귀 수준에 대한 데이터 하위 집합만 `ROWNUMBER`로 전달되기 때문입니다. 쿼리 재귀 부분이 반복될 때마다 각각 하나의 행만 `ROWNUMBER`로 전달됩니다.  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="l-using-a-common-table-expression-within-a-ctas-statement"></a>12. CTAS 문 내에서 공통 테이블 식 사용하기  
 다음 예에서는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]에서 각 판매 담당자의 연간 총 판매 주문 수를 포함한 새 테이블을 만듭니다.  
  
```  
-- Uses AdventureWorks  
  
CREATE TABLE SalesOrdersPerYear  
WITH  
(  
    DISTRIBUTION = HASH(SalesPersonID)  
)  
AS  
    -- Define the CTE expression name and column list.  
    WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
    AS  
    -- Define the CTE query.  
    (  
        SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
        FROM Sales.SalesOrderHeader  
        WHERE SalesPersonID IS NOT NULL  
    )  
    -- Define the outer query referencing the CTE name.  
    SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
    FROM Sales_CTE  
    GROUP BY SalesYear, SalesPersonID  
    ORDER BY SalesPersonID, SalesYear;  
GO  
```  
  
### <a name="m-using-a-common-table-expression-within-a-cetas-statement"></a>13. CETAS 문 내에서 공통 테이블 식 사용하기  
 다음 예에서는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]에서 각 판매 담당자의 연간 총 판매 주문 수를 포함한 새 외부 테이블을 만듭니다.  
  
```  
-- Uses AdventureWorks  
  
CREATE EXTERNAL TABLE SalesOrdersPerYear  
WITH  
(  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:5000/files/Customer',  
    FORMAT_OPTIONS ( FIELD_TERMINATOR = '|' )   
)  
AS  
    -- Define the CTE expression name and column list.  
    WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
    AS  
    -- Define the CTE query.  
    (  
        SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
        FROM Sales.SalesOrderHeader  
        WHERE SalesPersonID IS NOT NULL  
    )  
    -- Define the outer query referencing the CTE name.  
    SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
    FROM Sales_CTE  
    GROUP BY SalesYear, SalesPersonID  
    ORDER BY SalesPersonID, SalesYear;  
GO  
```  
  
### <a name="n-using-multiple-comma-separated-ctes-in-a-statement"></a>14. 문에서 쉼표로 구분하는 여러 CTE 사용하기  
 다음 예에서는 단일 명령문에 두 개의 CTE를 포함하는 방법을 보여줍니다. CTE는 중첩될 수 없습니다(재귀 제외).  
  
```  
WITH   
 CountDate (TotalCount, TableName) AS  
    (  
     SELECT COUNT(datekey), 'DimDate' FROM DimDate  
    ) ,  
 CountCustomer (TotalAvg, TableName) AS  
    (  
     SELECT COUNT(CustomerKey), 'DimCustomer' FROM DimCustomer  
    )  
SELECT TableName, TotalCount FROM CountDate  
UNION ALL  
SELECT TableName, TotalAvg FROM CountCustomer;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [EXCEPT and INTERSECT &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
