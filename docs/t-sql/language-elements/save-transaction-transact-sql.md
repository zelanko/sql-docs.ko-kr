---
title: "트랜잭션 (Transact SQL) 저장 | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SAVE
- SAVE_TSQL
- SAVE_TRANSACTION_TSQL
- SAVE TRANSACTION
dev_langs: TSQL
helpviewer_keywords:
- rolling back transactions, SAVE TRANSACTION
- SAVE TRANSACTION statement
- transactions [SQL Server], rolling back
- marking transactions [SQL Server]
- savepoints [SQL Server]
- marked transactions [SQL Server], SAVE TRANSACTION statement
- duplicate savepoints
ms.assetid: b953c3f1-f96d-42f1-95a2-30e314292b35
caps.latest.revision: "53"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 715c7bd289f8cd2133799e268e14a31a48290b7a
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="save-transaction-transact-sql"></a>SAVE TRANSACTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  트랜잭션 내에서 저장점을 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
.|  
 ## <a name="syntax"></a>구문  
  
```  
  
SAVE { TRAN | TRANSACTION } { savepoint_name | @savepoint_variable }  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *savepoint_name*  
 저장점에 할당된 이름입니다. 저장점 이름은 식별자에 적용되는 규칙을 준수해야 하지만 길이는 32자로 제한됩니다. *savepoint_name* 항상 대/소문자 구분, 경우에 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대/소문자를 무시 합니다.  
  
 @*savepoint_variable*  
 유효한 저장점 이름이 포함된 사용자 정의 변수의 이름입니다. 변수를 사용 하 여 선언 해야 합니다는 **char**, **varchar**, **nchar**, 또는 **nvarchar** 데이터 형식입니다. 변수에 32자 이상 전달할 수 있지만 전달된 문자의 처음부터 32자까지만 사용됩니다.  
  
## <a name="remarks"></a>주의  
 사용자가 트랜잭션 내에서 저장점 또는 표식을 설정할 수 있습니다. 저장점은 트랜잭션의 일부가 조건에 따라 취소될 경우에 트랜잭션이 되돌아갈 수 있는 위치를 정의합니다. 트랜잭션이 저장점으로 롤백되면 완료될 때까지 계속 실행되거나(필요할 경우 더 많은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 COMMIT TRANSACTION 문 사용) 트랜잭션을 시작 부분으로 롤백하여 모두 함께 취소되어야 합니다. 트랜잭션을 취소 하는 전체, 양식을 ROLLBACK TRANSACTION을 사용 하 여 *transaction_name*합니다. 트랜잭션의 모든 문이나 프로시저의 실행이 취소됩니다.  
  
 중복된 저장점 이름을 트랜잭션에서 사용할 수 있지만 저장점 이름을 지정하는 ROLLBACK TRANSACTION 문은 해당 이름을 사용하는 최신 SAVE TRANSACTION으로만 트랜잭션을 롤백합니다.  
  
 BEGIN DISTRIBUTED TRANSACTION으로 명시적으로 시작되거나 로컬 트랜잭션에서 에스컬레이션된 분산 트랜잭션에서는 SAVE TRANSACTION이 지원되지 않습니다.  
  
> [!IMPORTANT]  
>  savepoint_name을 지정하는 ROLLBACK TRANSACTION 문은 에스컬레이션과 변환을 제외하고 저장점을 초과하여 획득한 모든 잠금을 해제합니다. 이러한 잠금은 해제되지 않으며 이전 잠금 모드로 다시 변환되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 저장 프로시저가 실행되기 전에 활성 트랜잭션이 시작되는 경우 트랜잭션 저장점을 사용하여 저장 프로시저에서 수정된 내용만 롤백하는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
           WHERE name = N'SaveTranExample')  
    DROP PROCEDURE SaveTranExample;  
GO  
CREATE PROCEDURE SaveTranExample  
    @InputCandidateID INT  
AS  
    -- Detect whether the procedure was called  
    -- from an active transaction and save  
    -- that for later use.  
    -- In the procedure, @TranCounter = 0  
    -- means there was no active transaction  
    -- and the procedure started one.  
    -- @TranCounter > 0 means an active  
    -- transaction was started before the   
    -- procedure was called.  
    DECLARE @TranCounter INT;  
    SET @TranCounter = @@TRANCOUNT;  
    IF @TranCounter > 0  
        -- Procedure called when there is  
        -- an active transaction.  
        -- Create a savepoint to be able  
        -- to roll back only the work done  
        -- in the procedure if there is an  
        -- error.  
        SAVE TRANSACTION ProcedureSave;  
    ELSE  
        -- Procedure must start its own  
        -- transaction.  
        BEGIN TRANSACTION;  
    -- Modify database.  
    BEGIN TRY  
        DELETE HumanResources.JobCandidate  
            WHERE JobCandidateID = @InputCandidateID;  
        -- Get here if no errors; must commit  
        -- any transaction started in the  
        -- procedure, but not commit a transaction  
        -- started before the transaction was called.  
        IF @TranCounter = 0  
            -- @TranCounter = 0 means no transaction was  
            -- started before the procedure was called.  
            -- The procedure must commit the transaction  
            -- it started.  
            COMMIT TRANSACTION;  
    END TRY  
    BEGIN CATCH  
        -- An error occurred; must determine  
        -- which type of rollback will roll  
        -- back only the work done in the  
        -- procedure.  
        IF @TranCounter = 0  
            -- Transaction started in procedure.  
            -- Roll back complete transaction.  
            ROLLBACK TRANSACTION;  
        ELSE  
            -- Transaction started before procedure  
            -- called, do not roll back modifications  
            -- made before the procedure was called.  
            IF XACT_STATE() <> -1  
                -- If the transaction is still valid, just  
                -- roll back to the savepoint set at the  
                -- start of the stored procedure.  
                ROLLBACK TRANSACTION ProcedureSave;  
                -- If the transaction is uncommitable, a  
                -- rollback to the savepoint is not allowed  
                -- because the savepoint rollback writes to  
                -- the log. Just return to the caller, which  
                -- should roll back the outer transaction.  
  
        -- After the appropriate rollback, echo error  
        -- information to the caller.  
        DECLARE @ErrorMessage NVARCHAR(4000);  
        DECLARE @ErrorSeverity INT;  
        DECLARE @ErrorState INT;  
  
        SELECT @ErrorMessage = ERROR_MESSAGE();  
        SELECT @ErrorSeverity = ERROR_SEVERITY();  
        SELECT @ErrorState = ERROR_STATE();  
  
        RAISERROR (@ErrorMessage, -- Message text.  
                   @ErrorSeverity, -- Severity.  
                   @ErrorState -- State.  
                   );  
    END CATCH  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [커밋 작업 &#40; Transact SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ERROR_LINE&#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [Error_state &#40; Transact SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [ROLLBACK TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40; Transact SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [XACT_STATE &#40; Transact SQL &#41;](../../t-sql/functions/xact-state-transact-sql.md)  
  
  
