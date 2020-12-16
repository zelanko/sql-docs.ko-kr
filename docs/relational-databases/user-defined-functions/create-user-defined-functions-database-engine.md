---
description: 사용자 정의 함수 만들기(데이터베이스 엔진)
title: 사용자 정의 함수 만들기(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 11/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SCHEMABINDING clause
- schema-bound functions [SQL Server]
- user-defined functions [SQL Server], creating
- CREATE FUNCTION statement
- valid statements [SQL Server]
- UDF
- TVF
ms.assetid: f0d5dd10-73fd-4e05-9177-07f56552bdf7
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d66e435bb902951f6cc1a06037ef1826560c8638
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482303"
---
# <a name="create-user-defined-functions-database-engine"></a>사용자 정의 함수 만들기(데이터베이스 엔진)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 사용자 정의 함수를 만드는 방법에 대해 설명합니다.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   사용자 정의 함수는 데이터베이스 상태 수정 동작을 수행하는 데 사용할 수 없습니다.  
  
-   사용자 정의 함수에는 테이블이 대상인 `OUTPUT INTO` 절을 포함할 수 없습니다.  
  
-   사용자 정의 함수는 여러 결과 집합을 반환할 수 없습니다. 여러 결과 집합을 반환해야 하는 경우 저장 프로시저를 사용하세요.  
  
-   오류 처리는 사용자 정의 함수에서 제한됩니다. UDF는 `TRY...CATCH`, `@ERROR` 또는 `RAISERROR`를 지원하지 않습니다.  
  
-   사용자 정의 함수는 저장 프로시저를 호출할 수 없지만 확장 저장 프로시저는 호출할 수 있습니다.  
  
-   사용자 정의 함수는 동적 SQL 또는 임시 테이블을 사용할 수 없습니다. 테이블 변수는 허용됩니다.  
  
-   `SET` 문은 사용자 정의 함수에서 허용되지 않습니다.  
  
-   `FOR XML` 절은 허용되지 않습니다.  
  
-   사용자 정의 함수는 중첩될 수 있습니다. 즉, 하나의 사용자 정의 함수가 다른 사용자 정의 함수를 호출할 수 있습니다. 중첩 수준은 호출된 함수의 실행이 시작되면 늘어나고 호출된 함수의 실행이 끝나면 줄어듭니다. 사용자 정의 함수는 최대 32 수준까지 중첩될 수 있습니다. 최대 중첩 수준을 초과하면 전체 함수 호출 체인이 실패합니다. Transact-SQL 사용자 정의 함수의 관리 코드 참조는 32 수준의 중첩 제한에 대해 한 수준으로 계산됩니다. 관리 코드 내에서 호출된 메서드는 이 제한에 따라 계산되지 않습니다.  
  
-   다음 Service Broker 문은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수에 **포함시킬 수 없습니다**.  
  
    -   `BEGIN DIALOG CONVERSATION`  
  
    -   `END CONVERSATION`  
  
    -   `GET CONVERSATION GROUP`  
  
    -   `MOVE CONVERSATION`  
  
    -   `RECEIVE`  
  
    -   `SEND`  
  
###  <a name="permissions"></a><a name="Security"></a> 권한 

데이터베이스에 대한 `CREATE FUNCTION` 권한과 함수가 생성되는 스키마에 대한 `ALTER` 권한이 필요합니다. 함수가 사용자 정의 형식을 지정하면 해당 유형에 대한 `EXECUTE` 권한이 필요합니다.  
  
##  <a name="scalar-functions"></a><a name="Scalar"></a> 스칼라 함수  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 다중 명령문 **스칼라 함수(스칼라 UDF)** 를 만듭니다. 함수에 `ProductID`가 단일 입력 값으로 입력되고 지정한 제품의 총 재고 수량이 단일 데이터 값으로 반환됩니다.  
  
```sql  
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
```  
  
 다음 예에서는 `ufnGetInventoryStock` 함수를 사용하여 `ProductModelID` 가 75와 80 사이인 제품의 현재 재고 수량을 반환합니다.  
  
```sql  
SELECT ProductModelID, Name, dbo.ufnGetInventoryStock(ProductID)AS CurrentSupply  
FROM Production.Product  
WHERE ProductModelID BETWEEN 75 and 80;  
```  

> [!NOTE]  
> 스칼라 함수에 대한 자세한 내용 및 예제는 [CREATE FUNCTION(Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)을 참조하세요. 

##  <a name="table-valued-functions"></a><a name="TVF"></a> 테이블 반환 함수  
다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 **인라인 TVF(테이블 반환 함수)** 를 만듭니다. 함수에 고객(상점) ID가 단일 입력 매개 변수로 입력되고 `ProductID`, `Name`및 `YTD Total` (해당 상점에 판매된 각 제품의 연간 총 매출액) 열이 반환됩니다.  
  
```sql  
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
  
```sql  
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 **MSTVF(다중 명령문 테이블 반환 함수)** 를 만듭니다. 함수에 `EmployeeID` 가 단일 입력 매개 변수로 입력되고 지정한 직원에게 직접 또는 간접적으로 보고하는 모든 직원의 목록이 반환됩니다. 그런 다음 직원 ID 109를 지정하여 함수를 호출합니다.  
  
```sql  
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
```  
  
다음 예제에서는 함수를 호출하고 고객 ID 1을 지정합니다.  
  
```sql  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);  
```  

> [!NOTE]  
> 인라인 TVF(테이블 반환 함수) 및 MSTVF(다중 명령문 테이블 반환 함수)에 대한 자세한 정보 및 예제는 [CREATE FUNCTION(Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)을 참조하세요. 

## <a name="best-practices"></a>모범 사례  
`SCHEMABINDING` 절을 사용하여 UDF(사용자 정의 함수)를 만들지 않은 경우 기본 개체에 대한 변경 내용이 함수의 정의에 영향을 주어 함수가 호출될 때 예기치 않은 결과를 초래할 수 있습니다. 기본 개체에 대한 변경으로 인해 함수가 최신 상태를 유지하지 못하게 되는 일이 발생하지 않도록 다음 메서드 중 하나를 구현하는 것이 좋습니다.  
  
-   UDF를 만들 때 `WITH SCHEMABINDING` 절을 지정합니다. 이렇게 하면 함수도 수정되지 않는 한 함수 정의에서 참조된 개체를 수정할 수 없습니다.  
  
-   UDF의 정의에 지정된 개체를 수정한 후 [sp_refreshsqlmodule](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md) 저장 프로시저를 실행합니다.  

데이터에 액세스하지 않는 UDF를 만드는 경우 `SCHEMABINDING` 옵션을 지정합니다. 이렇게 하면 쿼리 최적화 프로그램이 이러한 UDF와 관련된 쿼리 계획에 대해 불필요한 스풀 연산자를 생성하지 못하게 됩니다. 스풀에 대한 자세한 내용은 [실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)를 확인하세요. 스키마 바운드 함수를 만드는 방법은 [스키마 바운드 함수](../../relational-databases/user-defined-functions/user-defined-functions.md#SchemaBound)를 참조하세요.

`FROM` 절에서 MSTVF에 조인하는 것은 가능하지만 성능이 저하될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 MSTVF에 포함할 수 있는 일부 명령문에 대해 최적화되지 못한 쿼리 계획으로 이어지는 최적화된 기술은 모두 사용할 수 없습니다. 최상의 성능을 얻으려면 가능한 경우 기본 테이블 간에 함수 대신 조인을 사용합니다.  

> [!IMPORTANT]
> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서는 MSTVF에 대한 고정 카디널리티 추정이 100이고, 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 1입니다.    
> [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 MSTVF를 사용하는 실행 계획을 최적화하면 인터리브 실행을 활용할 수 있으므로 위의 추론 대신 실제 카디널리티를 사용할 수 있습니다.     
> 자세한 내용은 [다중 명령문 테이블 반환 함수에 대한 인터리브 실행](../../relational-databases/performance/intelligent-query-processing.md#interleaved-execution-for-mstvfs)을 참조합니다.

> [!NOTE]  
> 저장 프로시저나 사용자 정의 함수에 매개 변수를 전달할 때 또는 일괄 처리 문에서 변수를 선언하고 설정할 때 ANSI_WARNINGS는 인식되지 않습니다. 예를 들어 변수가 **char(3)** 로 정의된 경우 3자보다 큰 값으로 설정하면 해당 데이터가 정의된 크기로 잘리고 `INSERT` 또는 `UPDATE` 문은 성공합니다.

## <a name="see-also"></a>관련 항목  
 [사용자 정의 함수](../../relational-databases/user-defined-functions/user-defined-functions.md)     
 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)    
 [ALTER FUNCTION&#40;Transact-SQL&#41;](../../tools/sql-server-profiler/start-sql-server-profiler.md)    
 [DROP FUNCTION &#40;Transact-SQL&#41;](../../tools/sql-server-profiler/start-sql-server-profiler.md)     
 [DROP PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)    
 [커뮤니티](https://www.bing.com/search?q=user%20defined%20function%20%22sql%20server%202016%22%20examples&qs=n&form=QBRE&pq=user%20defined%20function%20%22sql%20server%202016%22%20examples&sc=0-48&sp=-1&sk=&cvid=C3AD337125A840AD9EEFA3AAC36A3712)에 나와 있는 추가 예제   
  
