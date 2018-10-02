---
title: TOP(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TOP_TSQL
- TOP
dev_langs:
- TSQL
helpviewer_keywords:
- TOP clause
- first set of query result rows [SQL Server]
- TOP clause, about TOP clause
- queries [SQL Server], results
ms.assetid: da983c0a-06c5-4cf8-a6a4-7f9d66f34f2c
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 39c9a070150b3353270463e362d89f4fe70db705
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601192"
---
# <a name="top-transact-sql"></a>TOP(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  쿼리 결과 집합에 반환되는 행을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지정한 행 수 또는 행의 백분율로 제한합니다. ORDER BY 절과 함께 TOP이 사용된 경우 결과 집합은 정렬된 처음 *N*개 행으로 제한되고, 그렇지 않은 경우에는 처음 *N*개 행을 정의되지 않은 순서로 반환합니다. 이 절을 사용하여 SELECT 문에서 반환되거나 INSERT, UPDATE, MERGE 또는 DELETE 문의 영향을 받는 행 수를 지정할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[   
    TOP (expression) [PERCENT]  
    [ WITH TIES ]  
]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[   
    TOP ( expression )   
    [ WITH TIES ]  
]  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 반환할 행의 수를 지정하는 숫자 식입니다. PERCENT가 지정된 경우 *expression*은 암시적으로 **float** 값으로 변환됩니다. 그렇지 않은 경우에는 **bigint**로 변환됩니다.  
  
 PERCENT  
 쿼리 결과 집합에서 처음 *expression*%의 행만 반환됨을 나타냅니다. 소수 값은 다음 정수 값으로 올림됩니다.  
  
 WITH  TIES  
 제한된 결과 집합의 마지막 위치에 대해 일치하는 둘 이상의 행을 반환하려고 할 때 사용합니다. **ORDER BY** 절과 함께 사용해야 합니다. **WITH TIES**는 *expression*에 지정된 값보다 많은 행이 반환될 수 있습니다. 예를 들어 *expression*이 5로 설정되었지만 2개의 추가 행이 행 5에 있는 **ORDER BY** 열의 값과 일치하는 경우 결과 집합에는 7개 행이 포함됩니다.  
  
 TOP...WITH TIES는 ORDER BY 절이 지정된 경우에만 사용할 수 있으며 SELECT 문에서만 지정할 수 있습니다. 연결 레코드의 반환 순서는 임의로 지정됩니다. ORDER BY는 이 규칙에 영향을 주지 않습니다.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 SELECT 문에서 ORDER BY 절을 항상 TOP 절과 함께 사용합니다. 이 방법은 TOP의 영향을 받는 행을 예측 가능한 방식으로 나타내는 유일한 방법입니다.  
  
 ORDER BY 절에서 TOP 절 대신 OFFSET 및 FETCH를 사용하여 쿼리 페이징 솔루션을 구현합니다. 데이터의 청크 또는 "페이지"를 클라이언트로 보내는 페이징 솔루션은 OFFSET 및 FETCH 절을 사용하여 구현하는 것이 보다 간편합니다. 자세한 내용은 [ORDER BY 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)을 참조하세요.  
  
 SET ROWCOUNT 대신 TOP(또는 OFFSET 및 FETCH)을 사용하여 반환되는 행 수를 제한합니다. SET ROWCOUNT보다 이러한 방법을 사용하는 것이 좋은 이유는 다음과 같습니다.  
  
-   SELECT 문의 일부로 쿼리 최적화 프로그램은 쿼리를 최적화하는 과정에서 TOP 또는 FETCH 절에 있는 *expression* 값을 고려할 수 있습니다. SET ROWCOUNT는 쿼리를 실행하는 문 외부에서 사용되기 때문에 쿼리 계획에서 이 값을 고려할 수 없습니다.  
  
## <a name="compatibility-support"></a>호환성 지원  
 이전 버전과의 호환성을 위해 SELECT 문에서 괄호를 사용하는 것은 선택 사항입니다. 그러나 괄호가 필요한 INSERT, UPDATE, MERGE 및 DELETE 문과의 일관성을 위해 SELECT 문의 TOP에 괄호를 항상 사용하는 것이 좋습니다.  
  
