---
title: THROW (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- THROW_TSQL
- THROW
dev_langs: TSQL
helpviewer_keywords: THROW statement
ms.assetid: 43661b89-8f13-4480-ad53-70306cbb14c5
caps.latest.revision: "24"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: bed4670dc0d683eea4920ddd39aec781177f7cc5
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="throw-transact-sql"></a>THROW(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 예외를 발생시키고 TRY…CATCH 구문의 CATCH 블록으로 실행을 이전합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
THROW [ { error_number | @local_variable },  
        { message | @local_variable },  
        { state | @local_variable } ]   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *error_number*  
 예외를 나타내는 상수 또는 변수입니다. *error_number* 은 **int** 50000 보다 크거나 여야 하 고 및 2147483647입니다.  
  
 *message*  
 예외를 설명하는 문자열 또는 변수입니다. *메시지* 은 **nvarchar (2048)**합니다.  
  
 *state*  
 메시지와 연결할 상태를 나타내는 0에서 255 사이의 상수 또는 변수입니다. *상태* 은 **tinyint**합니다.  
  
## <a name="remarks"></a>주의  
 THROW 문 앞의 문 다음에는 세미콜론(;) 문 종결자를 붙여야 합니다.  
  
 TRY…CATCH 구문을 사용할 수 없으면 세션이 종료됩니다. 예외가 발생한 줄 번호와 프로시저가 설정됩니다. 심각도는 16으로 설정됩니다.  
  
 매개 변수 없이 지정된 THROW 문은 CATCH 블록 안에 나타나야 합니다. 이렇게 하면 예외가 발생합니다. THROW 문에 발생하는 오류로 인해 문 일괄 처리가 종료됩니다.  
  
 %는 THROW 문의 메시지 텍스트에 예약된 문자이므로 이스케이프되어야 합니다. %를 메시지 텍스트의 일부로 반환하려면 % 문자를 두 개 사용하세요(예: '증가가 원래 값의 15%%를 초과했습니다.').  
  
## <a name="differences-between-raiserror-and-throw"></a>RAISERROR와 THROW의 차이점  
 다음 표에서는 RAISERROR 문과 THROW 문의 차이점을 보여 줍니다.  
  
|RAISERROR 문|THROW 문|  
|-------------------------|---------------------|  
|경우는 *msg_id* 전달 RAISERROR에 ID sys.messages에 정의 해야 합니다.|*error_number* 매개 변수가 있어서는 안 sys.messages에 정의 되어야 합니다.|  
|*msg_str* 매개 변수에 **printf** 서식 스타일입니다.|*메시지* 매개 변수를 받아들이지 않는 **printf** 스타일의 서식 지정 합니다.|  
|*심각도* 매개 변수는 예외의 심각도 지정 합니다.|없는 *심각도* 매개 변수입니다. 예외 심각도는 항상 16으로 설정됩니다.|  
  
## <a name="examples"></a>예  
  
### <a name="a-using-throw-to-raise-an-exception"></a>1. THROW를 사용하여 예외 발생  
 다음 예에서는 `THROW` 문을 사용하여 예외를 발생시키는 방법을 보여 줍니다.  
  
```sql  
THROW 51000, 'The record does not exist.', 1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Msg 51000, Level 16, State 1, Line 1  
  
 The record does not exist.
 ```  
  
### <a name="b-using-throw-to-raise-an-exception-again"></a>2. THROW를 사용하여 다시 예외 발생  
 다음 예에서는 `THROW` 문을 사용하여 발생한 예외를 다시 발생시키는 방법을 보여 줍니다.  
  
```sql  
USE tempdb;  
GO  
CREATE TABLE dbo.TestRethrow  
(    ID INT PRIMARY KEY  
);  
BEGIN TRY  
    INSERT dbo.TestRethrow(ID) VALUES(1);  
--  Force error 2627, Violation of PRIMARY KEY constraint to be raised.  
    INSERT dbo.TestRethrow(ID) VALUES(1);  
END TRY  
BEGIN CATCH  
  
    PRINT 'In catch block.';  
    THROW;  
END CATCH;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 PRINT 'In catch block.';  
 Msg 2627, Level 14, State 1, Line 1  
 Violation of PRIMARY KEY constraint 'PK__TestReth__3214EC272E3BD7D3'. Cannot insert duplicate key in object 'dbo.TestRethrow'.  
 The statement has been terminated.
 ```  
  
### <a name="c-using-formatmessage-with-throw"></a>3. THROW에 FORMATMESSAGE 사용  
 다음 예에서는 `FORMATMESSAGE` 함수를 `THROW`와 함께 사용하여 사용자 지정된 오류 메시지를 발생시키는 방법을 보여 줍니다. 이 예제에서는 먼저 `sp_addmessage`를 사용하여 사용자 정의 오류 메시지를 만듭니다. THROW 문은 대체 매개 변수에서 허용 하지 않으므로 *메시지* 오류 메시지 60000에 필요한 세 가지 매개 변수 값을 전달 하는 방식 RAISERROR는 FORMATMESSAGE 함수 매개 변수를 사용 합니다.  
  
```sql  
EXEC sys.sp_addmessage  
     @msgnum   = 60000  
,@severity = 16  
,@msgtext  = N'This is a test message with one numeric parameter (%d), one string parameter (%s), and another string parameter (%s).'  
    ,@lang = 'us_english';   
GO  
  
DECLARE @msg NVARCHAR(2048) = FORMATMESSAGE(60000, 500, N'First string', N'second string');   
  
THROW 60000, @msg, 1;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Msg 60000, Level 16, State 1, Line 2  
 This is a test message with one numeric parameter (500), one string parameter (First string), and another string parameter (second string).
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [FORMATMESSAGE &#40; Transact SQL &#41;](../../t-sql/functions/formatmessage-transact-sql.md)   
 [데이터베이스 엔진 오류 심각도](../../relational-databases/errors-events/database-engine-error-severities.md)   
 [ERROR_LINE&#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [Error_state &#40; Transact SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)   
 [GOTO &#40; Transact SQL &#41;](../../t-sql/language-elements/goto-transact-sql.md)   
 [시작 중... 최종 &#40; Transact SQL &#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [XACT_STATE &#40; Transact SQL &#41;](../../t-sql/functions/xact-state-transact-sql.md)   
 [SET XACT_ABORT &#40; Transact SQL &#41;](../../t-sql/statements/set-xact-abort-transact-sql.md)  
  
  

