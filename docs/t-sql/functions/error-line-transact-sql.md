---
title: ERROR_LINE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fe54b0a56e90dd7c4645fd0e78db7e97f6c838f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770981"
---
# <a name="errorline-transact-sql"></a>ERROR_LINE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 TRY...CATCH 구문의 CATCH 블록을 실행시키는 오류의 발생 줄 번호를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ERROR_LINE ( )  
```  
  
## <a name="return-type"></a>반환 형식  
**int**  
  
## <a name="return-value"></a>반환 값  
CATCH 블록에서 호출된 경우 `ERROR_LINE`은 다음을 반환합니다.  
  
-   오류가 발생한 줄 번호입니다.    
-   오류가 저장 프로시저 또는 트리거 내에서 발생한 경우 루틴의 줄 번호  
-   CATCH 블록 범위 밖에서 호출된 경우 NULL입니다.  
  
## <a name="remarks"></a>Remarks  
`ERROR_LINE`에 대한 호출은 CATCH 블록 범위 내의 어디에서나 발생할 수 있습니다.  
  
`ERROR_LINE`은 오류가 발생한 줄 번호를 반환합니다. 이는 CATCH 블록의 범위 내에서 위치와 `ERROR_LINE` 호출의 위치 및 `ERROR_LINE`에 대한 호출 수에 관계 없이 발생합니다. 이는 @ERROR 같은 함수와 대조적입니다. @@ERROR는 오류가 발생한 명령문 바로 다음 명령문 또는 CATCH 블록의 첫 번째 명령문에 오류 번호를 반환합니다.  
  
중첩된 CATCH 블록에서 `ERROR_LINE`은 참조되는 CATCH 블록의 범위에 해당하는 오류 줄 번호를 반환합니다. 예를 들어 TRY...CATCH 구조의 CATCH 블록에는 중첩된 TRY...CATCH 구문이 포함될 수 있습니다. 중첩된 CATCH 블록 내에서 `ERROR_LINE`은 중첩된 CATCH 블록을 호출한 오류의 줄 번호를 반환합니다. `ERROR_LINE`이 외부 CATCH 블록에서 실행되는 경우 해당 특정 CATCH 블록을 호출한 오류의 줄 번호를 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-errorline-in-a-catch-block"></a>1. CATCH 블록에서 ERROR_LINE 사용  
이 코드 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. `ERROR_LINE`은 오류가 발생한 줄 번호를 반환합니다.  
  
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
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
```  
Result 
-----------

(0 row(s) affected)

ErrorLine
-----------
4

(1 row(s) affected)
```  
  
### <a name="b-using-errorline-in-a-catch-block-with-a-stored-procedure"></a>2. 저장 프로시저의 오류 줄 번호 반환을 위해 CATCH 블록에서 ERROR_LINE 사용  
이 예에서는 0으로 나누기 오류를 생성하는 저장 프로시저를 보여 줍니다. `ERROR_LINE`은 오류가 발생한 줄 번호를 반환합니다.  
  
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
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
```  
-----------

(0 row(s) affected)

ErrorLine
-----------
7

(1 row(s) affected)  
   
```

### <a name="c-using-errorline-in-a-catch-block-with-other-error-handling-tools"></a>3. CATCH 블록에서 다른 오류 처리 도구와 함께 ERROR_LINE 사용  
이 코드 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. `ERROR_LINE`은 오류가 발생한 줄 번호 및 오류 자체와 관련된 정보를 반환합니다.  
  
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
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
```  
-----------

(0 row(s) affected)

ErrorNumber ErrorSeverity ErrorState ErrorProcedure ErrorLine ErrorMessage
----------- ------------- ---------- -------------- --------- ---------------------------------
8134        16            1          NULL           3         Divide by zero error encountered.

(1 row(s) affected)
  
```
  
## <a name="see-also"></a>참고 항목  
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
