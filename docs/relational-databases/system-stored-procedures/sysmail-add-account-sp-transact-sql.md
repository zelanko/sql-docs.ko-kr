---
title: sysmail_add_account_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_account_sp
- sysmail_add_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_account_sp
ms.assetid: 65e15e2e-107c-49c3-b12c-f4edf0eb1617
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6f09f54a4b5869279cfa3c53c5e82d86213736f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017837"
---
# <a name="sysmailaddaccountsp-transact-sql"></a>sysmail_add_account_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  SMTP 계정에 대한 정보를 저장할 새로운 데이터베이스 메일 계정을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_add_account_sp  [ @account_name = ] 'account_name',  
    [ @email_address = ] 'email_address' ,  
    [ [ @display_name = ] 'display_name' , ]  
    [ [ @replyto_address = ] 'replyto_address' , ]  
    [ [ @description = ] 'description' , ]  
    [ @mailserver_name = ] 'server_name'   
    [ , [ @mailserver_type = ] 'server_type' ]  
    [ , [ @port = ] port_number ]  
    [ , [ @username = ] 'username' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @use_default_credentials = ] use_default_credentials ]  
    [ , [ @enable_ssl = ] enable_ssl ]  
    [ , [ @account_id = ] account_id OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
`[ @account_name = ] 'account_name'` 추가할 계정의 이름입니다. *account_name* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @email_address = ] 'email_address'` 메시지를 보낼 전자 메일 주소입니다. 이 주소는 인터넷 전자 메일 주소여야 합니다. *email_address* 됩니다 **nvarchar (128)** , 기본값은 없습니다. 예를 들어 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 주소에서 전자 메일을 보낼 수 있습니다 **SqlAgent@Adventure-Works.com** 합니다.  
  
`[ @display_name = ] 'display_name'` 이 계정에서 전자 메일 메시지에 사용할 표시 이름입니다. *display_name* 됩니다 **nvarchar (128)** , 기본값은 NULL입니다. 예를 들어 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 이름에 표시 될 수 있습니다 **SQL Server Agent Automated Mailer** 전자 메일 메시지에 있습니다.  
  
`[ @replyto_address = ] 'replyto_address'` 이 계정에서 메시지에 대 한 응답으로 전송 되는 주소입니다. *replyto_address* 됩니다 **nvarchar (128)** , 기본값은 NULL입니다. 예를 들어,에 대 한 계정에 회신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 관리자 인 에이전트를 실행할 수 있습니다 **danw@Adventure-Works.com** 합니다.  
  
`[ @description = ] 'description'` 계정에 대 한 설명이입니다. *설명* 됩니다 **nvarchar(256)** , 기본값은 NULL입니다.  
  
`[ @mailserver_name = ] 'server_name'` 이름 또는이 계정에 사용할 SMTP 메일 서버 IP 주소. 실행 하는 컴퓨터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확인할 수 있어야 합니다 *server_name* IP 주소를 합니다. *server_name* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @mailserver_type = ] 'server_type'` 전자 메일 서버의 유형입니다. *server_type* 됩니다 **sysname**, 기본값은 **'SMTP'** ...  
  
`[ @port = ] port_number` 전자 메일 서버에 대 한 포트 번호입니다. *port_number* 됩니다 **int**, 기본값은 25입니다.  
  
`[ @username = ] 'username'` 전자 메일 서버에 로그온 하는 데 사용자 이름입니다. *사용자 이름* 됩니다 **nvarchar (128)** , 기본값은 NULL입니다. 이 매개 변수가 NULL이면 데이터베이스 메일은 이 계정에 대한 인증을 사용하지 않습니다. 메일 서버에 인증이 필요하지 않은 경우 username에 NULL을 사용합니다.  
  
`[ @password = ] 'password'` 전자 메일 서버에 로그온 하는 데 암호입니다. *암호* 됩니다 **nvarchar (128)** , 기본값은 NULL입니다. username을 지정하지 않으면 암호를 제공할 필요가 없습니다.  
  
