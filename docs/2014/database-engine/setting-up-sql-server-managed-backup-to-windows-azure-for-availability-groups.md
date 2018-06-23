---
title: 가용성 그룹에 대 한 SQL Server Managed Backup to Windows Azure 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0c4553cd-d8e4-4691-963a-4e414cc0f1ba
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8a367b7835b08c9a5b2b7226b8f3e4d127235487
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181871"
---
# <a name="setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups"></a>가용성 그룹의 Microsoft Azure에 대한 SQL Server 관리되는 백업 설정
  이 항목은 AlwaysOn 가용성 그룹에 참여하는 데이터베이스를 위해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 구성하는 방법에 대한 자습서입니다.  
  
## <a name="availability-group-configurations"></a>가용성 그룹 구성  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 모든 복제본이 구성된 위치가 온-프레미스이든, Windows Azure이든, 온-프레미스와 하나 이상의 Windows Azure 가상 컴퓨터 간의 하이브리드 구현이든 간에 가용성 그룹 데이터베이스에 대해 지원됩니다. 그러나 하나 이상의 구현에 대해 다음 사항을 고려해야 할 수 있습니다.  
  
-   로그 백업 빈도: 로그 백업 빈도 시간과 로그 증가 합니다. 예를 들어 로그 백업은 2시간 안에 사용되는 로그 공간이 5MB 미만인 경우 2시간마다 한 번씩 수행됩니다. 이는 모든 구현(온-프레미스, 클라우드 또는 하이브리드)에 적용됩니다.  
  
-   네트워크 대역폭:이 복제본 위치 서로 다른 물리적 위치에 같은 하이브리드 클라우드 나 클라우드 전용 구성에서 서로 다른 Windows Azure 지역 구현에 적용 합니다. 네트워크 대역폭은 보조 복제본의 대기 시간에 영향을 미칠 수 있으며, 보조 복제본이 동기 복제로 설정된 경우 이로 인해 주 복제본에서 로그가 증가할 수 있습니다. 보조 복제본이 동기 복제로 설정된 경우, 보조 복제본이 네트워크 대기 시간 때문에 동기화 상태를 유지하지 못할 수 있으며 이로 인해 보조 복제본으로 장애 조치(failover) 시 데이터 손실이 발생할 수 있습니다.  
  
### <a name="configuring-includesssmartbackupincludesss-smartbackup-mdmd-for-availability-databases"></a>가용성 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 구성  
 **사용 권한:**  
  
-   멤버 자격이 필요 **db_backupoperator** 와 데이터베이스 역할 **ALTER ANY CREDENTIAL** 사용 권한 및 `EXECUTE` 에 대 한 권한을 **sp_delete_backuphistory**저장 프로시저입니다.  
  
-   필요한 **선택** 에 대 한 권한을 **smart_admin.fn_get_current_xevent_settings**함수입니다.  
  
-   필요한 `EXECUTE` 에 대 한 권한을 **smart_admin.sp_get_backup_diagnostics** 저장 프로시저입니다. 또한 `VIEW SERVER STATE` 권한도 필요한데, 이 권한이 필요한 다른 시스템 개체를 내부적으로 호출하기 때문입니다.  
  
-   필요한 `EXECUTE` 에 대 한 권한을 `smart_admin.sp_set_instance_backup` 및 `smart_admin.sp_backup_master_switch` 저장 프로시저입니다.  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 사용하여 AlwaysOn 가용성 그룹을 설정하는 기본적인 단계는 다음과 같습니다. 자세한 단계별 자습서는 이 항목의 뒷부분에서 설명합니다.  
  
