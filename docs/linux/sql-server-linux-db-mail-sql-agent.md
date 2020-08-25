---
title: Linux에서 SQL 에이전트와 함께 DB 메일 및 메일 경고 사용
description: Linux에서 SQL Server 에이전트(mssql-server-agent)와 함께 DB 메일을 사용하고 메일 경고를 설정하는 방법을 알아봅니다.
author: VanMSFT
ms.author: vanto
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: tbd
ms.openlocfilehash: 92306aa0c6fa28b2cd094e85f439d654605483b6
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088987"
---
# <a name="db-mail-and-email-alerts-with-sql-agent-on-linux"></a>Linux에서 SQL 에이전트와 함께 DB 메일 및 메일 경고 사용

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

다음 단계에서는 Linux에서 DB 메일을 설정하고 SQL Server 에이전트(**mssql-server-agent**)와 함께 사용하는 방법을 보여 줍니다. 

## <a name="1-enable-db-mail"></a>1. DB 메일 사용

```sql
USE master 
GO 
sp_configure 'show advanced options',1 
GO 
RECONFIGURE WITH OVERRIDE 
GO 
sp_configure 'Database Mail XPs', 1 
GO 
RECONFIGURE  
GO  
```

## <a name="2-create-a-new-account"></a>2. 새 계정 만들기
```sql
EXECUTE msdb.dbo.sysmail_add_account_sp 
@account_name = 'SQLAlerts', 
@description = 'Account for Automated DBA Notifications', 
@email_address = 'sqlagenttest@gmail.com', 
@replyto_address = 'sqlagenttest@gmail.com', 
@display_name = 'SQL Agent', 
@mailserver_name = 'smtp.gmail.com', 
@port = 587, 
@enable_ssl = 1, 
@username = 'sqlagenttest@gmail.com', 
@password = '<password>' 
GO
```

## <a name="3-create-a-default-profile"></a>3. 기본 프로필 만들기

```sql
EXECUTE msdb.dbo.sysmail_add_profile_sp 
@profile_name = 'default', 
@description = 'Profile for sending Automated DBA Notifications' 
GO
```

## <a name="4-add-the-database-mail-account-to-a-database-mail-profile"></a>4. 데이터베이스 메일 프로필에 데이터베이스 메일 계정 추가
```sql
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp 
@profile_name = 'default', 
@principal_name = 'public', 
@is_default = 1 ; 
 ```
 
## <a name="5-add-account-to-profile"></a>5. 프로필에 계정 추가 
```sql
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp   
@profile_name = 'default',   
@account_name = 'SQLAlerts',   
@sequence_number = 1;  
 ```
 
## <a name="6-send-test-email"></a>6. 테스트 메일 보내기
> [!NOTE]
> 메일 클라이언트로 이동하여 “보안 수준이 낮은 클라이언트에서 메일을 보내도록 허용”을 사용하도록 설정해야 할 수도 있습니다. 일부 클라이언트는 DB 메일을 메일 디먼으로 인식하지 않습니다.

```
EXECUTE msdb.dbo.sp_send_dbmail 
@profile_name = 'default', 
@recipients = 'recipient-email@gmail.com', 
@Subject = 'Testing DBMail', 
@Body = 'This message is a test for DBMail' 
GO
```

## <a name="7-set-db-mail-profile-using-mssql-conf-or-environment-variable"></a>7. mssql-conf 또는 환경 변수를 사용하여 DB 메일 프로필 설정
mssql-conf 유틸리티 또는 환경 변수를 사용하여 DB 메일 프로필을 등록할 수 있습니다. 이 예제에서는 프로필 기본값을 호출해 보겠습니다.

```bash
# via mssql-conf
sudo /opt/mssql/bin/mssql-conf set sqlagent.databasemailprofile default
# via environment variable
MSSQL_AGENT_EMAIL_PROFILE=default
```

## <a name="8-set-up-an-operator-for-sqlagent-job-notifications"></a>8. SQLAgent 작업 알림의 운영자 설정 

```sql
EXEC msdb.dbo.sp_add_operator 
@name=N'JobAdmins',  
@enabled=1, 
@email_address=N'recipient-email@gmail.com',  
@category_name=N'[Uncategorized]' 
GO 
```

## <a name="9-send-email-when-agent-test-job-succeeds"></a>9. ‘에이전트 테스트 작업’ 성공 시 메일 보내기 

```
EXEC msdb.dbo.sp_update_job 
@job_name='Agent Test Job', 
@notify_level_email=1, 
@notify_email_operator_name=N'JobAdmins' 
GO
```

## <a name="next-steps"></a>다음 단계
SQL Server 에이전트를 사용하여 작업을 만들고 예약 및 실행하는 방법에 대한 자세한 내용은 [Linux에서 SQL Server 에이전트 작업 실행](sql-server-linux-run-sql-server-agent-job.md)을 참조하세요.
