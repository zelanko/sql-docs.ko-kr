---
title: ALTER DATABASE 파일 및 파일 그룹
description: Transact-SQL을 사용하여 데이터베이스의 파일 및 파일 그룹을 업데이트합니다.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ADD FILE
- ADD_FILE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting files
- removing files
- deleting filegroups
- file modifications [SQL Server]
- databases [SQL Server], size
- relocating files
- databases [SQL Server], modifying
- file additions [SQL Server], ALTER DATABASE
- file moving [SQL Server]
- default filegroups
- ALTER DATABASE statement, files and filegroups
- initializing files [SQL Server]
- database files [SQL Server]
- moving files
- filegroups [SQL Server], deleting
- adding filegroups
- adding files
- database filegroups [SQL Server]
- adding log files
- modifying files
- filegroups [SQL Server], adding
- file initialization [SQL Server]
- files [SQL Server], deleting
- files [SQL Server], adding
- databases [SQL Server], moving
ms.assetid: 1f635762-f7aa-4241-9b7a-b51b22292b07
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 9fa653040cdbd1ac08225e04203eeae6ecd344d5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541429"
---
# <a name="alter-database-transact-sql-file-and-filegroup-options"></a>ALTER DATABASE(Transact-SQL) 파일 및 파일 그룹 옵션

데이터베이스와 연결된 파일 및 파일 그룹을 수정합니다. 데이터베이스의 파일과 파일 그룹을 추가 또는 제거하고 데이터베이스 또는 해당 파일과 파일 그룹의 특성을 변경합니다. 다른 ALTER DATABASE 옵션은 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.

구문 표기 규칙에 대한 자세한 내용은 [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)을 참조하십시오.

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [SQL Database<br />Managed Instance](alter-database-transact-sql-file-and-filegroup-options.md?view=azuresqldb-mi-current)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="syntax"></a>구문

```syntaxsql
ALTER DATABASE database_name
{
    <add_or_modify_files>
  | <add_or_modify_filegroups>
}

<add_or_modify_files>::=
{
    ADD FILE <filespec> [ ,...n ]
        [ TO FILEGROUP { filegroup_name } ]
  | ADD LOG FILE <filespec> [ ,...n ]
  | REMOVE FILE logical_file_name
  | MODIFY FILE <filespec>
}

<filespec>::=
(
    NAME = logical_file_name
    [ , NEWNAME = new_logical_name ]
    [ , FILENAME = {'os_file_name' | 'filestream_path' | 'memory_optimized_data_path' } ]
    [ , SIZE = size [ KB | MB | GB | TB ] ]
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB| % ] ]
    [ , OFFLINE ]
)

<add_or_modify_filegroups>::=
{
    | ADD FILEGROUP filegroup_name
        [ CONTAINS FILESTREAM | CONTAINS MEMORY_OPTIMIZED_DATA ]
    | REMOVE FILEGROUP filegroup_name
    | MODIFY FILEGROUP filegroup_name
        { <filegroup_updatability_option>
        | DEFAULT
        | NAME = new_filegroup_name
        | { AUTOGROW_SINGLE_FILE | AUTOGROW_ALL_FILES }
        }
}
<filegroup_updatability_option>::=
{
    { READONLY | READWRITE }
    | { READ_ONLY | READ_WRITE }
}

```

## <a name="arguments"></a>인수

**\<add_or_modify_files>::=**

추가, 제거 또는 수정할 파일을 지정합니다.

*database_name* 수정할 데이터베이스의 이름입니다.

ADD FILE 데이터베이스에 파일을 추가합니다.

TO FILEGROUP { *filegroup_name* } 지정된 파일을 추가할 파일 그룹을 지정합니다. 현재 파일 그룹을 표시하고 어떤 파일 그룹이 현재 기본 파일 그룹인지 표시하려면 [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) 카탈로그 뷰를 사용하십시오.

ADD LOG FILE 지정된 데이터베이스에 로그 파일을 추가합니다.

REMOVE FILE *logical_file_name*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 논리적 파일 설명을 제거하고 물리적 파일을 삭제합니다. 파일이 비어 있어야 제거할 수 있습니다.

*logical_file_name* 파일 참조 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 논리적 이름입니다.

> [!WARNING]
> `FILE_SNAPSHOT` 백업과 연결된 데이터베이스 파일을 제거하는 것은 성공하지만 연결된 스냅샷은 데이터베이스 파일을 참조하는 백업이 무효화되는 것을 방지하기 위해 삭제되지 않습니다. 파일은 잘라지지만 FILE_SNAPSHOT 백업을 그대로 유지하기 위해 물리적으로 삭제되지는 않습니다. 자세한 내용은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요. **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상).

MODIFY FILE 수정할 파일을 지정합니다. \<filespec> 속성은 한 번에 한 개씩만 변경할 수 있습니다. 수정할 파일을 식별하려면 \<filespec>에 항상 NAME을 지정해야 합니다. SIZE를 지정할 경우 새 크기가 현재 파일 크기보다 커야 합니다.

데이터 파일이나 로그 파일의 논리적 이름을 수정하려면 `NAME` 절에 이름을 바꿀 논리적 파일 이름을 지정하고 `NEWNAME` 절에 파일의 새 논리적 이름을 지정합니다. 예를 들면 다음과 같습니다.

```sql
MODIFY FILE ( NAME = logical_file_name, NEWNAME = new_logical_name )
```

데이터 파일 또는 로그 파일을 새 위치로 이동하려면 `NAME` 절에 파일의 현재 논리적 이름을 지정하고 `FILENAME` 절에 새 경로와 운영 체제 파일 이름을 지정합니다. 예를 들면 다음과 같습니다.

```sql
MODIFY FILE ( NAME = logical_file_name, FILENAME = ' new_path/os_file_name ' )
```

전체 텍스트 카탈로그를 이동하는 경우 FILENAME 절에 새 경로만 지정합니다. 운영 체제 파일 이름은 지정하지 마십시오.

자세한 내용은 [데이터베이스 파일 이동](../../relational-databases/databases/move-database-files.md)을 참조하세요.

FILESTREAM 파일 그룹의 경우 NAME을 온라인으로 수정할 수 있습니다. FILENAME은 온라인으로 수정할 수 있지만 컨테이너를 물리적으로 재배치하고 서버를 종료한 다음 다시 시작하기 전까지는 변경 내용이 적용되지 않습니다.

FILESTREAM 파일을 OFFLINE으로 설정할 수 있습니다. FILESTREAM 파일이 오프라인인 경우 부모 파일 그룹이 내부적으로 오프라인으로 표시되므로 해당 파일 그룹 내에서 FILESTREAM 데이터에 대한 모든 액세스가 실패합니다.

