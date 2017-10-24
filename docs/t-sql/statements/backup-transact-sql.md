---
title: "백업 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BACKUP_TSQL
- BACKUP
- BACKUP_DATABASE_TSQL
- BACKUP_LOG_TSQL
- BACKUP LOG
- BACKUP DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], BACKUP statement
- backing up filegroups [SQL Server]
- backup file formats [SQL Server]
- backups [SQL Server]
- database backups [SQL Server], BACKUP statement
- multifamily media sets [SQL Server]
- mirrored media sets [SQL Server]
- backing up files [SQL Server]
- backup sets [SQL Server], BACKUP statement
- backup compression [SQL Server], BACKUP statement
- BACKUP statement
- backups [SQL Server], BACKUP statement
- backup history tables [SQL Server]
- transaction log backups [SQL Server], BACKUP LOG statement
- READ_WRITE_FILEGROUPS option
- BACKUP DATABASE statement
- concurrency [SQL Server], backups
- backing up databases [SQL Server]
- passwords [SQL Server], backups
- security [SQL Server], backups
- media families [SQL Server]
- BACKUP LOG statement
- backing up transaction logs [SQL Server]
- stripe sets [SQL Server]
- cross-platform backups
ms.assetid: 89a4658a-62f1-4289-8982-f072229720a1
caps.latest.revision: 275
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 6e754198cf82a7ba0752fe8f20c3780a8ac551d7
ms.openlocfilehash: 3654be2e02163cd8069a95eb5e82d4649cec1ab5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/14/2017

---
# <a name="backup-transact-sql"></a>BACKUP(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  전체 백업 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 데이터베이스 백업 또는 하나 이상의 파일 또는 파일 그룹 데이터베이스의 파일 백업 (BACKUP DATABASE)를 만들려고 합니다. 또한 전체 복구 모델 또는 대량 로그 복구 모델에서 데이터베이스의 트랜잭션 로그를 백업하여 로그 백업(BACKUP LOG)을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
``` 
Backing Up a Whole Database   
BACKUP DATABASE { database_name | @database_name_var }   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Backing Up Specific Files or Filegroups  
BACKUP DATABASE { database_name | @database_name_var }   
 <file_or_filegroup> [ ,...n ]   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Creating a Partial Backup  
BACKUP DATABASE { database_name | @database_name_var }   
 READ_WRITE_FILEGROUPS [ , <read_only_filegroup> [ ,...n ] ]  
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Backing Up the Transaction Log (full and bulk-logged recovery models)  
BACKUP LOG { database_name | @database_name_var }   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { <general_WITH_options> | \<log-specific_optionspec> } [ ,...n ] ]  
[;]  
  
<backup_device>::=   
 {  
   { logical_device_name | @logical_device_name_var }   
 | { DISK | TAPE | URL} =   
     { 'physical_device_name' | @physical_device_name_var }  
 }   
  
<MIRROR TO clause>::=  
 MIRROR TO <backup_device> [ ,...n ]  
  
<file_or_filegroup>::=  
 {  
   FILE = { logical_file_name | @logical_file_name_var }   
 | FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }  
 }   
  
<read_only_filegroup>::=  
FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }  
  
<general_WITH_options> [ ,...n ]::=   
--Backup Set Options  
   COPY_ONLY   
 | { COMPRESSION | NO_COMPRESSION }   
 | DESCRIPTION = { 'text' | @text_variable }   
 | NAME = { backup_set_name | @backup_set_name_var }   
 | CREDENTIAL  
 | ENCRYPTION  
 | FILE_SNAPSHOT  
 | { EXPIREDATE = { 'date' | @date_var }   
        | RETAINDAYS = { days | @days_var } }   
  
--Media Set Options  
   { NOINIT | INIT }   
 | { NOSKIP | SKIP }   
 | { NOFORMAT | FORMAT }   
 | MEDIADESCRIPTION = { 'text' | @text_variable }   
 | MEDIANAME = { media_name | @media_name_variable }   
 | BLOCKSIZE = { blocksize | @blocksize_variable }   
  
--Data Transfer Options  
   BUFFERCOUNT = { buffercount | @buffercount_variable }   
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }  
  
--Error Management Options  
   { NO_CHECKSUM | CHECKSUM }  
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Compatibility Options  
   RESTART   
  
--Monitoring Options  
   STATS [ = percentage ]   
  
--Tape Options  
   { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }   
  
--Log-specific Options  
   { NORECOVERY | STANDBY = undo_file_name }  
 | NO_TRUNCATE  
  
--Encryption Options  
 ENCRYPTION (ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY } , encryptor_options ) <encryptor_options> ::=   
   SERVER CERTIFICATE = Encryptor_Name | SERVER ASYMMETRIC KEY = Encryptor_Name   
```  
  
## <a name="arguments"></a>인수  
 DATABASE  
 전체 데이터베이스 백업을 지정합니다. 파일 및 파일 그룹의 목록이 지정되어 있으면 해당 파일 및 파일 그룹만 백업됩니다. 전체 또는 차등 데이터베이스 백업 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 백업을 복원할 때 일관성 있는 데이터베이스를 생성하기 위해 충분한 트랜잭션 로그를 백업합니다.  
  
 백업 데이터베이스에서 만든 백업을 복원 하는 경우 (한 *데이터 백업*), 전체 백업을 복원 합니다. 백업 내의 특정 시간이나 트랜잭션으로는 로그 백업만 복원할 수 있습니다.  
  
> [!NOTE]  
>  전체 데이터베이스 백업만 수행할 수는 **마스터** 데이터베이스입니다.  
  
 LOG  
 트랜잭션 로그만 백업하도록 지정합니다. 성공적으로 실행된 마지막 로그 백업에서 현재 로그의 끝에 로그가 백업됩니다. 첫 로그 백업을 만들려면 먼저 전체 백업을 만들어야 합니다.  
  
 WITH STOPAT, STOPATMARK 또는 STOPBEFOREMARK를 지정 하 여 특정 시간이 나 백업 내의 트랜잭션 로그 백업을 복원할 수 있습니다 프로그램 [RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md) 문.  
  
