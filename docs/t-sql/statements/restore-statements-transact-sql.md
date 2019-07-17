---
title: RESTORE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: b673b21eca837e9ccaacd3a47c819287a854e6f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65947048"
---
# <a name="restore-statements-transact-sql"></a>RESTORE 문(Transact-SQL)

BACKUP 명령을 사용하여 만든 SQL 데이터베이스 백업을 복원합니다.

작업 중인 특정 SQL 버전에 대한 구문, 인수, 설명, 사용 권한 및 예제를 보려면 다음 탭 중 하나를 클릭합니다.

구문 표기 규칙에 대한 자세한 내용은 [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)을 참조하십시오.

## <a name="click-a-product"></a>제품을 클릭하세요.

다음 행에서 관심이 있는 제품 이름을 클릭합니다. 클릭하면 여기에서 클릭한 제품에 적절한 다른 콘텐츠를 표시합니다.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

||||
|-|-|-|
|** _\* SQL Server \*_** &nbsp;|[SQL Database<br />관리되는 인스턴스](restore-statements-transact-sql.md?view=azuresqldb-mi-current)|[Analytics Platform<br />System(PDW)](restore-statements-transact-sql.md?view=aps-pdw-2016)
||||

&nbsp;

## <a name="sql-server"></a>SQL Server

이 명령을 사용하면 다음과 같은 복원 시나리오를 수행할 수 있습니다.

- 전체 데이터베이스 백업에서 전체 데이터베이스를 복원합니다(전체 복원).
- 데이터베이스의 일부를 복원합니다(부분 복원).
- 특정 파일 또는 파일 그룹을 데이터베이스로 복원합니다(파일 복원).
- 특정 페이지를 데이터베이스로 복원합니다(페이지 복원).
- 트랜잭션 로그를 데이터베이스로 복원합니다(트랜잭션 로그 복원).
- 데이터베이스 스냅샷에서 캡처한 지점으로 데이터베이스를 되돌립니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복원 시나리오에 대한 자세한 내용은 [복원 및 복구 개요](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)를 참조하세요. 인수 설명에 대한 자세한 내용은 [RESTORE 인수](../../t-sql/statements/restore-statements-arguments-transact-sql.md)를 참조하세요. 다른 인스턴스에서 데이터베이스를 복원할 때 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리(SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)의 정보를 참조하세요.

> [!NOTE]
> Microsoft Azure Blob Storage 서비스에서 복원에 대한 자세한 내용은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요.

## <a name="syntax"></a>구문

```sql
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
   | , \<point_in_time_WITH_options-RESTORE_DATABASE>
   } [ ,...n ]
 ]
[;]

--To perform the first step of the initial restore sequence of a piecemeal restore:
RESTORE DATABASE { database_name | @database_name_var }
   <files_or_filegroups> [ ,...n ]
 [ FROM <backup_device> [ ,...n ] ]
   WITH
      PARTIAL, NORECOVERY
      [  , <general_WITH_options> [ ,...n ]
       | , \<point_in_time_WITH_options-RESTORE_DATABASE>
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
    | , <general_WITH_options> [ ,...n ]
    | , <replication_WITH_option>
    | , \<point_in_time_WITH_options-RESTORE_LOG>
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
 | { DISK
     | TAPE
     | URL
   } = { 'physical_backup_device_name' |
      @physical_backup_device_name_var }
}
Note: URL is the format used to specify the location and the file name for the Microsoft Azure Blob. Although Microsoft Azure storage is a service, the implementation is similar to disk and tape to allow for a consistent and seamless restore experience for all the three devices.
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
 | RESTRICTED_USER | CREDENTIAL

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

--Tape Options.
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

\<point_in_time_WITH_options-RESTORE_DATABASE>::=
 | {
   STOPAT = { 'datetime'| @datetime_var }
 | STOPATMARK = 'lsn:lsn_number'
                 [ AFTER 'datetime']
 | STOPBEFOREMARK = 'lsn:lsn_number'
                 [ AFTER 'datetime']
   }

\<point_in_time_WITH_options-RESTORE_LOG>::=
 | {
   STOPAT = { 'datetime'| @datetime_var }
 | STOPATMARK = { 'mark_name' | 'lsn:lsn_number' }
                 [ AFTER 'datetime']
 | STOPBEFOREMARK = { 'mark_name' | 'lsn:lsn_number' }
                 [ AFTER 'datetime']
   }
```

## <a name="arguments"></a>인수

인수 설명은 [RESTORE 인수](../../t-sql/statements/restore-statements-arguments-transact-sql.md)를 참조하세요.

## <a name="about-restore-scenarios"></a>복원 시나리오

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 다양한 복원 시나리오를 지원합니다.

- 전체 데이터베이스 복원

  전체 데이터베이스 백업에서 시작하여 전체 데이터베이스를 복원한 다음 차등 데이터베이스 백업 및 로그 백업을 복원할 수 있습니다. 자세한 내용은 [전체 데이터베이스 복원 - 단순 복구 모델](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md) 또는 [전체 데이터베이스 복원 - 전체 복구 모델](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)을 참조하세요.

- 파일 복원

  파일 그룹이 여러 개인 데이터베이스에서 파일 또는 파일 그룹을 복원합니다. 단순 복구 모델에서 파일은 읽기 전용 파일 그룹에 속해야 합니다. 전체 파일 복원 후에는 차등 파일 백업을 복원할 수 있습니다. 자세한 내용은 [파일 복원 - 전체 복구 모델](../../relational-databases/backup-restore/file-restores-full-recovery-model.md) 및 [파일 복원 - 단순 복구 모델](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)을 참조하세요.

- 페이지 복원

  개별 페이지를 복원합니다. 페이지 복원은 전체 및 대량 로그 복구 모델에서만 사용할 수 있습니다. 자세한 내용은 [페이지 복원 - SQL Server](../../relational-databases/backup-restore/restore-pages-sql-server.md)를 참조하세요.

- 증분 복원

  주 파일 그룹 및 하나 이상의 보조 파일 그룹에서 시작하여 단계별로 데이터베이스를 복원합니다. 증분 복원은 PARTIAL 옵션을 사용하고 복원할 보조 파일 그룹을 하나 이상 지정하여 RESTORE DATABASE에서 시작합니다. 자세한 내용은 [증분 복원 - SQL Server](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)를 참조하세요.

- 복원만

  데이터베이스와 이미 일치하는 데이터를 복원하여 사용 가능하도록 설정만 하면 됩니다. 자세한 내용은 [데이터를 복원하지 않고 데이터베이스 복구](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)를 참조하세요.

- 트랜잭션 로그 복원

  전체 또는 대량 로그 복구 모델에서는 로그 백업을 복원해야 원하는 복구 지점에 도달할 수 있습니다. 로그 백업 복원에 대한 자세한 내용은 [트랜잭션 로그 백업 적용 - SQL Server](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)를 참조하세요.

- Always On 가용성 그룹을 위한 가용성 데이터베이스 준비

  자세한 내용은 [가용성 그룹에 대한 보조 데이터베이스 수동 준비 - SQL Server](../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)를 참조하세요.

- 데이터베이스 미러링을 위한 미러 데이터베이스 준비

  자세한 내용은 [미러 데이터베이스의 미러링 준비 - SQL Server](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)를 참조하세요.

