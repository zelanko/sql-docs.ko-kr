---
description: BACKUP(Transact-SQL)
title: BACKUP(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: afcf2e560b5fd4300c02ddf6bcc548ef68fdc05b
ms.sourcegitcommit: 3efd8bbf91f4f78dce3a4ac03348037d8c720e6a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91024572"
---
# <a name="backup-transact-sql"></a>BACKUP(Transact-SQL)

SQL 데이터베이스를 백업합니다.

작업 중인 특정 SQL 버전에 대한 구문, 인수, 설명, 사용 권한 및 예제를 보려면 다음 탭 중 하나를 클릭합니다.

구문 표기 규칙에 대한 자세한 내용은 [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)을 참조하십시오.

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [SQL Database<br />Managed Instance](backup-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](backup-transact-sql.md?view=aps-pdw-2016)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server"></a>SQL Server

전체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 백업하여 데이터베이스 백업을 만들거나 데이터베이스의 파일 하나 이상 또는 파일 그룹을 백업하여 파일 백업(BACKUP DATABASE)을 만듭니다. 또한 전체 복구 모델 또는 대량 로그 복구 모델에서 데이터베이스의 트랜잭션 로그를 백업하여 로그 백업(BACKUP LOG)을 만듭니다.

## <a name="syntax"></a>구문

```syntaxsql
--Backing Up a Whole Database
BACKUP DATABASE { database_name | @database_name_var }
  TO <backup_device> [ ,...n ]
  [ <MIRROR TO clause> ] [ next-mirror-to ]
  [ WITH { DIFFERENTIAL
           | <general_WITH_options> [ ,...n ] } ]
[;]

--Backing Up Specific Files or Filegroups
BACKUP DATABASE { database_name | @database_name_var }
 <file_or_filegroup> [ ,...n ]
  TO <backup_device> [ ,...n ]
  [ <MIRROR TO clause> ] [ next-mirror-to ]
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]
[;]

--Creating a Partial Backup
BACKUP DATABASE { database_name | @database_name_var }
 READ_WRITE_FILEGROUPS [ , <read_only_filegroup> [ ,...n ] ]
  TO <backup_device> [ ,...n ]
  [ <MIRROR TO clause> ] [ next-mirror-to ]
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]
[;]

--Backing Up the Transaction Log (full and bulk-logged recovery models)
BACKUP LOG
  { database_name | @database_name_var }
  TO <backup_device> [ ,...n ]
  [ <MIRROR TO clause> ] [ next-mirror-to ]
  [ WITH { <general_WITH_options> | \<log-specific_optionspec> } [ ,...n ] ]
[;]
  
<backup_device>::=
 {
  { logical_device_name | @logical_device_name_var }
 | {   DISK
     | TAPE
     | URL } =
     { 'physical_device_name' | @physical_device_name_var | 'NUL' }
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
   `SERVER CERTIFICATE` = Encryptor_Name | SERVER ASYMMETRIC KEY = Encryptor_Name
```

## <a name="arguments"></a>인수

DATABASE 전체 데이터베이스 백업을 지정합니다. 파일 및 파일 그룹의 목록이 지정되어 있으면 해당 파일 및 파일 그룹만 백업됩니다. 전체 또는 차등 데이터베이스 백업 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 백업을 복원할 때 일관성 있는 데이터베이스를 생성하기 위해 충분한 트랜잭션 로그를 백업합니다.

BACKUP DATABASE(데이터베이스 백업)로 만든 백업을 복원하면 전체 백업이 복원됩니다. 백업 내의 특정 시간이나 트랜잭션으로는 로그 백업만 복원할 수 있습니다.

> [!NOTE]
> 전체 데이터베이스 백업만 **master** 데이터베이스에서 수행할 수 있습니다.

LOG

트랜잭션 로그만 백업하도록 지정합니다. 성공적으로 실행된 마지막 로그 백업에서 현재 로그의 끝에 로그가 백업됩니다. 첫 로그 백업을 만들려면 먼저 전체 백업을 만들어야 합니다.

[RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md) 문에 `WITH STOPAT`, `STOPATMARK` 또는 `STOPBEFOREMARK`를 지정하면 백업 내의 특정 시간이나 트랜잭션으로 로그 백업을 복원할 수 있습니다.

> [!NOTE]
> 일반적인 로그 백업 후 `WITH NO_TRUNCATE` 또는 `COPY_ONLY`를 지정하지 않으면 일부 트랜잭션 로그 레코드가 비활성 상태가 됩니다. 하나 이상의 가상 로그 파일 내의 모든 레코드가 비활성 상태가 된 후에는 로그가 잘립니다. 일상적인 로그 백업 후 로그가 잘리지 않을 경우 로그 잘림이 지연되는 것일 수 있습니다. 자세한 내용은 [로그 잘림을 지연시킬 수 있는 요소](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation)를 참조하세요.

{ _database\_name_ |  **@** _database\_name\_var_ } 트랜잭션 로그, 일부 데이터베이스, 전체 데이터베이스가 백업되는 데이터베이스입니다. 변수( **@** _database\_name\_var_)로 제공된 경우, 이 이름은 문자열 상수( **@** _database\_name\_var_ **=** _database name_)나 **ntext** 또는 **text** 데이터 형식을 제외한 문자열 데이터 형식의 변수로 지정할 수 있습니다.

> [!NOTE]
> 데이터베이스 미러링 파트너 관계의 미러 데이터베이스는 백업할 수 없습니다.

\<file_or_filegroup> [ **,** ...*n* ] BACKUP DATABASE와 함께만 사용되며, 파일 백업에 포함시킬 데이터베이스 파일 또는 파일 그룹을 지정하거나 부분 백업에 포함시킬 읽기 전용 파일 또는 파일 그룹을 지정합니다.

FILE **=** { *logical_file_name* | **@** _logical\_file\_name\_var_ } 파일의 논리적 이름이거나 해당 값이 백업에 포함할 파일의 논리적 이름과 같은 변수입니다.

FILEGROUP **=** { _logical\_filegroup\_name_ |  **@** _logical\_filegroup\_name\_var_ } 파일 그룹의 논리적 이름이거나 해당 값이 백업에 포함시킬 파일 그룹의 논리적 이름과 같은 변수입니다. 단순 복구 모델에서 파일 그룹 백업은 읽기 전용 파일 그룹에만 사용할 수 있습니다.

> [!NOTE]
> 데이터베이스 크기와 성능 요구 사항으로 인해 데이터베이스 백업이 불가능할 경우 파일 백업을 사용하십시오. NUL 디바이스는 백업 성능을 테스트하는 데 사용할 수 있지만 프로덕션 환경에서는 사용하지 말아야 합니다.

*n* 쉼표로 구분된 목록에 여러 개의 파일 및 파일 그룹을 지정할 수 있음을 나타내는 자리 표시자입니다. 사용할 수 있는 숫자에는 제한이 없습니다.

자세한 내용은 [전체 파일 백업](../../relational-databases/backup-restore/full-file-backups-sql-server.md) 및 [파일 및 파일 그룹 백업](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)을 참조하세요.

READ_WRITE_FILEGROUPS [ **,** FILEGROUP = { _logical\_filegroup\_name_ |  **@** _logical\_filegroup\_name\_var_ } [ **,** ..._n_ ] ] 부분 백업을 지정합니다. 부분 백업은 주 파일 그룹, 모든 읽기/쓰기 보조 파일 그룹, 지정된 모든 읽기 전용 파일이나 파일 그룹과 같은 데이터베이스에 있는 모든 읽기/쓰기 파일을 포함합니다.

READ_WRITE_FILEGROUPS 부분 백업 시 모든 읽기/쓰기 파일 그룹을 백업하도록 지정합니다. 데이터베이스가 읽기 전용일 경우 READ_WRITE_FILEGROUPS에는 주 파일 그룹만 포함됩니다.

> [!IMPORTANT]
> READ_WRITE_FILEGROUPS 대신 FILEGROUP을 사용하여 읽기/쓰기 파일 그룹을 명시적으로 나열하면 파일 백업이 생성됩니다.

FILEGROUP = { *logical_filegroup_name* |  **@** _logical\_filegroup\_name\_var_ } 읽기 전용 파일 그룹의 논리적 이름이거나 해당 값이 부분 백업에 포함할 읽기 전용 파일 그룹의 논리적 이름과 같은 변수입니다. 자세한 내용은 이 주제의 앞부분에 있는 "\<file_or_filegroup>"을 참조하세요.

*n* 쉼표로 구분된 목록에 여러 개의 읽기 전용 파일 그룹을 지정할 수 있음을 나타내는 자리 표시자입니다.

부분 백업에 대한 자세한 내용은 [부분 백업](../../relational-databases/backup-restore/partial-backups-sql-server.md)을 참조하세요.

TO \<backup_device> [ **,** ...*n* ] 함께 제공되는 [백업 디바이스](../../relational-databases/backup-restore/backup-devices-sql-server.md) 세트가 미러되지 않은 미디어 세트이거나 하나 이상의 MIRROR TO 절이 선언된 경우 미러된 미디어 세트 내의 미러 중 첫 번째임을 나타냅니다.

\<backup_device>

백업 작업에 사용할 논리적 백업 디바이스나 물리적 백업 디바이스를 지정합니다.

{ *logical_device_name* \| **@** _logical\_device\_name\_var_ } **적용 대상:** SQL Server 데이터베이스를 백업할 백업 디바이스의 논리적 이름입니다. 논리적 이름은 식별자 규칙을 따라야 합니다. 변수(@*logical_device_name_var*)로 제공한 경우 백업 디바이스 이름은 문자열 상수(@_logical\_device\_name\_var_ **=** 논리적 백업 디바이스 이름)나 **ntext** 또는 **text** 데이터 형식을 제외한 문자열 데이터 형식의 변수로 지정할 수 있습니다.

{ DISK \| TAPE \| URL} **=** { **'** _physical\_device\_name_ **'** \| **@** _physical\_device\_name\_var_ \| 'NUL' } **적용 대상:** DISK, TAPE 및 URL이 SQL Server에 적용됩니다.
디스크 파일이나 테이프 디바이스 또는 Microsoft Azure Blob Storage 서비스를 지정합니다. URL 형식은 Microsoft Azure Storage 서비스에 대한 백업을 만드는 데 사용됩니다. 자세한 내용과 예제는 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요. 자습서는 [자습서: Microsoft Azure Blob Storage Service에 SQL Server 백업 및 복원](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)을 참조하세요.

> [!NOTE]
> NUL 디스크 디바이스는 전송된 모든 정보를 버리고 테스트용으로만 사용해야 합니다. 프로덕션용이 아닙니다.
> [!IMPORTANT]
> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2부터 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]까지는 URL로 백업할 때 단일 디바이스로만 백업할 수 있습니다. URL로 백업할 때 여러 디바이스에 백업하려면 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상을 사용해야 하고 SAS(공유 액세스 서명) 토큰을 사용해야 합니다. 공유 액세스 서명 만들기에 대한 자세한 내용은 [URL에 대한 SQL Server 백업](../../relational-databases/backup-restore/sql-server-backup-to-url.md) 및 [Powershell로 Azure Storage의 SAS(공유 액세스 서명) 토큰이 있는 SQL 자격 증명 만들기 간소화](https://docs.microsoft.com/archive/blogs/sqlcat/simplifying-creation-of-sql-credentials-with-shared-access-signature-sas-tokens-on-azure-storage-with-powershell)를 참조하세요.

**URL 적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 이상).

BACKUP 문에 지정되기 전에는 디스크 디바이스가 없어도 됩니다. 물리적 디바이스가 존재하고 BACKUP 문에서 INIT 옵션이 지정되지 않은 경우에는 백업이 디바이스에 추가됩니다.

> [!NOTE]
> NUL 디바이스는 이 파일로 보낸 모든 입력을 버리지만 백업은 모든 페이지를 백업된 것으로 표시합니다.

