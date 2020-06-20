---
title: 사용자 정의 함수 만들기(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SCHEMABINDING clause
- schema-bound functions [SQL Server]
- user-defined functions [SQL Server], creating
- CREATE FUNCTION statement
- valid statements [SQL Server]
ms.assetid: f0d5dd10-73fd-4e05-9177-07f56552bdf7
author: rothja
ms.author: jroth
ms.openlocfilehash: 790fa1b969f933890e050311173fcde3f12c37ef
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066400"
---
# <a name="create-user-defined-functions-database-engine"></a>사용자 정의 함수 만들기(데이터베이스 엔진)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 사용자 정의 함수를 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **사용자 정의 함수를 만들려면**  
  
     [스칼라 함수 만들기](#Scalar)  
  
     [테이블 반환 함수 만들기](#TVF)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   사용자 정의 함수는 데이터베이스 상태 수정 동작을 수행하는 데 사용할 수 없습니다.  
  
-   사용자 정의 함수에는 테이블이 대상인 OUTPUT INTO 절을 포함할 수 없습니다.  
  
-   사용자 정의 함수는 여러 결과 집합을 반환할 수 없습니다. 여러 결과 집합을 반환해야 하는 경우 저장 프로시저를 사용하세요.  
  
-   오류 처리는 사용자 정의 함수에서 제한됩니다. UDF는 TRY...CATCH를 지원 하지 않습니다. CATCH @ERROR 또는 RAISERROR.  
  
-   사용자 정의 함수는 저장 프로시저를 호출할 수 없지만 확장 저장 프로시저는 호출할 수 있습니다.  
  
-   사용자 정의 함수는 동적 SQL 또는 임시 테이블을 사용할 수 없습니다. 테이블 변수는 허용됩니다.  
  
-   SET 문은 사용자 정의 함수에서 허용되지 않습니다.  
  
-   FOR XML 절은 허용되지 않습니다.  
  
-   사용자 정의 함수는 중첩될 수 있습니다. 즉, 하나의 사용자 정의 함수가 다른 사용자 정의 함수를 호출할 수 있습니다. 중첩 수준은 호출된 함수의 실행이 시작되면 늘어나고 호출된 함수의 실행이 끝나면 줄어듭니다. 사용자 정의 함수는 최대 32 수준까지 중첩될 수 있습니다. 최대 중첩 수준을 초과하면 전체 함수 호출 체인이 실패합니다. Transact-SQL 사용자 정의 함수의 관리 코드 참조는 32 수준의 중첩 제한에 대해 한 수준으로 계산됩니다. 관리 코드 내에서 호출된 메서드는 이 제한에 따라 계산되지 않습니다.  
  
-   다음 Service Broker 문은 Transact-SQL 사용자 정의 함수에 포함될 수 없습니다.  
  
    -   BEGIN DIALOG CONVERSATION  
  
    -   END CONVERSATION  
  
    -   GET CONVERSATION GROUP  
  
    -   MOVE CONVERSATION  
  
    -   RECEIVE  
  
    -   SEND  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 데이터베이스에 대한 CREATE FUNCTION 권한과 함수가 생성되는 스키마에 대한 ALTER 권한이 필요합니다. 함수에 사용자 정의 형식이 지정되면 해당 유형에 대한 EXECUTE 권한이 필요합니다.  
  
##  <a name="scalar-functions"></a><a name="Scalar"></a>스칼라 함수  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 다중 문 스칼라 함수를 만듭니다. 함수에 `ProductID`가 단일 입력 값으로 입력되고 지정한 제품의 총 재고 수량이 단일 데이터 값으로 반환됩니다.  
  
```  
IF OBJECT_ID (N'dbo.ufnGetInventoryStock', N'FN') IS NOT NULL  
    DROP FUNCTION ufnGetInventoryStock;  
GO  
CREATE FUNCTION dbo.ufnGetInventoryStock(@ProductID int)  
RETURNS int   
AS   
-- Returns the stock level for the product.  
BEGIN  
    DECLARE @ret int;  
    SELECT @ret = SUM(p.Quantity)   
    FROM Production.ProductInventory p   
    WHERE p.ProductID = @ProductID   
        AND p.LocationID = '6';  
     IF (@ret IS NULL)   
        SET @ret = 0;  
    RETURN @ret;  
END;  
GO  
  
```  
  
 다음 예에서는 `ufnGetInventoryStock` 함수를 사용하여 `ProductModelID` 가 75와 80 사이인 제품의 현재 재고 수량을 반환합니다.  
  
```  
SELECT ProductModelID, Name, dbo.ufnGetInventoryStock(ProductID)AS CurrentSupply  
FROM Production.Product  
WHERE ProductModelID BETWEEN 75 and 80;  
  
```  
  
##  <a name="table-valued-functions"></a><a name="TVF"></a>테이블 반환 함수  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 인라인 테이블 값 함수를 만듭니다. 함수에 고객(상점) ID가 단일 입력 매개 변수로 입력되고 `ProductID`, `Name`및 `YTD Total` (해당 상점에 판매된 각 제품의 연간 총 매출액) 열이 반환됩니다.  
  
```  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
  
```  
  
 다음 예에서는 함수를 호출하고 고객 ID 602를 지정합니다.  
  
```  
SELECT * FROM Sales.ufn_SalesByStore (602);  
  
```  
  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 테이블 값 함수를 만듭니다. 함수에 `EmployeeID` 가 단일 입력 매개 변수로 입력되고 지정한 직원에게 직접 또는 간접적으로 보고하는 모든 직원의 목록이 반환됩니다. 그런 다음 직원 ID 109를 지정하여 함수를 호출합니다.  
  
```  
IF OBJECT_ID (N'dbo.ufn_FindReports', N'TF') IS NOT NULL  
    DROP FUNCTION dbo.ufn_FindReports;  
GO  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0 -- Get the initial list of Employees for Manager n  
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1 -- Join recursive member to anchor  
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [사용자 정의 함수](user-defined-functions.md)   
 [CREATE FUNCTION&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)  
  
  