`[ @use_default_credentials = ] use_default_credentials` 메일의 자격 증명을 사용 하 여 SMTP 서버로 보낼지 여부를 지정 된 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]합니다. **use_default_credentials** 는 bit 이며 기본값은 0입니다. 이 매개 변수가 1이면 데이터베이스 메일은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 자격 증명을 사용합니다. 데이터베이스 메일에서는이 매개 변수가 0 인 경우는 **@username** 하 고 **@password** 있으면 매개 변수 없이 메일을 보냅니다 그렇지 않으면 **@username** 하 고 **@password** 매개 변수입니다.  
  
`[ @enable_ssl = ] enable_ssl` 데이터베이스 메일 Secure Sockets Layer를 사용 하 여 통신을 암호화할지 여부를 지정 합니다. **Enable_ssl** 는 bit 이며 기본값은 0입니다.  
  
`[ @account_id = ] account_id OUTPUT` 새 계정의 계정 id를 반환합니다. *account_id* 됩니다 **int**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 데이터베이스 메일에 대 한 별도 매개 변수를 제공 **@email_address** 하십시오 **@display_name** , 및 **@replyto_address** 합니다. 합니다 **@email_address** 매개 변수는 메시지를 보낼 주소입니다. 합니다 **@display_name** 매개 변수는 표시 된 이름을 합니다 **에서:** 전자 메일 메시지의 필드입니다. 합니다 **@replyto_address** 매개 변수는 전자 메일 메시지 회신을 보낼 주소입니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 사용된 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에만 사용되는 전자 메일 주소에서 전자 메일 메시지를 보낼 수 있습니다. 해당 주소에서 보낸 메시지는 쉽게 알아 볼 수 있는 이름으로 표시되므로 수신자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 메시지를 보냈는지를 쉽게 확인할 수 있습니다. 수신자가 메시지에 회신하면 회신은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 사용하는 주소가 아니라 데이터베이스 관리자에게 전달되어야 합니다. 이 시나리오에서는 계정 사용 **SqlAgent@Adventure-Works.com** 전자 메일 주소로 합니다. 표시 이름 설정 되어 **SQL Server Agent Automated Mailer**합니다. 계정을 사용 하 여 **danw@Adventure-Works.com** 주소로 회신으로이 계정에서 보낸 메시지에 대 한 응답으로가 서에 대 한 전자 메일 주소가 아니라 데이터베이스 관리자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트입니다. 이 세 매개 변수에 독립된 설정을 제공하면 데이터베이스 메일에서 사용자 요구 사항에 맞게 메시지를 구성할 수 있습니다.  
  
 합니다 **@mailserver_type** 매개 변수 값을 지원 합니다 **'SMTP'** 합니다.  
  
 때 **@use_default_credentials** 1 메일의 자격 증명을 사용 하 여 SMTP 서버에 전송 되는 여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]입니다. 때 **@use_default_credentials** 0 및 **@username** 및 **@password** 계정에서는 SMTP 인증 계정에 지정 됩니다. **@username** 하 고 **@password** 에 대 한 자격 증명이 아닌 SMTP 서버에 대 한 계정을 사용 하 여 자격 증명은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 컴퓨터에 있는 네트워크입니다.  
  
 저장된 프로시저 **sysmail_add_account_sp** 에 **msdb** 데이터베이스 및 소유 하는 **dbo** 스키마입니다. 현재 데이터베이스에는 없는 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다 **msdb**합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저 기본의 멤버에 대 한 권한을 실행 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks Administrator`라는 계정을 만듭니다. 이 계정은 `dba@Adventure-Works.com`이라는 전자 메일 주소를 사용하고 SMTP 메일 서버 `smtp.Adventure-Works.com`으로 메일을 보냅니다. 이 계정 표시에서 보낸 전자 메일 메시지 `AdventureWorks Automated Mailer` 에 **에서:** 메시지의 줄입니다. 메시지에 대한 회신은 `danw@Adventure-Works.com`으로 전달됩니다.  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [데이터베이스 메일 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