> [!NOTE]  
>  일반적인 로그 백업 후 WITH NO_TRUNCATE 또는 COPY_ONLY를 지정하지 않으면 일부 트랜잭션 로그 레코드가 비활성 상태가 됩니다. 하나 이상의 가상 로그 파일 내의 모든 레코드가 비활성 상태가 된 후에는 로그가 잘립니다. 일상적인 로그 백업 후 로그가 잘리지 않을 경우 로그 잘림이 지연되는 것일 수 있습니다. 자세한 내용은 다음을 참조하십시오.  
  
 { *database_name* | **@**database_name_var *을 (를)   
 트랜잭션 로그, 일부 데이터베이스, 전체 데이터베이스가 백업되는 데이터베이스입니다. 변수로 제공한 경우 (**@***database_name_var*),이 이름은 문자열 상수를 지정 (** @ ** * database_name_var***=***데이터베이스 이름*) 또는 문자 문자열 데이터 형식의 변수를 제외 하 고는 **ntext** 또는 **텍스트** 데이터 형식입니다.  
  
> [!NOTE]  
>  데이터베이스 미러링 파트너 관계의 미러 데이터베이스는 백업할 수 없습니다.  
  
\<file_or_filegroup > [ **,**... *n* ]  
 BACKUP DATABASE와 함께만 사용되며 파일 백업에 포함시킬 데이터베이스 파일 또는 파일 그룹을 지정하거나 부분 백업에 포함시킬 읽기 전용 파일 또는 파일 그룹을 지정합니다.  
  
 파일 ** = ** { *logical_file_name*| **@***logical_file_name_var* }  
 파일의 논리적 이름이거나 해당 값이 백업에 포함시킬 파일의 논리적 이름과 같은 변수입니다.  
  
 파일 그룹 ** = ** { *logical_filegroup_name*| **@***logical_filegroup_name_var* }  
 파일 그룹의 논리적 이름이거나 해당 값이 백업에 포함시킬 파일 그룹의 논리적 이름과 같은 변수입니다. 단순 복구 모델에서 파일 그룹 백업은 읽기 전용 파일 그룹에만 사용할 수 있습니다.  
  
> [!NOTE]  
>  데이터베이스 크기와 성능 요구 사항으로 인해 데이터베이스 백업이 불가능할 경우 파일 백업을 사용하십시오.  
  
 *n*  
 쉼표로 구분된 목록에 여러 개의 파일 및 파일 그룹을 지정할 수 있음을 나타내는 자리 표시자입니다. 사용할 수 있는 숫자에는 제한이 없습니다. 
  
 자세한 내용은 참조: [전체 파일 백업 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/full-file-backups-sql-server.md) 및 [파일 및 파일 그룹 &#40; 백업 SQL Server &#41; ](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md).  
  
 READ_WRITE_FILEGROUPS [ **,** 파일 그룹 = { *logical_filegroup_name*| **@***logical_filegroup_name_var* } [ **,**... *n* ] ]  
 부분 백업을 지정합니다. 부분 백업은 주 파일 그룹, 모든 읽기/쓰기 보조 파일 그룹, 지정된 모든 읽기 전용 파일이나 파일 그룹과 같은 데이터베이스에 있는 모든 읽기/쓰기 파일을 포함합니다.  
  
 READ_WRITE_FILEGROUPS  
 부분 백업 시 모든 읽기/쓰기 파일 그룹을 백업하도록 지정합니다. 데이터베이스가 읽기 전용일 경우 READ_WRITE_FILEGROUPS에는 주 파일 그룹만 포함됩니다.  
  
> [!IMPORTANT]  
>  READ_WRITE_FILEGROUPS 대신 FILEGROUP을 사용하여 읽기/쓰기 파일 그룹을 명시적으로 나열하면 파일 백업이 생성됩니다.  
  
 파일 그룹 = { *logical_filegroup_name*| **@***logical_filegroup_name_var* }  
읽기 전용 파일 그룹의 논리적 이름이거나 해당 값이 부분 백업에 포함시킬 읽기 전용 파일 그룹의 논리적 이름과 같은 변수입니다. 자세한 내용은 참조 하십시오. "\<file_or_filegroup >,"이이 항목의에서 앞부분입니다.
  
 *n*  
 쉼표로 구분된 목록에 여러 개의 읽기 전용 파일 그룹을 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
 부분 백업에 대 한 자세한 내용은 참조 하세요. [부분 백업 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/partial-backups-sql-server.md).  
  
\<backup_device > [ **,**... * n * ] 집합이 함께 제공 되는 나타냅니다 [백업 장치](../../relational-databases/backup-restore/backup-devices-sql-server.md) 미러되지 않은 미디어 세트 이거나 미러된 미디어 세트 (에 하나 이상의 MIRROR TO 내의 미러 중 첫 번째 절은 선언 됨).  
  
\<backup_device > 백업 작업에 사용할 논리적 또는 물리적 백업 장치를 지정 합니다.  
  
 { *logical_device_name* | **@***logical_device_name_var* }  
 데이터베이스를 백업할 백업 장치의 논리적 이름입니다. 논리적 이름은 식별자 규칙을 따라야 합니다. 변수로 제공한 경우 (@*logical_device_name_var*), 백업 장치 이름은 수 지정 하는 문자열 상수 (@*logical_device_name_var* ** = ** 논리적 백업 장치 이름) 또는 모든 문자열 형식의 데이터를 제외 하 고 변수는 **ntext** 또는 **텍스트** 데이터 형식입니다.  
  
 {디스크 | 테이프 | URL을 (를) ** = ** { **'***physical_device_name***'**  |  ** @ ** *physical_device_name_var* }  
 디스크 파일이나 테이프 장치 또는 Windows Azure Blob 스토리지 서비스를 지정합니다. URL 형식은 Windows Azure 저장소 서비스에 백업을 만드는 데 사용 됩니다. 자세한 내용 및 예제에 대 한 참조 [SQL Server 백업 및 Microsoft Azure Blob 저장소 서비스로 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)합니다. 자습서를 참조 하십시오. [자습서: SQL Server 백업 및 복원 Windows Azure Blob 저장소 서비스에](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)합니다.  
  
> [!IMPORTANT]  
>  와 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 까지 SP1 CU2 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], URL에 백업할 때만 단일 장치에 백업할 수 있습니다. 여러 장치에 URL에 백업할 때를 백업 하기 위해 사용 해야 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 공유 액세스 서명 (SAS) 토큰을 사용 해야 합니다. 공유 액세스 서명을 만드는 예제를 보려면 [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md) 및 [Powershell 포함 Azure Storage에서 공유 액세스 서명 (SAS) 토큰으로 SQL 자격 증명 만들기 간소화](http://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx)합니다.  
  
**URL에 적용 됩니다.**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2- [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 BACKUP 문에 지정되기 전에는 디스크 장치가 없어도 됩니다. 물리적 장치가 존재하고 BACKUP 문에서 INIT 옵션이 지정되지 않은 경우에는 백업이 장치에 추가됩니다.  
  
 자세한 내용은 [백업 장치&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)인스턴스에서 가져온 경우에 필요합니다.  
  
> [!NOTE]  
>  TAPE 옵션은 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.  
  
 *n*  
 쉼표로 구분된 목록에 백업 장치를 최대 64개까지 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
MIRROR TO \<backup_device > [ **,**... * n * ] 최대 3 개의 보조 백업 장치, 파일 TO 절에 백업 장치에 지정 된 각 미러는 집합을 지정 합니다. MIRROR TO 절은 TO 절과 같은 유형과 개수의 백업 장치를 지정 해야 합니다. MIRROR TO 절은 최대 3개까지 포함시킬 수 있습니다.  
  
 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 엔터프라이즈 버전에서만 사용할 수 있습니다.  
  
> [!NOTE]  
>  MIRROR TO = DISK인 경우 BACKUP은 디스크 장치에 적합한 블록 크기를 자동으로 결정합니다. 블록 크기에 대한 자세한 내용은 이 표의 뒷부분에 나오는 "BLOCKSIZE"를 참조하십시오.  
  
\<backup_device > 참조 "\<backup_device >,"이이 섹션의에서 앞부분입니다.
  
 *n*  
 쉼표로 구분된 목록에 백업 장치를 최대 64개까지 지정할 수 있음을 나타내는 자리 표시자입니다. MIRROR TO 절의 장치 수는 TO 절의 장치 수와 같아야 합니다.  
  
 자세한 내용은 이 항목의 뒷부분에 나오는 "주의" 섹션의 "미러된 미디어 세트의 미디어 패밀리"를 참조하십시오.  
  
 [ *다음-미러-하려면* ]  
 단일 TO 절을 포함하여 단일 BACKUP 문에 MIRROR TO 절을 최대 3개까지 포함시킬 수 있음을 나타내는 자리 표시자입니다.  
  
### <a name="with-options"></a>WITH 옵션  
 백업 작업에 사용할 옵션을 지정합니다.  
  
 CREDENTIAL  
 Windows Azure Blob 저장소 서비스로 백업을 만들 때에만 사용됩니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2- [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 FILE_SNAPSHOT  
 Azure Blob 저장소 서비스를 사용 하 여 모든 SQL Server 데이터베이스 파일을 저장 하면 데이터베이스 파일의 Azure 스냅숏이 만드는 데 사용 합니다. 자세한 내용은 참조 [Microsoft Azure에서 SQL Server 데이터 파일](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]스냅숏 백업이 일관 된 상태에서 데이터베이스 파일 (데이터 및 로그 파일)의 Azure 스냅숏이 됩니다. Azure 스냅숏 집합 일관 된 백업을 구성 하와 백업 파일에 기록 됩니다. 유일한 차이점 **백업 데이터베이스를 URL WITH FILE_SNAPSHOT** 및 **백업 로그를 URL WITH FILE_SNAPSHOT** 는 후자 잘라 버립니다 트랜잭션 로그 전자는 손실 됩니다. 와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스냅숏 백업, 여는 데 필요한 초기 전체 백업 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 단일 트랜잭션 로그 백업 지점에 데이터베이스를 트랜잭션 로그 백업 시점으로 복원 하는 데 필요한 파일인 백업 체인을 설정 합니다. 또한 두 개의 트랜잭션 로그 백업의 시간 간격의 지점에 데이터베이스를 복원 하려면 두 개의 트랜잭션 로그 백업이 필요 합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 DIFFERENTIAL  
 BACKUP DATABASE와 함께만 사용되며 데이터베이스 또는 파일 백업이 마지막 전체 백업 이후 변경된 데이터베이스 또는 파일 부분으로만 구성되도록 지정합니다. 일반적으로 차등 백업은 전체 백업보다 적은 공간을 사용합니다. 마지막 전체 백업 이후 수행된 개별 로그 백업 중 일부를 적용할 필요가 없도록 하려면 이 옵션을 사용합니다.  
  
> [!NOTE]  
>  기본적으로 BACKUP DATABASE는 전체 백업을 만듭니다.  
  
 자세한 내용은 [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)을 참조하세요.  
  
 ENCRYPTION  
 백업에 대한 암호화를 지정하는 데 사용됩니다. 백업을 암호화하는 데 사용할 암호화 알고리즘을 지정하거나 백업이 암호화되지 않도록 하려면 ‘NO_ENCRYPTION’을 지정할 수 있습니다. 암호화는 백업 파일을 보호하는 데 권장되는 방법입니다. 지정할 수 있는 알고리즘의 목록은 다음과 같습니다.  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 암호화하도록 선택하는 경우 암호기 옵션을 사용하여 암호기도 지정해야 합니다.  
  
-   SERVER CERTIFICATE = Encryptor_Name  
  
-   SERVER ASYMMETRIC KEY = Encryptor_Name  
  
    > [!WARNING]  
    >  FILE_SNAPSHOT 인수와 함께에서 암호화를 사용 하는 경우 지정 된 암호화 알고리즘을 사용 하는 메타 데이터 파일 자체 암호화 하 고 시스템 TDE는 데이터베이스에 대 한 완료 되었음을 확인 합니다. 데이터 자체에 대 한 추가 암호화 되지 않은 오류 발생합니다. 데이터베이스 암호화 되지 않은 이거나 백업 문이 실행 된 암호화 하기 전에 완료 되지 않은 경우 백업이 실패 합니다.  
  
**백업 세트 옵션**  
  
이러한 옵션은 이 백업 작업에서 만든 백업 세트에서 작동합니다.  
  
> [!NOTE]  
>  복원 작업에 백업 세트를 지정 하려면 파일을 사용 하 여 ** = ** * \<backup_set_file_number >* 옵션입니다. 백업 세트를 지정 하는 방법에 대 한 자세한 내용은 "백업 세트 지정"의 참조 [RESTORE 인수 &#40; Transact SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).
  
 COPY_ONLY  
 백업 임을 지정는 *복사 전용 백업은*는 정상적인 백업 시퀀스에는 영향을 주지 않습니다. 복사 전용 백업은 정기적으로 예약되어 수행되는 기존 백업과는 별개로 생성됩니다. 복사 전용 백업은 백업 전체에 영향을 주지 않고 데이터베이스에 대한 프로시저를 복원합니다.  
  
 복사 전용 백업은 온라인 파일을 복원하기 전에 로그를 백업하는 것과 같은 특별한 목적을 위해 백업을 수행할 때 사용됩니다. 일반적으로 복사 전용 로그 백업은 한 번만 사용된 후 삭제됩니다.  
  
-   BACKUP DATABASE와 함께 사용하는 경우 COPY_ONLY 옵션은 차등 기반으로 사용할 수 없는 전체 백업을 만듭니다. 차등 비트맵은 업데이트되지 않으며 차등 백업은 복사 전용 백업이 없는 것처럼 작동합니다. 후속 차등 백업은 가장 최근의 기존 전체 백업을 기반으로 사용합니다.  
  
    > [!IMPORTANT]  
    >  DIFFERENTIAL과 COPY_ONLY를 함께 사용하면 COPY_ONLY가 무시되고 차등 백업이 생성됩니다.  
  
-   BACKUP LOG를 사용할 때는 COPY_ONLY 옵션 만듭니다는 *복사 전용 로그 백업은*, 트랜잭션 로그를 자르지 않는 합니다. 복사 전용 로그 백업은 로그 체인에 영향을 주지 않으며 기타 로그 백업은 복사 전용 백업이 없는 것처럼 작동합니다.  
  
자세한 내용은 [복사 전용 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)를 참조하세요.  
  
{ COMPRESSION | NO_COMPRESSION }  
[!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상 버전을 지정 하 고 있는지 여부를 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md) 서버 수준 기본값을 재정의이 백업에서 수행 됩니다.  
  
설치 시 백업 압축은 기본 동작이 아닙니다. 하지만이 기본값을 설정 하 여 변경할 수 있습니다는 [백업 압축 기본값](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) 서버 구성 옵션입니다. 이 옵션의 현재 값을 보는 방법에 대 한 정보를 참조 하십시오. [보기 또는 변경 서버 속성 &#40; SQL Server &#41; ](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md).  
  
COMPRESSION  
백업 압축을 명시적으로 활성화합니다.  
  
NO_COMPRESSION  
백업 압축을 명시적으로 비활성화합니다.  
  
DESCRIPTION **=** { **'***text***'** | **@***text_variable* }  
백업 세트를 설명하는 자유 형식의 텍스트를 지정합니다. 문자열을 최대 255자까지 지정할 수 있습니다.  
  
이름 ** = ** { *backup_set_name*| **@***backup_set_var* }  
백업 세트의 이름을 지정합니다. 이름은 최대 128자까지 지정할 수 있습니다. NAME을 지정하지 않으면 공백이 됩니다.  
  
{EXPIREDATE **='***날짜***'**| RETAINDAYS ** = ** *일* }  
이 백업에 대한 백업 세트를 덮어쓸 수 있는 날짜를 지정합니다. 두 옵션을 모두 사용하면 RETAINDAYS가 EXPIREDATE보다 우선적으로 적용됩니다.  
  
따라 만료 날짜가 결정은 두 옵션을 지정 하는 경우는 **mediaretention** 구성 설정입니다. 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)서버 구성 옵션을 구성하는 방법에 대해 설명합니다.  
  
> [!IMPORTANT]  
>  이러한 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 파일을 덮어쓰지 못하도록 하기 위한 것입니다. 테이프는 다른 방법을 사용하여 지울 수 있고 디스크 파일은 운영 체제를 통해 삭제할 수 있습니다. 만료일 확인에 대한 자세한 내용은 이 항목에서 SKIP과 FORMAT을 참조하십시오.  
  
EXPIREDATE ** = ** { **'***날짜***'** |  ** @ ** *date_var* }  
 백업 세트가 만료되어 덮어쓸 수 있는 날짜를 지정합니다. 변수로 제공한 경우 (@*date_var*),이 날짜에 구성 된 시스템 따라야 합니다. **datetime** 서식을 지정 하 고 다음 중 하나로 지정 해야 합니다.  
  
-   문자열 상수 (@*date_var* ** = ** 날짜)  
-   문자열 데이터 형식의 변수 (제외 하 고는 **ntext** 또는 **텍스트** 데이터 형식)  
-   A **smalldatetime**  
-   A **datetime** 변수  
  
예를 들어  
  
-   `'Dec 31, 2020 11:59 PM'`  
-   `'1/1/2021'`  
  
지정 하는 방법에 대 한 내용은 **datetime** 값, 참조 [날짜 및 시간 형식](../../t-sql/data-types/date-and-time-types.md)합니다.  
  
> [!NOTE]  
>  만료 날짜를 무시하려면 SKIP 옵션을 사용하십시오.  
  
RETAINDAYS ** = ** { *일*| **@***days_var* }  
 백업 미디어 세트를 덮어쓰지 않고 보존할 일 수를 지정합니다. 변수로 제공한 경우 (**@***days_var*)을 정수로 지정 해야 합니다.  
  
**미디어 세트 옵션**  
  
이러한 옵션은 전체 미디어 세트에서 작동합니다.  
  
{ **NOINIT** | INIT}  
 백업 작업이 백업 미디어의 기존 백업 세트에 추가되는지 또는 이를 덮어쓰는지 여부를 제어합니다. 기본적으로 백업 작업은 미디어의 최신 백업 세트에 추가됩니다(NOINIT).  
  
> [!NOTE]  
>  간의 상호 작용에 대 한 정보에 대 한 { **NOINIT** | INIT}와 { **NOSKIP** | SKIP}이 항목의 뒷부분에 나오는 "주의"를 참조 합니다.  
  
NOINIT  
 백업 세트가 기존 백업 세트를 보존하면서 지정된 미디어 세트에 추가되는 것을 나타냅니다. 미디어 세트에 미디어 암호가 정의되어 있는 경우에는 암호를 제공해야 합니다. NOINIT는 기본값입니다.  
  
자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)을 참조하세요.  
  
INIT  
 미디어 헤더만 보존하고 모든 백업 세트를 덮어쓰도록 지정합니다. INIT가 지정되면 조건이 허용되는 경우 해당 장치의 기존 백업 세트를 모두 덮어씁니다. 기본적으로 BACKUP은 다음 조건을 확인하고 둘 중 한 조건에 해당되면 백업 미디어를 덮어쓰지 않습니다.  
  
-   백업 세트가 아직 만료되지 않은 경우. 자세한 내용은 EXPIREDATE 및 RETAINDATYS 옵션을 참조하십시오.  
-   BACKUP 문에 지정된 백업 세트 이름이 백업 미디어에 있는 이름과 일치하지 않을 경우. 자세한 내용은 이 섹션의 앞부분에 나오는 NAME 옵션을 참조하십시오.  
  
이러한 검사를 무시하려면 SKIP 옵션을 사용합니다.  
  
자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)을 참조하세요.  
  
{ **NOSKIP** | SKIP}  
백업 작업에서 미디어에 있는 백업 세트의 만료 날짜 및 시간을 덮어쓰기 전에 검사하는지 여부를 제어합니다.  
  
> [!NOTE]  
>  간의 상호 작용에 대 한 정보에 대 한 { **NOINIT** | INIT}와 { **NOSKIP** | SKIP}이 항목의 뒷부분에 나오는 "주의"를 참조 합니다.  
  
NOSKIP  
BACKUP 문이 백업 세트를 덮어쓰기 전에 미디어에 있는 모든 백업 세트의 만료 날짜를 확인하도록 지정합니다. 이것이 기본 동작입니다.  
  
SKIP  
백업 세트를 덮어쓰지 않도록 BACKUP 문에서 일반적으로 수행되는 백업 세트 만료 날짜와 이름 확인을 해제합니다. { INIT | NOINIT }와 { NOSKIP | SKIP } 간 상호 작용에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
백업 세트의 만료 날짜를 보려면 쿼리는 **expiration_date** 의 열은 [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) 기록 테이블입니다.  
  
{ **종류가 NOFORMAT** | 형식}  
이 백업 작업에 사용된 볼륨에 미디어 헤더를 기록하여 기존 미디어 헤더와 백업 세트를 덮어써야 하는지 여부를 지정합니다.  
  
NOFORMAT  
백업 작업에서 이 작업에 사용된 미디어 볼륨의 기존 미디어 헤더와 백업 세트를 유지하도록 지정합니다. 이것이 기본 동작입니다.  
  
FORMAT  
새 미디어 세트가 만들어지도록 지정합니다. FORMAT을 사용하면 백업 작업에서 해당 작업에 사용된 모든 미디어 볼륨의 새 미디어 헤더를 기록합니다. 이때 볼륨의 기존 내용은 기존의 모든 미디어 헤더와 백업 세트가 덮어쓰이므로 사용할 수 없게 됩니다.  
  
> [!IMPORTANT]  
>  FORMAT 옵션은 신중하게 사용해야 합니다. 미디어 세트의 볼륨을 포맷하면 전체 미디어 세트를 사용할 수 없게 됩니다. 예를 들어 기존 스트라이프 미디어 세트에 속하는 테이프 하나를 초기화하면 전체 미디어 세트를 사용할 수 없게 됩니다.  
  
FORMAT 지정은 SKIP을 의미하며 SKIP은 명시적으로 지정할 필요가 없습니다.  
  
MEDIADESCRIPTION ** = ** { *텍스트* | **@***text_variable* }  
미디어 세트에 대한 설명 텍스트를 최대 255자까지 지정합니다.  
  
MEDIANAME ** = ** { *media_name* | **@***media_name_variable* }  
전체 백업 미디어 세트에 대한 미디어 이름을 지정합니다. 미디어 이름은 128자 이하여야 합니다. MEDIANAME을 지정하면 백업 볼륨에 이미 있는 이전에 지정한 미디어 이름과 일치해야 합니다. 지정하지 않거나 SKIP 옵션을 지정하면 미디어 이름에 대한 확인을 수행하지 않습니다.  
  
BLOCKSIZE ** = ** { *blocksize* | **@***blocksize_variable* }  
물리적 블록 크기(바이트)를 지정합니다. 지원되는 크기는 512, 1024, 2048, 4096, 8192, 16384, 32768 및 65536(64KB) 바이트입니다. 테이프 장치의 기본값은 65536이고 그렇지 않은 경우에는 512입니다. 일반적으로 BACKUP에서 장치에 적합한 블록 크기를 자동으로 선택하기 때문에 이 옵션은 필요하지 않습니다. 명시적으로 지정된 블록 크기는 자동 선택된 블록 크기보다 우선 적용됩니다.  
  
CD-ROM으로 복사하거나 CD-ROM에서 복원할 백업을 만드는 경우 BLOCKSIZE=2048을 지정합니다.  
  
> [!NOTE]  
>  이 옵션은 일반적으로 테이프 장치에 쓰는 경우에만 성능에 영향을 줍니다.  
  
**데이터 전송 옵션**  
  
BUFFERCOUNT ** = ** { *buffercount* | **@***buffercount_variable* }  
백업 작업에 사용되는 I/O 버퍼의 총 수를 지정합니다. 임의의 양의 정수를 지정할 수 있지만 버퍼 수가 많으면 Sqlservr.exe 프로세스의 부적절한 가상 주소 공간으로 인해 "메모리가 부족합니다"라는 오류가 발생할 수 있습니다.  
  
버퍼에서 사용 하는 총 공간에 의해 결정 됩니다: *buffercount***\****maxtransfersize*합니다.  
  
> [!NOTE]  
>  BUFFERCOUNT 옵션을 사용 하는 방법에 대 한 중요 한 정보에 대 한 참조는 [잘못 된 BufferCount 데이터 전송 옵션 OOM 상태가 발생할 수](http://blogs.msdn.com/b/sqlserverfaq/archive/2010/05/06/incorrect-buffercount-data-transfer-option-can-lead-to-oom-condition.aspx) 블로그.  
  
MAXTRANSFERSIZE ** = ** { *maxtransfersize* | **@***maxtransfersize_variable* }  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 백업 미디어 간에 사용되는 가장 큰 전송 단위(바이트)를 지정합니다. 가능한 값은 최대 4194304바이트(4MB)까지 65536바이트(64KB)의 배수입니다.  
> [!NOTE]  
>  데이터베이스에 FILESTREAM을 구성한 또는 메모리 내 OLTP 파일 그룹을 포함 하는 경우 SQL 기록기 서비스를 사용 하 여 백업을 만들 때 하면 `MAXTRANSFERSIZE` 복원 시 해야 보다 크거나 같은 경우는 `MAXTRANSFERSIZE` 된 때 사용 되는 백업이 생성 되었습니다. 
  
**오류 관리 옵션**  
  
이러한 옵션을 사용 하 여 백업 작업에 대 한 백업 체크섬의 설정 여부 및 오류 발생 시 작업을 중지 하는지 여부를 확인할 수 있습니다.  
  
{ **NO_CHECKSUM** | 체크섬을 (를)  
 백업 체크섬의 설정 여부를 제어합니다.  
  
NO_CHECKSUM  
백업 체크섬 생성 및 페이지 체크섬의 유효성 검사를 명시적으로 해제합니다. 이것이 기본 동작입니다.  
  
CHECKSUM  
백업 작업을 사용할 수 및 사용 하도록 설정 하는 경우 각 페이지의 체크섬과 조각난된 페이지를 확인 하 고 전체 백업에 대 한 체크섬을 생성을 지정 합니다.  
  
백업 체크섬을 사용하면 작업 및 백업 처리량에 영향을 줄 수 있습니다.  
  
자세한 내용은 참조 [가능한 미디어 오류 시 백업 및 복원 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
{ **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR}  
페이지 체크섬 오류가 발생한 후 백업 작업을 중지할지, 아니면 계속할지를 제어합니다.  
  
STOP_ON_ERROR  
페이지 체크섬에서 확인하지 않을 경우 BACKUP이 실패하도록 지정합니다. 이것이 기본 동작입니다.  
  
CONTINUE_AFTER_ERROR  
잘못된 체크섬이나 조각난 페이지 등의 오류가 발생하더라도 BACKUP을 계속하도록 지시합니다.  
  
꼬리를 백업할 수 없는 경우 데이터베이스가 손상 된 경우 NO_TRUNCATE를 사용 하 여 로그 옵션, 시작할 수 있습니다. 한 [비상 로그 백업](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) NO_TRUNCATE 대신 CONTINUE_AFTER_ERROR를 지정 하 여 합니다.  
  
자세한 내용은 참조 [가능한 미디어 오류 시 백업 및 복원 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
**호환성 옵션**  
  
RESTART  
[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 아무 효과가 없습니다. 이 옵션은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와의 호환성을 위해 사용됩니다.  
  
**모니터링 옵션**  
  
STATS [ ** = ** *백분율* ]  
 다른 사용자가 메시지를 표시 *백분율* 완료 되 고 진행 상태를 측정 하는 데 사용 됩니다. 경우 *백분율* 를 생략 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 각 10%가 완료 된 후 메시지를 표시 합니다.  
  
STATS 옵션은 다음 간격을 보고할 임계값에 도달한 시점까지의 완료 백분율을 보고합니다. 간격은 지정된 비율을 대략적으로 나타냅니다. 예를 들어 STATS=10인 경우 완료된 크기가 40%이면 옵션은 43%를 표시할 수 있습니다. 대용량 백업 세트의 경우 완료 백분율이 완료된 I/O 호출 간에 매우 느리게 진행되므로 문제가 되지 않습니다.  
  
**테이프 옵션**  
  
이러한 옵션은 테이프 장치에만 사용됩니다. 테이프가 아닌 장치를 사용할 경우 이러한 옵션은 무시됩니다.  
  
{ **REWIND** | NOREWIND }  
REWIND  
 지정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 해제 하 고 테이프를 되감습니다. 기본값은 REWIND입니다.  
  
NOREWIND  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 백업 작업 후에 테이프를 열어 놓도록 지정합니다. 테이프에 여러 개의 백업 작업을 수행할 때 이 옵션을 사용하면 성능을 향상시킬 수 있습니다.  
  
NOREWIND는 NOUNLOAD를 의미하며 두 옵션은 단일 BACKUP 문 내에서 호환되지 않습니다.  
  
> [!NOTE]  
>  NOREWIND를 사용하는 경우 같은 프로세스에서 실행 중인 BACKUP 또는 RESTORE 문이 REWIND 또는 UNLOAD 옵션을 사용하거나 서버 인스턴스가 종료될 때까지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 테이프 드라이브에 대한 소유권을 보유합니다. 테이프를 열어 두면 다른 프로세스에서 테이프를 액세스하는 것을 방지합니다. 열려 있는 테이프 목록을 표시 하 고 열려 있는 테이프를 닫고 하는 방법에 대 한 정보를 참조 하십시오. [백업 장치 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
{ **언로드** | NOUNLOAD}  
> [!NOTE]  
>  UNLOAD/NOUNLOAD는 세션 기간 동안이나 다른 옵션을 지정하여 다시 설정할 때까지 유지되는 세션 설정입니다.  
  
UNLOAD  
 백업이 끝나면 테이프를 자동으로 되감고 언로드되도록 지정합니다. UNLOAD는 세션 시작 시의 기본값입니다. 
  
NOUNLOAD  
 후 백업 작업에서 테이프를 테이프 드라이브에 로드 된 상태로 유지 되도록 지정 합니다.  
  
> [!NOTE]  
>  테이프 백업 장치에 백업하는 경우 BLOCKSIZE 옵션은 백업 작업의 성능에 영향을 줍니다. 이 옵션은 일반적으로 테이프 장치에 쓰는 경우에만 성능에 영향을 줍니다.  
  
**로그 관련 옵션**  
  
이러한 옵션은 BACKUP LOG와 함께만 사용됩니다.  
  
> [!NOTE]  
>  로그 백업을 수행하지 않으려면 단순 복구 모델을 사용합니다. 자세한 내용은 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.  
  
{NORECOVERY | 대기 ** = ** *undo_file_name* }  
  NORECOVERY  
  비상 로그를 백업하고 데이터베이스를 RESTORING 상태로 유지합니다. NORECOVERY는 보조 데이터베이스로 장애 조치(failover)하거나 RESTORE 작업에 앞서 비상 로그를 저장할 때 유용합니다.  
  
  로그 잘림을 건너뛰는 최상의 로그 백업을 수행한 다음 데이터베이스를 자동으로 다시 RESTORING 상태로 되돌리려면 NO_TRUNCATE 및 NORECOVERY 옵션을 함께 사용하십시오.  
  
  대기 ** = ** *standby_file_name*  
  비상 로그를 백업하고 데이터베이스를 읽기 전용 및 STANDBY 상태로 유지합니다. STANDBY 절은 대기 데이터를 쓰고 롤백을 수행하지만 추가 복원 옵션을 사용해야 합니다. STANDBY 옵션 사용은 BACKUP LOG WITH NORECOVERY를 사용한 다음 RESTORE WITH STANDBY를 사용하는 것과 동일합니다.  
  
  지정한 대기 파일 대기 모드를 사용 하려면 *standby_file_name*, 데이터베이스의 로그에 위치가 저장 됩니다. 지정한 파일이 이미 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 해당 파일을 덮어쓰고 파일이 없으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 파일을 만듭니다. 대기 파일은 데이터베이스의 일부가 됩니다.  
  
  이 파일에는 롤백된 변경 내용이 저장되는데 다음에 RESTORE LOG를 적용하려는 경우 이 변경 내용은 취소해야 합니다. 커밋되지 않은 트랜잭션을 롤백하여 수정된 데이터베이스의 고유한 페이지가 모두 들어갈 수 있도록 대기 파일이 증가되므로 디스크 공간이 충분히 있어야 합니다.  
  
NO_TRUNCATE  
지정 하는 로그 잘리지 있고는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 데이터베이스의 상태에 관계 없이 백업을 시도 하도록 합니다. 따라서 NO_TRUNCATE 옵션으로 수행된 백업의 메타데이터는 완전하지 않을 수 있습니다. 이 옵션을 사용하면 데이터베이스가 손상된 경우에도 로그를 백업할 수 있습니다.  
  
BACKUP LOG의 NO_TRUNCATE 옵션은 COPY_ONLY와 CONTINUE_AFTER_ERROR를 모두 지정하는 것과 같습니다.  
  
NO_TRUNCATE 옵션을 사용하지 않으면 데이터베이스가 ONLINE 상태여야 합니다. 데이터베이스가 SUSPENDED 상태이면 NO_TRUNCATE를 지정하여 백업을 만들 수 있습니다. 그러나 데이터베이스가 OFFLINE 또는 EMERGENCY 상태이면 NO_TRUNCATE에서도 BACKUP을 사용할 수 없습니다. 데이터베이스 상태에 대 한 정보를 참조 하십시오. [데이터베이스 상태](../../relational-databases/databases/database-states.md)합니다.  
  
## <a name="about-working-with-sql-server-backups"></a>SQL Server 백업 사용 정보  
 이 섹션에서는 다음 필수 백업 개념을 설명합니다.  
  
 [백업 유형](#Backup_Types)  
 [트랜잭션 로그 잘림](#Tlog_Truncation)  
 [백업 미디어 포맷](#Formatting_Media)  
 [백업 장치 및 미디어 세트 사용](#Backup_Devices_and_Media_Sets)  
 [SQL Server 백업 복원](#Restoring_Backups)  
  
> [!NOTE]  
>  백업에 대 한 소개 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 참조 [백업 개요 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="Backup_Types"></a>백업 유형  
 지원되는 백업 유형은 다음과 같이 데이터베이스의 복구 모델에 따라 달라집니다.  
  
-   모든 복구 모델은 데이터의 전체 및 차등 백업을 지원합니다.  
  
    |백업 범위|백업 유형|  
    |---------------------|------------------|  
    |전체 데이터베이스|[데이터베이스 백업을](../../relational-databases/backup-restore/full-database-backups-sql-server.md) 전체 데이터베이스를 포함 합니다.<br /><br /> 각 데이터베이스 백업은 하나 이상의 일련의 기초로 사용 될 수 필요에 따라 [차등 데이터베이스 백업을](../../relational-databases/backup-restore/differential-backups-sql-server.md)합니다.|  
    |부분 데이터베이스|[부분 백업](../../relational-databases/backup-restore/partial-backups-sql-server.md) 은 읽기/쓰기 파일 그룹 및 하나 이상의 읽기 전용 파일이 나 파일 그룹입니다.<br /><br /> 각 부분 백업은 하나 이상의 일련의 기초로 사용 될 수 필요에 따라 [차등 부분 백업](../../relational-databases/backup-restore/differential-backups-sql-server.md)합니다.|  
    |파일 또는 파일 그룹|[파일 백업](../../relational-databases/backup-restore/full-file-backups-sql-server.md) 하나 이상의 파일 또는 파일 그룹을 포함 하 고 여러 개의 파일 그룹이 포함 하는 데이터베이스에 대해서만 관련이 있습니다. 단순 복구 모델에서 파일 백업은 기본적으로 읽기 전용 보조 파일 그룹으로 제한됩니다.<br /> 각 파일 백업은 하나 이상의 일련의 기초로 사용 될 수 필요에 따라 [차등 파일 백업을](../../relational-databases/backup-restore/differential-backups-sql-server.md)합니다.|  
  
-   전체 복구 모델 또는 대량 로그 복구 모델에서 기존 백업은 포함 순차적 *트랜잭션 로그 백업을* (또는 *로그 백업을*), 필요한 합니다. 각 로그 백업은 백업이 생성되었을 당시 활성 상태에 있었던 트랜잭션 로그 부분을 포함하며 이전 로그 백업에서 백업되지 않은 모든 로그 레코드를 포함합니다.  
  
     관리 오버헤드가 증가하더라도 작업 손실 가능성을 최소화하려면 자주 로그 백업을 예약해야 합니다. 전체 백업 사이에 차등 백업을 예약하면 데이터를 복원한 후 복원해야 하는 로그 백업 수가 감소하므로 복원 시간이 줄어들 수 있습니다.  
  
     로그 백업은 데이터베이스 백업과 별개의 볼륨에 보관하는 것이 좋습니다.  
  
    > [!NOTE]  
    >  첫 로그 백업을 만들려면 먼저 전체 백업을 만들어야 합니다.  
  
-   A *복사 전용 백업은* 특수 목적의 전체 백업 또는 정상적인 기존 백업 시퀀스와 독립적인 로그 백업입니다. 복사 전용 백업을 만들려면 BACKUP 문에 COPY_ONLY 옵션을 지정합니다. 자세한 내용은 [복사 전용 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)를 참조하세요.  
  
###  <a name="Tlog_Truncation"></a>트랜잭션 로그 잘림  
 데이터베이스의 트랜잭션 로그가 채워지는 것을 방지하려면 정기적인 백업이 중요합니다. 로그 잘림은 데이터베이스를 백업한 후에는 단순 복구 모델에서, 트랜잭션 로그를 백업한 후에는 전체 복구 모델에서 자동으로 발생합니다. 그러나 잘림 처리가 지연될 수 있는 경우도 있습니다. 로그 잘림을 지연시킬 수 있는 요소에 대한 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)를 참조하세요.  
  
> [!NOTE]  
>  BACKUP LOG WITH NO_LOG 및 WITH TRUNCATE_ONLY 옵션은 더 이상 지원되지 않습니다. 전체 또는 대량 로그 복구 모델 복구 사용 시 데이터베이스에서 로그 백업 체인을 제거해야 할 경우 단순 복구 모델로 전환하십시오. 자세한 내용은 [데이터베이스 복구 모델 보기 또는 변경&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)을 참조하세요.  
  
###  <a name="Formatting_Media"></a>백업 미디어 포맷  
 다음 조건이 충족되는 경우에만 BACKUP 문에 의해 백업 미디어가 포맷됩니다.  
  
-   FORMAT 옵션이 지정된 경우  
-   미디어가 비어 있는 경우  
-   작업이 연속 테이프를 기록하는 경우  
  
###  <a name="Backup_Devices_and_Media_Sets"></a>백업 장치 및 미디어 세트 사용  
  
#### <a name="backup-devices-in-a-striped-media-set-a-stripe-set"></a>스트라이프 미디어 세트(스트라이프 세트)의 백업 장치  
 A *세트 스트라이프* 집합 데이터 블록으로 분할 되 고 고정 순서로 분산 있는 디스크 파일입니다. 스트라이프 세트에 사용된 백업 장치 수는 미디어가 FORMAT으로 다시 초기화하지 않는 한 동일하게 유지해야 합니다.  
  
 다음 예에서는 3개의 디스크 파일을 사용하는 새 스트라이프 미디어 세트에 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 데이터베이스의 백업을 작성합니다.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO DISK='X:\SQLServerBackups\AdventureWorks1.bak',   
DISK='Y:\SQLServerBackups\AdventureWorks2.bak',   
DISK='Z:\SQLServerBackups\AdventureWorks3.bak'  
WITH FORMAT,  
   MEDIANAME = 'AdventureWorksStripedSet0',  
   MEDIADESCRIPTION = 'Striped media set for AdventureWorks2012 database;  
GO  
```  
  
 백업 장치가 스트라이프 세트의 일부로 정의되면 FORMAT을 지정하지 않을 경우 단일 장치 백업에 사용할 수 없습니다. 마찬가지로 스트라이프되지 않은 백업을 포함한 백업 장치는 FORMAT을 지정하지 않을 경우 스트라이프 세트에 사용될 수 없습니다. 스트라이프 백업 세트를 분할하려면 FORMAT을 사용하십시오.  
  
 미디어 헤더를 기록할 때 MEDIANAME 나 MEDIADESCRIPTION을 모두 지정은 빈 항목에 해당 하는 미디어 헤더 필드가 비어 있습니다.  
  
#### <a name="working-with-a-mirrored-media-set"></a>미러된 미디어 세트 작업  
 일반적으로 백업은 미러되지 않으며 BACKUP 문은 단순히 TO 절을 포함합니다. 그러나 미디어 세트당 총 4개의 미러를 사용할 수 있습니다. 미러된 미디어 세트의 경우 백업 작업에서는 여러 백업 장치 그룹에 기록합니다. 각 백업 장치 그룹은 미러된 미디어 세트 내에서 단일 미러를 구성합니다. 모든 미러는 동일한 수량과 유형의 물리적 백업 장치를 사용해야 하며 이 장치들은 모두 동일한 속성을 가지고 있어야 합니다.  
  
 미러된 미디어 세트로 백업하려면 모든 미러가 있어야 합니다. 미러된 미디어 세트로 백업하려면 TO 절을 지정하여 첫 번째 미러를 지정하고 MIRROR TO 절을 지정하여 각 추가 미러를 지정합니다.  
  
 미러된 미디어 세트의 경우 각 MIRROR TO 절은 TO 절과 동일한 수와 유형의 장치를 나열해야 합니다. 다음 예에서는 2개의 미러를 포함하고 미러당 3개의 장치를 사용하는 미러된 미디어 세트에 기록합니다.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO DISK='X:\SQLServerBackups\AdventureWorks1a.bak',   
DISK='Y:\SQLServerBackups\AdventureWorks2a.bak',   
DISK='Z:\SQLServerBackups\AdventureWorks3a.bak'  
MIRROR TO DISK='X:\SQLServerBackups\AdventureWorks1b.bak',   
DISK='Y:\SQLServerBackups\AdventureWorks2b.bak',   
DISK='Z:\SQLServerBackups\AdventureWorks3b.bak';  
GO  
```  
  
> [!IMPORTANT]  
>  이 예는 로컬 시스템에서 테스트할 수 있도록 디자인되었습니다. 실제로 같은 드라이브에서 여러 장치에 백업하면 성능이 저하될 수 있으며 미러된 미디어 세트에서 제공하도록 되어 있는 중복성이 제거됩니다.  
  
##### <a name="media-families-in-mirrored-media-sets"></a>미러된 미디어 세트의 미디어 패밀리  
 BACKUP 문의 TO 절에 지정된 각 백업 장치는 미디어 패밀리에 해당합니다. 예를 들어 TO 절에 3개의 장치가 나열되어 있으면 BACKUP은 3개의 미디어 패밀리에 데이터를 기록합니다. 미러된 미디어 세트에서 모든 미러에는 각 미디어 패밀리의 복사본이 있어야 합니다. 이로 인해 장치 수가 모든 미러에서 동일해야 합니다.  
  
 각 미러에 대해 여러 장치가 나열되어 있으면 장치의 순서에 따라 특정 장치에 기록할 미디어 패밀리가 결정됩니다. 예를 들어 각 장치 목록에서 두 번째 장치는 두 번째 미디어 패밀리에 해당됩니다. 다음 표에서는 위 예에서 언급한 장치에 대해 장치와 미디어 패밀리 간의 관계를 보여 줍니다.  
  
|미러|미디어 패밀리 1|미디어 패밀리 2|미디어 패밀리 3|  
|------------|--------------------|--------------------|--------------------|  
|0|`Z:\AdventureWorks1a.bak`|`Z:\AdventureWorks2a.bak`|`Z:\AdventureWorks3a.bak`|  
|1.|`Z:\AdventureWorks1b.bak`|`Z:\AdventureWorks2b.bak`|`Z:\AdventureWorks3b.bak`|  
  
 미디어 패밀리는 항상 특정 미러 내의 동일한 장치에 백업되어야 합니다. 따라서 기존 미디어 세트를 사용할 때마다 미디어 세트가 생성될 때 지정된 것과 동일한 순서로 각 미러의 장치를 나열하십시오.  
  
 미러된 미디어 세트에 대한 자세한 내용은 [미러된 백업 미디어 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)백업 및 복원의 기본적인 백업 미디어 관련 용어를 소개합니다. 미디어 세트 및 미디어 패밀리 일반에 대 한 자세한 내용은 참조 하십시오. [미디어 세트, 미디어 패밀리 및 백업 세트 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
###  <a name="Restoring_Backups"></a>SQL Server 백업 복원  
 데이터베이스를 복원 및 필요에 따라 온라인으로 전환 하거나 파일 또는 파일 그룹을 복원 하려면 복구를 하려면는 [!INCLUDE[tsql](../../includes/tsql-md.md)] [복원](../../t-sql/statements/restore-statements-transact-sql.md) 문 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **복원** 작업 합니다. 자세한 내용은 참조 하십시오. [복원 및 복구 개요 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
##  <a name="Additional_Considerations"></a>백업 옵션에 대 한 추가 고려 사항  
  
###  <a name="Interactions_SKIP_etc"></a>SKIP, NOSKIP, INIT 및 NOINIT의 상호 작용  
 이 표에서 간의 상호 작용은 { **NOINIT** | INIT}와 { **NOSKIP** | SKIP} 옵션입니다.  
  
> [!NOTE]  
>  테이프 미디어가 비어 있거나 디스크 백업 파일이 없는 경우에는 이러한 모든 상호 작용에서 미디어 헤더를 기록한 다음 작업을 계속 진행합니다. 미디어가 비어 있지 않은데도 유효한 미디어 헤더가 없는 경우에는 이러한 작업에서 유효한 MTF 미디어가 아니라는 사실을 알린 후 백업 작업을 종료합니다.  
  
||NOINIT|INIT|  
|------|------------|----------|  
|NOSKIP|볼륨에 유효한 미디어 헤더가 포함되어 있으면 미디어 이름이 지정된 MEDIANAME과 일치하는지 확인합니다. 이름이 일치하면 기존 백업 세트를 모두 유지하면서 백업 세트를 추가합니다.<br /> 볼륨에 유효한 미디어 헤더가 포함되어 있지 않으면 오류가 발생합니다.|볼륨에 유효한 미디어 헤더가 포함되어 있으면 다음 검사를 수행합니다.<br /> -지정 된 미디어 이름이 일치 하는지 미디어 헤더의 미디어 name.* * MEDIANAME이 지정 하는 경우 확인<br /> -미디어에 아직 만료 되지 않은 백업 세트가 없습니다 않은지 확인 합니다. 만료되지 않은 백업 세트가 있으면 백업을 종료합니다.<br /> 이러한 검사를 통과하면 미디어 헤더만 유지하며 미디어의 모든 백업 세트를 덮어씁니다.<br /> 볼륨에 유효한 미디어 헤더가 포함되어 있지 않으면 지정된 MEDIANAME 및 MEDIADESCRIPTION을 사용하여 미디어 헤더를 생성합니다.|  
|SKIP|볼륨에 유효한 미디어 헤더가 포함되어 있으면 기존 백업 세트를 모두 유지하면서 백업 세트를 추가합니다.|볼륨에 유효한 포함 되어 있으면 * 미디어 헤더를 미디어 헤더만 유지 하며 미디어의 모든 백업 세트를 덮어씁니다.<br /> 미디어가 비어 있으면 지정된 MEDIANAME 및 MEDIADESCRIPTION을 사용하여 미디어 헤더를 생성합니다.|  
  
 * 유효성에는 MTF 버전 번호와 기타 헤더 정보가 포함 됩니다. 지정한 버전이 지원되지 않거나 예기치 못한 값일 경우 오류가 발생합니다.  
  
 * * 적절 한 고정된 데이터베이스 또는 서버 역할에 백업 작업을 수행 하려면 사용자가 속해야 합니다.  
  
## <a name="compatibility"></a>호환성  
  
> [!CAUTION]  
>  최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 만든 백업은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복원할 수 없습니다.  
  
 BACKUP은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와의 호환성을 위해 RESTART 옵션을 지원합니다. 하지만 RESTART은 아무 효과가 없습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 데이터베이스와 트랜잭션 로그가 하나의 물리적 위치에 보관되도록 데이터베이스나 로그 백업을 디스크나 테이프 장치에 추가할 수 있습니다.  
  
 명시적 또는 암시적 트랜잭션에서는 BACKUP 문을 사용할 수 없습니다.  
  
 운영 체제가 데이터베이스의 데이터 정렬을 지원하는 한 프로세서 유형이 다르더라도 플랫폼 간 백업 작업을 수행할 수 있습니다.  
  
> [!NOTE]  
>  기본적으로 백업 작업을 성공적으로 수행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 시스템 이벤트 로그에 항목이 추가됩니다. 로그를 자주 백업하는 경우 이러한 성공 메시지는 바로 누적되므로 엄청난 오류 로그가 쌓여 다른 메시지를 찾기 힘들 수 있습니다. 이 경우 스크립트가 이러한 로그 항목에 종속되지 않을 경우 추적 플래그 3226을 사용하여 이러한 항목을 표시하지 않을 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.  
  
## <a name="interoperability"></a>상호 운용성  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 온라인 백업 프로세스를 사용하여 데이터베이스가 사용 중일 때도 데이터베이스 백업을 수행할 수 있습니다. 백업 시 대부분의 작업을 수행할 수 있습니다. 예를 들어 INSERT, UPDATE 또는 DELETE 문은 백업 작업 시에도 사용할 수 있습니다.  
  
 데이터베이스 또는 트랜잭션 로그 백업 시에 실행할 수 없는 작업은 다음과 같습니다.  
  
-   ADD FILE이나 REMOVE FILE 옵션과 함께 사용되는 ALTER DATABASE 문 등의 파일 관리 작업  
  
-   데이터베이스 축소 또는 파일 축소 작업. 자동 축소 작업도 포함됩니다.  
  
백업 작업이 파일 관리 또는 축소 작업과 겹치면 충돌이 발생합니다. 충돌하는 작업 중 어떤 작업이 먼저 시작되었는지에 관계없이 두 번째 작업은 첫 번째 작업이 설정한 잠금 시간이 초과될 때까지 대기합니다. 제한 시간은 세션 제한 시간 설정에서 제어합니다. 제한 시간 동안에 잠금이 해제되면 두 번째 작업이 계속됩니다. 잠금 제한 시간이 초과되면 두 번째 작업이 실패합니다.  
  
## <a name="metadata"></a>메타데이터  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 백업 작업을 추적하는 다음과 같은 백업 기록 테이블이 있습니다.  
  
-   [backupfile&#40; Transact SQL &#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)  
-   [backupfilegroup&#40; Transact SQL &#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
-   [backupmediafamily&#40; Transact SQL &#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
-   [backupmediaset&#40; Transact SQL &#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
-   [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
백업 세트에 아직 기록 되지 않았습니다 경우, 복원 수행 되는 **msdb** 데이터베이스, 백업 기록 테이블을 수정할 수도 있습니다.  
  
## <a name="security"></a>보안  
 부터는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], **암호** 및 **MEDIAPASSWORD** 옵션은 백업을 만드는 데 지원 되지 않습니다. 암호로 만든 백업을 여전히 복원할 수 있습니다.  
  
### <a name="permissions"></a>Permissions  
 BACKUP DATABASE 및 BACKUP LOG 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.  
  
 백업 장치의 물리적 파일에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 장치를 읽고 쓸 수 있어야 하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 쓰기 권한이 있어야 합니다. 그러나 시스템 테이블의 백업 장치에 대한 항목을 추가하는 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)는 파일 액세스 권한을 확인하지 않습니다. 백업 장치의 물리적 파일에서 발생하는 이러한 문제는 백업 또는 복원을 시도할 때 실제 리소스를 액세스하기 전까지는 발생하지 않습니다.  
  
##  <a name="examples"></a> 예  
 이 섹션에서는 다음과 같은 예를 보여 줍니다.  
  
-   1. [전체 데이터베이스 백업](#backing_up_db)  
-   2. [데이터베이스 및 로그 백업](#backing_up_db_and_log)  
-   3. [보조 파일 그룹의 전체 파일 백업 만들기](#full_file_backup)  
-   4. [보조 파일 그룹의 차등 파일 백업 만들기](#differential_file_backup)  
-   5. [세트 만들기 및 미러된 단일 패밀리 미디어에 백업](#create_single_family_mirrored_media_set)  
-   6. [세트 만들기 및 미러된 다중 패밀리 미디어에 백업](#create_multifamily_mirrored_media_set)  
-   G [미러된 미디어 세트를 기존의 백업](#existing_mirrored_media_set)  
-   8. [새 미디어 세트에 압축된 된 백업 만들기](#creating_compressed_backup_new_media_set)  
-   9.  [Microsoft Azure Blob 저장소 서비스에 백업](#url)  
  
> [!NOTE]  
>  백업 방법 도움말 항목에 추가적인 예가 포함되어 있습니다. 자세한 내용은 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)을 참조하세요.  
  
###  <a name="backing_up_db"></a> 1. 전체 데이터베이스 백업  
 다음 예에서는 백업에서 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 데이터베이스를 디스크 파일입니다.  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH FORMAT;  
GO  
```  
  
###  <a name="backing_up_db_and_log"></a> 2. 데이터베이스 및 로그 백업  
 다음 예에서는 기본적으로 단순 복구 모델을 사용하는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스를 백업하고 로그 백업을 지원하기 위해 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 전체 복구 모델을 사용하도록 수정합니다.  
  
 다음으로,이 예에서는 사용 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) 논리적 만들려는 [백업 장치](../../relational-databases/backup-restore/backup-devices-sql-server.md) 등 데이터를 백업 하기 위한 `AdvWorksData`, 로그를 백업 하기 위한 다른 논리적 백업 장치를 만듭니다 `AdvWorksLog`합니다.  
  
 마지막으로 `AdvWorksData`에 대한 전체 데이터베이스 백업을 만들고 업데이트 작업 기간이 경과된 후 로그를 `AdvWorksLog`에 백업합니다.  
  
```sql  
-- To permit log backups, before the full database backup, modify the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
   SET RECOVERY FULL;  
GO  
-- Create AdvWorksData and AdvWorksLog logical backup devices.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksData',   
'Z:\SQLServerBackups\AdvWorksData.bak';  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksLog',   
'X:\SQLServerBackups\AdvWorksLog.bak';  
GO  
  
-- Back up the full AdventureWorks2012 database.  
BACKUP DATABASE AdventureWorks2012 TO AdvWorksData;  
GO  
-- Back up the AdventureWorks2012 log.  
BACKUP LOG AdventureWorks2012  
   TO AdvWorksLog;  
GO  
```  
  
> [!NOTE]  
>  프로덕션 데이터베이스의 경우에는 로그를 정기적으로 백업하십시오. 로그 백업은 데이터 손실을 충분히 방지할 수 있을 만큼 자주 수행해야 합니다.  
  
###  <a name="full_file_backup"></a> 3. 보조 파일 그룹의 전체 파일 백업 만들기  
 다음 예에서는 두 보조 파일 그룹에 있는 모든 파일의 전체 파일 백업을 만듭니다.  
  
```sql  
--Back up the files in SalesGroup1:  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck';  
GO  
```  
  
###  <a name="differential_file_backup"></a> 4. 보조 파일 그룹의 차등 파일 백업 만들기  
 다음 예에서는 두 보조 파일 그룹에 있는 모든 파일의 차등 파일 백업을 만듭니다.  
  
```sql  
--Back up the files in SalesGroup1:  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck'  
   WITH   
      DIFFERENTIAL;  
GO  
```  
  
###  <a name="create_single_family_mirrored_media_set"></a> 5. 미러된 단일 패밀리 미디어 세트 만들기 및 백업  
 다음 예에서는 단일 미디어 패밀리와 4개의 미러를 포함하는 미러된 미디어 세트를 만들고 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 데이터베이스를 해당 미디어 세트에 백업합니다.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0'  
MIRROR TO TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2'  
MIRROR TO TAPE = '\\.\tape3'  
WITH  
   FORMAT,  
   MEDIANAME = 'AdventureWorksSet0';  
```  
  
###  <a name="create_multifamily_mirrored_media_set"></a> 6. 미러된 다중 패밀리 미디어 세트 만들기 및 백업  
 다음 예에서는 각 미러가 두 개의 미디어 패밀리로 구성되는 미러된 미디어 세트를 만듭니다. 그런 다음 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 데이터베이스를 두 미러에 백업합니다.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
   FORMAT,  
   MEDIANAME = 'AdventureWorksSet1';  
```  
  
###  <a name="existing_mirrored_media_set"></a>7. 기존 미러된 미디어 세트에 백업  
 다음 예에서는 앞부분에 나오는 예에서 만든 미디어 세트에 백업 세트를 추가합니다.  
  
```sql  
BACKUP LOG AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH   
   NOINIT,  
   MEDIANAME = 'AdventureWorksSet1';  
```  
  
> [!NOTE]  
>  기본값인 NOINIT는 쉽게 구분할 수 있도록 여기에 표시됩니다.  
  
###  <a name="creating_compressed_backup_new_media_set"></a>8. 새 미디어 세트에 압축된 백업 만들기  
 다음 예에서는 미디어를 포맷하여 새 미디어 세트를 만들고 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 데이터베이스에 대해 압축된 전체 백업을 수행합니다.  
  
```sql  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   COMPRESSION;  
```  

###  <a name="url"></a>I입니다. Microsoft Azure Blob 저장소 서비스에 백업 
이 예제에서는 수행의 전체 데이터베이스 백업을 `Sales` Microsoft Azure Blob 저장소 서비스에 있습니다.  저장소 계정 이름은 `mystorageaccount`입니다.  컨테이너는 `myfirstcontainer`입니다.  읽기, 쓰기, 삭제 및 나열 권한이 있는 저장된 액세스 정책을 만들었습니다.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, 저장 된 액세스 정책과 연결 된 공유 액세스 서명을 사용 하 여 만들어졌습니다.  에 대 한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows Azure Blob 저장소 서비스에 백업, 참조 [SQL Server 백업 및 Microsoft Azure Blob 저장소 서비스로 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) 및 [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)합니다.

```sql  
BACKUP DATABASE Sales
TO URL = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_20160726.bak'
WITH STATS = 5;
```

  
## <a name="see-also"></a>관련 항목:  
 [백업 장치&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [비상 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [DBCC sqlperf&#40; Transact SQL &#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [sp_addumpdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_helpfile &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_helpfilegroup &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [메모리 액세스에 최적화된 테이블이 있는 데이터베이스의 증분 복원](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md)  
  
  

