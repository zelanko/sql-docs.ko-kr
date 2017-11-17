---
title: ERROR_SEVERITY (Transact SQL) | Microsoft Docs
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
- ERROR_SEVERITY_TSQL
- ERROR_SEVERITY
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], severity
- messages [SQL Server], severity
- TRY...CATCH [SQL Server]
- CATCH block
- ERROR_SEVERITY function
ms.assetid: 50228f2f-6949-4d2e-8e43-fad11bf973ab
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 5c3cd713bcbb239c037ff0a43083058de117cb9b
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="errorseverity-transact-sql"></a>ERROR_SEVERITY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  TRY...CATCH 구문의 CATCH 블록이 실행되도록 한 오류의 심각도를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ERROR_SEVERITY ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="return-value"></a>반환 값  
 CATCH 블록에서 호출되는 경우 CATCH 블록이 실행되도록 한 오류 메시지의 심각도를 반환합니다.  
  
 CATCH 블록 범위 밖에서 호출된 경우 NULL을 반환합니다.  
  
## <a name="remarks"></a>주의  
 ERROR_SEVERITY는 CATCH 블록 범위 내의 아무 위치에서나 호출할 수 있습니다.  
  
 ERROR_SEVERITY는 실행 횟수 또는 CATCH 블록 범위 내의 실행 위치에 관계 없이 오류 심각도를 반환합니다. 이 같은 함수와 대조 @@ERROR만 반환 하는 오류 번호 또는 CATCH 블록의 첫 번째 문에서 오류를 발생 시킨 바로 다음 문으로에서 합니다.  
  
 CATCH 블록이 중첩된 경우 ERROR_SEVERITY는 참조되는 CATCH 블록의 범위에 해당되는 오류 심각도를 반환합니다. 예를 들어 외부 TRY...CATCH 구문의 CATCH 블록에는 중첩된 TRY...CATCH 구문이 있을 수 있습니다. 중첩된 CATCH 블록 내에 있는 ERROR_LINE은 중첩된 CATCH 블록을 호출한 오류의 심각도를 반환합니다. 외부 CATCH 블록에서 ERROR_SEVERITY를 실행하면 해당 CATCH 블록을 호출한 오류의 심각도를 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-errorseverity-in-a-catch-block"></a>1. CATCH 블록에서 ERROR_SEVERITY 사용  
 다음 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. 오류의 심각도가 반환됩니다.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_SEVERITY() AS ErrorSeverity;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorseverity-in-a-catch-block-with-other-error-handling-tools"></a>2. CATCH 블록에서 다른 오류 처리 도구와 함께 ERROR_SEVERITY 사용  
 다음 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. 심각도와 함께 오류와 관련된 정보가 반환됩니다.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errorseverity-in-a-catch-block-with-other-error-handling-tools"></a>3. CATCH 블록에서 다른 오류 처리 도구와 함께 ERROR_SEVERITY 사용  
 다음 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. 심각도와 함께 오류와 관련된 정보가 반환됩니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE&#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [Error_state&#40; Transact SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  


