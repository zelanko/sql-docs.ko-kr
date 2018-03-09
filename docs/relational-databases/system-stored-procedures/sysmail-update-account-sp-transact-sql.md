---
title: sysmail_update_account_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4be8c0c87771f89d92cc0344c207149467c4554c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailupdateaccountsp-transact-sql"></a>sysmail_update_account_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 데이터베이스 메일 계정의 정보를 변경합니다.  
 
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@account_id** = ] *account_id*  
 업데이트할 계정 ID입니다. *account_id* 은 **int**, 기본값은 NULL입니다. 중 하나 이상을 *account_id* 또는 *account_name* 지정 해야 합니다. 둘 다 지정할 경우 프로시저가 계정 이름을 변경합니다.  
  
 [ **@account_name** = ] **'***account_name***'**  
 업데이트할 계정 이름입니다. *account_name* 은 **sysname**, 기본값은 NULL입니다. 중 하나 이상을 *account_id* 또는 *account_name* 지정 해야 합니다. 둘 다 지정할 경우 프로시저가 계정 이름을 변경합니다.  
  
 [ **@email_address** = ] **'***email_address***'**  
 메시지를 보낼 새 전자 메일 주소입니다. 이 주소는 인터넷 전자 메일 주소여야 합니다. 주소의 서버 이름은 데이터베이스 메일이 이 계정에서 메일을 보낼 때 사용하는 서버입니다. *email_address* 은 **nvarchar (128)**, 기본값은 NULL입니다.  
  
 [ **@display_name** = ] **'***display_name***'**  
 이 계정에서 보내는 전자 메일 메시지에 사용할 새 표시 이름입니다. *display_name* 은 **nvarchar (128)**, 기본값은 없습니다.  
  
 [ **@replyto_address** = ] **'***replyto_address***'**  
 이 계정에서 보내는 전자 메일 메시지의 회신 머리글에 사용할 새 주소입니다. *replyto_address* 은 **nvarchar (128)**, 기본값은 없습니다.  
  
 [ **@description** = ] **'***description***'**  
 계정에 대한 새 설명입니다. *설명* 은 **nvarchar (256)**, 기본값은 NULL입니다.  
  
 [ **@mailserver_name** = ] **'***server_name***'**  
 이 계정에 사용할 SMTP 메일 서버의 새 이름입니다. 실행 하는 컴퓨터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확인할 수 있어야는 *server_name* IP 주소입니다. *server_name* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@mailserver_type** = ] **'***server_type***'**  
 전자 메일 서버의 새 유형입니다. *server_type* 은 **sysname**, 기본값은 없습니다. 값만 **'SMTP'** 지원 됩니다.  
  
 [ **@port** = ] *port_number*  
 전자 메일 서버의 새 포트 번호입니다. *port_number* 은 **int**, 기본값은 없습니다.  
  
 [  **@timeout**  =] **'***timeout***'**  
 단일 전자 메일 메시지의 SmtpClient.Send에 대한 시간 제한 매개 변수입니다. *제한 시간* 은 **int** (초) 이며 기본값은 없습니다.  
  
 [ **@username** = ] **'***username***'**  
 전자 메일 서버에 로그온하는 데 사용할 새 사용자 이름입니다. *사용자 이름* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@password** = ] **'***password***'**  
 전자 메일 서버에 로그온하는 데 사용할 새 암호입니다. *암호* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@use_default_credentials**  =] use_default_credentials  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서비스의 자격 증명을 사용하여 메일을 SMTP 서버로 보낼지 여부를 지정합니다. **use_default_credentials** 는 bit 이며 기본값은 없습니다. 이 매개 변수가 1이면 데이터베이스 메일은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 자격 증명을 사용합니다. 이 매개 변수가 0 이면 데이터베이스 메일 사용 하는  **@username**  및  **@password**  SMTP 서버에 인증 합니다. 경우  **@username**  및  **@password**  NULL은 다음 익명 인증을 사용 합니다. 이 매개 변수를 지정하기 전에 해당 SMTP 관리자에게 문의하세요.  
  
 [  **@enable_ssl**  =] enable_ssl  
 데이터베이스 메일에서 SSL(Secure Sockets Layer)을 사용하여 통신을 암호화할지 여부를 지정합니다. SMTP 서버에 SSL이 필요한 경우 이 옵션을 사용합니다. **enable_ssl** 는 bit 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 계정 이름과 계정 ID가 둘 다 지정되면 저장 프로시저는 계정에 대한 정보를 업데이트할 뿐만 아니라 계정 이름도 변경합니다. 계정 이름을 변경하면 계정 이름의 오류를 수정할 수 있습니다.  
  
 저장된 프로시저 **sysmail_update_account_sp** 에 **msdb** 데이터베이스에 있으며가 소유 하 고는 **dbo** 스키마입니다. 현재 데이터베이스 없는 경우 세 부분으로 이루어진 이름으로 프로시저를 실행 해야 **msdb**합니다.  
  
## <a name="permissions"></a>Permissions  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-information-for-an-account"></a>1. 계정에 대한 정보 변경  
 다음 예제에서는 계정을 업데이트 `AdventureWorks Administrator` 에 **msdb** 데이터베이스입니다. 계정에 대한 정보는 제공된 값으로 설정됩니다.  
  
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
  
### <a name="b-changing-the-name-of-an-account-and-the-information-for-an-account"></a>2. 계정 이름 및 계정에 대한 정보 변경  
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
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [데이터베이스 메일 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
