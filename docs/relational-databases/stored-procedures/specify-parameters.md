---
title: 매개 변수 지정 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parameters [SQL Server], stored procedures
- stored procedures [SQL Server], parameters
- output parameters [SQL Server]
- input parameters [SQL Server]
ms.assetid: 902314fe-5f9c-4d0d-a0b7-27e67c9c70ec
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 029b4f8eab1af6ebbd26c1d8fe877d38420e7f5c
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
# <a name="specify-parameters"></a>매개 변수 지정
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  프로시저 매개 변수를 지정하여 호출 프로그램이 값을 프로시저 본문에 전달할 수 있습니다. 이러한 값은 프로시저 실행 시 다양한 목적으로 쓰일 수 있습니다. 프로시저 매개 변수는 매개 변수가 OUTPUT 매개 변수로 표시된 경우 호출 프로그램에 값을 반환할 수도 있습니다.  
  
 프로시저는 최대 2100개의 매개 변수를 사용할 수 있으며 각각 이름, 데이터 형식, 방향이 할당됩니다. 필요에 따라 매개 변수가 기본값으로 할당될 수 있습니다.  
  
 다음 섹션에서는 값을 매개 변수에 전달하는 것과 프로시저 호출 시 각 매개 변수 특성이 어떻게 사용되는지 알려줍니다.  
  
## <a name="passing-values-into-parameters"></a>값을 매개 변수로 전달  
 프로시저 호출과 함께 입력된 매개 변수 값은 상수 또는 변수여야 합니다. 함수 이름은 매개 변수 값으로 사용될 수 없습니다. 변수는 @@spid와 같은 시스템 변수이거나 사용자 정의 변수일 수 있습니다.  
  
 다음 예에서는 프로시저 `uspGetWhereUsedProductID`에 매개 변수 값을 전달하는 방법을 설명합니다. 다음 예에서는 상수와 변수로 매개 변수를 전달하는 방법과 변수를 사용하여 함수 값을 전달하는 방법을 설명합니다.  
  
