---
title: ERROR_PROCEDURE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ERROR_PROCEDURE_TSQL
- ERROR_PROCEDURE
dev_langs:
- TSQL
helpviewer_keywords:
- ERROR_PROCEDURE function
- messages [SQL Server], trigger where occurred
- errors [SQL Server], stored procedure where occurred
- TRY...CATCH [SQL Server]
- CATCH block
- messages [SQL Server], stored procedure where occurred
- errors [SQL Server], trigger where occurred
ms.assetid: b81edbf0-856a-498f-ba87-48ff1426d980
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd5bd076bd3ee690d834c27f37544b8fd4ab6402
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="errorprocedure-transact-sql"></a>ERROR_PROCEDURE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  TRY...CATCH 구문의 CATCH 블록이 실행되는 오류가 발생한 저장 프로시저나 트리거의 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ERROR_PROCEDURE ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar (128)**  
  
## <a name="return-value"></a>반환 값  
 CATCH 블록에서 호출된 경우 오류가 발생한 저장 프로시저 이름을 반환합니다.  
  
 오류가 저장 프로시저나 트리거 내에서 발생하지 않은 경우 NULL을 반환합니다.  
  
 CATCH 블록 범위 밖에서 호출된 경우 NULL을 반환합니다.  
  
## <a name="remarks"></a>주의  
 CATCH 블록 범위 내의 아무 위치에서나 ERROR_PROCEDURE를 호출할 수 있습니다.  
  
 ERROR_PROCEDURE는 호출 횟수나 CATCH 블록 범위 내에서 호출된 위치에 관계없이 오류가 발생한 저장 프로시저나 트리거의 이름을 반환합니다. 이와 달리, 함수 등@ERROR를 바로 다음에 오류를 발생 시킨 문 또는 CATCH 블록의 첫 번째 문에서 오류 번호를 반환 하 합니다.  
  
 중첩된 CATCH 블록에서 ERROR_PROCEDURE는 참조되는 CATCH 블록의 범위에 해당하는 저장 프로시저나 트리거의 이름을 반환합니다. 예를 들어 TRY…CATCH 구문의 CATCH 블록에 중첩된 TRY…CATCH를 사용할 수 있습니다. 중첩된 CATCH 블록 내에서 ERROR_PROCEDURE는 중첩된 CATCH 블록을 호출했으나 오류가 발생한 저장 프로시저나 트리거의 이름을 반환합니다. ERROR_PROCEDURE가 외부 CATCH 블록에서 실행되는 경우 해당 CATCH 블록을 호출했으나 오류가 발생한 저장 프로시저나 트리거의 이름을 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-errorprocedure-in-a-catch-block"></a>1. CATCH 블록에서 ERROR_PROCEDURE 사용  
 다음 코드 예에서는 0으로 나누기 오류를 생성하는 저장 프로시저를 보여 줍니다. `ERROR_PROCEDURE`는 오류가 발생한 저장 프로시저의 이름을 반환합니다.  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_PROCEDURE() AS ErrorProcedure;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorprocedure-in-a-catch-block-with-other-error-handling-tools"></a>2. CATCH 블록에서 다른 오류 처리 도구와 함께 ERROR_PROCEDURE 사용  
 다음 코드 예에서는 0으로 나누기 오류를 생성하는 저장 프로시저를 보여 줍니다. 오류가 발생한 저장 프로시저 이름과 함께 해당 오류에 관한 정보가 반환됩니다.  
  
```  
  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_MESSAGE() AS ErrorMessage,  
        ERROR_LINE() AS ErrorLine;  
        END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errorprocedure-in-a-catch-block"></a>3. CATCH 블록에서 ERROR_PROCEDURE 사용  
 다음 코드 예에서는 0으로 나누기 오류를 생성하는 저장 프로시저를 보여 줍니다. `ERROR_PROCEDURE`는 오류가 발생한 저장 프로시저의 이름을 반환합니다.  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_PROCEDURE() AS ErrorProcedure;  
END CATCH;  
GO  
```  
  
### <a name="d-using-errorprocedure-in-a-catch-block-with-other-error-handling-tools"></a>4. CATCH 블록에서 다른 오류 처리 도구와 함께 ERROR_PROCEDURE 사용  
 다음 코드 예에서는 0으로 나누기 오류를 생성하는 저장 프로시저를 보여 줍니다. 오류가 발생한 저장 프로시저 이름과 함께 해당 오류에 관한 정보가 반환됩니다.  
  
```  
  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_MESSAGE() AS ErrorMessage;  
        END CATCH;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE&#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [Error_state&#40; Transact SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  


