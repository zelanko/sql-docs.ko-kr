---
title: RESTORE FILELISTONLY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
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
- RESTORE FILELISTONLY
- RESTORE_FILELISTONLY_TSQL
- FILELISTONLY
- FILELISTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backups [SQL Server], file lists
- RESTORE FILELISTONLY statement
- listing backed up files
ms.assetid: 0b4b4d11-eb9d-4f3e-9629-6c79cec7a81a
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e6776115033e6e7222abc610673dd8b0aaff81dc
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements---filelistonly-transact-sql"></a>RESTORE 문-FILELISTONLY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 백업 세트에 포함된 로그 파일과 데이터베이스의 목록을 결과 집합으로 반환합니다.  
  
> [!NOTE]  
>  인수 설명에 대 한 참조 [RESTORE 인수 &#40; Transact SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
RESTORE FILELISTONLY   
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
 RESTORE FILELISTONLY 인수 설명에 대 한 참조 [RESTORE 인수 &#40; Transact SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="result-sets"></a>결과 집합  
 클라이언트는 RESTORE FILELISTONLY를 사용하여 백업 세트에 포함되어 있는 파일 목록을 가져올 수 있습니다. 이 정보는 각 파일에 대해 행 하나가 포함된 결과 집합으로 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-|-|-|  
|LogicalName|**nvarchar(128)**|파일의 논리적 이름입니다.|  
|PhysicalName|**nvarchar(260)**|물리적 파일 이름 또는 운영 체제 이름입니다.|  
|형식|**char(1)**|다음 중 하나에 해당하는 파일 유형입니다.<br /><br /> **L** = Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일<br /><br /> **D**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일<br /><br /> **F** = 전체 텍스트 카탈로그<br /><br /> **S** = FileStream, FileTable 또는 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 컨테이너|  
|FileGroupName|**nvarchar(128)**|파일이 있는 파일 그룹의 이름입니다.|  
|크기|**numeric(20,0)**|현재 크기(바이트)입니다.|  
|MaxSize|**numeric(20,0)**|허용되는 최대 크기(바이트)입니다.|  
|FileID|**bigint**|데이터베이스 내에서 고유한 파일 식별자입니다.|  
|CreateLSN|**numeric(25,0)**|파일이 생성된 시점의 로그 시퀀스 번호입니다.|  
|DropLSN|**numeric(25,0)** NULL|파일이 삭제된 시점의 로그 시퀀스 번호입니다. 파일이 아직 삭제되지 않은 경우 이 값은 NULL입니다.|  
|UniqueID|**uniqueidentifier**|파일의 GUID(Globally Unique Identifier)입니다.|  
|ReadOnlyLSN|**numeric(25,0) NULL**|해당 파일이 포함된 파일 그룹이 읽기/쓰기에서 읽기 전용으로 변경된 시점(가장 최근 변경)의 로그 시퀀스 번호입니다.|  
|ReadWriteLSN|**numeric(25,0)** NULL|해당 파일이 포함된 파일 그룹이 읽기 전용에서 읽기/쓰기로 변경된 시점(가장 최근의 변경)의 로그 시퀀스 번호입니다.|  
|BackupSizeInBytes|**bigint**|이 파일의 백업의 크기(바이트)입니다.|  
|SourceBlockSize|**int**|백업 장치를 제외한 해당 파일이 포함된 물리적 장치의 블록 크기(바이트)입니다.|  
|FileGroupID|**int**|파일 그룹의 ID입니다.|  
|LogGroupGUID|**uniqueidentifier NULL**|NULL|  
|DifferentialBaseLSN|**numeric(25,0)** NULL|차등 백업에 대 한 로그 시퀀스 번호 보다 크거나 변경 **DifferentialBaseLSN** 차등에 포함 됩니다.<br /><br /> 다른 백업 유형의 경우 값은 NULL입니다.|  
|DifferentialBaseGUID|**uniqueidentifier**|차등 백업의 경우 차등 기반의 고유 식별자입니다.<br /><br /> 다른 백업 유형의 경우 값은 NULL입니다.|  
|IsReadOnly|**bit**|**1** = 파일이 읽기 전용입니다.|  
|IsPresent|**bit**|**1** = 파일이 백업 세트에 있습니다.|  
|TDEThumbprint|**varbinary(32)**|데이터베이스 암호화 키의 지문을 표시합니다. 암호기 지문은 키 암호화에 사용되는 인증서의 SHA-1 해시입니다. 데이터베이스 암호화에 대 한 정보를 참조 하세요. [투명 한 데이터 암호화 &#40; Tde&#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md).|  
|SnapshotURL|**nvarchar(360)**|FILE_SNAPSHOT 백업에 포함 된 데이터베이스 파일의 Azure 스냅샷에 대 한 URL입니다. FILE_SNAPSHOT 백업이 없는 경우 NULL을 반환 합니다.|  
  
## <a name="security"></a>보안  
 백업 작업은 미디어 세트, 백업 세트 또는 이 둘 모두에 대해 암호를 지정할 수 있습니다. 미디어 세트나 백업 세트에 암호가 정의되어 있는 경우 RESTORE 문에서 정확한 암호를 지정해야 합니다. 이러한 암호 무단으로 복원 작업을 하 고 사용 하 여 미디어에 사용할 백업 세트의 추가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구입니다. 하지만 암호를 사용해도 BACKUP 문의 FORMAT 옵션을 사용하여 미디어를 덮어쓰는 작업은 수행됩니다.  
  
> [!IMPORTANT]  
>  이 암호에 의한 보호 수준은 낮습니다. 권한 유무에 관계없이 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 잘못된 복원을 수행하는 것을 방지합니다. 다른 수단을 사용한 백업 데이터 읽기나 암호 바꾸기를 방지하지는 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 백업을 보호하는 최선의 구현 방법은 백업 테이프를 안전한 장소에 보관하거나 적합한 ACL(액세스 제어 목록)로 보호되는 디스크 파일에 백업하는 것입니다. ACL은 백업이 만들어지는 디렉터리 루트에 설정해야 합니다.  
  
### <a name="permissions"></a>Permissions  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 백업 세트나 백업 장치에 대한 정보를 얻으려면 CREATE DATABASE 권한이 필요합니다. 자세한 내용은 [GRANT 데이터베이스 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorksBackups`라는 백업 장치에서 정보를 반환합니다. 이 예에서는 `FILE` 옵션을 사용하여 장치에 두 번째 백업 세트를 지정합니다.  
  
```  
RESTORE FILELISTONLY FROM AdventureWorksBackups   
   WITH FILE=2;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [백업 기록 및 헤더 정보&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