```  
USE AdventureWorks2012;  
GO  
-- Passing values as constants.  
EXEC dbo.uspGetWhereUsedProductID 819, '20050225';  
GO  
-- Passing values as variables.  
DECLARE @ProductID int, @CheckDate datetime;  
SET @ProductID = 819;  
SET @CheckDate = '20050225';  
EXEC dbo.uspGetWhereUsedProductID @ProductID, @CheckDate;  
GO  
-- Try to use a function as a parameter value.  
-- This produces an error message.  
EXEC dbo.uspGetWhereUsedProductID 819, GETDATE();  
GO  
-- Passing the function value as a variable.  
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
## <a name="specifying-parameter-names"></a>매개 변수 이름 지정  
 프로시저를 생성하고 매개 변수를 선언할 때 매개 변수 이름은 하나의 @ 문자로 시작해야 하며 프로시저 범위 내에서 고유해야 합니다.  
  
 매개 변수 이름을 명시적으로 지정하고 프로시저 호출 시 적절한 값을 각 매개 변수에 할당하면 매개 변수를 임의의 순서로 제공할 수 있습니다. 예를 들어, 프로시저 **my_proc** 에서 **@first**, **@second**및 **@third**라는 세 개의 매개 변수를 사용하는 경우 다음과 같이 프로시저에 전달된 값을 매개 변수 이름에 할당할 수 있습니다. `EXECUTE my_proc @second = 2, @first = 1, @third = 3;`  
  
> [!NOTE]  
>  **@parameter =***value* 형식에 하나의 매개 변수 값이 입력되는 경우 모든 후속 매개 변수도 이러한 방식으로 입력되어야 합니다. **@parameter =***value* 형식에 매개 변수 값이 전달되지 않은 경우 해당 값은 CREATE PROCEDURE 문에 나열된 매개 변수를 따라 동일한 순서(왼쪽에서 오른쪽)로 제공되어야 합니다.  
  
> [!WARNING]  
>  철자가 잘못 입력된 매개 변수와 함께 **@parameter =***value* 형식으로 매개 변수가 전달될 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 오류가 발생하여 프로시저 실행을 방해할 수 있습니다.  
  
## <a name="specifying-parameter-data-types"></a>매개 변수 데이터 형식 지정  
 CREATE PROCEDURE 문에서 매개 변수가 선언될 때에는 데이터 형식이 함께 정의되어야 합니다. 프로시저가 호출될 때 매개 변수의 데이터 형식에 따라 매개 변수에 허용되는 값의 형식과 범위가 결정됩니다. 예를 들어 **tinyint** 데이터 형식으로 매개 변수를 정의하면 해당 매개 변수로는 0에서 255까지의 숫자 값만 전달될 수 있습니다. 데이터 형식과 맞지 않는 값으로 프로시저를 실행하면 오류가 반환됩니다.  
  
## <a name="specifying-parameter-default-values"></a>매개 변수 기본값 지정  
 매개 변수가 선언될 때 매개 변수에 지정된 기본값이 있는 경우 매개 변수는 선택적으로 간주됩니다. 프로시저 호출 시 선택적 매개 변수로 값을 제공해야 하는 것은 아닙니다.  
  
 매개 변수의 기본값은 다음 경우에 사용 됩니다.  
  
-   프로시저 호출 시 매개 변수에 값이 지정되어 있지 않은 경우  
  
-   프로시저 호출에서 DEFAULT 키워드가 값으로 지정된 경우  
  
> [!NOTE]  
>  기본값이 공백 또는 문장 부호가 포함된 문자열이거나 6xxx와 같이 숫자로 시작하면 기본값을 곧은 작은 따옴표로 묶어야 합니다.  
  
 매개 변수에 적당한 기본값을 지정할 수 없을 때는 NULL을 기본값으로 지정합니다. 프로시저가 매개 변수 값이 없이 실행되는 경우 프로시저에서 사용자 지정 메시지를 반환하는 것이 좋습니다.  
  
 다음 예는 한 개의 입력 매개 변수 `uspGetSalesYTD` 을 사용하여 `@SalesPerson`프로시저를 만듭니다. `@SalesPerson` 매개 변수 값 없이 프로시저를 실행할 경우 NULL이 이 매개 변수의 기본값으로 할당되고 사용자 지정 오류 메시지를 반환하는 오류 처리 문에서 NULL이 사용됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetSalesYTD  
@SalesPerson nvarchar(50) = NULL  -- NULL default value  
AS   
    SET NOCOUNT ON;   
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
BEGIN  
   PRINT 'ERROR: You must specify the last name of the sales person.'  
   RETURN  
END  
-- Get the sales for the specified sales person and   
-- assign it to the output parameter.  
SELECT SalesYTD  
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 다음 예는 프로시저를 실행합니다. 첫 번째 문은 입력 값을 지정하지 않고 프로시저를 실행하므로 프로시저의 오류 처리 문이 사용자 지정 오류 메시지를 반환합니다. 두 번째 문은 입력 값을 제공하고 예상 결과 집합을 반환합니다.  
  
```  
-- Run the procedure without specifying an input value.  
EXEC Sales.uspGetSalesYTD;  
GO  
-- Run the procedure with an input value.  
EXEC Sales.uspGetSalesYTD N'Blythe';  
GO  
```  
  
 기본값이 있는 매개 변수는 생략될 수 있지만 실제로는 매개 변수의 목록이 잘리는 것뿐입니다. 예를 들어 한 프로시저가 다섯 개의 매개 변수를 갖는 경우 4번째, 5번째 매개 변수는 생략될 수 있습니다. 하지만 매개 변수가 **@parameter =***value* 형식으로 입력되지 않는 한 5번째 매개 변수가 있는 경우 4번째 매개 변수는 생략할 수 없습니다.  
  
## <a name="specifying-parameter-direction"></a>매개 변수 방향 지정  
 매개 변수의 방향은 프로시저 본문으로 전달되는 값을 의미하는 입력 또는 프로시저가 호출 프로그램에 값을 반환함을 의미하는 출력입니다. 기본값은 입력 매개 변수입니다.  
  
 출력 매개 변수를 지정하려면 CREATE PROCEDURE 문의 매개 변수 정의에서 OUTPUT 키워드를 반드시 지정해야 합니다. 프로시저는 출력 매개 변수의 현재 값을 프로시저가 끝날 때 호출 프로그램에 반환합니다. 호출 프로그램에서 프로시저를 실행할 때 OUTPUT 키워드도 사용해야 호출 프로그램에서 사용할 수 있는 변수에 매개 변수 값을 저장할 수 있습니다.  
  
 다음 예에서는 지정된 가격을 초과하지 않는 제품 목록을 반환하는 `Production.usp_GetList` 프로시저를 만듭니다. 다음 예에서는 여러 SELECT 문과 여러 OUTPUT 매개 변수의 사용을 보여 줍니다. OUTPUT 매개 변수를 사용하면 프로시저를 실행하는 동안 외부 프로시저, 일괄 처리 또는 한 개 이상의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 값 집합에 액세스할 수 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Production.uspGetList', 'P' ) IS NOT NULL   
    DROP PROCEDURE Production.uspGetList;  
GO  
CREATE PROCEDURE Production.uspGetList @Product varchar(40)   
    , @MaxPrice money   
    , @ComparePrice money OUTPUT  
    , @ListPrice money OUT  
AS  
    SET NOCOUNT ON;  
    SELECT p.[Name] AS Product, p.ListPrice AS 'List Price'  
    FROM Production.Product AS p  
    JOIN Production.ProductSubcategory AS s   
      ON p.ProductSubcategoryID = s.ProductSubcategoryID  
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice;  
-- Populate the output variable @ListPprice.  
SET @ListPrice = (SELECT MAX(p.ListPrice)  
        FROM Production.Product AS p  
        JOIN  Production.ProductSubcategory AS s   
          ON p.ProductSubcategoryID = s.ProductSubcategoryID  
        WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice);  
-- Populate the output variable @compareprice.  
SET @ComparePrice = @MaxPrice;  
GO  
  
```  
  
 `usp_GetList` 를 실행하여 가격이 $700 미만인 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 제품(자전거) 목록을 반환합니다. OUTPUT 매개 변수인 **@cost** 와 **@compareprices** 는 **메시지** 창의 메시지를 반환하기 위해 흐름 제어 언어와 함께 사용됩니다.  
  
