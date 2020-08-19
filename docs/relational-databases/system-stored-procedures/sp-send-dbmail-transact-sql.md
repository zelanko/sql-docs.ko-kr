---
description: sp_send_dbmail(Transact-SQL)
title: sp_send_dbmail (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sendmail_sp_TSQL
- sendmail_sp
- SP_SEND_DBMAIL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_send_dbmail
ms.assetid: f1d7a795-a3fd-4043-ac4b-c781e76dab47
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 95b9b18b6f36ebbd8d43f38a2bc8fe28d8f3288b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446783"
---
# <a name="sp_send_dbmail-transact-sql"></a>sp_send_dbmail(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  지정된 수신자에게 전자 메일 메시지를 보냅니다. 이 메시지에는 쿼리 결과 집합, 첨부 파일 등이 포함될 수 있습니다. 데이터베이스 메일 큐에 메일이 성공적으로 배치 되 면 **sp_send_dbmail** 는 메시지의 **mailitem_id** 반환 합니다. 이 저장 프로시저는 **msdb** 데이터베이스에 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_send_dbmail [ [ @profile_name = ] 'profile_name' ]  
    [ , [ @recipients = ] 'recipients [ ; ...n ]' ]  
    [ , [ @copy_recipients = ] 'copy_recipient [ ; ...n ]' ]  
    [ , [ @blind_copy_recipients = ] 'blind_copy_recipient [ ; ...n ]' ]  
    [ , [ @from_address = ] 'from_address' ]  
    [ , [ @reply_to = ] 'reply_to' ]   
    [ , [ @subject = ] 'subject' ]   
    [ , [ @body = ] 'body' ]   
    [ , [ @body_format = ] 'body_format' ]  
    [ , [ @importance = ] 'importance' ]  
    [ , [ @sensitivity = ] 'sensitivity' ]  
    [ , [ @file_attachments = ] 'attachment [ ; ...n ]' ]  
    [ , [ @query = ] 'query' ]  
    [ , [ @execute_query_database = ] 'execute_query_database' ]  
    [ , [ @attach_query_result_as_file = ] attach_query_result_as_file ]  
    [ , [ @query_attachment_filename = ] query_attachment_filename ]  
    [ , [ @query_result_header = ] query_result_header ]  
    [ , [ @query_result_width = ] query_result_width ]  
    [ , [ @query_result_separator = ] 'query_result_separator' ]  
    [ , [ @exclude_query_output = ] exclude_query_output ]  
    [ , [ @append_query_error = ] append_query_error ]  
    [ , [ @query_no_truncate = ] query_no_truncate ]   
    [ , [ @query_result_no_padding = ] @query_result_no_padding ]   
    [ , [ @mailitem_id = ] mailitem_id ] [ OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
`[ @profile_name = ] 'profile_name'` 메시지를 보낼 프로필의 이름입니다. *Profile_name* 는 **sysname**형식 이며 기본값은 NULL입니다. *Profile_name* 는 기존 데이터베이스 메일 프로필의 이름 이어야 합니다. *Profile_name* 지정 하지 않으면 **sp_send_dbmail** 는 현재 사용자에 대 한 기본 개인 프로필을 사용 합니다. 사용자에 게 기본 개인 프로필이 없는 경우 **sp_send_dbmail** 는 **msdb** 데이터베이스에 대 한 기본 공개 프로필을 사용 합니다. 사용자에 게 기본 개인 프로필이 없고 데이터베이스에 대 한 기본 공개 프로필이 없는 경우 ** \@ profile_name** 를 지정 해야 합니다.  
  
`[ @recipients = ] 'recipients'` 메시지를 보낼 전자 메일 주소의 세미콜론으로 구분 된 목록입니다. 받는 사람 목록은 **varchar (max)** 형식입니다. 이 매개 변수는 선택 사항 이지만 하나 이상의 ** \@ 받는 사람**, ** \@ copy_recipients**또는 ** \@ blind_copy_recipients** 를 지정 해야 합니다. 그렇지 않으면 **sp_send_dbmail** 에서 오류를 반환 합니다.  
  
`[ @copy_recipients = ] 'copy_recipients'` 메시지를 복사 하는 데 대 한 세미콜론으로 구분 된 전자 메일 주소 목록입니다. 받는 사람 복사 목록은 **varchar (max)** 형식입니다. 이 매개 변수는 선택 사항 이지만 하나 이상의 ** \@ 받는 사람**, ** \@ copy_recipients**또는 ** \@ blind_copy_recipients** 를 지정 해야 합니다. 그렇지 않으면 **sp_send_dbmail** 에서 오류를 반환 합니다.  
  
`[ @blind_copy_recipients = ] 'blind_copy_recipients'` 메시지를 숨은 참조로 복사 하기 위한 세미콜론으로 구분 된 전자 메일 주소 목록입니다. 숨은 복사본 받는 사람 목록은 **varchar (max)** 유형입니다. 이 매개 변수는 선택 사항 이지만 하나 이상의 ** \@ 받는 사람**, ** \@ copy_recipients**또는 ** \@ blind_copy_recipients** 를 지정 해야 합니다. 그렇지 않으면 **sp_send_dbmail** 에서 오류를 반환 합니다.  
  
`[ @from_address = ] 'from_address'` 전자 메일 메시지의 ' 보낸 사람 주소 ' 값입니다. 이것은 메일 프로필의 설정을 재정의하는 데 사용되는 선택적 매개 변수입니다. 이 매개 변수는 **varchar (MAX)** 형식입니다. SMTP 보안 설정에 따라 재정의 허용 여부가 결정됩니다. 매개 변수를 지정하지 않으면 기본값은 NULL입니다.  
  
`[ @reply_to = ] 'reply_to'` 전자 메일 메시지의 ' 주소에 회신 '의 값입니다. 전자 메일 주소만 유효한 값으로 허용됩니다. 이것은 메일 프로필의 설정을 재정의하는 데 사용되는 선택적 매개 변수입니다. 이 매개 변수는 **varchar (MAX)** 형식입니다. SMTP 보안 설정에 따라 재정의 허용 여부가 결정됩니다. 매개 변수를 지정하지 않으면 기본값은 NULL입니다.  
  
`[ @subject = ] 'subject'` 전자 메일 메시지의 제목입니다. 제목은 **nvarchar (255)** 형식입니다. 제목을 지정하지 않으면 기본값은 'SQL Server Message'입니다.  
  
`[ @body = ] 'body'` 전자 메일 메시지의 본문입니다. 메시지 본문은 **nvarchar (max)** 형식 이며 기본값은 NULL입니다.  
  
`[ @body_format = ] 'body_format'` 메시지 본문의 형식입니다. 매개 변수는 **varchar (20)** 형식 이며 기본값은 NULL입니다. 이 매개 변수를 지정할 경우 나가는 메시지의 헤더가 보내져 메시지 본문이 지정된 형식임을 나타냅니다. 매개 변수에 포함할 수 있는 값은 다음과 같습니다.  
  
-   TEXT  
  
-   HTML  
  
 기본값은 TEXT입니다.  
  
`[ @importance = ] 'importance'` 메시지의 중요도입니다. 매개 변수의 형식은 **varchar (6)** 입니다. 매개 변수에 포함할 수 있는 값은 다음과 같습니다.  
  
-   낮음  
  
-   보통  
  
-   높음  
  
 기본값은 Normal입니다.  
  
`[ @sensitivity = ] 'sensitivity'` 메시지의 민감도입니다. 매개 변수의 형식은 **varchar (12)** 입니다. 매개 변수에 포함할 수 있는 값은 다음과 같습니다.  
  
-   보통  
  
-   Personal  
  
-   Private  
  
-   비밀  
  
 기본값은 Normal입니다.  
  
`[ @file_attachments = ] 'file_attachments'` 전자 메일 메시지에 첨부할 파일 이름의 세미콜론으로 구분 된 목록입니다. 목록의 파일은 절대 경로로 지정해야 합니다. 첨부 파일 목록은 **nvarchar (max)** 형식입니다. 기본적으로 데이터베이스 메일의 첨부 파일은 파일당 1MB로 제한됩니다.  
 
 > [!IMPORTANT]
 > 이 매개 변수는 로컬 파일 시스템에 액세스할 수 없기 때문에 Azure SQL Managed Instance에서 사용할 수 없습니다.
  
`[ @query = ] 'query'` 실행할 쿼리입니다. 쿼리 결과를 파일로 첨부할 수도 있고 전자 메일 메시지의 본문에 포함할 수도 있습니다. 쿼리는 **nvarchar (max)** 형식이 며 유효한 문을 포함할 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . 쿼리가 별도의 세션에서 실행 되므로 **sp_send_dbmail** 를 호출 하는 스크립트의 지역 변수는 쿼리에 사용할 수 없습니다.  
  
`[ @execute_query_database = ] 'execute_query_database'` 저장 프로시저가 쿼리를 실행 하는 데이터베이스 컨텍스트입니다. 매개 변수는 **sysname**형식 이며 기본값은 현재 데이터베이스입니다. 이 매개 변수는 ** \@ 쿼리가** 지정 된 경우에만 적용할 수 있습니다.  
  
`[ @attach_query_result_as_file = ] attach_query_result_as_file` 쿼리의 결과 집합이 첨부 파일로 반환 되는지 여부를 지정 합니다. *attach_query_result_as_file* 은 **bit**형식 이며 기본값은 0입니다.  
  
 값이 0 인 경우 쿼리 결과는 ** \@ 본문** 매개 변수의 내용 뒤에 오는 전자 메일 메시지의 본문에 포함 됩니다. 값이 1이면 결과가 첨부 파일로 반환됩니다. 이 매개 변수는 ** \@ 쿼리가** 지정 된 경우에만 적용할 수 있습니다.  
  
`[ @query_attachment_filename = ] query_attachment_filename` 쿼리 첨부 파일의 결과 집합에 사용할 파일 이름을 지정 합니다. *query_attachment_filename* 은 **nvarchar (255)** 형식 이며 기본값은 NULL입니다. *Attach_query_result* 가 0 이면이 매개 변수는 무시 됩니다. *Attach_query_result* 1이 고이 매개 변수가 NULL 이면 데이터베이스 메일 임의의 파일 이름을 만듭니다.  
  
`[ @query_result_header = ] query_result_header` 쿼리 결과에 열 머리글이 포함 되는지 여부를 지정 합니다. Query_result_header 값은 **bit**형식입니다. 값이 1이면 쿼리 결과에 열 머리글이 포함됩니다. 값이 0이면 쿼리 결과에 열 머리글이 포함되지 않습니다. 이 매개 변수의 기본값은 **1**입니다. 이 매개 변수는 ** \@ 쿼리가** 지정 된 경우에만 적용할 수 있습니다.  
 
   >[!NOTE]
   > \@Query_result_header를 0으로 설정 하 고 \@ query_no_truncate을 1로 설정 하는 경우 다음과 같은 오류가 발생할 수 있습니다.
   > <br> 메시지 22050, 수준 16, 상태 1, 줄 12: sqlcmd 라이브러리를 초기화 하지 못했습니다 (오류 번호-2147024809).
  
`[ @query_result_width = ] query_result_width` 쿼리 결과의 형식을 지정 하는 데 사용할 줄 너비 (문자 수)입니다. *Query_result_width* 은 **int**형식이 며 기본값은 256입니다. 10과 32767 사이의 값을 지정해야 합니다. 이 매개 변수는 ** \@ 쿼리가** 지정 된 경우에만 적용할 수 있습니다.  
  
`[ @query_result_separator = ] 'query_result_separator'` 쿼리 출력에서 열을 구분 하는 데 사용 되는 문자입니다. 구분 기호는 **char (1)** 형식입니다. 기본값은 ' '(공백)입니다.  
  
`[ @exclude_query_output = ] exclude_query_output` 전자 메일 메시지에 쿼리 실행의 출력을 반환할지 여부를 지정 합니다. **exclude_query_output** 은 bit 이며 기본값은 0입니다. 이 매개 변수가 0 이면 **sp_send_dbmail** 저장 프로시저를 실행 하면 콘솔에서 쿼리 실행 결과로 반환 된 메시지가 출력 됩니다. 이 매개 변수가 1 이면 **sp_send_dbmail** 저장 프로시저를 실행 해도 콘솔의 쿼리 실행 메시지가 인쇄 되지 않습니다.  
  
`[ @append_query_error = ] append_query_error`** \@ 쿼리** 인수에 지정 된 쿼리에서 오류가 반환 될 때 전자 메일을 보낼지 여부를 지정 합니다. **append_query_error** 은 **bit**이며 기본값은 0입니다. 이 매개 변수가 1이면 데이터베이스 메일에서 전자 메일 메시지의 본문에 쿼리 오류 메시지를 포함하여 전자 메일 메시지를 보냅니다. 이 매개 변수가 0 이면 데이터베이스 메일 전자 메일 메시지를 보내지 않고 **sp_send_dbmail** 는 반환 코드 1 (실패를 나타냄)으로 끝납니다.  
  
`[ @query_no_truncate = ] query_no_truncate` 대량 가변 길이 데이터 형식 (**varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **text**, **ntext**, **image**및 사용자 정의 데이터 형식) 잘림을 방지 하는 옵션을 사용 하 여 쿼리를 실행할지 여부를 지정 합니다. 설정된 경우 쿼리 결과에 열 머리글이 포함되지 않습니다. *Query_no_truncate* 값은 **bit**형식입니다. 값이 0이거나 지정되지 않은 경우에는 쿼리의 열이 256자로 잘립니다. 값이 1이면 쿼리의 열이 잘리지 않습니다. 이 매개 변수의 기본값은 0입니다.  
  
> [!NOTE]  
>  많은 양의 데이터를 사용 하는 경우 \@ **query_no_truncate** 옵션은 추가 리소스를 사용 하 고 서버 성능을 저하 시킬 수 있습니다.  
  
`[ @query_result_no_padding ] @query_result_no_padding` Bit 유형입니다. 기본값은 0입니다. 을 1로 설정 하면 쿼리 결과가 채워지지 않으므로 파일 크기가 줄어들 수 있습니다. \@Query_result_no_padding를 1로 설정 하 고 query_result_width 매개 변수를 설정 하는 경우 \@ \@ query_result_no_padding 매개 변수는 \@ query_result_width 매개 변수를 덮어씁니다.  
  
 이 경우 오류는 발생하지 않습니다.  
 
  >[!NOTE]
  > \@Query_result_no_padding를 1로 설정 하 고 query_no_truncate에 대 한 매개 변수를 제공 하면 다음과 같은 오류가 발생할 수 있습니다 \@ .
  > <br> 메시지 22050, 수준 16, 상태 1, 줄 0: \@ query_result_no_append 및 \@ query_no_truncate 옵션은 함께 사용할 수 없으므로 쿼리를 실행 하지 못했습니다. 
  
 \@Query_result_no_padding를 1로 설정 하 고 \@ query_no_truncate 매개 변수를 설정 하면 오류가 발생 합니다.  
  
`[ @mailitem_id = ] mailitem_id [ OUTPUT ]` 선택적 출력 매개 변수는 메시지의 *mailitem_id* 을 반환 합니다. *Mailitem_id* 은 **int**형식입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 반환 코드 0은 성공을 의미합니다. 다른 값은 실패를 의미합니다. 실패 한 문의 오류 코드는 \@ \@ 오류 변수에 저장 됩니다.  
  
## <a name="result-sets"></a>결과 집합  
 성공 시 "Mail queued" 메시지를 반환합니다.  
  
## <a name="remarks"></a>설명  
 데이터베이스 메일 구성 마법사 또는 **sp_configure**를 사용 하 여 데이터베이스 메일를 사용 하도록 설정 해야 합니다.  
  
 **sysmail_stop_sp** 는 외부 프로그램에서 사용 하는 Service Broker 개체를 중지 하 여 데이터베이스 메일를 중지 합니다. **sysmail_stop_sp**를 사용 하 여 데이터베이스 메일 중지 된 경우에도 **sp_send_dbmail** 메일을 수락 합니다. 데이터베이스 메일를 시작 하려면 **sysmail_start_sp**를 사용 합니다.  
  
 ** \@ 프로필** 을 지정 하지 않으면 **sp_send_dbmail** 는 기본 프로필을 사용 합니다. 전자 메일 메시지를 보내는 사용자에게 기본 프라이빗 프로필이 있을 경우 이 프로필이 사용됩니다. 사용자에 게 기본 개인 프로필이 없는 경우 **sp_send_dbmail** 기본 공개 프로필을 사용 합니다. 사용자에 대 한 기본 개인 프로필 및 기본 공개 프로필이 없는 경우 **sp_send_dbmail** 에서 오류를 반환 합니다.  
  
 **sp_send_dbmail** 는 내용이 없는 전자 메일 메시지를 지원 하지 않습니다. 전자 메일 메시지를 보내려면 ** \@ 본문**, ** \@ 쿼리**, ** \@ file_attachments**또는 ** \@ 제목**중 하나 이상을 지정 해야 합니다. 그렇지 않으면 **sp_send_dbmail** 에서 오류를 반환 합니다.  
  
 데이터베이스 메일에서는 현재 사용자의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 보안 컨텍스트를 사용하여 파일에 대한 액세스를 제어합니다. 따라서 인증을 사용 하 여 인증 된 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ** \@ file_attachments**를 사용 하 여 파일을 첨부할 수 없습니다. Windows에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하여 원격 컴퓨터에서 다른 원격 컴퓨터로 자격 증명을 제공할 수 없습니다. 그러므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터가 아닌 컴퓨터에서 명령을 실행할 경우 데이터베이스 메일은 네트워크 공유 위치에서 파일을 첨부할 수 없습니다.  
  
 ** \@ Query** 와 ** \@ file_attachments** 를 모두 지정 하 고 파일을 찾을 수 없는 경우 쿼리는 계속 실행 되지만 전자 메일은 전송 되지 않습니다.  
  
 쿼리를 지정한 경우 결과 집합의 서식은 인라인 텍스트로 지정됩니다. 결과 내 이진 데이터는 16진수 형식으로 전송됩니다.  
  
 ** \@ 받는 사람**, ** \@ copy_recipients**및 ** \@ blind_copy_recipients** 매개 변수는 세미콜론으로 구분 된 전자 메일 주소 목록입니다. 이러한 매개 변수 중 하나 이상을 제공 해야 합니다. 그렇지 않으면 **sp_send_dbmail** 에서 오류를 반환 합니다.  
  
 트랜잭션 컨텍스트 없이 **sp_send_dbmail** 를 실행 하는 경우 데이터베이스 메일는 암시적 트랜잭션을 시작 하 고 커밋합니다. 기존 트랜잭션 내에서 **sp_send_dbmail** 를 실행 하는 경우 데이터베이스 메일 사용자에 게 변경 내용을 커밋하거나 롤백해야 합니다. 내부 트랜잭션은 시작되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sp_send_dbmail** 에 대 한 실행 권한은 기본적으로 **msdb** 데이터베이스에 있는 **databasemailuser** 데이터베이스 역할의 모든 멤버에 게 부여 됩니다. 그러나 메시지를 보내는 사용자에 게 요청에 대해 프로필을 사용할 수 있는 권한이 없는 경우에는 **sp_send_dbmail** 에서 오류를 반환 하 고 메시지를 보내지 않습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-sending-an-e-mail-message"></a>A. 전자 메일 메시지 보내기  
 이 예에서는 전자 메일 주소를 사용 하 여 친구에 게 전자 메일 메시지를 보냅니다 `myfriend@Adventure-Works.com` . 메시지의 제목은 `Automated Success Message`입니다. 메시지의 본문에는 `'The stored procedure finished successfully'`라는 문장이 포함되어 있습니다.  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @body = 'The stored procedure finished successfully.',  
    @subject = 'Automated Success Message' ;  
```  
  
### <a name="b-sending-an-e-mail-message-with-the-results-of-a-query"></a>B. 쿼리 결과를 포함하여 전자 메일 메시지 보내기  
 이 예에서는 전자 메일 주소를 사용 하 여 친구에 게 전자 메일 메시지를 보냅니다 `yourfriend@Adventure-Works.com` . 메시지의 제목은 `Work Order Count`이며 이 메시지는 `DueDate`가 2004년 4월 30일부터 2일 내인 작업 주문 번호를 보여 주는 쿼리를 실행합니다. 데이터베이스 메일은 결과를 텍스트 파일로 첨부합니다.  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @query = 'SELECT COUNT(*) FROM AdventureWorks2012.Production.WorkOrder  
                  WHERE DueDate > ''2004-04-30''  
                  AND  DATEDIFF(dd, ''2004-04-30'', DueDate) < 2' ,  
    @subject = 'Work Order Count',  
    @attach_query_result_as_file = 1 ;  
```  
  
### <a name="c-sending-an-html-e-mail-message"></a>C. HTML 전자 메일 메시지 보내기  
 이 예에서는 전자 메일 주소를 사용 하 여 친구에 게 전자 메일 메시지를 보냅니다 `yourfriend@Adventure-Works.com` . 메시지의 제목은 `Work Order List`이며 이 메시지에는 `DueDate`가 2004년 4월 30일부터 2일 내인 작업 주문을 보여 주는 HTML 문서가 포함되어 있습니다. 데이터베이스 메일은 메시지를 HTML 형식으로 보냅니다.  
  
```  
DECLARE @tableHTML  NVARCHAR(MAX) ;  
  
SET @tableHTML =  
    N'<H1>Work Order Report</H1>' +  
    N'<table border="1">' +  
    N'<tr><th>Work Order ID</th><th>Product ID</th>' +  
    N'<th>Name</th><th>Order Qty</th><th>Due Date</th>' +  
    N'<th>Expected Revenue</th></tr>' +  
    CAST ( ( SELECT td = wo.WorkOrderID,       '',  
                    td = p.ProductID, '',  
                    td = p.Name, '',  
                    td = wo.OrderQty, '',  
                    td = wo.DueDate, '',  
                    td = (p.ListPrice - p.StandardCost) * wo.OrderQty  
              FROM AdventureWorks.Production.WorkOrder as wo  
              JOIN AdventureWorks.Production.Product AS p  
              ON wo.ProductID = p.ProductID  
              WHERE DueDate > '2004-04-30'  
                AND DATEDIFF(dd, '2004-04-30', DueDate) < 2   
              ORDER BY DueDate ASC,  
                       (p.ListPrice - p.StandardCost) * wo.OrderQty DESC  
              FOR XML PATH('tr'), TYPE   
    ) AS NVARCHAR(MAX) ) +  
    N'</table>' ;  
  
EXEC msdb.dbo.sp_send_dbmail @recipients='yourfriend@Adventure-Works.com',  
    @subject = 'Work Order List',  
    @body = @tableHTML,  
    @body_format = 'HTML' ;  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일 ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
  
  