> [!NOTE]
> 포함된 데이터베이스에서는 \<add_or_modify_files> 옵션을 사용할 수 없습니다.

**\<filespec>::=**

파일 속성을 제어합니다.

NAME *logical_file_name* 파일의 논리적 이름을 지정합니다.

*logical_file_name* 파일 참조 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 사용하는 논리적 이름입니다.

NEWNAME *new_logical_file_name* 파일의 새 논리적 이름을 지정합니다.

*new_logical_file_name* 기존 논리적 파일 이름을 바꿀 이름입니다. 이 이름은 데이터베이스 내에서 고유해야 하며 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다. 이름에 문자나 유니코드 상수, 일반 식별자, 구분 식별자를 지정할 수 있습니다.

FILENAME { **'** _os\_file\_name_ **'** | **'** _filestream\_path_ **'** | **'** _memory\_optimized\_data\_path_ **'** } 운영 체제(물리적) 파일 이름을 지정합니다.

' *os_file_name* ' 표준(행) 파일 그룹의 경우 이것은 파일을 만들 때 운영 체제에서 사용한 경로와 파일 이름입니다. 이 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치된 서버에 있어야 합니다. ALTER DATABASE 문을 실행하기 전에 지정된 경로가 존재해야 합니다.

> [!NOTE]
> 파일에 UNC 경로가 지정되면 `SIZE`, `MAXSIZE` 및 `FILEGROWTH` 매개 변수를 설정할 수 없습니다.
>
> 시스템 데이터베이스는 UNC 공유 디렉터리에 상주할 수 없습니다.

파일이 읽기 전용 보조 파일이 아니거나 데이터베이스가 읽기 전용이 아닌 경우 데이터 파일을 압축 파일 시스템에 저장하지 마십시오. 또한 로그 파일을 압축 파일 시스템에 저장하면 안 됩니다.

파일이 원시 파티션에 있는 경우 *os_file_name*은 기존 원시 파티션의 드라이브 문자만 지정해야 합니다. 각 원시 파티션에는 한 개의 파일만 저장할 수 있습니다.

**'** *filestream_path* **'** FILENAME 파일 그룹의 경우 FILENAME은 FILESTREAM 데이터가 저장될 경로를 참조합니다. 따라서 마지막 폴더 바로 위의 경로까지 있어야 하고 마지막 폴더 자체는 있으면 안 됩니다. 예를 들어 `C:\MyFiles\MyFilestreamData` 경로를 지정하는 경우 ALTER DATABASE를 실행하기 전에 `C:\MyFiles` 경로가 있어야 하지만 `MyFilestreamData` 폴더는 있으면 안 됩니다.

> [!NOTE]
> SIZE 및 FILEGROWTH 속성은 FILESTREAM 파일 그룹에 적용되지 않습니다.

**'** *memory_optimized_data_path* **'** 메모리 최적화 파일 그룹에서 FILENAME은 메모리 최적화 데이터가 저장되는 경로를 나타냅니다. 따라서 마지막 폴더 바로 위의 경로까지 있어야 하고 마지막 폴더 자체는 있으면 안 됩니다. 예를 들어 `C:\MyFiles\MyData` 경로를 지정하는 경우 ALTER DATABASE를 실행하기 전에 `C:\MyFiles` 경로가 있어야 하지만 `MyData` 폴더는 있으면 안 됩니다.

파일 그룹과 파일(`<filespec>`)은 같은 문으로 만들어야 합니다.

> [!NOTE]
> SIZE 및 FILEGROWTH 속성은 MEMORY_OPTIMIZED_DATA 파일 그룹에 적용되지 않습니다.

메모리 최적화 파일 그룹에 대한 자세한 내용은 [메모리 최적화 파일 그룹](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)을 참조하세요.

SIZE *size* 파일 크기를 지정합니다. SIZE는 FILESTREAM 파일 그룹에 적용되지 않습니다.

*size* 파일의 크기입니다.

ADD FILE과 함께 지정할 경우 *size*는 파일의 초기 크기입니다. MODIFY FILE과 함께 지정할 경우 *size*는 새로운 파일 크기를 나타내며 현재 파일 크기보다 커야 합니다.

기본 파일에 대해 *size*를 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **model** 데이터베이스의 기본 파일 크기를 사용합니다. 보조 데이터 파일 또는 로그 파일을 지정하지만 해당 파일의 *size*를 지정하지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 파일 크기를 1MB로 지정합니다.

KB, MB, GB 및 TB 접미사를 사용하여 각각 킬로바이트, 메가바이트, 기가바이트, 테라바이트를 지정할 수 있습니다. 기본값은 MB입니다. 소수점을 포함하지 않은 정수를 지정합니다. 소수로 된 MB 값을 지정하려면 1024를 곱하여 값을 KB로 변환합니다. 예를 들어 1.5MB인 경우 1536KB(1.5 x 1024 = 1536)를 지정합니다.

> [!NOTE]
> `SIZE`를 설정할 수 없습니다.
>
> - 파일에 대해 UNC 경로가 지정된 경우
> - `FILESTREAM` 및 `MEMORY_OPTIMIZED_DATA` 파일 그룹의 경우

MAXSIZE { *max_size*| UNLIMITED } 파일을 확장할 수 있는 최대 파일 크기를 지정합니다.

*max_size* 최대 파일 크기입니다. KB, MB, GB 및 TB 접미사를 사용하여 각각 킬로바이트, 메가바이트, 기가바이트, 테라바이트를 지정할 수 있습니다. 기본값은 MB입니다. 소수점을 포함하지 않은 정수를 지정합니다. *max_size*를 지정하지 않으면 디스크가 꽉 찰 때까지 파일 크기가 늘어납니다.

UNLIMITED 디스크가 꽉 찰 때까지 파일 크기가 증가하도록 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 무제한 증가로 지정된 로그 파일의 최대 크기는 2TB이고 데이터 파일의 최대 크기는 16TB입니다. 이 옵션이 FILESTREAM 컨테이너에 지정되면 최대 크기가 없습니다. 디스크가 꽉 찰 때까지 파일이 증가합니다.

> [!NOTE]
> 파일에 대해 UNC 경로가 지정된 경우 `MAXSIZE`를 설정할 수 없습니다.

FILEGROWTH *growth_increment* 파일의 자동 증분을 지정합니다. 파일의 FILEGROWTH 설정은 MAXSIZE 설정을 초과할 수 없습니다. FILEGROWTH는 FILESTREAM 파일 그룹에 적용되지 않습니다.

