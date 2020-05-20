---
title: sysmail_add_account_sp (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ee45e8d687f4da228508ebfdefc50fa55090f0b8
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814506"
---
# <a name="sysmail_add_account_sp-transact-sql"></a>sysmail_add_account_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  SMTP 계정에 대한 정보를 저장할 새로운 데이터베이스 메일 계정을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @account_name = ] 'account_name'`추가할 계정의 이름입니다. *account_name* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @email_address = ] 'email_address'`메시지를 보낼 전자 메일 주소입니다. 이 주소는 인터넷 전자 메일 주소여야 합니다. *email_address* 은 **nvarchar (128)** 이며 기본값은 없습니다. 예를 들어 에이전트의 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SqlAgent \@ Adventure-Works.com**주소에서 전자 메일을 보낼 수 있습니다.  
  
`[ @display_name = ] 'display_name'`이 계정의 전자 메일 메시지에 사용할 표시 이름입니다. *display_name* 은 **nvarchar (128)** 이며 기본값은 NULL입니다. 예를 들어 에이전트 계정에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전자 메일 메시지의 **자동 메일러 SQL Server 에이전트** 이름이 표시 될 수 있습니다.  
  
`[ @replyto_address = ] 'replyto_address'`이 계정에서 메시지에 대 한 응답을 보낼 주소입니다. *replyto_address* 은 **nvarchar (128)** 이며 기본값은 NULL입니다. 예를 들어 에이전트 계정에 대 한 회신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 데이터베이스 관리자 인 **danw \@ Adventure-Works.com**로 이동할 수 있습니다.  
  
`[ @description = ] 'description'`계정에 대 한 설명입니다. *description* 은 **nvarchar (256)** 이며 기본값은 NULL입니다.  
  
`[ @mailserver_name = ] 'server_name'`이 계정에 사용할 SMTP 메일 서버의 이름 또는 IP 주소입니다. 를 실행 하는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] IP 주소에 대 한 *server_name* 를 확인할 수 있어야 합니다. *server_name* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @mailserver_type = ] 'server_type'`전자 메일 서버의 유형입니다. *server_type* 는 **sysname**이며 기본값은 **' SMTP '** 입니다.  
  
`[ @port = ] port_number`전자 메일 서버의 포트 번호입니다. *port_number* 은 **int**이며 기본값은 25입니다.  
  
`[ @username = ] 'username'`전자 메일 서버에 로그온 하는 데 사용할 사용자 이름입니다. *username* 은 **nvarchar (128)** 이며 기본값은 NULL입니다. 이 매개 변수가 NULL이면 데이터베이스 메일은 이 계정에 대한 인증을 사용하지 않습니다. 메일 서버에 인증이 필요하지 않은 경우 username에 NULL을 사용합니다.  
  
`[ @password = ] 'password'`전자 메일 서버에 로그온 하는 데 사용할 암호입니다. *password* 는 **nvarchar (128)** 이며 기본값은 NULL입니다. username을 지정하지 않으면 암호를 제공할 필요가 없습니다.  
  
`[ @use_default_credentials = ] use_default_credentials`의 자격 증명을 사용 하 여 메일을 SMTP 서버로 보낼지 여부를 지정 합니다 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . **use_default_credentials** 은 bit 이며 기본값은 0입니다. 이 매개 변수가 1이면 데이터베이스 메일은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 자격 증명을 사용합니다. 이 매개 변수가 0 이면 데이터베이스 메일는 ** \@ 사용자 이름** 및 ** \@ 암호** 매개 변수를 보내고, 그렇지 않은 경우 ** \@ 사용자 이름** 및 ** \@ 암호** 매개 변수 없이 메일을 보냅니다.  
  
`[ @enable_ssl = ] enable_ssl`데이터베이스 메일에서 SSL(Secure Sockets Layer)를 사용 하 여 통신을 암호화할지 여부를 지정 합니다. **Enable_ssl** 은 bit 이며 기본값은 0입니다.  
  
`[ @account_id = ] account_id OUTPUT`새 계정에 대 한 계정 id를 반환 합니다. *account_id* 은 **int**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 데이터베이스 메일 ** \@ email_address**, ** \@ display_name**및 ** \@ replyto_address**에 대 한 별도의 매개 변수를 제공 합니다. ** \@ Email_address** 매개 변수는 메시지를 보낸 주소입니다. ** \@ Display_name** 매개 변수는 전자 메일 메시지의 **보낸 위치:** 필드에 표시 되는 이름입니다. ** \@ Replyto_address** 매개 변수는 전자 메일 메시지에 대 한 회신이 전송 되는 주소입니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 사용된 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에만 사용되는 전자 메일 주소에서 전자 메일 메시지를 보낼 수 있습니다. 해당 주소에서 보낸 메시지는 쉽게 알아 볼 수 있는 이름으로 표시되므로 수신자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 메시지를 보냈는지를 쉽게 확인할 수 있습니다. 수신자가 메시지에 회신하면 회신은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 사용하는 주소가 아니라 데이터베이스 관리자에게 전달되어야 합니다. 이 시나리오에서 계정은 **SqlAgent@Adventure-Works.com** 전자 메일 주소로를 사용 합니다. 표시 이름은 **SQL Server 에이전트 자동화 된 메일러**로 설정 됩니다. **danw@Adventure-Works.com**이 계정은를 회신 주소로 사용 하므로이 계정에서 보낸 메시지에 대 한 회신은 에이전트의 전자 메일 주소가 아니라 데이터베이스 관리자에 게 전달 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 됩니다. 이 세 매개 변수에 독립된 설정을 제공하면 데이터베이스 메일에서 사용자 요구 사항에 맞게 메시지를 구성할 수 있습니다.  
  
 ** \@ Mailserver_type** 매개 변수는 **' SMTP '** 값을 지원 합니다.  
  
 ** \@ Use_default_credentials** 1 이면의 자격 증명을 사용 하 여 메일을 SMTP 서버로 보냅니다 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . ** \@ Use_default_credentials** 이 0이 고 계정에 대 한 ** \@ 사용자 이름과** ** \@ 암호가** 지정 된 경우이 계정은 SMTP 인증을 사용 합니다. ** \@ 사용자 이름** 및 ** \@ 암호** 는 계정이 SMTP 서버에 사용 하는 자격 증명 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 컴퓨터가 있는 네트워크)입니다.  
  
 **Sysmail_add_account_sp** 저장 프로시저는 **msdb** 데이터베이스에 있으며 **dbo** 스키마가 소유 합니다. 현재 데이터베이스가 **msdb**가 아닌 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다.  
  
## <a name="permissions"></a>권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks Administrator`라는 계정을 만듭니다. 이 계정은 `dba@Adventure-Works.com`이라는 전자 메일 주소를 사용하고 SMTP 메일 서버 `smtp.Adventure-Works.com`으로 메일을 보냅니다. 이 계정에서 보낸 전자 메일 메시지는 `AdventureWorks Automated Mailer` 메시지의 **보낸 사람:** 줄에 표시 됩니다. 메시지에 대한 회신은 `danw@Adventure-Works.com`으로 전달됩니다.  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
