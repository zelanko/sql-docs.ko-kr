---
title: 데이터베이스 메일 구성 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqlimail.manageexistingaccount.f1
- sql12.swb.sqlimail.addaccounttoprofile.f1
- sql12.swb.sqlmailconfiguration.f1
- sql12.swb.sqlimail.profileandaccountmanagement.f1
- sql12.swb.sqlimail.manageprofilesecurity.principalview.f1
- sql12.swb.sqlimail.newsqlimailaccount.f1
- sql12.swb.sqlimail.configuresystem.f1
- sql12.swb.sqlimail.selectconfiguration.f1
- sql12.swb.sqlimail.newprofile.f1
- sql12.swb.sqlimail.manageexistingprofile.f1
- sql12.swb.sqlimail.welcome.f1
- sql12.swb.sqlimail.manageprofilesecurity.profileview.f1
- sql12.swb.sqlimail.completewizard.f1
- sql12.swb.sqlimail.newaccount.f1
helpviewer_keywords:
- Database Mail [SQL Server], configuration objects
- Database Mail [SQL Server], accounts
- configuration objects [Database Mail]
- Database Mail [SQL Server], profiles
- profiles [SQL Server], Database Mail
- accounts [Database Mail]
ms.assetid: 03f6e4c0-04ff-490a-bd91-637806215bd1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 45dd4bfc8cdb382f9ad093e92c5939986a9db8e0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84952641"
---
# <a name="database-mail-configuration-objects"></a>데이터베이스 메일 구성 개체
  데이터베이스 메일에는 두 가지 구성 개체가 있습니다. 데이터베이스 구성 개체를 사용하면 데이터베이스 애플리케이션 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 메일을 보낼 때 데이터베이스 메일에 사용할 설정을 구성할 수 있습니다.  
  
-   데이터베이스 메일 계정  
  
-   데이터베이스 메일 프로필  
  
  
##  <a name="database-mail-configuration-object-relationship"></a><a name="VisualElement"></a> 데이터베이스 메일 구성 개체 관계  
 위 그림에서는 2개의 프로필, 3개의 계정 및 3명의 사용자를 보여 줍니다. 사용자 1은 프로필 1에 대한 액세스 권한이 있고, 이 프로필은 계정 1과 계정 2를 사용합니다. 사용자 3은 프로필 2에 대한 액세스 권한이 있고, 이 프로필은 계정 2와 계정 3을 사용합니다. 사용자 2는 프로필 1과 프로필 2에 대한 액세스 권한이 있습니다.  
  
 ![사용자, 프로필 및 계정 관계](../../database-engine/media/databasemailprofileaccount.gif "사용자, 프로필 및 계정 관계")  
  
  
##  <a name="database-mail-account"></a><a name="DBAccount"></a> 데이터베이스 메일 계정  
 데이터베이스 메일 계정에는 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 전자 메일 메시지를 SMTP 서버로 보내기 위해 사용하는 정보가 포함되어 있습니다. 각 계정에는 하나의 전자 메일 서버에 대한 정보가 포함되어 있습니다.  
  
 데이터베이스 메일은 SMTP 서버와 통신하는 다음 3가지 인증 방법을 지원합니다.  
  
-   Windows 인증: 데이터베이스 메일이 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] Windows 서비스 계정의 자격 증명을 사용하여 SMTP 서버에 인증합니다.  
  
-   기본 인증:  데이터베이스 메일이 지정된 사용자 이름과 암호를 사용하여 SMTP 서버에 인증합니다.  
  
-   익명 인증:  SMTP 서버에 인증이 필요하지 않습니다.  데이터베이스 메일은 SMTP 서버 인증에 자격 증명을 사용하지 않습니다.  
  
 계정 정보는 **msdb** 데이터베이스에 저장됩니다. 각 계정은 다음 정보로 구성됩니다.  
  
-   계정 이름입니다.  
  
-   계정에 대한 설명  
  
-   운영자의 전자 메일 주소  
  
-   계정의 표시 이름입니다.  
  
-   계정에 대한 회신 정보로 사용하는 전자 메일 주소  
  
-   전자 메일 서버의 이름  
  
-   전자 메일 서버의 유형. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 항상 SMTP(Simple Mail Transfer Protocol)입니다.  
  
-   전자 메일 서버의 포트 번호  
  
-   SSL(Secure Sockets Layer)을 사용하여 SMTP 메일 서버에 연결하는지 여부를 나타내는 bit 열  
  
-   [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]에 대해 구성된 자격 증명을 사용하여 SMTP 서버에 연결하는지 여부를 나타내는 bit 열  
  
-   전자 메일 서버에 인증이 필요한 경우 전자 메일 서버에 대한 인증에 사용하는 사용자 이름  
  
-   전자 메일 서버에 인증이 필요한 경우 전자 메일 서버에 대한 인증에 사용하는 암호  
  
 데이터베이스 메일 구성 마법사를 사용하면 편리하게 계정을 만들고 관리할 수 있습니다. 또한 **msdb** 의 구성 저장 프로시저를 사용하여 계정을 만들고 관리할 수도 있습니다.  
  
  
