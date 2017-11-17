---
title: "저장 프로시저에서 데이터 반환 | Microsoft 문서"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedures [SQL Server], returning data
- returning data from stored procedure
ms.assetid: 7a428ffe-cd87-4f42-b3f1-d26aa8312bf7
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 715ce3fff853f4eab433d095ffd952033defad69
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="return-data-from-a-stored-procedure"></a>저장 프로시저에서 데이터 반환
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 > 이전 버전의 SQL Server와 관련된 콘텐츠 [저장 프로시저에서 데이터 반환](https://msdn.microsoft.com/en-US/library/ms188655(SQL.120).aspx)을 참조하세요.

  결과 집합 또는 데이터를 프로시저에서 호출 프로그램으로 반환하는 두 가지 방법인 출력 매개 변수 및 반환 코드가 있습니다. 이 항목은 두 방법에 대한 자세한 정보를 제공합니다.  
  
## <a name="returning-data-using-an-output-parameter"></a>출력 매개 변수를 사용하여 데이터 반환  
 프로시저 정의에서 매개 변수에 OUTPUT 키워드를 지정하면 해당 프로시저는 종료될 때 매개 변수의 현재 값을 호출 프로그램에 반환할 수 있습니다. 호출 프로그램에서 사용할 수 있는 변수에 매개 변수 값을 저장하려면 호출 프로그램이 프로시저를 실행할 때 OUTPUT 키워드를 사용해야 합니다. 출력 매개 변수로 사용될 수 있는 데이터 형식에 대한 자세한 내용은 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)를 참조하세요.  
  
### <a name="examples-of-output-parameter"></a>출력 매개 변수의 예  
 다음 예에서는 입력 및 출력 매개 변수가 있는 프로시저를 보여 줍니다. `@SalesPerson` 매개 변수는 호출 프로그램이 지정한 입력 값을 받습니다. SELECT 문은 입력 매개 변수에 전달된 값을 사용하여 정확한 `SalesYTD` 값을 가져옵니다. 또한 SELECT 문은 `@SalesYTD` 출력 매개 변수에 값을 할당하여 해당 프로시저가 종료될 때 호출 프로그램으로 값을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetEmployeeSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetEmployeeSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetEmployeeSalesYTD  
@SalesPerson nvarchar(50),  
@SalesYTD money OUTPUT  
AS    
  
    SET NOCOUNT ON;  
    SELECT @SalesYTD = SalesYTD  
    FROM Sales.SalesPerson AS sp  
    JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
    WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 다음 예에서는 첫 번째 예에 생성된 프로시저를 호출하고 호출 프로그램의 지역 변수인 `@SalesYTD` 변수의 호출된 프로시저로부터 반환된 출력 값을 저장합니다.  
  
```  
-- Declare the variable to receive the output value of the procedure.  
DECLARE @SalesYTDBySalesPerson money;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTDBySalesPerson  
EXECUTE Sales.uspGetEmployeeSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDBySalesPerson OUTPUT;  
-- Display the value returned by the procedure.  
PRINT 'Year-to-date sales for this employee is ' +   
    convert(varchar(10),@SalesYTDBySalesPerson);  
GO  
  
```  
  
 프로시저를 실행할 때 OUTPUT 매개 변수에 입력 값을 지정할 수도 있습니다. 이렇게 하면 프로시저가 호출 프로그램으로부터 값을 받아 변경하거나 연산을 수행한 다음 호출 프로그램에 새 값을 반환할 수 있습니다. 이전 예에서는 프로그램이 `@SalesYTDBySalesPerson` 프로시저를 호출하기 전에 `Sales.uspGetEmployeeSalesYTD` 변수에 값을 할당할 수 있습니다. execute 문은 `@SalesYTDBySalesPerson` 변수 값을 `@SalesYTD` OUTPUT 매개 변수로 전달할 수 있습니다. 그러면 프로시저 본문에서 해당 값을 새로운 값을 생성하는 계산에 사용될 수 있습니다. 새로운 값은 OUTPUT 매개 변수를 통해 프로시저 밖으로 다시 전달되어 프로시저가 종료될 때 `@SalesYTDBySalesPerson` 변수의 값으로 업데이트됩니다. 이것을 "참조 전달(pass-by-reference) 기능"이라고 합니다.  
  
 프로시저를 호출할 때 매개 변수에 OUTPUT을 지정하고 그 매개 변수가 프로시저 정의에서 OUTPUT을 사용하여 정의되지 않은 경우 오류 메시지가 나타납니다. 그러나 출력 매개 변수가 있는 프로시저를 실행할 수는 있지만 프로시저를 실행할 때는 OUTPUT을 지정할 수 없습니다. 오류가 반환되지는 않지만 호출 프로그램에서 출력 값을 사용할 수 없습니다.  
  
