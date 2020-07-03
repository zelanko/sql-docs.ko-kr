---
title: 가용성 그룹에 대해 Azure에 SQL Server 관리 되는 백업 설정 | Microsoft Docs
description: 이 자습서에서는 Always On 가용성 그룹에 참여 하는 데이터베이스에 대 한 Microsoft Azure SQL Server 관리 되는 백업을 구성 하는 방법을 보여 줍니다.
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 0c4553cd-d8e4-4691-963a-4e414cc0f1ba
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ebae9f75ac25698582b7f3e4c78c2fb773bd803e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891990"
---
# <a name="setting-up-sql-server-managed-backup-to-azure-for-availability-groups"></a>가용성 그룹의 Azure에 SQL Server 관리 백업 설정
  이 항목은 AlwaysOn 가용성 그룹에 참여하는 데이터베이스를 위해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 구성하는 방법에 대한 자습서입니다.  
  
## <a name="availability-group-configurations"></a>가용성 그룹 구성  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]는 가용성 그룹 데이터베이스에 대해 지원 됩니다. 복제본이 모두 온-프레미스로 구성 되었는지 아니면 Azure에서 완전히 구성 되었는지 또는 온-프레미스와 하나 이상의 Azure 가상 컴퓨터 간에 하이브리드 구현이 지원 되는지 여부입니다. 그러나 하나 이상의 구현에 대해 다음 사항을 고려해야 할 수 있습니다.  
  
-   로그 백업 빈도: 로그 백업 빈도는 시간 및 로그 증가입니다. 예를 들어 로그 백업은 2시간 안에 사용되는 로그 공간이 5MB 미만인 경우 2시간마다 한 번씩 수행됩니다. 이는 모든 구현(온-프레미스, 클라우드 또는 하이브리드)에 적용됩니다.  
  
-   네트워크 대역폭:이는 하이브리드 클라우드 또는 클라우드 전용 구성의 다른 Azure 지역에서 복제본이 서로 다른 물리적 위치에 있는 구현에 적용 됩니다. 네트워크 대역폭은 보조 복제본의 대기 시간에 영향을 미칠 수 있으며, 보조 복제본이 동기 복제로 설정된 경우 이로 인해 주 복제본에서 로그가 증가할 수 있습니다. 보조 복제본이 동기 복제로 설정된 경우, 보조 복제본이 네트워크 대기 시간 때문에 동기화 상태를 유지하지 못할 수 있으며 이로 인해 보조 복제본으로 장애 조치(failover) 시 데이터 손실이 발생할 수 있습니다.  
  
### <a name="configuring-ss_smartbackup-for-availability-databases"></a>가용성 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 구성  
 **사용 권한:**  
  
-   **ALTER ANY CREDENTIAL** 권한 및 **db_backupoperator** `EXECUTE` **sp_delete_backuphistory**저장 프로시저에 대 한 권한이 있는 db_backupoperator 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
-   Smart_admin에 대 한 **SELECT** 권한이 필요 합니다. **fn_get_current_xevent_settings**함수.  
  
-   `EXECUTE` **Smart_admin sp_get_backup_diagnostics** 저장 프로시저에 대 한 권한이 필요 합니다. 또한 `VIEW SERVER STATE` 권한도 필요한데, 이 권한이 필요한 다른 시스템 개체를 내부적으로 호출하기 때문입니다.  
  
-   `EXECUTE`및 저장 프로시저에 대 한 권한이 필요 `smart_admin.sp_set_instance_backup` `smart_admin.sp_backup_master_switch` 합니다.  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 사용하여 AlwaysOn 가용성 그룹을 설정하는 기본적인 단계는 다음과 같습니다. 자세한 단계별 자습서는 이 항목의 뒷부분에서 설명합니다.  
  
