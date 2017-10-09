---
title: RAISERROR (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/21/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 73
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15ed174d3f16a70f63973c586a15759afad72565
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="raiserror-transact-sql"></a>RAISERROR Transact SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  오류 메시지를 생성하고 세션에 대한 오류 처리를 시작합니다. RAISERROR는 sys.messages 카탈로그 뷰에 저장 된 사용자 정의 메시지를 참조 하거나 동적으로 메시지를 작성할 수 있습니다. 메시지는 호출하는 응용 프로그램 또는 연결된 TRY...CATCH 구문의 CATCH 블록에 서버 오류 메시지로 반환됩니다. 새 응용 프로그램 사용 해야 [THROW](../../t-sql/language-elements/throw-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
RAISERROR ( { msg_id | msg_str | @local_variable }  
    { ,severity ,state }  
    [ ,argument [ ,...n ] ] )  
    [ WITH option [ ,...n ] ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
RAISERROR ( { msg_str | @local_variable }  
    { ,severity ,state }  
    [ ,argument [ ,...n ] ] )  
    [ WITH option [ ,...n ] ]  
```  
  
## <a name="arguments"></a>인수  
 *msg_id*  
 사용자 정의 오류 메시지 번호 sp_addmessage를 사용 하 여 sys.messages 카탈로그 뷰에 저장 됩니다. 사용자 정의 오류 메시지의 오류 번호는 50000보다 커야 합니다. 때 *msg_id* 를 지정 하지 않으면 RAISERROR는 오류 번호가 50000 인 오류 메시지를 발생 시킵니다.  
  
 *msg_str*  
 서식이 지정 된 사용자 정의 메시지는 비슷합니다는 **printf** C 표준 라이브러리의 함수입니다. 오류 메시지는 최대 2,047자까지 지정할 수 있습니다. 메시지의 문자가 2,048자 이상이면 처음 2,044자만 표시되고 메시지가 잘렸음을 나타내기 위해 줄임표가 추가됩니다. 내부 저장 방식의 특성상 대체 매개 변수는 출력에 표시되는 것보다 더 많은 수의 문자를 사용합니다. 대체 매개 변수 예를 들어 *%d* 할당 된 값이 2 인 메시지 문자열에 문자 하나 실제로 생성 했지만 저장소 3 개의 추가 문자를 내부적으로 사용 합니다. 이러한 저장소 요구 사항 때문에 메시지 출력에 사용 가능한 문자 수가 감소됩니다.  
  
 때 *msg_str* 지정, RAISERROR는 오류 번호가 50000 인 오류 메시지를 발생 시킵니다.  
  
 *msg_str* 선택적으로 포함 된 변환 사양 가진 문자는 문자열입니다. 각 변환 사양은 인수 목록의 값은 형식 지정 및 변환 사양에서의 위치에 있는 필드에 배치 하는 방식을 정의 *msg_str*합니다. 변환 사양의 형식은 다음과 같습니다.  
  
 % [[*플래그*] [*너비*] [합니다. *정밀도*] [{h | l}]] *유형*  
  
 사용할 수 있는 매개 변수 *msg_str* 됩니다.  
  
 *플래그*  
  
 대체 값의 공백 처리 및 맞춤을 결정하는 코드입니다.  
  
|코드|접두사 또는 맞춤|Description|  
|----------|-----------------------------|-----------------|  
|-(빼기)|왼쪽 정렬|지정한 필드 너비 내에서 인수 값을 왼쪽으로 정렬합니다.|  
|+(더하기)|부호 접두사|값이 부호가 있는 형식일 경우 더하기(+)나 빼기(-) 부호를 인수 값 앞에 붙입니다.|  
|0(영)|0 패딩|최소 너비에 도달할 때까지 출력 앞에 0을 붙입니다. 0과 빼기(-) 부호가 있으면 0은 무시합니다.|  
|#(숫자)|x 또는 X의 16진수 유형에 대한 0x 접두사|o, x 또는 X 형식의 값에 사용할 경우 숫자 기호(#)는 0이 아닌 모든 값 앞에 0, 0x 또는 0X를 각각 붙입니다. d, i 또는 u 앞에 숫자 기호(#) 플래그가 있으면 플래그는 무시됩니다.|  
|' '(공백)|공간 채움|부호 있는 양수일 경우 출력 값 앞에 공백을 붙입니다. 더하기 부호(+) 플래그가 포함된 경우에는 무시됩니다.|  
  
 *너비*  
  
 인수 값이 배치될 필드의 최소 너비를 정의하는 정수입니다. 인수 값의 길이 보다 길거나 같아야 하는 경우 *너비*, 값은 패딩 없이 출력 됩니다. 값 보다 짧은 경우 *너비*, 값에 지정 된 길이까지 채워집니다 *너비*합니다.  
  
 별표(*)는 너비가 인수 목록의 관련 인수에 의해 지정되며 정수 값이어야 함을 의미합니다.  
  
 *전체 자릿수*  
  
 문자열 값의 경우 인수 값에서 가져온 문자의 최대 개수입니다. 예를 들어 문자열에 5개의 문자가 있고 precision이 3이면 문자열 값의 처음 3개 문자만 사용됩니다.  
  
 정수 값에 대 한 *정밀도* 은 인쇄 하는 최소 자릿수입니다.  
  
 별표(*)는 전체 자릿수가 인수 목록의 관련 인수에 의해 지정되며 정수 값이어야 함을 의미합니다.  
  
 {h | l} *유형*  
  
 문자 형식 d와 함께 사용 되 i, o, s, x, X 또는 u, 만듭니다 **shortint** (h) 또는 **longint** (l) 값입니다.  
  
|형식 사양|나타내는 대상|  
|------------------------|----------------|  
|d 또는 I|부호 있는 정수|  
|o|부호 없는 8진수|  
|s|문자열|  
|u|부호 없는 정수|  
|x 또는 X|부호 없는 16진수|  
  
> [!NOTE]  
>  이러한 유형 지정 기반에 대해 원래 정의 된 것으로는 **printf** C 표준 라이브러리의 함수입니다. RAISERROR 메시지 문자열 맵의 사용 되는 형식 사양을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터 형식에서 사용 하는 동안 **printf** C 언어 데이터 형식에 매핑됩니다. 형식에 사용 된 사양 들은 **printf** RAISERROR에서 지원 되지 않는 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 관련된 C 데이터 형식과 비슷한 데이터 형식을 없습니다. 예를 들어는 *%p* 때문에 포인터에 대 한 사양이 RAISERROR에서 지원 되지 않습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 포인터 데이터 형식이 없습니다.  
  
> [!NOTE]  
>  값을 변환 하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] **bigint** 지정 데이터 형식, **%I64d**합니다.  
  
 **@***local_variable*  
 과 동일한 방식으로 서식이 지정 된 문자열을 포함 하는 유효한 문자 데이터 형식의 변수는 *msg_str*합니다. **@***local_variable* 해야 **char** 또는 **varchar**, 이러한 데이터 형식으로 암시적으로 변환할 수 없습니다.  
  
 *심각도*  
 이 메시지에 연결된 사용자 정의 심각도입니다. 사용 하는 경우 *msg_id* RAISERROR에 지정 된 심각도 sp_addmessage를 사용 하 여 만든 사용자 정의 메시지를 발생 시키기 위해 sp_addmessage에 지정 된 심각도 보다 우선 합니다.  
  
 모든 사용자가 0부터 18까지의 심각도를 지정할 수 있습니다. 19부터 25 까지의 심각도 sysadmin 고정 서버 역할 또는 사용자가 ALTER TRACE 권한을 가진의 구성원이 지정할 수 있습니다. 19부터 25까지의 심각도에 대해서는 WITH LOG 옵션이 필요합니다. 0보다 작은 심각도 수준은 0으로 해석되고 25보다 작은 심각도 수준은 25로 해석됩니다.  
  
> [!CAUTION]  
>  20부터 25까지의 심각도는 치명적인 심각도입니다. 치명적인 심각도가 발생하면 메시지를 받은 다음 클라이언트 연결이 종료되고 오류 및 응용 프로그램 로그에 오류가 기록됩니다.  
  
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
 0에서 255 사이의 정수입니다. 음수 값은 기본적으로 1입니다. 값이 255 보다 큰 사용할 수 없습니다. 
  
 여러 위치에서 동일한 사용자 정의 오류가 발생하는 경우 각 위치의 고유 상태 번호를 사용하면 코드의 어떤 부분에서 오류가 발생하는지 찾는 데 도움이 됩니다.  
  
 *인수*  
 정의 된 변수의 대체에 사용 되는 매개 변수는 *msg_str* 또는 해당 하는 메시지 *msg_id*합니다. 0개 이상의 대체 매개 변수가 있을 수 있지만 대체 매개 변수의 총 개수가 20을 초과할 수는 없습니다. 각 대체 매개 변수는 지역 변수 이거나 다음 데이터 형식 중 될 수 있습니다: **tinyint**, **smallint**, **int**, **char**, **varchar**, **nchar**, **nvarchar**, **이진**, 또는 **varbinary**합니다. 다른 데이터 형식은 지원되지 않습니다.  
  
 *옵션*  
 오류에 대한 사용자 지정 옵션이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|LOG|오류 로그와 인스턴스에 대 한 응용 프로그램 로그에 오류가 기록 된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]합니다. 오류 로그에 기록되는 오류는 현재 최대 440바이트로 제한됩니다. Sysadmin 고정된 서버 역할 또는 ALTER TRACE 권한 가진 사용자의 구성원만 WITH LOG를 지정할 수 있습니다.<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|NOWAIT|즉시 클라이언트에게 메시지를 전송합니다.<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|SETERROR|설정의 @@ERROR 및 ERROR_NUMBER 값을 *msg_id* 또는 심각도 수준에 관계 없이 50000입니다.<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
  
## <a name="remarks"></a>주의  
 RAISERROR에 의해 생성된 오류는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 코드에 의해 생성된 오류와 동일하게 동작합니다. RAISERROR에 의해 지정 된 값에서 ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY, ERROR_STATE 및 @ 보고@ERROR 시스템 함수입니다. TRY 블록에서 심각도 11 이상으로 RAISERROR가 실행되면 제어권을 관련 CATCH 블록으로 전달합니다. RAISERROR가 다음과 같이 실행되면 호출자에게 오류가 반환됩니다.  
  
-   TRY 블록 외부에서 실행된 경우  
  
-   TRY 블록의 심각도가 10 이하인 경우  
  
-   데이터베이스 연결이 종료되는 20 이상의 심각도인 경우  
  
 CATCH 블록은 RAISERROR을 사용하여 자신을 호출한 오류를 다시 발생시키고, ERROR_NUMBER 및 ERROR_MESSAGE와 같은 시스템 함수를 사용하여 원래 오류의 정보를 얻을 수 있습니다. @@ERROR 1부터 10 까지의 심각도 가진 메시지에 대해 기본적으로 0으로 설정 합니다.  
  
 때 *msg_id* 지정 된 사용자 정의 메시지의 텍스트에 적용 될 때 동일한 규칙을 사용 하 여 텍스트 열의 메시지를에서 RAISERROR 프로세스 sys.messages 카탈로그 뷰에서 사용할 수 있는 사용자 정의 메시지를 지정 합니다. 사용 하 여 *msg_str*합니다. 사용자 정의 메시지 텍스트에는 변환 사양이 포함될 수 있으며 RAISERROR는 인수 값을 변환 사양에 매핑합니다. Sp_addmessage를 사용 하 여 사용자 정의 오류 메시지를 삭제 하는 사용자 정의 오류 메시지 및 sp_dropmessage 추가.  
  
 RAISERROR는 호출하는 응용 프로그램에 메시지를 반환하기 위해 PRINT 대신 사용할 수 있습니다. RAISERROR의 기능과 유사한 문자 대체를 지원 합니다.는 **printf** C 표준 라이브러리의 함수가 동안는 [!INCLUDE[tsql](../../includes/tsql-md.md)] PRINT 문에 그렇지 않습니다. PRINT 문은 TRY 블록의 영향을 받지 않지만 TRY 블록에서 실행된 RAISERROR가 11에서 19 사이의 심각도일 경우 제어권이 연결된 CATCH 블록으로 전달됩니다. CATCH 블록을 호출하지 않고 TRY 블록의 메시지를 반환하려면 RAISERROR에서 심각도를 10 이하로 지정하세요.  
  
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
  
### <a name="a-returning-error-information-from-a-catch-block"></a>1. CATCH 블록의 오류 정보 반환  
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
  
### <a name="b-creating-an-ad-hoc-message-in-sysmessages"></a>2. sys.messages에 임시 메시지 만들기  
 다음 예제에는 sys.messages 카탈로그 뷰에 저장 된 메시지를 발생 시키는 방법을 보여 줍니다. 사용 하 여 메시지가 sys.messages 카탈로그 뷰에 추가 된는 `sp_addmessage` 메시지 번호로 시스템 저장 프로시저 `50005`합니다.  
  
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
  
### <a name="c-using-a-local-variable-to-supply-the-message-text"></a>3. 지역 변수를 사용한 메시지 텍스트 제공  
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
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-returning-error-information-from-a-catch-block"></a>4. CATCH 블록의 오류 정보 반환  
 다음 코드 예제에서는 `RAISERROR` 블록 내의 `TRY`를 사용하여 관련 `CATCH` 블록으로 실행을 이동하는 방법을 보여 줍니다. 또한 `RAISERROR` 블록을 호출한 오류에 관한 정보를 반환하는 방법을 `CATCH`을 사용하여 보여 줍니다.  
  
> [!NOTE]  
>  RAISERROR는 1에서 18 사이의 상태의 오류만 생성합니다. PDW 엔진은 상태 0 사용 하 여 오류를 발생 시킬 수 있습니다, 때문에 RAISERROR의 상태 매개 변수 값으로 전달 하기 전에 ERROR_STATE에서 반환 된 오류 상태를 확인 하는 것이 좋습니다.  
  
```  
BEGIN TRY  
    -- RAISERROR with severity 11-18 will cause execution to   
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
  
    SET @ErrorMessage = ERROR_MESSAGE();  
    SET @ErrorSeverity = ERROR_SEVERITY();  
    SET @ErrorState = ERROR_STATE();  
  
    -- Use RAISERROR inside the CATCH block to return error  
    -- information about the original error that caused  
    -- execution to jump to the CATCH block.  
    RAISERROR (@ErrorMessage, -- Message text.  
               @ErrorSeverity, -- Severity.  
               @ErrorState -- State.  
               );  
END CATCH;  
```  
  
### <a name="e-using-a-local-variable-to-supply-the-message-text"></a>5. 지역 변수를 사용한 메시지 텍스트 제공  
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
  
## <a name="see-also"></a>관련 항목:  
 [선언 @local_variable (Transact SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md) [기본 제공 함수 &#40; Transact SQL &#41;](~/t-sql/functions/functions.md)   
 [PRINT&#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [sp_addmessage &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [xp_logevent &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/xp-logevent-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)   
 [ERROR_LINE&#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [Error_state&#40; Transact SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  