자세한 내용은 [백업 디바이스](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 참조하세요.

> [!NOTE]
> TAPE 옵션은 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.

*n* 쉼표로 구분된 목록에 백업 디바이스를 최대 64개까지 지정할 수 있음을 나타내는 자리 표시자입니다.

MIRROR TO \<backup_device> [ **,** ...*n* ] TO 절에 지정된 각각의 백업 디바이스를 미러할 최대 3개의 보조 백업 디바이스 세트를 지정합니다. MIRROR TO 절에는 TO 절에서와 같은 유형과 개수의 백업 디바이스를 지정해야 합니다. MIRROR TO 절은 최대 3개까지 포함시킬 수 있습니다.

이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 엔터프라이즈 버전에서만 사용할 수 있습니다.

> [!NOTE]
> MIRROR TO = DISK의 경우 BACKUP은 디스크의 섹터 크기에 따라 디스크 디바이스에 적절한 블록 크기를 자동으로 결정합니다. MIRROR TO 디스크가 기본 백업 디바이스로 지정된 디스크와 다른 섹터 크기로 포맷되면 백업 명령이 실패합니다. 백업을 섹터 크기가 다른 디바이스에 미러링하려면 BLOCKSIZE 매개 변수를 지정해야 하며, 모든 대상 디바이스 중에서 가장 높은 섹터 크기로 설정해야 합니다. 블록 크기에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "BLOCKSIZE"를 참조하세요.

\<backup_device> 이 섹션 앞부분에 나오는 "\<backup_device>"를 참조하세요.

*n* 쉼표로 구분된 목록에 백업 디바이스를 최대 64개까지 지정할 수 있음을 나타내는 자리 표시자입니다. MIRROR TO 절의 디바이스 수는 TO 절의 디바이스 수와 같아야 합니다.

자세한 내용은 이 항목의 뒷부분에 나오는 [주의 사항](#general-remarks) 섹션의 "미러된 미디어 세트의 미디어 패밀리"를 참조하세요.

[ *next-mirror-to* ] 단일 TO 절을 포함하여 단일 BACKUP 문에 MIRROR TO 절을 최대 3개까지 포함할 수 있음을 나타내는 자리 표시자입니다.

### <a name="with-options"></a>WITH 옵션

백업 작업에 사용할 옵션을 지정합니다.

CREDENTIAL **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 이상).
Microsoft Azure Blob Storage 서비스에 대한 백업을 만들 때에만 사용됩니다.

FILE_SNAPSHOT **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상).

Azure Blob 스토리지 서비스를 사용하여 모든 SQL Server 데이터베이스 파일을 저장할 때 데이터베이스 파일의 Azure 스냅샷을 만드는 데 사용됩니다. 자세한 내용은 [Microsoft Azure의 SQL Server 데이터 파일](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)을 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스냅샷 백업은 일관된 상태에서 데이터베이스 파일(데이터 및 로그 파일)의 Azure 스냅샷을 사용합니다. 일관된 Azure 스냅샷 집합이 백업을 구성하고 백업 파일에 기록됩니다. `BACKUP DATABASE TO URL WITH FILE_SNAPSHOT`과 `BACKUP LOG TO URL WITH FILE_SNAPSHOT`의 유일한 차이점은 후자는 트랜잭션 로그를 자르지만 전자는 그렇지 않다는 점입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Server 스냅샷 백업에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 백업 체인을 설정하는 데 필요한 초기 전체 백업 이후에 트랜잭션 로그 백업 시점으로 데이터베이스를 복원하려면 단일 트랜잭션 로그 백업만 필요합니다. 또한 두 건의 트랜잭션 로그 백업 시간 사이의 특정 시점으로 데이터베이스를 복원하려면 트랜잭션 로그 백업이 두 개만 필요합니다.

DIFFERENTIAL

BACKUP DATABASE와 함께만 사용되며 데이터베이스 또는 파일 백업이 마지막 전체 백업 이후 변경된 데이터베이스 또는 파일 부분으로만 구성되도록 지정합니다. 일반적으로 차등 백업은 전체 백업보다 적은 공간을 사용합니다. 마지막 전체 백업 이후 수행된 개별 로그 백업 중 일부를 적용할 필요가 없도록 하려면 이 옵션을 사용합니다.

> [!NOTE]
> 기본적으로 `BACKUP DATABASE`는 전체 백업을 만듭니다.

자세한 내용은 [차등 백업](../../relational-databases/backup-restore/differential-backups-sql-server.md)을 참조하세요.

ENCRYPTION 백업에 대한 암호화를 지정하는 데 사용됩니다. 백업을 암호화하는 데 사용할 암호화 알고리즘을 지정하거나 백업이 암호화되지 않도록 하려면 `NO_ENCRYPTION`을 지정할 수 있습니다. 암호화는 백업 파일을 보호하는 데 권장되는 방법입니다. 지정할 수 있는 알고리즘의 목록은 다음과 같습니다.

- `AES_128`
- `AES_192`
- `AES_256`
- `TRIPLE_DES_3KEY`
- `NO_ENCRYPTION`

암호화하도록 선택한 경우 암호기 옵션을 사용하여 암호기도 지정해야 합니다.

- `SERVER CERTIFICATE` = Encryptor_Name
- `SERVER ASYMMETRIC KEY` = Encryptor_Name

`SERVER CERTIFICATE` 및 `SERVER ASYMMETRIC KEY`는 `master` 데이터베이스에서 만든 비대칭 키와 인증서입니다. 자세한 내용은 각각 [`CREATE CERTIFICATE`](../../t-sql/statements/create-certificate-transact-sql.md) 및 [`CREATE ASYMMETRIC KEY`](../../t-sql/statements/create-asymmetric-key-transact-sql.md)을 참조하세요.

> [!WARNING]
> 암호화를 `FILE_SNAPSHOT` 인수와 함께 사용하면 메타데이터 파일 자체가 지정된 암호화 알고리즘을 사용하여 암호화되고 시스템에서 데이터베이스에 대해 [TDE(투명한 데이터 암호화)](../../relational-databases/security/encryption/transparent-data-encryption.md)가 완료되었는지 확인합니다. 데이터 자체에 대한 추가 암호화는 발생하지 않습니다. 데이터베이스가 암호화되지 않았거나 백업 문이 실행되기 전에 암호화가 완료되지 않으면 백업이 실패합니다.

**백업 세트 옵션**

이러한 옵션은 이 백업 작업에서 만든 백업 세트에서 작동합니다.

> [!NOTE]
> 복원 작업에 백업 세트를 지정하려면 `FILE = <backup_set_file_number>` 옵션을 사용합니다. 백업 세트를 지정하는 방법에 대한 자세한 내용은 [RESTORE 인수](../../t-sql/statements/restore-statements-arguments-transact-sql.md)에서 "백업 세트 지정"을 참조하세요.

COPY_ONLY 백업이 정상적인 백업 시퀀스에 영향을 주지 않는 복사 전용 백업(*copy-only backup*)임을 지정합니다. 복사 전용 백업은 정기적으로 예약되어 수행되는 기존 백업과는 별개로 생성됩니다. 복사 전용 백업은 백업 전체에 영향을 주지 않고 데이터베이스에 대한 프로시저를 복원합니다.

복사 전용 백업은 온라인 파일을 복원하기 전에 로그를 백업하는 것과 같은 특별한 목적을 위해 백업을 수행할 때 사용됩니다. 일반적으로 복사 전용 로그 백업은 한 번만 사용된 후 삭제됩니다.

- `BACKUP DATABASE`와 함께 사용하는 경우 `COPY_ONLY` 옵션은 차등 기반으로 사용할 수 없는 전체 백업을 만듭니다. 차등 비트맵은 업데이트되지 않으며 차등 백업은 복사 전용 백업이 없는 것처럼 작동합니다. 후속 차등 백업은 가장 최근의 기존 전체 백업을 기반으로 사용합니다.

    > [!IMPORTANT]
    > `DIFFERENTIAL`과 `COPY_ONLY`를 함께 사용하면 `COPY_ONLY`가 무시되고 차등 백업이 생성됩니다.

- `BACKUP LOG`와 함께 사용하는 경우 `COPY_ONLY` 옵션은 트랜잭션 로그를 자르지 않는 복사 전용 백업(*copy-only log backup*)을 만듭니다. 복사 전용 로그 백업은 로그 체인에 영향을 주지 않으며 기타 로그 백업은 복사 전용 백업이 없는 것처럼 작동합니다.

자세한 내용은 [복사 전용 백업](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)을 참조하세요.

{ COMPRESSION | NO_COMPRESSION } [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상 버전에서만 사용 가능합니다. 이 백업에서 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)을 수행하는지 여부를 지정하며 서버 수준의 기본값을 재정의합니다.

설치 시 백업 압축은 기본 동작이 아닙니다. 하지만 이 기본값은 [백업 압축 기본값](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) 서버 구성 옵션을 설정하여 변경할 수 있습니다. 이 옵션의 현재 값을 보는 방법은 [서버 속성 보기 또는 변경](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)을 참조하세요.

[TDE(투명한 데이터 암호화)](../../relational-databases/security/encryption/transparent-data-encryption.md) 가능 데이터베이스에 백업 압축 사용에 대한 자세한 내용은 [주의 사항](#general-remarks) 섹션을 참조하세요.

COMPRESSION 백업 압축을 명시적으로 사용하도록 설정합니다.

NO_COMPRESSION 백업 압축을 명시적으로 사용하지 않도록 설정합니다.

DESCRIPTION **=** { **'** _text_ **'**  |  **@** _text\_variable_ } 백업 세트를 설명하는 자유 형식의 텍스트를 지정합니다. 문자열을 최대 255자까지 지정할 수 있습니다.

NAME **=** { *backup_set_name* |  **@** _backup\_set\_var_ } 백업 세트의 이름을 지정합니다. 이름은 최대 128자까지 지정할 수 있습니다. NAME을 지정하지 않으면 공백이 됩니다.

{ EXPIREDATE **='** _date_ **'** | RETAINDAYS **=** _days_ } 이 백업에 대한 백업 세트를 덮어쓸 수 있는 날짜를 지정합니다. 두 옵션을 모두 사용하면 RETAINDAYS가 EXPIREDATE보다 우선적으로 적용됩니다.

두 옵션 모두 지정하지 않으면 **mediaretention** 구성 설정에 따라 만료 날짜가 결정됩니다. 자세한 내용은 [서버 구성 옵션](../../database-engine/configure-windows/server-configuration-options-sql-server.md)을 참조하세요.

> [!IMPORTANT]
> 이러한 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 파일을 덮어쓰지 못하도록 하기 위한 것입니다. 테이프는 다른 방법을 사용하여 지울 수 있고 디스크 파일은 운영 체제를 통해 삭제할 수 있습니다. 만료일 확인에 대한 자세한 내용은 이 항목에서 SKIP과 FORMAT을 참조하십시오.

EXPIREDATE **=** { **'** _date_ **'**  |  **@** _date\_var_ } 백업 세트가 만료되어 덮어쓸 수 있는 날짜를 지정합니다. 변수(@_date\_var_)로 제공한 경우 이 날짜는 구성된 시스템 **datetime** 형식을 따라야 하며 다음 중 하나로 지정해야 합니다.

- 문자열 상수(@_date\_var_ **=** date)
- **ntext** 또는 **text** 데이터 형식을 제외한 문자열 데이터 형식의 변수
- **smalldatetime**
- **datetime** 변수

예를 들면 다음과 같습니다.

- `'Dec 31, 2020 11:59 PM'`
- `'1/1/2021'`

**datetime** 값을 지정하는 방법에 대한 자세한 내용은 [날짜 및 시간 형식](../../t-sql/data-types/date-and-time-types.md)을 참조하세요.

> [!NOTE]
> 만료 날짜를 무시하려면 `SKIP` 옵션을 사용합니다.

RETAINDAYS **=** { *days* |  **@** _days\_var_ } 백업 미디어 세트를 덮어쓰지 않고 보존할 일 수를 지정합니다. 변수( **@** _days\_var_)로 제공한 경우 정수로 지정해야 합니다.

**미디어 세트 옵션**

이러한 옵션은 전체 미디어 세트에서 작동합니다.

{ **NOINIT** | INIT } 백업 작업이 백업 미디어의 기존 백업 세트에 추가되는지 또는 이를 덮어쓰는지 여부를 제어합니다. 기본적으로 백업 작업은 미디어의 최신 백업 세트에 추가됩니다(NOINIT).

> [!NOTE]
> { **NOINIT** | INIT }와 { **NOSKIP** | SKIP } 간 상호 작용에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 [주의 사항](#general-remarks)을 참조하세요.

NOINIT 백업 세트가 기존 백업 세트를 보존하면서 지정된 미디어 세트에 추가되는 것을 나타냅니다. 미디어 세트에 미디어 암호가 정의되어 있는 경우에는 암호를 제공해야 합니다. NOINIT는 기본값입니다.

자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)를 참조하세요.

INIT 미디어 헤더만 보존하고 모든 백업 세트를 덮어쓰도록 지정합니다. INIT가 지정되면 조건이 허용되는 경우 해당 디바이스의 기존 백업 세트를 모두 덮어씁니다. 기본적으로 BACKUP은 다음 조건을 확인하고 둘 중 한 조건에 해당되면 백업 미디어를 덮어쓰지 않습니다.

- 백업 세트가 아직 만료되지 않은 경우. 자세한 내용은 `EXPIREDATE` 및 `RETAINDAYS` 옵션을 참조하세요.
- BACKUP 문에 지정된 백업 세트 이름이 백업 미디어에 있는 이름과 일치하지 않을 경우. 자세한 내용은 이 섹션의 앞부분에 나오는 NAME 옵션을 참조하십시오.

이러한 검사를 무시하려면 `SKIP` 옵션을 사용합니다.

자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)를 참조하세요.