- 온라인 복원

  > [!NOTE]
  > 온라인 복원은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 엔터프라이즈 버전에서만 허용됩니다.

온라인 복원이 지원되는 경우 데이터베이스가 온라인이면 파일 복원 및 페이지 복원은 자동으로 온라인 복원이 되며 초기 증분 복원을 실행한 다음에는 보조 파일 그룹의 복원이 되기도 합니다.

  > [!NOTE]
  > 온라인 복원에는 [지연된 트랜잭션](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)이 포함될 수 있습니다.

자세한 내용은 [온라인 복원](../../relational-databases/backup-restore/online-restore-sql-server.md)을 참조하세요.

## <a name="additional-considerations-about-restore-options"></a>RESTORE 옵션에 대한 추가 고려 사항

### <a name="discontinued-restore-keywords"></a>지원되지 않는 RESTORE 키워드

다음 키워드는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서 더 이상 지원되지 않습니다.

|지원되지 않는 키워드|다음으로 대체됩니다...|대체 키워드 예|
|--------------------------|------------------|------------------------------------|
|LOAD|RESTORE|`RESTORE DATABASE`|
|TRANSACTION|LOG|`RESTORE LOG`|
|DBO_ONLY|RESTRICTED_USER|`RESTORE DATABASE ... WITH RESTRICTED_USER`|

### <a name="restore-log"></a>RESTORE LOG

RESTORE LOG에 파일 목록을 포함하여 롤포워드 중에 파일을 만들 수 있습니다. 이 기능은 데이터베이스에 파일을 추가할 때 기록된 로그 레코드가 로그 백업에 포함되는 경우에 사용됩니다.

> [!NOTE]
> 전체 또는 대량 로그된 복구 모델을 사용하는 데이터베이스의 경우 대개 데이터베이스를 복원하기 전에 비상 로그 백업을 수행해야 합니다. RESTORE DATABASE 문에 데이터 백업이 종료된 후 발생한 시간 또는 트랜잭션을 지정해야 하는 WITH REPLACE나 WITH STOPAT 절이 포함되어 있지 않은 경우 비상 로그 백업을 먼저 수행하지 않고 데이터베이스를 복원하면 오류가 발생합니다. 비상 로그 백업에 대한 자세한 내용은 [비상 로그 백업](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 참조하세요.

### <a name="comparison-of-recovery-and-norecovery"></a>RECOVERY와 NORECOVERY 비교

RESTORE 문에서 다음과 같이 [ RECOVERY | NORECOVERY ] 옵션을 통해 롤백을 제어합니다.

- NORECOVERY는 롤백이 발생하지 않도록 지정합니다. 이렇게 하면 순서대로 다음 문으로 롤포워드를 계속할 수 있습니다.

  이런 경우 복원 시퀀스는 다른 백업을 복원하여 롤포워드할 수 있습니다.

- RECOVERY(기본값)는 현재 백업에 대해 롤포워드가 완료된 다음 롤백이 수행되어야 한다는 의미입니다.

  데이터베이스를 복구하려면 복원할 전체 데이터 집합(*롤포워드 세트*)가 데이터베이스와 일치해야 합니다. 롤포워드 세트가 데이터베이스와 일치할 만큼 충분히 롤포워드되지 않은 경우 RECOVERY를 지정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류가 발생합니다.

## <a name="compatibility-support"></a>호환성 지원

이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 사용하여 만든 **master**, **model** 및 **msdb** 백업은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 통해 복원할 수 없습니다.

> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업은 백업을 만든 버전 이전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전으로 복원할 수 없습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 각 버전은 이전 버전과는 다른 기본 경로를 사용합니다. 따라서 이전 버전 백업의 기본 위치에 만든 데이터베이스를 복원하려면 MOVE 옵션을 사용해야 합니다. 새 기본 경로에 대한 자세한 내용은 [SQL Server의 기본값 및 명명된 인스턴스에 대한 파일 위치](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)를 참조하세요.

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 이전 버전 데이터베이스를 복원하면 데이터베이스가 자동으로 업그레이드됩니다. 일반적으로 데이터베이스는 즉시 사용할 수 있습니다. 그러나 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스에 전체 텍스트 인덱스가 있는 경우 업그레이드 프로세스는 **upgrade_option** 서버 속성의 설정에 따라 인덱스를 가져오거나 다시 설정하거나 다시 작성합니다. 업그레이드 옵션이 가져오기(**upgrade_option** = 2) 또는 다시 작성(**upgrade_option** = 0)으로 설정되어 있는 경우 업그레이드하는 동안 전체 텍스트 인덱스를 사용할 수 없습니다. 인덱싱되는 데이터 양에 따라 가져오기 작업은 몇 시간씩 걸릴 수 있으며 다시 작성 작업은 10배 정도 더 걸릴 수 있습니다. 업그레이드 옵션이 가져오기로 설정되어 있으면 전체 텍스트 카탈로그를 사용할 수 없는 경우 관련된 전체 텍스트 인덱스가 다시 작성됩니다. **upgrade_option** 서버 속성의 설정을 변경하려면 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)를 사용합니다.

데이터베이스가 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 처음으로 연결되거나 복원될 때 데이터베이스 마스터 키(서비스 마스터 키로 암호화됨)의 복사본은 서버에 아직 저장되지 않은 상태입니다. 데이터베이스 마스터 키를 암호 해독하려면 **OPEN MASTER KEY** 문을 사용해야 합니다. DMK를 암호 해독한 후에는 **ALTER MASTER KEY REGENERATE** 문을 사용하여 SMK(서비스 마스터 키)로 암호화된 DMK의 복사본을 서버에 프로비전함으로써 앞으로 자동 암호 해독을 사용하도록 설정할 수 있습니다. 데이터베이스가 이전 버전에서 업그레이드되지 않은 경우에는 DMK를 다시 생성해야 최신 AES 알고리즘을 사용할 수 있습니다. DMK를 다시 생성하는 방법은 [ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md)를 참조하세요. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 데 소요되는 시간은 DMK에서 보호하는 개체 수에 따라 달라집니다. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 작업은 한 번만 필요하며 키 회전 전략의 일부로 이후에 수행하는 다시 생성 작업에 영향을 주지 않습니다.

## <a name="general-remarks"></a>일반적인 주의 사항

오프라인 복원 시에 지정된 데이터베이스가 사용 중이면 RESTORE는 짧은 지연 후 사용자가 강제로 로그오프되도록 합니다. 주 파일 그룹이 아닌 파일 그룹에 대한 온라인 복원의 경우 복원한 파일 그룹이 오프라인 상태가 되는 경우를 제외하면 데이터베이스는 사용 중 상태로 유지될 수 있습니다. 지정한 데이터베이스의 모든 데이터는 복원된 데이터로 대체됩니다.

데이터베이스에 대한 자세한 내용은 [복원 및 복구 개요](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)를 참조하세요.

플랫폼 간 복원 작업은 서로 다른 프로세서 유형 간 복원 작업인 경우에도 운영 체제에서 데이터베이스의 데이터 정렬을 지원하는 한 수행할 수 있습니다.

오류가 발생하면 RESTORE는 다시 시작할 수 있습니다. 또한 오류와 관계없이 RESTORE가 계속되도록 지시하여 최대한 많은 데이터를 복원할 수 있습니다(CONTINUE_AFTER_ERROR 옵션 참조).

