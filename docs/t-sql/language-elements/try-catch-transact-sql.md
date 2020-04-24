---
title: TRY...CATCH(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BEGIN_TRY_TSQL
- BEGIN_CATCH_TSQL
- TRY
- BEGIN TRY
- TRY_TSQL
- BEGIN CATCH
dev_langs:
- TSQL
helpviewer_keywords:
- BEGIN CATCH statement
- uncommittable transactions
- errors [SQL Server], TRY...CATCH
- TRY block [SQL Server]
- XACT_STATE function
- TRY...CATCH [SQL Server]
- BEGIN TRY statement
- CATCH block
ms.assetid: 248df62a-7334-4bca-8262-235a28f4b07f
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d82edc30239cb036befc428d25e530ccabf1cdf
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634895"
---
# <a name="trycatch-transact-sql"></a>TRY...CATCH(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]


  [!INCLUDE[tsql](../../includes/tsql-md.md)] Visual C# 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++ 언어의 예외 처리와 유사한 방식으로 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서 오류 처리를 구현합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 그룹을 TRY 블록으로 묶을 수 있으며 TRY 블록 내에서 오류가 발생하는 경우 CATCH 블록으로 묶은 또 다른 문의 그룹으로 제어가 전달됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
BEGIN TRY  
     { sql_statement | statement_block }  
END TRY  
BEGIN CATCH  
     [ { sql_statement | statement_block } ]  
END CATCH  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *sql_statement*  
 임의의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다.  
  
 *statement_block*  
 일괄 처리나 BEGIN...END 블록으로 묶은 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 그룹입니다.  
  
## <a name="remarks"></a>설명  
 TRY...CATCH 구문은 심각도가 10을 넘으며 데이터베이스 연결을 닫지 않는 모든 실행 오류를 catch합니다.  
  
 TRY 블록 다음에는 곧바로 연결된 CATCH 블록이 이어져야 합니다. END TRY와 BEGIN CATCH 문 사이에 다른 문을 포함시키면 구문 오류가 발생합니다.  
  
 TRY...CATCH 구문은 여러 일괄 처리에 걸쳐 있을 수 없으며 여러 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 블록에도 걸쳐 있을 수 없습니다. 예를 들어 하나의 TRY...CATCH 구문이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 BEGIN…END 블록 2개에 걸쳐 있거나 IF...ELSE 구문에 걸쳐 있을 수 없습니다.  
  
 TRY 블록의 마지막 문 실행을 완료할 때 TRY 블록으로 묶은 코드에 오류가 없는 경우 연결된 END CATCH 문 바로 다음 문으로 제어가 전달됩니다.
 
 TRY 블록으로 묶은 코드에 오류가 있는 경우 연결된 CATCH 블록의 첫 번째 문으로 제어가 전달됩니다. CATCH 블록의 코드를 완료하면 END CATCH 문 바로 다음 문으로 제어가 전달됩니다. 
 
 > [!NOTE] 
 > END CATCH 문이 저장 프로시저 또는 트리거의 마지막 문인 경우 해당 저장 프로시저를 호출하거나 트리거를 발생시킨 문으로 제어가 전달됩니다. 
 
 CATCH 블록이 포착한 오류는 호출 애플리케이션으로 반환되지 않습니다. 오류 정보를 애플리케이션으로 반환해야 하는 경우 CATCH 블록의 코드에서 SELECT 결과 집합 또는 RAISERROR 및 PRINT 문과 같은 메커니즘을 사용하세요.  
  
 TRY...CATCH 구문은 중첩될 수 있습니다. TRY 블록 또는 CATCH 블록에는 중첩된 TRY...CATCH 구문이 포함될 수 있습니다. 예를 들어 CATCH 블록에 TRY...CATCH 구문이 포함되어 CATCH 코드가 발견하는 오류를 처리할 수 있습니다.  
  
 CATCH 블록에서 발견되는 오류는 다른 곳에서 발생한 오류와 같이 취급됩니다. CATCH 블록에 중첩된 TRY...CATCH 구문이 포함되는 경우 중첩된 TRY 블록의 모든 오류는 중첩된 CATCH 블록으로 제어를 전달합니다. 중첩된 TRY...CATCH 구문이 없는 경우 호출자에게 오류를 다시 전달합니다.  
  
 TRY...CATCH 구문은 TRY 블록의 코드에서 실행된 저장 프로시저 또는 트리거에서 처리되지 않은 오류를 catch합니다. 또는 저장 프로시저나 트리거에는 해당 코드에서 발생된 오류를 처리할 수 있도록 TRY...CATCH 구문이 포함될 수 있습니다. 예를 들어 TRY 블록이 저장 프로시저를 실행하고 해당 저장 프로시저에서 오류가 발생하는 경우 다음과 같은 방법으로 오류를 처리할 수 있습니다.  
  
-   저장 프로시저에 해당 TRY...CATCH 구문이 포함되지 않는 경우 오류가 발생하면 EXECUTE 문을 포함하는 TRY 블록과 연결된 CATCH 블록으로 제어가 반환됩니다.  
  
-   저장 프로시저에 TRY...CATCH 구문이 포함되는 경우 오류가 발생하면 저장 프로시저의 CATCH 블록으로 제어가 전달됩니다. CATCH 블록 코드를 완료하면 해당 저장 프로시저를 호출한 EXECUTE 문 바로 다음 문으로 제어가 전달됩니다.  
  
 GOTO 문을 사용하여 TRY 또는 CATCH 블록에 진입할 수 없지만 동일한 TRY 또는 CATCH 블록 내의 레이블로 이동하거나 TRY 또는 CATCH 블록에서 나가는 것은 가능합니다.  
  
 사용자 정의 함수에서는 TRY...CATCH 구문을 사용할 수 없습니다.  
  
## <a name="retrieving-error-information"></a>오류 정보 검색  
 CATCH 블록의 범위에서 다음 시스템 함수를 사용하여 CATCH 블록을 실행하도록 만든 오류에 대한 정보를 얻을 수 있습니다.  
  
-   [ERROR_NUMBER()](../../t-sql/functions/error-number-transact-sql.md)는 오류 번호를 반환합니다.  
  
-   [ERROR_SEVERITY()](../../t-sql/functions/error-severity-transact-sql.md)는 심각도를 반환합니다.  
  
-   [ERROR_STATE()](../../t-sql/functions/error-state-transact-sql.md)는 오류 상태 번호를 반환합니다.  
  
-   [ERROR_PROCEDURE()](../../t-sql/functions/error-procedure-transact-sql.md)는 오류가 발생한 저장 프로시저 또는 트리거의 이름을 반환합니다.  
  
-   [ERROR_LINE()](../../t-sql/functions/error-line-transact-sql.md)은 오류를 발생시킨 루틴 내의 줄 번호를 반환합니다.  
  
-   [ERROR_MESSAGE()](../../t-sql/functions/error-message-transact-sql.md)는 오류 메시지의 전체 텍스트를 반환합니다. 이 텍스트는 길이, 개체 이름 또는 시간과 같은 대체 가능한 매개 변수에 제공된 값을 포함합니다.  
  
CATCH 블록의 범위를 벗어나서 이러한 함수를 호출하면 NULL이 반환됩니다. CATCH 블록의 범위 내 어디에서나 이들 함수를 사용하여 오류 정보를 검색할 수 있습니다. 예를 들어 다음 스크립트는 오류 처리 함수를 포함하는 저장 프로시저를 보여 줍니다. `CATCH` 구문의 `TRY...CATCH` 블록에서 이 저장 프로시저를 호출하면 오류에 대한 정보가 반환됩니다.  
  
```sql  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_GetErrorInfo', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_GetErrorInfo;  
GO  
  
-- Create procedure to retrieve error information.  
CREATE PROCEDURE usp_GetErrorInfo  
AS  
SELECT  
    ERROR_NUMBER() AS ErrorNumber  
    ,ERROR_SEVERITY() AS ErrorSeverity  
    ,ERROR_STATE() AS ErrorState  
    ,ERROR_PROCEDURE() AS ErrorProcedure  
    ,ERROR_LINE() AS ErrorLine  
    ,ERROR_MESSAGE() AS ErrorMessage;  
GO  
  
BEGIN TRY  
    -- Generate divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    -- Execute error retrieval routine.  
    EXECUTE usp_GetErrorInfo;  
END CATCH;   
```  
  
 ERROR\_\* 함수는 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md) 안의 `CATCH` 블록에서도 작동합니다.  
  