1.  가용성 그룹을 만든 후에는 기본 백업 복제본을 구성합니다. 가용성 그룹에 대한 이 설정은 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]이 백업에 사용할 복제본을 결정하는 데 사용됩니다. 백업 기본 설정을 지정 하는 방법에 대 한 단계별 지침은 [가용성 복제본에 백업 구성 &#40;SQL Server&#41;](availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)를 참조 하세요.  새 AlwaysOn 가용성 그룹을 만드는 경우 [시작 AlwaysOn 가용성 그룹 &#40;SQL Server&#41;](availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md)를 참조 하세요.  
  
2.  보조 복제본에 대한 읽기 전용 연결 액세스를 구성합니다. 읽기 전용 액세스를 구성 하는 방법에 대 한 단계별 지침은 [가용성 복제본에 대 한 읽기 전용 액세스 구성 &#40;SQL Server](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md) 을 참조 하세요&#41;  
  
3.  백업 복제본을 지정합니다. 기본 백업 복제본 설정은 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]이 백업 예약에 사용할 데이터베이스를 결정하는 데 사용됩니다.  현재 복제본이 기본 백업 복제본 인지 여부를 확인 하려면 [fn_hadr_backup_is_preferred_replica &#40;transact-sql&#41;](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql) 함수를 사용 합니다.  
  
4.  각 복제본에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] **sp_set_db_backup** 저장 프로시저를 사용 하 여 데이터베이스에 대 한 구성을 실행 합니다.  
  
     ** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 장애 조치 후의 동작:** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 는 장애 조치 (failover) 이벤트 후에도 계속 작동 하 고 백업 복사본 및 복구 기능을 유지 합니다. 장애 조치(Failover) 후에는 별도의 조치가 필요하지 않습니다.  
  
#### <a name="considerations-and-requirements"></a>고려 사항 및 요구 사항  
 데이터베이스가 AlwaysOn 가용성 그룹에 참여하도록 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 구성하려면 특별한 고려 사항 및 요구 사항이 필요합니다. 이러한 고려 사항 및 요구 사항은 다음과 같습니다.  
  
-   [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 구성 설정은 동일한 가용성 그룹에 참여하는 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 노드의 모든 데이터베이스에 대해 동일해야 합니다. 이를 위해서는 데이터베이스 수준에서 주 데이터베이스와 모든 복제본에 대해 동일한 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 구성 설정을 사용하거나 가용성 그룹에 참여하는 모든 노드에 대해 기본 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 설정을 동일하게 설정하면 됩니다. 데이터베이스 수준에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 구성하면 설정을 데이터베이스에 격리할 수 있으며 기본 설정을 변경하면 인스턴스의 다른 모든 데이터베이스에 영향을 미치기 때문에 데이터베이스에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 설정하는 것이 좋습니다.  
  
-   백업 복제본을 지정합니다. 기본 백업 복제본 설정은 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]에서 백업을 예약하는 데 사용됩니다. 현재 복제본이 기본 백업 복제본 인지 여부를 확인 하려면 [fn_hadr_backup_is_preferred_replica &#40;transact-sql&#41;](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql) 함수를 사용 합니다.  
  
-   보조 복제본이 기본 설정 복제본으로 구성된 경우 최소한 읽기 전용 연결 액세스를 보유하도록 구성해야 합니다. 보조 데이터베이스에 대한 연결 액세스가 없는 가용성 그룹은 지원되지 않습니다.  자세한 내용은 [&#40;SQL Server&#41;가용성 복제본에 대 한 읽기 전용 액세스 구성 ](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)을 참조 하세요.  
  
-   가용성 그룹을 구성한 후 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 구성하면 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]이 기존의 모든 기본 백업을 스토리지 컨테이너에 복사하려고 합니다.  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]에서 기존 백업을 찾거나 액세스할 수 없으면 전체 데이터베이스 백업이 예약됩니다. 이 작업은 특히 가용성 그룹 데이터베이스에 대한 백업 작업을 최적화하기 위해 수행됩니다.  
  
-   새 가용성 데이터베이스를 만들 때 인스턴스 수준 설정을 데이터베이스에 적용 하지 않으려는 경우 인스턴스 수준 설정을 사용 하지 않도록 설정할 수 있습니다.  
  
-   암호화를 사용하는 경우 모든 복제본에서 동일한 인증서를 사용합니다. 이렇게 하면 다른 복제본으로 장애 조치(failover)하거나 복원하는 경우 중단 없이 연속적으로 백업 작업을 수행하는 데 도움이 됩니다.  
  
#### <a name="enable-and-configure-ss_smartbackup-for-an-availability-database"></a>가용성 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 설정 및 구성  
 이 자습서에서는 Node1 및 Node2 컴퓨터에서 데이터베이스(AGTestDB)에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 설정 및 구성하고 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 상태에 대한 모니터링을 설정하는 단계에 대해 설명합니다.  
  
1.  **Azure 저장소 계정 만들기:** 백업은 Azure Blob 저장소 서비스에 저장 됩니다. 아직 없는 경우 먼저 Azure storage 계정을 만들어야 합니다. 자세한 내용은 [Azure Storage 계정 만들기](https://www.windowsazure.com/manage/services/storage/how-to-create-a-storage-account/)를 참조 하세요. 스토리지 계정 이름, 액세스 키 및 스토리지 계정의 URL을 기록합니다. 스토리지 계정 이름 및 액세스 키 정보는 SQL 자격 증명을 만드는 데 사용됩니다. SQL 자격 증명은 백업 작업 중 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]에서 스토리지 계정을 인증하는 데 사용됩니다.  
  
2.  **SQL 자격 증명 만들기:** 저장소 계정의 이름을 Id로 사용 하 고 저장소 액세스 키를 암호로 사용 하 여 SQL 자격 증명을 만듭니다.  
  
3.  **SQL Server 에이전트 서비스가 시작되고 실행 중인지 확인:** 현재 SQL Server 에이전트가 실행되지 않고 있으면 시작합니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 실행하여 백업 작업을 수행하려면 SQL Server 에이전트가 필요합니다.  SQL 에이전트가 자동으로 실행되어 백업 작업이 정기적으로 발생하도록 설정할 수 있습니다.  
  
4.  **보존 기간 결정:** 백업 파일에 대해 원하는 보존 기간을 결정 합니다. 보존 기간은 일 단위로 지정되며 1-30일의 범위로 설정할 수 있습니다. 보존 기간은 데이터베이스의 복구 가능 시간대를 결정합니다.  
  
5.  **백업 하는 동안 암호화에 사용할 인증서 또는 비대칭 키를 만듭니다.** 첫 번째 노드 Node1에서 인증서를 만든 다음 [백업 인증서 &#40;](/sql/t-sql/statements/backup-certificate-transact-sql)사용 하 여 파일로 내보냅니다. transact-sql&#41;. Node1에서 내보낸 파일을 사용하여 Node2에서 인증서를 만듭니다. 파일에서 인증서를 만드는 방법에 대 한 자세한 내용은 [CREATE certificate &#40;transact-sql&#41;](/sql/t-sql/statements/create-certificate-transact-sql)의 예제를 참조 하세요.  
  
6.  ** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] Node1에서 AGTestDB에 대해 설정 및 구성:** SQL Server Management Studio 시작 하 고 가용성 데이터베이스가 설치 된 노드 1의 인스턴스에 연결 합니다. 필요에 따라 데이터베이스 이름, 스토리지 URL, SQL 자격 증명 및 보존 기간 값을 수정한 후 쿼리 창에서 다음 문을 실행합니다.  
  
    ```sql  
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
  
     암호화에 대 한 인증서를 만드는 방법에 대 한 자세한 내용은 [암호화 된 백업 만들기](../relational-databases/backup-restore/create-an-encrypted-backup.md)의 **백업 인증서 만들기** 단계를 참조 하세요.  
  
7.  ** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 노드 2의 AGTestDB에 대해 설정 및 구성:** SQL Server Management Studio을 시작 하 고 가용성 데이터베이스가 설치 된 노드 2의 인스턴스에 연결 합니다. 필요에 따라 데이터베이스 이름, 스토리지 URL, SQL 자격 증명 및 보존 기간 값을 수정한 후 쿼리 창에서 다음 문을 실행합니다.  
  
    ```sql  
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
  
8.  **확장 이벤트 기본 구성 검토:**  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]에서 백업을 예약 하는 데 사용 하는 복제본에서 다음 transact-sql 문을 실행 하 여 확장 이벤트 구성을 검토 합니다. 이는 데이터베이스가 속한 가용성 그룹에 대한 기본 백업 복제본 설정입니다.  
  
    ```sql  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings(); 
    ```  
  
     Admin, Operational 및 Analytical 채널 이벤트가 기본적으로 설정되어 있고 해제할 수 없습니다. 수동 작업이 필요한 이벤트를 모니터링하기에 충분해야 합니다.  디버그 이벤트를 설정할 수 있지만 이러한 채널에는 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]에서 문제를 발견 및 해결하는 데 사용하는 정보와 디버그 이벤트가 포함되어 있습니다. 자세한 내용은 [Azure에 대 한 관리 되는 백업 SQL Server 모니터링](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)을 참조 하세요.  
  
