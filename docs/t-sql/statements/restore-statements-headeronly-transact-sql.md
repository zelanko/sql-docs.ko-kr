---
title: RESTORE HEADERONLY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- HEADERONLY
- RESTORE HEADERONLY
- RESTORE_HEADERONLY_TSQL
- HEADERONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup sets [SQL Server], header information
- headers [SQL Server]
- RESTORE HEADERONLY statement
- backup header information [SQL Server]
ms.assetid: 4b88e98c-49c4-4388-ab0e-476cc956977c
caps.latest.revision: 95
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bb001613cea3dd94131d028329d2fed159b8fc7c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38047092"
---
# <a name="restore-statements---headeronly-transact-sql"></a>RESTORE 문 - HEADERONLY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 특정 백업 장치의 모든 백업 세트에 대한 백업 헤더 정보를 모두 포함하는 결과 집합을 반환합니다. 

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)] 
  
> [!NOTE]  
>  인수에 대한 자세한 설명은 [RESTORE 인수&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
RESTORE HEADERONLY   
FROM <backup_device>   
[ WITH   
 {  
--Backup Set Options  
   FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }    
 } [ ,...n ]  
]  
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | { DISK | TAPE } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
  
## <a name="arguments"></a>인수  
 RESTORE HEADERONLY 인수 설명은 [RESTORE 인수 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)을 참조하세요.  
  
## <a name="result-sets"></a>결과 집합  
 지정한 장치의 각 백업에 대해 서버는 다음 열을 가진 헤더 정보 행을 보냅니다.  
  
> [!NOTE]  
>  RESTORE HEADERONLY는 미디어에 있는 모든 백업 세트를 확인합니다. 따라서 고용량 테이프 드라이브를 사용할 때 이 결과 집합을 생성하면 시간이 오래 걸릴 수 있습니다. 모든 백업 세트에 대한 정보를 가져오지 않고 미디어를 신속하게 확인하려면 RESTORE LABELONLY를 사용하거나 FILE**=** *backup_set_file_number*를 지정합니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 테이프 형식의 특성 때문에 다른 소프트웨어 프로그램의 백업 세트가 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 세트와 동일한 크기의 미디어의 공간을 차지할 수 있습니다. RESTORE HEADERONLY에서 반환한 결과 집합에는 각각의 다른 백업 세트에 대한 행이 포함되어 있습니다.  
  