1.  가용성 그룹을 만든 후에는 기본 백업 복제본을 구성합니다. 가용성 그룹에 대한 이 설정은 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]이 백업에 사용할 복제본을 결정하는 데 사용됩니다. 백업 기본 설정을 설정 하는 방법에 대 한 단계별 지침을 참조 하십시오. [가용성 복제본에 백업 구성 &#40;SQL Server&#41;](availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)합니다.  새 AlwaysOn 가용성 그룹을 만드는 경우 참조 [AlwaysOn 가용성 그룹 시작 &#40;SQL Server&#41;](availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md)합니다.  
  
2.  보조 복제본에 대한 읽기 전용 연결 액세스를 구성합니다. 읽기 전용 액세스를 구성 하는 방법에 대 한 단계별 지침을 참조 [가용성 복제본에 읽기 전용 액세스 구성 &#40;SQL Server&#41;](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
3.  백업 복제본을 지정합니다. 기본 백업 복제본 설정은 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]이 백업 예약에 사용할 데이터베이스를 결정하는 데 사용됩니다.  현재 복제본이 선호 백업 복제본 인지 확인 하려면는 [sys.fn_hadr_backup_is_preferred_replica &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql) 함수입니다.  
  
4.  실행 하는 각 복제본에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 사용 하 여 데이터베이스에 대 한 구성에서 **스마트 admin.sp_set_db_backup** 저장 프로시저입니다.  
  
     **[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 장애 조치 후 동작:** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 계속 작동 하 고 장애 조치 이벤트가 발생 한 후 백업 복사본 및 복구 기능을 유지 됩니다. 장애 조치(Failover) 후에는 별도의 조치가 필요하지 않습니다.  
  
#### <a name="considerations-and-requirements"></a>고려 사항 및 요구 사항  
 데이터베이스가 AlwaysOn 가용성 그룹에 참여하도록 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 구성하려면 특별한 고려 사항 및 요구 사항이 필요합니다. 이러한 고려 사항 및 요구 사항은 다음과 같습니다.  
  
-   [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 구성 설정은 동일한 가용성 그룹에 참여하는 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 노드의 모든 데이터베이스에 대해 동일해야 합니다. 이를 위해서는 데이터베이스 수준에서 주 데이터베이스와 모든 복제본에 대해 동일한 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 구성 설정을 사용하거나 가용성 그룹에 참여하는 모든 노드에 대해 기본 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 설정을 동일하게 설정하면 됩니다. 데이터베이스 수준에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 구성하면 설정을 데이터베이스에 격리할 수 있으며 기본 설정을 변경하면 인스턴스의 다른 모든 데이터베이스에 영향을 미치기 때문에 데이터베이스에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 설정하는 것이 좋습니다.  
  
-   백업 복제본을 지정합니다. 기본 백업 복제본 설정은 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]에서 백업을 예약하는 데 사용됩니다. 현재 복제본이 선호 백업 복제본 인지 확인 하려면는 [sys.fn_hadr_backup_is_preferred_replica &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql) 함수입니다.  
  
-   보조 복제본이 기본 설정 복제본으로 구성된 경우 최소한 읽기 전용 연결 액세스를 보유하도록 구성해야 합니다. 보조 데이터베이스에 대한 연결 액세스가 없는 가용성 그룹은 지원되지 않습니다.  자세한 내용은 [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)가 있어야 합니다.  
  
-   가용성 그룹을 구성한 후 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 구성하면 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]이 기존의 모든 기본 백업을 저장소 컨테이너에 복사하려고 합니다.  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]에서 기존 백업을 찾거나 액세스할 수 없으면 전체 데이터베이스 백업이 예약됩니다. 이 작업은 특히 가용성 그룹 데이터베이스에 대한 백업 작업을 최적화하기 위해 수행됩니다.  
  
-   새로운 가용성 데이터베이스를 만드는 경우 인스턴스 수준 설정을 데이터베이스에 적용하지 않으려면 인스턴스 수준 설정을 해제하는 것을 고려할 수 있습니다.  
  
-   암호화를 사용하는 경우 모든 복제본에서 동일한 인증서를 사용합니다. 이렇게 하면 다른 복제본으로 장애 조치(failover)하거나 복원하는 경우 중단 없이 연속적으로 백업 작업을 수행하는 데 도움이 됩니다.  
  