##  <a name="database-mail-profile"></a><a name="DBProfile"></a> 데이터베이스 메일 프로필  
 데이터베이스 메일 프로필은 관련 데이터베이스 메일 계정을 정렬하여 모아 놓은 것입니다. 데이터베이스 메일을 사용하여 전자 메일을 보내는 애플리케이션은 계정을 직접 사용하는 대신 프로필을 지정합니다. 애플리케이션에서 사용하는 개체와 개별 전자 메일 서버에 대한 정보를 분리하면 유연성과 안정성을 향상시킬 수 있습니다. 프로필은 자동 장애 조치(failover)를 제공하기 때문에 하나의 전자 메일 서버가 응답하지 않아도 데이터베이스 메일이 다른 전자 메일 서버로 메일을 보낼 수 있습니다. 데이터베이스 관리자는 애플리케이션 코드나 작업 단계를 변경할 필요 없이 계정을 추가, 제거 또는 다시 구성할 수 있습니다.  
  
 또한 프로필을 사용하면 데이터베이스 관리자가 전자 메일 액세스를 제어할 수 있습니다. 데이터베이스 메일을 보내려면 **DatabaseMailUserRole** 의 멤버 자격이 필요합니다. 프로필이 있으면 관리자는 메일을 보내는 사람과 사용되는 계정을 유연하게 제어할 수 있습니다.  
  
 프로필은 퍼블릭 또는 프라이빗 프로필일 수 있습니다.  
  
 **공개 프로필** 은 **msdb** 데이터베이스에 있는 **DatabaseMailUserRole** 데이터베이스 역할의 모든 멤버에 대해 사용할 수 있습니다. 공개 프로필이 있으면 **DatabaseMailUserRole** 역할의 모든 멤버는 해당 프로필을 사용하여 메일을 보낼 수 있습니다.  
  
 **프라이빗 프로필** 은 **msdb** 데이터베이스의 보안 주체에 대해 정의됩니다. 지정된 데이터베이스 사용자, 역할 및 **sysadmin** 고정 서버 역할의 멤버만 개인 프로필을 사용하여 메일을 보낼 수 있습니다. 기본적으로 프로필은 프라이빗 프로필이며 **sysadmin** 고정 서버 역할의 멤버에게만 액세스를 허용합니다. 프라이빗 프로필을 사용할 수 있도록 하려면 **sysadmin** 이 사용자에게 프로필 사용 권한을 부여해야 합니다. 또한 **sp_send_dbmail** 저장 프로시저에 대한 EXECUTE 권한은 **DatabaseMailUserRole**멤버에게만 부여됩니다. 사용자가 메일 메시지를 보내려면 시스템 관리자가 해당 사용자를 **DatabaseMailUserRole** 데이터베이스 역할에 추가해야 합니다.  
  
 프로필을 사용하면 전자 메일 서버에 연결할 수 없거나 전자 메일 서버가 메시지를 처리할 수 없는 경우 안정성이 향상됩니다. 프로필의 계정마다 시퀀스 번호가 있습니다. 시퀀스 번호는 데이터베이스 메일에서 프로필의 계정을 사용하는 순서를 결정합니다. 데이터베이스 메일은 메시지를 성공적으로 보낸 마지막 계정을 새 전자 메일 메시지에 사용합니다. 그러나 아직 보낸 메시지가 없는 경우에는 시퀀스 번호가 가장 낮은 계정을 사용합니다. 해당 계정이 실패하면 데이터베이스 메일에서는 시퀀스 번호가 다음으로 높은 계정을 사용하여 메시지가 성공적으로 전송될 때까지 또는 시퀀스 번호가 가장 높은 계정이 실패할 때까지 작업을 계속합니다. 시퀀스 번호가 가장 높은 계정이 실패하면 데이터베이스 메일은 **sysmail_configure_sp** 의 **AccountRetryDelay**매개 변수에서 구성한 기간 동안 메일을 보내려는 시도를 일시 중지했다가 가장 낮은 시퀀스 번호에서 시작하여 다시 메일을 보내려는 시도를 시작합니다. **sysmail_configure_sp** 의 **AccountRetryAttempts**매개 변수를 사용하여 외부 메일 프로세스가 지정한 프로필의 각 계정을 사용하여 전자 메일 메시지를 보내려고 시도하는 횟수를 구성합니다.  
  
 시퀀스 번호가 같은 계정이 둘 이상 있으면 데이터베이스 메일은 지정된 전자 메일 메시지에 대해 해당 계정 중 하나만 사용합니다. 이 경우 데이터베이스 메일에서 항상 특정 시퀀스 번호에 대해 해당 계정이 사용되거나 메시지 간 동일한 계정이 사용되는 것은 아닙니다.  
  
  
##  <a name="database-mail-configuration-tasks"></a><a name="RelatedTasks"></a> 데이터베이스 메일 구성 태스크  
 다음 표에서는 데이터베이스 메일 구성 태스크에 대해 설명합니다.  
  
