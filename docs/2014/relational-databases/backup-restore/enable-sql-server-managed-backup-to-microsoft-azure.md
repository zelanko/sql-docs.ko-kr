---
title: Azure에 대 한 SQL Server Managed Backup 설정 | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b69439226b55965e37f24f2131c77340ae833590
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154719"
---
# <a name="setting-up-sql-server-managed-backup-to-azure"></a>Azure에 대 한 SQL Server Managed Backup 설정
  이 항목에는 다음 두 자습서가 포함됩니다.  
  
 데이터베이스 수준에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 설정, 전자 메일 알림 설정 및 백업 작업 모니터링  
  
 인스턴스 수준에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 설정, 전자 메일 알림 설정 및 백업 작업 모니터링  
  
 가용성 그룹을 설정 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 하는 방법에 대 한 자습서는 [가용성 그룹에 대 한 Microsoft Azure SQL Server Managed Backup 설정](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)을 참조 하세요.  
  
## <a name="setting-up-includess_smartbackupincludesss-smartbackup-mdmd"></a>[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 설정  
  
### <a name="enable-and-configure-includess_smartbackupincludesss-smartbackup-mdmd-for-a-database"></a>데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 설정 및 구성  
 이 자습서는 데이터베이스(TestDB)에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 설정 및 구성하고 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 상태 모니터링을 설정하는 데 필요한 단계에 대해 설명합니다.  
  
 **사용 권한:**  
  
-   **ALTER ANY CREDENTIAL** 권한 및 `EXECUTE` **sp_delete_backuphistory**저장 프로시저에 대 한 권한이 있는 **db_backupoperator** 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
-   **Smart_admin. fn_get_current_xevent_settings**함수에 대 한 **SELECT** 권한이 필요 합니다.  
  
-   Sp_get_backup_diagnostics `EXECUTE` 저장 프로시저에 대 한 권한이 필요 **smart_admin.** 또한 `VIEW SERVER STATE` 권한도 필요한데, 이 권한이 필요한 다른 시스템 개체를 내부적으로 호출하기 때문입니다.  
  
-   `smart_admin.sp_set_instance_backup` `EXECUTE` 및`smart_admin.sp_backup_master_switch` 저장 프로시저에 대 한 권한이 필요 합니다.  


1.  **Microsoft Azure 저장소 계정 만들기:** 백업은 Microsoft Azure storage 서비스에 저장 됩니다. 계정이 아직 없는 경우 먼저 Microsoft Azure storage 계정을 만들어야 합니다.
    - SQL Server 2014는 블록 및 추가 blob과 다른 페이지 blob을 사용 합니다. 따라서 blob 계정이 아닌 범용 계정을 만들어야 합니다. 자세한 내용은 [Azure storage 계정 정보](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)를 참조 하세요.
    - 스토리지 계정 이름 및 액세스 키를 적어 둡니다. 스토리지 계정 이름 및 액세스 키 정보는 SQL 자격 증명을 만드는 데 사용됩니다. SQL 자격 증명은 스토리지 계정 인증에 사용됩니다.  
 
2.  **SQL 자격 증명 만들기:** 저장소 계정의 이름을 Id로 사용 하 고 저장소 액세스 키를 암호로 사용 하 여 SQL 자격 증명을 만듭니다.  
  
3.  **SQL Server 에이전트 서비스가 시작되고 실행 중인지 확인:**  현재 SQL Server 에이전트가 실행되지 않고 있으면 시작합니다.  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 실행하여 백업 작업을 수행하려면 SQL Server 에이전트가 필요합니다.  SQL Server 에이전트가 자동으로 실행되어 백업 작업이 정기적으로 발생하도록 설정할 수 있습니다.  
  
4.  **보존 기간 결정:** 백업 파일의 보존 기간을 결정합니다. 보존 기간은 일 단위로 지정되며 1-30일의 범위로 설정할 수 있습니다.  
  
5.  **설정 및 구성 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:** SQL Server Management Studio를 시작 하 고 데이터베이스가 설치 된 인스턴스에 연결 합니다. 요구 사항에 따라 데이터베이스 이름, SQL 자격 증명, 보존 기간 및 암호화 옵션의 값을 수정한 후 쿼리 창에서 다음 문을 실행합니다.  
  
     암호화에 대 한 인증서를 만드는 방법에 대 한 자세한 내용은 [암호화 된 백업 만들기](create-an-encrypted-backup.md)의 **백업 인증서 만들기** 단계를 참조 하세요.  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='TestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 설정되었습니다. 데이터베이스에서 백업 작업이 실행을 시작하려면 최대 15분이 필요합니다.  
  
6.  **확장 이벤트 기본 구성 검토:** 다음 Transact-SQL 문을 실행하여 확장 이벤트 설정을 검토합니다.  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     Admin, Operational 및 Analytical 채널 이벤트가 기본적으로 설정되어 있고 해제할 수 없습니다. 수동 작업이 필요한 이벤트를 모니터링하기에 충분해야 합니다.  디버그 이벤트를 설정할 수 있지만 디버그 채널에는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에서 문제를 발견 및 해결하는 데 사용하는 정보와 디버그 이벤트가 포함됩니다. 자세한 내용은 [Microsoft Azure에 대 한 관리 되는 백업 SQL Server 모니터링](sql-server-managed-backup-to-microsoft-azure.md)을 참조 하세요.  
  
