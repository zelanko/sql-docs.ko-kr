---
title: XACT_STATE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- XACT_STATE
- XACT_STATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- states [SQL Server], transactions
- uncommittable transactions
- sessions [SQL Server], active transactions
- XACT_STATE function
- transactions [SQL Server], state
- active transactions
ms.assetid: e9300827-e793-4eb6-9042-ffa0204aeb50
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d5760cf8b2da0abea5505245681ae5164cbc9aca
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="xactstate-transact-sql"></a>XACT_STATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 실행 중인 요청의 사용자 트랜잭션 상태를 보고하는 스칼라 함수입니다. XACT_STATE는 요청에 활성 사용자 트랜잭션이 있는지 여부 및 트랜잭션이 커밋될 수 있는지 여부를 나타냅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
XACT_STATE()  
```  
  
## <a name="return-type"></a>반환 형식  
 **smallint**  
  
## <a name="remarks"></a>주의  
 XACT_STATE는 다음 값을 반환합니다.  
  
|반환 값|의미|  
|------------------|-------------|  
|1.|현재 요청에 활성 사용자 트랜잭션이 있습니다. 해당 요청에서는 데이터를 쓰고 트랜잭션을 커밋하는 등 모든 동작을 수행할 수 있습니다.|  
|0|현재 요청에 대한 활성 사용자 트랜잭션이 없습니다.|  
|-1|현재 요청에 활성 사용자 트랜잭션이 있지만 오류가 발생하여 트랜잭션이 커밋할 수 없는 트랜잭션으로 분류된 상태입니다. 해당 요청에서는 트랜잭션을 커밋하거나 저장점까지 롤백할 수 없고 트랜잭션의 전체 롤백만 요청할 수 있습니다. 요청에서 트랜잭션을 롤백할 때까지 모든 쓰기 작업을 수행할 수 없습니다. 트랜잭션을 롤백할 때까지 읽기 작업만 수행할 수 있습니다. 트랜잭션이 롤백된 후에는 요청에서 읽기/쓰기 작업을 모두 수행할 수 있으며 새 트랜잭션을 시작할 수 있습니다.<br /><br /> 일괄 처리가 완료되면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 자동으로 커밋할 수 없는 활성 트랜잭션을 모두 롤백합니다. 트랜잭션이 커밋할 수 없는 상태가 되었을 때 오류 메시지가 전송되지 않은 경우 일괄 처리가 완료되면 오류 메시지가 클라이언트 응용 프로그램으로 전송됩니다. 이 메시지는 커밋할 수 없는 트랜잭션이 검색되어 롤백되었음을 보여 줍니다.|  
  
 둘 다에서 XACT_STATE와 @@TRANCOUNT 현재 요청에 활성 사용자 트랜잭션이 있는지 여부를 검색 하는 함수를 사용할 수 있습니다. @@TRANCOUNT 해당 트랜잭션이 커밋 불가능 트랜잭션으로 분류 되었습니다 있는지 여부를 확인 하기 위해 사용할 수 없습니다. 또한 XACT_STATE를 사용하여 중첩된 트랜잭션이 있는지 여부를 확인할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `XACT_STATE` 구문의 `CATCH` 블록에서 `TRY…CATCH`를 사용하여 트랜잭션을 커밋 또는 롤백하는지를 확인합니다. `SET XACT_ABORT`가 `ON`으로 설정되어 있으므로 제약 조건 위반 오류가 발생하면 트랜잭션은 커밋할 수 없는 상태가 됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
-- SET XACT_ABORT ON will render the transaction uncommittable  
-- when the constraint violation occurs.  
SET XACT_ABORT ON;  
  
BEGIN TRY  
    BEGIN TRANSACTION;  
        -- A FOREIGN KEY constraint exists on this table. This   
        -- statement will generate a constraint violation error.  
        DELETE FROM Production.Product  
            WHERE ProductID = 980;  
  
    -- If the delete operation succeeds, commit the transaction. The CATCH  
    -- block will not execute.  
    COMMIT TRANSACTION;  
END TRY  
BEGIN CATCH  
    -- Test XACT_STATE for 0, 1, or -1.  
    -- If 1, the transaction is committable.  
    -- If -1, the transaction is uncommittable and should   
    --     be rolled back.  
    -- XACT_STATE = 0 means there is no transaction and  
    --     a commit or rollback operation would generate an error.  
  
    -- Test whether the transaction is uncommittable.  
    IF (XACT_STATE()) = -1  
    BEGIN  
        PRINT 'The transaction is in an uncommittable state.' +  
              ' Rolling back transaction.'  
        ROLLBACK TRANSACTION;  
    END;  
  
    -- Test whether the transaction is active and valid.  
    IF (XACT_STATE()) = 1  
    BEGIN  
        PRINT 'The transaction is committable.' +   
              ' Committing transaction.'  
        COMMIT TRANSACTION;     
    END;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [@@TRANCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)   
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SAVE TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  
