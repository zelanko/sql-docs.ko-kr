---
title: backupset (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupset
- backupset_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backupset system table
- backup media [SQL Server], backupset system table
- backup sets [SQL Server]
ms.assetid: 6ff79bbf-4acf-4f75-926f-38637ca8a943
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0eb367dd29a96f5819563f0b10e036b7274c4303
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827381"
---
# <a name="backupset-transact-sql"></a>backupset(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  각 백업 세트마다 하나의 행을 포함합니다. *백업 세트*에는 하나의 성공한 백업 작업의 백업이 포함됩니다. RESTORE, RESTORE FILELISTONLY, RESTORE HEADERONLY 및 RESTORE VERIFYONLY 문은 지정한 백업 디바이스의 미디어 세트 내에 있는 단일 백업 세트에서 작동합니다.  
  
 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|백업 세트를 식별하는 고유한 백업 세트 ID입니다. ID, 즉 기본 키입니다.|  
|**backup_set_uuid**|**uniqueidentifier**|백업 세트를 식별하는 고유한 백업 세트 ID입니다.|  
|**media_set_id**|**int**|백업 세트를 포함한 미디어 세트를 식별하는 고유한 미디어 세트 ID입니다. **Backupmediaset (media_set_id)** 를 참조 합니다.|  
|**first_family_number**|**tinyint**|백업 세트가 시작되는 미디어의 패밀리 번호입니다. NULL일 수 있습니다.|  
|**first_media_number**|**smallint**|백업 세트가 시작되는 미디어의 미디어 번호입니다. NULL일 수 있습니다.|  
|**last_family_number**|**tinyint**|백업 세트가 끝나는 미디어의 패밀리 번호입니다. NULL일 수 있습니다.|  
|**last_media_number**|**smallint**|백업 세트가 끝나는 미디어의 미디어 번호입니다. NULL일 수 있습니다.|  
|**catalog_family_number**|**tinyint**|백업 세트 디렉터리의 시작을 포함한 미디어의 패밀리 번호입니다. NULL일 수 있습니다.|  
|**catalog_media_number**|**smallint**|백업 세트 디렉터리의 시작을 포함한 미디어의 미디어 번호입니다. NULL일 수 있습니다.|  
|**놓을**|**int**|적절한 백업 세트 및 파일의 위치를 찾기 위해 복원 작업에 사용되는 백업 세트 위치입니다. NULL일 수 있습니다. 자세한 내용은 백업에서 파일 [&#40;transact-sql&#41;](../../t-sql/statements/backup-transact-sql.md)을 참조 하세요.|  
|**expiration_date**|**datetime**|백업 세트가 만료되는 날짜 및 시간입니다. NULL일 수 있습니다.|  
|**software_vendor_id**|**int**|백업 미디어 헤더를 기록하는 소프트웨어 공급업체의 ID입니다. NULL일 수 있습니다.|  
|**name**|**nvarchar(128)**|백업 세트의 이름입니다. NULL일 수 있습니다.|  
|**한**|**nvarchar(255)**|백업 세트에 관한 설명입니다. NULL일 수 있습니다.|  
|**user_name**|**nvarchar(128)**|백업 작업을 수행하는 사용자의 이름입니다. NULL일 수 있습니다.|  
|**software_major_version**|**tinyint**|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]주 버전 번호입니다. NULL일 수 있습니다.|  
|**software_minor_version**|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 부 버전 번호입니다. NULL일 수 있습니다.|  
|**software_build_version**|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 빌드 번호입니다. NULL일 수 있습니다.|  
|**time_zone**|**smallint**|15분 간격으로 백업 작업이 수행되는 현지 시간과 UCT 간의 차이입니다. 값은 -48에서 +48까지 사용할 수 있으며 각 값을 포함합니다. 값 127은 알 수 없음을 의미합니다. 예를 들어 -20은 EST(동부 표준시) 또는 UTC 이후 5시간을 의미합니다. NULL일 수 있습니다.|  
|**mtf_minor_version**|**tinyint**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format의 부 버전 번호입니다. NULL일 수 있습니다.|  
|**first_lsn**|**numeric(25,0)**|백업 세트에서 첫 번째 또는 가장 오래된 로그 레코드의 로그 시퀀스 번호입니다. NULL일 수 있습니다.|  
|**last_lsn**|**numeric(25,0)**|백업 세트 다음에 오는 로그 레코드의 로그 시퀀스 번호입니다. NULL일 수 있습니다.|  
|**checkpoint_lsn**|**numeric(25,0)**|다시 실행이 시작되어야 하는 로그 레코드의 로그 시퀀스 번호입니다. NULL일 수 있습니다.|  
|**database_backup_lsn**|**numeric(25,0)**|가장 최근 전체 데이터베이스 백업의 로그 시퀀스 번호입니다. NULL일 수 있습니다.<br /><br /> **database_backup_lsn** 은 백업이 시작 될 때 트리거되는 "검사점의 시작"입니다. 데이터베이스가 유휴 상태이 고 복제가 구성 되지 않은 경우 백업이 수행 되 면이 LSN은 **first_lsn** 와 일치 합니다.|  
|**database_creation_date**|**datetime**|데이터베이스가 원래 생성된 날짜와 시간입니다. NULL일 수 있습니다.|  
|**backup_start_date**|**datetime**|백업 작업이 시작된 날짜와 시간입니다. NULL일 수 있습니다.|  
|**backup_finish_date**|**datetime**|백업 작업이 완료된 날짜와 시간입니다. NULL일 수 있습니다.|  
|**type**|**char (1)**|백업 유형입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> D = 데이터베이스<br /><br /> I = 차등 데이터베이스<br /><br /> L = 로그<br /><br /> F = 파일 또는 파일 그룹<br /><br /> G =차등 파일<br /><br /> P = 부분<br /><br /> Q = 차등 부분<br /><br /> NULL일 수 있습니다.|  
|**sort_order**|**smallint**|백업 작업을 수행하는 서버의 정렬 순서입니다. NULL일 수 있습니다. 정렬 순서 및 데이터 정렬에 대 한 자세한 내용은 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)을 참조 하세요.|  
|**code_page**|**smallint**|백업 작업을 수행하는 서버의 코드 페이지입니다. NULL일 수 있습니다. 코드 페이지에 대 한 자세한 내용은 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)을 참조 하세요.|  
|**compatibility_level**|**tinyint**|데이터베이스에 대한 호환성 수준 설정입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> 90 =[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> 100 =[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]<br /><br /> 110 =[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /><br /> 120 =[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]<br /><br /> NULL일 수 있습니다.<br /><br /> 호환성 수준에 대한 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.|  
|**database_version**|**int**|데이터베이스 버전 번호입니다. NULL일 수 있습니다.|  
|**backup_size**|**numeric(20,0)**|백업 세트의 크기(바이트)입니다. NULL일 수 있습니다. VSS 백업의 경우 예상 값은 backup_size입니다.|  
|**database_name**|**nvarchar(128)**|백업 작업과 연관된 데이터베이스의 이름입니다. NULL일 수 있습니다.|  
|**server_name**|**nvarchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 작업을 실행하고 있는 서버의 이름입니다. NULL일 수 있습니다.|  
|**machine_name**|**nvarchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행 중인 컴퓨터의 이름입니다. NULL일 수 있습니다.|  
|**flags**|**int**|에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **flags** 열은 더 이상 사용 되지 않으며 다음 비트 열로 대체 되 고 있습니다.<br /><br /> **has_bulk_logged_data** <br /> **is_snapshot** <br /> **is_readonly** <br /> **is_single_user** <br /> **has_backup_checksums** <br /> **is_damaged** <br /> **begins_log_chain** <br /> **has_incomplete_metadata** <br /> **is_force_offline** <br /> **is_copy_only**<br /><br /> NULL일 수 있습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 백업 세트에서 플래그 비트는 다음과 같습니다.<br />1 = 백업이 최소 기록 데이터를 포함합니다. <br />2 = WITH SNAPSHOT이 사용되었습니다. <br />4 = 백업 시 데이터베이스가 읽기 전용입니다.<br />8 = 백업 시 데이터베이스가 단일 사용자 모드였습니다.|  
|**unicode_locale**|**int**|유니코드 로캘입니다. NULL일 수 있습니다.|  
|**unicode_compare_style**|**int**|유니코드 비교 스타일입니다. NULL일 수 있습니다.|  
|**collation_name**|**nvarchar(128)**|데이터 정렬 이름입니다. NULL일 수 있습니다.|  
|**Is_password_protected**|**bit**|백업 세트입니다.<br /><br /> 다음과 같이 암호로 보호됩니다.<br /><br /> 0 = 보호되지 않음<br /><br /> 1 = 보호됨|  
|**recovery_model**|**nvarchar(60)**|데이터베이스의 복구 모델입니다.<br /><br /> FULL<br /><br /> BULK-LOGGED<br /><br /> SIMPLE|  
|**has_bulk_logged_data**|**bit**|1 = 백업이 대량 로그 데이터를 포함합니다.|  
|**is_snapshot**|**bit**|1 = SNAPSHOT 옵션을 사용하여 백업이 수행되었습니다.|  
|**is_readonly**|**bit**|1 = 백업 시 데이터베이스가 읽기 전용이었습니다.|  
|**is_single_user**|**bit**|1 = 백업 시 데이터베이스가 단일 사용자 모드였습니다.|  
|**has_backup_checksums**|**bit**|1 = 백업이 백업 체크섬을 포함합니다.|  
|**is_damaged**|**bit**|1 = 이 백업이 생성될 때 데이터베이스 손상이 감지되었습니다. 오류와 관계없이 백업 작업을 계속하도록 요청했습니다.|  
|**begins_log_chain**|**bit**|1 = 연속되는 로그 백업 체인에서 첫 번째입니다. 로그 체인은 데이터베이스가 생성된 후 또는 단순 복구 모델에서 전체 또는 대량 로그 복구 모델로 전환될 때 수행된 첫 번째 로그 백업에서 시작됩니다.|  
|**has_incomplete_metadata**|**bit**|1 = 메타데이터가 완전하지 않은 비상 로그 백업입니다. 자세한 내용은 [비상 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 참조하세요.|  
|**is_force_offline**|**bit**|1 = 백업이 수행될 때 NORECOVERY 옵션을 사용하여 데이터베이스가 오프라인 상태가 되었습니다.|  
|**is_copy_only**|**bit**|1 = 복사 전용 백업입니다. 자세한 내용은 [복사 전용 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)를 참조하세요.|  
|**first_recovery_fork_guid**|**uniqueidentifier**|복구 분기 시작 지점의 ID입니다. 이는 RESTORE HEADERONLY의 **Firstrecoveryforkid** 에 해당 합니다.<br /><br /> 데이터 백업의 경우 **first_recovery_fork_guid** **last_recovery_fork_guid**와 같습니다.|  
|**last_recovery_fork_guid**|**uniqueidentifier**|복구 분기 끝 지점의 ID입니다. 이는 RESTORE HEADERONLY의 **Recoveryforkid** 에 해당 합니다.<br /><br /> 데이터 백업의 경우 **first_recovery_fork_guid** **last_recovery_fork_guid**와 같습니다.|  
|**fork_point_lsn**|**numeric(25,0)**|**First_recovery_fork_guid** **last_recovery_fork_guid**같지 않은 경우 분기 지점의 로그 시퀀스 번호입니다. 그렇지 않으면 값은 NULL입니다.|  
|**database_guid**|**uniqueidentifier**|데이터베이스에 대한 고유 ID입니다. 복원 HEADERONLY의 **Bindingid** 에 해당 합니다. 데이터베이스를 복원하면 새 값이 할당됩니다.|  
|**family_guid**|**uniqueidentifier**|생성 시 원래 데이터베이스의 고유 ID입니다. 이 값은 데이터베이스가 다른 이름으로 복원되는 경우에도 동일하게 유지됩니다.|  
|**differential_base_lsn**|**numeric(25,0)**|차등 백업에 대한 기본 LSN입니다. 단일 기반 차등 백업의 경우 **differential_base_lsn** 보다 크거나 같은 lsn의 변경 내용은 차등 백업에 포함 됩니다.<br /><br /> 백업의 경우 차등의 경우 값은 NULL 이며 기본 LSN은 파일 수준에서 결정 해야 합니다 ( [backupfile &#40;transact-sql&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)참조).<br /><br /> 비차등 백업 유형의 경우 값은 항상 NULL입니다.|  
|**differential_base_guid**|**uniqueidentifier**|단일 백업을 기준으로 하는 차등 백업의 경우 값은 차등 기반의 고유 식별자입니다.<br /><br /> 여러 백업을 기반으로 하는 차등 백업의 경우 값은 NULL이며 기본 차등 백업은 파일 수준에서 결정해야 합니다.<br /><br /> 비차등 백업 유형의 경우 값은 NULL입니다.|  
|**compressed_backup_size**|**숫자 (20, 0)**|디스크에 저장된 백업의 총 바이트 수입니다.<br /><br /> 압축 비율을 계산 하려면 **compressed_backup_size** 와 **backup_size**를 사용 합니다.<br /><br /> **Msdb** 를 업그레이드 하는 동안이 값은 NULL로 설정 됩니다. 백업이 압축되지 않았음을 나타냅니다.|  
|**key_algorithm**|**nvarchar(32)**|백업을 암호화하는 데 사용되는 암호화 알고리즘입니다. NO_Encryption 값은 백업이 암호화되지 않았음을 나타냅니다.|  
|**encryptor_thumbprint**|**varbinary(20)**|데이터베이스에서 인증서나 비대칭 키를 찾는 데 사용할 수 있는 암호기의 지문입니다. 백업이 암호화되지 않은 경우 이 값은 NULL입니다.|  
|**encryptor_type**|**nvarchar(32)**|사용한 암호기 유형: 인증서 또는 비대칭 키입니다. . 백업이 암호화되지 않은 경우 이 값은 NULL입니다.|  
  
## <a name="remarks"></a>설명  
 LOADHISTORY를 사용 하는 *backup_device* 에서만 RESTORE verifyonly는 **backupmediaset** 테이블의 열을 미디어 세트 헤더의 적절 한 값으로 채웁니다.  
  
 이 테이블의 행 수와 다른 백업 및 기록 테이블의 행 수를 줄이려면 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) 저장 프로시저를 실행 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;테이블 백업 및 복원](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [백업 및 복원 중 발생 가능한 미디어 오류&#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [Transact-sql&#41;&#40;테이블 백업 및 복원](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)  
  
  