#### <a name="enable-and-configure-includesssmartbackupincludesss-smartbackup-mdmd-for-an-availability-database"></a>가용성 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 설정 및 구성  
 이 자습서에서는 Node1 및 Node2 컴퓨터에서 데이터베이스(AGTestDB)에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 설정 및 구성하고 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 상태에 대한 모니터링을 설정하는 단계에 대해 설명합니다.  
  
1.  **Windows Azure 저장소 계정 만들기:** 백업은 Windows Azure Blob 저장소 서비스에 저장 됩니다. Windows Azure 저장소 계정이 없는 경우 먼저 계정을 만들어야 합니다. 자세한 내용은 참조 [는 Windows Azure 저장소 계정을 만드는](http://www.windowsazure.com/manage/services/storage/how-to-create-a-storage-account/)합니다. 저장소 계정 이름, 액세스 키 및 저장소 계정의 URL을 기록합니다. 저장소 계정 이름 및 액세스 키 정보는 SQL 자격 증명을 만드는 데 사용됩니다. SQL 자격 증명은 백업 작업 중 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]에서 저장소 계정을 인증하는 데 사용됩니다.  
  
2.  **SQL 자격 증명 만들기:** 암호로 Id 및 저장소 액세스 키로 저장소 계정의 이름을 사용 하 여 SQL 자격 증명을 만듭니다.  
  
3.  **SQL Server 에이전트 서비스가 시작되고 실행 중인지 확인:** SQL 서버를 실행합니다(현재 실행되고 있지 않은 경우). [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 실행하여 백업 작업을 수행하려면 SQL Server 에이전트가 필요합니다.  SQL 에이전트가 자동으로 실행되어 백업 작업이 정기적으로 발생하도록 설정할 수 있습니다.  
  
4.  **보존 기간 결정:** 백업 파일에 대해 원하는 보존 기간을 결정 합니다. 보존 기간은 일 단위로 지정되며 1-30일의 범위로 설정할 수 있습니다. 보존 기간은 데이터베이스의 복구 가능 시간대를 결정합니다.  
  
5.  **백업 중에 암호화에 대 한 사용 가능한 최대 인증서 또는 비대칭 키 만들기:** Node1, 첫 번째 노드에서 인증서를 만들고 다음 사용 하 여 파일을 내보낼 [백업 인증서 &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/backup-certificate-transact-sql)... Node1에서 내보낸 파일을 사용하여 Node2에서 인증서를 만듭니다. 파일에서 인증서를 만드는 방법에 대 한 자세한 내용은 예제를 참조 [CREATE CERTIFICATE &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)합니다.  
  
6.  **설정 및 구성 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 에 노드 1의 AGTestDB에 대해:** SQL Server Management Studio를 시작 하 고 가용성 데이터베이스가 설치 된 위치 노드 1의 인스턴스에 연결 합니다. 필요에 따라 데이터베이스 이름, 저장소 URL, SQL 자격 증명 및 보존 기간 값을 수정한 후 쿼리 창에서 다음 문을 실행합니다.  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='AGTestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     암호화에 대 한 인증서를 만드는 방법에 대 한 자세한 내용은 참조는 **백업 인증서 만들기** 단계 [Create an Encrypted Backup](../relational-databases/backup-restore/create-an-encrypted-backup.md)합니다.  
  
7.  **설정 및 구성 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 노드 2에서의 AGTestDB에 대 한:** SQL Server Management Studio를 시작 하 고 가용성 데이터베이스가 설치 된 위치 노드 2의 인스턴스에 연결 합니다. 필요에 따라 데이터베이스 이름, 저장소 URL, SQL 자격 증명 및 보존 기간 값을 수정한 후 쿼리 창에서 다음 문을 실행합니다.  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='AGTestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 이 설정되었습니다. 데이터베이스에서 백업 작업이 실행을 시작하려면 최대 15분이 필요합니다. 백업은 기본 백업 복제본에서 실행됩니다.  
  
8.  **확장 이벤트 기본 구성 검토:** 복제본에 대해 다음 TRANSACT-SQL 문을 실행 하 여 확장 이벤트 구성을 검토 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 하는 백업을 예약 하는 데 사용 합니다. 이는 데이터베이스가 속한 가용성 그룹에 대한 기본 백업 복제본 설정입니다.  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     Admin, Operational 및 Analytical 채널 이벤트가 기본적으로 설정되어 있고 해제할 수 없습니다. 수동 작업이 필요한 이벤트를 모니터링하기에 충분해야 합니다.  디버그 이벤트를 설정할 수 있지만 이러한 채널에는 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]에서 문제를 발견 및 해결하는 데 사용하는 정보와 디버그 이벤트가 포함되어 있습니다. 자세한 내용은 참조 [모니터 SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)합니다.  
  
9. **Enable and Configure Notification for Health Status:** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] has a stored procedure that creates an agent job to send out e-mail notifications of errors or warnings that may require attention.  이러한 알림을 수신하려면 SQL Server 에이전트 작업을 만드는 저장 프로시저를 실행해야 합니다. 전자 메일 알림을 사용 및 구성하는 단계는 다음과 같습니다.  
  
    1.  인스턴스에 데이터베이스 메일이 설정되지 않은 경우 데이터베이스 메일을 설정합니다. 자세한 내용은 [Configure Database Mail](../relational-databases/database-mail/configure-database-mail.md)을 참조하세요.  
  
    2.  데이터베이스 메일을 사용하도록 SQL Server 에이전트 알림을 구성합니다. 자세한 내용은 [Configure SQL Server Agent Mail to Use Database Mail](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)을 참조하세요.  
  
    3.  **백업 오류 및 경고를 수신하도록 메일 알림 설정:** 쿼리 창에서 다음 Transact-SQL 문을 실행합니다.  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email>'  
  
        ```  
  
         자세한 내용과 전체 예제 스크립트에 대 한 참조 [모니터 SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)합니다.  
  
10. **Windows Azure 저장소 계정에서 백업 파일 보기:** SQL Server Management Studio 또는 Azure 관리 포털에서 저장소 계정에 연결 합니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 사용하도록 구성한 데이터베이스를 호스팅하는 SQL Server 인스턴스에 대한 컨테이너가 표시됩니다. 데이터베이스에 대한 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 설정한 후 15분 이내에 데이터베이스 및 로그 백업도 표시됩니다.  
  
11. **상태 모니터링:**  이전에 구성한 메일 알림을 통해 모니터링하거나 기록된 이벤트를 능동적으로 모니터링할 수 있습니다. 다음은 이벤트를 표시하는 데 사용하는 예제 Transact-SQL 문입니다.  
  
    ```  
    --  view all admin events  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event varchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 이 섹션에서는 데이터베이스에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 처음 구성하는 단계에 대해 설명합니다. 동일한 시스템 저장 프로시저를 사용 하 여 기존 구성을 수정할 수 있습니다 **smart_admin.sp_set_db_backup** 새 값을 지정 합니다. 자세한 내용은 참조 [SQL Server Managed Backup to Windows Azure-보존 및 저장소 설정](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)합니다.  
  
### <a name="considerations-when-removing-a-database-from-alwayson-availability-group-configuration"></a>AlwaysOn 가용성 그룹 구성에서 데이터베이스를 제거할 때의 고려 사항  
 데이터베이스가 AlwaysOn 가용성 그룹 구성에서 제거 되어 독립 실행형 데이터베이스가 경우 사용 하 여 백업을 수행 하는 것이 좋습니다 [smart_admin.sp_backup_on_demand &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)합니다. 이런 식으로 데이터베이스 백업을 만들면 새로운 백업 체인이 설정되고 파일이 인스턴스 관련 컨테이너에 배치됩니다. 이는 데이터베이스가 가용성 그룹에 속한 경우 백업이 가용성 컨테이너에 저장되는 것과 대조적입니다.  
  
> [!WARNING]  
>  이 시나리오에서 가용성 그룹 상태가 변경되기 이전의 백업에서 데이터베이스를 복구하는 것은 보장되지 않습니다.  
  
  
