---
title: "Microsoft Azure에 대한 SQL Server Managed Backup 설정 | Microsoft 문서"
ms.custom: 
ms.date: 10/03/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
caps.latest.revision: "25"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ee6f5c066b43c91d1317ca833599ac2f178b03fc
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="enable-sql-server-managed-backup-to-microsoft-azure"></a>Microsoft Azure에 대한 SQL Server Managed Backup 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목은 데이터베이스 및 인스턴스 수준에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]를 기본 설정으로 사용하는 방법에 대해 설명합니다. 또한 전자 메일 알림을 설정하고 백업 활동을 모니터링하는 방법에 대해서도 설명합니다.  
  
 이 자습서는 Azure PowerShell을 사용합니다. 자습서를 시작하기 전에 [Azure PowerShell을 다운로드 및 설치](http://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/)하십시오.  
  
> [!IMPORTANT]  
>  고급 옵션도 설정하거나 사용자 지정 일정을 사용하려는 경우에는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 설정하기 전에 해당 설정을 구성하십시오. 자세한 내용은 [Configure Advanced Options for SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md)을 참조하세요.  
  
## <a name="enable-and-configure-includesssmartbackupincludesss-smartbackup-mdmd-with-default-settings"></a>기본 설정으로 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 설정 및 구성  
  
#### <a name="create-the-azure-blob-container"></a>Azure Blob 컨테이너 만들기  
  
1.  **Azure 구독:** 이미 Azure 구독이 있는 경우 다음 단계로 이동합니다. 그렇지 않을 경우 [무료 평가판](http://azure.microsoft.com/pricing/free-trial/) 으로 시작한 후에 [구매 옵션](http://azure.microsoft.com/pricing/purchase-options/)을 살펴볼 수 있습니다.  
  
2.  **Azure Storage 계정 만들기:** 이미 저장소 계정이 있는 경우 다음 단계로 이동합니다. 그렇지 않을 경우 [Azure 관리 포털](https://manage.windowsazure.com/) 또는 Azure PowerShell을 사용하여 저장소 계정을 만들 수 있습니다. 다음 `New-AzureStorageAccount` 명령은 미국 동부 지역에 `managedbackupstorage` 라는 저장소 계정을 만듭니다.  
  
    ```powershell  
    New-AzureStorageAccount -StorageAccountName "managedbackupstorage" -Location "EAST US"  
    ```  
  
     저장소 계정에 대한 자세한 내용은 [Azure Storage 계정](http://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account/)을 참조하세요.  
  
3.  **백업 파일의 Blob 컨테이너 만들기:** Blob 컨테이너를 Azure 관리 포털에 만들거나 Azure PowerShell을 사용하여 만들 수 있습니다. 다음 `New-AzureStorageContainer` 명령은 `backupcontainer` 저장소 계정에 `managedbackupstorage` 라는 Blob 컨테이너를 만듭니다.  
  
    ```powershell  
    $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey (Get-AzureStorageKey -StorageAccountName managedbackupstorage).Primary  
    New-AzureStorageContainer -Name backupcontainer -Context $context  
    ```  
  
4.  **SAS(공유 액세스 서명) 생성:** 컨테이너에 액세스하려면 SAS를 만들어야 합니다. 이 작업은 몇 가지 도구, 코드 및 Azure PowerShell에서 수행할 수 있습니다. 다음 `New-AzureStorageContainerSASToken` 명령은 1년 후에 만료되는 `backupcontainer` Blob 컨테이너에 대한 SAS 토큰을 만듭니다.  
  
    ```powershell  
    $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey (Get-AzureStorageKey -StorageAccountName managedbackupstorage).Primary   
    New-AzureStorageContainerSASToken -Name backupcontainer -Permission rwdl -ExpiryTime (Get-Date).AddYears(1) -FullUri -Context $context  
    ```  
  
     이 명령의 출력에는 컨테이너와 SAS 토큰에 대한 URL이 포함됩니다. 다음은 이에 대한 예입니다.  
  
    ```  
    https://managedbackupstorage.blob.core.windows.net/backupcontainer?sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl  
    ```  
  
     위 예의 물음표 위치에서 SAS 토큰과 컨테이너 URL을 분리합니다(물음표는 포함하지 않음). 예를 들어 위의 출력은 다음과 같은 두 값이 됩니다.  
  
    |||  
    |-|-|  
    |**컨테이너 URL:**|https://managedbackupstorage.blob.core.windows.net/backupcontainer|  
    |**SAS 토큰:**|sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl|  
  
     SQL 자격 증명을 만드는 데 사용할 컨테이너 URL과 SAS를 기록합니다. SAS에 대한 자세한 내용은 [공유 액세스 서명, 1부: SAS 모델 이해](http://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)를 참조하세요.  
  
#### <a name="enable-includesssmartbackupincludesss-smartbackup-mdmd"></a>사용 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
1.  **SAS URL에 대한 SQL 자격 증명 만들기:** SAS 토큰을 사용하여 Blob 컨테이너 URL에 대한 SQL 자격 증명을 만듭니다. 다음 예제를 기준으로 SQL Server Management Studio에서 다음 Transact-SQL 쿼리를 사용하여 Blob 컨테이너 URL의 자격 증명을 만듭니다.  
  
    ```sql  
    CREATE CREDENTIAL [https://managedbackupstorage.blob.core.windows.net/backupcontainer]   
    WITH IDENTITY = 'Shared Access Signature',  
    SECRET = 'sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl'  
    ```  
  
2.  **SQL Server 에이전트 서비스가 시작되고 실행 중인지 확인:** SQL 서버를 실행합니다(현재 실행되고 있지 않은 경우).  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 실행하여 백업 작업을 수행하려면 SQL Server 에이전트가 필요합니다.  SQL Server 에이전트가 자동으로 실행되어 백업 작업이 정기적으로 발생하도록 설정할 수 있습니다.  
  
3.  **보존 기간 결정:** 백업 파일의 보존 기간을 결정합니다. 보존 기간은 일 단위로 지정되며 1-30일의 범위로 설정할 수 있습니다.  
  
4.  **Enable and configure [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] :** SQL Server Management Studio를 시작하고 대상 SQL Server 인스턴스에 연결합니다. 요구 사항에 따라 데이터베이스 이름, 컨테이너 URL, 보존 기간 값을 수정한 후 쿼리 창에서 다음 문을 실행합니다.  
  
    > [!IMPORTANT]  
    >  인스턴스 수준에서 Managed Backup을 사용하려면 `NULL` 매개 변수에 대해 `database_name` 을 지정합니다.  
  
    ```sql  
    Use msdb;  
    GO  
    EXEC msdb.managed_backup.sp_backup_config_basic   
     @enable_backup = 1,   
     @database_name = 'yourdatabasename',  
     @container_url = 'https://managedbackupstorage.blob.core.windows.net/backupcontainer',   
     @retention_days = 30  
    GO  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 설정되었습니다. 데이터베이스에서 백업 작업이 실행을 시작하려면 최대 15분이 필요합니다.  
  
5.  **확장 이벤트 기본 구성 검토:** 다음 transact-SQL 문을 실행하여 확장 이벤트 설정을 검토합니다.  
  
    ```  
    SELECT * FROM msdb.managed_backup.fn_get_current_xevent_settings()  
    ```  
  
     Admin, Operational 및 Analytical 채널 이벤트가 기본적으로 설정되어 있고 해제할 수 없습니다. 수동 작업이 필요한 이벤트를 모니터링하기에 충분해야 합니다.  디버그 이벤트를 설정할 수 있지만 디버그 채널에는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에서 문제를 발견 및 해결하는 데 사용하는 정보와 디버그 이벤트가 포함됩니다.  
  
6.  **상태 알림 사용 및 구성:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에는 주의가 요구될 수 있는 오류나 경고의 메일 알림을 보내는 에이전트 작업을 만드는 저장 프로시저가 있습니다. 전자 메일 알림을 사용 및 구성하는 단계는 다음과 같습니다.  
  
    1.  인스턴스에 데이터베이스 메일이 설정되지 않은 경우 데이터베이스 메일을 설정합니다. 자세한 내용은 [Configure Database Mail](../../relational-databases/database-mail/configure-database-mail.md)을 참조하세요.  
  
    2.  데이터베이스 메일을 사용하도록 SQL Server 에이전트 알림을 구성합니다. 자세한 내용은 [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)을 참조하세요.  
  
    3.  **백업 오류 및 경고를 수신하도록 메일 알림 설정:** 쿼리 창에서 다음 Transact-SQL 문을 실행합니다.  
  
        ```  
        EXEC msdb.managed_backup.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
  
        ```  
  
7.  **Microsoft Azure Storage 계정에서 백업 파일 보기:** SQL Server Management Studio 또는 Azure 관리 포털에서 저장소 계정에 연결합니다. 지정한 컨테이너에 백업 파일이 표시됩니다. 데이터베이스에 대한 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 설정한 후 5분 이내에 데이터베이스 및 로그 백업이 표시될 수 있습니다.  
  
8.  **상태 모니터링:**  이전에 구성한 메일 알림을 통해 모니터링하거나 기록된 이벤트를 능동적으로 모니터링할 수 있습니다. 다음은 이벤트를 표시하는 데 사용하는 예제 Transact-SQL 문입니다.  
  
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
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 이 섹션에서는 데이터베이스에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 처음 구성하는 단계에 대해 설명합니다. 동일한 시스템 저장 프로시저를 사용하여 기존 구성을 수정하고 새 값을 제공할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft Azure에 대한 SQL Server Managed Backup](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