9. **Health 상태 알림 사용 및 구성:** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]에는 주의가 필요할 수 있는 오류나 경고의 메일 알림을 보내는 에이전트 작업을 만드는 저장 프로시저가 있습니다.  이러한 알림을 수신하려면 SQL Server 에이전트 작업을 만드는 저장 프로시저를 실행해야 합니다. 전자 메일 알림을 사용 및 구성하는 단계는 다음과 같습니다.  
  
    1.  인스턴스에 데이터베이스 메일이 설정되지 않은 경우 데이터베이스 메일을 설정합니다. 자세한 내용은 [Configure Database Mail](../relational-databases/database-mail/configure-database-mail.md)을 참조하세요.  
  
    2.  데이터베이스 메일을 사용하도록 SQL Server 에이전트 알림을 구성합니다. 자세한 내용은 [Configure SQL Server Agent Mail to Use Database Mail](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)을 참조하세요.  
  
    3.  **백업 오류 및 경고를 수신하도록 이메일 알림 설정:** 쿼리 창에서 다음 Transact-SQL 문을 실행합니다.  
  
        ```sql  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email>'  
        ```  
  
         자세한 내용 및 전체 샘플 스크립트는 [Azure에 대 한 관리 되는 백업 SQL Server 모니터링](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)을 참조 하세요.  
  