|열 이름|데이터 형식|SQL Server 백업 세트에 대한 설명|  
|-----------------|---------------|--------------------------------------------|  
|**BackupName**|**nvarchar(128)**|백업 세트 이름|  
|**BackupDescription**|**nvarchar(255)**|백업 세트 설명입니다.|  
|**BackupType**|**smallint**|백업 유형:<br /><br /> **1** = 데이터베이스<br /><br /> **2** = 트랜잭션 로그<br /><br /> **4** = 파일<br /><br /> **5** = 차등 데이터베이스<br /><br /> **6** = 차등 파일<br /><br /> **7** = 부분<br /><br /> **8** = 차등 부분|  
|**ExpirationDate**|**datetime**|백업 세트에 대한 만료 일자|  
|**Compressed**|**BYTE(1)**|소프트웨어 기반 압축을 사용하여 백업 세트를 압축했는지 여부<br /><br /> **0** = 아니요<br /><br /> **1** = 예|  
|**위치**|**smallint**|볼륨에 있는 백업 세트의 위치(FILE = 옵션과 함께 사용)|  
|**DeviceType**|**tinyint**|백업 작업에 사용된 장치 번호<br /><br /> 디스크:<br /><br /> **2** = 논리적<br /><br /> **102** = 물리적<br /><br /> 테이프<br /><br /> **5** = 논리적<br /><br /> **105** = 물리적<br /><br /> 가상 장치<br /><br /> **7** = 논리적<br /><br /> **107** = 물리적<br /><br /> 논리적 장치 이름과 장치 번호는 **sys.backup_devices**에 있습니다. 자세한 내용은 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)을 참조하세요.|  
|**UserName**|**nvarchar(128)**|백업 작업을 수행한 사용자 이름|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar(128)**|백업 세트를 작성한 서버 이름|  
|**DatabaseName**|**nvarchar(128)**|백업한 데이터베이스 이름|  
|**DatabaseVersion**|**int**|백업을 만든 데이터베이스의 버전|  
|**DatabaseCreationDate**|**datetime**|데이터베이스를 만든 날짜와 시간|  
|**BackupSize**|**numeric(20,0)**|바이트 단위의 백업 크기|  
|**FirstLSN**|**numeric(25,0)**|백업 세트에 있는 첫 번째 로그 레코드의 로그 시퀀스 번호|  
|**LastLSN**|**numeric(25,0)**|백업 세트 다음에 오는 로그 레코드의 로그 시퀀스 번호입니다.|  
|**CheckpointLSN**|**numeric(25,0)**|백업 생성 시 가장 최근 검사점의 로그 시퀀스 번호|  
|**DatabaseBackupLSN**|**numeric(25,0)**|가장 최근 전체 데이터베이스 백업의 로그 시퀀스 번호입니다.<br /><br /> **DatabaseBackupLSN**은 백업이 시작될 때 트리거되는 "검사점의 시작"입니다. 데이터베이스가 유휴 상태이고 복제가 구성되지 않은 경우 백업이 수행되면 이 LSN은 **FirstLSN**과 일치하게 됩니다.|  
|**BackupStartDate**|**datetime**|백업 작업이 시작된 날짜와 시간|  
|**BackupFinishDate**|**datetime**|백업 작업이 완료된 날짜와 시간|  
|**SortOrder**|**smallint**|서버 정렬 순서. 이 열은 데이터베이스 백업에만 유효하고 이전 버전과의 호환성을 위해 제공됩니다.|  
|**CodePage**|**smallint**|서버 코드 페이지 또는 서버에서 사용한 문자 집합|  
|**UnicodeLocaleId**|**int**|유니코드 문자 데이터 정렬에 사용한 서버 유니코드 로캘 ID 구성 옵션. 이전 버전과의 호환성을 위해 제공됩니다.|  
|**UnicodeComparisonStyle**|**int**|유니코드 데이터 정렬에 대한 추가 제어를 제공하는 서버 유니코드 비교 스타일 구성 옵션. 이전 버전과의 호환성을 위해 제공됩니다.|  
|**CompatibilityLevel**|**tinyint**|백업을 만든 데이터베이스의 호환성 수준 설정|  
|**SoftwareVendorId**|**int**|소프트웨어 공급업체 ID. SQL Server의 경우 이 번호는 **4608**(또는 16진수 **0x1200**)입니다.|  
|**SoftwareVersionMajor**|**int**|백업 세트를 만든 서버의 주 버전 번호|  
|**SoftwareVersionMinor**|**int**|백업 세트를 만든 서버의 부 버전 번호|  
|**SoftwareVersionBuild**|**int**|백업 세트를 만든 서버의 빌드 번호|  
|**MachineName**|**nvarchar(128)**|백업 작업을 수행한 컴퓨터의 이름|  
|**플래그**|**int**|**1**로 설정된 경우 개별 플래그 비트의 의미는 다음과 같습니다.<br /><br /> **1** = 로그 백업에 대량 로그 작업을 포함합니다.<br /><br /> **2** = 스냅숏 백업입니다.<br /><br /> **4** = 데이터베이스가 읽기 전용으로 백업되었습니다.<br /><br /> **8** = 데이터베이스가 단일 사용자 모드로 백업되었습니다.<br /><br /> **16** = 백업이 백업 체크섬을 포함합니다.<br /><br /> **32** = 백업 시 데이터베이스가 손상되었으나 오류가 있더라도 백업 작업을 계속하도록 요청했습니다.<br /><br /> **64** = 비상 로그 백업입니다.<br /><br /> **128** = 메타데이터가 완전하지 않은 비상 로그 백업입니다.<br /><br /> **256** = NORECOVERY 상태의 비상 로그 백업입니다.<br /><br /> **중요:** **Flags** 대신 개별 Boolean 열을 사용하는 것이 좋습니다. 이 열은 아래의 **HasBulkLoggedData**부터 **IsCopyOnly**까지 나열되어 있습니다.|  
|**BindingID**|**uniqueidentifier**|데이터베이스에 대한 바인딩 ID. 이 열은 **sys.database_recovery_status****database_guid**에 해당됩니다. 데이터베이스를 복원하면 새 값이 할당됩니다. 아래의 **FamilyGUID**를 참조하세요.|  
|**RecoveryForkID**|**uniqueidentifier**|복구 분기 끝 지점의 ID. 이 열은 [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) 테이블의 **last_recovery_fork_guid**에 해당됩니다.<br /><br /> 데이터 백업의 경우 **RecoveryForkID**가 **FirstRecoveryForkID**와 동일합니다.|  
|**데이터 정렬**|**nvarchar(128)**|데이터베이스에서 사용한 데이터 정렬|  
|**FamilyGUID**|**uniqueidentifier**|생성된 원본 데이터베이스의 ID. 이 값은 데이터베이스가 복구될 때와 동일하게 유지됩니다.|  
|**HasBulkLoggedData**|**bit**|**1** = 대량 로그 작업을 포함하는 로그 백업입니다.|  
|**IsSnapshot**|**bit**|**1** = 스냅숏 백업입니다.|  
|**IsReadOnly**|**bit**|**1** = 데이터베이스가 읽기 전용으로 백업되었습니다.|  
|**IsSingleUser**|**bit**|**1** = 데이터베이스가 단일 사용자 모드로 백업되었습니다.|  
|**HasBackupChecksums**|**bit**|**1** = 백업이 백업 체크섬을 포함합니다.|  
|**IsDamaged**|**bit**|**1** = 백업 시 데이터베이스가 손상되었으나 오류가 있더라도 백업 작업을 계속하도록 요청했습니다.|  
|**BeginsLogChain**|**bit**|**1** = 연속되는 로그 백업 체인에서 첫 번째 체인입니다. 로그 체인은 데이터베이스가 생성된 후 또는 단순 복구 모델에서 전체 또는 대량 로그 복구 모델로 전환될 때 수행된 첫 번째 로그 백업에서 시작됩니다.|  
|**HasIncompleteMetaData**|**bit**|**1** = 메타데이터가 완전하지 않은 비상 로그 백업입니다.<br /><br /> 백업 메타데이터가 완전하지 않은 비상 로그 백업에 대한 자세한 내용은 [비상 로그 백업 &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)를 참조하세요.|  
|**IsForceOffline**|**bit**|**1** = NORECOVERY 옵션으로 수행된 백업이며 데이터베이스는 백업에 의해 오프라인 상태가 되었습니다.|  
|**IsCopyOnly**|**bit**|**1** = 복사 전용 백업입니다.<br /><br /> 복사 전용 백업은 백업 전체에 영향을 주지 않고 데이터베이스에 대한 프로시저를 복원합니다. 자세한 내용은 [복사 전용 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)를 참조하세요.|  
|**FirstRecoveryForkID**|**uniqueidentifier**|복구 분기 시작 지점의 ID. 이 열은 [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) 테이블의 **first_recovery_fork_guid**에 해당됩니다.<br /><br /> 데이터 백업의 경우 **FirstRecoveryForkID**가 **RecoveryForkID**와 동일합니다.|  
|**ForkPointLSN**|**numeric(25,0)** NULL|**FirstRecoveryForkID**가 **RecoveryForkID**와 다른 경우 이 열은 분기 지점의 로그 시퀀스 번호입니다. 그렇지 않은 경우 이 값은 NULL입니다.|  
|**RecoveryModel**|**nvarchar(60)**|데이터베이스의 복구 모델이며 다음 중 하나입니다.<br /><br /> FULL<br /><br /> BULK-LOGGED<br /><br /> SIMPLE|  
|**DifferentialBaseLSN**|**numeric(25,0)** NULL|단일 백업을 기준으로 하는 차등 백업의 경우 이 값은 차등 기반의 **FirstLSN**과 같으며 **DifferentialBaseLSN**보다 크거나 같도록 LSN을 변경하면 차등 백업에 포함됩니다.<br /><br /> 여러 백업을 기반으로 하는 차등 백업의 경우 값은 NULL이며 기본 LSN은 파일 수준에서 결정해야 합니다. 자세한 내용은 [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)를 참조하세요.<br /><br /> 비 차등 백업 유형의 경우 값은 항상 NULL입니다.<br /><br /> 자세한 내용은 [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)을 참조하세요.|  
|**DifferentialBaseGUID**|**uniqueidentifier**|단일 백업을 기준으로 하는 차등 백업의 경우 값은 차등 기반의 고유 식별자입니다.<br /><br /> 여러 백업을 기반으로 하는 차등 백업의 경우 값은 NULL이며 기본 차등 백업은 파일 단위로 결정해야 합니다.<br /><br /> 비 차등 백업 유형의 경우 값은 NULL입니다.|  
|**BackupTypeDescription**|**nvarchar(60)**|백업 유형이 문자열인 경우 다음 중 하나입니다.<br /><br /> DATABASE<br /><br /> TRANSACTION LOG<br /><br /> FILE OR FILEGROUP<br /><br /> DATABASE DIFFERENTIAL<br /><br /> FILE DIFFERENTIAL PARTIAL<br /><br /> PARTIAL DIFFERENTIAL|  
|**BackupSetGUID**|**uniqueidentifier** NULL|미디어에서 식별의 기준이 되는 백업 세트의 고유 ID|  
|**CompressedBackupSize**|**bigint**|백업 세트의 바이트 수. 압축되지 않은 백업의 경우 이 값은 **BackupSize**와 같습니다.<br /><br /> 압축 비율을 계산하려면 **CompressedBackupSize** 및 **BackupSize**를 사용합니다.<br /><br /> **msdb**를 업그레이드하는 동안 이 값은 **BackupSize** 열의 값과 일치하도록 설정됩니다.|  
|**포함**|NULL이 아닌 **tinyint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 데이터베이스의 포함 상태를 나타냅니다.<br /><br /> 0 = 데이터베이스가 포함되지 않습니다.<br /><br /> 1 = 데이터베이스가 부분적으로 포함됩니다.|  
|**KeyAlgorithm**|**nvarchar(32)**|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) ~ 현재 버전).<br /><br /> 백업을 암호화하는 데 사용되는 암호화 알고리즘입니다. NO_Encryption은 백업이 암호화되지 않았음을 나타냅니다. 올바른 값을 확인할 수 없는 경우 값은 NULL 이어야 합니다.|  
|**EncryptorThumbprint**|**varbinary(20)**|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) ~ 현재 버전).<br /><br /> 데이터베이스에서 인증서나 비대칭 키를 찾는 데 사용할 수 있는 암호기의 지문입니다. 백업이 암호화되지 않은 경우이 값은 NULL입니다.|  
|**EncryptorType**|**nvarchar(32)**|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) ~ 현재 버전).<br /><br /> 사용한 암호기 유형: 인증서 또는 비대칭 키입니다. 백업이 암호화되지 않은 경우이 값은 NULL입니다.|  
  