7.  **상태 알림 사용 및 구성:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에는 주의가 요구될 수 있는 오류나 경고의 메일 알림을 보내는 에이전트 작업을 만드는 저장 프로시저가 있습니다. 전자 메일 알림을 사용 및 구성하는 단계는 다음과 같습니다.  
  
    1.  인스턴스에 데이터베이스 메일이 설정되지 않은 경우 데이터베이스 메일을 설정합니다. 자세한 내용은 [Configure Database Mail](../database-mail/configure-database-mail.md)을 참조하세요.  
  
    2.  데이터베이스 메일을 사용하도록 SQL Server 에이전트 알림을 구성합니다. 자세한 내용은 [Configure SQL Server Agent Mail to Use Database Mail](../database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)을 참조하세요.  
  
    3.  **백업 오류 및 경고를 수신하도록 이메일 알림 설정:** 쿼리 창에서 다음 Transact-SQL 문을 실행합니다.  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
  
        ```  
  
         자세한 내용 및 전체 샘플 스크립트는 [Microsoft Azure에 대 한 관리 되는 백업 SQL Server 모니터링](sql-server-managed-backup-to-microsoft-azure.md)을 참조 하세요.  
  
8.  **Microsoft Azure Storage 계정의 백업 파일 보기:** SQL Server Management Studio 또는 Azure 관리 포털에서 스토리지 계정에 연결합니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하도록 구성한 데이터베이스를 호스팅하는 SQL Server 인스턴스에 대한 컨테이너가 표시됩니다. 데이터베이스에 대한 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 설정한 후 15분 이내에 데이터베이스 및 로그 백업도 표시됩니다.  
  
9. **상태 모니터링:**  이전에 구성한 메일 알림을 통해 모니터링하거나 기록된 이벤트를 적극적으로 모니터링할 수 있습니다. 다음은 이벤트를 표시하는 데 사용하는 예제 Transact-SQL 문입니다.  
  
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
    event nvarchar (512),  
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
  
 이 섹션에서는 데이터베이스에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 처음 구성하는 단계에 대해 설명합니다. 동일한 시스템 저장 프로시저 **smart_admin** 를 사용 하 여 기존 구성을 수정 하 고 새 값을 제공할 수 있습니다. 자세한 내용은 [Microsoft Azure SQL Server 관리 되는 백업-보존 및 저장소 설정](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)을 참조 하세요.  
  
### <a name="enable-includess_smartbackupincludesss-smartbackup-mdmd-for-the-instance-with-default-settings"></a>기본 설정을 사용하여 인스턴스에 대한 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 설정  
 이 자습서에서는 ' MyInstance [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] \\' 인스턴스를 사용 하도록 설정 하 고 구성 하는 단계를 설명 합니다. 여기에는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 상태 모니터링을 설정하는 단계가 포함되어 있습니다.  
  
 **사용 권한:**  
  
-   **ALTER ANY CREDENTIAL** 권한 및 `EXECUTE` **sp_delete_backuphistory**저장 프로시저에 대 한 권한이 있는 **db_backupoperator** 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
-   **Smart_admin. fn_get_current_xevent_settings**함수에 대 한 **SELECT** 권한이 필요 합니다.  
  
-   Sp_get_backup_diagnostics `EXECUTE` 저장 프로시저에 대 한 권한이 필요 **smart_admin.** 또한 `VIEW SERVER STATE` 권한도 필요한데, 이 권한이 필요한 다른 시스템 개체를 내부적으로 호출하기 때문입니다.  


1.  **Microsoft Azure 저장소 계정 만들기:** 백업은 Microsoft Azure storage 서비스에 저장 됩니다. 계정이 아직 없는 경우 먼저 Microsoft Azure storage 계정을 만들어야 합니다.
    - SQL Server 2014는 블록 및 추가 blob과 다른 페이지 blob을 사용 합니다. 따라서 blob 계정이 아닌 범용 계정을 만들어야 합니다. 자세한 내용은 [Azure storage 계정 정보](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)를 참조 하세요.
    - 스토리지 계정 이름 및 액세스 키를 적어 둡니다. 스토리지 계정 이름 및 액세스 키 정보는 SQL 자격 증명을 만드는 데 사용됩니다. SQL 자격 증명은 스토리지 계정 인증에 사용됩니다.  
  
2.  **SQL 자격 증명 만들기:** 저장소 계정의 이름을 Id로 사용 하 고 저장소 액세스 키를 암호로 사용 하 여 SQL 자격 증명을 만듭니다.  
  
3.  **SQL Server 에이전트 서비스가 시작되고 실행 중인지 확인:** 현재 SQL Server 에이전트가 실행되지 않고 있으면 시작합니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 실행하여 백업 작업을 수행하려면 SQL Server 에이전트가 필요합니다.  SQL Server 에이전트가 자동으로 실행되어 백업 작업이 정기적으로 발생하도록 설정할 수 있습니다.  
  
4.  **보존 기간 결정:** 백업 파일의 보존 기간을 결정합니다. 보존 기간은 일 단위로 지정되며 1-30일의 범위로 설정할 수 있습니다. 기본값을 사용하여 인스턴스 수준에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 설정되면 이후 만들어진 모든 새 데이터베이스는 해당 설정을 상속합니다. 전체 또는 대량 로그 복구 모델로 설정된 데이터베이스만 지원되고 자동으로 구성됩니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성을 원하지 않는 경우 언제든지 특정 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 해제할 수 있습니다. 또한 데이터베이스 수준에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 구성하여 특정 데이터베이스에 대한 구성을 변경할 수 있습니다.  
  
5.  **설정 및 구성 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:** SQL Server Management Studio를 시작 하 고 SQL Server 인스턴스에 연결 합니다. 요구 사항에 따라 데이터베이스 이름, SQL 자격 증명, 보존 기간 및 암호화 옵션의 값을 수정한 후 쿼리 창에서 다음 문을 실행합니다.  
  
     암호화에 대 한 인증서를 만드는 방법에 대 한 자세한 내용은 [암호화 된 백업 만들기](create-an-encrypted-backup.md)의 **백업 인증서 만들기** 단계를 참조 하세요.  
  
    ```  
    Use msdb;  
    Go  
       EXEC smart_admin.sp_set_instance_backup  
                     @enable_backup=1  
                    ,@retention_days=30   
                    ,@credential_name='sqlbackuptoURL'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert';  
    GO  
  
    ```  
  
     이제 인스턴스에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용합니다.  
  
6.  다음 Transact-SQL 문을 실행하여 구성 설정을 확인합니다.  
  
    ```  
    Use msdb;  
    GO  
    SELECT * FROM smart_admin.fn_backup_instance_config ();  
  
    ```  
  
7.  인스턴스에 대한 새 데이터베이스를 만듭니다. 다음 Transact-SQL 문을 실행하여 데이터베이스에 대한 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성 설정을 봅니다.  
  
    ```  
    Use msdb  
    GO  
    SELECT * FROM smart_admin.fn_backup_db_config('NewDB')  
    ```  
  
     설정이 표시되고 데이터베이스에 대한 백업 작업이 실행을 시작하려면 최대 15분이 필요합니다.  
  
8.  **상태 알림 사용 및 구성:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에는 주의가 요구될 수 있는 오류나 경고의 메일 알림을 보내는 에이전트 작업을 만드는 저장 프로시저가 있습니다.  이러한 알림을 수신하려면 SQL Server 에이전트 작업을 만드는 저장 프로시저를 실행해야 합니다. 전자 메일 알림을 사용 및 구성하는 단계는 다음과 같습니다.  
  
    1.  인스턴스에 데이터베이스 메일이 설정되지 않은 경우 데이터베이스 메일을 설정합니다. 자세한 내용은 [Configure Database Mail](../database-mail/configure-database-mail.md)을 참조하세요.  
  
    2.  데이터베이스 메일을 사용하도록 SQL Server 에이전트 알림을 구성합니다. 자세한 내용은 [Configure SQL Server Agent Mail to Use Database Mail](../database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)을 참조하세요.  
  
    3.  **백업 오류 및 경고를 수신하도록 이메일 알림 설정:** 쿼리 창에서 다음 Transact-SQL 문을 실행합니다.  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email address>'  
  
        ```  
  
         을 모니터링 하는 방법에 대 한 자세한 내용 및 전체 샘플 스크립트는 [Microsoft Azure에 대 한 관리 되는 백업 SQL Server 모니터링](sql-server-managed-backup-to-microsoft-azure.md)을 참조 하세요.  
  
9. **Microsoft Azure Storage 계정의 백업 파일 보기:** SQL Server Management Studio 또는 Azure 관리 포털에서 스토리지 계정에 연결합니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하도록 구성한 데이터베이스를 호스팅하는 SQL Server 인스턴스에 대한 컨테이너가 표시됩니다. 새 데이터베이스를 만든 후 15분 이내에 데이터베이스 및 로그 백업도 표시됩니다.  
  
10. **상태 모니터링:**  이전에 구성한 메일 알림을 통해 모니터링하거나 기록된 이벤트를 적극적으로 모니터링할 수 있습니다. 다음은 이벤트를 표시하는 데 사용하는 예제 Transact-SQL 문입니다.  
  
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
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    --  to enable debug events  
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
  
 데이터베이스 수준에서 설정을 구성하여 특정 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 기본 설정을 재정의할 수 있습니다. 또한 일시적으로 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 서비스를 일시 중지하고 다시 시작할 수 있습니다. 자세한 내용은 [Microsoft Azure SQL Server 관리 되는 백업-보존 및 저장소 설정](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md) 을 참조 하세요.  
  
  