## <a name="interoperability"></a>상호 운용성  
 TOP 식은 트리거로 인해 실행될 수 있는 문에 영향을 주지 않습니다. 트리거에서 **inserted** 및 **deleted** 테이블은 INSERT, UPDATE, MERGE 또는 DELETE 문의 영향을 받는 행만 반환합니다. 예를 들어 TOP 절이 사용된 INSERT 문으로 인해 INSERT TRIGGER가 실행된 경우  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 뷰를 통해 행을 업데이트할 수 있습니다. TOP 절은 뷰 정의에 포함될 수 있으므로 행이 TOP 식의 요구 사항을 더 이상 충족하지 않는 경우에는 업데이트로 인해 특정 행이 뷰에서 사라질 수 있습니다.  
  
 MERGE 문에 지정되는 경우 TOP 절은 전체 원본 테이블과 전체 대상 테이블이 조인되고 삽입, 업데이트 또는 삭제 동작에 적합하지 않은 조인된 행이 제거된 *후에* 적용됩니다. TOP 절은 조인된 행 수를 지정된 값으로 더 줄이며, 삽입, 업데이트 또는 삭제 동작은 나머지 조인된 행에 순서 없이 적용됩니다. 즉, 행은 WHEN 절에 정의된 동작에 순서 없이 분산됩니다. 예를 들어 TOP (10)을 지정하면 10개 행이 영향을 받습니다. 이 10개의 행 중 7개가 업데이트되고 3개가 삽입되거나, 1개가 삭제되고 5개가 업데이트되고 4개가 삽입될 수 있습니다. MERGE 문은 원본과 대상 테이블 모두에 전체 테이블 검색을 수행하므로 큰 테이블을 수정하기 위해 TOP 절을 사용하여 다중 일괄 처리를 생성하는 경우에는 I/O 성능에 영향을 줄 수 있습니다. 이러한 시나리오에서 연속된 모든 일괄 처리는 새로운 행을 대상으로 해야 합니다.  
  
 UNION, UNION ALL, EXCEPT 또는 INTERSECT 연산자가 포함된 쿼리에서 TOP 절을 지정할 때는 주의해야 합니다. 이러한 연산자가 SELECT 작업에 사용된 경우에는 TOP 및 ORDER BY 절이 논리적으로 처리되는 순서가 직관적이지 않을 수 있으므로 예기치 않은 결과를 반환하는 쿼리가 작성될 수 있습니다. 예를 들어 다음 테이블 및 데이터에서 가장 저렴한 빨간색 차와 가장 저렴한 파란색 차, 즉 red sedan과 blue van을 반환하려는 경우를 가정해 봅니다.  
  
```sql  
CREATE TABLE dbo.Cars(Model varchar(15), Price money, Color varchar(10));  
INSERT dbo.Cars VALUES  
    ('sedan', 10000, 'red'), ('convertible', 15000, 'blue'),   
    ('coupe', 20000, 'red'), ('van', 8000, 'blue');  
```  
  
 이러한 결과를 얻기 위해 다음과 같은 쿼리를 작성할 수 있습니다.  
  
```sql  
SELECT TOP(1) Model, Color, Price  
FROM dbo.Cars  
WHERE Color = 'red'  
UNION ALL  
SELECT TOP(1) Model, Color, Price  
FROM dbo.Cars  
WHERE Color = 'blue'  
ORDER BY Price ASC;  
GO    
```  
  
 결과 집합은 다음과 같습니다.  
  
 ```
 Model         Color      Price  
 ------------- ---------- -------  
 sedan         red        10000.00  
 convertible   blue       15000.00
 ```  
  
 ORDER BY 절이 연산자(이 경우 UNION ALL) 결과를 정렬하기 전에 TOP 절이 논리적으로 실행되므로 예기치 않은 결과가 반환됩니다. 즉, 위 쿼리는 임의의 빨간색 차와 임의의 파란색 차를 반환한 다음 이 합집합의 결과를 가격 순으로 정렬합니다. 다음 예에서는 원하는 결과를 얻을 수 있도록 이 쿼리를 올바르게 작성하는 방법을 보여 줍니다.  
  
