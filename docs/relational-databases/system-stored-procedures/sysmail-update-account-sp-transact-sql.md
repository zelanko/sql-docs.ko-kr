---
title: sysmail_update_account_sp (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: df0cbdda40b8e473ce81bf95b7c38e1cd2ec75c0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783680"
---
# <a name="sysmail_update_account_sp-transact-sql"></a>sysmail_update_account_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  기존 데이터베이스 메일 계정의 정보를 변경합니다.  
 
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_update_account_sp [ [ @account_id = ] account_id ] [ , ] [ [ @account_name = ] 'account_name' ] ,  
    [ @email_address = ] 'email_address' ,   
    [ @display_name = ] 'display_name' ,   
    [ @replyto_address = ] 'replyto_address' ,  
    [ @description = ] 'description' ,   
    [ @mailserver_name = ] 'server_name' ,   
    [ @mailserver_type = ] 'server_type' ,   
    [ @port = ] port_number ,   
    [ @timeout = ] 'timeout' ,  
    [ @username = ] 'username' ,  
    [ @password = ] 'password' ,  
    [ @use_default_credentials = ] use_default_credentials ,  
    [ @enable_ssl = ] enable_ssl   
```  
  
## <a name="arguments"></a>인수  
`[ @account_id = ] account_id`업데이트할 계정 ID입니다. *account_id* 은 **int**이며 기본값은 NULL입니다. *Account_id* 또는 *account_name* 중 하나 이상을 지정 해야 합니다. 둘 다 지정할 경우 프로시저가 계정 이름을 변경합니다.  
  
`[ @account_name = ] 'account_name'`업데이트할 계정의 이름입니다. *account_name* 는 **sysname**이며 기본값은 NULL입니다. *Account_id* 또는 *account_name* 중 하나 이상을 지정 해야 합니다. 둘 다 지정할 경우 프로시저가 계정 이름을 변경합니다.  
  
`[ @email_address = ] 'email_address'`메시지를 보낼 새 전자 메일 주소입니다. 이 주소는 인터넷 전자 메일 주소여야 합니다. 주소의 서버 이름은 데이터베이스 메일이 이 계정에서 메일을 보낼 때 사용하는 서버입니다. *email_address* 은 **nvarchar (128)** 이며 기본값은 NULL입니다.  
  
`[ @display_name = ] 'display_name'`이 계정의 전자 메일 메시지에 사용할 새 표시 이름입니다. *display_name* 은 **nvarchar (128)** 이며 기본값은 없습니다.  
  
`[ @replyto_address = ] 'replyto_address'`이 계정에서 보낸 전자 메일 메시지의 회신 머리글에 사용할 새 주소입니다. *replyto_address* 은 **nvarchar (128)** 이며 기본값은 없습니다.  
  
`[ @description = ] 'description'`계정에 대 한 새 설명입니다. *description* 은 **nvarchar (256)** 이며 기본값은 NULL입니다.  
  
`[ @mailserver_name = ] 'server_name'`이 계정에 사용할 SMTP 메일 서버의 새 이름입니다. 를 실행 하는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] IP 주소에 대 한 *server_name* 를 확인할 수 있어야 합니다. *server_name* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @mailserver_type = ] 'server_type'`메일 서버의 새 형식입니다. *server_type* 는 **sysname**이며 기본값은 없습니다. **' SMTP '** 값만 지원 됩니다.  
  
`[ @port = ] port_number`메일 서버의 새 포트 번호입니다. *port_number* 는 **int**이며 기본값은 없습니다.  
  
`[ @timeout = ] 'timeout'`단일 전자 메일 메시지의 System.net.mail.smtpclient에 대 한 시간 제한 매개 변수입니다. *Timeout* 은 **int** (초) 이며 기본값은 없습니다.  
  
`[ @username = ] 'username'`메일 서버에 로그온 하는 데 사용할 새 사용자 이름입니다. *사용자 이름은* **sysname**이며 기본값은 없습니다.  
  
`[ @password = ] 'password'`메일 서버에 로그온 하는 데 사용할 새 암호입니다. *password* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @use_default_credentials = ] use_default_credentials`서비스의 자격 증명을 사용 하 여 메일을 SMTP 서버로 보낼지 여부를 지정 합니다 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . **use_default_credentials** 은 bit 이며 기본값은 없습니다. 이 매개 변수가 1이면 데이터베이스 메일은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 자격 증명을 사용합니다. 이 매개 변수가 0 이면 데이터베이스 메일는 SMTP 서버의 인증에 ** \@ 사용자 이름과** ** \@ 암호** 를 사용 합니다. ** \@ 사용자 이름** 및 ** \@ 암호가** NULL 이면 익명 인증을 사용 합니다. 이 매개 변수를 지정하기 전에 해당 SMTP 관리자에게 문의하세요.  
  
`[ @enable_ssl = ] enable_ssl`데이터베이스 메일 TLS (Transport Layer Security)를 사용 하 여 통신을 암호화할지 여부를 지정 합니다 (이전에는 SSL (SSL(Secure Sockets Layer))). SMTP 서버에 TLS가 필요한 경우이 옵션을 사용 합니다. **enable_ssl** 은 bit 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 계정 이름과 계정 ID가 둘 다 지정되면 저장 프로시저는 계정에 대한 정보를 업데이트할 뿐만 아니라 계정 이름도 변경합니다. 계정 이름을 변경하면 계정 이름의 오류를 수정할 수 있습니다.  
  
 **Sysmail_update_account_sp** 저장 프로시저는 **msdb** 데이터베이스에 있으며 **dbo** 스키마가 소유 합니다. 현재 데이터베이스가 **msdb**가 아닌 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-changing-the-information-for-an-account"></a>A. 계정에 대한 정보 변경  
 다음 예에서는 `AdventureWorks Administrator` **msdb** 데이터베이스의 계정을 업데이트 합니다. 계정에 대한 정보는 제공된 값으로 설정됩니다.  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_name = 'AdventureWorks Administrator'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
### <a name="b-changing-the-name-of-an-account-and-the-information-for-an-account"></a>B. 계정 이름 및 계정에 대한 정보 변경  
 다음 예에서는 계정 ID `125`에 대한 계정 이름을 변경하고 계정 정보를 업데이트합니다. 계정의 새 이름은 `Backup Mail Server`입니다.  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_id = 125  
    ,@account_name = 'Backup Mail Server'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp-backup.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
