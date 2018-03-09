---
title: ERROR_LINE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ERROR_LINE
- ERROR_LINE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], line number
- messages [SQL Server], line number
- TRY...CATCH [SQL Server]
- line number of error [SQL Server]
- ERROR_LINE function
- CATCH block
ms.assetid: 47335734-0baf-45a6-8b3b-6c4fd80d2cb8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 83783fdaa950777ae0a8002182abc273e32c2ca0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="errorline-transact-sql"></a>ERROR_LINE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  TRY...CATCH 구문의 CATCH 블록 실행을 유발한 오류가 발생한 줄 번호를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ERROR_LINE ( )  
```  
  
## <a name="return-type"></a>반환 형식  
 **int**  
  
## <a name="return-value"></a>반환 값  
 CATCH 블록에서 호출된 경우 다음을 반환합니다.  
  
-   오류가 발생한 줄 번호를 반환합니다.  
  
-   오류가 저장 프로시저 또는 트리거에서 발생한 경우 루틴 내의 줄 번호를 반환합니다.  
  
 CATCH 블록 범위 밖에서 호출된 경우 NULL을 반환합니다.  
  
## <a name="remarks"></a>주의  
 이 함수는 CATCH 블록 내의 어떤 위치에서도 호출할 수 있습니다.  
  
 ERROR_LINE은 호출 횟수 또는 CATCH 블록 내에서 호출된 위치에 관계 없이 오류가 발생한 줄 번호를 반환합니다. 이와 달리, 함수 등@ERROR를 바로 다음에 오류를 발생 시키는 문 또는 CATCH 블록의 첫 번째 문에서 오류 번호를 반환 하 합니다.  
  
 CATCH 블록이 중첩된 경우 ERROR_LINE은 참조되는 CATCH 블록의 범위에 해당하는 오류 줄 번호를 반환합니다. 예를 들어 TRY...CATCH 구조의 CATCH 블록에는 중첩된 TRY...CATCH 구문이 포함될 수 있습니다. 중첩된 CATCH 블록 내에 있는 ERROR_LINE은 중첩된 CATCH 블록을 호출한 오류의 줄 번호를 반환합니다. 외부 CATCH 블록에서 ERROR_LINE을 실행하면 해당 CATCH 블록을 호출한 오류의 줄 번호를 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-errorline-in-a-catch-block"></a>1. CATCH 블록에서 ERROR_LINE 사용  
 다음 코드 예에서는 0으로 나누기 오류를 생성하는 `SELECT` 문을 보여 줍니다. 오류가 발생한 줄 번호가 반환됩니다.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorline-in-a-catch-block-with-a-stored-procedure"></a>2. 저장 프로시저의 오류 줄 번호 반환을 위해 CATCH 블록에서 ERROR_LINE 사용  
 다음 코드 예에서는 0으로 나누기 오류를 생성하는 저장 프로시저를 보여 줍니다. `ERROR_LINE`은 오류가 발생한 저장 프로시저의 줄 번호를 반환합니다.  
  
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
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
```  
  
### <a name="c-using-errorline-in-a-catch-block-with-other-error-handling-tools"></a>3. CATCH 블록에서 다른 오류 처리 도구와 함께 ERROR_LINE 사용  
 다음 코드 예에서는 0으로 나누기 오류를 생성하는 `SELECT` 문을 보여 줍니다. 오류가 발생한 줄 번호와 함께 오류에 관련된 정보가 반환됩니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [Error_state &#40; Transact SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