10. **Azure Storage 계정에서 백업 파일 보기:** SQL Server Management Studio 또는 Azure 관리 포털에서 저장소 계정에 연결 합니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 사용하도록 구성한 데이터베이스를 호스팅하는 SQL Server 인스턴스에 대한 컨테이너가 표시됩니다. 데이터베이스에 대한 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 설정한 후 15분 이내에 데이터베이스 및 로그 백업도 표시됩니다.  
  
11. **상태 모니터링:**  이전에 구성한 메일 알림을 통해 모니터링하거나 기록된 이벤트를 적극적으로 모니터링할 수 있습니다. 다음은 이벤트를 표시하는 데 사용하는 예제 Transact-SQL 문입니다.  
  
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
    event varchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
    ```  
  
    ```sql  
    -- to enable debug events  
    Use msdb;  
    Go  
    EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
    ```  
  
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
  
 이 섹션에서는 데이터베이스에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 처음 구성하는 단계에 대해 설명합니다. 동일한 시스템 저장 프로시저 smart_admin를 사용 하 여 기존 구성을 수정할 수 있습니다 **. sp_set_db_backup** 하 고 새 값을 제공 합니다. 자세한 내용은 [Azure에 대 한 관리 되는 백업-보존 및 저장소 설정 SQL Server](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)을 참조 하세요.  
  
### <a name="considerations-when-removing-a-database-from-alwayson-availability-group-configuration"></a>AlwaysOn 가용성 그룹 구성에서 데이터베이스를 제거할 때의 고려 사항  
 AlwaysOn 가용성 그룹 구성에서 데이터베이스를 제거 하 고 현재 독립 실행형 데이터베이스인 경우 smart_admin를 사용 하 여 백업을 수행 하는 것이 좋습니다 [. sp_backup_on_demand &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql). 이런 식으로 데이터베이스 백업을 만들면 새로운 백업 체인이 설정되고 파일이 인스턴스 관련 컨테이너에 배치됩니다. 이는 데이터베이스가 가용성 그룹에 속한 경우 백업이 가용성 컨테이너에 저장되는 것과 대조적입니다.  
  
> [!WARNING]  
>  이 시나리오에서 가용성 그룹 상태가 변경되기 이전의 백업에서 데이터베이스를 복구하는 것은 보장되지 않습니다.  
  