*growth_increment* 공간이 새로 필요할 때마다 파일에 추가되는 공간 크기입니다.

이 값은 MB, KB, GB, TB 또는 %(퍼센트) 단위로 지정할 수 있습니다. MB, KB 또는 % 접미사를 붙이지 않고 숫자를 지정하면 MB가 기본값이 됩니다. %가 지정되면 증분 크기는 파일 크기 증가가 발생하는 시점에서 해당 파일 크기에 대한 특정 비율입니다. 지정한 크기는 64KB 단위로 반올림됩니다.

값 0은 자동 증가를 사용하지 않고 추가 공간을 허용하지 않음을 나타냅니다.

FILEGROWTH를 지정하지 않은 경우 기본값은 다음과 같습니다.

|버전|기본값|
|-------------|--------------------|
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]로 시작|데이터는 64MB입니다. 로그 파일은 64MB입니다.|
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]로 시작|데이터는 1MB입니다. 로그 파일은 10%입니다.|
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이전|데이터는 10%입니다. 로그 파일은 10%입니다.|

> [!NOTE]
> `FILEGROWTH`를 설정할 수 없습니다.
>
> - 파일에 대해 UNC 경로가 지정된 경우
> - `FILESTREAM` 및 `MEMORY_OPTIMIZED_DATA` 파일 그룹의 경우

OFFLINE 파일을 오프라인으로 설정하고 파일 그룹 내의 모든 개체를 액세스할 수 없도록 합니다.

> [!CAUTION]
> 파일이 손상되고 복원이 가능한 경우에만 이 옵션을 사용하십시오. OFFLINE으로 설정된 파일은 해당 파일을 백업에서 복원해야만 온라인 상태로 설정할 수 있습니다. 단일 파일 복원에 대한 자세한 내용은 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)를 참조하세요.
>
> 포함된 데이터베이스에서는 \<filespec> 옵션을 사용할 수 없습니다.

**\<add_or_modify_filegroups>::=**

데이터베이스의 파일 그룹을 추가, 수정 또는 제거합니다.

ADD FILEGROUP *filegroup_name* 데이터베이스에 파일 그룹을 추가합니다.

CONTAINS FILESTREAM 파일 그룹이 FILESTREAM BLOB(Binary Large Object)을 파일 시스템에 저장하도록 지정합니다.

CONTAINS MEMORY_OPTIMIZED_DATA

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]( [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상)

파일 그룹이 메모리 액세스에 최적화된 데이터를 파일 시스템에 저장하도록 지정합니다. 자세한 내용은 [메모리 내 OLTP - 메모리 내 최적화](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요. 데이터베이스당 하나의 `MEMORY_OPTIMIZED_DATA` 파일 그룹만 허용됩니다. 메모리 액세스에 최적화된 테이블을 만들기 위해서는 파일 그룹을 비워 둘 수 없습니다. 적어도 한 개의 파일이 있어야 합니다. *filegroup_name*은 경로를 참조합니다. 따라서 마지막 폴더 바로 위의 경로까지 있어야 하고 마지막 폴더 자체는 있으면 안 됩니다.

REMOVE FILEGROUP *filegroup_name* 데이터베이스에서 파일 그룹을 제거합니다. 파일 그룹은 비어 있어야 제거할 수 있습니다. 먼저 파일 그룹에서 모든 파일을 제거합니다. 자세한 내용은 이 토픽의 앞부분에 나오는 "REMOVE FILE *logical_file_name*"을 참조하세요.

> [!NOTE]
> FILESTREAM 가비지 수집기가 FILESTREAM 컨테이너에서 모든 파일을 제거하지 않은 경우 FILESTREAM 컨테이너를 제거하기 위한 `ALTER DATABASE REMOVE FILE` 작업이 실패하고 오류를 반환합니다. 이 항목의 뒷부분에 나오는 [FILESTREAM 컨테이너 제거](#removing-a-filestream-container) 섹션을 참조하세요.

MODIFY FILEGROUP *filegroup_name* { \<filegroup_updatability_option> | DEFAULT | NAME **=** _new\_filegroup\_name_ } 파일 그룹 상태를 READ_ONLY 또는 READ_WRITE로 설정하고 파일 그룹을 데이터베이스에 대한 기본 파일 그룹으로 설정하거나 파일 그룹 이름을 바꿔 파일 그룹을 수정합니다.

\<filegroup_updatability_option> 파일 그룹에 대한 읽기 전용 또는 읽기/쓰기 속성을 설정합니다.

DEFAULT 기본 데이터베이스 파일 그룹을 *filegroup_name*으로 변경합니다. 데이터베이스에서 한 개의 파일 그룹만 기본 파일 그룹이 될 수 있습니다. 자세한 내용은 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)을 참조하세요.

NAME = *new_filegroup_name* 파일 그룹 이름을 *new_filegroup_name*으로 변경합니다.

AUTOGROW_SINGLE_FILE **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상)

파일 그룹의 파일이 자동 증가 임계값을 충족하면 해당 파일만이 증가합니다. 이것이 기본값입니다.

AUTOGROW_ALL_FILES

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상)

파일 그룹의 파일이 자동 증가 임계값을 충족하면 파일 그룹의 모든 파일이 커집니다.

> [!NOTE]
> TempDB의 기본값입니다.

**\<filegroup_updatability_option>::=**

파일 그룹에 대한 읽기 전용 또는 읽기/쓰기 속성을 설정합니다.

READ_ONLY | READONLY 파일 그룹을 읽기 전용으로 지정합니다. 해당 파일 그룹의 개체를 업데이트할 수 없습니다. 주 파일 그룹은 읽기 전용으로 만들 수 없습니다. 이 상태를 변경하려면 데이터베이스에 대해 배타적 액세스 권한이 있어야 합니다. 자세한 내용은 SINGLE_USER 절을 참조하십시오.

읽기 전용 데이터베이스는 데이터 수정을 허용하지 않기 때문에 다음과 같은 특성을 포함합니다.

- 시스템 시작 시 자동 복원을 하지 않습니다.
- 데이터베이스 축소가 불가능합니다.
- 읽기 전용 데이터베이스에서는 잠금이 발생하지 않습니다. 따라서 쿼리 성능은 더 향상될 수 있습니다.

> [!NOTE]
> 키워드 `READONLY`는 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 향후 버전에서 제거될 예정입니다. 향후 개발 작업에서는 `READONLY`를 사용하지 않도록 하고 현재 `READONLY`를 사용하는 애플리케이션은 수정하세요. 대신 `READ_ONLY`를 사용하세요.

