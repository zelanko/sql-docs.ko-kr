---
title: Linux에서 SQL Server의 로그 전달 구성
description: 이 자습서에서는 로그 전달을 사용하여 Linux의 SQL Server 인스턴스를 보조 인스턴스에 복제하는 방법에 대한 기본 예제를 보여 줍니다.
author: VanMSFT
ms.author: vanto
ms.date: 07/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: fdabd19b81a880c0969cc6359c703cd156a03fab
ms.sourcegitcommit: 36fe62a3ccf34979bfde3e192cfa778505add465
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94521112"
---
# <a name="get-started-with-log-shipping-on-linux"></a>Linux에서 로그 전달 시작

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

SQL Server 로그 전달은 주 서버의 데이터베이스가 하나 이상의 보조 서버에 복제되는 HA 구성입니다. 간단히 말해서 원본 데이터베이스의 백업이 보조 서버로 복원됩니다. 그런 다음, 주 서버가 트랜잭션 로그 백업을 주기적으로 만들고, 보조 서버에서 데이터베이스의 보조 복사본을 업데이트하여 복원합니다. 

  ![로그 전달 워크플로를 보여 주는 다이어그램](https://preview.ibb.co/hr5Ri5/logshipping.png)

이 그림에 설명된 대로, 로그 전달 세션에는 다음 단계가 포함됩니다.

- 주 SQL Server 인스턴스에서 트랜잭션 로그 파일 백업
- 네트워크를 통해 하나 이상의 보조 SQL Server 인스턴스에 트랜잭션 로그 백업 파일 복사
- 보조 SQL Server 인스턴스에서 트랜잭션 로그 백업 파일 복원

## <a name="prerequisites"></a>사전 요구 사항
- [Linux에 SQL Server 에이전트 설치](./sql-server-linux-setup-sql-agent.md)

## <a name="setup-a-network-share-for-log-shipping-using-cifs"></a>CIFS를 사용하여 로그 전달에 대한 네트워크 공유 설정 

> [!NOTE] 
> 이 자습서에서는 CIFS + Samba를 사용하여 네트워크 공유를 설정합니다. NFS를 사용하려는 경우 의견을 남기면 문서에 추가해 드립니다.       

### <a name="configure-primary-server"></a>주 서버 구성
-   다음을 실행하여 Samba를 설치합니다.

    ```bash
    sudo apt-get install samba #For Ubuntu
    sudo yum -y install samba #For RHEL/CentOS
    ```
-   로그 전달을 위한 로그를 저장할 디렉터리를 만들고 mssql에 필요한 사용 권한을 부여합니다.

    ```bash
    mkdir /var/opt/mssql/tlogs
    chown mssql:mssql /var/opt/mssql/tlogs
    chmod 0700 /var/opt/mssql/tlogs
    ```

-   /etc/samba/smb.conf 파일을 편집하고(루트 권한 필요) 다음 섹션을 추가합니다.

    ```bash
    [tlogs]
    path=/var/opt/mssql/tlogs
    available=yes
    read only=yes
    browsable=yes
    public=yes
    writable=no
    ```

-   Samba의 mssql 사용자를 만듭니다.

    ```bash
    sudo smbpasswd -a mssql
    ```

-   Samba 서비스를 다시 시작합니다.
    ```bash
    sudo systemctl restart smbd.service nmbd.service
    ```
 
### <a name="configure-secondary-server"></a>보조 서버를 구성합니다.

-   다음을 실행하여 CIFS 클라이언트를 설치합니다.
    ```bash   
    sudo apt-get install cifs-utils #For Ubuntu
    sudo yum -y install cifs-utils #For RHEL/CentOS
    ```

-   자격 증명을 저장할 파일을 만듭니다. mssql Samba 계정에 대해 최근에 설정한 암호를 사용합니다. 

    ```console
        vim /var/opt/mssql/.tlogcreds
        #Paste the following in .tlogcreds
        username=mssql
        domain=<domain>
        password=<password>
    ```

-   다음 명령을 실행하여 탑재할 빈 디렉터리를 만들고 권한 및 소유권을 올바르게 설정합니다.
    ```bash   
    mkdir /var/opt/mssql/tlogs
    sudo chown root:root /var/opt/mssql/tlogs
    sudo chmod 0550 /var/opt/mssql/tlogs
    sudo chown root:root /var/opt/mssql/.tlogcreds
    sudo chmod 0660 /var/opt/mssql/.tlogcreds
    ```

-   공유를 유지하기 위해 etc/fstab에 다음 줄을 추가합니다. 

    ```console
        //<ip_address_of_primary_server>/tlogs /var/opt/mssql/tlogs cifs credentials=/var/opt/mssql/.tlogcreds,ro,uid=mssql,gid=mssql 0 0
    ```

-   공유를 탑재합니다.
    ```bash   
    sudo mount -a
    ```
       
## <a name="setup-log-shipping-via-t-sql"></a>T-SQL을 통한 로그 전달 설정

- 주 서버에서 이 스크립트를 실행합니다.

    ```sql
    BACKUP DATABASE SampleDB
    TO DISK = '/var/opt/mssql/tlogs/SampleDB.bak'
    GO
    ```

    ```sql
    DECLARE @LS_BackupJobId AS uniqueidentifier 
    DECLARE @LS_PrimaryId   AS uniqueidentifier 
    DECLARE @SP_Add_RetCode As int 
    EXECUTE @SP_Add_RetCode = master.dbo.sp_add_log_shipping_primary_database 
             @database = N'SampleDB' 
            ,@backup_directory = N'/var/opt/mssql/tlogs' 
            ,@backup_share = N'/var/opt/mssql/tlogs' 
            ,@backup_job_name = N'LSBackup_SampleDB' 
            ,@backup_retention_period = 4320
            ,@backup_compression = 2
            ,@backup_threshold = 60 
            ,@threshold_alert_enabled = 1
            ,@history_retention_period = 5760 
            ,@backup_job_id = @LS_BackupJobId OUTPUT 
            ,@primary_id = @LS_PrimaryId OUTPUT 
            ,@overwrite = 1 

    IF (@@ERROR = 0 AND @SP_Add_RetCode = 0) 
    BEGIN 

    DECLARE @LS_BackUpScheduleUID   As uniqueidentifier 
    DECLARE @LS_BackUpScheduleID    AS int 

    EXECUTE msdb.dbo.sp_add_schedule 
            @schedule_name =N'LSBackupSchedule' 
            ,@enabled = 1 
            ,@freq_type = 4 
            ,@freq_interval = 1 
            ,@freq_subday_type = 4 
            ,@freq_subday_interval = 15 
            ,@freq_recurrence_factor = 0 
            ,@active_start_date = 20170418 
            ,@active_end_date = 99991231 
            ,@active_start_time = 0 
            ,@active_end_time = 235900 
            ,@schedule_uid = @LS_BackUpScheduleUID OUTPUT 
            ,@schedule_id = @LS_BackUpScheduleID OUTPUT 

    EXECUTE msdb.dbo.sp_attach_schedule 
            @job_id = @LS_BackupJobId 
            ,@schedule_id = @LS_BackUpScheduleID  

    EXECUTE msdb.dbo.sp_update_job 
            @job_id = @LS_BackupJobId 
            ,@enabled = 1 
            
    END 

    EXECUTE master.dbo.sp_add_log_shipping_alert_job 

    EXECUTE master.dbo.sp_add_log_shipping_primary_secondary 
            @primary_database = N'SampleDB' 
            ,@secondary_server = N'<ip_address_of_secondary_server>' 
            ,@secondary_database = N'SampleDB' 
            ,@overwrite = 1 
    ```


- 보조 서버에서 이 스크립트를 실행합니다.

    ```sql
    RESTORE DATABASE SampleDB FROM DISK = '/var/opt/mssql/tlogs/SampleDB.bak'
    WITH NORECOVERY;
    ```
    
    ```sql
    DECLARE @LS_Secondary__CopyJobId    AS uniqueidentifier 
    DECLARE @LS_Secondary__RestoreJobId AS uniqueidentifier 
    DECLARE @LS_Secondary__SecondaryId  AS uniqueidentifier 
    DECLARE @LS_Add_RetCode As int 

    EXECUTE @LS_Add_RetCode = master.dbo.sp_add_log_shipping_secondary_primary 
            @primary_server = N'<ip_address_of_primary_server>' 
            ,@primary_database = N'SampleDB' 
            ,@backup_source_directory = N'/var/opt/mssql/tlogs/' 
            ,@backup_destination_directory = N'/var/opt/mssql/tlogs/' 
            ,@copy_job_name = N'LSCopy_SampleDB' 
            ,@restore_job_name = N'LSRestore_SampleDB' 
            ,@file_retention_period = 4320 
            ,@overwrite = 1 
            ,@copy_job_id = @LS_Secondary__CopyJobId OUTPUT 
            ,@restore_job_id = @LS_Secondary__RestoreJobId OUTPUT 
            ,@secondary_id = @LS_Secondary__SecondaryId OUTPUT 

    IF (@@ERROR = 0 AND @LS_Add_RetCode = 0) 
    BEGIN 

    DECLARE @LS_SecondaryCopyJobScheduleUID As uniqueidentifier 
    DECLARE @LS_SecondaryCopyJobScheduleID  AS int 

    EXECUTE msdb.dbo.sp_add_schedule 
            @schedule_name =N'DefaultCopyJobSchedule' 
            ,@enabled = 1 
            ,@freq_type = 4 
            ,@freq_interval = 1 
            ,@freq_subday_type = 4 
            ,@freq_subday_interval = 15 
            ,@freq_recurrence_factor = 0 
            ,@active_start_date = 20170418 
            ,@active_end_date = 99991231 
            ,@active_start_time = 0 
            ,@active_end_time = 235900 
            ,@schedule_uid = @LS_SecondaryCopyJobScheduleUID OUTPUT 
            ,@schedule_id = @LS_SecondaryCopyJobScheduleID OUTPUT 

    EXECUTE msdb.dbo.sp_attach_schedule 
            @job_id = @LS_Secondary__CopyJobId 
            ,@schedule_id = @LS_SecondaryCopyJobScheduleID  

    DECLARE @LS_SecondaryRestoreJobScheduleUID  As uniqueidentifier 
    DECLARE @LS_SecondaryRestoreJobScheduleID   AS int 

    EXECUTE msdb.dbo.sp_add_schedule 
            @schedule_name =N'DefaultRestoreJobSchedule' 
            ,@enabled = 1 
            ,@freq_type = 4 
            ,@freq_interval = 1 
            ,@freq_subday_type = 4 
            ,@freq_subday_interval = 15 
            ,@freq_recurrence_factor = 0 
            ,@active_start_date = 20170418 
            ,@active_end_date = 99991231 
            ,@active_start_time = 0 
            ,@active_end_time = 235900 
            ,@schedule_uid = @LS_SecondaryRestoreJobScheduleUID OUTPUT 
            ,@schedule_id = @LS_SecondaryRestoreJobScheduleID OUTPUT 

    EXECUTE msdb.dbo.sp_attach_schedule 
            @job_id = @LS_Secondary__RestoreJobId 
            ,@schedule_id = @LS_SecondaryRestoreJobScheduleID  
            
    END 
    DECLARE @LS_Add_RetCode2    As int 
    IF (@@ERROR = 0 AND @LS_Add_RetCode = 0) 
    BEGIN 

    EXECUTE @LS_Add_RetCode2 = master.dbo.sp_add_log_shipping_secondary_database 
            @secondary_database = N'SampleDB' 
            ,@primary_server = N'<ip_address_of_primary_server>' 
            ,@primary_database = N'SampleDB' 
            ,@restore_delay = 0 
            ,@restore_mode = 0 
            ,@disconnect_users  = 0 
            ,@restore_threshold = 45   
            ,@threshold_alert_enabled = 1 
            ,@history_retention_period  = 5760 
            ,@overwrite = 1 

    END 

    IF (@@error = 0 AND @LS_Add_RetCode = 0) 
    BEGIN 

    EXECUTE msdb.dbo.sp_update_job 
            @job_id = @LS_Secondary__CopyJobId 
            ,@enabled = 1 

    EXECUTE msdb.dbo.sp_update_job 
            @job_id = @LS_Secondary__RestoreJobId 
            ,@enabled = 1 

    END 
    ```

## <a name="verify-log-shipping-works"></a>로그 전달이 작동되는지 확인

- 주 서버에서 다음 작업을 시작하여 로그 전달이 작동되는지 확인합니다.

    ```sql
    USE msdb ;  
    GO  

    EXECUTE dbo.sp_start_job N'LSBackup_SampleDB' ;  
    GO  
    ```

- 보조 서버에서 다음 작업을 시작하여 로그 전달이 작동되는지 확인합니다.
 
    ```sql
    USE msdb ;  
    GO  

    EXECUTE dbo.sp_start_job N'LSCopy_SampleDB' ;  
    GO  
    EXECUTE dbo.sp_start_job N'LSRestore_SampleDB' ;  
    GO  
    ```
 - 다음 명령을 실행하여 로그 전달 장애 조치(failover)가 작동하는지 확인합니다.
 
    > [!WARNING]
    > 이 명령은 보조 데이터베이스를 온라인 상태로 전환하고 로그 전달 구성을 중단합니다. 이 명령을 실행한 후에는 로그 전달을 다시 구성해야 합니다.
 
    ```sql
    RESTORE DATABASE SampleDB WITH RECOVERY;
    ```