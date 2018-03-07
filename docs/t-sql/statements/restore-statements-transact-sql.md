---
title: "복원 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE DATABASE
- RESTORE_TSQL
- RESTORE_DATABASE_TSQL
- RESTORE
- RESTORE_LOG_TSQL
- RESTORE LOG
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE DATABASE, see RESTORE statement
- full backups [SQL Server]
- RECOVERY option
- database snapshots [SQL Server], reverting to
- STOPAT syntax
- differential backups, RESTORE statement
- point in time recovery [SQL Server]
- restoring [SQL Server]
- NORECOVERY option
- online restores [SQL Server], RESTORE statement
- moving databases
- RESTORE statement, syntax
- cross-platform restores
- restoring databases [SQL Server], options
- RESTORE statement
- snapshots [SQL Server database snapshots], reverting to
- reverting database snapshots
- transaction log backups [SQL Server], RESTORE statement
- RESTORE LOG, see RESTORE statement
ms.assetid: 877ecd57-3f2e-4237-890a-08f16e944ef1
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: edafff7cc70224c67ef970ca4c13e47cce113f23
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements-transact-sql"></a>RESTORE 문 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  BACKUP 명령을 사용하여 만든 백업을 복원합니다. 이 명령을 사용하면 다음과 같은 복원 시나리오를 수행할 수 있습니다.  
  
-   전체 데이터베이스 백업에서 전체 데이터베이스를 복원합니다(전체 복원).  
  
-   데이터베이스의 일부를 복원합니다(부분 복원).  
  
-   특정 파일 또는 파일 그룹을 데이터베이스로 복원합니다(파일 복원).  
  
-   특정 페이지를 데이터베이스로 복원합니다(페이지 복원).  
  
-   트랜잭션 로그를 데이터베이스로 복원합니다(트랜잭션 로그 복원).  
  