## <a name="errors-unaffected-by-a-trycatch-construct"></a>TRY...CATCH 구문의 영향을 받지 않는 오류  
 TRY...CATCH 구문은 다음과 같은 조건을 트래핑하지 않습니다.  
  
-   심각도가 10 이하인 경고 또는 정보 메시지  
  
-   해당 세션에 대한 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 태스크 처리를 중지하게 만드는 심각도 20 이상의 오류. 심각도가 20 이상인 오류가 발생하고 데이터베이스 연결이 끊기지 않은 경우 TRY...CATCH 구문이 오류를 처리합니다.  
  
-   클라이언트 인터럽트 요청 또는 클라이언트 연결 끊김과 같은 주의  
  
-   시스템 관리자가 KILL 문을 사용하여 세션을 종료할 때  
  
다음 유형의 오류가 TRY...CATCH 구문과 동일한 실행 수준에서 발생하는 경우 CATCH 블록에서 처리되지 않습니다.  
  
-   구문 오류와 같이 일괄 처리의 실행을 막는 컴파일 오류  
  
-   문 수준 다시 컴파일 단계에서 발생한 오류(예: 컴파일 이후에 지연된 이름 확인으로 발생한 개체 이름 확인 오류)  
-   개체 이름 확인 오류   

  
이런 오류는 해당 일괄 처리, 저장 프로시저 또는 트리거를 실행한 수준으로 반환됩니다.  
  