### <a name="using-the-cursor-data-type-in-output-parameters"></a>OUTPUT 매개 변수에 Cursor 데이터 형식 사용  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저는 OUTPUT 매개 변수에만 **cursor** 데이터 형식을 사용할 수 있습니다. 매개 변수에 **cursor** 데이터 형식을 지정한 경우에는 프로시저 정의에서 해당 매개 변수에 대해 VARYING 및 OUTPUT 키워드 모두 지정되어야 합니다. 매개 변수는 OUTPUT으로만 지정될 수 있지만 매개 변수 선언 시 VARYING 키워드가 지정된 경우에는 데이터 형식은 **cursor** 여야 하고 OUTPUT 키워드도 지정되어야 합니다.  
  
> [!NOTE]  
>  **cursor** 데이터 형식은 OLE DB, ODBC, ADO, DB-Library 등의 데이터베이스 API를 통해 응용 프로그램 변수에 바인딩할 수 없습니다. OUTPUT 매개 변수는 응용 프로그램이 프로시저를 실행하기 전에 바인딩되어야 하므로 **cursor** OUTPUT 매개 변수가 있는 프로시저는 데이터베이스 API에서 호출할 수 없습니다. 이러한 프로시저는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 로컬 **cursor** 변수에 [!INCLUDE[tsql](../../includes/tsql-md.md)] cursor **OUTPUT 변수가 할당된 경우에만** 일괄 처리, 프로시저 또는 트리거에서 호출할 수 있습니다.  
  
### <a name="rules-for-cursor-output-parameters"></a>Cursor Output 매개 변수 규칙  
 프로시저 실행 시 **cursor** Output 매개 변수에는 다음 규칙이 적용됩니다.  
  
-   정방향 전용 커서의 경우, 프로시저의 실행이 끝났을 때 커서의 결과 집합에는 커서 위치와 같거나 이보다 뒤에 있는 행만 반환됩니다. 예를 들면 다음과 같습니다.  
  
    -   비스크롤형 커서는 프로시저에서 100개의 행이 있는 RS라는 결과 집합에 열려 있습니다.  
  
    -   프로시저는 RS 결과 집합의 처음 5개 행을 인출합니다.  
  
    -   프로시저가 호출자에게 반환됩니다.  
  
    -   호출자에게 반환된 RS 결과 집합은 6에서 100 사이인 RS의 행으로 구성되며 호출자의 커서는 RS의 첫 번째 행 앞에 놓입니다.  
  
-   정방향 전용 커서의 경우, 프로시저의 실행이 끝났을 때 커서가 첫 번째 행보다 앞에 있으면 호출한 일괄 처리, 프로시저, 트리거에 전체 결과 집합이 반환됩니다. 반환될 때 커서 위치는 첫 번째 행 앞으로 설정됩니다.  
  
-   정방향 전용 커서의 경우, 프로시저의 실행이 끝났을 때 커서가 마지막 행보다 뒤에 있으면 호출한 일괄 처리, 프로시저, 트리거에 빈 결과 집합이 반환됩니다.  
  
    > [!NOTE]  
    >  빈 결과 집합은 Null 값과 다릅니다.  
  
-   스크롤형 커서의 경우, 프로시저의 실행이 끝났을 때 결과 집합의 모든 행이 호출한 일괄 처리, 프로시저, 트리거에 반환됩니다. 반환될 때 커서 위치는 프로시저에서 마지막으로 실행된 인출 위치가 됩니다.  
  
-   커서의 종류에 관계없이 커서를 닫으면 호출한 일괄 처리, 프로시저, 트리거에 Null 값이 전달됩니다. 매개 변수에 커서를 할당했지만 해당 커서를 전혀 열지 않은 경우도 마찬가지입니다.  
  
    > [!NOTE]  
    >  커서의 닫힌 상태는 반환 시에만 문제가 됩니다. 예를 들어 프로시저를 통해 커서를 일부 닫은 후 프로시저에서 나중에 다시 열어 호출한 일괄 처리, 프로시저, 트리거에 커서의 결과 집합을 반환하는 것은 유효합니다.  
  
### <a name="examples-of-cursor-output-parameters"></a>Cursor Output 매개 변수의 예  
 다음 예에서는 **cursor** 데이터 형식을 사용하여 출력 매개 변수 `@currency_cursor`를 지정하는 프로시저가 생성됩니다. 그런 다음 일괄 처리로 프로시저가 호출됩니다.  
  
 먼저 선언된 프로시저를 만들고 Currency 테이블에서 커서를 엽니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspCurrencyCursor', 'P' ) IS NOT NULL  
    DROP PROCEDURE dbo.uspCurrencyCursor;  
GO  
CREATE PROCEDURE dbo.uspCurrencyCursor   
    @CurrencyCursor CURSOR VARYING OUTPUT  
AS  
    SET NOCOUNT ON;  
    SET @CurrencyCursor = CURSOR  
    FORWARD_ONLY STATIC FOR  
      SELECT CurrencyCode, Name  
      FROM Sales.Currency;  
    OPEN @CurrencyCursor;  
GO  
  
