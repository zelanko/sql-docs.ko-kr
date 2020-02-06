---
title: 일반적인 데이터베이스 메일 오류 | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- architecture [SQL Server], Database Mail
- Database Mail [SQL Server], architecture
- Database Mail [SQL Server], components
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ee5e7fd6511a624b05b4d6c7d03c1f2dcd288054
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70228436"
---
# <a name="common-errors-with-database-mail"></a>일반적인 데이터베이스 메일 오류 
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

이 문서에서는 데이터베이스 메일에서 발생하는 몇 가지 일반적인 오류와 그 솔루션에 대해 설명합니다.

## <a name="could-not-find-stored-procedure-sp_send_dbmail"></a>'sp_send_dbmail' 저장 프로시저를 찾을 수 없음
[sp_send_dbmail](../system-stored-procedures/sp-send-dbmail-transact-sql.md) 저장 프로시저는 msdb 데이터베이스에 설치됩니다. msdb 데이터베이스에서 **sp_send_dbmail**을 실행하거나 저장 프로시저 이름의 세 부분을 모두 지정해야 합니다.

예제:
```sql
EXEC msdb.dbo.sp_send_dbmail ...
```

또는

```sql
USE msdb;
GO
EXEC dbo.sp_send_dbmail ...
```

[데이터베이스 메일 구성 마법사](configure-database-mail.md)를 사용하여 프로필을 만들고 구성합니다.

## <a name="profile-not-valid"></a>프로필이 잘못됨
이 오류의 원인은 주로 두 가지입니다. 지정한 프로필이 존재하지 않거나 [sp_send_dbmail(Transact-SQL)](../system-stored-procedures/sp-send-dbmail-transact-sql.md)을 실행하는 사용자가 프로필에 액세스할 권한이 없기 때문입니다.

프로필에 대한 권한을 확인하려면 프로필 이름으로 저장 프로시저 [sysmail_help_principalprofile_sp(Transact-SQL)](../system-stored-procedures/sysmail-help-principalprofile-sp-transact-sql.md)를 실행합니다. 저장 프로시저 [sysmail_add_principalprofile_sp(Transact-SQL)](../system-stored-procedures/sysmail-help-principalprofile-sp-transact-sql.md) 또는 [데이터베이스 메일 구성 마법사](configure-database-mail.md)를 사용하여 msdb 사용자 또는 그룹에 프로필 액세스 권한을 부여합니다.

## <a name="permission-denied-on-sp_send_dbmail"></a>sp_send_dbmail에 대해 권한이 거부 경우

이 항목에서는 데이터베이스 메일 보내기를 시도하는 사용자가 sp_send_dbmail을 실행할 권한이 없음을 나타내는 오류 메시지를 받은 경우의 문제 해결 방법을 설명합니다.

오류 텍스트는 다음과 같습니다.

```
EXECUTE permission denied on object 'sp_send_dbmail', 
database 'msdb', schema 'dbo'.
```

데이터베이스 메일을 보내려면 사용자가 msdb 데이터베이스의 사용자여야 하며 msdb 데이터베이스에서 DatabaseMailUserRole 데이터베이스 역할의 멤버여야 합니다. msdb 사용자나 그룹을 이 역할에 추가하려면 SQL Server Management Studio를 사용하거나 데이터베이스 메일을 보내려는 사용자나 역할에 대해 다음 명령문을 실행합니다.

```sql
EXEC msdb.dbo.sp_addrolemember @rolename = 'DatabaseMailUserRole'
    ,@membername = '<user or role name>';
GO
```
자세한 내용은 [sp_addrolemember](../system-stored-procedures/sp-addrolemember-transact-sql.md) 및 [sp_droprolemember](../system-stored-procedures/sp-droprolemember-transact-sql.md)를 참조하세요.

## <a name="database-mail-queued-no-entries-in-sysmail_event_log-or-windows-application-event-log"></a>데이터베이스 메일이 큐에서 대기하고 sysmail_event_log 또는 Windows 애플리케이션 이벤트 로그에 항목이 없음 

데이터베이스 메일은 Service Broker를 사용하여 이메일 메시지를 큐에 보냅니다. 데이터베이스 메일이 중지되었거나 **msdb** 데이터베이스에서 Service Broker 메시지 배달이 활성화되지 않은 경우, 데이터베이스 메일은 데이터베이스 큐에 메시지를 보내기는 하지만 배달할 수는 없습니다. 이 경우 Service Broker 메시지는 Service Broker 메일 큐에 남아 있습니다. Service Broker가 외부 프로그램을 활성화하지 않으므로 **sysmail_event_log**에 로그 항목이 없으며 **sysmail_allitems** 및 관련 뷰의 항목 상태도 업데이트되지 않습니다.

다음 명령문을 실행하여 **msdb** 데이터베이스에서 Service Broker를 사용하는지 확인합니다.

```sql
SELECT is_broker_enabled FROM sys.databases WHERE name = 'msdb';
```

0 값은 msdb 데이터베이스에서 Service Broker 메시지 배달이 사용되지 않음을 나타냅니다. 문제를 해결하려면 다음 Transact-SQL 명령으로 데이터베이스에서 Service Broker를 활성화합니다.

```sql
USE master ;
GO

ALTER DATABASE msdb SET ENABLE_BROKER ;
GO
``` 

데이터베이스 메일은 많은 내부 저장 프로시저를 사용합니다. SQL Server를 새로 설치하면 노출 영역을 줄이기 위해 이러한 저장 프로시저가 사용하지 않도록 설정됩니다. 이러한 저장 프로시저를 설정하려면 다음 예제에서처럼 [sp_configure](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) 시스템 저장 프로시저의 **Database Mail XPs 옵션**을 사용합니다.

```sql
EXEC sp_configure 'show advanced options', 1;  
RECONFIGURE;
EXEC sp_configure 'Database Mail XPs', 1;  
RECONFIGURE  
GO  

Database Mail may be stopped in the **msdb** database. To check status of Database Mail, execute the following statement:

```sql
EXECUTE dbo.sysmail_help_status_sp;
```

메일 호스트 데이터베이스에서 데이터베이스 메일을 시작하려면 msdb 데이터베이스에서 다음 명령을 실행합니다.

```sql
EXECUTE dbo.sysmail_start_sp;
```

Service Broker는 자신이 활성화될 때 메시지의 대화 수명을 검사하며 지정된 대화 수명보다 오랫동안 Service Broker 전송 큐에 남아있던 메시지는 즉시 실패합니다. 데이터베이스 메일은 실패한 메시지의 상태를 [sysmail_allitems](../system-catalog-views/sysmail-allitems-transact-sql.md) 및 관련 뷰에 업데이트합니다. 사용자는 전자 메일 메시지를 다시 보낼지 여부를 결정해야 합니다. 데이터베이스 메일이 사용하는 대화 수명의 구성 방법은 [sysmail_configure_sp(Transact-SQL)](../system-stored-procedures/sysmail-configure-sp-transact-sql.md)를 참조하세요.



##  <a name="RelatedContent"></a> 참고 항목
  
-  [데이터베이스 메일 개요](database-mail.md)
-  [데이터베이스 메일 프로필 만들기](create-a-database-mail-profile.md)
  
  