-   데이터베이스 스냅숏에서 캡처한 지점으로 데이터베이스를 되돌립니다.  
  
 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복원 시나리오, 참조 [복원 및 복구 개요 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  인수 설명에 대 한 자세한 내용은 참조 하세요. [RESTORE 인수 &#40; Transact SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).   다른 인스턴스에서 데이터베이스를 복원할 때 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리(SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)의 정보를 참조하세요.
  
> **참고:** Windows Azure Blob 저장소 서비스로 복원 하는 방법에 대 한 자세한 내용은 참조 [SQL Server 백업 및 Microsoft Azure Blob 저장소 서비스로 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
--To Restore an Entire Database from a Full database backup (a Complete Restore):  
RESTORE DATABASE { database_name | @database_name_var }   
 [ FROM <backup_device> [ ,...n ] ]  
 [ WITH   
   {  
    [ RECOVERY | NORECOVERY | STANDBY =   
        {standby_file_name | @standby_file_name_var }   
       ]  
   | ,  <general_WITH_options> [ ,...n ]  
   | , <replication_WITH_option>  
   | , <change_data_capture_WITH_option>  
   | , <FILESTREAM_WITH_option>  
   | , <service_broker_WITH options>   
   | , \<point_in_time_WITH_options—RESTORE_DATABASE>   
   } [ ,...n ]  
 ]  
[;]  
  
--To perform the first step of the initial restore sequence  
-- of a piecemeal restore:  
RESTORE DATABASE { database_name | @database_name_var }   
   <files_or_filegroups> [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
      PARTIAL, NORECOVERY   
      [  , <general_WITH_options> [ ,...n ]   
       | , \<point_in_time_WITH_options—RESTORE_DATABASE>   
      ] [ ,...n ]   
[;]  
  
--To Restore Specific Files or Filegroups:   
RESTORE DATABASE { database_name | @database_name_var }   
   <file_or_filegroup> [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
   {  
      [ RECOVERY | NORECOVERY ]  
      [ , <general_WITH_options> [ ,...n ] ]  
   } [ ,...n ]   
[;]  
  
--To Restore Specific Pages:   
RESTORE DATABASE { database_name | @database_name_var }   
   PAGE = 'file:page [ ,...n ]'   
 [ , <file_or_filegroups> ] [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
       NORECOVERY     
      [ , <general_WITH_options> [ ,...n ] ]  
[;]  
  
--To Restore a Transaction Log:  
RESTORE LOG { database_name | @database_name_var }   
 [ <file_or_filegroup_or_pages> [ ,...n ] ]  
 [ FROM <backup_device> [ ,...n ] ]   
 [ WITH   
   {  
     [ RECOVERY | NORECOVERY | STANDBY =   
        {standby_file_name | @standby_file_name_var }   
       ]  
    | ,  <general_WITH_options> [ ,...n ]  
    | , <replication_WITH_option>  
    | , \<point_in_time_WITH_options—RESTORE_LOG>   
   } [ ,...n ]  
 ]   
[;]  
  
--To Revert a Database to a Database Snapshot:     
RESTORE DATABASE { database_name | @database_name_var }   
FROM DATABASE_SNAPSHOT = database_snapshot_name   
  
<backup_device>::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
 | { DISK | TAPE | URL } = { 'physical_backup_device_name' |  
      @physical_backup_device_name_var }   
}   
Note: URL is the format used to specify the location and the file name for the Windows Azure Blob. Although Windows Azure storage is a service, the implementation is similar to disk and tape to allow for a consistent and seemless restore experince for all the three devices.  
<files_or_filegroups>::=   
{   
   FILE = { logical_file_name_in_backup | @logical_file_name_in_backup_var }   
 | FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }   
 | READ_WRITE_FILEGROUPS  
}   
  
<general_WITH_options> [ ,...n ]::=   
--Restore Operation Options  
   MOVE 'logical_file_name_in_backup' TO 'operating_system_file_name'   
          [ ,...n ]   
 | REPLACE   
 | RESTART   
 | RESTRICTED_USER  | CREDENTIAL  
  
--Backup Set Options  
 | FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }   
 | BLOCKSIZE = { blocksize | @blocksize_variable }   
  
--Data Transfer Options  
 | BUFFERCOUNT = { buffercount | @buffercount_variable }   
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }   
  
--Monitoring Options  
 | STATS [ = percentage ]   
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }   
  
<replication_WITH_option>::=  
 | KEEP_REPLICATION   
  
<change_data_capture_WITH_option>::=  
 | KEEP_CDC  
  
<FILESTREAM_WITH_option>::=  
 | FILESTREAM ( DIRECTORY_NAME = directory_name )  
  
<service_broker_WITH_options>::=   
 | ENABLE_BROKER   
 | ERROR_BROKER_CONVERSATIONS   
 | NEW_BROKER  
  
\<point_in_time_WITH_options—RESTORE_DATABASE>::=   
 | {  
   STOPAT = { 'datetime'| @datetime_var }   
 | STOPATMARK = 'lsn:lsn_number'  
                 [ AFTER 'datetime']   
 | STOPBEFOREMARK = 'lsn:lsn_number'  
                 [ AFTER 'datetime']   
   }   
  
\<point_in_time_WITH_options—RESTORE_LOG>::=   
 | {  
   STOPAT = { 'datetime'| @datetime_var }   
 | STOPATMARK = { 'mark_name' | 'lsn:lsn_number' }  
                 [ AFTER 'datetime']   
 | STOPBEFOREMARK = { 'mark_name' | 'lsn:lsn_number' }  
                 [ AFTER 'datetime']   
   }  
  
```  
  
## <a name="arguments"></a>인수  
 인수 설명에 대 한 참조 [RESTORE 인수 &#40; Transact SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="about-restore-scenarios"></a>복원 시나리오  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 다양한 복원 시나리오를 지원합니다.  
  
-   전체 데이터베이스 복원  
  
     전체 데이터베이스 백업에서 시작하여 전체 데이터베이스를 복원한 다음 차등 데이터베이스 백업 및 로그 백업을 복원할 수 있습니다. 자세한 내용은 [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md) 또는 [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)을 참조하세요.  
  
-   파일 복원  
  
     파일 그룹이 여러 개인 데이터베이스에서 파일 또는 파일 그룹을 복원합니다. 단순 복구 모델에서 파일은 읽기 전용 파일 그룹에 속해야 합니다. 전체 파일 복원 후에는 차등 파일 백업을 복원할 수 있습니다. 자세한 내용은 참조 [파일 복원 &#40; 전체 복구 모델 &#41; ](../../relational-databases/backup-restore/file-restores-full-recovery-model.md) 및 [파일 복원 &#40; 단순 복구 모델 &#41; ](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md).  
  
-   페이지 복원  
  
     개별 페이지를 복원합니다. 페이지 복원은 전체 및 대량 로그 복구 모델에서만 사용할 수 있습니다. 자세한 내용은 [페이지 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)을 참조하세요.  
  
-   증분 복원  
  
     주 파일 그룹 및 하나 이상의 보조 파일 그룹에서 시작하여 단계별로 데이터베이스를 복원합니다. 증분 복원은 PARTIAL 옵션을 사용하고 복원할 보조 파일 그룹을 하나 이상 지정하여 RESTORE DATABASE에서 시작합니다. 자세한 내용은 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)을 참조하세요.  
  
-   복원만  
  
     데이터베이스와 이미 일치하는 데이터를 복원하여 사용 가능하도록 설정만 하면 됩니다. 자세한 내용은 [데이터를 복원하지 않고 데이터베이스 복구&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)를 참조하세요.  
  
-   트랜잭션 로그 복원  
  
     전체 또는 대량 로그 복구 모델에서는 로그 백업을 복원해야 원하는 복구 지점에 도달할 수 있습니다. 로그 백업을 복원 하는 방법에 대 한 자세한 내용은 참조 [트랜잭션 로그 백업 적용 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
-   Always On 가용성 그룹에 대 한 가용성 데이터베이스 준비  
  
     자세한 내용은 [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)를 참조하세요.  
  
-   데이터베이스 미러링을 위한 미러 데이터베이스 준비  
  
     자세한 내용은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)의 몇 가지 기능에 대한 백업 및 복원 고려 사항에 대해 설명합니다.  
  
-   온라인 복원  
  
    > **참고:** 온라인 복원의 Enterprise edition에만 허용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
     온라인 복원이 지원되는 경우 데이터베이스가 온라인이면 파일 복원 및 페이지 복원은 자동으로 온라인 복원이 되며 초기 증분 복원을 실행한 다음에는 보조 파일 그룹의 복원이 되기도 합니다.  
  
    > **참고:** 온라인 복원 될 수 있습니다 [지연 된 트랜잭션을](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)합니다.  
  
     자세한 내용은 참조 [온라인 복원 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/online-restore-sql-server.md).  
  
## <a name="additional-considerations-about-restore-options"></a>RESTORE 옵션에 대한 추가 고려 사항  
  
### <a name="discontinued-restore-keywords"></a>지원되지 않는 RESTORE 키워드  
 다음 키워드는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서 더 이상 지원되지 않습니다.  
  
|지원되지 않는 키워드|대체 키워드|대체 키워드 예|  
|--------------------------|------------------|------------------------------------|  
|LOAD|RESTORE|`RESTORE DATABASE`|  
|TRANSACTION|LOG|`RESTORE LOG`|  
|DBO_ONLY|RESTRICTED_USER|`RESTORE DATABASE ... WITH RESTRICTED_USER`|  
  
### <a name="restore-log"></a>RESTORE LOG  
 RESTORE LOG에 파일 목록을 포함하여 롤포워드 중에 파일을 만들 수 있습니다. 이 기능은 데이터베이스에 파일을 추가할 때 기록된 로그 레코드가 로그 백업에 포함되는 경우에 사용됩니다.  
  
> **참고:** 전체 또는 대량 로그 복구 모델을 사용 하 여 데이터베이스에 대 한 대부분의 경우에서 백업 해야 비상 로그 데이터베이스를 복원 하기 전에. RESTORE DATABASE 문에 데이터 백업이 종료된 후 발생한 시간 또는 트랜잭션을 지정해야 하는 WITH REPLACE나 WITH STOPAT 절이 포함되어 있지 않은 경우 비상 로그 백업을 먼저 수행하지 않고 데이터베이스를 복원하면 오류가 발생합니다. 비상 로그 백업에 대한 자세한 내용은 [비상 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 참조하세요.  
  
### <a name="comparison-of-recovery-and-norecovery"></a>RECOVERY와 NORECOVERY 비교  
 RESTORE 문에서 다음과 같이 [ RECOVERY | NORECOVERY ] 옵션을 통해 롤백을 제어합니다.  
  
-   NORECOVERY는 롤백이 발생하지 않도록 지정합니다. 이렇게 하면 순서대로 다음 문으로 롤포워드를 계속할 수 있습니다.  
  
     이런 경우 복원 시퀀스는 다른 백업을 복원하여 롤포워드할 수 있습니다.  
  
-   RECOVERY(기본값)는 현재 백업에 대해 롤포워드가 완료된 다음 롤백이 수행되어야 한다는 의미입니다.  
  
     전체 데이터 집합을 복원 중인 데이터베이스를 복구 하려면 (의 *롤포워드 세트*)는 데이터베이스와 일치 합니다. 롤포워드 세트가 데이터베이스와 일치할 만큼 충분히 롤포워드되지 않은 경우 RECOVERY를 지정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류가 발생합니다.  
  
## <a name="compatibility-support"></a>호환성 지원  
 백업 **마스터**, **모델** 및 **msdb** 의 이전 버전을 사용 하 여 만든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 복원할 수 없습니다 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다.  
  
> **참고:** 아니요 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 백업을 복원할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업을 만든 버전 보다 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 각 버전은 이전 버전과는 다른 기본 경로를 사용합니다. 따라서 이전 버전 백업의 기본 위치에 만든 데이터베이스를 복원하려면 MOVE 옵션을 사용해야 합니다. 새 기본 경로 대 한 정보를 참조 하십시오. [Named Instances of SQL Server 인스턴스 및 기본 파일 위치](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)합니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 이전 버전 데이터베이스를 복원하면 데이터베이스가 자동으로 업그레이드됩니다. 일반적으로 데이터베이스는 즉시 사용할 수 있습니다. 그러나 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스에 전체 텍스트 인덱스가 있는 경우 업그레이드 프로세스는  **upgrade_option** 서버 속성의 설정에 따라 인덱스를 가져오거나 다시 설정하거나 다시 작성합니다. 업그레이드 옵션이 가져오기(**upgrade_option** = 2) 또는 다시 작성(**upgrade_option** = 0)으로 설정되어 있는 경우 업그레이드하는 동안 전체 텍스트 인덱스를 사용할 수 없습니다. 인덱싱되는 데이터 양에 따라 가져오기 작업은 몇 시간씩 걸릴 수 있으며 다시 작성 작업은 10배 정도 더 걸릴 수 있습니다. 업그레이드 옵션이 가져오기로 설정되어 있으면 전체 텍스트 카탈로그를 사용할 수 없는 경우 관련된 전체 텍스트 인덱스가 다시 작성됩니다. **upgrade_option** 서버 속성의 설정을 변경하려면 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)를 사용합니다.  
  
 데이터베이스가 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 처음으로 연결되거나 복원될 때 데이터베이스 마스터 키(서비스 마스터 키로 암호화됨)의 복사본은 서버에 아직 저장되지 않은 상태입니다. 데이터베이스 마스터 키를 암호 해독하려면 **OPEN MASTER KEY** 문을 사용해야 합니다. DMK를 암호 해독한 후에는 **ALTER MASTER KEY REGENERATE** 문을 사용하여 SMK(서비스 마스터 키)로 암호화된 DMK의 복사본을 서버에 프로비전함으로써 앞으로 자동 암호 해독을 사용하도록 설정할 수 있습니다. 데이터베이스가 이전 버전에서 업그레이드되지 않은 경우에는 DMK를 다시 생성해야 최신 AES 알고리즘을 사용할 수 있습니다. DMK를 다시 생성하는 방법은 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)를 참조하세요. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 데 소요되는 시간은 DMK에서 보호하는 개체 수에 따라 달라집니다. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 작업은 한 번만 필요하며 키 회전 전략의 일부로 이후에 수행하는 다시 생성 작업에 영향을 주지 않습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 오프라인 복원 시에 지정된 데이터베이스가 사용 중이면 RESTORE는 짧은 지연 후 사용자가 강제로 로그오프되도록 합니다. 주 파일 그룹이 아닌 파일 그룹에 대한 온라인 복원의 경우 복원한 파일 그룹이 오프라인 상태가 되는 경우를 제외하면 데이터베이스는 사용 중 상태로 유지될 수 있습니다. 지정한 데이터베이스의 모든 데이터는 복원된 데이터로 대체됩니다.  
  
 데이터베이스를 복구 하는 방법에 대 한 자세한 내용은 참조 [복원 및 복구 개요 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
 플랫폼 간 복원 작업은 서로 다른 프로세서 유형 간 복원 작업인 경우에도 운영 체제에서 데이터베이스의 데이터 정렬을 지원하는 한 수행할 수 있습니다.  
  
 오류가 발생하면 RESTORE는 다시 시작할 수 있습니다. 또한 오류와 관계없이 RESTORE가 계속되도록 지시하여 최대한 많은 데이터를 복원할 수 있습니다(CONTINUE_AFTER_ERROR 옵션 참조).  
  
 RESTORE는 명시적 또는 암시적 트랜잭션에서 사용할 수 없습니다.  
  
 손상 된 복원 **마스터** 데이터베이스 특별 한 프로시저를 사용 하 여 수행 됩니다. 자세한 내용은 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)를 참조하세요.  
  
 데이터베이스를 복원하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 계획 캐시가 지워집니다. 계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 "데이터베이스 유지 관리 또는 재구성 작업으로 인해 '%s' 캐시스토어(계획 캐시의 일부)에 대한 캐시스토어 플러시가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 %d번 발견되었습니다"라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.  
  
 가용성 데이터베이스를 복원하려면 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 데이터베이스를 복원한 다음 데이터베이스를 가용성 그룹에 추가합니다.  
  
## <a name="interoperability"></a>상호 운용성  
  
### <a name="database-settings-and-restoring"></a>데이터베이스 설정 및 복원  
 복원 시에는 ALTER DATABASE를 사용하여 설정할 수 있는 대부분의 데이터베이스 옵션이 백업 종료 시에 유효한 값으로 다시 설정됩니다.  
  
 그러나 WITH RESTRICTED_USER 옵션을 사용하면 사용자 액세스 옵션 설정 시에 이 동작이 무시됩니다. 이 설정은 항상 WITH RESTRICTED_USER 옵션이 포함되어 있는 RESTORE 문 다음에 지정됩니다.  
  
### <a name="restoring-an-encrypted-database"></a>암호화된 데이터베이스 복원  
 암호화된 데이터베이스를 복원하려면 데이터베이스를 암호화하는 데 사용된 인증서 또는 비대칭 키에 대한 액세스 권한이 있어야 합니다. 인증서 또는 비대칭 키가 없으면 데이터베이스를 복원할 수 없습니다. 따라서 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서는 백업이 필요한 동안에는 유지되어야 합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.  
  
### <a name="restoring-a-database-enabled-for-vardecimal-storage"></a>VarDecimal 저장소에 사용할 수 있는 데이터베이스 복원  
 백업 및 복원 작업을 올바르게는 **vardecimal** 저장소 형식입니다. 에 대 한 자세한 내용은 **vardecimal** 저장소 형식을 참조 [sp_db_vardecimal_storage_format &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md).  
  
### <a name="restore-full-text-data"></a>전체 텍스트 데이터 복원  
 전체 텍스트 데이터가 전체 복원 시에 다른 데이터베이스 데이터와 함께 복원됩니다. 전체 텍스트 파일은 일반 `RESTORE DATABASE database_name FROM backup_device` 구문을 사용하여 데이터베이스 파일 복원의 일부로 복원됩니다.  
  
 또한 RESTORE 문을 사용하여 대체 위치로 복원, 차등 복원, 파일 및 파일 그룹 복원, 전체 텍스트 데이터의 차등 파일 및 파일 그룹 복원을 수행할 수 있습니다. 또한 RESTORE를 사용하면 전체 텍스트 파일만 복원할 수도 있고 데이터베이스 데이터를 함께 복원할 수도 있습니다.  
  
> **참고:** 에서 가져온 전체 텍스트 카탈로그 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 여전히 데이터베이스 파일로 처리 됩니다. 따라서 백업 작업 중에 더 이상 일시 중지하고 재개할 필요가 없다는 점을 제외하고 전체 텍스트 카탈로그를 백업하는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 절차는 계속 적용 가능합니다. 자세한 내용은 참조 [복원 전체 텍스트 카탈로그 백업 및](http://go.microsoft.com/fwlink/?LinkId=107381)합니다.  
  
## <a name="metadata"></a>메타데이터  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 각 서버 인스턴스의 백업 및 복원 작업을 추적하는 백업 및 복원 기록 테이블이 있습니다. 복원을 수행하면 백업 기록 테이블도 수정됩니다. 이러한 테이블에 대 한 자세한 내용은 참조 [백업 기록 및 헤더 정보 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md).  
  
##  <a name="REPLACEoption"></a>REPLACE 옵션의 영향  
 REPLACE는 신중한 검토 후에만 사용해야 하며 되도록 사용하지 않아야 합니다. 복원은 보통 실수로 복원 중 다른 데이터베이스로 현재 데이터베이스를 덮어쓰는 일을 방지합니다. RESTORE 문에서 지정된 데이터베이스가 현재 서버에 이미 존재하고 지정된 데이터베이스 패밀리 GUID가 백업 세트에 기록된 데이터베이스 패밀리 GUID와 다르면 해당 데이터베이스는 복원되지 않습니다. 이것은 중요한 보호 수단입니다.  
  
 REPLACE 옵션은 복원 작업 중 일반적으로 수행하는 몇 가지 중요한 안전성 검사를 무시합니다. 무시되는 검사는 다음과 같습니다.  
  
-   다른 데이터베이스의 백업으로 기존 데이터베이스 복원  
  
     REPLACE 옵션을 사용하면 복원 중에 백업 세트에 있는 데이터베이스가 어떤 것이든 관계 없이 해당 데이터베이스로 기존 데이터베이스를 덮어쓸 수 있습니다. 심지어 지정된 데이터베이스 이름이 백업 세트에 기록된 데이터베이스 이름과 다른 경우에도 마찬가지입니다. 이로 인해 실수로 다른 데이터베이스로 데이터베이스를 덮어쓰는 경우가 생길 수 있습니다.  
  
-   비상 로그 백업을 수행하지 않았고 STOPAT 옵션을 사용하지 않은 상태에서 전체 또는 대량 로그 복구 모델을 사용한 데이터베이스 복원  
  
     최근에 기록된 로그가 백업되지 않았으므로 REPLACE 옵션을 사용하면 커밋된 작업이 손실될 수 있습니다.  
  
-   기존 파일 덮어쓰기  
  
     예를 들어 .xls 파일과 같은 잘못된 유형의 파일 또는 현재 온라인 상태가 아닌 다른 데이터베이스에서 사용 중인 파일을 덮어쓸 수 있습니다. 데이터 복원이 완료되어도 기존 파일을 덮어쓴 경우에는 임의의 데이터 손실이 발생할 수 있습니다.  
  
## <a name="redoing-a-restore"></a>복원 다시 실행  
 복원 결과는 실행 취소할 수 없지만 데이터 복사 결과를 무시하고 파일 단위로 다시 시작하여 롤포워드할 수 있습니다. 다시 시작하려면 원하는 파일을 복원하고 롤포워드를 다시 수행하십시오. 예를 들어 실수로 너무 많은 로그 백업을 복원하고 원하는 중지 지점을 지난 경우에는 해당 시퀀스를 다시 시작해야 합니다.  
  
 복원 시퀀스를 중단하고 영향을 받는 파일의 전체 내용을 복원하여 다시 시작할 수 있습니다.  
  
## <a name="reverting-a-database-to-a-database-snapshot"></a>데이터베이스를 데이터베이스 스냅숏으로 되돌리기  
 A *데이터베이스 되돌리기 작업* (지정 된가 사용 하 여 DATABASE_SNAPSHOT 옵션)은 전체 원본 데이터베이스에서 시간에서 지점에서 데이터를 원본 데이터베이스를 덮어쓰는 즉, 데이터베이스 스냅숏에서 되돌리기 시간에서 지정한 데이터베이스 스냅숏에 유지 관리 합니다. 현재 되돌리는 스냅숏만 있을 수 있습니다. 그런 다음 되돌리기 작업은 로그를 다시 작성하므로 되돌린 데이터베이스를 사용자 오류 발생 지점으로 나중에 롤포워드할 수 없습니다.  
  
 데이터 손실은 스냅숏 생성 이후의 데이터베이스 업데이트로 제한됩니다. 되돌린 데이터베이스의 메타데이터는 스냅숏 생성 시의 메타데이터와 동일합니다. 그러나 스냅숏으로 되돌리면 전체 텍스트 카탈로그가 모두 삭제됩니다.  
  
 데이터베이스 스냅숏에서 되돌리기는 미디어 복구용으로 사용할 수 없습니다. 일반 백업 세트와는 달리 데이터베이스 스냅숏은 데이터베이스 파일의 불완전한 복사본입니다. 데이터베이스나 데이터베이스 스냅숏이 손상된 경우 스냅숏에서 되돌릴 수 없는 경우가 많습니다. 되돌릴 수 있는 경우에도 손상 문제가 해결될 가능성은 거의 없습니다.  
  
### <a name="restrictions-on-reverting"></a>되돌리기 제한 사항  
 다음과 같은 경우에는 되돌리기가 지원되지 않습니다.  
  
-   원본 데이터베이스에는 읽기 전용 파일 그룹이나 압축 파일 그룹이 포함되어 있는 경우  
  
-   스냅숏이 만들어질 때 온라인 상태였던 파일이 오프라인 상태인 경우  
  
-   현재 데이터베이스에 대한 스냅숏이 여러 개 있는 경우  
  
 자세한 내용은 참조 [데이터베이스를 데이터베이스 스냅숏으로 되돌리기](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)합니다.  
  
## <a name="security"></a>보안  
 백업 작업은 미디어 세트, 백업 세트 또는 이 둘 모두에 대해 암호를 지정할 수 있습니다. 미디어 세트나 백업 세트에 암호가 정의되어 있는 경우 RESTORE 문에서 정확한 암호를 지정해야 합니다. 이러한 암호를 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 무단으로 복원 작업을 수행하거나 미디어에 백업 세트를 무단으로 추가하는 작업을 방지할 수 있습니다. 그러나 암호로 보호된 미디어는 BACKUP 문의 FORMAT 옵션으로 덮어쓸 수 있습니다.  
  
> [!IMPORTANT]  
>  이 암호에 의한 보호 수준은 낮습니다. 권한 유무에 관계없이 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 잘못된 복원을 수행하는 것을 방지합니다. 다른 수단을 사용한 백업 데이터 읽기나 암호 바꾸기를 방지하지는 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]백업을 보호 하는 것에 대 한 백업 테이프를 저장 하 여 안전한 위치에 또는 디스크 파일에 적절 한 액세스 제어 목록 (Acl)로 보호 되는 백업 하는 것이 좋습니다. ACL은 백업이 만들어지는 디렉터리 루트에 설정해야 합니다.  
>   
>  Windows Azure Blob 저장소로 SQL Server 백업 및 복원에 관련 된 정보를 참조 하십시오. [SQL Server 백업 및 Microsoft Azure Blob 저장소 서비스로 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)합니다.  
  
### <a name="permissions"></a>Permissions  
 복원할 데이터베이스가 없으면 CREATE DATABASE 권한이 있어야 RESTORE를 실행할 수 있습니다. 데이터베이스가 있으면 RESTORE 권한은 기본적으로 **sysadmin** 및 **dbcreator** 고정 서버 역할의 멤버와 데이터베이스의 소유자(**dbo**)에 설정됩니다. FROM DATABASE_SNAPSHOT 옵션의 경우 데이터베이스가 항상 있습니다.  
  
 멤버 자격 정보를 서버에서 항상 사용할 수 있는 역할에 RESTORE 권한이 제공됩니다. 고정 데이터베이스 역할의 멤버 자격은 데이터베이스가 액세스 가능한 상태이며 손상되지 않은 경우에만 확인할 수 있는데, RESTORE 실행 시 데이터베이스가 항상 이러한 상태인 것은 아니므로 **db_owner** 고정 데이터베이스 역할의 멤버에게는 RESTORE 권한이 없습니다.  
  
##  <a name="examples"></a> 예  
 모든 예에서는 전체 데이터베이스 백업을 수행한 것으로 가정합니다.  
  
 RESTORE 예에는 다음이 포함됩니다.  
  
-   1. [전체 데이터베이스 복원](#restoring_full_db)  
  
-   2. [전체 및 차등 데이터베이스 백업 복원](#restoring_full_n_differential_db_backups)  
  
-   3. [RESTART 구문을 사용 하 여 데이터베이스 복원](#restoring_db_using_RESTART)  
  
-   4. [복원 된 데이터베이스 및 파일 이동](#restoring_db_n_move_files)  
  
-   5. [백업과 복원을 사용 하 여 데이터베이스 복사](#copying_db_using_bnr)  
  
-   6. [STOPAT를 사용하여 지정 시간으로 복원](#restoring_to_pit_using_STOPAT)  
  
-   7. [트랜잭션 로그 표시로 복원](#restoring_transaction_log_to_mark)  
  
-   8. [TAPE 구문을 사용 하 여 복원](#restoring_using_TAPE)  
  
-   9. [FILE 및 FILEGROUP 구문을 사용 하 여 복원](#restoring_using_FILE_n_FG)  
  
-   10. [데이터베이스 스냅숏으로 되돌리기](#reverting_from_db_snapshot)  
  
-   11. [Microsoft Azure Blob 저장소 서비스에서 복원](#Azure_Blob)  
  
> **참고:** 추가 예에 나열 된 복원 방법 도움말 항목을 참조 하십시오. [복원 및 복구 개요 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
###  <a name="restoring_full_db"></a> 1. 전체 데이터베이스 복원  
 다음 예에서는 `AdventureWorksBackups` 논리적 백업 장치에서 전체 데이터베이스 백업을 복원합니다. 이 장치를 만드는 예제를 보려면 [백업 장치](../../relational-databases/backup-restore/backup-devices-sql-server.md)합니다.  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM AdventureWorks2012Backups;  
```  
  
> **참고:** 전체 또는 대량 로그 복구 모델을 사용 하 여 데이터베이스에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 복원 하기 전에 비상 로그를 백업 하는 대부분의 경우 필요 합니다. 자세한 내용은 [비상 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 참조하세요.  
  
 [&#91;이 고, 이러한 예 &#93;의 맨 위에](#examples)  
  
###  <a name="restoring_full_n_differential_db_backups"></a> 2. 전체 및 차등 데이터베이스 백업 복원  
 다음 예에서는 `Z:\SQLServerBackups\AdventureWorks2012.bak` 백업 장치에서 전체 데이터베이스 백업을 복원한 다음 차등 백업을 복원합니다. 이 백업 장치에는 전체 데이터베이스 백업 및 차등 백업이 모두 포함되어 있습니다. 이 백업 장치에는 전체 데이터베이스 백업 및 차등 백업이 모두 포함되어 있습니다. 복원할 전체 데이터베이스 백업은 장치의 6번째 백업 세트(`FILE = 6`)이고 차등 데이터베이스 백업은 장치의 9번째 백업 세트(`FILE = 9`)입니다. 차등 백업이 복구되면 바로 데이터베이스가 복구됩니다.  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH FILE = 6  
      NORECOVERY;  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH FILE = 9  
      RECOVERY;  
```  
  
 [&#91;이 고, 이러한 예 &#93;의 맨 위에](#examples)  
  
###  <a name="restoring_db_using_RESTART"></a> 3. RESTART 구문을 사용하여 데이터베이스 복원  
 다음 예에서는 `RESTART` 옵션을 사용하여 서버 전원 고장으로 중단된 `RESTORE` 작업을 다시 시작합니다.  
  
```  
-- This database RESTORE halted prematurely due to power failure.  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups;  
-- Here is the RESTORE RESTART operation.  
RESTORE DATABASE AdventureWorks2012   
   FROM AdventureWorksBackups WITH RESTART;  
```  
  
 [&#91;이 고, 이러한 예 &#93;의 맨 위에](#examples)  
  
###  <a name="restoring_db_n_move_files"></a> 4. 데이터베이스 복원 및 파일 이동  
 다음 예에서는 전체 데이터베이스와 트랜잭션 로그를 복원하고 복원된 데이터베이스를 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data` 디렉터리로 이동합니다.  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH NORECOVERY,   
      MOVE 'AdventureWorks2012_Data' TO   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\NewAdvWorks.mdf',   
      MOVE 'AdventureWorks2012_Log'   
TO 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\NewAdvWorks.ldf';  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH RECOVERY;  
```  
  
 [&#91;이 고, 이러한 예 &#93;의 맨 위에](#examples)  
  
###  <a name="copying_db_using_bnr"></a> 5. BACKUP 및 RESTORE를 사용하여 데이터베이스 복사  
 다음 예에서는 `BACKUP` 및 `RESTORE` 문을 사용하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 복사본을 만듭니다. `MOVE` 문을 사용하면 데이터와 로그 파일이 지정한 위치로 복원됩니다. `RESTORE FILELISTONLY` 문은 복원할 데이터베이스에 있는 파일의 수와 이름을 확인하는 데 사용합니다. 데이터베이스의 새 복사본 이름은 `TestDB`입니다. 자세한 내용은 [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)를 참조하세요.  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO AdventureWorksBackups ;  
  
RESTORE FILELISTONLY   
   FROM AdventureWorksBackups ;  
  
RESTORE DATABASE TestDB   
   FROM AdventureWorksBackups   
   WITH MOVE 'AdventureWorks2012_Data' TO 'C:\MySQLServer\testdb.mdf',  
   MOVE 'AdventureWorks2012_Log' TO 'C:\MySQLServer\testdb.ldf';  
GO  
```  
  
 [&#91;이 고, 이러한 예 &#93;의 맨 위에](#examples)  
  
###  <a name="restoring_to_pit_using_STOPAT"></a> 6. STOPAT를 사용하여 지정 시간으로 복원  
 다음 예에서는 `12:00 AM` , `April 15, 2020` 상태로 데이터베이스를 복원하고 여러 로그 백업이 연관된 복원 작업을 보여 줍니다. 백업 장치 `AdventureWorksBackups`에서 복원할 전체 데이터베이스 백업은 해당 장치의 세 번째 백업 세트(`FILE = 3`)이고, 첫 번째 로그 백업은 네 번째 백업 세트(`FILE = 4`)이고, 두 번째 로그 백업은 다섯 번째 백업 세트(`FILE = 5`)입니다.  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=3, NORECOVERY;  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=4, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=5, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
RESTORE DATABASE AdventureWorks2012 WITH RECOVERY;  
  
```  
  
 [&#91;이 고, 이러한 예 &#93;의 맨 위에](#examples)  
  
###  <a name="restoring_transaction_log_to_mark"></a> G. 트랜잭션 로그를 표시까지 복원  
 다음 예에서는 트랜잭션 로그를 복원하여 `ListPriceUpdate`라는 표시된 트랜잭션에 나타냅니다.  
  
```  
USE AdventureWorks2012  
GO  
BEGIN TRANSACTION ListPriceUpdate  
   WITH MARK 'UPDATE Product list prices';  
GO  
  
UPDATE Production.Product  
   SET ListPrice = ListPrice * 1.10  
   WHERE ProductNumber LIKE 'BK-%';  
GO  
  
COMMIT TRANSACTION ListPriceUpdate;  
GO  
  
-- Time passes. Regular database   
-- and log backups are taken.  
-- An error occurs in the database.  
USE master;  
GO  
  
RESTORE DATABASE AdventureWorks2012  
FROM AdventureWorksBackups  
WITH FILE = 3, NORECOVERY;  
GO  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups   
   WITH FILE = 4,  
   RECOVERY,   
   STOPATMARK = 'UPDATE Product list prices';  
```  
  
 [&#91;이 고, 이러한 예 &#93;의 맨 위에](#examples)  
  
###  <a name="restoring_using_TAPE"></a> H. TAPE 구문을 사용하여 복원  
 다음 예에서는 `TAPE` 백업 장치에서 전체 데이터베이스 백업을 복원합니다.  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM TAPE = '\\.\tape0';  
```  
  
 [&#91;이 고, 이러한 예 &#93;의 맨 위에](#examples)  
  
###  <a name="restoring_using_FILE_n_FG"></a> I. FILE 및 FILEGROUP 구문을 사용하여 복원  
 다음 예에서는 하나의 보조 파일 그룹과 하나의 트랜잭션 로그인 두 파일이 있는 `MyDatabase`라는 데이터베이스를 복원합니다. 이 데이터베이스는 전체 복구 모델을 사용합니다.  
  
 데이터베이스 백업은 `MyDatabaseBackups`라는 논리적 백업 장치에 있는 미디어 세트의 9번째 백업 세트입니다. 그런 다음 `10` 장치의 다음 3개 백업 세트(`11`, `12` 및 `MyDatabaseBackups`)에 있는 3개 로그 백업이 `WITH NORECOVERY`를 사용하여 복원됩니다. 마지막 로그 백업을 복원한 다음 데이터베이스가 복구됩니다.  
  
> **참고:** 백업이 복원 되기 전에 모든 로그, 복구 너무 빨리 복구 가능성을 줄이기 위해 별도 단계로 수행 됩니다.  
  
 `RESTORE DATABASE`에는 두 가지 유형의 `FILE` 옵션이 있습니다. 백업 장치 이름 앞에 있는 `FILE` 옵션은 백업 세트에서 복원될 데이터베이스 파일의 논리적 파일 이름을 지정합니다(예: `FILE = 'MyDatabase_data_1'`). 이 백업 세트는 미디어 세트의 첫 번째 데이터베이스 백업이 아니므로 미디어 세트에서의 해당 위치는 `FILE` 절의 `WITH` 옵션인 `FILE=9`를 사용하여 나타냅니다.  
  
```  
RESTORE DATABASE MyDatabase  
   FILE = 'MyDatabase_data_1',  
   FILE = 'MyDatabase_data_2',  
   FILEGROUP = 'new_customers'  
   FROM MyDatabaseBackups  
   WITH   
      FILE = 9,  
      NORECOVERY;  
GO  
-- Restore the log backups.  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 10,   
      NORECOVERY;  
GO  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 11,   
      NORECOVERY;  
GO  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 12,   
      NORECOVERY;  
GO  
--Recover the database:  
RESTORE DATABASE MyDatabase WITH RECOVERY;  
GO  
```  
  
 [&#91;이 고, 이러한 예 &#93;의 맨 위에](#examples)  
  
###  <a name="reverting_from_db_snapshot"></a> J. 데이터베이스 스냅숏으로 되돌리기  
 다음 예에서는 데이터베이스를 데이터베이스 스냅숏으로 되돌립니다. 이 예에서는 현재 하나의 스냅숏만 데이터베이스에 있는 것으로 가정합니다. 이 데이터베이스 스냅숏을 만드는 방법의 예제를 보려면 [데이터베이스 스냅숏 &#40; 만들기 Transact SQL &#41; ](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
> **참고:** 스냅숏으로 되돌리기 모든 전체 텍스트 카탈로그를 삭제 합니다.  
  
```  
USE master;    
RESTORE DATABASE AdventureWorks2012 FROM DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
 자세한 내용은 참조 [데이터베이스를 데이터베이스 스냅숏으로 되돌리기](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)합니다.  

 [&#91;이 고, 이러한 예 &#93;의 맨 위에](#examples)  
  
###  <a name="Azure_Blob"></a> K. Microsoft Azure Blob 저장소 서비스에서 복원  
아래 세 가지 예제에는 Microsoft Azure 저장소 서비스 사용 작업이 포함 됩니다.  저장소 계정 이름은 `mystorageaccount`입니다.  데이터 파일에 대 한 컨테이너 라고 `myfirstcontainer`합니다.  백업 파일에 대 한 컨테이너 라고 `mysecondcontainer`합니다.  각 컨테이너에 대 한 읽기, 쓰기, 삭제 및 목록으로 저장된 된 액세스 정책을 만들었습니다.  저장 된 액세스 정책은 연관 된 공유 액세스 서명을 사용 하 여 SQL Server 자격 증명을 만들었습니다.  Microsoft Azure Blob 저장소로 SQL Server 백업 및 복원에 관련 된 정보를 참조 하십시오. [SQL Server 백업 및 Microsoft Azure Blob 저장소 서비스로 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)합니다.  

**K1.  Microsoft Azure 저장소 서비스에서 전체 데이터베이스 백업 복원**  
전체 데이터베이스 백업에 있는 `mysecondcontainer`의 `Sales` 으로 복원 됩니다 `myfirstcontainer`합니다.  `Sales`서버에 현재 존재 하지 않습니다. 
```
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'   
  WITH  MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf', 
  STATS = 10;
```

**K2. 로컬 저장소에 Microsoft Azure 저장소 서비스에서 전체 데이터베이스 백업 복원**  
전체 데이터베이스 백업에 있는 `mysecondcontainer`의 `Sales` 로컬 저장소에 복원 됩니다.  `Sales`서버에 현재 존재 하지 않습니다.
```
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'   
  WITH  MOVE 'Sales_Data1' to 'H:\DATA\Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'O:\LOG\Sales_log.ldf', 
  STATS = 10;
```
  
**K3. Microsoft Azure 저장소 서비스에 로컬 저장소에서 전체 데이터베이스 백업 복원**  
```
RESTORE DATABASE Sales
  FROM DISK = 'E:\BAK\Sales.bak'
  WITH  MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf', 
  STATS = 10;
```  
  

  
 [&#91;이 고, 이러한 예 &#93;의 맨 위에](#examples)  
  
## <a name="much-more-information"></a>훨씬 더 많은 정보!!  
 - [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) 
- [백업 및 복원 시스템 데이터베이스 (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md) 
 - [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
 - [전체 텍스트 카탈로그와 인덱스 백업 및 복원](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 - [복제된 데이터베이스 백업 및 복원](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 - [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 - [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 - [RESTORE rewindonly&#40; Transact SQL &#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 - [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 - [RESTORE FILELISTONLY (Transact SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
 - [RESTORE HEADERONLY (Transact SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
 - [백업 기록 및 헤더 정보&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
