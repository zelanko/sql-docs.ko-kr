---
title: ERROR_STATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ERROR_STATE_TSQL
- ERROR_STATE
dev_langs:
- TSQL
helpviewer_keywords:
- messages [SQL Server], state
- ERROR_STATE function
- errors [SQL Server], state
- TRY...CATCH [SQL Server]
- CATCH block
- states [SQL Server], error numbers
ms.assetid: 6059af00-83fe-409f-ab7c-daad111bc671
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5ec35734716a2808e3b8450588498caf8a610e8d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="errorstate-transact-sql"></a>ERROR_STATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  TRY...CATCH 구문의 CATCH 블록을 실행시킨 오류의 상태 번호를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ERROR_STATE ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="return-value"></a>반환 값  
 CATCH 블록 내에서 호출된 경우 CATCH 블록을 실행하도록 만든 오류 메시지의 상태 번호를 반환합니다.  
  
 CATCH 블록 범위 밖에서 호출된 경우 NULL을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 일부 오류 메시지는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]코드의 여러 곳에서 발생할 수 있습니다. 예를 들어 "1105" 오류는 여러 가지 다른 오류 상황에서 발생합니다. 오류를 발생시키는 특정 조건은 각각 고유한 상태 코드를 할당합니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 기술 자료 등을 사용하여 데이터베이스의 알려진 문제를 확인하는 경우 상태 번호를 사용하여 기록된 문제가 실제로 발생한 오류와 동일한 것인지 판단할 수 있습니다. 예를 들어 기술 자료 문서에서 상태가 2인 1105 오류 메시지를 다루고 있고 실제로 수신한 1105 오류 메시지의 상태가 3인 경우 이 오류는 기술 자료 문서에 보고된 것과 다른 원인에서 비롯되었을 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원 엔지니어는 상태 코드를 사용하여 원본 코드에서 해당 오류가 발생한 위치를 찾고 문제를 해결할 수 있습니다.  
  
 ERROR_STATE는 CATCH 블록 범위 내의 어떤 위치에서나 호출할 수 있습니다.  
  
 ERROR_STATE는 실행 횟수 또는 CATCH 블록의 범위 내의 실행되는 위치에 상관없이 오류 상태를 반환합니다. 이 함수는 오류를 발생시킨 명령문 바로 다음 명령문에서 오류 번호만 반환하거나 CATCH 블록의 첫 번째 명령문에서 발생한 오류 번호만 반환하는 @@ERROR과 같은 함수와는 대조적입니다.  
  
 중첩된 CATCH 블록 내의 ERROR_STATE는 참조되는 CATCH 블록의 범위에 한정된 오류 상태를 반환합니다. 예를 들어 외부 TRY...CATCH 구문의 CATCH 블록에는 중첩된 TRY...CATCH 구문이 있을 수 있습니다. 중첩된 CATCH 블록 내의 ERROR_STATE는 중첩된 CATCH 블록을 호출한 오류에서 상태를 반환합니다. ERROR_STATE가 외부 CATCH 블록에서 실행되는 경우 해당 CATCH 블록을 호출한 오류에서 상태를 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-errorstate-in-a-catch-block"></a>1. CATCH 블록에서 ERROR_STATE 사용  
 다음 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. 오류의 상태가 반환됩니다.  
  
```  
BEGIN TRY  
    -- Generate a divide by zero error  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_STATE() AS ErrorState;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorstate-in-a-catch-block-with-other-error-handling-tools"></a>2. 다른 오류 처리 도구와 함께 CATCH 블록에서 ERROR_STATE 사용  
 다음 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. 오류 상태와 함께 오류와 관련된 정보가 반환됩니다.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_LINE() AS ErrorLine,  
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errorstate-in-a-catch-block-with-other-error-handling-tools"></a>3. 다른 오류 처리 도구와 함께 CATCH 블록에서 ERROR_STATE 사용  
 다음 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. 오류 상태와 함께 오류와 관련된 정보가 반환됩니다.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
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
  
## <a name="see-also"></a>참고 항목  
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE&#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  