RESTORE는 명시적 또는 암시적 트랜잭션에서 사용할 수 없습니다.

손상된 **master** 데이터베이스는 특별한 프로시저를 사용하여 복원할 수 있습니다. 자세한 내용은 [시스템 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)을 참조하세요.

데이터베이스를 복원하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 계획 캐시가 지워집니다. 계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 "데이터베이스 유지 관리 또는 재구성 작업으로 인해 '%s' 캐시스토어(계획 캐시의 일부)에 대한 캐시스토어 플러시가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 %d번 발견되었습니다"라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.

가용성 데이터베이스를 복원하려면 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 데이터베이스를 복원한 다음 데이터베이스를 가용성 그룹에 추가합니다.

## <a name="interoperability"></a>상호 운용성

### <a name="database-settings-and-restoring"></a>데이터베이스 설정 및 복원

복원 시에는 ALTER DATABASE를 사용하여 설정할 수 있는 대부분의 데이터베이스 옵션이 백업 종료 시에 유효한 값으로 다시 설정됩니다.

그러나 WITH RESTRICTED_USER 옵션을 사용하면 사용자 액세스 옵션 설정 시에 이 동작이 무시됩니다. 이 설정은 항상 WITH RESTRICTED_USER 옵션이 포함되어 있는 RESTORE 문 다음에 지정됩니다.

### <a name="restoring-an-encrypted-database"></a>암호화된 데이터베이스 복원

암호화된 데이터베이스를 복원하려면 데이터베이스를 암호화하는 데 사용된 인증서 또는 비대칭 키에 대한 액세스 권한이 있어야 합니다. 인증서 또는 비대칭 키가 없으면 데이터베이스를 복원할 수 없습니다. 따라서 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서는 백업이 필요한 동안에는 유지되어야 합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.

### <a name="restoring-a-database-enabled-for-vardecimal-storage"></a>VarDecimal 스토리지에 사용할 수 있는 데이터베이스 복원

백업 및 복원은 **vardecimal** 스토리지 형식에서 올바르게 작동합니다. **vardecimal** 스토리지 형식에 대한 자세한 내용은 [sp_db_vardecimal_storage_format](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)을 참조하세요.

### <a name="restore-full-text-data"></a>전체 텍스트 데이터 복원

전체 텍스트 데이터가 전체 복원 시에 다른 데이터베이스 데이터와 함께 복원됩니다. 전체 텍스트 파일은 일반 `RESTORE DATABASE database_name FROM backup_device` 구문을 사용하여 데이터베이스 파일 복원의 일부로 복원됩니다.

또한 RESTORE 문을 사용하여 대체 위치로 복원, 차등 복원, 파일 및 파일 그룹 복원, 전체 텍스트 데이터의 차등 파일 및 파일 그룹 복원을 수행할 수 있습니다. 또한 RESTORE를 사용하면 전체 텍스트 파일만 복원할 수도 있고 데이터베이스 데이터를 함께 복원할 수도 있습니다.

> [!NOTE]
> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 가져온 전체 텍스트 카탈로그는 여전히 데이터베이스 파일로 처리됩니다. 따라서 백업 작업 중에 더 이상 일시 중지하고 재개할 필요가 없다는 점을 제외하고 전체 텍스트 카탈로그를 백업하는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 절차는 계속 적용 가능합니다. 자세한 내용은 [전체 텍스트 카탈로그 백업 및 복원](https://go.microsoft.com/fwlink/?LinkId=107381)을 참조하세요.

## <a name="metadata"></a>메타데이터

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 각 서버 인스턴스의 백업 및 복원 작업을 추적하는 백업 및 복원 기록 테이블이 있습니다. 복원을 수행하면 백업 기록 테이블도 수정됩니다. 이 테이블에 대한 자세한 내용은 [백업 기록 및 헤더 정보](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)를 참조하세요.

## <a name="REPLACEoption"></a> REPLACE 옵션의 영향

REPLACE는 신중한 검토 후에만 사용해야 하며 되도록 사용하지 않아야 합니다. 복원은 보통 실수로 복원 중 다른 데이터베이스로 현재 데이터베이스를 덮어쓰는 일을 방지합니다. RESTORE 문에서 지정된 데이터베이스가 현재 서버에 이미 존재하고 지정된 데이터베이스 패밀리 GUID가 백업 세트에 기록된 데이터베이스 패밀리 GUID와 다르면 해당 데이터베이스는 복원되지 않습니다. 이것은 중요한 보호 수단입니다.

REPLACE 옵션은 복원 작업 중 일반적으로 수행하는 몇 가지 중요한 안전성 검사를 무시합니다. 무시되는 검사는 다음과 같습니다.

- 다른 데이터베이스의 백업으로 기존 데이터베이스 복원

  REPLACE 옵션을 사용하면 복원 중에 백업 세트에 있는 데이터베이스가 어떤 것이든 관계 없이 해당 데이터베이스로 기존 데이터베이스를 덮어쓸 수 있습니다. 심지어 지정된 데이터베이스 이름이 백업 세트에 기록된 데이터베이스 이름과 다른 경우에도 마찬가지입니다. 이로 인해 실수로 다른 데이터베이스로 데이터베이스를 덮어쓰는 경우가 생길 수 있습니다.
  
- 비상 로그 백업을 수행하지 않았고 STOPAT 옵션을 사용하지 않은 상태에서 전체 또는 대량 로그 복구 모델을 사용한 데이터베이스 복원

  최근에 기록된 로그가 백업되지 않았으므로 REPLACE 옵션을 사용하면 커밋된 작업이 손실될 수 있습니다.

- 기존 파일 덮어쓰기

  예를 들어 .xls 파일과 같은 잘못된 유형의 파일 또는 현재 온라인 상태가 아닌 다른 데이터베이스에서 사용 중인 파일을 덮어쓸 수 있습니다. 데이터 복원이 완료되어도 기존 파일을 덮어쓴 경우에는 임의의 데이터 손실이 발생할 수 있습니다.

## <a name="redoing-a-restore"></a>복원 다시 실행

복원 결과는 실행 취소할 수 없지만 데이터 복사 결과를 무시하고 파일 단위로 다시 시작하여 롤포워드할 수 있습니다. 다시 시작하려면 원하는 파일을 복원하고 롤포워드를 다시 수행하십시오. 예를 들어 실수로 너무 많은 로그 백업을 복원하고 원하는 중지 지점을 지난 경우에는 해당 시퀀스를 다시 시작해야 합니다.

복원 시퀀스를 중단하고 영향을 받는 파일의 전체 내용을 복원하여 다시 시작할 수 있습니다.

## <a name="reverting-a-database-to-a-database-snapshot"></a>데이터베이스를 데이터베이스 스냅샷으로 되돌리기

DATABASE_SNAPSHOT 옵션을 사용하여 지정한 *데이터베이스 되돌리기 작업*은 전체 원본 데이터베이스를 데이터베이스 스냅샷 시점으로 되돌려 지정한 데이터베이스 스냅샷에 유지 관리된 시점의 데이터로 원본 데이터베이스를 덮어씁니다. 현재 되돌리는 스냅샷만 있을 수 있습니다. 그런 다음 되돌리기 작업은 로그를 다시 작성하므로 되돌린 데이터베이스를 사용자 오류 발생 지점으로 나중에 롤포워드할 수 없습니다.

데이터 손실은 스냅샷 생성 이후의 데이터베이스 업데이트로 제한됩니다. 되돌린 데이터베이스의 메타데이터는 스냅샷 생성 시의 메타데이터와 동일합니다. 그러나 스냅샷으로 되돌리면 전체 텍스트 카탈로그가 모두 삭제됩니다.

데이터베이스 스냅샷에서 되돌리기는 미디어 복구용으로 사용할 수 없습니다. 일반 백업 세트와는 달리 데이터베이스 스냅샷은 데이터베이스 파일의 불완전한 복사본입니다. 데이터베이스나 데이터베이스 스냅샷이 손상된 경우 스냅샷에서 되돌릴 수 없는 경우가 많습니다. 되돌릴 수 있는 경우에도 손상 문제가 해결될 가능성은 거의 없습니다.

### <a name="restrictions-on-reverting"></a>되돌리기 제한 사항

다음과 같은 경우에는 되돌리기가 지원되지 않습니다.

- 원본 데이터베이스에는 읽기 전용 파일 그룹이나 압축 파일 그룹이 포함되어 있는 경우
- 스냅샷이 만들어질 때 온라인 상태였던 파일이 오프라인 상태인 경우
- 현재 데이터베이스에 대한 스냅샷이 여러 개 있는 경우

자세한 내용은 [데이터베이스를 데이터베이스 스냅샷으로 되돌리기](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)를 참조하세요.

## <a name="security"></a>보안

필요한 경우 백업 작업에서 미디어 세트, 백업 세트 또는 이 둘 모두에 대해 암호를 지정할 수 있습니다. 미디어 세트나 백업 세트에 암호가 정의되어 있는 경우 RESTORE 문에서 정확한 암호를 지정해야 합니다. 이러한 암호를 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 무단으로 복원 작업을 수행하거나 미디어에 백업 세트를 무단으로 추가하는 작업을 방지할 수 있습니다. 그러나 암호로 보호된 미디어는 BACKUP 문의 FORMAT 옵션으로 덮어쓸 수 있습니다.

> [!IMPORTANT]
> 이 암호에 의한 보호 수준은 낮습니다. 권한 유무에 관계없이 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 잘못된 복원을 수행하는 것을 방지합니다. 다른 수단을 사용한 백업 데이터 읽기나 암호 바꾸기를 방지하지는 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]백업을 보호하는 최선의 구현 방법은 백업 테이프를 안전한 장소에 보관하거나 적합한 ACL(액세스 제어 목록)로 보호되는 디스크 파일에 백업하는 것입니다. ACL은 백업이 만들어지는 디렉터리 루트에 설정해야 합니다.
> [!NOTE]
> Microsoft Azure Blob Storage로 SQL Server 백업 및 복원 관련 정보는 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요.

