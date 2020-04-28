---
title: Azure에 대 한 SQL Server Managed Backup 모니터링 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: cfb9e431-7d4c-457c-b090-6f2528b2f315
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 25e45e5877d528d1f01fe8695d8575466991c381
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798041"
---
# <a name="monitor-sql-server-managed-backup-to-azure"></a>Azure에 SQL Server 관리 백업 모니터링
  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 백업 프로세스 중에 문제 및 오류와 가능한 경우 수정 작업을 포함하는 해결책을 식별하는 기본 제공된 조치를 포함합니다.  그러나 사용자 개입이 필요한 특정 상황이 있습니다. 이 항목에서는 백업의 전체 상태를 확인하고 해결해야 할 오류를 식별하는 데 사용할 수 있는 도구에 대해 설명합니다.  
  
## <a name="overview-of-ss_smartbackup-built-in-debugging"></a>[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 기본 제공 디버깅 개요  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 예약된 백업을 정기적으로 검토하고 실패한 백업을 다시 예약하려고 합니다. 또한 스토리지 계정을 정기적으로 폴링하여 데이터베이스의 복구 기능에 영향을 주는 로그 체인이 끊어지는 상황을 식별하고 이에 따라 새 백업을 예약합니다. 또한 Azure 제한 정책을 고려 하 고 여러 데이터베이스 백업을 관리 하는 메커니즘이 있습니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 확장 이벤트를 사용하여 모든 작업을 추적합니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 에이전트에서 사용하는 확장 이벤트 채널에는 Admin, Operational, Analytical 및 Debug가 있습니다. Admin 범주 아래에 있는 이벤트는 일반적으로 오류와 관련이 있으며 사용자 개입을 필요로 하고 기본적으로 설정되어 있습니다. Analytical 이벤트도 기본적으로 설정되어 있지만 일반적으로 사용자 개입이 필요한 오류와 관련이 없습니다. Operation 이벤트는 일반적으로 정보 제공용입니다. 예를 들어 운영 이벤트에는 백업 예약, 성공적인 백업 완료 등이 포함 됩니다. 디버그는 가장 자세한 정보를 표시 하며 문제를 확인 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 하 고 필요한 경우 수정 하는 데 내부적으로 사용 됩니다.  
  
### <a name="configure-monitoring-parameters-for-ss_smartbackup"></a>[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]에 대한 모니터링 매개 변수 구성  
 **Smart_admin sp_set_parameter** 시스템 저장 프로시저를 사용 하 여 모니터링 설정을 지정할 수 있습니다. 다음 섹션은 확장 이벤트를 설정하고 오류 및 경고에 대한 전자 메일 알림을 설정하는 프로세스를 안내합니다.  
  
 **Smart_admin fn_get_parameter** 함수를 사용 하 여 특정 매개 변수 또는 구성 된 모든 매개 변수에 대 한 현재 설정을 가져올 수 있습니다. 매개 변수가 이전에 구성되지 않은 경우 함수가 값을 반환하지 않습니다.  
  