> [!NOTE]  
>  OUTPUT 변수는 프로시저를 만들 때와 변수를 사용할 때 정의되어야 합니다. 매개 변수 이름과 변수 이름은 일치하지 않아도 되지만 **@listprice=** *variable*을 사용하지 않는 경우 데이터 형식과 매개 변수 위치는 일치해야 합니다.  
  
```  
DECLARE @ComparePrice money, @Cost money ;  
EXECUTE Production.uspGetList '%Bikes%', 700,   
    @ComparePrice OUT,   
    @Cost OUTPUT  
IF @Cost <= @ComparePrice   
BEGIN  
    PRINT 'These products can be purchased for less than   
    $'+RTRIM(CAST(@ComparePrice AS varchar(20)))+'.'  
END  
ELSE  
    PRINT 'The prices for all products in this category exceed   
    $'+ RTRIM(CAST(@ComparePrice AS varchar(20)))+'.';  
  
```  
  
 다음은 결과 집합의 일부입니다.  
  
```  
Product                                            List Price  
-------------------------------------------------- ------------------  
Road-750 Black, 58                                 539.99  
Mountain-500 Silver, 40                            564.99  
Mountain-500 Silver, 42                            564.99  
...  
Road-750 Black, 48                                 539.99  
Road-750 Black, 52                                 539.99  
  
(14 row(s) affected)  
  
These items can be purchased for less than $700.00.  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
  