```sql  
SELECT Model, Color, Price  
FROM (SELECT TOP(1) Model, Color, Price  
      FROM dbo.Cars  
      WHERE Color = 'red'  
      ORDER BY Price ASC) AS a  
UNION ALL  
SELECT Model, Color, Price  
FROM (SELECT TOP(1) Model, Color, Price  
      FROM dbo.Cars  
      WHERE Color = 'blue'  
      ORDER BY Price ASC) AS b;  
GO    
```  
  
 TOP과 ORDER BY를 하위 SELECT 작업에서 사용하면 ORDER BY 절의 결과가 TOP 절에 적용되어 UNION 연산의 결과를 정렬하지 않습니다.  
  
 결과 집합은 다음과 같습니다.  
  
 ```
 Model         Color      Price  
 ------------- ---------- -------  
 sedan         red        10000.00  
 van           blue        8000.00
 ```  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 TOP을 INSERT, UPDATE, MERGE 또는 DELETE와 함께 사용할 경우 참조된 행은 어떠한 순서로도 정렬되지 않으며 ORDER BY 절을 이러한 문에서 직접 지정할 수 없습니다. TOP을 사용하여 시간순으로 행을 삽입, 삭제 또는 수정하려면 하위 SELECT 문에서 지정된 ORDER BY 절과 함께 TOP을 사용해야 합니다. 이 항목의 뒷부분에 나오는 예 섹션을 참조하세요.  
  
 TOP은 분할된 뷰에서 UPDATE 및 DELETE 문에 사용할 수 없습니다.  
  
 같은 쿼리 식(같은 쿼리 범위)에서 TOP을 OFFSET 및 FETCH와 결합할 수 없습니다. 자세한 내용은 [ORDER BY 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
|범주|중요한 구문 요소|  
|--------------|------------------------------|  
|[기본 구문](#BasicSyntax)|TOP • PERCENT|  
|[동률 값 포함](#tie)|WITH  TIES|  
|[DELETE, INSERT 또는 UPDATE의 영향을 받는 행 제한](#DML)|DELETE • INSERT • UPDATE|  
  
###  <a name="BasicSyntax"></a>기본 구문  
 이 섹션의 예에서는 최소 필수 구문을 사용하여 ORDER BY 절의 기본 기능을 보여 줍니다.  
  
#### <a name="a-using-top-with-a-constant-value"></a>1. TOP에 상수 값 사용  
 다음 예에서는 상수 값을 사용하여 쿼리 결과 집합에 반환되는 직원 수를 지정합니다. 첫 번째 예에서는 ORDER BY 절을 사용하지 않으므로 정의되지 않은 처음 10개 행이 반환됩니다. 두 번째 예에서는 ORDER BY 절을 사용하여 최근에 고용된 상위 10명의 직원을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Select the first 10 random employees.  
SELECT TOP(10)JobTitle, HireDate  
FROM HumanResources.Employee;  
GO  
-- Select the first 10 employees hired most recently.  
SELECT TOP(10)JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY HireDate DESC;  
GO  
```  
  
#### <a name="b-using-top-with-a-variable"></a>2. TOP에 변수 사용  
 다음 예에서는 변수를 사용하여 쿼리 결과 집합에 반환되는 직원 수를 지정합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @p AS int = 10;  
SELECT TOP(@p)JobTitle, HireDate, VacationHours  
FROM HumanResources.Employee  
ORDER BY VacationHours DESC;  
GO  
```  
  
#### <a name="c-specifying-a-percentage"></a>3. 백분율 지정  
 다음 예에서는 PERCENT를 사용하여 쿼리 결과 집합에 반환되는 직원 수를 지정합니다. `HumanResources.Employee` 테이블에 290명의 직원이 있습니다. 290의 5%는 소수이므로 값이 다음 정수로 올림됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT TOP(5)PERCENT JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY HireDate DESC;  
GO    
```  
  
###  <a name="tie"></a>동률 값 포함  
  
#### <a name="a-using-with-ties-to-include-rows-that-match-the-values-in-the-last-row"></a>1. WITH TIES를 사용하여 마지막 행의 값과 일치하는 행 포함  
 다음 예에서는 급여가 가장 많은 `10`%의 직원을 검색하여 급여에 따라 내림차순으로 반환합니다. `WITH TIES`를 지정하면 가장 급여가 낮은 직원(마지막 행)이 여러 명이어서 `10`%를 넘는 경우에도 이러한 직원이 모두 결과 집합에 포함됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT TOP(10) PERCENT WITH TIES  
pp.FirstName, pp.LastName, e.JobTitle, e.Gender, r.Rate  
FROM Person.Person AS pp   
    INNER JOIN HumanResources.Employee AS e  
        ON pp.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN HumanResources.EmployeePayHistory AS r  
        ON r.BusinessEntityID = e.BusinessEntityID  
ORDER BY Rate DESC;  
GO    
```  
  
###  <a name="DML"></a>DELETE, INSERT 또는 UPDATE의 영향을 받는 행 제한  
  
#### <a name="a-using-top-to-limit-the-number-of-rows-deleted"></a>1. TOP를 사용하여 삭제되는 행 수 제한  
 DELETE 문과 함께 TOP (*n*) 절을 사용하면 임의로 선택된 *n*개의 행에 대해 삭제 작업이 수행됩니다. 즉, DELETE 문이 WHERE 절에 정의된 조건을 충족하는 행의 수(*n*)를 선택합니다. 다음 예에서는 `20` 테이블에서 기한이 2002년 7월 1일 이전인 행 중 `PurchaseOrderDetail`개의 행을 삭제합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
DELETE TOP (20)   
FROM Purchasing.PurchaseOrderDetail  
WHERE DueDate < '20020701';  
GO  
```  
  
 TOP을 사용하여 시간 순서로 행을 삭제해야 하는 경우에는 하위 SELECT 문에서 ORDER BY를 지정하는 방식으로 TOP을 사용해야 합니다. 다음 쿼리는 `PurchaseOrderDetail` 테이블에서 기한이 가장 빠른 10개의 행을 삭제합니다. 10개의 행만 삭제하기 위해 하위 SELECT  문에서 지정한 열(`PurchaseOrderID`)은 테이블의 기본 키입니다. 하위 SELECT 문에 키가 아닌 열을 사용하면 지정한 열에 중복 값이 있을 경우 10개가 넘는 행이 삭제될 수 있습니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
DELETE FROM Purchasing.PurchaseOrderDetail  
WHERE PurchaseOrderDetailID IN  
   (SELECT TOP 10 PurchaseOrderDetailID   
    FROM Purchasing.PurchaseOrderDetail   
    ORDER BY DueDate ASC);  
GO  
```  
  
#### <a name="b-using-top-to-limit-the-number-of-rows-inserted"></a>2. TOP를 사용하여 삽입되는 행 수 제한  
 다음 예에서는 `EmployeeSales` 테이블을 만들고 `HumanResources.Employee` 테이블에서 가져온 상위 5명의 직원에 대한 이름 및 연간 매출 데이터를 삽입합니다. 즉,  INSERT  문이 `SELECT` 문에서 반환되는 행 중 WHERE  절에 정의된 조건을 충족하는 5개의 행을 선택합니다.  OUTPUT  절은 `EmployeeSales` 테이블에 삽입되는 행을 표시합니다. SELECT 문의 ORDER BY 절은 상위 5명의 직원을 결정하는 데 사용되지 않습니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
IF OBJECT_ID ('dbo.EmployeeSales', 'U') IS NOT NULL  
    DROP TABLE dbo.EmployeeSales;  
GO  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   nvarchar(11) NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  YearlySales  money NOT NULL  
 );  
GO  
INSERT TOP(5)INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, inserted.LastName, inserted.YearlySales  
    SELECT sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
GO    
```  
  
 TOP을 사용하여 시간 순서로 행을 삽입해야 할 경우 다음 예와 같이 하위 SELECT 문에서 ORDER BY 절과 함께 TOP을 사용해야 합니다. OUTPUT  절은 `EmployeeSales` 테이블에 삽입되는 행을 표시합니다. 이제 정의되지 않은 행이 아니라 ORDER BY 절의 결과에 따라 상위 5명의 직원이 삽입됩니다.  
  
```sql  
INSERT INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, inserted.LastName, inserted.YearlySales  
    SELECT TOP (5) sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
GO    
```  
  
#### <a name="c-using-top-to-limit-the-number-of-rows-updated"></a>3. TOP를 사용하여 업데이트되는 행 수 제한  
 다음 예에서는 TOP 절을 사용하여 테이블의 행을 업데이트합니다. UPDATE 문과 함께 TOP (*n*) 절을 사용하면 정의되지 않은 수의 행에 대해 업데이트 작업이 수행됩니다. 즉, UPDATE 문이 WHERE 절에 정의된 조건을 충족하는 행의 수(*n*)를 선택합니다. 다음 예에서는 한 영업 직원의 고객 10명을 다른 영업 직원에게 지정합니다.  
  
```sql  
USE AdventureWorks2012;  
UPDATE TOP (10) Sales.Store  
SET SalesPersonID = 276  
WHERE SalesPersonID = 275;  
GO  
```  
  
 TOP를 사용하여 의미 있는 연대순으로 업데이트를 적용해야 할 경우 하위 SELECT 문에서 TOP를 ORDER BY와 함께 사용해야 합니다. 다음 예에서는 채용일이 가장 빠른 직원 10명의 휴가 기간을 업데이트합니다.  
  
```sql  
UPDATE HumanResources.Employee  
SET VacationHours = VacationHours + 8  
FROM (SELECT TOP 10 BusinessEntityID FROM HumanResources.Employee  
     ORDER BY HireDate ASC) AS th  
WHERE HumanResources.Employee.BusinessEntityID = th.BusinessEntityID;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예제에서는 쿼리 조건과 일치하는 상위 31개 행을 반환합니다. **ORDER BY** 절을 사용하여 31번째 반환된 행이 `LastName` 열의 알파벳 순서에 따라 처음 31행이 되도록 합니다.  
  
 동률을 지정하지 않고 **TOP**을 사용합니다.  
  
```sql  
SELECT TOP (31) FirstName, LastName   
FROM DimEmployee ORDER BY LastName;  
```  
  
 결과: 31개 행이 반환됩니다.  
  
 동률을 지정하여 TOP을 사용합니다.  
  
```sql  
SELECT TOP (31) WITH TIES FirstName, LastName   
FROM DimEmployee ORDER BY LastName;  
```  
  
 결과: Brown이라는 3명의 직원이 31행에 대해 동률이기 때문에 33개 행이 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [ORDER BY 절 &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)   
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md)   
 [MERGE&#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  
  
 