1.  [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣은 후 **실행**을 클릭합니다. 이렇게 하면 확장 이벤트 및 전자 메일 알림에 대한 현재 구성이 반환됩니다.  
  
```sql
Use msdb  
Go  
SELECT * FROM smart_admin.fn_get_parameter (NULL)  
GO  
```  
  
 자세한 내용은 [smart_admin fn_get_parameter &#40;&#41;transact-sql](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql) 을 참조 하세요.  
  
### <a name="extended-events-for-monitoring"></a>모니터링에 대한 확장 이벤트  
 기본적으로 Admin, Operational 및 Analytical 이벤트가 설정되어 있습니다. 문제를 해결하기 위해 수동 개입이 필요한 오류를 식별할 때 Admin 이벤트가 가장 중요하고 유용합니다. Operational 및 Debug 이벤트를 설정할 수 있지만 이러한 이벤트는 자세한 정보를 포함하고 필터링이 필요할 수 있다는 사실을 고려하십시오. 다음 절차에서는 확장 이벤트를 통해 기록된 이벤트를 모니터링하는 방법에 대해 설명합니다.  
  
> [!IMPORTANT]  
>  SQL 엔진용 확장 이벤트와 달리 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 확장 이벤트 세션 개념을 지원하지 않습니다. 시스템 저장 프로시저와 함수는 확장 이벤트와 상호 작용하는 데 사용되는 도구입니다. 또한 로그 디렉터리에서 확장 이벤트 로그를 볼 수 있습니다.  
  
##### <a name="to-configure-and-view-extended-events"></a>확장 이벤트를 구성하고 보려면  
  
1.  사용 가능한 확장 이벤트 채널 및 해당 현재 상태를 보려면 다음 쿼리를 실행합니다.  
  
    ```sql
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     이 쿼리의 출력은 event_name, 해당 이벤트가 구성 가능한지 여부 및 해당 이벤트가 현재 설정되어 있는지 여부를 표시합니다.  자세한 내용은 [smart_admin fn_get_current_xevent_settings &#40;transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql)를 참조 하세요.  
  
2.  Debug 이벤트를 설정하려면 다음 쿼리를 실행합니다.  
  
    ```sql
    --  to enable debug events  
    Use msdb;  
    GO 
    EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
    ```  
  
     저장 프로시저에 대 한 자세한 내용은 [smart_admin sp_set_parameter &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql)를 참조 하세요.  
  
3.  기록된 이벤트를 보려면 다음 쿼리를 실행합니다.  
  
    ```sql
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;
    ```  
  
    ```sql
    --  view all admin events  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'
    ```  
  
### <a name="aggregated-error-countshealth-status"></a>집계된 오류 수/상태  
 **Smart_admin fn_get_health_status** 함수는의 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]상태를 모니터링 하는 데 사용할 수 있는 각 범주에 대 한 집계 된 오류 개수 테이블을 반환 합니다. 이 동일한 함수는 이 항목 뒷부분에서 설명하는 시스템에서 구성된 전자 메일 알림 메커니즘에서도 사용됩니다.   
이 집계 수는 시스템 상태를 모니터링하는 데 사용될 수 있습니다. 예를 들어 number_ of_retention_loops 열이 30분에서 0인 경우 보존 관리 작업에 시간이 오래 걸리고 있거나 제대로 작동하지 않고 있을 가능성이 있습니다. 0이 아닌 오류 열은 문제를 나타내며 해당 문제를 검색하기 위해 확장 이벤트 로그를 확인해야 합니다. 또는 smart_admin 저장 프로시저를 호출 하 여 오류에 대 한 세부 정보를 찾을 수 **sp_get_backup_diagnostics 있습니다.**  
  
### <a name="using-agent-notification-for-assessing-backup-status-and-health"></a>백업 상태 확인을 위해 에이전트 알림 사용  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 SQL Server 정책 기반 관리 정책에 따른 알림 메커니즘을 포함합니다.  
  
 **사전**  
  
-   이러한 기능을 사용하려면 데이터베이스 메일이 필요합니다. SQL Server 인스턴스에 대해 DB 메일을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [데이터베이스 메일 구성](../relational-databases/database-mail/configure-database-mail.md)을 참조 하세요.  
  
-   SQL Server 에이전트 경고 시스템 속성은 데이터베이스 메일을 사용하도록 설정되어야 합니다.  
  
 **알림 아키텍처:**  
  
-   **정책 기반 관리:** 백업 상태를 모니터링 하는 두 가지 정책: **스마트 관리 시스템 상태 정책**및 **스마트 관리 사용자 작업 상태 정책**. 스마트 관리 시스템 상태 정책은 SQL 자격 증명 부족 또는 잘못된 SQL 자격 증명과 같은 중요한 오류, 연결 오류를 평가하거나 시스템 상태를 보고합니다. 이 경우 일반적으로 기본 문제를 해결하는 데 수동 작업이 필요합니다. 스마트 관리 사용자 작업 상태 정책은 손상된 백업과 같은 경고를 평가합니다.  이 경우 작업은 필요하지 않지만 이벤트 경고만 필요할 수 있습니다. 이러한 문제는 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 에이전트에 의해 자동으로 처리될 것입니다.  
  
-   **SQL Server 에이전트** 작업: 세 개의 작업 단계를 포함 하는 SQL Server 에이전트 작업을 사용 하 여 알림이 수행 됩니다. 첫 번째 작업 단계에서는 데이터베이스 또는 인스턴스에 대한 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]이 구성되어 있는지 여부를 검색합니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 사용 하도록 설정 되 고 구성 된 경우 두 번째 단계를 실행 합니다. SQL Server 정책 기반 관리 정책을 평가 하 여 상태를 평가 하는 PowerShell cmdlet을 실행 합니다. 오류 또는 경고가 발견 되 면 오류가 발생 하 고 세 번째 단계를 트리거합니다. 세 번째 단계는 오류/경고 보고서와 함께 전자 메일 알림을 보냅니다.  그러나 이 SQL Server 에이전트 작업은 기본적으로 설정되지 않습니다. 전자 메일 알림 작업을 사용 하도록 설정 하려면 **smart_admin. sp_set_backup_parameter** 시스템 저장 프로시저를 사용 합니다.  다음 절차에서 이러한 단계를 자세히 설명합니다.  
  
##### <a name="enabling-email-notification"></a>전자 메일 알림 설정  
  
1.  데이터베이스 메일 아직 구성 되지 않은 경우 [데이터베이스 메일 구성](../relational-databases/database-mail/configure-database-mail.md)에 설명 된 단계를 사용 합니다.  
  
2.  SQL Server 경고 시스템에 대 한 메일 시스템으로 데이터베이스 설정: **SQL Server 에이전트**을 마우스 오른쪽 단추로 클릭 하 고, **경고 시스템**을 선택 하 고, **메일 프로필 사용** 확인란을 선택 하 고, **메일 시스템**으로 **데이터베이스 메일** 을 선택 하 고, 이전에 만든 메일 프로필을 선택 합니다.  
  
3.  쿼리 창에서 다음 쿼리를 실행하고 알림을 보낼 전자 메일 주소를 제공합니다.  
  
    ```sql
    Use msdb  
    Go  
    EXEC smart_admin.sp_set_parameter @parameter_name = 'SSMBackup2WANotificationEmailIds', @parameter_value = '<email address>'
    ```  
  
     이렇게 하면 상태를 수집하고 백업과 함께 오류 또는 문제가 발생하는 경우 알림을 보내는 데 사용되는 SQL Server 에이전트 작업이 생성됩니다.  
  
 다음은 SQL Server 에이전트 작업을 통해 DB 메일을 설정하고 전자 메일 알림을 설정하는 샘플 스크립트입니다.  
  
```sql
-- Prereq: Make sure that SQL Server service runs in a service account that has  
--  access to SMTP Server   
-- set SQL Server service account as domain account   
  
EXEC sp_configure 'show advanced', 1  
RECONFIGURE  
GO  
  
-- Enable DBMail  
EXEC sp_configure 'Database Mail XPs',1  
GO  
RECONFIGURE  
GO  
  
-- Configure DBMail  
DECLARE @emailid NVARCHAR(255)  
-- Note: change this email to your own email id  
SET @emailid = N'emailalias@mycompany.com'  
  
DECLARE @smtpserver NVARCHAR(255)  
SET @smtpserver = N'smtphost.domainname.com'  
  
DECLARE @mailprofile NVARCHAR(255)  
SET @mailprofile = N'my_profile'  
  
EXEC msdb.dbo.sysmail_add_account_sp @account_name=N'myaccount',  
                @email_address = @emailid,  
                @replyto_address = @emailid,  
                @mailserver_name = @smtpserver,  
                @use_default_credentials = 1  
  
EXEC msdb.dbo.sysmail_add_profile_sp @profile_name=@mailprofile  
EXEC msdb.dbo.sysmail_add_profileaccount_sp @profile_name=@mailprofile, @account_name=N'myaccount', @sequence_number=1  
  
-- Set SQL Agent to use DBMail profile  
EXEC msdb.dbo.sp_set_sqlagent_properties @databasemail_profile = @mailprofile  
  
-- Configure Notifications   
EXEC msdb.smart_admin.sp_set_parameter  
@parameter_name = 'SSMBackup2WANotificationEmailIds',  
@parameter_value = @emailid  
  
-- To test is you are receiving notifications  
-- delete few backup files from your storage container, Wait for 15 minutes & see if you get any email notification
```  
  
### <a name="using-powershell-to-setup-custom-health-monitoring"></a>PowerShell을 사용하여 사용자 지정 상태 모니터링  
 **Set-sqlsmartadmin** cmdlet을 사용 하 여 사용자 지정 상태 모니터링을 만들 수 있습니다. 예를 들어 이전 섹션에서 설명한 알림 옵션은 인스턴스 수준에서 구성될 수 있습니다.  여러 SQL Server 인스턴스가 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 사용하도록 구성된 경우 PowerShell cmdlet을 사용하여 모든 인스턴스의 백업 상태를 수집하는 스크립트를 만들 수 있습니다.  
  
 **Set-sqlsmartadmin** cmdlet은 SQL Server 정책 기반 관리 정책에 의해 반환 되는 오류 및 경고를 평가 하 고 롤업 된 상태를 보고 합니다.  기본적으로 이 cmdlet은 시스템 정책을 사용합니다. 사용자 지정 정책을 포함하려면 `-AllowUserPolicies` 매개 변수를 사용합니다.  
  
 다음은 생성된 모든 사용자 정책 및 시스템 정책을 기반으로 하는 오류 및 경고 보고서를 반환하는 샘플 PowerShell 스크립트입니다.  
  
```powershell
$policyResults = Get-SqlSmartAdmin | Test-SqlSmartAdmin -AllowUserPolicies  
$policyResults.PolicyEvaluationDetails | Select Name, Category, Expression, Result, Exception | fl
```  
  
 다음 스크립트는 기본 인스턴스 (`\SQL\COMPUTER\DEFAULT`)에 대 한 오류 및 경고에 대 한 자세한 보고서를 반환 합니다.  
  
```powershell
(Get-SqlSmartAdmin ).EnumHealthStatus()  
```  
  
### <a name="objects-in-msdb-database"></a>MSDB 데이터베이스의 개체  
 기능을 구현하기 위해 설치된 개체가 있습니다. 이러한 개체는 내부 사용을 위해 예약됩니다. 그러나 smart_backup_files 백업 상태를 모니터링 하는 데 유용할 수 있는 시스템 테이블이 하나 있습니다. 백업 유형, 데이터베이스 이름, 첫 번째 및 마지막 lsn, 백업 만료 날짜와 같은 모니터링과 관련 된이 테이블에 저장 된 대부분의 정보는 시스템 함수를 통해 [smart_admin fn_available_backups &#40;transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql)를 통해 제공 됩니다. 백업 파일의 상태를 나타내는 smart_backup_files 테이블의 상태 열은 이 함수를 통해 사용할 수 없습니다. 다음은 시스템 테이블에서 상태를 비롯한 몇 가지 정보를 검색하는 데 사용할 수 있는 예제 쿼리입니다.  
  
```sql
USE msdb  
GO  
SELECT  
 database_name AS [Database Name] ,backup_path AS [Backup Destination and File]  
,[Backup Type] =  
CASE backup_type  
WHEN 1 THEN 'FULL'  
WHEN 2 THEN 'LOG'  
END  
,[Backup Status] =  
CASE [status]  
WHEN 'A' THEN 'Available'  
WHEN 'B' THEN 'Copy In Progress'  
WHEN 'C' THEN 'Corrupted'  
WHEN 'D' THEN 'Deleted'  
WHEN 'F' THEN 'Copy Failed'  
WHEN 'U' THEN 'Unknown'  
END  
,first_lsn AS [First LSN]  
,last_lsn AS [Last LSN]  
,backup_start_date AS [Backup Start Time]  
,backup_finish_date AS [Backup Completion Time]  
,expiration_date AS [Backup Expiry Date/Time]  
FROM  
smart_backup_files;
```  
  
 다음은 반환된 다른 상태에 대한 자세한 설명입니다.  
  
-   **사용 가능-A:** 일반 백업 파일입니다. 백업이 완료 되었으며 Azure storage에서 사용할 수 있는지도 확인 되었습니다.  
  
-   **복사 진행 중-B:** 이 상태는 특히 가용성 그룹 데이터베이스에 대 한 것입니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 백업 로그 체인이 끊어진 것을 검색하는 경우 먼저 그 원인이 될 수 있는 백업을 식별하려고 시도합니다. 백업 파일을 찾을 때 파일을 Azure storage로 복사 하려고 합니다. 복사 프로세스가 진행 중일 때 이 상태를 표시합니다.  
  
-   **복사 실패-F:** 진행 중인 복사와 마찬가지로이는 특정 가용성 그룹 데이터베이스입니다. 복사 프로세스가 실패하면 상태가 F로 표시됩니다.  
  
-   **손상 됨-C:** 가 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 여러 번의 시도 후에도 RESTORE HEADER_ONLY 명령을 수행 하 여 저장소의 백업 파일을 확인할 수 없는 경우이 파일을 손상 된 것으로 표시 합니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 손상된 파일로 인해 백업 체인이 끊어지지 않도록 하기 위해 백업을 예약합니다.  
  
-   **삭제 됨-D:** Azure storage에서 해당 파일을 찾을 수 없습니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 삭제된 파일로 인해 백업 체인이 끊어지는 경우 백업을 예약합니다.  
  
-   **알 수 없음-U:** 이 상태는에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 아직 파일의 존재 여부와 Azure storage의 속성을 확인할 수 없는 것으로 표시 되었습니다. 약 15분 간격으로 다음에 프로세스가 실행될 때 이 상태가 업데이트됩니다.  