> [!NOTE]  
>  백업 세트에 대한 암호를 정의한 경우 RESTORE HEADERONLY는 명령의 지정한 PASSWORD 옵션과 일치하는 암호의 백업 세트에 대한 정보만 모두 표시합니다. RESTORE HEADERONLY는 보호되지 않은 백업 세트에 대한 정보도 모두 표시합니다. 암호로 보호된 미디어의 다른 백업 세트에 대한 **BackupName** 열은 '***암호로 보호됨\*\*\*'으로 설정되고 다른 열은 모두 NULL이 됩니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 클라이언트는 RESTORE HEADERONLY를 사용하여 특정 백업 장치의 모든 백업에 대한 백업 헤더 정보를 모두 검색합니다. 서버는 백업 장치의 각 백업에 대한 헤더 정보를 행으로 보냅니다.  
  
## <a name="security"></a>보안  
 백업 작업은 미디어 세트, 백업 세트 또는 이 둘 모두에 대해 암호를 지정할 수 있습니다. 미디어 세트나 백업 세트에 암호가 정의되어 있는 경우 RESTORE 문에서 정확한 암호를 지정해야 합니다. 이러한 암호를 지정하면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 무단으로 복원 작업을 수행하거나 미디어에 백업 세트를 무단으로 추가하는 작업을 방지할 수 있습니다. 하지만 암호를 사용해도 BACKUP 문의 FORMAT 옵션을 사용하여 미디어를 덮어쓰는 작업은 수행됩니다.  
  
> [!IMPORTANT]  
>  이 암호에 의한 보호 수준은 낮습니다. 권한 유무에 관계없이 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 잘못된 복원을 수행하는 것을 방지합니다. 다른 수단을 사용한 백업 데이터 읽기나 암호 바꾸기를 방지하지는 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]백업을 보호하는 최선의 구현 방법은 백업 테이프를 안전한 장소에 보관하거나 적합한 ACL(액세스 제어 목록)로 보호되는 디스크 파일에 백업하는 것입니다. ACL은 백업이 만들어지는 디렉터리 루트에 설정해야 합니다.  
  
### <a name="permissions"></a>Permissions  
 백업 세트나 백업 장치에 대한 정보를 얻으려면 CREATE DATABASE 권한이 필요합니다. 자세한 내용은 [GRANT 데이터베이스 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 디스크 파일 `C:\AdventureWorks-FullBackup.bak`에 대한 헤더 정보를 반환합니다.  
  
```  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks-FullBackup.bak'   
WITH NOUNLOAD;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE REWINDONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [백업 기록 및 헤더 정보&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [백업 또는 복원 중 백업 체크섬 설정 또는 해제&#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