|구성 태스크|항목 링크|  
|------------------------|----------------|  
|데이터베이스 메일 계정을 만드는 방법에 대해 설명합니다.|[데이터베이스 메일 계정 만들기](create-a-database-mail-account.md)|  
|데이터베이스 메일 프로필을 만드는 방법에 대해 설명합니다.|[데이터베이스 메일 프로필 만들기](create-a-database-mail-profile.md)|  
|데이터베이스 메일을 구성하는 방법에 대해 설명합니다.|[데이터베이스 메일 구성](configure-database-mail.md)|  
|템플릿을 사용하여 데이터베이스 메일 구성 스크립트를 만드는 방법에 대해 설명합니다.||  
  
  
##  <a name="additional-database-configuration-tasks-system-stored-procedures"></a><a name="Add_Tasks"></a> 추가 데이터베이스 구성 태스크(시스템 저장 프로시저)  
 데이터베이스 메일 구성 저장 프로시저는 **msdb** 데이터베이스에 있습니다.  
  
 다음 표에서는 데이터베이스 메일을 구성하고 관리하는 데 사용되는 저장 프로시저를 나열합니다.  
  
### <a name="database-mail-settings"></a>데이터베이스 메일 설정  
  
|속성|Description|  
|----------|-----------------|  
|[sysmail_configure_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql)|데이터베이스 메일의 구성 설정을 변경합니다.|  
|[sysmail_help_configure_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-help-configure-sp-transact-sql)|데이터베이스 메일의 구성 설정을 표시합니다.|  
  
### <a name="accounts-and-profiles"></a>계정 및 프로필  
  
|속성|Description|  
|----------|-----------------|  
|[sysmail_add_profileaccount_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql)|데이터베이스 메일 프로필에 메일 계정을 추가합니다.|  
|[sysmail_delete_account_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-delete-account-sp-transact-sql)|데이터베이스 메일 계정을 삭제합니다.|  
|[sysmail_delete_profile_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-delete-profile-sp-transact-sql)|데이터베이스 메일 프로필을 삭제합니다.|  
|[sysmail_delete_profileaccount_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-delete-profileaccount-sp-transact-sql)|데이터베이스 메일 프로필에서 계정을 제거합니다.|  
|[sysmail_help_account_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-help-account-sp-transact-sql)|데이터베이스 메일 계정에 대한 정보를 나열합니다.|  
|[sysmail_help_profile_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-help-profile-sp-transact-sql)|하나 이상의 데이터베이스 메일 프로필에 대한 정보를 나열합니다.|  
|[sysmail_help_profileaccount_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-help-profileaccount-sp-transact-sql)|하나 이상의 데이터베이스 메일 프로필과 연관된 계정을 나열합니다.|  
|[sysmail_update_account_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-update-account-sp-transact-sql)|기존 데이터베이스 메일 계정의 정보를 업데이트합니다.|  
|[sysmail_update_profile_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-update-profile-sp-transact-sql)|데이터베이스 메일 프로필의 설명이나 이름을 변경합니다.|  
|[sysmail_update_profileaccount_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql)|데이터베이스 메일 프로필 내에서 계정의 시퀀스 번호를 업데이트합니다.|  
  
### <a name="security"></a>보안  
  
|속성|Description|  
|----------|-----------------|  
|[sysmail_add_principalprofile_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql)|데이터베이스 보안 주체에 대해 데이터베이스 메일 프로필을 사용할 수 있는 권한을 부여합니다.|  
|[sysmail_delete_principalprofile_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-delete-principalprofile-sp-transact-sql)|퍼블릭 또는 프라이빗 데이터베이스 메일 프로필을 사용할 수 있는 데이터베이스 보안 주체에 대한 사용 권한을 제거합니다.|  
|[sysmail_help_principalprofile_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-help-principalprofile-sp-transact-sql)|지정한 데이터베이스 사용자에 대한 데이터베이스 메일 프로필 정보를 나열합니다|  
|[sysmail_update_principalprofile_sp(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-update-principalprofile-sp-transact-sql)|지정한 데이터베이스 사용자에 대한 사용 권한 정보를 업데이트합니다.|  
  
### <a name="system-state"></a>시스템 상태  
  
|속성|Description|  
|----------|-----------------|  
|[sysmail_start_sp&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql)|데이터베이스 메일 외부 프로그램 및 관련 SQL Service Broker 큐를 시작합니다.|  
|[sysmail_stop_sp&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql)|데이터베이스 메일 외부 프로그램 및 관련 SQL Service Broker 큐를 중지합니다.|  
|[sysmail_help_status_sp&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-help-status-sp-transact-sql)|데이터베이스 메일이 시작되었는지 여부를 나타냅니다.|  
  
##  <a name="additional-references"></a><a name="RelatedContent"></a> 추가 참조  
  
-   [데이터베이스 메일 로그 및 감사](database-mail-log-and-audits.md)  
  
  
  