READ_WRITE | READWRITE 파일 그룹을 READ_WRITE로 지정합니다. 해당 파일 그룹의 개체를 업데이트할 수 있습니다. 이 상태를 변경하려면 데이터베이스에 대해 배타적 액세스 권한이 있어야 합니다. 자세한 내용은 SINGLE_USER 절을 참조하십시오.

> [!NOTE]
> 키워드 `READWRITE`는 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 향후 버전에서 제거될 예정입니다. 새 개발 작업에서 `READWRITE`를 사용하지 않도록 하고 현재 `READWRITE`를 사용하는 애플리케이션을 `READ_WRITE`를 대신 사용하도록 수정하세요.
> [!TIP]
> 이러한 옵션의 상태는 **sys.databases** 카탈로그 뷰의 **is_read_only** 열 또는 `DATABASEPROPERTYEX` 함수의 **Updateability** 속성을 검사하여 결정할 수 있습니다.

## <a name="remarks"></a>설명

데이터베이스의 크기를 줄이려면 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)를 사용합니다.

`BACKUP` 문이 실행 중인 동안에는 파일을 추가 또는 제거할 수 없습니다.

각 데이터베이스에 최대 32,767개의 파일과 32,767개의 파일 그룹을 지정할 수 있습니다.

[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 데이터베이스 파일의 상태(예: 온라인 또는 오프라인)는 데이터베이스의 상태와 독립적으로 유지됩니다. 자세한 내용은 [파일 상태](../../relational-databases/databases/file-states.md)를 참조하세요.

- 전체 파일 그룹의 가용성은 파일 그룹 내 파일의 상태에 따라 결정됩니다. 파일 그룹을 사용하려면 파일 그룹 내의 모든 파일이 온라인 상태여야 합니다.
- 파일 그룹이 오프라인 상태인 경우 SQL 문을 사용한 파일 그룹 액세스 시도는 오류가 발생하며 실패하게 됩니다. `SELECT` 문에 대한 쿼리 계획을 작성하는 경우, 쿼리 최적화 프로그램은 비클러스터형 인덱스 및 오프라인 파일 그룹에 상주하는 인덱싱된 뷰를 사용하지 않습니다. 이러한 문이 성공하도록 합니다. 그러나 오프라인 파일 그룹에 대상 테이블의 힙이나 클러스터형 인덱스가 있는 경우 `SELECT` 문은 실패합니다. 또한 오프라인 파일 그룹에 인덱스를 가진 테이블을 수정하는 `INSERT`, `UPDATE` 또는 `DELETE` 문은 실패합니다.

파일에 UNC 경로가 지정되면 SIZE, MAXSIZE 및 FILEGROWTH 매개 변수를 설정할 수 없습니다.

메모리 최적화 파일 그룹에 대해 SIZE 및 FILEGROWTH 매개 변수를 설정할 수 없습니다.

키워드 `READONLY`는 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 향후 버전에서 제거될 예정입니다. 향후 개발 작업에서는 `READONLY`를 사용하지 않도록 하고 현재 READONLY를 사용하는 애플리케이션은 수정하세요. 대신 `READ_ONLY`를 사용하세요.

키워드 `READWRITE`는 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 향후 버전에서 제거될 예정입니다. 새 개발 작업에서 `READWRITE`를 사용하지 않도록 하고 현재 `READWRITE`를 사용하는 애플리케이션을 `READ_WRITE`를 대신 사용하도록 수정하세요.

## <a name="moving-files"></a>파일 이동

FILENAME에 새 위치를 지정하여 시스템 또는 사용자 정의 데이터 및 로그 파일을 이동할 수 있습니다. 이는 다음과 같은 시나리오에서 유용합니다.

- 오류 복구. 예를 들어 데이터베이스가 주의 대상 모드이거나 하드웨어 오류로 인해 종료된 경우입니다.
- 계획된 재배치
- 예약된 디스크 유지 관리를 위한 재배치

자세한 내용은 [데이터베이스 파일 이동](../../relational-databases/databases/move-database-files.md)을 참조하세요.

## <a name="initializing-files"></a>파일 초기화

기본적으로 데이터 및 로그 파일은 사용자가 다음 작업 중 하나를 수행할 때 0으로 채워져 초기화됩니다.

- 데이터베이스 만들기
- 기존 데이터베이스에 파일 추가
- 기존 파일의 크기 증가
- 데이터베이스 또는 파일 그룹을 복원합니다.

데이터 파일을 즉시 초기화할 수 있습니다. 이를 통해 이와 같은 파일 작업을 신속히 실행할 수 있습니다. 자세한 내용은 [데이터베이스 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)를 참조하세요.

## <a name="removing-a-filestream-container"></a><a name="removing-a-filestream-container"></a> FILESTREAM 컨테이너 제거

"DBCC SHRINKFILE" 작업을 사용하여 FILESTREAM 컨테이너를 비웠어도 데이터베이스에서 여러 가지 시스템 유지 관리상의 이유로 삭제된 파일에 대한 참조를 보존해야 하는 경우가 있습니다. [sp_filestream_force_garbage_collection](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)은 안전하다고 판단되면 FILESTREAM 가비지 수집기를 실행하여 이러한 파일을 제거합니다. FILESTREAM 가비지 수집기가 FILESTREAM 컨테이너에서 모든 파일을 제거하지 않은 경우 FILESTREAM 컨테이너를 제거하기 위한 ALTER DATABASE REMOVE FILE 작업이 실패하고 오류를 반환합니다. 다음 프로세스를 사용하여 FILESTREAM 컨테이너를 제거하는 것이 좋습니다.

1. EMPTYFILE을 지정하고 [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)을 실행하여 이 컨테이너의 활성 콘텐츠를 다른 컨테이너로 이동합니다.
2. FULL 또는 BULK_LOGGED 복구 모델에서 로그 백업이 수행되었는지 확인합니다.
3. 복제 로그 판독기 작업이 실행되었는지 확인합니다(해당되는 경우).
4. [sp_filestream_force_garbage_collection](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)을 실행하여 가비지 수집기가 이 컨테이너에 더 이상 필요하지 않은 파일을 삭제하게 합니다.
5. ALTER DATABASE를 REMOVE FILE 옵션과 함께 실행하여 이 컨테이너를 제거합니다.
6. 2-4단계를 두 번 이상 반복하여 가비지 수집을 완료합니다.
7. ALTER Database...REMOVE FILE을 사용하여 이 컨테이너를 제거합니다.

## <a name="examples"></a>예

### <a name="a-adding-a-file-to-a-database"></a>A. 데이터베이스에 파일 추가

다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 5MB 데이터 파일을 추가합니다.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
ADD FILE
(
    NAME = Test1dat2,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat2.ndf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
);
GO
```

### <a name="b-adding-a-filegroup-with-two-files-to-a-database"></a>B. 데이터베이스에 두 개의 파일이 포함된 파일 그룹 추가

다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 `Test1FG1` 파일 그룹을 만들고 이 파일 그룹에 두 개의 5MB 파일을 추가합니다.

```sql
USE master
GO
ALTER DATABASE AdventureWorks2012
ADD FILEGROUP Test1FG1;
GO
ALTER DATABASE AdventureWorks2012
ADD FILE
(
    NAME = test1dat3,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat3.ndf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
),  
(  
    NAME = test1dat4,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat4.ndf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
)  
TO FILEGROUP Test1FG1;
GO
```

### <a name="c-adding-two-log-files-to-a-database"></a>C. 데이터베이스에 두 개의 로그 파일 추가

다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 두 개의 5MB 로그 파일을 추가합니다.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
ADD LOG FILE
(
    NAME = test1log2,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\test2log.ldf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
),
(
    NAME = test1log3,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\DATA\test3log.ldf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
);
GO
```

### <a name="d-removing-a-file-from-a-database"></a>D. 데이터베이스에서 파일 제거

다음 예에서는 2번 예에서 추가한 파일 중 하나를 제거합니다.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
REMOVE FILE test1dat4;
GO
```

### <a name="e-modifying-a-file"></a>E. 파일 수정

다음 예에서는 예제 B에서 추가한 파일 중 하나의 크기를 늘립니다. MODIFY FILE 명령을 포함한 ALTER DATABASE는 파일 크기를 더 크게 만들 수만 있으므로 파일 크기를 더 작게 만들려면 DBCC SHRINKFILE을 사용해야 합니다.

```sql
USE master;
GO

ALTER DATABASE AdventureWorks2012
MODIFY FILE
(NAME = test1dat3,
SIZE = 200MB);
GO
```

이 예제에서는 데이터 파일의 크기를 100 MB로 줄인 다음, 크기를 해당 크기로 지정합니다.

```sql
USE AdventureWorks2012;
GO

DBCC SHRINKFILE (AdventureWorks2012_data, 100);
GO

USE master;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILE
(NAME = test1dat3,
SIZE = 200MB);
GO
```

### <a name="f-moving-a-file-to-a-new-location"></a>F. 파일을 새 위치로 이동

다음 예에서는 1번 예에서 만든 `Test1dat2` 파일을 새 디렉터리로 이동합니다.

> [!NOTE]
> 이 예를 실행하기 전에 해당 파일을 새 디렉터리로 물리적으로 이동해야 합니다. 그 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 중지한 후 다시 시작하거나 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 OFFLINE으로 설정한 후 다시 ONLINE으로 되돌려 변경 사항을 적용합니다.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILE
(
    NAME = Test1dat2,
    FILENAME = N'c:\t1dat2.ndf'
);
GO
```

### <a name="g-moving-tempdb-to-a-new-location"></a>G. tempdb를 새 위치로 이동

다음 예에서는 `tempdb`를 디스크의 현재 위치에서 다른 디스크 위치로 이동합니다. MSSQLSERVER 서비스를 시작할 때마다 `tempdb`가 다시 생성되므로 데이터와 로그 파일을 물리적으로 이동할 필요는 없습니다. 3단계에서 서비스를 다시 시작할 때 파일이 생성됩니다. 서비스를 다시 시작하기 전까지는 `tempdb`가 기존의 위치에서 작업을 수행합니다.

1. `tempdb` 데이터베이스의 논리적 파일 이름 및 디스크에서 현재 위치를 결정합니다.

    ```sql
    SELECT name, physical_name
    FROM sys.master_files
    WHERE database_id = DB_ID('tempdb');
    GO
    ```

2. `ALTER DATABASE`를 사용하여 각 파일의 위치를 변경합니다.

    ```sql
    USE master;
    GO
    ALTER DATABASE tempdb
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');
    GO
    ALTER DATABASE tempdb
    MODIFY FILE (NAME = templog, FILENAME = 'E:\SQLData\templog.ldf');
    GO
    ```

3. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 중지한 후 다시 시작합니다.

4. 파일 변경 내용을 확인합니다.

    ```sql
    SELECT name, physical_name
    FROM sys.master_files
    WHERE database_id = DB_ID('tempdb');
    ```

5. tempdb.mdf 및 templog.ldf 파일을 원래 위치에서 삭제합니다.

### <a name="h-making-a-filegroup-the-default"></a>H. 기본 파일 그룹 설정

다음 예제에서는 예제 B에서 만든 `Test1FG1` 파일 그룹을 기본 파일 그룹으로 만듭니다. 그 다음 `PRIMARY` 파일 그룹을 기본 파일 그룹으로 다시 설정합니다. `PRIMARY`는 대괄호 또는 따옴표로 구분해야 합니다.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILEGROUP Test1FG1 DEFAULT;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILEGROUP [PRIMARY] DEFAULT;
GO
```

### <a name="i-adding-a-filegroup-using-alter-database"></a>9\. ALTER DATABASE를 사용하여 파일 그룹 추가

다음 예에서는 `FILEGROUP` 절을 포함하는 `FILESTREAM`을 `FileStreamPhotoDB` 데이터베이스에 추가합니다.

```sql
--Create and add a FILEGROUP that CONTAINS the FILESTREAM clause.
ALTER DATABASE FileStreamPhotoDB
ADD FILEGROUP TodaysPhotoShoot
CONTAINS FILESTREAM;
GO

--Add a file for storing database photos to FILEGROUP
ALTER DATABASE FileStreamPhotoDB
ADD FILE
(
  NAME= 'PhotoShoot1',
  FILENAME = 'C:\Users\Administrator\Pictures\TodaysPhotoShoot.ndf'
)
TO FILEGROUP TodaysPhotoShoot;
GO
```

다음 예에서는 `FILEGROUP` 절을 포함하는 `MEMORY_OPTIMIZED_DATA`을 `xtp_db` 데이터베이스에 추가합니다. 파일 그룹은 메모리 최적화 데이터를 저장합니다.

```sql
--Create and add a FILEGROUP that CONTAINS the MEMORY_OPTIMIZED_DATA clause.
ALTER DATABASE xtp_db
ADD FILEGROUP xtp_fg
CONTAINS MEMORY_OPTIMIZED_DATA;
GO

--Add a file for storing memory optimized data to FILEGROUP
ALTER DATABASE xtp_db
ADD FILE
(
  NAME='xtp_mod',
  FILENAME='d:\data\xtp_mod'
)
TO FILEGROUP xtp_fg;
GO
```

### <a name="j-change-filegroup-so-that-when-a-file-in-the-filegroup-meets-the-autogrow-threshold-all-files-in-the-filegroup-grow"></a>J. 파일 그룹을 파일 그룹의 파일이 자동 증가 임계값을 충족하면 파일 그룹의 모든 파일이 증가하도록 변경합니다.

 다음 예제에서는 필수 `ALTER DATABASE` 문을 생성하고 `AUTOGROW_ALL_FILES` 설정을 사용하여 읽기-쓰기 파일 그룹을 수정합니다.

```sql
--Generate ALTER DATABASE ... MODIFY FILEGROUP statements
--so that all read-write filegroups grow at the same time.
SET NOCOUNT ON;

DROP TABLE IF EXISTS #tmpdbs
CREATE TABLE #tmpdbs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, isdone bit);

DROP TABLE IF EXISTS #tmpfgs
CREATE TABLE #tmpfgs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, fgname sysname, isdone bit);

INSERT INTO #tmpdbs ([dbid], [dbname], [isdone])
SELECT database_id, name, 0 FROM master.sys.databases (NOLOCK) WHERE is_read_only = 0 AND state = 0;

DECLARE @dbid int, @query VARCHAR(1000), @dbname sysname, @fgname sysname

WHILE (SELECT COUNT(id) FROM #tmpdbs WHERE isdone = 0) > 0
BEGIN
  SELECT TOP 1 @dbname = [dbname], @dbid = [dbid] FROM #tmpdbs WHERE isdone = 0

  SET @query = 'SELECT ' + CAST(@dbid AS NVARCHAR) + ', ''' + @dbname + ''', [name], 0 FROM [' + @dbname + '].sys.filegroups WHERE [type] = ''FG'' AND is_read_only = 0;'
  INSERT INTO #tmpfgs
  EXEC (@query)

  UPDATE #tmpdbs
  SET isdone = 1
  WHERE [dbid] = @dbid
END;

IF (SELECT COUNT(ID) FROM #tmpfgs) > 0
BEGIN
  WHILE (SELECT COUNT(id) FROM #tmpfgs WHERE isdone = 0) > 0
  BEGIN
    SELECT TOP 1 @dbname = [dbname], @dbid = [dbid], @fgname = fgname FROM #tmpfgs WHERE isdone = 0

    SET @query = 'ALTER DATABASE [' + @dbname + '] MODIFY FILEGROUP [' + @fgname + '] AUTOGROW_ALL_FILES;'

    PRINT @query

    UPDATE #tmpfgs
    SET isdone = 1
    WHERE [dbid] = @dbid AND fgname = @fgname
  END
END;
GO
```

## <a name="see-also"></a>참고 항목

- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [BLOB(Binary Large Object)](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)
- [DBCC SHRINKFIL](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)
- [sp_filestream_force_garbage_collection](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)
- [데이터베이스 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql-file-and-filegroup-options.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        **_\* SQL Database<br />Managed Instance \*_**<br />&nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-sql-managed-instance"></a>Azure SQL Managed Instance

Azure SQL Managed Instance의 데이터베이스에 이 문을 사용합니다.

## <a name="syntax-for-azure-sql-managed-instance"></a>Azure SQL Managed Instance용 구문

```syntaxsql
ALTER DATABASE database_name
{
    <add_or_modify_files>
  | <add_or_modify_filegroups>
}
[;]

<add_or_modify_files>::=
{
    ADD FILE <filespec> [ ,...n ]
        [ TO FILEGROUP { filegroup_name } ]
  | REMOVE FILE logical_file_name
  | MODIFY FILE <filespec>
}
  
<filespec>::=
(
    NAME = logical_file_name
    [ , SIZE = size [ KB | MB | GB | TB ] ]
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB| % ] ]
)

<add_or_modify_filegroups>::=
{
    | ADD FILEGROUP filegroup_name
    | REMOVE FILEGROUP filegroup_name
    | MODIFY FILEGROUP filegroup_name
        { <filegroup_updatability_option>
        | DEFAULT
        | NAME = new_filegroup_name
        | { AUTOGROW_SINGLE_FILE | AUTOGROW_ALL_FILES }
        }
}  
<filegroup_updatability_option>::=
{
    { READONLY | READWRITE }
    | { READ_ONLY | READ_WRITE }
}

```

## <a name="arguments"></a>인수

**\<add_or_modify_files>::=**

추가, 제거 또는 수정할 파일을 지정합니다.

*database_name* 수정할 데이터베이스의 이름입니다.

ADD FILE 데이터베이스에 파일을 추가합니다.

TO FILEGROUP { *filegroup_name* } 지정된 파일을 추가할 파일 그룹을 지정합니다. 현재 파일 그룹을 표시하고 어떤 파일 그룹이 현재 기본 파일 그룹인지 표시하려면 [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) 카탈로그 뷰를 사용하십시오.

REMOVE FILE *logical_file_name*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 논리적 파일 설명을 제거하고 물리적 파일을 삭제합니다. 파일이 비어 있어야 제거할 수 있습니다.

*logical_file_name* 파일 참조 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 논리적 이름입니다.

MODIFY FILE 수정할 파일을 지정합니다. \<filespec> 속성은 한 번에 한 개씩만 변경할 수 있습니다. 수정할 파일을 식별하려면 \<filespec>에 항상 NAME을 지정해야 합니다. SIZE를 지정할 경우 새 크기가 현재 파일 크기보다 커야 합니다.

**\<filespec>::=**

파일 속성을 제어합니다.

NAME *logical_file_name* 파일의 논리적 이름을 지정합니다.

*logical_file_name* 파일 참조 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 사용하는 논리적 이름입니다.

NEWNAME *new_logical_file_name* 파일의 새 논리적 이름을 지정합니다.

*new_logical_file_name* 기존 논리적 파일 이름을 바꿀 이름입니다. 이 이름은 데이터베이스 내에서 고유해야 하며 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다. 이름에 문자나 유니코드 상수, 일반 식별자, 구분 식별자를 지정할 수 있습니다.

SIZE *size* 파일 크기를 지정합니다.

*size* 파일의 크기입니다.

ADD FILE과 함께 지정할 경우 *size*는 파일의 초기 크기입니다. MODIFY FILE과 함께 지정할 경우 *size*는 새로운 파일 크기를 나타내며 현재 파일 크기보다 커야 합니다.

기본 파일에 대해 *size*를 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **model** 데이터베이스의 기본 파일 크기를 사용합니다. 보조 데이터 파일 또는 로그 파일을 지정하지만 해당 파일의 *size*를 지정하지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 파일 크기를 1MB로 지정합니다.

KB, MB, GB 및 TB 접미사를 사용하여 각각 킬로바이트, 메가바이트, 기가바이트, 테라바이트를 지정할 수 있습니다. 기본값은 MB입니다. 소수점을 포함하지 않은 정수를 지정합니다. 소수로 된 MB 값을 지정하려면 1024를 곱하여 값을 KB로 변환합니다. 예를 들어 1.5MB인 경우 1536KB(1.5 x 1024 = 1536)를 지정합니다.

MAXSIZE { *max_size*| UNLIMITED } 파일을 확장할 수 있는 최대 파일 크기를 지정합니다.

*max_size* 최대 파일 크기입니다. KB, MB, GB 및 TB 접미사를 사용하여 각각 킬로바이트, 메가바이트, 기가바이트, 테라바이트를 지정할 수 있습니다. 기본값은 MB입니다. 소수점을 포함하지 않은 정수를 지정합니다. *max_size*를 지정하지 않으면 디스크가 꽉 찰 때까지 파일 크기가 늘어납니다.

UNLIMITED 디스크가 꽉 찰 때까지 파일 크기가 증가하도록 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 무제한 증가로 지정된 로그 파일의 최대 크기는 2TB이고 데이터 파일의 최대 크기는 16TB입니다.

FILEGROWTH *growth_increment* 파일의 자동 증분을 지정합니다. 파일의 FILEGROWTH 설정은 MAXSIZE 설정을 초과할 수 없습니다.

*growth_increment* 공간이 새로 필요할 때마다 파일에 추가되는 공간 크기입니다.

이 값은 MB, KB, GB, TB 또는 %(퍼센트) 단위로 지정할 수 있습니다. MB, KB 또는 % 접미사를 붙이지 않고 숫자를 지정하면 MB가 기본값이 됩니다. %가 지정되면 증분 크기는 파일 크기 증가가 발생하는 시점에서 해당 파일 크기에 대한 특정 비율입니다. 지정한 크기는 64KB 단위로 반올림됩니다.

값 0은 자동 증가를 사용하지 않고 추가 공간을 허용하지 않음을 나타냅니다.

FILEGROWTH를 지정하지 않은 경우 기본값은 다음과 같습니다.

- 데이터 64MB
- 로그 파일 64MB

**\<add_or_modify_filegroups>::=**

데이터베이스의 파일 그룹을 추가, 수정 또는 제거합니다.

ADD FILEGROUP *filegroup_name* 데이터베이스에 파일 그룹을 추가합니다.

다음 예에서는 sql_db_mi 데이터베이스에 추가된 파일 그룹을 만들고 파일을 이 파일 그룹에 추가합니다.

```sql
ALTER DATABASE sql_db_mi ADD FILEGROUP sql_db_mi_fg;
GO
ALTER DATABASE sql_db_mi ADD FILE (NAME='sql_db_mi_mod') TO FILEGROUP sql_db_mi_fg;
```

REMOVE FILEGROUP *filegroup_name* 데이터베이스에서 파일 그룹을 제거합니다. 파일 그룹은 비어 있어야 제거할 수 있습니다. 먼저 파일 그룹에서 모든 파일을 제거합니다. 자세한 내용은 이 토픽의 앞부분에 나오는 "REMOVE FILE *logical_file_name*"을 참조하세요.

MODIFY FILEGROUP _filegroup\_name_ { \<filegroup_updatability_option> | DEFAULT | NAME **=** _new\_filegroup\_name_ } 파일 그룹 상태를 READ_ONLY 또는 READ_WRITE로 설정하고 파일 그룹을 데이터베이스에 대한 기본 파일 그룹으로 설정하거나 파일 그룹 이름을 바꿔 파일 그룹을 수정합니다.

\<filegroup_updatability_option> 파일 그룹에 대한 읽기 전용 또는 읽기/쓰기 속성을 설정합니다.

DEFAULT 기본 데이터베이스 파일 그룹을 *filegroup_name*으로 변경합니다. 데이터베이스에서 한 개의 파일 그룹만 기본 파일 그룹이 될 수 있습니다. 자세한 내용은 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)을 참조하세요.

NAME = *new_filegroup_name* 파일 그룹 이름을 *new_filegroup_name*으로 변경합니다.

AUTOGROW_SINGLE_FILE

파일 그룹의 파일이 자동 증가 임계값을 충족하면 해당 파일만이 증가합니다. 이것이 기본값입니다.

AUTOGROW_ALL_FILES

파일 그룹의 파일이 자동 증가 임계값을 충족하면 파일 그룹의 모든 파일이 커집니다.

**\<filegroup_updatability_option>::=**

파일 그룹에 대한 읽기 전용 또는 읽기/쓰기 속성을 설정합니다.

READ_ONLY | READONLY 파일 그룹을 읽기 전용으로 지정합니다. 해당 파일 그룹의 개체를 업데이트할 수 없습니다. 주 파일 그룹은 읽기 전용으로 만들 수 없습니다. 이 상태를 변경하려면 데이터베이스에 대해 배타적 액세스 권한이 있어야 합니다. 자세한 내용은 SINGLE_USER 절을 참조하십시오.

읽기 전용 데이터베이스는 데이터 수정을 허용하지 않기 때문에 다음과 같은 특성을 포함합니다.

- 시스템 시작 시 자동 복원을 하지 않습니다.
- 데이터베이스 축소가 불가능합니다.
- 읽기 전용 데이터베이스에서는 잠금이 발생하지 않습니다. 따라서 쿼리 성능은 더 향상될 수 있습니다.

> [!NOTE]
> READONLY 키워드는 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 향후 버전에서 제거될 예정입니다. 향후 개발 작업에서는 READONLY를 사용하지 않도록 하고 현재 READONLY를 사용하는 애플리케이션은 수정하십시오. 대신 READ_ONLY를 사용하십시오.

READ_WRITE | READWRITE 파일 그룹을 READ_WRITE로 지정합니다. 해당 파일 그룹의 개체를 업데이트할 수 있습니다. 이 상태를 변경하려면 데이터베이스에 대해 배타적 액세스 권한이 있어야 합니다. 자세한 내용은 SINGLE_USER 절을 참조하십시오.

> [!NOTE]
> 키워드 `READWRITE`는 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 향후 버전에서 제거될 예정입니다. 새 개발 작업에서 `READWRITE`를 사용하지 않도록 하고 현재 `READWRITE`를 사용하는 애플리케이션을 `READ_WRITE`를 대신 사용하도록 수정하세요.

이러한 옵션의 상태는 **sys.databases** 카탈로그 뷰의 **is_read_only** 열 또는 `DATABASEPROPERTYEX` 함수의 **Updateability** 속성을 검사하여 결정할 수 있습니다.

## <a name="remarks"></a>설명

데이터베이스의 크기를 줄이려면 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)를 사용합니다.

`BACKUP` 문이 실행 중인 동안에는 파일을 추가 또는 제거할 수 없습니다.

각 데이터베이스에 최대 32,767개의 파일과 32,767개의 파일 그룹을 지정할 수 있습니다.

## <a name="examples"></a>예

### <a name="a-adding-a-file-to-a-database"></a>A. 데이터베이스에 파일 추가

다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 5MB 데이터 파일을 추가합니다.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
ADD FILE
(
  NAME = Test1dat2,
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
);
GO
```

### <a name="b-adding-a-filegroup-with-two-files-to-a-database"></a>B. 데이터베이스에 두 개의 파일이 포함된 파일 그룹 추가

다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 `Test1FG1` 파일 그룹을 만들고 이 파일 그룹에 두 개의 5MB 파일을 추가합니다.

```sql
USE master
GO
ALTER DATABASE AdventureWorks2012
ADD FILEGROUP Test1FG1;
GO
ALTER DATABASE AdventureWorks2012
ADD FILE
(
    NAME = test1dat3,
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
),
(
    NAME = test1dat4,
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
)  
TO FILEGROUP Test1FG1;
GO

```

### <a name="c-removing-a-file-from-a-database"></a>C. 데이터베이스에서 파일 제거

다음 예에서는 2번 예에서 추가한 파일 중 하나를 제거합니다.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
REMOVE FILE test1dat4;
GO
```

### <a name="d-modifying-a-file"></a>D. 파일 수정

다음 예에서는 예제 B에서 추가한 파일 중 하나의 크기를 늘립니다. MODIFY FILE 명령을 포함한 ALTER DATABASE는 파일 크기를 더 크게 만들 수만 있으므로 파일 크기를 더 작게 만들려면 DBCC SHRINKFILE을 사용해야 합니다.

```sql
USE master;
GO

ALTER DATABASE AdventureWorks2012
MODIFY FILE
(NAME = test1dat3,
SIZE = 200MB);
GO
```

이 예제에서는 데이터 파일의 크기를 100 MB로 줄인 다음, 크기를 해당 크기로 지정합니다.

```sql
USE AdventureWorks2012;
GO

DBCC SHRINKFILE (AdventureWorks2012_data, 100);
GO

USE master;
GO

ALTER DATABASE AdventureWorks2012
MODIFY FILE
(NAME = test1dat3,
SIZE = 200MB);
GO
```

### <a name="e-making-a-filegroup-the-default"></a>E. 기본 파일 그룹 설정

다음 예제에서는 예제 B에서 만든 `Test1FG1` 파일 그룹을 기본 파일 그룹으로 만듭니다. 그 다음 `PRIMARY` 파일 그룹을 기본 파일 그룹으로 다시 설정합니다. `PRIMARY`는 대괄호 또는 따옴표로 구분해야 합니다.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILEGROUP Test1FG1 DEFAULT;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILEGROUP [PRIMARY] DEFAULT;
GO
```

### <a name="f-adding-a-filegroup-using-alter-database"></a>F. ALTER DATABASE를 사용하여 파일 그룹 추가

다음 예에서는 `FILEGROUP`을 `MyDB` 데이터베이스에 추가합니다.

```sql
--Create and add a FILEGROUP
ALTER DATABASE MyDB
ADD FILEGROUP NewFG;
GO

--Add a file to FILEGROUP
ALTER DATABASE MyDB
ADD FILE
(
    NAME= 'MyFile',
)
TO FILEGROUP NewFG;
GO
```

### <a name="g-change-filegroup-so-that-when-a-file-in-the-filegroup-meets-the-autogrow-threshold-all-files-in-the-filegroup-grow"></a>G. 파일 그룹을 파일 그룹의 파일이 자동 증가 임계값을 충족하면 파일 그룹의 모든 파일이 증가하도록 변경합니다.

다음 예제에서는 필수 `ALTER DATABASE` 문을 생성하고 `AUTOGROW_ALL_FILES` 설정을 사용하여 읽기-쓰기 파일 그룹을 수정합니다.

```sql
--Generate ALTER DATABASE ... MODIFY FILEGROUP statements
--so that all read-write filegroups grow at the same time.
SET NOCOUNT ON;

DROP TABLE IF EXISTS #tmpdbs
CREATE TABLE #tmpdbs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, isdone bit);

DROP TABLE IF EXISTS #tmpfgs
CREATE TABLE #tmpfgs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, fgname sysname, isdone bit);

INSERT INTO #tmpdbs ([dbid], [dbname], [isdone])
SELECT database_id, name, 0 FROM master.sys.databases (NOLOCK) WHERE is_read_only = 0 AND state = 0;

DECLARE @dbid int, @query VARCHAR(1000), @dbname sysname, @fgname sysname

WHILE (SELECT COUNT(id) FROM #tmpdbs WHERE isdone = 0) > 0
BEGIN
    SELECT TOP 1 @dbname = [dbname], @dbid = [dbid] FROM #tmpdbs WHERE isdone = 0

    SET @query = 'SELECT ' + CAST(@dbid AS NVARCHAR) + ', ''' + @dbname + ''', [name], 0 FROM [' + @dbname + '].sys.filegroups WHERE [type] = ''FG'' AND is_read_only = 0;'
    INSERT INTO #tmpfgs
    EXEC (@query)

    UPDATE #tmpdbs
    SET isdone = 1
    WHERE [dbid] = @dbid
END;

IF (SELECT COUNT(ID) FROM #tmpfgs) > 0
BEGIN
    WHILE (SELECT COUNT(id) FROM #tmpfgs WHERE isdone = 0) > 0
    BEGIN
        SELECT TOP 1 @dbname = [dbname], @dbid = [dbid], @fgname = fgname FROM #tmpfgs WHERE isdone = 0

        SET @query = 'ALTER DATABASE [' + @dbname + '] MODIFY FILEGROUP [' + @fgname + '] AUTOGROW_ALL_FILES;'

        PRINT @query

        UPDATE #tmpfgs
        SET isdone = 1
        WHERE [dbid] = @dbid AND fgname = @fgname
    END
END;
GO
```

## <a name="see-also"></a>참고 항목

- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-mi-current)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)
- [메모리 최적화 파일 그룹](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)

::: moniker-end