{ **NOSKIP** | SKIP } 백업 작업에서 미디어에 있는 백업 세트의 만료 날짜 및 시간을 덮어쓰기 전에 검사하는지 여부를 제어합니다.

> [!NOTE]
> { **NOINIT** | INIT }와 { **NOSKIP** | SKIP } 간 상호 작용에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의 사항"을 참조하세요.

NOSKIP BACKUP 문이 백업 세트를 덮어쓰기 전에 미디어에 있는 모든 백업 세트의 만료 날짜를 확인하도록 지정합니다. 기본 동작입니다.

SKIP 백업 세트를 덮어쓰지 않도록 BACKUP 문에서 일반적으로 수행되는 백업 세트 만료 날짜와 이름 확인을 해제합니다. { INIT | NOINIT }와 { NOSKIP | SKIP } 간 상호 작용에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.
백업 세트의 만료 날짜를 보려면 [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) 기록 테이블의 **expiration_date** 열을 쿼리합니다.

{ **NOFORMAT** | FORMAT } 이 백업 작업에 사용된 볼륨에 미디어 헤더를 기록하여 기존 미디어 헤더와 백업 세트를 덮어써야 하는지 여부를 지정합니다.

NOFORMAT 백업 작업에서 이 작업에 사용된 미디어 볼륨의 기존 미디어 헤더와 백업 세트를 유지하도록 지정합니다. 기본 동작입니다.

FORMAT 새 미디어 세트가 만들어지도록 지정합니다. FORMAT을 사용하면 백업 작업에서 해당 작업에 사용된 모든 미디어 볼륨의 새 미디어 헤더를 기록합니다. 이때 볼륨의 기존 내용은 기존의 모든 미디어 헤더와 백업 세트가 덮어쓰이므로 사용할 수 없게 됩니다.

> [!IMPORTANT]
> `FORMAT`은 신중하게 사용하십시오. 미디어 세트의 볼륨을 포맷하면 전체 미디어 세트를 사용할 수 없게 됩니다. 예를 들어 기존 스트라이프 미디어 세트에 속하는 테이프 하나를 초기화하면 전체 미디어 세트를 사용할 수 없게 됩니다.

FORMAT 지정은 `SKIP`을 의미하며 `SKIP`은 명시적으로 지정할 필요가 없습니다.

MEDIADESCRIPTION **=** { *text* | **@** _text\_variable_ } 미디어 세트에 대한 자유 형식의 텍스트 설명을 최대 255자까지 지정합니다.

MEDIANAME **=** { *media_name* |  **@** _media\_name\_variable_ } 전체 백업 미디어 세트에 대한 미디어 이름을 지정합니다. 미디어 이름은 128자 이하여야 합니다. `MEDIANAME`을 지정하면 백업 볼륨에 이미 있는 이전에 지정한 미디어 이름과 일치해야 합니다. 지정하지 않거나 SKIP 옵션을 지정하면 미디어 이름에 대한 확인을 수행하지 않습니다.

BLOCKSIZE **=** { *blocksize* |  **@** _blocksize\_variable_ } 물리적 블록 크기(바이트)를 지정합니다. 지원되는 크기는 512, 1024, 2048, 4096, 8192, 16384, 32768 및 65536(64KB) 바이트입니다. 테이프 디바이스의 기본값은 65536이고 그렇지 않은 경우에는 512입니다. 일반적으로 BACKUP에서 디바이스에 적합한 블록 크기를 자동으로 선택하기 때문에 이 옵션은 필요하지 않습니다. 명시적으로 지정된 블록 크기는 자동 선택된 블록 크기보다 우선 적용됩니다.

CD-ROM으로 복사하거나 CD-ROM에서 복원할 백업을 만드는 경우 BLOCKSIZE=2048을 지정합니다.

> [!NOTE]
> 이 옵션은 일반적으로 테이프 디바이스에 쓰는 경우에만 성능에 영향을 줍니다.

**데이터 전송 옵션**

BUFFERCOUNT **=** { *buffercount* |  **@** _buffercount\_variable_ } 백업 작업에 사용되는 I/O 버퍼의 총 수를 지정합니다. 임의의 양의 정수를 지정할 수 있지만 버퍼 수가 많으면 Sqlservr.exe 프로세스의 부적절한 가상 주소 공간으로 인해 "메모리가 부족합니다"라는 오류가 발생할 수 있습니다.

버퍼에 사용되는 총 공간은 다음 식으로 결정됩니다. `BUFFERCOUNT * MAXTRANSFERSIZE`.