TRY 블록 내의 더 낮은 실행 수준(예: sp_executesql 또는 사용자 정의 저장 프로시저 실행 시)에서 컴파일하는 동안 또는 명령문 수준으로 다시 컴파일하는 동안 오류가 발생하는 경우 이 오류는 TRY...CATCH 구문보다 낮은 수준에서 발생하며 연결된 CATCH 블록에서 처리됩니다.  
  
다음 예에서는 `SELECT` 문에서 발생한 개체 이름 확인 오류가 `TRY...CATCH` 구문으로는 포착되지 않지만 저장 프로시저 내에서 동일한 `CATCH` 문을 실행할 때 `SELECT` 블록에서 포착되는 상황을 보여 줍니다.  
  
```sql  
BEGIN TRY  
    -- Table does not exist; object name resolution  
    -- error not caught.  
    SELECT * FROM NonexistentTable;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber  
       ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH  
```  
  
 오류가 포착되지 않고 `TRY...CATCH` 구문 밖으로 제어가 전달되어 다음으로 높은 수준으로 이동됩니다.  
  
 저장 프로시저 내에서 `SELECT` 문을 실행하면 `TRY` 블록보다 낮은 수준에서 오류가 발생하여 `TRY...CATCH` 구문에서 오류를 처리할 수 있습니다.  
  
```sql  
-- Verify that the stored procedure does not exist.  
IF OBJECT_ID ( N'usp_ExampleProc', N'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that will cause an   
-- object resolution error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT * FROM NonexistentTable;  
GO  
  
BEGIN TRY  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
```  
  