### <a name="permissions"></a>사용 권한

복원할 데이터베이스가 없으면 CREATE DATABASE 권한이 있어야 RESTORE를 실행할 수 있습니다. 데이터베이스가 있으면 RESTORE 권한은 기본적으로 **sysadmin** 및 **dbcreator** 고정 서버 역할의 멤버와 데이터베이스의 소유자(**dbo**)에 설정됩니다. FROM DATABASE_SNAPSHOT 옵션의 경우 데이터베이스가 항상 있습니다.

멤버 자격 정보를 서버에서 항상 사용할 수 있는 역할에 RESTORE 권한이 제공됩니다. 고정 데이터베이스 역할의 멤버 자격은 데이터베이스가 액세스 가능한 상태이며 손상되지 않은 경우에만 확인할 수 있는데, RESTORE 실행 시 데이터베이스가 항상 이러한 상태인 것은 아니므로 **db_owner** 고정 데이터베이스 역할의 멤버에게는 RESTORE 권한이 없습니다.

## <a name="examples"></a> 예

모든 예에서는 전체 데이터베이스 백업을 수행한 것으로 가정합니다.

RESTORE 예에는 다음이 포함됩니다.

- 1\. [전체 데이터베이스 복원](#restoring_full_db)
- 2\. [전체 및 차등 데이터베이스 백업 복원](#restoring_full_n_differential_db_backups)
- C. [RESTART 구문을 사용하여 데이터베이스 복원](#restoring_db_using_RESTART)
- D. [데이터베이스 복원 및 파일 이동](#restoring_db_n_move_files)
- E. [BACKUP 및 RESTORE를 사용하여 데이터베이스 복사](#copying_db_using_bnr)
- F. [STOPAT를 사용하여 지정 시간으로 복원](#restoring_to_pit_using_STOPAT)
- G. [트랜잭션 로그를 표시까지 복원](#restoring_transaction_log_to_mark)
- H. [TAPE 구문을 사용하여 복원](#restoring_using_TAPE)
- 9\. [FILE 및 FILEGROUP 구문을 사용하여 복원](#restoring_using_FILE_n_FG)
- J. [데이터베이스 스냅숏으로 되돌리기](#reverting_from_db_snapshot)
- 11. [Microsoft Azure Blob Storage 서비스에서 복원](#Azure_Blob)

> [!NOTE]
> 추가 예제는 [복원 및 복구 개요](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)에 나열된 복원 방법 항목을 참조하세요.

### <a name="restoring_full_db"></a> 1. 전체 데이터베이스 복원

다음 예에서는 `AdventureWorksBackups` 논리적 백업 장치에서 전체 데이터베이스 백업을 복원합니다. 이 디바이스를 만드는 예는 [백업 디바이스](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 참조하세요.

```sql
RESTORE DATABASE AdventureWorks2012
  FROM AdventureWorks2012Backups;
```

> [!NOTE]
> 전체 또는 대량 로그 복구 모델을 사용하는 데이터베이스의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 대개 데이터베이스를 복원하기 전에 비상 로그 백업을 수행해야 합니다. 자세한 내용은 [비상 로그 백업](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 참조하세요.

[&#91;주요 예제&#93;](#examples)

### <a name="restoring_full_n_differential_db_backups"></a> 2. 전체 및 차등 데이터베이스 백업 복원

다음 예에서는 `Z:\SQLServerBackups\AdventureWorks2012.bak` 백업 장치에서 전체 데이터베이스 백업을 복원한 다음 차등 백업을 복원합니다. 이 백업 장치에는 전체 데이터베이스 백업 및 차등 백업이 모두 포함되어 있습니다. 이 백업 장치에는 전체 데이터베이스 백업 및 차등 백업이 모두 포함되어 있습니다. 복원할 전체 데이터베이스 백업은 장치의 6번째 백업 세트(`FILE = 6`)이고 차등 데이터베이스 백업은 장치의 9번째 백업 세트(`FILE = 9`)입니다. 차등 백업이 복구되면 바로 데이터베이스가 복구됩니다.

```sql
RESTORE DATABASE AdventureWorks2012
    FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'
    WITH FILE = 6
      NORECOVERY;
RESTORE DATABASE AdventureWorks2012
    FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'
    WITH FILE = 9
      RECOVERY;
```

[&#91;주요 예제&#93;](#examples)

### <a name="restoring_db_using_RESTART"></a> 3. RESTART 구문을 사용하여 데이터베이스 복원

다음 예에서는 `RESTART` 옵션을 사용하여 서버 전원 고장으로 중단된 `RESTORE` 작업을 다시 시작합니다.

```sql
-- This database RESTORE halted prematurely due to power failure.
RESTORE DATABASE AdventureWorks2012
    FROM AdventureWorksBackups;
-- Here is the RESTORE RESTART operation.
RESTORE DATABASE AdventureWorks2012
    FROM AdventureWorksBackups WITH RESTART;
```

[&#91;주요 예제&#93;](#examples)

### <a name="restoring_db_n_move_files"></a> 4. 데이터베이스 복원 및 파일 이동

다음 예에서는 전체 데이터베이스와 트랜잭션 로그를 복원하고 복원된 데이터베이스를 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data` 디렉터리로 이동합니다.

```sql
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

[&#91;주요 예제&#93;](#examples)

### <a name="copying_db_using_bnr"></a> 5. BACKUP 및 RESTORE를 사용하여 데이터베이스 복사

다음 예에서는 `BACKUP` 및 `RESTORE` 문을 사용하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 복사본을 만듭니다. `MOVE` 문을 사용하면 데이터와 로그 파일이 지정한 위치로 복원됩니다. `RESTORE FILELISTONLY` 문은 복원할 데이터베이스에 있는 파일의 수와 이름을 확인하는 데 사용합니다. 데이터베이스의 새 복사본 이름은 `TestDB`입니다. 자세한 내용은 [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)를 참조하세요.

```sql
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

[&#91;주요 예제&#93;](#examples)

### <a name="restoring_to_pit_using_STOPAT"></a> 6. STOPAT를 사용하여 지정 시간으로 복원

다음 예에서는 `12:00 AM` , `April 15, 2020` 상태로 데이터베이스를 복원하고 여러 로그 백업이 연관된 복원 작업을 보여 줍니다. 백업 디바이스 `AdventureWorksBackups`에서 복원할 전체 데이터베이스 백업은 해당 디바이스의 세 번째 백업 세트(`FILE = 3`)이고, 첫 번째 로그 백업은 네 번째 백업 세트(`FILE = 4`)이고, 두 번째 로그 백업은 다섯 번째 백업 세트(`FILE = 5`)입니다.

```sql
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

[&#91;주요 예제&#93;](#examples)

### <a name="restoring_transaction_log_to_mark"></a> G. 트랜잭션 로그를 표시까지 복원

다음 예에서는 트랜잭션 로그를 복원하여 `ListPriceUpdate`라는 표시된 트랜잭션에 나타냅니다.

```sql
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

[&#91;주요 예제&#93;](#examples)

### <a name="restoring_using_TAPE"></a> H. TAPE 구문을 사용하여 복원

다음 예에서는 `TAPE` 백업 장치에서 전체 데이터베이스 백업을 복원합니다.

```sql
RESTORE DATABASE AdventureWorks2012
    FROM TAPE = '\\.\tape0';
```

[&#91;주요 예제&#93;](#examples)

### <a name="restoring_using_FILE_n_FG"></a> I. FILE 및 FILEGROUP 구문을 사용하여 복원

다음 예에서는 하나의 보조 파일 그룹과 하나의 트랜잭션 로그인 두 파일이 있는 `MyDatabase`라는 데이터베이스를 복원합니다. 이 데이터베이스는 전체 복구 모델을 사용합니다.

데이터베이스 백업은 `MyDatabaseBackups`라는 논리적 백업 장치에 있는 미디어 세트의 9번째 백업 세트입니다. 그런 다음 `10` 장치의 다음 3개 백업 세트(`11`, `12` 및 `MyDatabaseBackups`)에 있는 3개 로그 백업이 `WITH NORECOVERY`를 사용하여 복원됩니다. 마지막 로그 백업을 복원한 다음 데이터베이스가 복구됩니다.

> [!NOTE]
> 모든 로그 백업이 복원되기 전에 너무 빨리 복구하는 경우를 방지하기 위해 복구 작업은 별도의 단계로 수행됩니다.

`RESTORE DATABASE`에는 두 가지 유형의 `FILE` 옵션이 있습니다. 백업 장치 이름 앞에 있는 `FILE` 옵션은 백업 세트에서 복원될 데이터베이스 파일의 논리적 파일 이름을 지정합니다(예: `FILE = 'MyDatabase_data_1'`). 이 백업 세트는 미디어 세트의 첫 번째 데이터베이스 백업이 아니므로 미디어 세트에서의 해당 위치는 `FILE` 절의 `WITH` 옵션인 `FILE=9`를 사용하여 나타냅니다.

```sql
RESTORE DATABASE MyDatabase
    FILE = 'MyDatabase_data_1',
    FILE = 'MyDatabase_data_2',
    FILEGROUP = 'new_customers'
    FROM MyDatabaseBackups
    WITH
      FILE = 9,
      NORECOVERY;
GO  
-- Restore the log backups
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
--Recover the database
RESTORE DATABASE MyDatabase WITH RECOVERY;
GO
```

[&#91;주요 예제&#93;](#examples)

### <a name="reverting_from_db_snapshot"></a> J. 데이터베이스 스냅샷으로 되돌리기

다음 예에서는 데이터베이스를 데이터베이스 스냅샷으로 되돌립니다. 이 예에서는 현재 하나의 스냅샷만 데이터베이스에 있는 것으로 가정합니다. 이 데이터베이스 스냅샷을 만드는 방법의 예는 [데이터베이스 스냅샷 만들기](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)를 참조하세요.

> [!NOTE]
> 스냅샷으로 되돌리면 전체 텍스트 카탈로그가 모두 삭제됩니다.

```sql
USE master;
RESTORE DATABASE AdventureWorks2012 FROM DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';
GO
```

자세한 내용은 [데이터베이스를 데이터베이스 스냅샷으로 되돌리기](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)를 참조하세요.

[&#91;주요 예제&#93;](#examples)

### <a name="Azure_Blob"></a> K. Microsoft Azure Blob Storage 서비스에서 복원

아래의 세 예제에서는 Microsoft Azure Storage 서비스를 사용하게 됩니다. 스토리지 계정 이름은 `mystorageaccount`입니다. 데이터 파일의 컨테이너는 `myfirstcontainer`입니다. 백업 파일의 컨테이너는 `mysecondcontainer`입니다. 각 컨테이너에 대한 읽기, 쓰기, 삭제 및 나열 권한이 있는 저장된 액세스 정책을 만들었습니다. 저장된 액세스 정책에 연결된 공유 액세스 서명을 사용하여 SQL Server 자격 증명을 만들었습니다. Microsoft Azure Blob Storage로 SQL Server 백업 및 복원 관련 정보는 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요.

**K1. Microsoft Azure Storage 서비스에서 전체 데이터베이스 백업 복원** `Sales`의 `mysecondcontainer`에 있는 전체 데이터베이스 백업이 `myfirstcontainer`로 복원됩니다. `Sales`는 현재 서버에 없습니다.

```sql
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'
  WITH MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf',
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf',
  STATS = 10;
```

**K2. Microsoft Azure Storage 서비스에서 로컬 스토리지로 전체 데이터베이스 백업 복원** `Sales`의 `mysecondcontainer`에 있는 전체 데이터베이스 백업이 로컬 스토리지로 복원됩니다. `Sales`는 현재 서버에 없습니다.

```sql
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'
  WITH MOVE 'Sales_Data1' to 'H:\DATA\Sales_Data1.mdf',
  MOVE 'Sales_log' to 'O:\LOG\Sales_log.ldf',
  STATS = 10;
```

**K3. 로컬 스토리지에서 Microsoft Azure Storage 서비스로 전체 데이터베이스 백업 복원**

```sql
RESTORE DATABASE Sales
  FROM DISK = 'E:\BAK\Sales.bak'
  WITH MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf',
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf',
  STATS = 10;
```

[&#91;주요 예제&#93;](#examples)

## <a name="more-information"></a>자세한 정보

- [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)
- [시스템 데이터베이스 백업 및 복원(SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)
- [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
- [전체 텍스트 카탈로그와 인덱스 백업 및 복원](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)
- [복제된 데이터베이스 백업 및 복원](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)
- [BACKUP](../../t-sql/statements/restore-statements-transact-sql.md)
- [미디어 세트, 미디어 패밀리 및 백업 세트](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)
- [RESTORE REWINDONLY](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)
- [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)
- [RESTORE FILELISTONLY(Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)
- [RESTORE HEADERONLY(Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)
- [백업 기록 및 헤더 정보](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> ||||
> |-|-|-|
> |[SQL Server](restore-statements-transact-sql.md?view=sql-server-2017)|** _\*SQL Database<br />관리되는 인스턴스\*_**|[Analytics Platform<br />System(PDW)](restore-statements-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Azure SQL Database 관리되는 인스턴스

이 명령을 사용하면 Azure Blob Storage 계정의 전체 데이터베이스 백업(전체 복원)에서 전체 데이터베이스를 복원할 수 있습니다.

지원되는 다른 복원 명령은 다음을 참조하세요.

- [RESTORE FILELISTONLY(Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)
- [RESTORE HEADERONLY(Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)
- [RESTORE LABELONLY ONLY(Transact-SQL)](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)
- [RESTORE VERIFYONLY(Transact-SQL)](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)

> [!IMPORTANT]
> Azure SQL Database 관리되는 인스턴스 자동 백업에서 복원하려면 [SQL Database 복원](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups)을 참조하세요.

## <a name="syntax"></a>구문

```sql
--To Restore an Entire Database from a Full database backup (a Complete Restore):
RESTORE DATABASE { database_name | @database_name_var }
 FROM URL = { 'physical_device_name' | @physical_device_name_var } [ ,...n ]
[;]

```

## <a name="arguments"></a>인수

DATABASE

대상 데이터베이스를 지정합니다.

FROM URL

복원 작업에 사용되는 URL에 배치된 하나 이상의 백업 디바이스를 지정합니다. URL 형식은 Microsoft Azure Storage 서비스에서 백업을 복구하는 데 사용됩니다.

> [!IMPORTANT]
> URL에서 복원할 때 여러 디바이스에서 복원하려면 SAS(공유 액세스 서명) 토큰을 사용해야 합니다. 공유 액세스 서명 만들기에 대한 자세한 내용은 [URL에 대한 SQL Server 백업](../../relational-databases/backup-restore/sql-server-backup-to-url.md) 및 [Powershell로 Azure Storage의 SAS(공유 액세스 서명) 토큰이 있는 SQL 자격 증명 만들기 간소화](https://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx)를 참조하세요.

*n* 쉼표로 구분된 목록에 백업 디바이스를 최대 64개까지 지정할 수 있음을 나타내는 자리 표시자입니다.

## <a name="general-remarks"></a>일반적인 주의 사항

전제 조건으로 BLOB 스토리지 계정 URL과 일치하는 이름으로 자격 증명을 만들고, 공유 액세스 서명을 암호로 배치해야 합니다. RESTORE 명령은 BLOB 저장소 URL을 사용하여 자격 증명을 조회하고 백업 디바이스를 읽는 데 필요한 정보를 찾습니다.

RESTORE 작업은 비동기식으로, 클라이언트 연결을 중단하는 경우에도 복원은 계속됩니다. 사용자 연결을 드롭하는 경우 복원 작업의 상태에 대한 [sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) 보기를 확인할 수 있습니다(데이터베이스의 CREATE 및 DROP 경우 포함).

다음 데이터베이스 옵션은 설정/재정의되며 나중에 변경할 수 없습니다.

- NEW_BROKER(broker가 .bak 파일에서 활성화되지 않은 경우)
- ENABLE_BROKER(broker가 .bak 파일에서 활성화되지 않은 경우)
- AUTO_CLOSE=OFF(.bak 파일의 데이터베이스에 AUTO_CLOSE=ON이 있는 경우)
- RECOVERY FULL(.bak 파일의 데이터베이스에 SIMPLE 또는 BULK_LOGGED 복구 모드가 있는 경우)
- 메모리에 최적화된 파일 그룹이 추가되고 원본 .bak 파일에 없는 경우 XTP를 호출합니다. 모든 기존 메모리에 최적화된 파일 그룹은 XTP로 이름이 변경됩니다.
- SINGLE_USER 및 RESTRICTED_USER 옵션은 MULTI_USER로 변환됩니다.

## <a name="limitations---sql-database-managed-instance"></a>제한 사항 - SQL Database 관리되는 인스턴스

다음과 같은 제한이 적용됩니다.

- 여러 백업 세트를 포함하는 .BAK 파일은 복원할 수 없습니다.
- 여러 로그 파일을 포함하는 .BAK 파일은 복원할 수 없습니다.
- .bak에 FILESTREAM 데이터가 포함된 경우 복원이 실패합니다.
- 활성 메모리 내 개체가 있는 데이터베이스를 포함하는 백업은 범용 관리되는 인스턴스로 복원될 수 없습니다.
- 읽기 전용 모드인 데이터베이스를 포함하는 백업은 현재 복원할 수 없습니다. 이 제한 사항은 곧 삭제될 예정입니다.

자세한 내용은 [관리되는 인스턴스](/azure/sql-database/sql-database-managed-instance) 참조

## <a name="restoring-an-encrypted-database"></a>암호화된 데이터베이스 복원

암호화된 데이터베이스를 복원하려면 데이터베이스를 암호화하는 데 사용된 인증서 또는 비대칭 키에 대한 액세스 권한이 있어야 합니다. 인증서 또는 비대칭 키가 없으면 데이터베이스를 복원할 수 없습니다. 따라서 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서는 백업이 필요한 동안에는 유지되어야 합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.

## <a name="permissions"></a>사용 권한

RESTORE를 실행하려면 사용자에게 CREATE DATABASE 권한이 있어야 합니다.

```sql
CREATE LOGIN mylogin WITH PASSWORD = 'Very Strong Pwd123!';
GRANT CREATE ANY DATABASE TO [mylogin];
```

멤버 자격 정보를 서버에서 항상 사용할 수 있는 역할에 RESTORE 권한이 제공됩니다. 고정 데이터베이스 역할의 멤버 자격은 데이터베이스가 액세스 가능한 상태이며 손상되지 않은 경우에만 확인할 수 있는데, RESTORE 실행 시 데이터베이스가 항상 이러한 상태인 것은 아니므로 **db_owner** 고정 데이터베이스 역할의 멤버에게는 RESTORE 권한이 없습니다.

## <a name="examples"></a> 예

다음 예제에서는 URL에서 자격 증명 생성을 비롯한 복사 전용 데이터베이스 백업을 복원합니다.

### <a name="restore-mi-database"></a> 1. 네 개의 백업 디바이스에서 데이터베이스를 복원합니다.

```sql

-- Create credential
CREATE CREDENTIAL [https://mybackups.blob.core.windows.net/wide-world-importers]
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
      SECRET = 'sv=2017-11-09&ss=bq&srt=sco&sp=rl&se=2022-06-19T22:41:07Z&st=2018-06-01T14:41:07Z&spr=https&sig=s7wddcf0w%3D';
GO
-- Restore database
RESTORE DATABASE WideWorldImportersStandard
FROM URL = N'https://mybackups.blob.core.windows.net/wide-world-importers/00-WideWorldImporters-Standard.bak',
URL = N'https://mybackups.blob.core.windows.net/wide-world-importers/01-WideWorldImporters-Standard.bak',
URL = N'https://mybackups.blob.core.windows.net/wide-world-importers/02-WideWorldImporters-Standard.bak',
URL = N'https://mybackups.blob.core.windows.net/wide-world-importers/03-WideWorldImporters-Standard.bak'
```

데이터베이스가 이미 있는 경우 다음 오류가 표시됩니다.

```
Msg 1801, Level 16, State 1, Line 9
Database 'WideWorldImportersStandard' already exists. Choose a different database name.
```

### <a name="restore-mi-database-variables"></a> 2. 변수를 통해 지정된 데이터베이스를 복원합니다.

```sql
DECLARE @db_name sysname = 'WideWorldImportersStandard';
DECLARE @url nvarchar(400) = N'https://mybackups.blob.core.windows.net/wide-world-importers/WideWorldImporters-Standard.bak';

RESTORE DATABASE @db_name
FROM URL = @url
```

### <a name="restore-mi-database-progress"></a> 3. RESTORE 문의 진행 상태를 추적합니다.

```sql
SELECT query = a.text, start_time, percent_complete,
    eta = dateadd(second,estimated_completion_time/1000, getdate())
FROM sys.dm_exec_requests r
    CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) a
WHERE r.command = 'RESTORE DATABASE'
```

> [!Note]
> 이 보기에는 두 개의 복원 요청이 표시될 수 있습니다. 하나는 클라이언트가 보낸 원래 RESTORE 문이고, 다른 하나는 클라이언트 연결에 실패하더라도 실행되는 백그라운드 RESTORE 문입니다.

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

> ||||
> |-|-|-|
> |[SQL Server](restore-statements-transact-sql.md?view=sql-server-2017)|[SQL Database<br />관리되는 인스턴스](restore-statements-transact-sql.md?view=azuresqldb-mi-current)|** _\* Analytics<br />Platform System(PDW) \*_**

&nbsp;

## <a name="analytics-platform-system"></a>분석 플랫폼 시스템

데이터베이스 백업에서 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 어플라이언스로 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 사용자 데이터베이스를 복원합니다. 데이터베이스는 이전에 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] [BACKUP DATABASE - Analytics Platform System](../../t-sql/statements/backup-transact-sql.md) 명령으로 만든 백업에서 복원됩니다. 백업 및 복원 작업을 사용하여 재해 복구 계획을 작성하거나 한 어플라이언스에서 다른 어플라이언스로 데이터베이스를 이동합니다.

> [!NOTE]
> master 복원에는 어플라이언스 로그인 정보 복원이 포함됩니다. master를 복원하려면 **Configuration Manager** 도구의 [master 데이터베이스 복원](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md) 페이지를 사용합니다. 제어 노드에 액세스할 수 있는 관리자가 이 작업을 수행할 수 있습니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스 백업에 대한 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에 있는 “백업 및 복원”을 참조하세요.

## <a name="syntax"></a>구문

```sql

-- Restore the master database
-- Use the Configuration Manager tool.

Restore a full user database backup.
RESTORE DATABASE database_name
    FROM DISK = '\\UNC_path\full_backup_directory'
[;]

--Restore a full user database backup and then a differential backup.
RESTORE DATABASE database_name
    FROM DISK = '\\UNC_path\differential_backup_directory'
    WITH [ ( ] BASE = '\\UNC_path\full_backup_directory' [ ) ]
[;]

--Restore header information for a full or differential user database backup.
RESTORE HEADERONLY
    FROM DISK = '\\UNC_path\backup_directory'
[;]
```

## <a name="arguments"></a>인수

RESTORE DATABASE *database_name* 사용자 데이터베이스를 *database_name*이라는 데이터베이스로 복원하도록 지정합니다. 복원된 데이터베이스 이름은 백업했던 원본 데이터베이스와 다를 수 있습니다. *database_name*은 대상 어플라이언스에 데이터베이스로 이미 존재할 수 없습니다. 허용된 데이터베이스 이름에 대한 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]의 “개체 명명 규칙”을 참조하세요.

사용자 데이터베이스를 복원하면 전체 데이터베이스 백업을 복원한 다음, 선택적으로 차등 백업을 어플라이언스에 복원합니다. 사용자 데이터베이스 복원에는 데이터베이스 사용자 및 데이터베이스 역할이 포함됩니다.

FROM DISK = '\\\\*UNC_path*\\*backup_directory*' [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]가 백업 파일을 복원할 네트워크 경로 및 디렉터리입니다. 예: FROM DISK = ‘\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup’.

*backup_directory* 전체 또는 차등 백업이 포함된 디렉터리의 이름을 지정합니다. 예를 들어 전체 또는 차등 백업에서 RESTORE HEADERONLY 작업을 수행할 수 있습니다.

*full_backup_directory* 전체 백업이 포함된 디렉터리의 이름을 지정합니다.

*differential_backup_directory* 차등 백업이 포함된 디렉터리의 이름을 지정합니다.

- 경로 및 백업 디렉터리는 이미 존재해야 하며 정규화된 UNC(범용 명명 규칙) 경로로 지정해야 합니다.
- 백업 디렉터리 경로는 로컬 경로일 수 없으며 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 어플라이언스 노드의 위치일 수 없습니다.
- UNC 경로 및 백업 디렉터리 이름의 최대 길이는 200자입니다.
- 서버 또는 호스트는 IP 주소로 지정해야 합니다.

RESTORE HEADERONLY 한 명의 사용자 데이터베이스 백업에 대한 헤더 정보만 반환하도록 지정합니다. 다른 필드 간에 헤더의 텍스트 설명 및 백업 이름을 포함합니다. 백업 이름은 백업 파일을 저장하는 디렉터리의 이름과 같을 필요는 없습니다.

RESTORE HEADERONLY 결과는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RESTORE HEADERONLY 결과 뒤에 패턴화됩니다. 결과에는 50개 이상의 열이 있으며 모두 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 사용되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RESTORE HEADERONLY 결과의 열에 대한 설명은 [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)를 참조하세요.

## <a name="permissions"></a>사용 권한

**CREATE ANY DATABASE** 권한이 필요합니다.

백업 디렉터리에 액세스하고 읽을 수 있는 권한이 있는 Windows 계정이 필요합니다. 또한 Windows 계정 이름 및 암호를 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 저장해야 합니다.

- 자격 증명이 이미 있는지 확인하려면 [sys.dm_pdw_network_credentials](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)를 사용합니다.
- 자격 증명을 추가하거나 업데이트하려면 [sp_pdw_add_network_credentials - SQL Data Warehouse](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)를 사용합니다.
- [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 자격 증명을 제거하려면 [sp_pdw_remove_network_credentials - SQL Data Warehouse](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)를 사용합니다.

## <a name="error-handling"></a>오류 처리

RESTORE DATABASE 명령은 다음과 같은 조건에서 오류를 발생시킵니다.

- 저장할 데이터베이스의 이름이 이미 대상 어플라이언스에 있습니다. 이를 방지하려면 고유한 데이터베이스 이름을 선택하거나 복원을 실행하기 전에 기존 데이터베이스를 삭제합니다.
- 백업 디렉터리에 백업 파일의 잘못된 집합이 있습니다.
- 로그인 권한이 데이터베이스를 복원하기에 충분하지 않습니다.
- [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 백업 파일이 저장될 네트워크 위치에 대한 올바른 사용 권한이 없습니다.
- 백업 디렉터리에 대한 네트워크 위치가 존재하지 않거나 사용할 수 없습니다.
- 컴퓨팅 노드 또는 제어 노드에 충분한 디스크 공간이 없습니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 복원을 시작하기 전에 어플라이언스에 충분한 디스크 공간이 있는지를 확인하지 않습니다. 따라서 RESTORE DATABASE 문을 실행하는 동안 디스크 공간 부족 오류가 발생할 가능성이 있습니다. 디스크 공간이 부족하면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 복원을 롤백합니다.
- 데이터베이스를 복원하는 대상 어플라이언스는 데이터베이스를 백업한 원본 어플라이언스보다 컴퓨팅 노드가 더 적습니다.
- 데이터베이스 복원은 트랜잭션 내에서 시도됩니다.

## <a name="general-remarks"></a>일반적인 주의 사항

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 데이터베이스 복원의 성공 여부를 추적합니다. 차등 데이터베이스 백업을 복원하기 전에 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 성공적으로 전체 데이터베이스 복원이 완료되었는지 확인합니다.

복원 후 사용자 데이터베이스는 데이터베이스 호환성 수준 120을 갖게 됩니다. 이는 원래 호환성 수준에 관계 없이 모든 데이터베이스에 마찬가지입니다.

## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>컴퓨팅 노드 수가 더 많은 어플라이언스에 복원

재배포하면 트랜잭션 로그가 증가하므로 작은 어플라이언스에서 큰 어플라이언스로 데이터베이스를 복원한 후 [DBCC SHRINKLOG(Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)를 실행합니다.

컴퓨팅 노드 수가 많은 어플라이언스로 백업을 복원하면 컴퓨팅 노드 수에 비례하여 할당된 데이터베이스 크기가 커집니다.

예를 들어 60GB의 데이터베이스를 2개 노드 어플라이언스(노드당 30GB)에서 6개 노드 어플라이언스로 복원하는 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 6개 노드 어플라이언스에서 180GB 데이터베이스(노드당 30GB의 6개 노드)를 만듭니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 처음에 데이터베이스를 원본 구성에 일치하도록 2개 노드로 복원한 다음, 6개 노드 모두에 데이터를 다시 배포합니다.

재배포 후 각 컴퓨팅 노드는 더 작은 원본 어플라이언스에서 각 컴퓨팅 노드에 비해 더 적은 실제 데이터와 더 많은 여유 공간을 포함하게 됩니다. 데이터베이스에 더 많은 데이터를 추가하려면 추가 공간을 사용합니다. 복원된 데이터베이스 크기가 필요한 것보다 더 큰 경우 [ALTER DATABASE - PDW](../../t-sql/statements/alter-database-transact-sql.md?view=aps-pdw-2016-au7)를 사용하여 데이터베이스 파일 크기를 축소할 수 있습니다.

## <a name="limitations-and-restrictions"></a>제한 사항

이러한 제한 사항의 경우 원본 어플라이언스는 데이터베이스 백업을 만든 어플라이언스이며, 대상 어플라이언스는 데이터베이스를 복원할 어플라이언스입니다.

- 데이터베이스 복원은 통계를 자동으로 빌드하지 않습니다.
- 하나의 RESTORE DATABASE 또는 BACKUP DATABASE 문은 언제든지 어플라이언스에서 실행할 수 있습니다. 동시에 여러 백업 및 복원 명령문이 제출되면 어플라이언스는 이를 큐에 배치하고 한 번에 하나씩 처리합니다.
- 데이터베이스 백업은 원본 어플라이언스에 비해 컴퓨팅 노드가 동일하거나 더 많은 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 대상 어플라이언스에 복원할 수 있습니다. 대상 어플라이언스는 원본 어플라이언스보다 컴퓨팅 노드가 더 많아야 합니다.
- SQL Server 2012 PDW 하드웨어가 있는 어플라이언스에서 만든 백업을 SQL Server 2008 R2 하드웨어가 있는 어플라이언스에 복원할 수 없습니다. 처음에 SQL Server 2008 R2 PDW 하드웨어와 함께 어플라이언스를 구매했고 현재 SQL Server 2012 PDW 소프트웨어를 실행하는 경우에도 마찬가지입니다.

## <a name="locking"></a>잠금

DATABASE 개체에서 배타적 잠금을 사용합니다.

## <a name="examples"></a>예

### <a name="a-simple-restore-examples"></a>1\. 간단한 RESTORE 예

다음 예에서는 전체 백업을 `SalesInvoices2013` 데이터베이스에 복원합니다. 백업 파일은 \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full 디렉터리에 저장됩니다. SalesInvoices2013 데이터베이스는 대상 어플라이언스에 이미 존재할 수 없으며, 그렇지 않으면 이 명령은 오류가 발생하여 실패합니다.

```sql
RESTORE DATABASE SalesInvoices2013
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';
```

### <a name="b-restore-a-full-and-differential-backup"></a>2\. 전체 및 차등 백업 복원

다음 예에서는 SalesInvoices2013 데이터베이스에 전체 및 차등 백업을 차례로 복원합니다.

데이터베이스의 전체 백업은 ‘\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full’ 디렉터리에 저장되는 전체 백업에서 복원됩니다. 복원이 성공적으로 완료되면 차등 백업이 SalesInvoices2013 데이터베이스에 복원됩니다. 차등 백업은 '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff' 디렉터리에 저장됩니다.

```sql
RESTORE DATABASE SalesInvoices2013
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'
[;]

```

### <a name="c-restoring-the-backup-header"></a>C. 백업 헤더 복원

이 예제는 데이터베이스 백업 ‘\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full’에 대한 헤더 정보를 복원합니다. 명령은 Invoices2013Full 백업에 대한 정보에서 하나의 행에 발생합니다.

```sql
RESTORE HEADERONLY
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'
[;]
```

헤더 정보를 사용하여 백업 복원을 시도하기 전에 백업의 콘텐츠를 확인하거나 대상 복원 어플라이언스가 원본 백업 어플라이언스와 호환되는지 확인할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [BACKUP DATABASE - Analytics Platform System](../../t-sql/statements/backup-transact-sql.md?view=aps-pdw-2016-au7)

::: moniker-end