```  
  
 다음으로 지역 커서 변수를 선언하는 일괄 처리를 실행하고, 지역 변수에 커서를 할당하는 프로시저를 실행한 다음, 커서에서 행을 인출합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyCursor CURSOR;  
EXEC dbo.uspCurrencyCursor @CurrencyCursor = @MyCursor OUTPUT;  
WHILE (@@FETCH_STATUS = 0)  
BEGIN;  
     FETCH NEXT FROM @MyCursor;  
END;  
CLOSE @MyCursor;  
DEALLOCATE @MyCursor;  
GO  
  
```  
  
## <a name="returning-data-using-a-return-code"></a>반환 코드를 사용하여 데이터 반환  
 프로시저는 반환 코드라고 하는 정수 값을 반환하여 프로시저의 실행 상태를 나타낼 수 있습니다. RETURN 문을 사용하여 프로시저의 반환 코드를 지정할 수 있습니다. OUTPUT 매개 변수에서와 같이 프로시저가 실행될 때 호출 프로그램에서 사용할 수 있도록 반환 코드 값을 변수에 저장해야 합니다. 예를 들어 `@result` int **데이터 형식의** 할당 변수는 다음과 같은 `my_proc`프로시저의 반환 코드를 저장하는 데 사용됩니다.  
  
```  
DECLARE @result int;  
EXECUTE @result = my_proc;  
```  
  
 반환 코드는 대개 프로시저의 흐름 제어 블록에서 발생 가능한 각 오류 상태의 반환 코드 값을 설정하는 데 사용됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 다음에 @@ERROR 함수를 사용하면 문이 실행될 때 오류가 발생했는지 여부를 알 수 있습니다.  
  
### <a name="examples-of-return-codes"></a>반환 코드의 예  
 다음 예에서는 여러 오류에 대한 특정 반환 코드 값을 설정하는 오류 처리가 포함된 `usp_GetSalesYTD` 프로시저를 보여 줍니다. 다음 표에서는 발생 가능한 각 오류에 프로시저에서 할당한 정수 값 및 각 값에 해당하는 의미를 보여 줍니다.  
  
|반환 코드 값|의미|  
|-----------------------|-------------|  
|0|성공한 실행 수입니다.|  
|1|필요한 매개 변수 값이 지정되지 않았습니다.|  
|2|지정된 매개 변수 값이 잘못되었습니다.|  
|3|판매량을 가져오는 동안 오류가 발생했습니다.|  
|4|판매 직원의 NULL 판매량을 찾았습니다.|  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.usp_GetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.usp_GetSalesYTD;  
GO  
CREATE PROCEDURE Sales.usp_GetSalesYTD  
@SalesPerson nvarchar(50) = NULL,  -- NULL default value  
@SalesYTD money = NULL OUTPUT  
AS    
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
   BEGIN  
       PRINT 'ERROR: You must specify a last name for the sales person.'  
       RETURN(1)  
   END  
ELSE  
   BEGIN  
   -- Make sure the value is valid.  
   IF (SELECT COUNT(*) FROM HumanResources.vEmployee  
          WHERE LastName = @SalesPerson) = 0  
      RETURN(2)  
   END  
-- Get the sales for the specified name and   
-- assign it to the output parameter.  
SELECT @SalesYTD = SalesYTD   
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
-- Check for SQL Server errors.  
IF @@ERROR <> 0   
   BEGIN  
      RETURN(3)  
   END  
ELSE  
   BEGIN  
   -- Check to see if the ytd_sales value is NULL.  
     IF @SalesYTD IS NULL  
       RETURN(4)   
     ELSE  
      -- SUCCESS!!  
        RETURN(0)  
   END  
-- Run the stored procedure without specifying an input value.  
EXEC Sales.usp_GetSalesYTD;  
GO  
-- Run the stored procedure with an input value.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTD  
EXECUTE Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
PRINT N'Year-to-date sales for this employee is ' +  
    CONVERT(varchar(10), @SalesYTDForSalesPerson);  
  
```  
  
 다음 예에서는 `usp_GetSalesYTD` 프로시저에서 반환되는 반환 코드를 처리하기 위한 프로그램을 만듭니다.  
  
```  
-- Declare the variables to receive the output value and return code   
-- of the procedure.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
  
-- Execute the procedure with a title_id value  
-- and save the output value and return code in variables.  
EXECUTE @ret_code = Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
--  Check the return codes.  
IF @ret_code = 0  
BEGIN  
   PRINT 'Procedure executed successfully'  
   -- Display the value returned by the procedure.  
   PRINT 'Year-to-date sales for this employee is ' + CONVERT(varchar(10),@SalesYTDForSalesPerson)  
END  
ELSE IF @ret_code = 1  
   PRINT 'ERROR: You must specify a last name for the sales person.'  
ELSE IF @ret_code = 2   
   PRINT 'EERROR: You must enter a valid last name for the sales person.'  
ELSE IF @ret_code = 3  
   PRINT 'ERROR: An error occurred getting sales value.'  
ELSE IF @ret_code = 4  
   PRINT 'ERROR: No sales recorded for this employee.'     
GO  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [PRINT&#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)   
 [커서](../../relational-databases/cursors.md)   
 [RETURN&#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  

