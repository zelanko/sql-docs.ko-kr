---
description: RAISERROR(Transact-SQL)
title: RAISERROR(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RAISERROR
- RAISERROR_TSQL
- RAISEERROR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmessages system table
- errors [SQL Server], RAISERROR statement
- user-defined error messages [SQL Server]
- system flags
- generating errors [SQL Server]
- TRY block [SQL Server]
- recording errors
- ad hoc messages
- RAISERROR statement
- CATCH block
- messages [SQL Server], RAISERROR statement
ms.assetid: 483588bd-021b-4eae-b4ee-216268003e79
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efe7c892d5fbf369f0bf7f4bd9e63ffa5de16faa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445497"
---
# <a name="raiserror-transact-sql"></a>RAISERROR(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

> [!NOTE]
> **RAISERROR** 문은 **SET XACT_ABORT**를 적용하지 않습니다. 새 애플리케이션에서는 **RAISERROR** 대신 **THROW**를 사용해야 합니다.

  오류 메시지를 생성하고 세션에 대한 오류 처리를 시작합니다. RAISERROR는 sys.messages 카탈로그 뷰에 저장된 사용자 정의 메시지를 참조하거나 동적으로 메시지를 작성할 수 있습니다. 메시지는 호출하는 애플리케이션 또는 연결된 TRY...CATCH 구문의 CATCH 블록에 서버 오류 메시지로 반환됩니다. 새 애플리케이션에서는 [THROW](../../t-sql/language-elements/throw-transact-sql.md)를 대신 사용해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
RAISERROR ( { msg_id | msg_str | @local_variable }  
    { ,severity ,state }  
    [ ,argument [ ,...n ] ] )  
    [ WITH option [ ,...n ] ]  
```  
  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
RAISERROR ( { msg_str | @local_variable }  
    { ,severity ,state }  
    [ ,argument [ ,...n ] ] )  
    [ WITH option [ ,...n ] ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *msg_id*  
 sp_addmessage를 사용하여 sys.messages 카탈로그 뷰에 저장된 사용자 정의 오류 메시지 번호입니다. 사용자 정의 오류 메시지의 오류 번호는 50000보다 커야 합니다. *msg_id*를 지정하지 않으면 RAISERROR는 오류 번호가 50000인 오류 메시지를 발생시킵니다.  
  
 *msg_str*  
 C 표준 라이브러리의 **printf** 함수와 유사한 형식을 가진 사용자 정의 메시지입니다. 오류 메시지는 최대 2,047자까지 지정할 수 있습니다. 메시지의 문자가 2,048자 이상이면 처음 2,044자만 표시되고 메시지가 잘렸음을 나타내기 위해 줄임표가 추가됩니다. 내부 스토리지 방식의 특성상 대체 매개 변수는 출력에 표시되는 것보다 더 많은 수의 문자를 사용합니다. 예를 들어 값 2가 할당된 대체 매개 변수 *%d*는 메시지 문자열에서 실제로 1개의 문자로 생성되지만 내부적으로는 스토리지에서 3개의 추가 문자를 사용합니다. 이러한 스토리지 요구 사항 때문에 메시지 출력에 사용 가능한 문자 수가 감소됩니다.  
  
 *msg_str*를 지정하면 RAISERROR는 오류 번호가 50000인 오류 메시지를 발생시킵니다.  
  
 *msg_str*는 선택적으로 포함된 변환 사양을 가진 문자열입니다. 각각의 변환 사양은 인수 목록의 값이 *msg_str*의 각 변환 사양 위치에 어떤 형식으로 어떻게 배치되는지 정의합니다. 변환 사양의 형식은 다음과 같습니다.  
  
 % [[*flag*] [*width*] [. *precision*] [{h | l}]] *type*  
  
 *msg_str*에서 사용할 수 있는 매개 변수는 다음과 같습니다.  
  
 *flag*  
  
 대체 값의 공백 처리 및 맞춤을 결정하는 코드입니다.  
  
|코드|접두사 또는 맞춤|Description|  
|----------|-----------------------------|-----------------|  
|-(빼기)|왼쪽 정렬|지정한 필드 너비 내에서 인수 값을 왼쪽으로 정렬합니다.|  
|+(더하기)|부호 접두사|값이 부호가 있는 형식일 경우 더하기(+)나 빼기(-) 부호를 인수 값 앞에 붙입니다.|  
|0(영)|0 패딩|최소 너비에 도달할 때까지 출력 앞에 0을 붙입니다. 0과 빼기(-) 부호가 있으면 0은 무시합니다.|  
|#(숫자)|x 또는 X의 16진수 유형에 대한 0x 접두사|o, x 또는 X 형식의 값에 사용할 경우 숫자 기호(#)는 0이 아닌 모든 값 앞에 0, 0x 또는 0X를 각각 붙입니다. d, i 또는 u 앞에 숫자 기호(#) 플래그가 있으면 플래그는 무시됩니다.|  
|' '(공백)|공간 채움|부호 있는 양수일 경우 출력 값 앞에 공백을 붙입니다. 더하기 부호(+) 플래그가 포함된 경우에는 무시됩니다.|  
  
 *width*  
  
 인수 값이 배치될 필드의 최소 너비를 정의하는 정수입니다. 인수 값의 길이가 *width*와 같거나 길면 값은 패딩 없이 출력됩니다. 값이 *width*보다 짧으면 값은 *width*에 지정된 길이로 패딩됩니다.  
  
 별표(*)는 너비가 인수 목록의 관련 인수에 의해 지정되며 정수 값이어야 함을 의미합니다.  
  
 *전체 자릿수*  
  
 문자열 값의 경우 인수 값에서 가져온 문자의 최대 개수입니다. 예를 들어 문자열에 5개의 문자가 있고 precision이 3이면 문자열 값의 처음 3개 문자만 사용됩니다.  
  
 정수 값의 경우 *precision*은 출력되는 최소 자릿수입니다.  
  
 별표(*)는 전체 자릿수가 인수 목록의 관련 인수에 의해 지정되며 정수 값이어야 함을 의미합니다.  
  
 {h | l} *type*  
  
 i, o, s, x, X 또는 u 문자 유형에 사용되며 **shortint**(h) 또는 **longint**(l) 값을 만듭니다.  
  
|형식 사양|나타내는 대상|  
|------------------------|----------------|  
|d 또는 I|부호 있는 정수|  
|o|부호 없는 8진수|  
|s|String|  
|u|부호 없는 정수|  
|x 또는 X|부호 없는 16진수|  
  
> [!NOTE]  
>  이 형식 사양들은 원래 C 표준 라이브러리의 **printf** 함수용으로 정의된 것들을 기반으로 합니다. RAISERROR 메시지 문자열에 사용된 형식 사양들은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터 형식으로 매핑되고 **printf**에서 사용된 사양들은 C 언어 데이터 형식에 매핑됩니다. **printf**에 사용된 형식 사양들은 [!INCLUDE[tsql](../../includes/tsql-md.md)]에 관련 C 데이터 형식과 유사한 데이터 형식이 없을 경우 RAISERROR에서 지원되지 않습니다. 예를 들어 포인터용 *%p* 사양은 [!INCLUDE[tsql](../../includes/tsql-md.md)]에 포인터 데이터 형식이 없기 때문에 RAISERROR에서 지원되지 않습니다.  
  
> [!NOTE]  
>  값을 [!INCLUDE[tsql](../../includes/tsql-md.md)] **bigint** 데이터 형식으로 변환하려면 **%I64d**를 지정합니다.  
  
 *\@local_variable*  
 *msg_str*와 동일한 방식으로 형식이 지정된 문자열을 포함하는 유효한 문자 데이터 형식의 변수입니다. *\@local_variable*은 **char** 또는 **varchar**이거나 암시적으로 이러한 데이터 형식으로 변환될 수 있어야 합니다.  
  
 *severity*  
 이 메시지에 연결된 사용자 정의 심각도입니다. sp_addmessage를 사용해 만든 사용자 정의 메시지를 발생시키기 위해 *msg_id*를 사용할 경우 RAISERROR에 지정된 심각도가 sp_addmessage에 지정된 심각도보다 우선합니다.  
  
 모든 사용자가 0부터 18까지의 심각도를 지정할 수 있습니다. 19부터 25까지의 심각도는 sysadmin 고정 서버 역할의 멤버 또는 ALTER TRACE 권한을 가진 사용자만이 지정할 수 있습니다. 19부터 25까지의 심각도에 대해서는 WITH LOG 옵션이 필요합니다. 0보다 작은 심각도 수준은 0으로 해석되고 25보다 작은 심각도 수준은 25로 해석됩니다.  
  
> [!CAUTION]  
>  20부터 25까지의 심각도는 치명적인 심각도입니다. 치명적인 심각도가 발생하면 메시지를 받은 다음 클라이언트 연결이 종료되고 오류 및 애플리케이션 로그에 오류가 기록됩니다.  
  
 다음 예와 같이 -1을 지정하여 오류와 연결된 심각도 값을 반환할 수 있습니다.  
  
```  
RAISERROR (15600,-1,-1, 'mysp_CreateCustomer');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Msg 15600, Level 15, State 1, Line 1   
 An invalid parameter or option was specified for procedure 'mysp_CreateCustomer'.
 ```  
  
 *상태*  
 0에서 255 사이의 정수입니다. 음수 값은 기본적으로 1입니다. 255보다 큰 값은 사용해서는 안 됩니다. 
  
 여러 위치에서 동일한 사용자 정의 오류가 발생하는 경우 각 위치의 고유 상태 번호를 사용하면 코드의 어떤 부분에서 오류가 발생하는지 찾는 데 도움이 됩니다.  
  
 *argument*  
 *msg_str*에서 정의된 변수의 대체에 사용되는 매개 변수 또는 *msg_id*에 해당하는 메시지입니다. 0개 이상의 대체 매개 변수가 있을 수 있지만 대체 매개 변수의 총 개수가 20을 초과할 수는 없습니다. 각 대체 매개 변수는 지역 변수이거나 **tinyint**, **smallint**, **int**, **char**, **varchar**, **nchar**, **nvarchar**, **binary** 또는 **varbinary**의 데이터 형식 중 하나일 수 있습니다. 다른 데이터 형식은 지원되지 않습니다.  
  
 *옵션*  
 오류에 대한 사용자 지정 옵션이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|LOG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스용 오류 로그 및 애플리케이션 로그에 오류를 기록합니다. 오류 로그에 기록되는 오류는 현재 최대 440바이트로 제한됩니다. sysadmin 고정 서버 역할의 멤버 또는 ALTER TRACE 권한을 가진 사용자만 WITH LOG를 지정할 수 있습니다.<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|NOWAIT|즉시 클라이언트에게 메시지를 전송합니다.<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|SETERROR|심각도에 상관없이 @@ERROR과 ERROR_NUMBER 값을 *msg_id*나 50000으로 설정합니다.<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
  
## <a name="remarks"></a>설명  
 RAISERROR에 의해 생성된 오류는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 코드에 의해 생성된 오류와 동일하게 동작합니다. RAISERROR에 의해 지정된 값은 ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY, ERROR_STATE 및 @@ERROR 시스템 함수에 의해 보고됩니다. TRY 블록에서 심각도 11 이상으로 RAISERROR가 실행되면 제어권을 관련 CATCH 블록으로 전달합니다. RAISERROR가 다음과 같이 실행되면 호출자에게 오류가 반환됩니다.  
  
-   TRY 블록 외부에서 실행된 경우  
  
-   TRY 블록의 심각도가 10 이하인 경우  
  
-   데이터베이스 연결이 종료되는 20 이상의 심각도인 경우  
  
 CATCH 블록은 RAISERROR을 사용하여 자신을 호출한 오류를 다시 발생시키고, ERROR_NUMBER 및 ERROR_MESSAGE와 같은 시스템 함수를 사용하여 원래 오류의 정보를 얻을 수 있습니다. 1부터 10까지의 심각도를 가진 메시지에 대해서는 기본적으로 @@ERROR이 0으로 설정됩니다.  
  
 *msg_id*가 sys.messages 카탈로그 뷰에서 사용자 정의 메시지를 지정할 경우 RAISERROR는 *msg_str*를 통해 사용자 정의 메시지의 텍스트에 적용한 규칙과 동일한 규칙을 사용하여 텍스트 열의 메시지를 처리합니다. 사용자 정의 메시지 텍스트에는 변환 사양이 포함될 수 있으며 RAISERROR는 인수 값을 변환 사양에 매핑합니다. 사용자 정의 오류 메시지를 추가하려면 sp_addmessage를, 사용자 정의 오류 메시지를 삭제하려면 sp_dropmessage를 사용하십시오.  
  
 RAISERROR는 호출하는 애플리케이션에 메시지를 반환하기 위해 PRINT 대신 사용할 수 있습니다. RAISERROR은 C 표준 라이브러리의 **printf** 함수의 기능과 유사한 문자 대체를 지원하지만 [!INCLUDE[tsql](../../includes/tsql-md.md)] PRINT 문은 지원하지 않습니다. PRINT 문은 TRY 블록의 영향을 받지 않지만 TRY 블록에서 실행된 RAISERROR가 11에서 19 사이의 심각도일 경우 제어권이 연결된 CATCH 블록으로 전달됩니다. CATCH 블록을 호출하지 않고 TRY 블록의 메시지를 반환하려면 RAISERROR에서 심각도를 10 이하로 지정하세요.  
  
 일반적으로 연속적인 인수는 첫 번째 인수가 첫 번째 변환 사양을, 두 번째 인수가 두 번째 변환 사양을 대체하는 식으로 연속적인 변환 사양을 대체합니다. 예를 들어 다음 `RAISERROR` 문에서 첫 번째 인수인 `N'number'`는 첫 번째 변환 사양인 `%s`를 대체하고 두 번째 인수인 `5`는 두 번째 변환 사양인 `%d.`를 대체합니다.  
  
```  
RAISERROR (N'This is message %s %d.', -- Message text.  
           10, -- Severity,  
           1, -- State,  
           N'number', -- First argument.  
           5); -- Second argument.  
-- The message text returned is: This is message number 5.  
GO  
```  
  
 변환 사양의 width 또는 precision으로 별표(*)를 지정하면 너비나 전체 자릿수로 사용될 값은 정수 인수 값으로 지정됩니다. 이 경우 한 개의 변환 사양은 최대 3개의 인수(각각 너비, 전체 자릿수 및 대체 값)를 사용할 수 있습니다.  
  
 예를 들어 다음 `RAISERROR` 문은 모두 동일한 문자열을 반환합니다. 첫 번째 경우는 인수 목록에서 너비와 전체 자릿수를 지정하며 두 번째 경우는 변환 사양에서 이를 지정합니다.  
  
```  
RAISERROR (N'<\<%*.*s>>', -- Message text.  
           10, -- Severity,  
           1, -- State,  
           7, -- First argument used for width.  
           3, -- Second argument used for precision.  
           N'abcde'); -- Third argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
RAISERROR (N'<\<%7.3s>>', -- Message text.  
           10, -- Severity,  
           1, -- State,  
           N'abcde'); -- First argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
```  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-error-information-from-a-catch-block"></a>A. CATCH 블록의 오류 정보 반환  
 다음 코드 예제에서는 `RAISERROR` 블록 내의 `TRY`를 사용하여 관련 `CATCH` 블록으로 실행을 이동하는 방법을 보여 줍니다. 또한 `RAISERROR` 블록을 호출한 오류에 관한 정보를 반환하는 방법을 `CATCH`을 사용하여 보여 줍니다.  
  
> [!NOTE]  
>  RAISERROR는 1에서 127까지 상태의 오류만 생성합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 상태 0의 오류를 발생시킬 수 있으므로 RAISERROR의 상태 매개 변수 값으로 전달하기 전에 ERROR_STATE에서 반환된 오류 상태를 확인하는 것이 좋습니다.  
  
```  
BEGIN TRY  
    -- RAISERROR with severity 11-19 will cause execution to   
    -- jump to the CATCH block.  
    RAISERROR ('Error raised in TRY block.', -- Message text.  
               16, -- Severity.  
               1 -- State.  
               );  
END TRY  
BEGIN CATCH  
    DECLARE @ErrorMessage NVARCHAR(4000);  
    DECLARE @ErrorSeverity INT;  
    DECLARE @ErrorState INT;  
  
    SELECT   
        @ErrorMessage = ERROR_MESSAGE(),  
        @ErrorSeverity = ERROR_SEVERITY(),  
        @ErrorState = ERROR_STATE();  
  
    -- Use RAISERROR inside the CATCH block to return error  
    -- information about the original error that caused  
    -- execution to jump to the CATCH block.  
    RAISERROR (@ErrorMessage, -- Message text.  
               @ErrorSeverity, -- Severity.  
               @ErrorState -- State.  
               );  
END CATCH;  
```  
  
### <a name="b-creating-an-ad-hoc-message-in-sysmessages"></a>B. sys.messages에 임시 메시지 만들기  
 다음 예에서는 sys.messages 카탈로그 뷰에 저장된 메시지를 발생시키는 방법을 보여 줍니다. `sp_addmessage` 시스템 저장 프로시저를 사용하여 sys.messages 카탈로그 뷰에 `50005`의 메시지 번호로 메시지가 추가되었습니다.  
  
```  
sp_addmessage @msgnum = 50005,  
              @severity = 10,  
              @msgtext = N'<\<%7.3s>>';  
GO  
RAISERROR (50005, -- Message id.  
           10, -- Severity,  
           1, -- State,  
           N'abcde'); -- First argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
sp_dropmessage @msgnum = 50005;  
GO  
```  
  
### <a name="c-using-a-local-variable-to-supply-the-message-text"></a>C. 지역 변수를 사용한 메시지 텍스트 제공  
 다음 코드 예제에서는 지역 변수를 사용하여 `RAISERROR` 문에 메시지 텍스트를 제공하는 방법을 보여 줍니다.  
  
```  
DECLARE @StringVariable NVARCHAR(50);  
SET @StringVariable = N'<\<%7.3s>>';  
  
RAISERROR (@StringVariable, -- Message text.  
           10, -- Severity,  
           1, -- State,  
           N'abcde'); -- First argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [DECLARE @local_variable(Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [PRINT&#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [xp_logevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logevent-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)   
 [ERROR_LINE&#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  