> [!NOTE]
> `BUFFERCOUNT` 옵션을 사용하는 방법은 [잘못된 BufferCount 데이터 전송 옵션을 사용하면 OOM 상태가 발생할 수 있음](https://docs.microsoft.com/archive/blogs/sqlserverfaq/incorrect-buffercount-data-transfer-option-can-lead-to-oom-condition) 블로그를 참조하세요.

MAXTRANSFERSIZE **=** { *maxtransfersize* | _**@** maxtransfersize\_variable_ } [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 백업 미디어 간에 사용되는 가장 큰 전송 단위(바이트)를 지정합니다. 가능한 값은 최대 4194304바이트(4MB)까지 65536바이트(64KB)의 배수입니다.

> [!NOTE]
> SQL 기록기 서비스를 사용하여 백업을 만들 때 데이터베이스에서 [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md)이 구성되었거나 [메모리 최적화 파일 그룹](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)이 포함된 경우 복원 시 `MAXTRANSFERSIZE`가 백업을 만들 때 사용된 `MAXTRANSFERSIZE`보다 커야 합니다.

> [!NOTE]
> 단일 데이터 파일이 있는 [TDE(투명한 데이터 암호화)](../../relational-databases/security/encryption/transparent-data-encryption.md) 가능 데이터베이스의 경우 기본 `MAXTRANSFERSIZE`는 65536(64 KB)입니다. 비-TDE 암호화된 데이터베이스의 경우 디스크 백업을 사용할 때 기본 `MAXTRANSFERSIZE`는 1048576(1MB)이고 VDI 또는 TAPE를 사용하는 경우에는 65536(64KB)입니다.
> TDE 암호화된 데이터베이스에 백업 압축 사용에 대한 자세한 내용은 [주의 사항](#general-remarks) 섹션을 참조하세요.

**오류 관리 옵션**

이러한 옵션을 사용하면 백업 작업에 대해 백업 체크섬을 설정할 수 있는지 여부와 오류 발생 시 해당 작업을 중지할지 여부를 결정할 수 있습니다.

{ **NO_CHECKSUM** | CHECKSUM } 백업 체크섬의 설정 여부를 제어합니다.

NO_CHECKSUM 백업 체크섬 생성 및 페이지 체크섬의 유효성 검사를 명시적으로 사용하지 않도록 설정합니다. 기본 동작입니다.

CHECKSUM 백업 작업이 각 페이지의 체크섬과 조각난 페이지를 확인하고 사용 가능할 경우 전체 백업에 대해 체크섬을 생성하도록 지정합니다.

백업 체크섬을 사용하면 작업 및 백업 처리량에 영향을 줄 수 있습니다.

자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.

{ **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR } 페이지 체크섬 오류가 발생한 후 백업 작업을 중지할지, 아니면 계속할지를 제어합니다.

STOP_ON_ERROR 페이지 체크섬에서 확인하지 않을 경우 BACKUP이 실패하도록 지정합니다. 기본 동작입니다.

CONTINUE_AFTER_ERROR 잘못된 체크섬이나 조각난 페이지 등의 오류가 발생하더라도 BACKUP을 계속하도록 지시합니다.

데이터베이스가 손상된 경우 NO_TRUNCATE 옵션을 사용하여 비상 로그 백업을 수행할 수 없으면 NO_TRUNCATE 대신 CONTINUE_AFTER_ERROR를 지정하여 [비상 로그 백업](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 수행할 수 있습니다.

자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.

**호환성 옵션**

RESTART [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 아무 효과가 없습니다. 이 옵션은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와의 호환성을 위해 사용됩니다.

**모니터링 옵션**

STATS [ **=** _percentage_ ] 새로 *percentage*가 완료될 때마다 메시지를 표시하여 진행 상태를 측정하는 데 사용됩니다. *percentage*를 생략하면 10%가 완료될 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 메시지를 표시합니다.

STATS 옵션은 다음 간격을 보고할 임계값에 도달한 시점까지의 완료 백분율을 보고합니다. 간격은 지정된 비율을 대략적으로 나타냅니다. 예를 들어 STATS=10인 경우 완료된 크기가 40%이면 옵션은 43%를 표시할 수 있습니다. 대용량 백업 세트의 경우 완료 백분율이 완료된 I/O 호출 간에 매우 느리게 진행되므로 문제가 되지 않습니다.

**테이프 옵션**

이러한 옵션은 테이프 디바이스에만 사용됩니다. 테이프가 아닌 디바이스를 사용할 경우 이러한 옵션은 무시됩니다.

{ **REWIND** | NOREWIND } REWIND

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 테이프를 해제한 다음, 되감도록 지정합니다. 기본값은 REWIND입니다.

NOREWIND

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 백업 작업 후에 테이프를 열어 놓도록 지정합니다. 테이프에 여러 개의 백업 작업을 수행할 때 이 옵션을 사용하면 성능을 향상시킬 수 있습니다.

NOREWIND는 NOUNLOAD를 의미하며 두 옵션은 단일 BACKUP 문 내에서 호환되지 않습니다.

> [!NOTE]
> `NOREWIND`를 사용하는 경우 같은 프로세스에서 실행 중인 BACKUP 또는 RESTORE 문이 `REWIND` 또는 `UNLOAD` 옵션을 사용하거나 서버 인스턴스가 종료될 때까지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 테이프 드라이브에 대한 소유권을 보유합니다. 테이프를 열어 두면 다른 프로세스에서 테이프를 액세스하는 것을 방지합니다. 열린 테이프 목록을 표시하고 열린 테이프를 닫는 방법은 [백업 디바이스](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 참조하세요.

{ **UNLOAD** | NOUNLOAD }

> [!NOTE]
> `UNLOAD` 및 `NOUNLOAD`는 세션 기간 동안이나 다른 옵션을 지정하여 다시 설정할 때까지 유지되는 세션 설정입니다.

UNLOAD

백업이 끝나면 테이프를 자동으로 되감고 언로드되도록 지정합니다. UNLOAD는 세션 시작 시의 기본값입니다.

NOUNLOAD

BACKUP 작업 후에 테이프가 테이프 드라이브에 로드된 상태로 남아 있도록 지정합니다.

> [!NOTE]
> 테이프 백업 디바이스에 백업하는 경우 `BLOCKSIZE` 옵션은 백업 작업의 성능에 영향을 줍니다. 이 옵션은 일반적으로 테이프 디바이스에 쓰는 경우에만 성능에 영향을 줍니다.

**로그 관련 옵션**

이러한 옵션은 `BACKUP LOG`와 함께만 사용됩니다.

> [!NOTE]
> 로그 백업을 수행하지 않으려면 단순 복구 모델을 사용합니다. 자세한 내용은 [복구 모델](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.

{ NORECOVERY | STANDBY **=** _undo_file_name_ }

NORECOVERY

비상 로그를 백업하고 데이터베이스를 RESTORING 상태로 유지합니다. NORECOVERY는 보조 데이터베이스로 장애 조치(failover)하거나 RESTORE 작업에 앞서 비상 로그를 저장할 때 유용합니다.

로그 잘림을 건너뛰는 최상의 로그 백업을 수행한 다음, 데이터베이스를 자동으로 다시 RESTORING 상태로 되돌리려면 `NO_TRUNCATE` 및 `NORECOVERY` 옵션을 함께 사용하십시오.

STANDBY **=** _standby_file_name_

비상 로그를 백업하고 데이터베이스를 읽기 전용 및 STANDBY 상태로 유지합니다. STANDBY 절은 대기 데이터를 쓰고 롤백을 수행하지만 추가 복원 옵션을 사용해야 합니다. STANDBY 옵션 사용은 BACKUP LOG WITH NORECOVERY를 사용한 다음 RESTORE WITH STANDBY를 사용하는 것과 동일합니다.

대기 모드를 사용하려면 *standby_file_name*으로 지정하는 대기 파일이 필요합니다. 이 파일의 위치는 데이터베이스의 로그에 저장됩니다. 지정한 파일이 이미 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 해당 파일을 덮어쓰고 파일이 없으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 파일을 만듭니다. 대기 파일은 데이터베이스의 일부가 됩니다.

이 파일에는 롤백된 변경 내용이 저장되는데 다음에 RESTORE LOG를 적용하려는 경우 이 변경 내용은 취소해야 합니다. 커밋되지 않은 트랜잭션을 롤백하여 수정된 데이터베이스의 고유한 페이지가 모두 들어갈 수 있도록 대기 파일이 증가되므로 디스크 공간이 충분히 있어야 합니다.

NO_TRUNCATE

로그가 잘리지 않도록 지정하고 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 데이터베이스 상태에 관계없이 백업을 시도하도록 합니다. 따라서 `NO_TRUNCATE` 옵션으로 수행된 백업의 메타데이터는 완전하지 않을 수 있습니다. 이 옵션을 사용하면 데이터베이스가 손상된 경우에도 로그를 백업할 수 있습니다.

BACKUP LOG의 NO_TRUNCATE 옵션은 COPY_ONLY와 CONTINUE_AFTER_ERROR를 모두 지정하는 것과 같습니다.

`NO_TRUNCATE` 옵션을 사용하지 않으면 데이터베이스가 ONLINE 상태여야 합니다. 데이터베이스가 SUSPENDED 상태이면 `NO_TRUNCATE`를 지정하여 백업을 만들 수 있습니다. 그러나 데이터베이스가 OFFLINE 또는 EMERGENCY 상태이면 `NO_TRUNCATE`에서도 BACKUP을 사용할 수 없습니다. 데이터베이스 상태에 대한 내용은 [데이터베이스 상태](../../relational-databases/databases/database-states.md)를 참조하세요.

## <a name="about-working-with-sql-server-backups"></a>SQL Server 백업 사용 정보

이 섹션에서는 다음 필수 백업 개념을 설명합니다.

[백업 유형](#Backup_Types)
[트랜잭션 로그 잘림](#Tlog_Truncation)
[백업 미디어 포맷](#Formatting_Media)
[백업 디바이스 및 미디어 사용](#Backup_Devices_and_Media_Sets)
[SQL Server 백업 복원](#Restoring_Backups)

> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 백업에 대한 소개는 [백업 개요](../../relational-databases/backup-restore/backup-overview-sql-server.md)를 참조하세요.

### <a name="backup-types"></a><a name="Backup_Types"></a> 백업 유형

지원되는 백업 유형은 다음과 같이 데이터베이스의 복구 모델에 따라 달라집니다.

- 모든 복구 모델은 데이터의 전체 및 차등 백업을 지원합니다.

    |백업 범위|Backup 유형|
    |---------------------|------------------|
    |전체 데이터베이스|[데이터베이스 백업](../../relational-databases/backup-restore/full-database-backups-sql-server.md)은 전체 데이터베이스를 포함합니다.<br /><br /> 필요에 따라, 각 데이터베이스 백업은 하나 이상의 일련의 [차등 데이터베이스 백업](../../relational-databases/backup-restore/differential-backups-sql-server.md)의 기반으로 사용될 수 있습니다.|
    |부분 데이터베이스|[부분 백업](../../relational-databases/backup-restore/partial-backups-sql-server.md)은 읽기/쓰기 파일 그룹과 필요에 따라 하나 이상의 읽기 전용 파일 또는 파일 그룹을 포함합니다.<br /><br /> 필요에 따라, 각 부분 백업은 하나 이상의 일련의 [차등 부분 백업](../../relational-databases/backup-restore/differential-backups-sql-server.md)의 기반으로 사용될 수 있습니다.|
    |파일 또는 파일 그룹|[파일 백업](../../relational-databases/backup-restore/full-file-backups-sql-server.md)은 하나 이상의 파일 또는 파일 그룹을 포함하며 여러 파일 그룹을 포함하는 데이터베이스에만 해당됩니다. 단순 복구 모델에서 파일 백업은 기본적으로 읽기 전용 보조 파일 그룹으로 제한됩니다.<br /> 필요에 따라, 각 파일 백업은 하나 이상의 일련의 [차등 파일 백업](../../relational-databases/backup-restore/differential-backups-sql-server.md)의 기반으로 사용될 수 있습니다.|

- 전체 복구 모델이나 대량 로그 복구 모델에서 기존 백업은 필요한 순차적 *트랜잭션 로그 백업* 또는 *로그 백업*도 포함합니다. 각 로그 백업은 백업이 생성되었을 당시 활성 상태에 있었던 트랜잭션 로그 부분을 포함하며 이전 로그 백업에서 백업되지 않은 모든 로그 레코드를 포함합니다.

    관리 오버헤드가 증가하더라도 작업 손실 가능성을 최소화하려면 자주 로그 백업을 예약해야 합니다. 전체 백업 사이에 차등 백업을 예약하면 데이터를 복원한 후 복원해야 하는 로그 백업 수가 감소하므로 복원 시간이 줄어들 수 있습니다.

     로그 백업은 데이터베이스 백업과 별개의 볼륨에 보관하는 것이 좋습니다.

    > [!NOTE]
    > 첫 로그 백업을 만들려면 먼저 전체 백업을 만들어야 합니다.

- *복사 전용 백업*은 정상적인 기존 백업 시퀀스와 독립적인 특수 목적의 전체 백업 또는 로그 백업입니다. 복사 전용 백업을 만들려면 BACKUP 문에 COPY_ONLY 옵션을 지정합니다. 자세한 내용은 [복사 전용 백업](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)을 참조하세요.

### <a name="transaction-log-truncation"></a><a name="Tlog_Truncation"></a> 트랜잭션 로그 잘림

데이터베이스의 트랜잭션 로그가 채워지는 것을 방지하려면 정기적인 백업이 중요합니다. 로그 잘림은 데이터베이스를 백업한 후에는 단순 복구 모델에서, 트랜잭션 로그를 백업한 후에는 전체 복구 모델에서 자동으로 발생합니다. 그러나 잘림 처리가 지연될 수 있는 경우도 있습니다. 로그 잘림을 지연시킬 수 있는 요소에 대한 자세한 내용은 [트랜잭션 로그](../../relational-databases/logs/the-transaction-log-sql-server.md)를 참조하세요.

> [!NOTE]
> `BACKUP LOG WITH NO_LOG` 및 `WITH TRUNCATE_ONLY` 옵션은 더 이상 지원되지 않습니다. 전체 또는 대량 로그 복구 모델 복구 사용 시 데이터베이스에서 로그 백업 체인을 제거해야 할 경우 단순 복구 모델로 전환하십시오. 자세한 내용은 [데이터베이스 복구 모델 보기 또는 변경](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)을 참조하세요.

### <a name="formatting-backup-media"></a><a name="Formatting_Media"></a> 백업 미디어 포맷

다음 조건이 충족되는 경우에만 BACKUP 문에 의해 백업 미디어가 포맷됩니다.

- `FORMAT` 옵션이 지정된 경우
- 미디어가 비어 있는 경우
- 작업이 연속 테이프를 기록하는 경우

### <a name="working-with-backup-devices-and-media-sets"></a><a name="Backup_Devices_and_Media_Sets"></a> 백업 디바이스 및 미디어 세트 사용

#### <a name="backup-devices-in-a-striped-media-set-a-stripe-set"></a>다중 미디어 세트(스트라이프 세트)의 백업 디바이스
*스트라이프 세트*는 데이터가 블록으로 구분되고 고정 순서로 분산되는 디스크 파일 세트입니다. 스트라이프 세트에 사용된 백업 디바이스 수는 미디어가 `FORMAT`으로 다시 초기화하지 않는 한 동일하게 유지해야 합니다.

다음 예에서는 3개의 디스크 파일을 사용하는 새 스트라이프 미디어 세트에 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 데이터베이스의 백업을 작성합니다.

```sql
BACKUP DATABASE AdventureWorks2012
TO DISK='X:\SQLServerBackups\AdventureWorks1.bak',
DISK='Y:\SQLServerBackups\AdventureWorks2.bak',
DISK='Z:\SQLServerBackups\AdventureWorks3.bak'
WITH FORMAT,
  MEDIANAME = 'AdventureWorksStripedSet0',
  MEDIADESCRIPTION = 'Striped media set for AdventureWorks2012 database';
GO
```

백업 디바이스가 스트라이프 세트의 일부로 정의되면 FORMAT을 지정하지 않을 경우 단일 디바이스 백업에 사용할 수 없습니다. 마찬가지로 스트라이프되지 않은 백업을 포함한 백업 디바이스는 FORMAT을 지정하지 않을 경우 스트라이프 세트에 사용될 수 없습니다. 스트라이프 백업 세트를 분할하려면 FORMAT을 사용하십시오.

미디어 헤더를 기록할 때 MEDIANAME 또는 MEDIADESCRIPTION을 지정하지 않으면 빈 항목에 해당하는 미디어 헤더 필드가 비어 있게 됩니다.

#### <a name="working-with-a-mirrored-media-set"></a>미러된 미디어 세트 작업

일반적으로 백업은 미러되지 않으며 BACKUP 문은 단순히 TO 절을 포함합니다. 그러나 미디어 세트당 총 4개의 미러를 사용할 수 있습니다. 미러된 미디어 세트의 경우 백업 작업에서는 여러 백업 디바이스 그룹에 기록합니다. 각 백업 디바이스 그룹은 미러된 미디어 세트 내에서 단일 미러를 구성합니다. 모든 미러는 동일한 수량과 유형의 물리적 백업 디바이스를 사용해야 하며 이 디바이스들은 모두 동일한 속성을 가지고 있어야 합니다.

미러된 미디어 세트로 백업하려면 모든 미러가 있어야 합니다. 미러된 미디어 세트로 백업하려면 `TO` 절을 지정하여 첫 번째 미러를 지정하고 `MIRROR TO` 절을 지정하여 각 추가 미러를 지정합니다.

미러된 미디어 세트의 경우 각 `MIRROR TO` 절은 TO 절과 동일한 수와 유형의 디바이스를 나열해야 합니다. 다음 예에서는 2개의 미러를 포함하고 미러당 3개의 디바이스를 사용하는 미러된 미디어 세트에 기록합니다.

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
> 이 예는 로컬 시스템에서 테스트할 수 있도록 디자인되었습니다. 실제로 같은 드라이브에서 여러 디바이스에 백업하면 성능이 저하될 수 있으며 미러된 미디어 세트에서 제공하도록 되어 있는 중복성이 제거됩니다.

##### <a name="media-families-in-mirrored-media-sets"></a>미러된 미디어 세트의 미디어 패밀리

BACKUP 문의 `TO` 절에 지정된 각 백업 디바이스는 미디어 패밀리에 해당합니다. 예를 들어 `TO` 절에 3개의 디바이스가 나열되어 있으면 BACKUP은 3개의 미디어 패밀리에 데이터를 기록합니다. 미러된 미디어 세트에서 모든 미러에는 각 미디어 패밀리의 복사본이 있어야 합니다. 이로 인해 디바이스 수가 모든 미러에서 동일해야 합니다.

각 미러에 대해 여러 디바이스가 나열되어 있으면 디바이스의 순서에 따라 특정 디바이스에 기록할 미디어 패밀리가 결정됩니다. 예를 들어 각 디바이스 목록에서 두 번째 디바이스는 두 번째 미디어 패밀리에 해당됩니다. 다음 표에서는 위 예에서 언급한 디바이스에 대해 디바이스와 미디어 패밀리 간의 관계를 보여 줍니다.

|미러|미디어 패밀리 1|미디어 패밀리 2|미디어 패밀리 3|
|---------|---------|---------|---------|
|0|`Z:\AdventureWorks1a.bak`|`Z:\AdventureWorks2a.bak`|`Z:\AdventureWorks3a.bak`|
|1|`Z:\AdventureWorks1b.bak`|`Z:\AdventureWorks2b.bak`|`Z:\AdventureWorks3b.bak`|

 미디어 패밀리는 항상 특정 미러 내의 동일한 디바이스에 백업되어야 합니다. 따라서 기존 미디어 세트를 사용할 때마다 미디어 세트가 생성될 때 지정된 것과 동일한 순서로 각 미러의 디바이스를 나열하십시오.

미러된 미디어 세트에 대한 자세한 내용은 [미러된 백업 미디어 세트](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)를 참조하세요. 일반적인 미디어 세트 및 미디어 패밀리에 대한 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)를 참조하세요.

### <a name="restoring-sql-server-backups"></a><a name="Restoring_Backups"></a> SQL Server 백업 복원

데이터베이스를 복원하고, 필요에 따라 복구하여 온라인 상태로 만들거나 파일 또는 파일 그룹을 복원하려면 [!INCLUDE[tsql](../../includes/tsql-md.md)] [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 문 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **복원** 작업을 사용합니다. 자세한 내용은 [복원 및 복구 개요](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)를 참조하세요.

## <a name="additional-considerations-about-backup-options"></a><a name="Additional_Considerations"></a> BACKUP 옵션에 대한 추가 고려 사항

### <a name="interaction-of-skip-noskip-init-and-noinit"></a><a name="Interactions_SKIP_etc"></a> SKIP, NOSKIP, INIT, NOINIT의 상호 작용

다음 표에서는 { **NOINIT** | INIT }와 { **NOSKIP** | SKIP } 옵션 간의 상호 작용을 보여 줍니다.

> [!NOTE]
> 테이프 미디어가 비어 있거나 디스크 백업 파일이 없는 경우에는 이러한 모든 상호 작용에서 미디어 헤더를 기록한 다음 작업을 계속 진행합니다. 미디어가 비어 있지 않은데도 유효한 미디어 헤더가 없는 경우에는 이러한 작업에서 유효한 MTF 미디어가 아니라는 사실을 알린 후 백업 작업을 종료합니다.

|skip 옵션|NOINIT|INIT|
|------|------------|----------|
|NOSKIP|볼륨에 유효한 미디어 헤더가 포함되어 있으면 미디어 이름이 지정된 `MEDIANAME`과 일치하는지 확인합니다. 이름이 일치하면 기존 백업 세트를 모두 유지하면서 백업 세트를 추가합니다.<br /> 볼륨에 유효한 미디어 헤더가 포함되어 있지 않으면 오류가 발생합니다.|볼륨에 유효한 미디어 헤더가 포함되어 있으면 다음 검사를 수행합니다.<br /><ul><li>`MEDIANAME`이 지정되어 있으면 지정된 미디어 이름이 미디어 헤더의 미디어 이름과 일치하는지 확인합니다.<sup>1</sup></li><li>미디어에 만료되지 않은 백업 세트가 없는지 확인합니다. 만료되지 않은 백업 세트가 있으면 백업을 종료합니다.</li></ul><br />이러한 검사를 통과하면 미디어 헤더만 유지하며 미디어의 모든 백업 세트를 덮어씁니다.<br /> 볼륨에 유효한 미디어 헤더가 포함되어 있지 않으면 지정된 `MEDIANAME` 및 `MEDIADESCRIPTION`을 사용하여 미디어 헤더를 생성합니다.|
|SKIP|볼륨에 유효한 미디어 헤더가 포함되어 있으면 기존 백업 세트를 모두 유지하면서 백업 세트를 추가합니다.|볼륨에 유효한<sup>2</sup> 미디어 헤더가 포함되어 있으면 미디어 헤더만 유지하며 미디어의 모든 백업 세트를 덮어씁니다.<br /> 미디어가 비어 있으면 지정된 `MEDIANAME` 및 `MEDIADESCRIPTION`을 사용하여 미디어 헤더를 생성합니다.|

<sup>1</sup> 적절한 고정 데이터베이스 또는 서버 역할에 속하는 사용자만 백업 작업을 수행할 수 있습니다.

<sup>2</sup> 유효성에는 MTF 버전 번호와 기타 헤더 정보가 포함됩니다. 지정한 버전이 지원되지 않거나 예기치 못한 값일 경우 오류가 발생합니다.

## <a name="compatibility"></a>호환성

> [!CAUTION]
> 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 만든 백업은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복원할 수 없습니다.

BACKUP은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와의 호환성을 위해 `RESTART` 옵션을 지원합니다. 하지만 RESTART은 아무 효과가 없습니다.

## <a name="general-remarks"></a>일반적인 설명

데이터베이스와 트랜잭션 로그가 하나의 물리적 위치에 보관되도록 데이터베이스나 로그 백업을 디스크나 테이프 디바이스에 추가할 수 있습니다.

명시적 또는 암시적 트랜잭션에서는 BACKUP 문을 사용할 수 없습니다.

운영 체제가 데이터베이스의 데이터 정렬을 지원하는 한 프로세서 유형이 다르더라도 플랫폼 간 백업 작업을 수행할 수 있습니다.

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터, **65536(64KB)보다 큰** `MAXTRANSFERSIZE`를 설정 시 압축 알고리즘이 사용됩니다. 이 알고리즘은 먼저 페이지를 해독하고 압축한 다음 다시 암호화하는 [TDE(투명한 데이터 암호화)](../../relational-databases/security/encryption/transparent-data-encryption.md)로 암호화된 데이터베이스에 최적화되어 있습니다. `MAXTRANSFERSIZE`를 지정하지 않은 경우 또는 `MAXTRANSFERSIZE = 65536`(64KB)을 사용하는 경우 TDE 암호화 데이터베이스를 통해 백업 압축을 수행하면 암호화된 페이지가 바로 압축되어 압축률이 좋지 않을 수 있습니다. 자세한 내용은 [TDE 가능 데이터베이스의 백업 압축](https://blogs.msdn.microsoft.com/sqlcat/2016/06/20/sqlsweet16-episode-1-backup-compression-for-tde-enabled-databases/)을 참조하세요.

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CU5부터 더 이상 이 TDE를 사용하는 최적화된 압축 알고리즘을 사용하도록 `MAXTRANSFERSIZE`를 설정할 필요가 없습니다. 백업 명령에 `WITH COMPRESSION`이 지정되거나 *백업 압축 기본값* 서버 구성이 1로 설정되어 있으면 `MAXTRANSFERSIZE`가 자동으로 128K로 증가하여 최적화된 알고리즘을 사용하도록 설정합니다. 백업 명령에 `MAXTRANSFERSIZE`가 64K를 초과하는 값으로 지정되면 제공된 값이 적용됩니다. 즉, SQL Server는 자동으로 이 값을 줄이지 않고 늘리기만 합니다. `MAXTRANSFERSIZE = 65536`을 사용하여 TDE 암호화 데이터베이스를 백업해야 하는 경우 `WITH NO_COMPRESSION`를 지정하거나 *백업 압축 기본값* 서버 구성이 0으로 설정되어 있어야 합니다.

> [!NOTE]
> 기본값 `MAXTRANSFERSIZE`이 64K를 초과하는 경우가 있습니다.
>
> - 데이터베이스에서 여러 데이터 파일을 만든 경우 `MAXTRANSFERSIZE` > 64K를 사용합니다.
> - URL로 백업을 수행할 때 기본 `MAXTRANSFERSIZE = 1048576`(1MB)입니다.
>
> 이러한 조건 중 하나가 적용되는 경우에도 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CU5 이상이 아니면 최적화된 백업 압축 알고리즘을 가져오기 위해 백업 명령에서 `MAXTRANSFERSIZE` 64K를 초과하도록 명시적으로 설정해야 합니다.

기본적으로 백업 작업을 성공적으로 수행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 시스템 이벤트 로그에 항목이 추가됩니다. 로그를 자주 백업하는 경우 이러한 성공 메시지는 바로 누적되므로 엄청난 오류 로그가 쌓여 다른 메시지를 찾기 힘들 수 있습니다. 이 경우 스크립트가 이러한 로그 항목에 종속되지 않을 경우 추적 플래그 3226을 사용하여 이러한 항목을 표시하지 않을 수 있습니다. 자세한 내용은 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.

## <a name="interoperability"></a>상호 운용성

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 온라인 백업 프로세스를 사용하여 데이터베이스가 사용 중일 때도 데이터베이스 백업을 수행할 수 있습니다. 백업 시 대부분의 작업을 수행할 수 있습니다. 예를 들어 INSERT, UPDATE 또는 DELETE 문은 백업 작업 시에도 사용할 수 있습니다.

데이터베이스 또는 트랜잭션 로그 백업 시에 실행할 수 없는 작업은 다음과 같습니다.

- `ADD FILE` 또는 `REMOVE FILE` 옵션이 있는 `ALTER DATABASE`문과 같은 파일 관리 작업.

- 데이터베이스 축소 또는 파일 축소 작업. 자동 축소 작업도 포함됩니다.

백업 작업이 파일 관리 또는 축소 작업과 겹치면 충돌이 발생합니다. 충돌하는 작업 중 어떤 작업이 먼저 시작되었는지에 관계없이 두 번째 작업은 첫 번째 작업이 설정한 잠금 시간이 초과될 때까지 대기합니다. 제한 시간은 세션 제한 시간 설정에서 제어합니다. 제한 시간 동안에 잠금이 해제되면 두 번째 작업이 계속됩니다. 잠금 제한 시간이 초과되면 두 번째 작업이 실패합니다.

## <a name="metadata"></a>메타데이터

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 백업 작업을 추적하는 다음과 같은 백업 기록 테이블이 있습니다.

- [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)
- [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)
- [backupmediafamily](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)
- [backupmediaset](../../relational-databases/system-tables/backupmediaset-transact-sql.md)
- [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)

복원이 수행될 때 백업 세트가 **msdb** 데이터베이스에 아직 기록되어 있지 않으면 백업 기록 테이블을 수정할 수 있습니다.

## <a name="security"></a>보안

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 `PASSWORD` 및 `MEDIAPASSWORD` 옵션은 백업을 만드는 데 지원되지 않습니다. 암호로 만든 백업을 여전히 복원할 수 있습니다.

### <a name="permissions"></a>사용 권한

BACKUP DATABASE 및 BACKUP LOG 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.

백업 디바이스의 물리적 파일에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 디바이스를 읽고 쓸 수 있어야 하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 쓰기 권한이 있어야 합니다. 그러나 시스템 테이블의 백업 디바이스에 대한 항목을 추가하는 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)는 파일 액세스 권한을 확인하지 않습니다. 백업 디바이스의 물리적 파일에서 발생하는 이러한 문제는 백업 또는 복원을 시도할 때 실제 리소스를 액세스하기 전까지는 발생하지 않습니다.

## <a name="examples"></a><a name="examples"></a> 예

이 섹션에는 다음 예제가 포함되어 있습니다.

- A. [전체 데이터베이스 백업](#backing_up_db)
- B. [데이터베이스 및 로그 백업](#backing_up_db_and_log)
- C. [보조 파일 그룹의 전체 파일 백업 만들기](#full_file_backup)
- D. [보조 파일 그룹의 차등 파일 백업 만들기](#differential_file_backup)
- E. [미러된 단일 패밀리 미디어 세트 만들기 및 백업](#create_single_family_mirrored_media_set)
- F. [미러된 다중 패밀리 미디어 세트 만들기 및 백업](#create_multifamily_mirrored_media_set)
- G. [기존 미러된 미디어 세트에 백업](#existing_mirrored_media_set)
- H. [새 미디어 세트에 압축된 백업 만들기](#creating_compressed_backup_new_media_set)
- 9\. [Microsoft Azure Blob Storage 서비스에 백업](#url)
- J. [Backup 문의 진행률 추적](#backup_progress)

> [!NOTE]
> 백업 방법 도움말 항목에 추가적인 예가 포함되어 있습니다. 자세한 내용은 [백업 개요](../../relational-databases/backup-restore/backup-overview-sql-server.md)를 참조하세요.

### <a name="a-backing-up-a-complete-database"></a><a name="backing_up_db"></a> 1. 전체 데이터베이스 백업

다음 예에서는 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 데이터베이스를 디스크 파일에 백업합니다.

```sql
BACKUP DATABASE AdventureWorks2012
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'
    WITH FORMAT;
GO
```

### <a name="b-backing-up-the-database-and-log"></a><a name="backing_up_db_and_log"></a> 2. 데이터베이스 및 로그 백업

다음 예에서는 기본적으로 단순 복구 모델을 사용하는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스를 백업하고 로그 백업을 지원하기 위해 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 전체 복구 모델을 사용하도록 수정합니다.

그런 다음, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)를 사용하여 `AdvWorksData` 데이터를 백업하기 위한 논리적 [백업 디바이스](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 만들고 `AdvWorksLog` 로그를 백업하기 위한 다른 논리적 백업 디바이스를 만듭니다.

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
> 프로덕션 데이터베이스의 경우에는 로그를 정기적으로 백업하십시오. 로그 백업은 데이터 손실을 충분히 방지할 수 있을 만큼 자주 수행해야 합니다.

### <a name="c-creating-a-full-file-backup-of-the-secondary-filegroups"></a><a name="full_file_backup"></a> 3. 보조 파일 그룹의 전체 파일 백업 만들기

다음 예에서는 두 보조 파일 그룹에 있는 모든 파일의 전체 파일 백업을 만듭니다.

```sql
--Back up the files in SalesGroup1:
BACKUP DATABASE Sales
    FILEGROUP = 'SalesGroup1',
    FILEGROUP = 'SalesGroup2'
    TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck';
GO
```

### <a name="d-creating-a-differential-file-backup-of-the-secondary-filegroups"></a><a name="differential_file_backup"></a> 4. 보조 파일 그룹의 차등 파일 백업 만들기

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

### <a name="e-creating-and-backing-up-to-a-single-family-mirrored-media-set"></a><a name="create_single_family_mirrored_media_set"></a> 5. 미러된 단일 패밀리 미디어 세트 만들기 및 백업

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

### <a name="f-creating-and-backing-up-to-a-multifamily-mirrored-media-set"></a><a name="create_multifamily_mirrored_media_set"></a> 6. 미러된 다중 패밀리 미디어 세트 만들기 및 백업

다음 예에서는 각 미러가 두 개의 미디어 패밀리로 구성되는 미러된 미디어 세트를 만듭니다. 그런 다음 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 데이터베이스를 두 미러에 백업합니다.

```sql
BACKUP DATABASE AdventureWorks2012
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'
WITH
    FORMAT,
    MEDIANAME = 'AdventureWorksSet1';
```

### <a name="g-backing-up-to-an-existing-mirrored-media-set"></a><a name="existing_mirrored_media_set"></a> G. 기존 미러된 미디어 세트에 백업

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
> 기본값인 NOINIT는 쉽게 구분할 수 있도록 여기에 표시됩니다.

### <a name="h-creating-a-compressed-backup-in-a-new-media-set"></a><a name="creating_compressed_backup_new_media_set"></a> H. 새 미디어 세트에 압축된 백업 만들기

다음 예에서는 미디어를 포맷하여 새 미디어 세트를 만들고 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 데이터베이스에 대해 압축된 전체 백업을 수행합니다.

```sql
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'
WITH
    FORMAT,
    COMPRESSION;
```

### <a name="i-backing-up-to-the-microsoft-azure-blob-storage-service"></a><a name="url"></a> I. Microsoft Azure Blob Storage 서비스에 백업

이 예에서는 Microsoft Azure Blob Storage 서비스에 `Sales`의 전체 데이터베이스 백업을 수행합니다. 스토리지 계정 이름은 `mystorageaccount`입니다. 컨테이너는 `myfirstcontainer`입니다. 읽기, 쓰기, 삭제 및 나열 권한이 있는 저장된 액세스 정책을 만들었습니다. 저장된 액세스 정책에 연결된 공유 액세스 서명을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명인 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`를 만들었습니다. Microsoft Azure Blob Storage 서비스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업의 자세한 내용은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) 및 [URL에 대한 SQL Server 백업](../../relational-databases/backup-restore/sql-server-backup-to-url.md)을 참조하세요.

```sql
BACKUP DATABASE Sales
TO URL = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_20160726.bak'
WITH STATS = 5;
```

### <a name="j-track-the-progress-of-backup-statement"></a><a name="backup_progress"></a> J. Backup 문의 진행률 추적

다음 쿼리는 현재 실행 중인 backup 문에 대한 정보를 반환합니다.
```sql
SELECT query = a.text, start_time, percent_complete,
    eta = dateadd(second,estimated_completion_time/1000, getdate())
FROM sys.dm_exec_requests r
    CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) a
WHERE r.command LIKE 'BACKUP%'
```

## <a name="see-also"></a>참고 항목

- [백업 디바이스](../../relational-databases/backup-restore/backup-devices-sql-server.md)
- [미디어 세트, 미디어 패밀리 및 백업 세트](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)
- [비상 로그 백업](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)
- [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)
- [DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)
- [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)
- [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)
- [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)
- [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)
- [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)
- [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sp_helpfile](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)
- [sp_helpfilegroup](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)
- [서버 구성 옵션](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [메모리 액세스에 최적화된 테이블이 있는 데이터베이스의 증분 복원](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](backup-transact-sql.md?view=sql-server-2016)
    :::column-end:::
    :::column:::
        **_\* SQL Database<br />Managed Instance \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](backup-transact-sql.md?view=aps-pdw-2016)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-sql-managed-instance"></a>Azure SQL Managed Instance

Azure SQL Managed Instance에 배치/호스트되는 SQL 데이터베이스를 백업합니다. SQL [Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에는 자동 백업이 있으며, 사용자가 전체 데이터베이스 `COPY_ONLY` 백업을 만들 수 있습니다. 차등, 로그 및 파일 스냅샷 백업은 지원되지 않습니다.

## <a name="syntax"></a>구문

```syntaxsql
BACKUP DATABASE { database_name | @database_name_var }
  TO URL = { 'physical_device_name' | @physical_device_name_var }[ ,...n ]
  WITH COPY_ONLY [, { <general_WITH_options> } ]
[;]

<general_WITH_options> [ ,...n ]::=

--Media Set Options
   MEDIADESCRIPTION = { 'text' | @text_variable }
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

--Encryption Options
 ENCRYPTION (ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY } , encryptor_options ) <encryptor_options> ::=
   SERVER CERTIFICATE = Encryptor_Name | SERVER ASYMMETRIC KEY = Encryptor_Name
```

## <a name="arguments"></a>인수

DATABASE 전체 데이터베이스 백업을 지정합니다. 데이터베이스 백업 중에 Azure SQL Managed Instance는 백업을 복원할 때 일관성 있는 데이터베이스를 생성하기 위해 충분한 트랜잭션 로그를 백업합니다.

> [!IMPORTANT]
> Azure SQL Managed Instance에서 생성된 데이터베이스 백업은 다른 관리되는 인스턴스에서만 복원할 수 있습니다. SQL Server 온-프레미스 인스턴스로 복원할 수 없습니다(SQL Server 2016 데이터베이스의 백업을 SQL Server 2012 인스턴스로 복원할 수 없는 방식과 비슷함).

BACKUP DATABASE(데이터베이스 백업)로 만든 백업을 복원하면 전체 백업이 복원됩니다. SQL Managed Instance 자동 백업에서 복원하려면 [관리되는 인스턴스로 데이터베이스 복원](/azure/sql-database/sql-database-managed-instance-get-started-restore)을 참조하세요.

{ *database_name* |  **@** _database\_name\_var_ } 전체 데이터베이스를 백업하는 데이터베이스입니다. 변수( **@** _database\_name\_var_)로 제공된 경우, 이 이름은 문자열 상수( **@** _database\_name\_var_ **=** _database name_)나 **ntext** 또는 **text** 데이터 형식을 제외한 문자열 데이터 형식의 변수로 지정할 수 있습니다.

자세한 내용은 [전체 파일 백업](../../relational-databases/backup-restore/full-file-backups-sql-server.md) 및 [파일 및 파일 그룹 백업](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)을 참조하세요.

TO URL

백업 작업에 사용할 URL을 지정합니다. URL 형식은 Microsoft Azure Storage 서비스에 대한 백업을 만드는 데 사용됩니다.

> [!IMPORTANT]
> URL로 백업할 때 여러 디바이스에 백업하려면 SAS(공유 액세스 서명) 토큰을 사용해야 합니다. 공유 액세스 서명 만들기에 대한 자세한 내용은 [URL에 대한 SQL Server 백업](../../relational-databases/backup-restore/sql-server-backup-to-url.md) 및 [Powershell로 Azure Storage의 SAS(공유 액세스 서명) 토큰이 있는 SQL 자격 증명 만들기 간소화](https://docs.microsoft.com/archive/blogs/sqlcat/simplifying-creation-of-sql-credentials-with-shared-access-signature-sas-tokens-on-azure-storage-with-powershell)를 참조하세요.

*n* 쉼표로 구분된 목록에 백업 디바이스를 최대 64개까지 지정할 수 있음을 나타내는 자리 표시자입니다.

### <a name="with-optionsspecifies-options-to-be-used-with-a-backup-operation"></a>WITH 백업 작업에 사용할 옵션을 지정합니다.

CREDENTIAL Microsoft Azure Blob Storage 서비스에 대한 백업을 만들 때에만 사용됩니다.

ENCRYPTION 백업에 대한 암호화를 지정하는 데 사용됩니다. 백업을 암호화하는 데 사용할 암호화 알고리즘을 지정하거나 백업이 암호화되지 않도록 하려면 `NO_ENCRYPTION`을 지정할 수 있습니다. 암호화는 백업 파일을 보호하는 데 권장되는 방법입니다. 지정할 수 있는 알고리즘의 목록은 다음과 같습니다.

- `AES_128`
- `AES_192`
- `AES_256`
- `TRIPLE_DES_3KEY`
- `NO_ENCRYPTION`

암호화하도록 선택하는 경우 암호기 옵션을 사용하여 암호기도 지정해야 합니다.

- `SERVER CERTIFICATE = <Encryptor_Name>`
- `SERVER ASYMMETRIC KEY = <Encryptor_Name>`

**백업 세트 옵션**

COPY_ONLY 백업이 정상적인 백업 시퀀스에 영향을 주지 않는 복사 전용 백업(*copy-only backup*)임을 지정합니다. 복사 전용 백업은 Azure SQL Database 자동 백업과 독립적으로 만들어집니다. 자세한 내용은 [복사 전용 백업](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)을 참조하세요.

{ COMPRESSION | NO_COMPRESSION } 이 백업에서 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)을 수행할지 여부를 지정하여 서버 수준 기본값을 재정의합니다.

백업 압축은 기본 동작이 아닙니다. 하지만 이 기본값은 [백업 압축 기본값](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) 서버 구성 옵션을 설정하여 변경할 수 있습니다. 이 옵션의 현재 값을 보는 방법은 [서버 속성 보기 또는 변경](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)을 참조하세요.

COMPRESSION 백업 압축을 명시적으로 사용하도록 설정합니다.

NO_COMPRESSION 백업 압축을 명시적으로 사용하지 않도록 설정합니다.

DESCRIPTION **=** { **'** _text_ **'**  |  **@** _text\_variable_ } 백업 세트를 설명하는 자유 형식의 텍스트를 지정합니다. 문자열을 최대 255자까지 지정할 수 있습니다.

NAME **=** { *backup_set_name* |  **@** _backup\_set\_var_ } 백업 세트의 이름을 지정합니다. 이름은 최대 128자까지 지정할 수 있습니다. NAME을 지정하지 않으면 공백이 됩니다.

MEDIADESCRIPTION **=** { *text* | **@** _text\_variable_ } 미디어 세트에 대한 자유 형식의 텍스트 설명을 최대 255자까지 지정합니다.

MEDIANAME **=** { *media_name* |  **@** _media\_name\_variable_ } 전체 백업 미디어 세트에 대한 미디어 이름을 지정합니다. 미디어 이름은 128자 이하여야 합니다. `MEDIANAME`을 지정하면 백업 볼륨에 이미 있는 이전에 지정한 미디어 이름과 일치해야 합니다. 지정하지 않거나 SKIP 옵션을 지정하면 미디어 이름에 대한 확인을 수행하지 않습니다.

BLOCKSIZE **=** { *blocksize* |  **@** _blocksize\_variable_ } 물리적 블록 크기(바이트)를 지정합니다. 지원되는 크기는 512, 1024, 2048, 4096, 8192, 16384, 32768 및 65536(64KB) 바이트입니다. 테이프 디바이스의 기본값은 65536이고 그렇지 않은 경우에는 512입니다. 일반적으로 BACKUP에서 디바이스에 적합한 블록 크기를 자동으로 선택하기 때문에 이 옵션은 필요하지 않습니다. 명시적으로 지정된 블록 크기는 자동 선택된 블록 크기보다 우선 적용됩니다.

**데이터 전송 옵션**

BUFFERCOUNT **=** { *buffercount* |  **@** _buffercount\_variable_ } 백업 작업에 사용되는 I/O 버퍼의 총 수를 지정합니다. 임의의 양의 정수를 지정할 수 있지만 버퍼 수가 많으면 Sqlservr.exe 프로세스의 부적절한 가상 주소 공간으로 인해 "메모리가 부족합니다"라는 오류가 발생할 수 있습니다.

버퍼에 사용되는 총 공간은 다음 식으로 결정됩니다. `BUFFERCOUNT * MAXTRANSFERSIZE`.

> [!NOTE]
> `BUFFERCOUNT` 옵션을 사용하는 방법은 [잘못된 BufferCount 데이터 전송 옵션을 사용하면 OOM 상태가 발생할 수 있음](https://docs.microsoft.com/archive/blogs/sqlserverfaq/incorrect-buffercount-data-transfer-option-can-lead-to-oom-condition) 블로그를 참조하세요.

MAXTRANSFERSIZE **=** { *maxtransfersize* | _**@** maxtransfersize\_variable_ } [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 백업 미디어 간에 사용되는 가장 큰 전송 단위(바이트)를 지정합니다. 가능한 값은 최대 4194304바이트(4MB)까지 65536바이트(64KB)의 배수입니다.

> [!NOTE]
> 단일 데이터 파일이 있는 [TDE(투명한 데이터 암호화)](../../relational-databases/security/encryption/transparent-data-encryption.md) 가능 데이터베이스의 경우 기본 `MAXTRANSFERSIZE`는 65536(64 KB)입니다. 비-TDE 암호화된 데이터베이스의 경우 디스크 백업을 사용할 때 기본 `MAXTRANSFERSIZE`는 1048576(1MB)이고 VDI 또는 TAPE를 사용하는 경우에는 65536(64KB)입니다.

**오류 관리 옵션**

이러한 옵션을 사용하면 백업 작업에 대해 백업 체크섬을 설정할 수 있는지 여부와 오류 발생 시 해당 작업을 중지할지 여부를 결정할 수 있습니다.

{ **NO_CHECKSUM** | CHECKSUM } 백업 체크섬의 설정 여부를 제어합니다.

NO_CHECKSUM 백업 체크섬 생성 및 페이지 체크섬의 유효성 검사를 명시적으로 사용하지 않도록 설정합니다. 기본 동작입니다.

CHECKSUM 백업 작업이 각 페이지의 체크섬과 조각난 페이지를 확인하고 사용 가능할 경우 전체 백업에 대해 체크섬을 생성하도록 지정합니다.

백업 체크섬을 사용하면 작업 및 백업 처리량에 영향을 줄 수 있습니다.

자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.

{ **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR } 페이지 체크섬 오류가 발생한 후 백업 작업을 중지할지, 아니면 계속할지를 제어합니다.

STOP_ON_ERROR 페이지 체크섬에서 확인하지 않을 경우 BACKUP이 실패하도록 지정합니다. 기본 동작입니다.

CONTINUE_AFTER_ERROR 잘못된 체크섬이나 조각난 페이지 등의 오류가 발생하더라도 BACKUP을 계속하도록 지시합니다.

데이터베이스가 손상된 경우 NO_TRUNCATE 옵션을 사용하여 비상 로그 백업을 수행할 수 없으면 NO_TRUNCATE 대신 CONTINUE_AFTER_ERROR를 지정하여 [비상 로그 백업](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 수행할 수 있습니다.

자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.

**호환성 옵션**

RESTART 아무 효과가 없습니다. 이 옵션은 이전 버전의 SQL Server와의 호환성을 위해 사용됩니다.

**모니터링 옵션**

STATS [ **=** _percentage_ ] 새로 *percentage*가 완료될 때마다 메시지를 표시하여 진행 상태를 측정하는 데 사용됩니다. *percentage*를 생략하면 10%가 완료될 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 메시지를 표시합니다.

STATS 옵션은 다음 간격을 보고할 임계값에 도달한 시점까지의 완료 백분율을 보고합니다. 간격은 지정된 비율을 대략적으로 나타냅니다. 예를 들어 STATS=10인 경우 완료된 크기가 40%이면 옵션은 43%를 표시할 수 있습니다. 대용량 백업 세트의 경우 완료 백분율이 완료된 I/O 호출 간에 매우 느리게 진행되므로 문제가 되지 않습니다.

## <a name="limitations-for-sql-managed-instance"></a>SQL Managed Instance 제한 사항

최대 백업 스트라이프 크기는 195GB(최대 blob 크기)입니다. 개별 스트라이프 크기를 줄이고 이 제한 내로 유지하려면 백업 명령에서 스트라이프 수를 늘립니다.

## <a name="security"></a>보안

### <a name="permissions"></a>사용 권한

BACKUP DATABASE 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.

URL에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 디바이스를 읽고 쓸 수 있어야 하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 쓰기 권한이 있어야 합니다.

## <a name="examples"></a><a name="examples"></a> 예

이 예제에서는 Microsoft Azure Blob Storage 서비스에 `Sales`의 COPY_ONLY 백업을 수행합니다. 스토리지 계정 이름은 `mystorageaccount`입니다. 컨테이너는 `myfirstcontainer`입니다. 읽기, 쓰기, 삭제 및 나열 권한이 있는 저장된 액세스 정책을 만들었습니다. 저장된 액세스 정책에 연결된 공유 액세스 서명을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명인 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`를 만들었습니다. Microsoft Azure Blob Storage 서비스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업의 자세한 내용은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) 및 [URL에 대한 SQL Server 백업](../../relational-databases/backup-restore/sql-server-backup-to-url.md)을 참조하세요.

```sql
BACKUP DATABASE Sales
TO URL = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_20160726.bak'
WITH STATS = 5, COPY_ONLY;
```

## <a name="see-also"></a>참고 항목

[데이터베이스 복원](restore-statements-transact-sql.md)

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](backup-transact-sql.md?view=sql-server-2016)
    :::column-end:::
    :::column:::
        [SQL Database<br />Managed Instance](backup-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Analytics<br />Platform System(PDW) \*_** &nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="analytics-platform-system"></a>분석 플랫폼 시스템

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스의 백업을 만들고 사용자 지정 네트워크 위치에 어플라이언스의 백업을 저장합니다. 재해 복구를 하거나 하나의 어플라이언스에서 다른 어플라이언스로 데이터베이스를 복사하려면 [RESTORE DATABASE - Analytics Platform System](../../t-sql/statements/restore-statements-transact-sql.md)과 함께 이 문을 사용합니다.

**시작하기 전에**, [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 "백업 서버 확보 및 구성"을 참조하세요.

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에는 두 가지 백업 유형이 있습니다. *전체 데이터베이스 백업*은 전체 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스의 백업입니다. *차등 데이터베이스 백업*에는 마지막 전체 백업 이후의 변경 내용만 포함됩니다. 사용자 데이터베이스 백업에는 데이터베이스 사용자 및 데이터베이스 역할이 포함됩니다. master 데이터베이스 백업에는 로그인 정보가 포함됩니다.

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스 백업에 대한 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에 있는 “백업 및 복원”을 참조하세요.

## <a name="syntax"></a>구문

```syntaxsql
--Create a full backup of a user database or the master database.
BACKUP DATABASE database_name
    TO DISK = '\\UNC_path\backup_directory'
    [ WITH [ ( ]<with_options> [ ,...n ][ ) ] ]
[;]

--Create a differential backup of a user database.
BACKUP DATABASE database_name
    TO DISK = '\\UNC_path\backup_directory'
    WITH [ ( ] DIFFERENTIAL
    [ , <with_options> [ ,...n ] [ ) ]
[;]

<with_options> ::=
    DESCRIPTION = 'text'
    | NAME = 'backup_name'
```

## <a name="arguments"></a>인수

*database_name* 백업을 만들 데이터베이스의 이름입니다. 데이터베이스는 master 데이터베이스 또는 사용자 데이터베이스가 될 수 있습니다.

TO DISK = '\\\\*UNC_path*\\*backup_directory*' [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]가 백업 파일을 작성할 네트워크 경로 및 디렉터리입니다. 예: '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.

- 백업 디렉터리 이름에 대한 경로가 이미 존재해야 하며 정규화된 UNC(범용 명명 규칙) 경로로 지정해야합니다.
- 백업 명령을 실행하기 전에는 백업 디렉토리 *backup_directory*가 없어야 합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 백업 디렉토리를 만듭니다.
- 백업 디렉터리 경로는 로컬 경로일 수 없으며 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 어플라이언스 노드의 위치일 수 없습니다.
- UNC 경로 및 백업 디렉터리 이름의 최대 길이는 200자입니다.
- 서버 또는 호스트는 IP 주소로 지정해야 합니다. 그것을 호스트 또는 서버 이름으로 지정할 수 없습니다.

DESCRIPTION = **'** _text_ **'** 백업에 대한 텍스트 설명을 지정합니다. 최대 텍스트 길이는 255자입니다.

설명은 메타데이터에 저장되며, 백업 헤더가 RESTORE HEADERONLY를 사용하여 복원될 때 표시됩니다.

NAME = **'** _backup \_name_ **'** 백업의 이름을 지정합니다. 백업 이름은 데이터베이스 이름과 다를 수 있습니다.

- 이름은 최대 128자까지 지정할 수 있습니다.
- 경로를 포함할 수 없습니다.
- 문자, 숫자 또는 밑줄(_)로 시작해야 합니다. 허용되는 특수 문자는 밑줄(\_), 하이픈(-) 또는 공백( )입니다. 백업 이름은 공백 문자로 끝날 수 없습니다.
- *backup_name*이 지정된 위치에 이미 존재하면 문은 실패합니다.

이 이름은 메타데이터에 저장되며, 백업 헤더가 RESTORE HEADERONLY를 사용하여 복원될 때 표시됩니다.

DIFFERENTIAL 사용자 데이터베이스의 차등 백업을 수행하도록 지정합니다. 생략할 경우 기본값은 전체 데이터베이스 백업입니다. 차등 백업의 이름이 전체 백업의 이름과 일치할 필요는 없습니다. 차등 및 해당하는 전체 백업을 추적하려면 동일한 이름에 'full' 또는 'diff'를 추가하여 사용하는 것이 좋습니다.

예를 들면 다음과 같습니다.

`BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`

`BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`

## <a name="permissions"></a>사용 권한

**db_backupoperator** 고정 데이터베이스 역할에서 **BACKUP DATABASE** 권한 또는 멤버 자격이 필요합니다. master 데이터베이스는 백업할 수 없지만 **db_backupoperator** 고정 데이터베이스 역할에 추가된 일반 사용자의 경우 할 수 있습니다. master 데이터베이스는 **sa**, 패브릭 관리자 또는 **sysadmin** 고정 서버 역할을 하는 멤버만이 백업할 수 있습니다.

백업 디렉토리에 액세스하고, 만들고, 쓸 수 있는 권한이 있는 Windows 계정이 필요합니다. 또한 Windows 계정 이름 및 암호를 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 저장해야 합니다. 해당 네트워크 자격 증명을 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 추가하려면 [sp_pdw_add_network_credentials - [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 저장 프로시저를 사용합니다.

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서의 자격 증명 관리에 대한 자세한 내용은 [보안](#Security) 섹션을 참조하세요.

## <a name="error-handling"></a>오류 처리

다음 조건에서 BACKUP DATABASE 오류가 발생합니다.

- 사용자 권한은 백업을 수행하기에 충분하지 않습니다.
- [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 백업이 저장될 네트워크 위치에 대한 올바른 사용 권한이 없습니다.
- 데이터베이스가 없습니다.
- 대상 디렉터리가 네트워크 공유에 이미 있습니다.
- 대상 네트워크 공유를 사용할 수 없습니다.
- 대상 네트워크 공유에 백업을 위한 충분한 공간이 없습니다. BACKUP DATABASE 명령은 백업을 시작하기에 앞서 디스크 공간이 충분한지 확인하지 않으므로 BACKUP DATABASE를 실행하는 동안 디스크 공간 부족 오류가 일어날 수 있습니다. 디스크 공간이 부족하면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 BACKUP DATABASE 명령을 롤백합니다. 데이터베이스 크기를 줄이려면 [DBCC SHRINKLOG([!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)])](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)를 실행합니다.
- 트랜잭션 내에서 백업을 시작하려고 시도합니다.

::: moniker-end
::: moniker range=">=aps-pdw-2016||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"
## <a name="general-remarks"></a>일반적인 주의 사항

데이터베이스 백업을 수행하기 전에 [DBCC SHRINKLOG([!INCLUDE[ssPDW](../../includes/sspdw-md.md)])](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)를 사용하여 데이터베이스 크기를 줄입니다. 

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 백업은 동일한 디렉토리에 여러 파일의 집합으로 저장됩니다.

차등 백업은 일반적으로 전체 백업보다 시간이 적게 들며 더 자주 수행할 수 있습니다. 여러 차등 백업이 동일한 전체 백업을 기반으로 하는 경우 각 차등 백업에는 이전 차등 백업의 모든 변경 사항이 포함됩니다.

BACKUP 명령을 취소하면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 대상 디렉토리 및 백업을 위해 생성된 모든 파일을 제거합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]의 공유에 대한 네트워크 연결이 끊어지면 롤백을 완료할 수 없습니다.

전체 백업과 차등 백업은 서로 다른 디렉토리에 저장됩니다. 전체 백업과 차등 백업이 서로 관련 있음을 나타내기 위한 명명 규칙이 강제되지 않습니다. 자신 만의 명명 규칙을 통해 이 관련성을 추적할 수 있습니다. 또는 WITH DESCRIPTION 옵션을 사용하여 설명을 추가한 다음, RESTORE HEADERONLY 문을 사용하여 설명을 검색할 수 있습니다.

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"
## <a name="limitations-and-restrictions"></a>제한 사항

master 데이터베이스의 차등 백업을 수행할 수 없습니다. master 데이터베이스의 전체 백업 만 지원됩니다.

백업 파일은 [RESTORE DATABASE - Analytics Platform System](../../t-sql/statements/restore-statements-transact-sql.md) 문을 사용하여 백업을 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 어플라이언스에 복원하는 데 적합한 형식으로만 저장됩니다.

BACKUP DATABASE 문을 사용한 백업은 데이터 또는 사용자 정보를 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스로 전송하는 데 사용할 수 없습니다. 그 기능을 위해서는 원격 테이블 복사 기능을 사용할 수 있습니다. 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 "원격 테이블 복사"를 참조하세요.

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 기술을 사용하여 데이터베이스를 백업하고 복원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 옵션은 백업 압축을 사용하도록 미리 구성됩니다. 압축, 체크섬, 블록 크기 및 버퍼 개수 등의 백업 옵션을 설정할 수 없습니다.

주어진 시간에 어플라이언스에서 오직 하나의 데이터베이스 백업 또는 복원만을 실행할 수 있습니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 현재 백업 또는 복원 명령이 완료될 때까지 백업 또는 복원 명령을 대기열에 넣습니다.

백업을 복원하기 위한 대상 어플라이언스에는 적어도 원본 어플라이언스와 같은 정도의 컴퓨팅 노드가 있어야 합니다. 대상이 원본 어플라이언스보다 컴퓨팅 노드를 많이 가질 수는 있으나 적게 가질 수는 없습니다.

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 백업이 어플라이언스에 저장되므로 백업의 위치와 이름을 추적하지 않습니다.

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 데이터베이스 백업의 성공 또는 실패를 추적합니다.

차등 백업은 마지막 전체 백업이 성공적으로 완료된 경우에만 허용됩니다. 예를 들어 월요일에 판매 데이터베이스의 전체 백업을 만들었고 백업이 성공적으로 완료되었다고 가정합니다. 그런 다음, 화요일에 판매 데이터베이스의 전체 백업을 다시 만들고 실패합니다. 이 실패 후에는 월요일의 전체 백업을 기반으로 차등 백업을 만들 수 없습니다. 차등 백업을 만들기 전에 먼저 성공적인 전체 백업을 만들어야합니다.

## <a name="metadata"></a>메타데이터

이러한 동적 관리 뷰에는 모든 백업, 복원 및 로드 작업에 대한 정보가 들어 있습니다. 이 정보는 시스템을 다시 시작해도 유지됩니다.

- [sys.pdw_loader_backup_runs](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)
- [sys.pdw_loader_backup_run_details](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)
- [sys.pdw_loader_run_stages](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)

## <a name="performance"></a>성능

백업을 수행하려면, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 먼저 메타데이터를 백업한 다음, 컴퓨팅 노드에 저장된 데이터베이스 데이터의 병렬 백업을 수행합니다. 데이터는 각 컴퓨팅 노드에서 백업 디렉토리로 직접 복사됩니다. 최상의 성능으로 데이터를 컴퓨팅 노드에서 백업 디렉토리로 옮기기 위해 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 동시에 데이터를 복사하는 컴퓨팅 노드의 수를 조정합니다.

## <a name="locking"></a>잠금

DATABASE 개체에서 ExclusiveUpdate 잠금을 얻습니다.

## <a name="security"></a><a name="Security"></a> 보안

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 백업은 어플라이언스에 저장되지 않습니다. 따라서 IT 팀은 백업 보안의 모든 측면을 관리하는 일을 담당합니다. 예를 들어, 여기에는 백업 데이터의 보안, 백업을 저장하는데 사용되는 서버의 보안 및 백업 서버를 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 기기에 연결하는 네트워킹 인프라의 보안 관리가 포함됩니다.

**네트워크 자격 증명 관리**

백업 디렉터리에 대한 네트워크 액세스는 표준 운영 체제 파일 공유 보안을 기반으로 합니다. 백업을 수행하기 전에 백업 디렉토리에 대해 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]을 인증하는 데 사용할 Windows 계정을 만들거나 지정해야 합니다. 이 Windows 계정에는 백업 디렉토리에 액세스, 작성 및 쓰기할 수 있는 권한이 있어야 합니다.

> [!IMPORTANT]
> 데이터의 보안 위험을 줄이려면 Windows 계정 하나를 전적으로 백업 및 복원 작업을 수행할 목적으로 지정하는 것이 좋습니다. 이 계정에 전적으로 백업 위치에 대해서만 권한을 갖도록 허용합니다.

[sp_pdw_add_network_credentials - [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 저장 프로시저를 실행하여 사용자 이름과 암호를 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 저장해야 합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 Windows Credential Manager를 사용하여 사용자 이름과 암호를 제어 노드와 컴퓨팅 노드에 저장하고 암호화합니다. 자격 증명은 BACKUP DATABASE 명령으로 백업되지 않습니다.

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 네트워크 자격 증명을 제거하려면 [sp_pdw_remove_network_credentials - [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)를 참조하세요.

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 저장된 모든 네트워크 자격 증명을 나열하려면 [sys.dm_pdw_network_credentials](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) 동적 관리 뷰를 사용합니다.

## <a name="examples"></a>예제

### <a name="a-add-network-credentials-for-the-backup-location"></a>A. 백업 위치에 대한 네트워크 자격 증명 추가

백업을 만들려면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에게 백업 디렉토리에 대한 읽기/쓰기 권한이 있어야 합니다. 다음 예제에서는 사용자에 대한 자격 증명을 추가하는 방법을 보여 줍니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 이러한 자격 증명을 저장하고 백업 및 복원 작업에 그것을 사용합니다.

> [!IMPORTANT]
> 보안상의 이유로 하나의 도메인 계정을 전적으로 백업을 수행할 목적으로 만드는 것이 좋습니다.

```sql
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';
```

### <a name="b-remove-network-credentials-for-the-backup-location"></a>B. 백업 위치에 대한 네트워크 자격 증명 제거

다음 예에서는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 도메인 사용자의 자격 증명을 제거하는 방법을 보여줍니다.

```sql
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';
```

### <a name="c-create-a-full-backup-of-a-user-database"></a>C. 사용자 데이터베이스의 전체 백업 만들기

다음 예에서는 송장 사용자 데이터베이스의 전체 백업을 만듭니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 Invoices2013 디렉토리를 만들고 백업 파일을 \\\10.192.63.147\backups\yearly\Invoices2013Full 디렉토리에 저장합니다.

```sql
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';
```

### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. 사용자 데이터베이스의 전체 백업 만들기

다음 예에서는 송장 데이터베이스의 마지막 전체 백업 이후에 발생한 모든 변경 내용을 포함하는 차등 백업을 만듭니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 파일을 저장할 \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff 디렉토리를 만듭니다. '송장 2013 차등 백업' 설명이 백업에 대한 헤더 정보와 함께 저장됩니다.

차등 백업은 송장의 마지막 전체 백업이 성공적으로 완료된 경우에만 성공적으로 실행됩니다.

```sql
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'
    WITH DIFFERENTIAL,
    DESCRIPTION = 'Invoices 2013 differential backup';
```

### <a name="e-create-a-full-backup-of-the-master-database"></a>E. master 데이터베이스의 전체 백업 만들기

다음 예제에서는 master 데이터베이스의 전체 백업을 만들고 '\\\10.192.63.147\backups\2013\daily\20130722\master' 디렉터리에 저장합니다.

```sql
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';
```

### <a name="f-create-a-backup-of-appliance-login-information"></a>F. 어플라이언스 로그인 정보의 백업 만들기

마스터 데이터베이스는 어플라이언스 로그인 정보를 저장합니다. 어플라이언스 로그인 정보를 백업하려면 master를 백업해야 합니다.

다음 예에서는 마스터 데이터베이스의 백업을 만듭니다.

```sql
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'
WITH (
    DESCRIPTION = 'Master Backup 20130722',
    NAME = 'login-backup'
)
;
```

## <a name="see-also"></a>참고 항목

[RESTORE DATABASE -병렬 데이터 웨어하우스](../../t-sql/statements/restore-statements-transact-sql.md)

::: moniker-end
