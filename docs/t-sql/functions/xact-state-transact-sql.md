---
title: XACT_STATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dc7a0495a9289d538e71397e96b9393e91c542e0
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87112580"
---
# <a name="xact_state-transact-sql"></a>XACT_STATE(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 실행 중인 요청의 사용자 트랜잭션 상태를 보고하는 스칼라 함수입니다. XACT_STATE는 요청에 활성 사용자 트랜잭션이 있는지 여부 및 트랜잭션이 커밋될 수 있는지 여부를 나타냅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
XACT_STATE()  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-type"></a>반환 형식  
 **smallint**  
  
## <a name="remarks"></a>설명  
 XACT_STATE는 다음 값을 반환합니다.  
  
|반환 값|의미|  
|------------------|-------------|  
|1|현재 요청에 활성 사용자 트랜잭션이 있습니다. 해당 요청에서는 데이터를 쓰고 트랜잭션을 커밋하는 등 모든 동작을 수행할 수 있습니다.|  
|0|현재 요청에 대한 활성 사용자 트랜잭션이 없습니다.|  
|-1|현재 요청에 활성 사용자 트랜잭션이 있지만 오류가 발생하여 트랜잭션이 커밋할 수 없는 트랜잭션으로 분류된 상태입니다. 해당 요청에서는 트랜잭션을 커밋하거나 저장점까지 롤백할 수 없고 트랜잭션의 전체 롤백만 요청할 수 있습니다. 요청에서 트랜잭션을 롤백할 때까지 모든 쓰기 작업을 수행할 수 없습니다. 트랜잭션을 롤백할 때까지 읽기 작업만 수행할 수 있습니다. 트랜잭션이 롤백된 후에는 요청에서 읽기/쓰기 작업을 모두 수행할 수 있으며 새 트랜잭션을 시작할 수 있습니다.<br /><br /> 가장 바깥쪽 일괄 처리가 완료되면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 자동으로 커밋할 수 없는 활성 트랜잭션을 모두 롤백합니다. 트랜잭션이 커밋할 수 없는 상태가 되었을 때 오류 메시지가 전송되지 않은 경우 일괄 처리가 완료되면 오류 메시지가 클라이언트 애플리케이션으로 전송됩니다. 이 메시지는 커밋할 수 없는 트랜잭션이 검색되어 롤백되었음을 보여 줍니다.|  
  
 XACT_STATE와 @@TRANCOUNT 함수는 모두 현재 요청에 활성 사용자 트랜잭션이 있는지 여부를 검색하는 데 사용될 수 있습니다. @@TRANCOUNT을 사용하여 트랜잭션이 커밋되지 않은 트랜잭션으로 분류되었는지 여부를 확인할 수는 없습니다. 또한 XACT_STATE를 사용하여 중첩된 트랜잭션이 있는지 여부를 확인할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `XACT_STATE` 구문의 `CATCH` 블록에서 `TRY...CATCH`를 사용하여 트랜잭션을 커밋 또는 롤백하는지를 확인합니다. `SET XACT_ABORT`가 `ON`으로 설정되어 있으므로 제약 조건 위반 오류가 발생하면 트랜잭션은 커밋할 수 없는 상태가 됩니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [@@TRANCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)   
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TransactION&#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SAVE TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  