## <a name="uncommittable-transactions-and-xact_state"></a>커밋 불가능 트랜잭션 및 XACT_STATE  
 TRY 블록에서 생성된 오류로 인해 현재 트랜잭션의 상태가 무효화되는 경우 그 트랜잭션은 커밋 불가능 트랜잭션으로 분류됩니다. 일반적으로 TRY 블록 바깥에서 트랜잭션을 종료하게 만드는 오류가 TRY 블록 내부에서 발생하면 트랜잭션이 커밋 불가능 상태가 됩니다. 커밋 불가능 트랜잭션은 읽기 작업 또는 ROLLBACK TRANSACTION만 수행할 수 있습니다. 커밋할 수 없는 트랜잭션은 쓰기 작업 또는 COMMIT TRANSACTION을 생성하는 어떤 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문도 실행할 수 없습니다. 어떤 트랜잭션이 커밋 불가능 트랜잭션으로 분류된 경우 XACT_STATE 함수는 -1 값을 반환합니다. 일괄 처리가 완료되면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 커밋 불가능 활성 트랜잭션을 모두 롤백합니다. 트랜잭션이 커밋할 수 없는 상태가 되었을 때 오류 메시지가 전송되지 않은 경우 일괄 처리가 완료되면 오류 메시지가 클라이언트 애플리케이션으로 전송됩니다. 이 메시지는 커밋 불가능 트랜잭션이 검색되어 롤백되었음을 보여 줍니다.  
  
 커밋 불가능 트랜잭션과 XACT_STATE 함수에 대한 자세한 내용은 [XACT_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/xact-state-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-trycatch"></a>A. TRY...CATCH 사용  
 다음 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. 이 오류로 인해 연결된 `CATCH` 블록으로 실행이 이동합니다.  
  
```sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
### <a name="b-using-trycatch-in-a-transaction"></a>B. 트랜잭션에서 TRY...CATCH 사용  
 다음 예에서는 트랜잭션 내에서 `TRY...CATCH` 블록이 작동하는 방법을 보여 줍니다. `TRY` 블록 내의 문은 제약 조건 위반 오류를 일으킵니다.  
  
```sql  
BEGIN TRANSACTION;  
  
BEGIN TRY  
    -- Generate a constraint violation error.  
    DELETE FROM Production.Product  
    WHERE ProductID = 980;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
  
    IF @@TRANCOUNT > 0  
        ROLLBACK TRANSACTION;  
END CATCH;  
  
IF @@TRANCOUNT > 0  
    COMMIT TRANSACTION;  
GO  
```  
  
### <a name="c-using-trycatch-with-xact_state"></a>C. XACT_STATE에서 TRY...CATCH 사용  
 다음 예에서는 트랜잭션 내부에서 발생하는 오류를 `TRY...CATCH` 구문을 사용하여 처리하는 방법을 보여 줍니다. 트랜잭션을 커밋해야 하는지 또는 롤백해야 하는지는 `XACT_STATE` 함수가 결정합니다. 이 예에서 `SET XACT_ABORT`는 `ON`입니다. 이렇게 하면 제약 조건 위반 오류가 발생할 경우 트랜잭션을 커밋할 수 없습니다.  
  
```sql  
-- Check to see whether this stored procedure exists.  
IF OBJECT_ID (N'usp_GetErrorInfo', N'P') IS NOT NULL  
    DROP PROCEDURE usp_GetErrorInfo;  
GO  
  
-- Create procedure to retrieve error information.  
CREATE PROCEDURE usp_GetErrorInfo  
AS  
    SELECT   
         ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_LINE () AS ErrorLine  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_MESSAGE() AS ErrorMessage;  
GO  
  
-- SET XACT_ABORT ON will cause the transaction to be uncommittable  
-- when the constraint violation occurs.   
SET XACT_ABORT ON;  
  
BEGIN TRY  
    BEGIN TRANSACTION;  
        -- A FOREIGN KEY constraint exists on this table. This   
        -- statement will generate a constraint violation error.  
        DELETE FROM Production.Product  
            WHERE ProductID = 980;  
  
    -- If the DELETE statement succeeds, commit the transaction.  
    COMMIT TRANSACTION;  
END TRY  
BEGIN CATCH  
    -- Execute error retrieval routine.  
    EXECUTE usp_GetErrorInfo;  
  
    -- Test XACT_STATE:  
        -- If 1, the transaction is committable.  
        -- If -1, the transaction is uncommittable and should   
        --     be rolled back.  
        -- XACT_STATE = 0 means that there is no transaction and  
        --     a commit or rollback operation would generate an error.  
  
    -- Test whether the transaction is uncommittable.  
    IF (XACT_STATE()) = -1  
    BEGIN  
        PRINT  
            N'The transaction is in an uncommittable state.' +  
            'Rolling back transaction.'  
        ROLLBACK TRANSACTION;  
    END;  
  
    -- Test whether the transaction is committable.  
    IF (XACT_STATE()) = 1  
    BEGIN  
        PRINT  
            N'The transaction is committable.' +  
            'Committing transaction.'  
        COMMIT TRANSACTION;     
    END;  
END CATCH;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-trycatch"></a>D. TRY...CATCH 사용  
 다음 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. 이 오류로 인해 연결된 `CATCH` 블록으로 실행이 이동합니다.  
  
```sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [데이터베이스 엔진 오류 심각도](../../relational-databases/errors-events/database-engine-error-severities.md)   
 [ERROR_LINE&#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)   
 [GOTO &#40;Transact-SQL&#41;](../../t-sql/language-elements/goto-transact-sql.md)   
 [BEGIN...END &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [XACT_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/xact-state-transact-sql.md)   
 [SET XACT_ABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-xact-abort-transact-sql.md)  
  
  

