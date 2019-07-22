---
title: CREATE DATABASE(Transact-SQL) | Microsoft Docs
description: SQL Server, Azure SQL Database, Azure SQL Data Warehouse 및 Analytics Platform System의 데이터베이스 구문 만들기
ms.custom: ''
ms.date: 03/18/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATABASE_TSQL
- DATABASE
- CONTAINMENT_TSQL
- CREATE DATABASE
- CREATE_DATABASE_TSQL
- CONTAINS_FILESTREAM_TSQL
- CONTAINS FILESTREAM
- CONTAINMENT
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server database snapshots], creating
- databases [SQL Server], creating
- model database [SQL Server], database creation
- mounted drives [SQL Server]
- CREATE DATABASE
- CREATE DATABASE statement
- file creation [SQL Server]
- creating databases
- containment
- filegroups [SQL Server], database creation
- database creation [SQL Server], CREATE DATABASE statement
- moving databases
- attaching databases [SQL Server], CREATE DATABASE...FOR ATTACH
ms.assetid: 29ddac46-7a0f-4151-bd94-75c1908c89f8
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-current||=azuresqldb-mi-current||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: cb2dc637dff24b6e3864d3c14f94ea817767de41
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060967"
---
# <a name="create-database"></a>CREATE DATABASE

새 데이터베이스를 만듭니다.

작업 중인 특정 SQL 버전에 대한 구문, 인수, 설명, 사용 권한 및 예제를 보려면 다음 탭 중 하나를 클릭합니다.

구문 표기 규칙에 대한 자세한 내용은 [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)을 참조하십시오.

## <a name="click-a-product"></a>제품을 클릭하세요.

다음 행에서 관심이 있는 제품 이름을 클릭합니다. 클릭하면 웹페이지의 여기에서 클릭한 제품에 적절한 다른 콘텐츠를 표시합니다.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

|||||
|-|-|-|-|
|**_\* SQL Server \*_** &nbsp;| [SQL Database<br />단일 데이터베이스/탄력적 풀](create-database-transact-sql.md?view=azuresqldb-current) | [SQL Database<br />관리되는 인스턴스](create-database-transact-sql.md?view=azuresqldb-mi-current) | [SQL Data<br />Warehouse](create-database-transact-sql.md?view=azure-sqldw-latest) | [Analytics Platform<br />System(PDW)](create-database-transact-sql.md?view=aps-pdw-2016) |
|||||

&nbsp;

## <a name="sql-server"></a>SQL Server

## <a name="overview"></a>개요

SQL Server에서 이 문은 새 데이터베이스 및 사용되는 파일과 해당 파일 그룹을 만듭니다. 또한 데이터베이스 스냅샷을 만드는 데 사용하거나, 데이터베이스 파일을 첨부하여 다른 데이터베이스의 분리된 파일에서 데이터베이스를 만드는 데 사용할 수도 있습니다.

## <a name="syntax"></a>구문

데이터베이스를 만듭니다.

```
CREATE DATABASE database_name
[ CONTAINMENT = { NONE | PARTIAL } ]
[ ON
      [ PRIMARY ] <filespec> [ ,...n ]
      [ , <filegroup> [ ,...n ] ]
      [ LOG ON <filespec> [ ,...n ] ]
]
[ COLLATE collation_name ]
[ WITH <option> [,...n ] ]
[;]

<option> ::=
{
      FILESTREAM ( <filestream_option> [,...n ] )
    | DEFAULT_FULLTEXT_LANGUAGE = { lcid | language_name | language_alias }
    | DEFAULT_LANGUAGE = { lcid | language_name | language_alias }
    | NESTED_TRIGGERS = { OFF | ON }
    | TRANSFORM_NOISE_WORDS = { OFF | ON}
    | TWO_DIGIT_YEAR_CUTOFF = <two_digit_year_cutoff>
    | DB_CHAINING { OFF | ON }
    | TRUSTWORTHY { OFF | ON }
    | PERSISTENT_LOG_BUFFER=ON ( DIRECTORY_NAME='<Filepath to folder on DAX formatted volume>' )
}

<filestream_option> ::=
{
      NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }
    | DIRECTORY_NAME = 'directory_name'
}

<filespec> ::=
{
(
    NAME = logical_file_name ,
    FILENAME = { 'os_file_name' | 'filestream_path' }
    [ , SIZE = size [ KB | MB | GB | TB ] ]
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB | % ] ]
)
}

<filegroup> ::=
{
FILEGROUP filegroup name [ [ CONTAINS FILESTREAM ] [ DEFAULT ] | CONTAINS MEMORY_OPTIMIZED_DATA ]
    <filespec> [ ,...n ]
}

<service_broker_option> ::=
{
    ENABLE_BROKER
  | NEW_BROKER
  | ERROR_BROKER_CONVERSATIONS
}

```

데이터베이스 연결

```
CREATE DATABASE database_name
    ON <filespec> [ ,...n ]
    FOR { { ATTACH [ WITH <attach_database_option> [ , ...n ] ] }
        | ATTACH_REBUILD_LOG }
[;]

<attach_database_option> ::=
{
      <service_broker_option>
    | RESTRICTED_USER
    | FILESTREAM ( DIRECTORY_NAME = { 'directory_name' | NULL } )
}
```

데이터베이스 스냅샷 만들기

```
CREATE DATABASE database_snapshot_name
    ON
    (
        NAME = logical_file_name,
        FILENAME = 'os_file_name'
    ) [ ,...n ]
    AS SNAPSHOT OF
[;]
```

## <a name="arguments"></a>인수

*database_name* 새 데이터베이스의 이름입니다. 데이터베이스 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유해야 하고 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다.

로그 파일에 논리적 이름을 지정하는 경우 *database_name*은 최대 128자가 될 수 있습니다. 논리적 로그 파일 이름을 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 *database_name*에 접미사를 추가하여 로그의 *logical_file_name*과 *os_file_name*을 생성합니다. 생성할 논리적 파일 이름이 128자를 넘지 않도록 *database_name*은 123자로 제한됩니다.

데이터 파일 이름을 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 *database_name*을 *logical_file_name* 및 *os_file_name*으로 사용합니다. 기본 경로는 레지스트리에서 가져옵니다. 기본 경로는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 **서버 속성(데이터베이스 설정 페이지)** 을 사용하여 변경할 수 있습니다. 기본 경로를 변경하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작해야 합니다.

CONTAINMENT = { NONE | PARTIAL }

**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

데이터베이스의 포함 상태를 지정합니다. NONE = 포함되지 않은 데이터베이스입니다. PARTIAL = 부분적으로 포함된 데이터베이스입니다.

ON     
데이터베이스의 데이터 섹션을 저장하는 데 사용하는 디스크 파일인 데이터 파일을 명시적으로 정의하도록 지정합니다. 주 파일 그룹의 데이터 파일을 정의하는 \<filespec> 항목의 쉼표로 구분된 목록을 나열할 때는 ON이 필요합니다. 주 파일 그룹의 파일 목록 다음에는 필요에 따라 사용자 파일 그룹과 해당 파일을 정의하는 쉼표로 구분된 \<filegroup> 항목의 목록이 올 수 있습니다.

PRIMARY     
연결된 \<filespec> 목록이 주 파일을 정의하도록 지정합니다. 주 파일 그룹의 \<filespec> 항목에서 지정한 첫 번째 파일이 주 파일이 됩니다. 데이터베이스에는 주 파일이 하나만 있을 수 있습니다. 자세한 내용은 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)을 참조하세요.

PRIMARY를 지정하지 않으면 CREATE DATABASE 문에 나열된 첫 번째 파일이 주 파일이 됩니다.

LOG ON     
데이터베이스 로그를 저장하는 데 사용하는 디스크 파일인 로그 파일을 명시적으로 정의하도록 지정합니다. LOG ON 다음에는 로그 파일을 정의하는 쉼표로 구분된 \<filespec> 항목의 목록이 옵니다. LOG ON을 지정하지 않은 경우에는 데이터베이스의 모든 데이터 파일 크기를 합한 값의 25% 또는 512KB 중에서 더 큰 값을 갖는 로그 파일 하나가 자동으로 만들어집니다. 이 파일은 기본 로그 파일 위치에 저장됩니다. 이 위치에 대한 자세한 내용은 [데이터 및 로그 파일의 기본 위치 보기 또는 변경 - SSMS](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)를 참조하세요.

데이터베이스 스냅샷에는 LOG ON을 지정할 수 없습니다.

COLLATE *collation_name*     
데이터베이스의 기본 데이터 정렬을 지정합니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 이 인수를 지정하지 않으면 데이터베이스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 기본 데이터 정렬이 할당됩니다. 데이터베이스 스냅샷에는 데이터 정렬 이름을 지정할 수 없습니다.

FOR ATTACH 또는 FOR ATTACH_REBUILD_LOG 절을 사용하여 데이터 정렬 이름을 지정할 수 없습니다. 연결된 데이터베이스의 데이터 정렬을 변경하는 방법은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?linkid=16419&kbid=325335)를 참조하세요.

Windows 데이터 정렬 이름 및 SQL 데이터 정렬 이름에 대한 자세한 내용은 [COLLATE](~/t-sql/statements/collations.md)를 참조하세요.

> [!NOTE]
> 포함된 데이터베이스는 포함되지 않은 데이터베이스와 다른 방식으로 데이터가 정렬됩니다. 자세한 내용은 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)을 참조하세요.

WITH \<option>      
**\<filestream_options>**

NON_TRANSACTED_ACCESS = { **OFF** | READ_ONLY | FULL } **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

데이터베이스에 대한 비트랜잭션 FILESTREAM 액세스 수준을 지정합니다.

|값|설명|
|-----------|-----------------|
|OFF|비트랜잭션 액세스는 사용할 수 없습니다.|
|READONLY|비트랜잭션 프로세스에서 이 데이터베이스의 FILESTREAM 데이터를 읽을 수 있습니다.|
|FULL|FILESTREAM FileTable에 대한 전체 비트랜잭션 액세스를 사용할 수 있습니다.|

DIRECTORY_NAME = \<directory_name>     
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

Windows 호환 디렉터리 이름입니다. 이 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 Database_Directory 이름 중에서 고유해야 합니다. 고유성 비교는 대/소문자를 구분하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬 설정과 관계가 없습니다. 데이터베이스에 FileTable을 만들기 전에 이 옵션을 설정해야 합니다.

CONTAINMENT가 PARTIAL로 설정된 경우에만 다음 옵션을 사용할 수 있습니다. CONTAINMENT가 NONE으로 설정되어 있으면 오류가 발생합니다.

- **DEFAULT_FULLTEXT_LANGUAGE = \<lcid> | \<language name> | \<language alias>**

  **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

  이 옵션에 대한 전체 설명은 [기본 전체 텍스트 언어 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md)을 참조하세요.

- **DEFAULT_LANGUAGE = \<lcid> | \<language name> | \<language alias>**

  **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

  이 옵션에 대한 전체 설명은 [기본 언어 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)을 참조하세요.

- **NESTED_TRIGGERS = { OFF | ON}**

  **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

  이 옵션에 대한 전체 설명은 [nested triggers 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)을 참조하세요.

- **TRANSFORM_NOISE_WORDS = { OFF | ON}**

  **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

  이 옵션에 대한 전체 설명은 [의미 없는 단어 변환 서버 구성 옵션](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)을 참조하세요.

- **TWO_DIGIT_YEAR_CUTOFF = { 2049 | \<any year between 1753 and 9999> }**

  연도를 나타내는 4자리 숫자입니다. 기본값은 2049입니다. 이 옵션에 대한 자세한 내용은 [두 자리 연도 구분 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 참조하세요.

- **DB_CHAINING { OFF | ON }**

  ON이 지정되면 데이터베이스가 데이터베이스 간 소유권 체인의 원본 또는 대상이 될 수 있습니다.

  OFF가 지정되면 데이터베이스가 데이터베이스 간 소유권 체인에 참여할 수 없습니다. 기본값은 OFF입니다.

  > [!IMPORTANT]
  > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 cross db ownership chaining 서버 옵션이 0(OFF)일 때 이 설정을 인식할 수 있습니다. cross db ownership chaining이 1(ON)이면 모든 사용자 데이터베이스는 이 옵션 값에 관계없이 데이터베이스 간 소유권 체인에 참여할 수 있습니다. 이 옵션은 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용하여 설정합니다.

  이 옵션을 설정하려면 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다. DB_CHAINING 옵션은 master, model, tempdb 시스템 데이터베이스에서는 설정할 수 없습니다.

- **TRUSTWORTHY { OFF | ON }**

  ON이 지정되면 뷰, 사용자 정의 함수 또는 저장 프로시저와 같이 가장 컨텍스트를 사용하는 데이터베이스 모듈이 데이터베이스 외부 리소스에 액세스할 수 있습니다.

  OFF가 지정되면 가장 컨텍스트의 데이터베이스 모듈이 데이터베이스 외부의 리소스에 액세스할 수 없습니다. 기본값은 OFF입니다.

  TRUSTWORTHY는 데이터베이스가 연결될 때마다 OFF로 설정됩니다.

  기본적으로 msdb 데이터베이스를 제외한 모든 시스템 데이터베이스는 TRUSTWORTHY가 OFF로 설정되어 있습니다. model 및 tempdb 데이터베이스에 대해서는 이 값을 변경할 수 없습니다. master 데이터베이스의 경우 TRUSTWORTHY 옵션을 ON으로 설정하지 않는 것이 좋습니다.

- **PERSISTENT_LOG_BUFFER=ON ( DIRECTORY_NAME='' )**

  이 옵션을 지정하면 트랜잭션 로그 버퍼는 저장소 클래스 메모리(NVDIMM-N 비휘발성 저장소)로 지원되는 디스크 디바이스에 있는 볼륨에서 생성되며 영구적 로그 버퍼라고도 합니다. 자세한 내용은 [스토리지 클래스 메모리를 사용하는 트랜잭션 커밋 대기 시간 가속화](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/) 를 참조하세요. **적용 대상**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 이상.

FOR ATTACH [ WITH \< attach_database_option > ]     
기존 운영 체제 파일 세트를 [연결](../../relational-databases/databases/database-detach-and-attach-sql-server.md)하여 데이터베이스를 만들도록 지정합니다. 여기에는 주 파일을 지정하는 \<filespec> 항목이 반드시 필요합니다. 또한 데이터베이스를 처음 만들었거나 마지막으로 연결했을 때 경로가 다른 파일에 대한 \<filespec> 항목이 필요합니다. 이러한 파일에는 반드시 \<filespec> 항목을 지정해야 합니다.

FOR ATTACH를 사용하려면 다음과 같은 조건을 충족해야 합니다.

- 모든 데이터 파일(MDF 및 NDF)을 사용할 수 있어야 합니다.
- 로그 파일이 여러 개 있는 경우 해당 파일을 모두 사용할 수 있어야 합니다.

읽기/쓰기 데이터베이스에 현재 사용할 수 없는 로그 파일이 하나 있고 연결 작업 이전에 사용자 또는 열린 트랜잭션 없이 데이터베이스가 종료된 경우 FOR ATTACH를 사용하면 자동으로 로그 파일이 다시 작성되고 주 파일이 업데이트됩니다. 반면에 읽기 전용 데이터베이스의 경우에는 주 파일을 업데이트할 수 없으므로 로그를 다시 작성할 수 없습니다. 따라서 사용할 수 없는 로그와 읽기 전용 데이터베이스를 연결할 때는 로그 파일 또는 FOR ATTACH 절 내의 파일을 제공해야 합니다.

> [!NOTE]
> 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 만든 데이터베이스를 이전 버전에서 연결할 수 없습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 연결 중인 데이터베이스에 속한 모든 전체 텍스트 파일이 데이터베이스에 연결됩니다. 전체 텍스트 카탈로그의 새 경로를 지정하려면 전체 텍스트 운영 체제 파일 이름을 제외한 새 위치를 지정합니다. 자세한 내용은 예 섹션을 참조하십시오.

"Directory name"이 있는 FILESTREAM 옵션을 포함하는 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 Database_Directory 이름이 고유한지 확인하라는 메시지가 표시됩니다. 고유하지 않으면 연결 작업이 실패하고 "FILESTREAM Database_Directory 이름 \<name>이(가) 이 SQL Server 인스턴스에서 고유하지 않습니다"와 같은 오류 메시지가 표시됩니다. 이 오류를 방지하려면 선택적 매개 변수 *directory_name*이 이 작업에 전달되어야 합니다.

데이터베이스 스냅샷에는 FOR ATTACH를 지정할 수 없습니다.

FOR ATTACH에 RESTRICTED_USER 옵션을 지정할 수 있습니다. RESTRICTED_USER는 db_owner 고정 데이터베이스 역할 및 dbcreator와 sysadmin 고정 서버 역할의 멤버만 데이터베이스로의 연결을 허용하지만 연결되는 수는 제한하지 않습니다. 자격이 없는 사용자의 연결 시도는 거부됩니다.

데이터베이스에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용하는 경우 다음과 같이 FOR ATTACH 절에 WITH \<service_broker_option>을 사용합니다.

\<service_broker_option>     
데이터베이스에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 배달 및 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자를 제어합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 옵션은 FOR ATTACH 절을 사용할 때만 지정할 수 있습니다.

ENABLE_BROKER    
지정된 데이터베이스에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용할 수 있도록 지정합니다. 즉, 메시지 배달이 시작되고 sys.databases 카탈로그 뷰에서 is_broker_enabled가 True로 설정됩니다. 데이터베이스에 기존 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자가 유지됩니다.

NEW_BROKER     
sys.databases와 복원된 데이터베이스 둘 다에서 새 service_broker_guid 값을 만들고 정리 작업을 통해 모든 대화 엔드포인트를 끝냅니다. 이때 Service Broker가 설정되지만 원격 대화 엔드포인트에 메시지가 전송되지 않습니다. 이전 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자를 참조하는 경로는 새 식별자로 다시 만들어야 합니다.

ERROR_BROKER_CONVERSATIONS      
데이터베이스가 연결 또는 복원되었다는 오류 메시지를 표시하고 모든 대화를 끝냅니다. Service Broker는 이 작업이 완료될 때까지 해제된 후 설정됩니다. 데이터베이스에 기존 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자가 유지됩니다.

분리되지 않고 복사된 복제 데이터베이스를 연결하는 경우에는 다음 사항을 고려합니다.

- 데이터베이스를 원래 데이터베이스와 동일한 서버 인스턴스 및 버전에 연결하는 경우에는 추가 작업이 필요하지 않습니다.
- 데이터베이스를 동일한 서버 인스턴스의 업그레이드된 버전에 연결하는 경우에는 연결 작업이 완료된 다음, [sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md)을 실행하여 복제를 업그레이드해야 합니다.
- 데이터베이스를 버전에 관계없이 다른 서버 인스턴스에 연결하는 경우에는 연결 작업이 완료된 다음, [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 실행하여 복제를 제거해야 합니다.

> [!NOTE]
> **vardecimal** 스토리지 형식으로 연결 작업을 수행할 수는 있지만 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서비스 팩 2 이상으로 업그레이드해야 합니다. vardecimal 저장소 형식을 사용하는 데이터베이스는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 수 없습니다. **vardecimal** 스토리지 형식에 대한 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하십시오.

데이터베이스가 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 처음으로 연결되거나 복원될 때 데이터베이스 마스터 키(서비스 마스터 키로 암호화됨)의 복사본은 서버에 아직 저장되지 않은 상태입니다. 데이터베이스 마스터 키를 암호 해독하려면 **OPEN MASTER KEY** 문을 사용해야 합니다. DMK를 암호 해독한 후에는 **ALTER MASTER KEY REGENERATE** 문을 사용하여 SMK(서비스 마스터 키)로 암호화된 DMK의 복사본을 서버에 프로비전함으로써 앞으로 자동 암호 해독을 사용하도록 설정할 수 있습니다. 데이터베이스가 이전 버전에서 업그레이드되지 않은 경우에는 DMK를 다시 생성해야 최신 AES 알고리즘을 사용할 수 있습니다. DMK를 다시 생성하는 방법은 [ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md)를 참조하세요. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 데 소요되는 시간은 DMK에서 보호하는 개체 수에 따라 달라집니다. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 작업은 한 번만 필요하며 키 회전 전략의 일부로 이후에 수행하는 다시 생성 작업에 영향을 주지 않습니다. 연결을 사용하여 데이터베이스를 업그레이드하는 방법은 [분리 및 연결을 사용하여 데이터베이스 업그레이드](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md)를 참조하세요.

> [!IMPORTANT]
> 출처를 알 수 없거나 신뢰할 수 없는 데이터베이스는 연결하지 않는 것이 좋습니다. 이러한 데이터베이스에 포함된 악성 코드가 의도하지 않은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 실행하거나 스키마 또는 물리적 데이터베이스 구조를 수정하여 오류가 발생할 수 있습니다. 알 수 없거나 신뢰할 수 없는 소스의 데이터베이스를 사용하기 전에 비프로덕션 서버의 데이터베이스에서 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)를 실행하여 데이터베이스에서 코드(예: 저장 프로시저 또는 다른 사용자 정의 코드)를 시험해 보세요.

> [!NOTE]
> 데이터베이스를 연결할 때 **TRUSTWORTHY** 및 **DB_CHAINING** 옵션은 영향도 주지 않습니다.

FOR ATTACH_REBUILD_LOG     
기존 운영 체제 파일 집합을 연결하여 데이터베이스를 만들도록 지정합니다. 이 옵션은 읽기/쓰기 데이터베이스로 제한됩니다. 주 파일을 지정하는 *\<filespec>* 항목이 있어야 합니다. 하나 이상의 트랜잭션 로그 파일이 없으면 로그 파일이 다시 작성됩니다. ATTACH_REBUILD_LOG는 1MB의 새 로그 파일을 자동으로 만듭니다. 이 파일은 기본 로그 파일 위치에 저장됩니다. 이 위치에 대한 자세한 내용은 [데이터 및 로그 파일의 기본 위치 보기 또는 변경 - SSMS](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)를 참조하세요.

> [!NOTE]
> 로그 파일이 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 로그 파일을 다시 작성하지 않고 해당 파일을 사용합니다.

FOR ATTACH_REBUILD_LOG를 사용하려면 다음과 같은 조건을 충족해야 합니다.

- 데이터베이스가 완전하게 종료된 상태여야 합니다.
- 모든 데이터 파일(MDF 및 NDF)을 사용할 수 있어야 합니다.

> [!IMPORTANT]
> 이 작업을 실행하면 로그 백업 체인이 끊어집니다. 따라서 작업이 완료된 후 전체 데이터베이스 백업을 수행하는 것이 좋습니다. 자세한 내용은 [BACKUP](../../t-sql/statements/backup-transact-sql.md)을 참조하세요.

일반적으로 FOR ATTACH_REBUILD_LOG는 로그 크기가 큰 읽기/쓰기 데이터베이스를 복사본이 주로 읽기 작업에만 사용되어 원본 데이터베이스에 비해 로그 공간이 덜 필요한 다른 서버에 복사할 때 사용됩니다.

데이터베이스 스냅샷에는 FOR ATTACH_REBUILD_LOG를 지정할 수 없습니다.

데이터베이스를 연결 및 분리하는 방법은 [데이터베이스 분리 및 연결](../../relational-databases/databases/database-detach-and-attach-sql-server.md)을 참조하세요.

\<filespec>     
파일 속성을 제어합니다.

NAME *logical_file_name*     
파일의 논리적 이름을 지정합니다. FOR ATTACH 절 중 하나를 지정하는 경우가 아니면 FILENAME이 지정될 때 NAME이 필요합니다. FILESTREAM 파일 그룹 이름은 PRIMARY로 지정할 수 없습니다.

*logical_file_name*     
파일 참조 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 논리적 이름입니다. *Logical_file_name*은 데이터베이스에서 고유해야 하며 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다. 이 이름은 문자 상수, 유니코드 상수, 일반 식별자 또는 구분 식별자가 될 수 있습니다.

FILENAME { **'**_os\_file\_name_**'** | **'**_filestream\_path_**'** }      
운영 체제(물리적) 파일 이름을 지정합니다.

**'** *os_file_name* **'**     
파일을 만들 때 운영 체제에서 사용한 경로와 파일 이름입니다. 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치된 로컬 서버, SAN(저장 영역 네트워크) 또는 iSCSI 기반 네트워크 중 하나의 디바이스에 있어야 합니다. 지정한 경로는 CREATE DATABASE 문을 실행하기 전에 반드시 존재해야 합니다. 자세한 내용은 주의 사항 섹션의 "데이터베이스 파일 및 파일 그룹"을 참조하십시오.

파일에 UNC 경로가 지정되면 SIZE, MAXSIZE 및 FILEGROWTH 매개 변수를 설정할 수 있습니다.

파일이 원시 파티션에 있는 경우 *os_file_name*은 기존 원시 파티션의 드라이브 문자만 지정해야 합니다. 각 원시 파티션에는 데이터 파일을 하나만 만들 수 있습니다.

파일이 읽기 전용 보조 파일이 아니거나 데이터베이스가 읽기 전용이 아니면 데이터 파일을 압축 파일 시스템에 저장하지 마십시오. 또한 로그 파일을 압축 파일 시스템에 저장하면 안 됩니다.

**'** *filestream_path* **'**      
FILENAME 파일 그룹의 경우 FILENAME은 FILESTREAM 데이터가 저장될 경로를 참조합니다. 따라서 마지막 폴더 바로 위의 경로까지 있어야 하고 마지막 폴더 자체는 있으면 안 됩니다. 예를 들어 C:\MyFiles\MyFilestreamData 경로를 지정하는 경우 ALTER DATABASE를 실행하기 전에 C:\MyFiles 경로가 있어야 하지만 MyFilestreamData 폴더는 있으면 안 됩니다.

파일 그룹과 파일(`<filespec>`)은 같은 문으로 만들어야 합니다.

SIZE 및 FILEGROWTH 속성은 FILESTREAM 파일 그룹에 적용되지 않습니다.

SIZE *size*     
파일의 크기를 지정합니다.

*os_file_name*이 UNC 경로로 지정된 경우에는 SIZE를 지정할 수 없습니다. SIZE는 FILESTREAM 파일 그룹에 적용되지 않습니다.

*크기*     
파일의 처음 크기입니다.

기본 파일에 대해 *size*를 지정하지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 model 데이터베이스의 기본 파일 크기를 사용합니다. model의 기본 크기는 8MB([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터) 또는 1MB(이전 버전)입니다. 보조 데이터 파일 또는 로그 파일을 지정하고 해당 파일의 *size*를 지정하지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 파일 크기를 8MB([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터) 또는 1MB(이전 버전)로 지정합니다. 주 파일에 지정된 크기는 최소한 model 데이터베이스의 주 파일 크기와 같아야 합니다.

KB(킬로바이트), MB(메가바이트), GB(기가바이트) 또는 TB(테라바이트) 접미사를 사용할 수 있습니다. 기본값은 MB입니다. 소수점이 포함되지 않은 정수를 지정하십시오. *Size*는 정수 값입니다. 2147483647보다 큰 값에는 더 큰 단위를 사용합니다.

MAXSIZE *max_size*     
파일이 증가할 수 있는 최대 크기를 지정합니다. *os_file_name*이 UNC 경로로 지정된 경우에는 MAXSIZE를 지정할 수 없습니다.

*max_size*     
최대 파일 크기입니다. KB, MB, GB 및 TB 접미사를 사용할 수 있습니다. 기본값은 MB입니다. 소수점이 포함되지 않은 정수를 지정하십시오. *max_size*를 지정하지 않으면 디스크가 꽉 찰 때까지 파일이 커집니다. *Max_size*는 정수 값입니다. 2147483647보다 큰 값에는 더 큰 단위를 사용합니다.

UNLIMITED    
디스크가 꽉 찰 때까지 파일 크기가 증가하도록 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 무제한 증가로 지정된 로그 파일의 최대 크기는 2TB이고 데이터 파일의 최대 크기는 16TB입니다.

> [!NOTE]
> 이 옵션이 FILESTREAM 컨테이너에 지정되면 최대 크기가 없습니다. 디스크가 꽉 찰 때까지 파일이 증가합니다.

FILEGROWTH *growth_increment*    
파일의 자동 증분을 지정합니다. 파일의 FILEGROWTH 설정은 MAXSIZE 설정을 초과할 수 없습니다. *os_file_name*이 UNC 경로로 지정된 경우에는 FILEGROWTH를 지정할 수 없습니다. FILEGROWTH는 FILESTREAM 파일 그룹에 적용되지 않습니다.

*growth_increment*    
공간이 새로 필요할 때마다 파일에 추가되는 공간 크기입니다.

이 값은 MB, KB, GB, TB 또는 %(퍼센트) 단위로 지정할 수 있습니다. MB, KB 또는 % 접미사를 붙이지 않고 숫자를 지정하면 MB가 기본값이 됩니다. %가 지정되면 증분 크기는 파일 크기 증가가 발생하는 시점에서 해당 파일 크기에 대한 특정 비율입니다. 지정한 크기는 64KB 단위로 반올림되며 최소 값은 64KB입니다.

값이 0이면 자동 증가가 해제되어 있고 추가 공간이 허용되지 않음을 나타냅니다.

FILEGROWTH를 지정하지 않은 경우 기본값은 다음과 같습니다.

|버전 옵션|기본값|
|-------------|--------------------|
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터|데이터는 64MB입니다. 로그 파일은 64MB입니다.|
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터|데이터는 1MB입니다. 로그 파일은 10%입니다.|
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이전|데이터는 10%입니다. 로그 파일은 10%입니다.|

\<filegroup>     
파일 그룹 속성을 제어합니다. 데이터베이스 스냅샷에는 파일 그룹을 지정할 수 없습니다.

FILEGROUP *filegroup_name*     
파일 그룹의 논리적 이름입니다.

*filegroup_name*     
*filegroup_name*은 데이터베이스 내에서 고유해야 하고 시스템에서 제공한 이름인 PRIMARY 및 PRIMARY_LOG일 수 없습니다. 이 이름은 문자 상수, 유니코드 상수, 일반 식별자 또는 구분 식별자가 될 수 있습니다. 이 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.

CONTAINS FILESTREAM     
파일 그룹이 FILESTREAM BLOB(Binary Large Object)를 파일 시스템에 저장하도록 지정합니다.

CONTAINS MEMORY_OPTIMIZED_DATA     

**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

파일 그룹이 memory_optimized 데이터를 파일 시스템에 저장하도록 지정합니다. 자세한 내용은 [메모리 내 OLTP - 메모리 내 최적화](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요. 데이터베이스당 MEMORY_OPTIMIZED_DATA 파일 그룹이 하나만 허용됩니다. 메모리 최적화 데이터를 저장하기 위해 파일 그룹을 만드는 코드 샘플은 [메모리 최적화 테이블 및 고유하게 컴파일된 저장 프로시저 만들기](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)를 참조하세요.

DEFAULT     
명명한 파일 그룹이 데이터베이스의 기본 파일 그룹임을 지정합니다.

*database_snapshot_name*    
새 데이터베이스 스냅샷의 이름입니다. 데이터베이스 스냅샷 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유해야 하며 식별자에 대한 규칙을 따라야 합니다. *database_snapshot_name*은 최대 128자까지 가능합니다.

ON **(** NAME **=**_logical\_file\_name_**,** FILENAME **='**_os\_file\_name_**')** [ **,**... *n* ]    
데이터베이스 스냅샷을 만들기 위해 원본 데이터베이스의 파일 목록을 지정합니다. 스냅샷이 동작하려면 모든 데이터 파일을 개별적으로 지정해야 합니다. 그러나 데이터베이스 스냅샷에는 로그 파일이 허용되지 않습니다. FILESTREAM 파일 그룹은 데이터베이스 스냅샷에서 지원되지 않습니다. FILESTREAM 데이터 파일이 CREATE DATABASE ON 절에 포함되어 있으면 문이 실패하고 오류가 발생합니다.

NAME, FILENAME 및 각 값에 대한 내용은 해당하는 \<filespec> 값의 설명을 참조하십시오.

> [!NOTE]
> 데이터베이스 스냅샷을 만들 때는 다른 \<filespec&gt; 옵션 및 PRIMARY 키워드를 사용할 수 없습니다.

AS SNAPSHOT OF *source_database_name* 만들고 있는 데이터베이스를 *source_database_name*에 지정된 원본 데이터베이스의 데이터베이스 스냅샷으로 지정합니다. 스냅샷 및 원본 데이터베이스는 같은 인스턴스에 있어야 합니다.

자세한 내용은 주의 사항 섹션의 [데이터베이스 스냅샷](#database-snapshots)을 참조하세요.

## <a name="remarks"></a>Remarks

사용자 데이터베이스를 생성, 수정 또는 삭제할 때마다 [마스터 데이터베이스](../../relational-databases/databases/master-database.md)를 백업해야 합니다.

`CREATE DATABASE` 문은 자동 커밋 모드(기본 트랜잭션 관리 모드)에서 실행되어야 하며 명시적 또는 암시적 트랜잭션에서는 허용되지 않습니다.

`CREATE DATABASE` 문 하나를 사용하여 데이터베이스 및 해당 데이터베이스를 저장하는 파일을 만들 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 다음과 같은 단계로 CREATE DATABASE 문을 구현합니다.

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [model 데이터베이스](../../relational-databases/databases/model-database.md)의 복사본을 사용하여 데이터베이스 및 해당 메타데이터를 초기화합니다.
2. 데이터베이스에 Service Broker GUID가 할당됩니다.
3. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 데이터베이스 내의 공간 사용 방법을 기록하는 내부 데이터가 포함된 페이지를 제외하고 데이터베이스의 나머지 부분을 빈 페이지로 채웁니다.

하나의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스당 최대 32,767개의 데이터베이스를 지정할 수 있습니다.

각 데이터베이스에는 해당 데이터베이스에서 특수한 작업을 수행할 수 있는 소유자가 있습니다. 소유자는 데이터베이스를 만든 사용자입니다. [sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)를 사용하여 데이터베이스 소유자를 변경할 수 있습니다.

일부 데이터베이스 기능은 파일 시스템의 기능이 있어야 데이터베이스의 모든 기능을 사용할 수 있습니다. 파일 시스템 기능 집합이 필요한 일부 기능의 예를 들면 다음과 같습니다.

- DBCC CHECKDB
- FileStream
- VSS 및 파일 스냅샷을 이용한 온라인 백업
- 데이터베이스 스냅샷 생성
- 메모리 최적화 데이터 파일 그룹

## <a name="database-files-and-filegroups"></a>데이터베이스 파일 및 파일 그룹
모든 데이터베이스에는 *주 파일*과 *트랜잭션 로그 파일*이라는 2개의 파일과 하나 이상의 파일 그룹이 있습니다. 각 데이터베이스에 최대 32,767개의 파일과 32,767개의 파일 그룹을 지정할 수 있습니다.

데이터베이스를 만들 때는 데이터베이스에서 예상되는 최대 데이터 크기를 고려하여 데이터 파일을 가능한 한 크게 만드는 것이 좋습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 성능과 안정성을 최적화하는 구성을 위해 SAN(스토리지 영역 네트워크), iSCSI 기반 네트워크 또는 로컬로 연결된 디스크에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 파일을 스토리지하는 것이 좋습니다.

## <a name="database-snapshots"></a>데이터베이스 스냅샷
`CREATE DATABASE` 문을 사용하여 *원본 데이터베이스*의 읽기 전용 정적 뷰인 *데이터베이스 스냅샷*을 만들 수 있습니다. 데이터베이스 스냅샷은 스냅샷을 만들었을 당시의 원본 데이터베이스와 트랜잭션 측면에서 일관성을 가집니다. 원본 데이터베이스 하나에 스냅샷이 여러 개 있을 수 있습니다.

> [!NOTE]
> 데이터베이스 스냅샷을 만드는 경우 `CREATE DATABASE` 문은 로그 파일, 오프라인 파일, 복원 파일 및 존재하지 않는 파일을 참조할 수 없습니다.

데이터베이스 스냅샷 만들기에 실패한 경우 해당 스냅샷은 주의 대상이 되며 삭제해야 합니다. 자세한 내용은 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)를 참조하세요.

각 스냅샷은 `DROP DATABASE`를 사용하여 삭제할 때까지 그대로 유지됩니다.

자세한 내용은 [데이터베이스 스냅샷](../../relational-databases/databases/database-snapshots-sql-server.md)을 참조하세요.

## <a name="database-options"></a>데이터베이스 옵션
데이터베이스를 만들 때마다 몇 가지 데이터베이스 옵션이 자동으로 설정됩니다. 이러한 옵션에 대한 자세한 내용은 [ALTER DATABASE SET 옵션](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.

## <a name="the-model-database-and-creating-new-databases"></a>새 데이터베이스 만들기 및 model 데이터베이스
[model 데이터베이스](../../relational-databases/databases/model-database.md)에 있는 모든 사용자 정의 개체는 새로 만든 데이터베이스에 복사됩니다. 테이블, 뷰, 저장 프로시저, 데이터 형식 등의 모든 개체를 model 데이터베이스에 추가하여 새로 만든 모든 데이터베이스에 포함할 수 있습니다.

크기 매개 변수를 추가하지 않고 `CREATE DATABASE <database_name>` 문을 지정하면 model 데이터베이스의 주 파일과 크기가 같은 주 데이터 파일이 만들어집니다.

`FOR ATTACH`를 지정하지 않은 경우 모든 새 데이터베이스는 model 데이터베이스에서 데이터베이스 옵션 설정을 상속합니다. 예를 들어 자동 축소와 같은 데이터베이스 옵션은 model 데이터베이스와 새로 만드는 모든 데이터베이스에서 **true**로 설정됩니다. model 데이터베이스에서 옵션을 변경하면 새로 만드는 모든 데이터베이스에 이러한 새 옵션 설정이 사용됩니다. 기존 데이터베이스는 model 데이터베이스 변경 내용의 영향을 받지 않습니다. CREATE DATABASE 문에 FOR ATTACH를 지정하는 경우 새 데이터베이스는 원본 데이터베이스의 데이터베이스 옵션 설정을 상속합니다.

## <a name="viewing-database-information"></a>데이터베이스 정보 보기
카탈로그 뷰, 시스템 함수 및 시스템 저장 프로시저를 사용하여 데이터베이스, 파일 및 파일 그룹에 대한 정보를 반환할 수 있습니다. 자세한 내용은 [시스템 뷰](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)를 참조하세요.

## <a name="permissions"></a>사용 권한
`CREATE DATABASE`, `CREATE ANY DATABASE` 또는 `ALTER ANY DATABASE` 권한이 필요합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디스크 사용을 제어하기 위해 일반적으로 데이터베이스를 만들 수 있는 사용 권한은 일부 로그인 계정으로 제한됩니다.

다음 예에서는 데이터베이스 사용자 Fay에게 데이터베이스를 만들 수 있는 권한을 제공합니다.

```sql
USE master;
GO
GRANT CREATE DATABASE TO [Fay];
GO
```

### <a name="permissions-on-data-and-log-files"></a>데이터 및 로그 파일에 대한 사용 권한
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 각 데이터베이스의 데이터 및 로그 파일에 특정 사용 권한이 설정됩니다. 데이터베이스에 다음 작업이 적용될 때마다 다음과 같은 사용 권한이 설정됩니다.

|||
|-|-|
|만든 날짜|새 파일을 추가하기 위해 수정됨|
|연결|백업|
|분리|복원|

이러한 사용 권한을 설정하면 누구나 액세스할 수 있는 디렉터리에 있는 파일이 실수로 변경되는 것을 방지할 수 있습니다.

> [!NOTE]
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)]에서는 데이터 및 로그 파일 사용 권한을 설정하지 않습니다.

## <a name="examples"></a>예
### <a name="a-creating-a-database-without-specifying-files"></a>1. 파일을 지정하지 않고 데이터베이스 만들기
다음 예에서는 `mytest` 데이터베이스를 만들고 해당 주 파일 및 트랜잭션 로그 파일을 만듭니다. 문에 \<filespec> 항목이 없으므로 주 데이터베이스 파일의 크기는 model 데이터베이스 주 파일의 크기와 같습니다. 트랜잭션 로그는 주 데이터 파일의 25% 크기 또는 512KB 중 큰 값으로 설정됩니다. MAXSIZE를 지정하지 않았으므로 사용 가능한 디스크 공간을 모두 채울 때까지 파일 크기가 증가할 수 있습니다. 이 예에서는 `mytest` 데이터베이스를 만들기 전에 `mytest`라는 데이터베이스(있는 경우)를 삭제하는 방법도 보여 줍니다.

```sql
USE master;
GO
IF DB_ID (N'mytest') IS NOT NULL
DROP DATABASE mytest;
GO
CREATE DATABASE mytest;
GO
-- Verify the database files and sizes
SELECT name, size, size*1.0/128 AS [Size in MBs]
FROM sys.master_files
WHERE name = N'mytest';
GO
```

### <a name="b-creating-a-database-that-specifies-the-data-and-transaction-log-files"></a>2. 데이터 파일 및 트랜잭션 로그 파일을 지정하는 데이터베이스 만들기
다음 예에서는 `Sales` 데이터베이스를 만듭니다. 주 키워드를 사용하지 않았으므로 첫 번째 파일(`Sales_dat`)이 주 파일이 됩니다. `Sales_dat` 파일의 SIZE 매개 변수에 MB 또는 KB를 지정하지 않았으므로 기본값 MB를 사용하여 할당됩니다. 사용자 데이터베이스를 생성, 수정 또는 삭제할 때마다 `Sales_log` 파일은 `MB` 매개 변수에 명시적으로 `SIZE` 접미사를 지정했으므로 메가바이트(MB)로 공간이 할당됩니다.

```sql
USE master;
GO
CREATE DATABASE Sales
ON
( NAME = Sales_dat,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\saledat.mdf',
    SIZE = 10,
    MAXSIZE = 50,
    FILEGROWTH = 5 )
LOG ON
( NAME = Sales_log,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\salelog.ldf',
    SIZE = 5MB,
    MAXSIZE = 25MB,
    FILEGROWTH = 5MB ) ;
GO
```

### <a name="c-creating-a-database-by-specifying-multiple-data-and-transaction-log-files"></a>C. 데이터 파일 및 트랜잭션 로그 파일을 여러 개 지정하여 데이터베이스 만들기
다음 예에서는 3개의 `Archive` 데이터 파일과 2개의 `100-MB` 트랜잭션 로그 파일을 가진 `100-MB` 데이터베이스를 만듭니다. 주 파일은 목록의 첫 번째 파일이며 `PRIMARY` 키워드로 명시적으로 지정되어 있습니다. 트랜잭션 로그 파일은 `LOG ON` 키워드 다음에 지정됩니다. `FILENAME` 옵션에서 파일에 사용된 확장명에 유의하십시오. 주 데이터 파일에는 `.mdf`, 보조 데이터 파일에는 `.ndf`, 트랜잭션 로그 파일에는 `.ldf`가 각각 사용됩니다. 이 예에서는 데이터베이스를 `D:` 데이터베이스와 함께 배치하는 대신 `master` 드라이브에 배치합니다.

```sql
USE master;
GO
CREATE DATABASE Archive
ON
PRIMARY
    (NAME = Arch1,
    FILENAME = 'D:\SalesData\archdat1.mdf',
    SIZE = 100MB,
    MAXSIZE = 200,
    FILEGROWTH = 20),
    ( NAME = Arch2,
    FILENAME = 'D:\SalesData\archdat2.ndf',
    SIZE = 100MB,
    MAXSIZE = 200,
    FILEGROWTH = 20),
    ( NAME = Arch3,
    FILENAME = 'D:\SalesData\archdat3.ndf',
    SIZE = 100MB,
    MAXSIZE = 200,
    FILEGROWTH = 20)
LOG ON
  (NAME = Archlog1,
    FILENAME = 'D:\SalesData\archlog1.ldf',
    SIZE = 100MB,
    MAXSIZE = 200,
    FILEGROWTH = 20),
  (NAME = Archlog2,
    FILENAME = 'D:\SalesData\archlog2.ldf',
    SIZE = 100MB,
    MAXSIZE = 200,
    FILEGROWTH = 20) ;
GO
```

### <a name="d-creating-a-database-that-has-filegroups"></a>D. 파일 그룹이 있는 데이터베이스 만들기
다음 예에서는 아래에 나열된 파일 그룹을 포함하는 `Sales` 데이터베이스를 만듭니다.

- `Spri1_dat` 및 `Spri2_dat` 파일을 포함하는 주 파일 그룹. 이러한 파일의 FILEGROWTH 증가분은 `15%`로 지정됩니다.
- `SalesGroup1` 및 `SGrp1Fi1` 파일을 포함하는 `SGrp1Fi2` 파일 그룹
- `SalesGroup2` 및 `SGrp2Fi1` 파일을 포함하는 `SGrp2Fi2` 파일 그룹

이 예에서는 성능을 향상시키기 위해 데이터 파일과 로그 파일을 서로 다른 디스크에 배치합니다.

```sql
USE master;
GO
CREATE DATABASE Sales
ON PRIMARY
( NAME = SPri1_dat,
    FILENAME = 'D:\SalesData\SPri1dat.mdf',
    SIZE = 10,
    MAXSIZE = 50,
    FILEGROWTH = 15% ),
( NAME = SPri2_dat,
    FILENAME = 'D:\SalesData\SPri2dt.ndf',
    SIZE = 10,
    MAXSIZE = 50,
    FILEGROWTH = 15% ),
FILEGROUP SalesGroup1
( NAME = SGrp1Fi1_dat,
    FILENAME = 'D:\SalesData\SG1Fi1dt.ndf',
    SIZE = 10,
    MAXSIZE = 50,
    FILEGROWTH = 5 ),
( NAME = SGrp1Fi2_dat,
    FILENAME = 'D:\SalesData\SG1Fi2dt.ndf',
    SIZE = 10,
    MAXSIZE = 50,
    FILEGROWTH = 5 ),
FILEGROUP SalesGroup2
( NAME = SGrp2Fi1_dat,
    FILENAME = 'D:\SalesData\SG2Fi1dt.ndf',
    SIZE = 10,
    MAXSIZE = 50,
    FILEGROWTH = 5 ),
( NAME = SGrp2Fi2_dat,
    FILENAME = 'D:\SalesData\SG2Fi2dt.ndf',
    SIZE = 10,
    MAXSIZE = 50,
    FILEGROWTH = 5 )
LOG ON
( NAME = Sales_log,
    FILENAME = 'E:\SalesLog\salelog.ldf',
    SIZE = 5MB,
    MAXSIZE = 25MB,
    FILEGROWTH = 5MB ) ;
GO
```

### <a name="e-attaching-a-database"></a>E. 데이터베이스 연결
다음 예에서는 예 4에서 만든 `Archive` 데이터베이스를 분리한 다음, `FOR ATTACH` 절을 사용하여 데이터베이스를 연결합니다. `Archive`는 데이터 파일과 로그 파일을 여러 개 포함하도록 정의되었습니다. 그러나 파일을 만든 후 위치를 변경하지 않았으므로 `FOR ATTACH` 절에 주 파일만 지정해야 합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 연결 중인 데이터베이스에 속한 모든 전체 텍스트 파일이 데이터베이스에 연결됩니다.

```sql
USE master;
GO
sp_detach_db Archive;
GO
CREATE DATABASE Archive
      ON (FILENAME = 'D:\SalesData\archdat1.mdf')
      FOR ATTACH ;
GO
```

### <a name="f-creating-a-database-snapshot"></a>F. 데이터베이스 스냅샷 만들기
다음 예에서는 `sales_snapshot0600` 데이터베이스 스냅샷을 만듭니다. 데이터베이스 스냅샷은 읽기 전용이므로 로그 파일을 지정할 수 없습니다. 구문에 맞게 원본 데이터베이스의 모든 파일을 지정하며 파일 그룹은 지정하지 않습니다.

이 예의 원본 데이터베이스는 예 4에서 만든 `Sales` 데이터베이스입니다.

```sql
USE master;
GO
CREATE DATABASE sales_snapshot0600 ON
    ( NAME = SPri1_dat, FILENAME = 'D:\SalesData\SPri1dat_0600.ss'),
    ( NAME = SPri2_dat, FILENAME = 'D:\SalesData\SPri2dt_0600.ss'),
    ( NAME = SGrp1Fi1_dat, FILENAME = 'D:\SalesData\SG1Fi1dt_0600.ss'),
    ( NAME = SGrp1Fi2_dat, FILENAME = 'D:\SalesData\SG1Fi2dt_0600.ss'),
    ( NAME = SGrp2Fi1_dat, FILENAME = 'D:\SalesData\SG2Fi1dt_0600.ss'),
    ( NAME = SGrp2Fi2_dat, FILENAME = 'D:\SalesData\SG2Fi2dt_0600.ss')
AS SNAPSHOT OF Sales ;
GO
```

### <a name="g-creating-a-database-and-specifying-a-collation-name-and-options"></a>G. 데이터베이스 만들기 및 데이터 정렬 이름과 옵션 지정
다음 예에서는 `MyOptionsTest` 데이터베이스를 만듭니다. 데이터 정렬 이름을 지정하고 `TRUSTYWORTHY` 및 `DB_CHAINING` 옵션을 `ON`으로 설정합니다.

```sql
USE master;
GO
IF DB_ID (N'MyOptionsTest') IS NOT NULL
DROP DATABASE MyOptionsTest;
GO
CREATE DATABASE MyOptionsTest
COLLATE French_CI_AI
WITH TRUSTWORTHY ON, DB_CHAINING ON;
GO
--Verifying collation and option settings.
SELECT name, collation_name, is_trustworthy_on, is_db_chaining_on
FROM sys.databases
WHERE name = N'MyOptionsTest';
GO
```

### <a name="h-attaching-a-full-text-catalog-that-has-been-moved"></a>H. 이동된 전체 텍스트 카탈로그 연결
다음 예에서는 `AdvWksFtCat` 전체 텍스트 카탈로그를 `AdventureWorks2012` 데이터 및 로그 파일과 연결합니다. 이 예에서는 전체 텍스트 카탈로그를 기본 위치에서 새 위치 `c:\myFTCatalogs`로 이동하고 데이터 및 로그 파일은 기본 위치에 그대로 남아 있습니다.

```sql
USE master;
GO
--Detach the AdventureWorks2012 database
sp_detach_db AdventureWorks2012;
GO
-- Physically move the full text catalog to the new location.
--Attach the AdventureWorks2012 database and specify the new location of the full-text catalog.
CREATE DATABASE AdventureWorks2012 ON
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_data.mdf'),
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_log.ldf'),
    (FILENAME = 'c:\myFTCatalogs\AdvWksFtCat')
FOR ATTACH;
GO
```

### <a name="i-creating-a-database-that-specifies-a-row-filegroup-and-two-filestream-filegroups"></a>9. 행 파일 그룹 하나와 FILESTREAM 파일 그룹 두 개를 지정하는 데이터베이스 만들기
다음 예에서는 `FileStreamDB` 데이터베이스를 만듭니다. 이 데이터베이스에는 행 파일 그룹 하나와 FILESTREAM 파일 그룹 두 개가 있습니다. 각 파일 그룹에는 다음과 같이 하나의 파일이 포함됩니다.

- `FileStreamDB_data`는 행 데이터를 포함합니다. 여기에는 기본 경로가 지정된 `FileStreamDB_data.mdf` 파일 하나가 포함됩니다.
- `FileStreamPhotos`는 FILESTREAM 데이터를 포함합니다. 여기에는 두 개의 FILESTREAM 데이터 컨테이너가 포함됩니다. 하나는 `FSPhotos`에 있는 `C:\MyFSfolder\Photos`이고 다른 하나는 `FSPhotos2`에 있는 `D:\MyFSfolder\Photos`입니다. 이 그룹은 기본 FILESTREAM 파일 그룹으로 표시됩니다.
- `FileStreamResumes`는 FILESTREAM 데이터를 포함합니다. 여기에는 `FSResumes`에 있는 FILESTREAM 데이터 컨테이너 `C:\MyFSfolder\Resumes`가 포함됩니다.

```sql
USE master;
GO
-- Get the SQL Server data path.
DECLARE @data_path nvarchar(256);
SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
                  FROM master.sys.master_files
                  WHERE database_id = 1 AND file_id = 1);

 -- Execute the CREATE DATABASE statement.
EXECUTE ('CREATE DATABASE FileStreamDB
ON PRIMARY
    (
    NAME = FileStreamDB_data
    ,FILENAME = ''' + @data_path + 'FileStreamDB_data.mdf''
    ,SIZE = 10MB
    ,MAXSIZE = 50MB
    ,FILEGROWTH = 15%
    ),
FILEGROUP FileStreamPhotos CONTAINS FILESTREAM DEFAULT
    (
    NAME = FSPhotos
    ,FILENAME = ''C:\MyFSfolder\Photos''
-- SIZE and FILEGROWTH should not be specified here.
-- If they are specified an error will be raised.
, MAXSIZE = 5000 MB
    ),
    (
      NAME = FSPhotos2
      , FILENAME = ''D:\MyFSfolder\Photos''
      , MAXSIZE = 10000 MB
     ),
FILEGROUP FileStreamResumes CONTAINS FILESTREAM
    (
    NAME = FileStreamResumes
    ,FILENAME = ''C:\MyFSfolder\Resumes''
    )
LOG ON
    (
    NAME = FileStream_log
    ,FILENAME = ''' + @data_path + 'FileStreamDB_log.ldf''
    ,SIZE = 5MB
    ,MAXSIZE = 25MB
    ,FILEGROWTH = 5MB
    )'
);
GO
```

### <a name="j-creating-a-database-that-has-a-filestream-filegroup-with-multiple-files"></a>J. 여러 파일이 포함된 FILESTREAM 파일 그룹이 있는 데이터베이스 만들기
다음 예에서는 `BlobStore1` 데이터베이스를 만듭니다. 이 데이터베이스에는 행 파일 그룹 하나와 FILESTREAM 파일 그룹 하나(`FS`)가 있습니다. FILESTREAM 파일 그룹에는 두 개의 파일(`FS1` 및 `FS2`)이 포함됩니다. 그런 다음 세 번째 파일(`FS3`)을 FILESTREAM 파일 그룹에 추가하여 데이터베이스를 변경합니다.

```sql
USE master;
GO

CREATE DATABASE [BlobStore1]
CONTAINMENT = NONE
ON PRIMARY
(
    NAME = N'BlobStore1',
    FILENAME = N'C:\BlobStore\BlobStore1.mdf',
    SIZE = 100MB,
    MAXSIZE = UNLIMITED,
    FILEGROWTH = 1MB
),
FILEGROUP [FS] CONTAINS FILESTREAM DEFAULT
(  
    NAME = N'FS1',
    FILENAME = N'C:\BlobStore\FS1',
    MAXSIZE = UNLIMITED
),
(
    NAME = N'FS2',
    FILENAME = N'C:\BlobStore\FS2',
    MAXSIZE = 100MB
)
LOG ON
(
    NAME = N'BlobStore1_log',
    FILENAME = N'C:\BlobStore\BlobStore1_log.ldf',
    SIZE = 100MB,
    MAXSIZE = 1GB,
    FILEGROWTH = 1MB
);
GO

ALTER DATABASE [BlobStore1]
ADD FILE
(
    NAME = N'FS3',
    FILENAME = N'C:\BlobStore\FS3',
    MAXSIZE = 100MB
)
TO FILEGROUP [FS];
GO
```

## <a name="see-also"></a>참고 항목

- [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)
- [데이터베이스 분리 및 연결](../../relational-databases/databases/database-detach-and-attach-sql-server.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)
- [sp_detach_db](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)
- [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)
- [데이터베이스 스냅샷](../../relational-databases/databases/database-snapshots-sql-server.md)
- [데이터베이스 파일 이동](../../relational-databases/databases/move-database-files.md)
- [데이터베이스](../../relational-databases/databases/databases.md)
- [BLOB(Binary Large Object) - Blob 데이터](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

> |||||
> |-|-|-|-|
> |[SQL Server](create-database-transact-sql.md?view=sql-server-2017)| **_\*SQL Database<br />단일 데이터베이스/탄력적 풀\*_** | [SQL Database<br />관리되는 인스턴스](create-database-transact-sql.md?view=azuresqldb-mi-current) | [SQL Data<br />Warehouse](create-database-transact-sql.md?view=azure-sqldw-latest) | [Analytics Platform<br />System(PDW)](create-database-transact-sql.md?view=aps-pdw-2016) |

&nbsp;

## <a name="azure-sql-database-single-databaseelastic-pool"></a>Azure SQL Database 단일 데이터베이스/탄력적 풀

## <a name="overview"></a>개요

[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 단일 데이터베이스/탄력적 풀에서 이 명령문은 Azure SQL Server와 함께 사용하여 단일 데이터베이스 또는 탄력적 풀의 데이터베이스를 만들 수 있습니다. 이 문을 사용하여 데이터베이스 이름, 데이터 정렬, 최대 크기, 버전, 서비스 목표 및 새 데이터베이스의 탄력적 풀(해당하는 경우)을 지정합니다. 탄력적 풀에서 데이터베이스를 만드는 데 사용할 수도 있습니다. 또한 다른 SQL Database 서버에서 데이터베이스 복사본을 만드는 데 사용할 수 있습니다.

## <a name="syntax"></a>구문

### <a name="create-a-database"></a>데이터베이스 만들기
```
CREATE DATABASE database_name [ COLLATE collation_name ]
{
  (<edition_options> [, ...n])
}
[ WITH CATALOG_COLLATION = { DATABASE_DEFAULT | SQL_Latin1_General_CP1_CI_AS }]
[;]

<edition_options> ::=
{

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 ... 1024 ... 4096 GB }
  | ( EDITION = { 'basic' | 'standard' | 'premium' | 'GeneralPurpose' | 'BusinessCritical' | 'Hyperscale' }
  | SERVICE_OBJECTIVE =
    { 'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12'
      | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_3' | 'GP_GEN4_4' | 'GP_GEN4_5' | 'GP_GEN4_6'
      | 'GP_Gen4_7' | 'GP_Gen4_8' | 'GP_Gen4_9' | 'GP_Gen4_10' | 'GP_Gen4_16' | 'GP_Gen4_24'
      | 'GP_Gen5_2' | 'GP_Gen5_4' | 'GP_Gen5_6' | 'GP_Gen5_8' | 'GP_Gen5_10' | 'GP_Gen5_12' | 'GP_Gen5_14'
      | 'GP_Gen5_16' | 'GP_Gen5_18' | 'GP_Gen5_20' | 'GP_Gen5_24' | 'GP_Gen5_32' | 'GP_Gen5_40' | 'GP_Gen5_80'
      | 'BC_Gen4_1' | 'BC_Gen4_2' | 'BC_Gen4_3' | 'BC_Gen4_4' | 'BC_Gen4_5' | 'BC_Gen4_6'
      | 'BC_Gen4_7' | 'BC_Gen4_8' | 'BC_Gen4_9' | 'BC_Gen4_10' | 'BC_Gen4_16' | 'BC_Gen4_24'
      | 'BC_Gen5_2' | 'BC_Gen5_4' | 'BC_Gen5_6' | 'BC_Gen5_8' | 'BC_Gen5_10' | 'BC_Gen5_12' | 'BC_Gen5_14'
      | 'BC_Gen5_16' | 'BC_Gen5_18' | 'BC_Gen5_20' | 'BC_Gen5_24' | 'BC_Gen5_32' | 'BC_Gen5_40' | 'BC_Gen5_80'
      | 'HS_GEN4_1' | 'HS_GEN4_2' | 'HS_GEN4_4' | 'HS_GEN4_8' | 'HS_GEN4_16' | 'HS_GEN4_24'
      | 'HS_GEN5_2' | 'HS_GEN5_4' | 'HS_GEN5_8' | 'HS_GEN5_16' | 'HS_GEN5_24' | 'HS_GEN5_32' | 'HS_GEN5_48' | 'HS_GEN5_80'
      | { ELASTIC_POOL(name = <elastic_pool_name>) } })
}
```

### <a name="copy-a-database"></a>데이터베이스 복사
```
CREATE DATABASE database_name
    AS COPY OF [source_server_name.] source_database_name
    [ ( SERVICE_OBJECTIVE =
      { 'basic' |'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12'
      | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_3' | 'GP_GEN4_4' | 'GP_GEN4_5' | 'GP_GEN4_6'
      | 'GP_Gen4_7' | 'GP_Gen4_8' | 'GP_Gen4_9' | 'GP_Gen4_10' | 'GP_Gen4_16' | 'GP_Gen4_24'
      | 'GP_Gen5_2' | 'GP_Gen5_4' | 'GP_Gen5_6' | 'GP_Gen5_8' | 'GP_Gen5_10' | 'GP_Gen5_12' | 'GP_Gen5_14'
      | 'GP_Gen5_16' | 'GP_Gen5_18' | 'GP_Gen5_20' | 'GP_Gen5_24' | 'GP_Gen5_32' | 'GP_Gen5_40' | 'GP_Gen5_80'
      | 'BC_Gen4_1' | 'BC_Gen4_2' | 'BC_Gen4_3' | 'BC_Gen4_4' | 'BC_Gen4_5' | 'BC_Gen4_6'
      | 'BC_Gen4_7' | 'BC_Gen4_8' | 'BC_Gen4_9' | 'BC_Gen4_10' | 'BC_Gen4_16' | 'BC_Gen4_24'
      | 'BC_Gen5_2' | 'BC_Gen5_4' | 'BC_Gen5_6' | 'BC_Gen5_8' | 'BC_Gen5_10' | 'BC_Gen5_12' | 'BC_Gen5_14'
      | 'BC_Gen5_16' | 'BC_Gen5_18' | 'BC_Gen5_20' | 'BC_Gen5_24' | 'BC_Gen5_32' | 'BC_Gen5_40' | 'BC_Gen5_80'
      | 'HS_GEN4_1' | 'HS_GEN4_2' | 'HS_GEN4_4' | 'HS_GEN4_8' | 'HS_GEN4_16' | 'HS_GEN4_24'
      | 'HS_GEN5_2' | 'HS_GEN5_4' | 'HS_GEN5_8' | 'HS_GEN5_16' | 'HS_GEN5_24' | 'HS_GEN5_32' | 'HS_GEN5_48' | 'HS_GEN5_80'
      | { ELASTIC_POOL(name = <elastic_pool_name>) } )
   ]
[;]
```

## <a name="arguments"></a>인수

*database_name*     
새 데이터베이스의 이름입니다. 이 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 고유해야 하며 식별자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 규칙을 따라야 합니다. 자세한 내용은 [식별자](https://go.microsoft.com/fwlink/p/?LinkId=180386)를 참조하세요.

*Collation_name*     
데이터베이스의 기본 데이터 정렬을 지정합니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 지정되지 않는 경우 해당 데이터베이스가 기본 데이터 정렬 SQL_Latin1_General_CP1_CI_AS에 할당됩니다.

Windows 및 SQL 데이터 정렬 이름에 대한 자세한 내용은 [COLLATE(Transact-SQL)](../../t-sql/statements/collations.md)를 참조하세요.

CATALOG_COLLATION      
메타데이터 카탈로그의 기본 데이터 정렬을 지정합니다. *DATABASE_DEFAULT*는 시스템 뷰와 시스템 테이블에 사용된 메타데이터 카탈로그가 데이터베이스의 기본 데이터 정렬과 일치하게 데이터를 정렬하도록 지정합니다.  이것은 SQL Server에서 발견되는 동작입니다.

*SQL_Latin1_General_CP1_CI_AS*는 시스템 뷰와 테이블에 사용된 메타데이터 카탈로그가 고정된 SQL_Latin1_General_CP1_CI_AS 데이터 정렬로 정렬되도록 지정합니다. 이것이 지정되지 않은 경우 Azure SQL Database의 기본 설정입니다.

버전     
데이터베이스의 서비스 계층을 지정합니다.

단일 데이터베이스/탄력적 풀의 단일 및 풀링된 데이터베이스입니다. 사용 가능한 값은 ‘기본’, ‘표준’, ‘프리미엄’, ‘GeneralPurpose’, ‘BusinessCritical’ 및 ‘Hyperscale’입니다.

MAXSIZE     
데이터베이스의 최대 크기를 지정합니다. MAXSIZE는 지정된 EDITION(서비스 계층)에 대해 유효해야 합니다. 지원되는 MAXSIZE 값 및 서비스 계층의 기본값(D)은 다음과 같습니다.

> [!NOTE]
> **MAXSIZE** 인수는 하이퍼스케일 서비스 계층의 단일 데이터베이스에 적용되지 않습니다. 하이퍼스케일 계층 데이터베이스는 필요에 따라 100TB까지 증가합니다. SQL Database 서비스는 스토리지를 자동으로 추가하므로 최대 크기를 설정할 필요가 없습니다.

**SQL Database 서버의 단일 및 풀링된 데이터베이스에 대한 DTU 기반 모델**

|**MAXSIZE**|**기본**|**S0-S2**|**S3-S12**|**P1-P6**| **P11-P15** |
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|
|100MB|√|√|√|√|√|
|250MB|√|√|√|√|√|
|500MB|√|√|√|√|√|
|1GB|√|√|√|√|√|
|2GB|√ (D)|√|√|√|√|
|5GB|해당 사항 없음|√|√|√|√|
|10GB|해당 사항 없음|√|√|√|√|
|20GB|해당 사항 없음|√|√|√|√|
|30GB|해당 사항 없음|√|√|√|√|
|40GB|해당 사항 없음|√|√|√|√|
|50GB|해당 사항 없음|√|√|√|√|
|100GB|해당 사항 없음|√|√|√|√|
|150GB|해당 사항 없음|√|√|√|√|
|200GB|해당 사항 없음|√|√|√|√|
|250GB|해당 사항 없음|√ (D)|√ (D)|√|√|
|300GB|해당 사항 없음|해당 사항 없음|√|√|√|
|400GB|해당 사항 없음|해당 사항 없음|√|√|√|
|500GB|해당 사항 없음|해당 사항 없음|√|√ (D)|√|
|750GB|해당 사항 없음|해당 사항 없음|√|√|√|
|1024GB|해당 사항 없음|해당 사항 없음|√|√|√ (D)|
|1024GB에서 최대 4096GB(256 GB*로 증분) |해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|√|√|

\* P11과 P15는 기본 크기인 1024를 사용하여 MAXSIZE를 최대 4TB까지 허용합니다. P11 및 P15는 추가 비용 없이 최대 4TB가 포함된 스토리지를 사용할 수 있습니다. 프리미엄 계층에서 1TB 초과 MAXSIZE는 현재 다음 지역에서 사용할 수 있습니다. 미국 동부2, 미국 서부, 미국 버지니아 주 정부, 유럽 서부, 독일 중부, 동남 아시아, 일본 동부, 오스트레일리아 동부, 캐나다 중부 및 캐나다 동부. DTU 기반 모델에 대한 리소스 제한에 대한 자세한 내용은 [DTU 기반 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)을 참조하세요.

DTU 기반 모델에 대한 MAXSIZE 값은 지정된 경우 지정된 서비스 계층에 대한 위의 표에 표시된 유효한 값이어야 합니다.

**vCore 기반 모델**

**범용 서비스 계층 - 4세대 컴퓨팅 플랫폼(1부)**

|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_3|GP_Gen4_4|GP_Gen4_5|GP_Gen4_6|
|:----- | ------: |-------: |-------: |-------: |-------: |--------:|
|최대 데이터 크기(GB)|1024|1024|1024|1536|1536|1536|

**범용 서비스 계층 - 4세대 컴퓨팅 플랫폼(2부)**

|MAXSIZE|GP_Gen4_7|GP_Gen4_8|GP_Gen4_9|GP_Gen4_10|GP_Gen4_16|GP_Gen4_24|
|:----- | ------: |-------: |-------: |-------: |-------: |--------:|
|최대 데이터 크기(GB)|1536|3072|3072|3072|4096|4096|

**범용 서비스 계층 - 5세대 컴퓨팅 플랫폼(1부)**

|MAXSIZE|GP_Gen5_2|GP_Gen5_4|GP_Gen5_6|GP_Gen5_8|GP_Gen5_10|GP_Gen5_12|GP_Gen5_14|
|:----- | ------: |-------: |-------: |-------: |--------: |---------:|--------: |
|최대 데이터 크기(GB)|1024|1024|1024|1536|1536|1536|1536|

**범용 서비스 계층 - 5세대 컴퓨팅 플랫폼(2부)**

|MAXSIZE|GP_Gen5_16|GP_Gen5_18|GP_Gen5_20|GP_Gen5_24|GP_Gen5_32|GP_Gen5_40|GP_Gen5_80|
|:----- | ------: |-------: |-------: |-------: |--------: |---------:|--------: |
|최대 데이터 크기(GB)|3072|3072|3072|4096|4096|4096|4096|

**중요 비즈니스용 서비스 계층 - 4세대 컴퓨팅 플랫폼(1부)**

|성능 수준|BC_Gen4_1|BC_Gen4_2|BC_Gen4_3|BC_Gen4_4|BC_Gen4_5|BC_Gen4_6|
|:--------------- | ------: |-------: |-------: |-------: |-------: |-------: |
|최대 데이터 크기(GB)|1024|1024|1024|1024|1024|1024|

**중요 비즈니스용 서비스 계층 - 4세대 컴퓨팅 플랫폼(2부)**

|성능 수준|BC_Gen4_7|BC_Gen4_8|BC_Gen4_9|BC_Gen4_10|BC_Gen4_16|BC_Gen4_24|
|:--------------- | ------: |-------: |-------: |--------: |--------: |--------: |
|최대 데이터 크기(GB)|1024|1024|1024|1024|1024|1024|

**중요 비즈니스용 서비스 계층 - 5세대 컴퓨팅 플랫폼(1부)**

|MAXSIZE|BC_Gen5_2|BC_Gen5_4|BC_Gen5_6|BC_Gen5_8|BC_Gen5_10|BC_Gen5_12|BC_Gen5_14|
|:----- | ------: |-------: |-------: |-------: |---------: |--------:|--------: |
|최대 데이터 크기(GB)|1024|1024|1024|1536|1536|1536|1536|

**중요 비즈니스용 서비스 계층 - 5세대 컴퓨팅 플랫폼(2부)**

|MAXSIZE|BC_Gen5_16|BC_Gen5_18|BC_Gen5_20|BC_Gen5_24|BC_Gen5_32|BC_Gen5_40|BC_Gen5_80|
|:----- | -------: |--------: |--------: |--------: |--------: |---------:|--------: |
|최대 데이터 크기(GB)|3072|3072|3072|4096|4096|4096|4096|

vCore 모델을 사용할 때 `MAXSIZE` 값을 설정하지 않으면 기본값은 32GB입니다. vCore 기반 모델에 대한 리소스 제한에 대한 자세한 내용은 [vCore 기반 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)을 참조하세요.

MAXSIZE 및 EDITION 인수에는 다음과 같은 규칙이 적용됩니다.

- EDITION이 지정되었지만 MAXSIZE가 지정되지 않은 경우 해당 버전에 대한 기본값이 사용됩니다. 예를 들어 EDITION이 Standard로 설정되었고 MAXSIZE가 지정되지 않았으면 MAXSIZE가 자동으로 250MB로 설정됩니다.
- MAXSIZE 또는 EDITION을 모두 지정하지 않으면 EDITION이 General Purpose로 설정되고, MAXSIZE는 32GB로 설정됩니다.

SERVICE_OBJECTIVE     
- **단일 및 풀링된 데이터베이스**

  - 성능 수준을 지정합니다. 서비스 목표의 사용 가능한 값은 `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_3`, `GP_GEN4_4`, `GP_GEN4_5`, `GP_GEN4_6`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_9`, `GP_GEN4_10`, `GP_GEN4_16`, `GP_GEN4_24`, `BC_GEN4_1`, `BC_GEN4_2`, `BC_GEN4_3`, `BC_GEN4_4`, `BC_GEN4_5`, `BC_GEN4_6`, `BC_GEN4_7`, `BC_GEN4_8`, `BC_GEN4_9`, `BC_GEN4_10`, `BC_GEN4_16`, `BC_GEN4_24`, `GP_Gen5_2`, `GP_Gen5_4`, `GP_Gen5_6`, `GP_Gen5_8`, `GP_Gen5_10`, `GP_Gen5_12`, `GP_Gen5_14`, `GP_Gen5_16`, `GP_Gen5_18`, `GP_Gen5_20`, `GP_Gen5_24`, `GP_Gen5_32`, `GP_Gen5_40`, `GP_Gen5_80`, `BC_Gen5_2`, `BC_Gen5_4`, `BC_Gen5_6`, `BC_Gen5_8`, `BC_Gen5_10`, `BC_Gen5_12`, `BC_Gen5_14`, `BC_Gen5_16`, `BC_Gen5_18`, `BC_Gen5_20`, `BC_Gen5_24`, `BC_Gen5_32`,`BC_Gen5_40`, `BC_Gen5_80`입니다.

  - **하이퍼스케일 서비스 계층의 단일 데이터베이스인 경우**

  성능 수준을 지정합니다. 서비스 목표의 사용 가능한 값은 `HS_GEN4_1` `HS_GEN4_2` `HS_GEN4_4` `HS_GEN4_8` `HS_GEN4_16`, `HS_GEN4_24`, `HS_Gen5_2`, `HS_Gen5_4`, `HS_Gen5_8`, `HS_Gen5_16`, `HS_Gen5_24`, `HS_Gen5_32`, `HS_Gen5_48`, `HS_Gen5_80`입니다.

서비스 목표 설명과 크기, 버전 및 서비스 목표 조합 등의 정보에 대한 자세한 내용은 [Azure SQL Database 서비스 계층](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers)을 참조하세요. 지정된 SERVICE_OBJECTIVE를 EDITION에서 지원하지 않는 경우 오류가 표시됩니다. SERVICE_OBJECTIVE 값을 한 계층에서 다른 계층으로 변경하려면(예: S1에서 P1로 변경), EDITION 값도 변경해야 합니다. 서비스 목표 설명과 크기, 버전 및 서비스 목표 조합 등의 정보에 대한 자세한 내용은 [Azure SQL Database 서비스 계층 및 성능 수준](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) 및 [DTU 기반 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) 및 [vCore 기반 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)을 참조하세요. PRS 서비스 목표에 대한 지원이 제거되었습니다. 질문에 대해서는, 이메일 별칭(premium-rs@microsoft.com)을 사용하세요.

ELASTIC_POOL(name = \<elastic_pool_name>)      
**적용 대상:** 단일 및 풀링된 데이터베이스만. 하이퍼스케일 서비스 계층의 데이터베이스에는 적용되지 않습니다.
탄력적 데이터베이스 풀에서 새 데이터베이스를 만들려면 데이터베이스의 SERVICE_OBJECTIVE를 ELASTIC_POOL로 설정하고 풀의 이름을 제공합니다. 자세한 내용은 [SQL Database 탄력적 풀 만들기 및 관리](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)를 참조하세요.

AS COPY OF [source_server_name.]source_database_name      
**적용 대상:** 단일 및 풀링된 데이터베이스만.
동일한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버 또는 다른 서버에 데이터베이스를 복사하기 위한 것입니다.

*source_server_name*      
원본 데이터베이스가 위치한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버의 이름입니다. 이 매개 변수는 원본 데이터베이스와 대상 데이터베이스가 동일한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 있을 때 선택할 수 있습니다.

> [!NOTE]
> `AS COPY OF` 인수는 정규화된 고유 도메인 이름을 지원하지 않습니다. 즉, 서버의 정규화된 도메인 이름은 `serverName.database.windows.net`이며, 데이터베이스 복사 중 `serverName`만 사용합니다.

*source_database_name*

복사할 데이터베이스의 이름입니다.

## <a name="remarks"></a>Remarks
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 데이터베이스에는 데이터베이스가 만들어질 때 설정된 몇 가지 기본 설정이 있습니다. 이러한 기본 설정에 대한 자세한 내용은 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)의 값 목록을 참조하세요.

`MAXSIZE`는 데이터베이스의 크기를 제한하는 기능을 제공합니다. 데이터베이스 크기가 `MAXSIZE`에 도달하면 40544 오류 코드가 나타납니다. 이 경우, 데이터를 삽입 또는 업데이트하거나 새 개체(예: 테이블, 저장된 프로시저, 뷰 및 함수)를 만들 수 없습니다. 그러나 데이터 읽기 및 삭제, 테이블 자르기, 테이블 및 인덱스 삭제, 인덱스 다시 작성은 가능합니다. 그런 다음, `MAXSIZE`를 현재 데이터베이스 크기보다 큰 값으로 업데이트하거나 일부 데이터를 삭제하여 스토리지 공간을 비울 수 있습니다. 새 데이터 삽입까지 최대 15분을 지연시킬 수 있습니다.

나중에 크기, 버전 또는 서비스 목표 값을 변경하려면, [ALTER DATABASE - Azure SQL Database](../../t-sql/statements/alter-database-transact-sql.md?view=azuresqldb-currentls)를 사용합니다.

`CATALOG_COLLATION` 인수는 데이터베이스를 생성하는 동안에만 사용할 수 있습니다.

## <a name="database-copies"></a>데이터베이스 복사본

**적용 대상:** 단일 및 풀링된 데이터베이스만.

`CREATE DATABASE` 문을 사용한 데이터베이스 복사는 비동기 작업입니다. 따라서 전체 복사 프로세스가 끝날 때까지 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 연결할 필요가 없습니다. `CREATE DATABASE` 문은 sys.databases에서 항목을 만든 후 데이터베이스 복사 작업이 완료되기 전에 사용자에게 컨트롤을 반환합니다. 즉, 데이터베이스 복사가 진행 중인 동안에 `CREATE DATABASE` 문을 반환합니다.

- [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 서버에서 복사 프로세스 모니터링: [dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)의 `percentage_complete` 또는 `replication_state_desc` 열 또는 **sys.databases** 보기의 `state` 열을 쿼리합니다. 데이터베이스 복사를 포함해서 데이터베이스 작업의 상태를 반환하는 것뿐만 아니라 [ sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) 보기도 사용할 수 있습니다.

복사 프로세스가 완료되면 트랜잭션에서 대상 데이터베이스가 원본 데이터베이스와 일치하게 됩니다.

`AS COPY OF` 인수를 사용할 때는 다음 구문 및 의미 체계 규칙에 따라야 합니다.

- 원본 서버 이름과 복사 대상 서버의 이름은 서로 같아도 되고 달라도 됩니다. 이름이 동일한 경우 이 매개 변수는 선택적으로, 현재 세션의 서버 컨텍스트가 기본값으로 사용됩니다.
- 원본 및 대상 데이터베이스 이름은 고유하게 지정해야 하며 식별자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 규칙을 따라야 합니다. 자세한 내용은 [식별자](https://go.microsoft.com/fwlink/p/?LinkId=180386)를 참조하세요.
- `CREATE DATABASE` 문은 새 데이터베이스가 만들어질 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버의 master 데이터베이스 컨텍스트 내에서 실행되어야 합니다.
- 복사를 마친 뒤에는 대상 데이터베이스를 독립적인 데이터베이스로 관리해야 합니다. 원본 데이터베이스와 별도로 새 데이터베이스에 대해 `ALTER DATABASE` 및 `DROP DATABASE` 문을 실행할 수 있습니다. 또한 새 데이터베이스를 다른 새 데이터베이스에 복사할 수 있습니다.
- 데이터베이스 복사가 진행 중인 동안에도 계속해서 원본 데이터베이스에 액세스할 수 있습니다.

자세한 내용은 [Transact-SQL을 사용하여 Azure SQL 데이터베이스의 복사본 만들기](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/)를 참조하세요.

## <a name="permissions"></a>사용 권한
데이터베이스를 만들려면 로그인은 다음 중 하나여야 합니다.

- 서버 수준 보안 주체 로그인
- 로컬 Azure SQL Server에 대한 Azure AD 관리자
- 로그인은 `dbmanager` 데이터베이스 역할의 멤버입니다.

**`CREATE DATABASE ... AS COPY OF` 구문 사용 관련 추가 요구 사항:** 로컬 서버에 문을 실행하는 로그인은 적어도 `db_owner` 원본 서버에 있어야 합니다. 로그인이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 기반으로 하는 경우, 로컬 서버의 문을 실행하는 로그인에는 동일한 이름과 암호를 사용하여 원본 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에서 일치하는 로그온이 있어야 합니다.

## <a name="examples"></a>예

### <a name="simple-example"></a>간단한 예
데이터베이스를 만드는 간단한 예

```sql
CREATE DATABASE TestDB1;
```

### <a name="simple-example-with-edition"></a>에디션을 사용하는 간단한 예
범용 데이터베이스를 만드는 간단한 예제

```sql
CREATE DATABASE TestDB2
( EDITION = 'GeneralPurpose' );
```

### <a name="example-with-additional-options"></a>추가 옵션이 있는 예
여러 옵션을 사용하는 예

```sql
CREATE DATABASE hito
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS
( MAXSIZE = 500 MB, EDITION = 'GeneralPurpose', SERVICE_OBJECTIVE = 'GP_GEN4_8' ) ;
```

### <a name="creating-a-copy"></a>복사본 만들기
데이터베이스의 복사본을 만드는 예

**적용 대상:** 단일 및 풀링된 데이터베이스만.

```sql
CREATE DATABASE escuela
AS COPY OF school;
```

### <a name="creating-a-database-in-an-elastic-pool"></a>탄력적 풀에 데이터베이스 만들기
S3M100이라는 풀에 새 데이터베이스를 만듭니다.

**적용 대상:** 단일 및 풀링된 데이터베이스만.

```sql
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;
```

### <a name="creating-a-copy-of-a-database-on-another-server"></a>다른 서버에서 데이터베이스 복사본 만들기
다음 예에서는 단일 데이터베이스의 P2 성능 수준에 db_copy라는 이름의 db_original 데이터베이스의 복사본을 만듭니다. 이것은 db_original이 단일 데이터베이스의 탄력적 풀 또는 성능 수준에 관계없이 적용됩니다.

**적용 대상:** 단일 및 풀링된 데이터베이스만.

```sql
CREATE DATABASE db_copy
  AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' );
```

다음 예에서는 ep1이라는 이름의 탄력적 풀에 db_copy라는 이름의 db_original 데이터베이스의 복사본을 만듭니다. 이것은 db_original이 단일 데이터베이스의 탄력적 풀 또는 성능 수준에 관계없이 적용됩니다. Db_original이 다른 이름을 가진 탄력적 풀에 있으면 db_copy는 여전히 ep1에 생성됩니다.

**적용 대상:** 단일 및 풀링된 데이터베이스만.

```sql
CREATE DATABASE db_copy
  AS COPY OF ozabzw7545.db_original
  (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;
```

### <a name="create-database-with-specified-catalog-collation-value"></a>지정된 카탈로그 데이터 정렬 값을 사용하여 데이터베이스 만들기
다음 예에서는 카탈로그 데이터 정렬을 데이터베이스 데이터 생성 중에 DATABASE_DEFAULT로 설정하며, 카탈로그 데이터 정렬을 데이터베이스 데이터 정렬과 동일하게 설정합니다.

```sql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140 (MAXSIZE = 100 MB, EDITION = 'basic')
  WITH CATALOG_COLLATION = DATABASE_DEFAULT
```

## <a name="see-also"></a>관련 항목:
- [sys.dm_database_copies - Azure SQL Database](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)
- [ALTER DATABASE - Azure SQL Database](alter-database-transact-sql.md?view=azuresqldb-currentls)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |-|-|-|-|
> |[SQL Server](create-database-transact-sql.md?view=sql-server-2017)| [SQL Database<br />단일 데이터베이스/탄력적 풀](create-database-transact-sql.md?view=azuresqldb-current)| **_\*SQL Database<br />관리되는 인스턴스\*_** | [SQL Data<br />Warehouse](create-database-transact-sql.md?view=azure-sqldw-latest) | [Analytics Platform<br />System(PDW)](create-database-transact-sql.md?view=aps-pdw-2016) |

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Azure SQL Database Managed Instance

## <a name="overview"></a>개요
Azure SQL Database Managed Instance에서 이 문은 데이터베이스를 만드는 데 사용됩니다. 관리되는 인스턴스에서 데이터베이스를 만들 때 데이터베이스 이름 및 데이터 정렬을 지정합니다.

## <a name="syntax"></a>구문
```
CREATE DATABASE database_name [ COLLATE collation_name ]
[;]
```

> [!IMPORTANT]
> 관리되는 인스턴스에서 데이터베이스에 대한 파일을 추가하거나 포함을 설정하려면 [ALTER DATABASE](alter-database-transact-sql.md?view=sqlallproducts-allversions&tabs=sqldbmi) 문을 사용합니다.

## <a name="arguments"></a>인수

*database_name*       
새 데이터베이스의 이름입니다. 이 이름은 SQL Server에서 고유해야 하며 식별자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 규칙을 따라야 합니다. 자세한 내용은 [식별자](https://go.microsoft.com/fwlink/p/?LinkId=180386)를 참조하세요.

*Collation_name*      
데이터베이스의 기본 데이터 정렬을 지정합니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 지정되지 않는 경우 해당 데이터베이스가 기본 데이터 정렬 SQL_Latin1_General_CP1_CI_AS에 할당됩니다.

Windows 및 SQL 데이터 정렬 이름에 대한 자세한 내용은 [COLLATE(Transact-SQL)](../../t-sql/statements/collations.md)를 참조하세요.

## <a name="remarks"></a>Remarks
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 데이터베이스에는 데이터베이스가 만들어질 때 설정된 몇 가지 기본 설정이 있습니다. 이러한 기본 설정에 대한 자세한 내용은 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)의 값 목록을 참조하세요.

> [!IMPORTANT]
> `CREATE DATABASE` 문은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리의 유일한 문이어야 합니다.

다음은 `CREATE DATABASE` 제한 사항입니다.

- 파일 및 파일 그룹을 정의할 수 없습니다.
- `WITH` 옵션이 지원되지 않습니다.

  > [!TIP]
  > 해결 방법으로 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md?view=azuresqldb-mi-current)를 `CREATE DATABASE` 뒤에 사용하여 데이터베이스 옵션을 설정하고 파일을 추가합니다.

## <a name="permissions"></a>사용 권한
데이터베이스를 만들려면 로그인은 다음 중 하나여야 합니다.

- 서버 수준 보안 주체 로그인
- 로컬 Azure SQL Server에 대한 Azure AD 관리자
- 로그인은 `dbcreator` 데이터베이스 역할의 멤버입니다.

## <a name="examples"></a>예

### <a name="simple-example"></a>간단한 예
데이터베이스를 만드는 간단한 예

```sql
CREATE DATABASE TestDB1;
```

## <a name="see-also"></a>관련 항목:

[ALTER DATABASE](alter-database-transact-sql.md?view=azuresqldb-mi-current) 참조

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> |||||
> |-|-|-|-|
> |[SQL Server](create-database-transact-sql.md?view=sql-server-2017)| [SQL Database<br />단일 데이터베이스/탄력적 풀](create-database-transact-sql.md?view=azuresqldb-current)| [SQL Database<br />관리되는 인스턴스](create-database-transact-sql.md?view=azuresqldb-mi-current)| **_\* SQL Data<br />Warehouse \*_**| [Analytics Platform<br />System(PDW)](create-database-transact-sql.md?view=aps-pdw-2016) |

&nbsp;

## <a name="azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스

## <a name="overview"></a>개요
Azure SQL Data Warehouse에서 이 문을 Azure SQL Database 서버와 함께 사용하여 SQL Data Warehouse 데이터베이스를 만들 수 있습니다. 이 문을 사용하여 데이터베이스 이름, 데이터 정렬, 최대 크기, 버전 및 서비스 목표를 지정합니다.

## <a name="syntax"></a>구문
```
CREATE DATABASE database_name [ COLLATE collation_name ]
(
    [ MAXSIZE = {
          250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720
        | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400
        | 153600 | 204800 | 245760
      } GB ,
    ]
    EDITION = 'datawarehouse',
    SERVICE_OBJECTIVE = {
         'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600'
        | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000'
        |'DW100c' | 'DW200c' | 'DW300c' | 'DW400c' | 'DW500c'
        | 'DW1000c' | 'DW1500c' | 'DW2000c' | 'DW2500c' | 'DW3000c' | 'DW5000c'
        | 'DW6000c' | 'DW7500c' | 'DW10000c' | 'DW15000c' | 'DW30000c'
    }
)
[;]
```

## <a name="arguments"></a>인수

*database_name*       
새 데이터베이스의 이름입니다. 이 이름은 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 데이터베이스 및 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 데이터베이스를 모두 호스트할 수 있고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자에 대한 규칙을 준수할 수 있는 SQL 서버에서 고유해야 합니다. 자세한 내용은 [식별자](https://go.microsoft.com/fwlink/p/?LinkId=180386)를 참조하세요.

*collation_name*       
데이터베이스의 기본 데이터 정렬을 지정합니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 지정되지 않는 경우 해당 데이터베이스가 기본 데이터 정렬 SQL_Latin1_General_CP1_CI_AS에 할당됩니다.

Windows 및 SQL 데이터 정렬 이름에 대한 자세한 내용은 [COLLATE(Transact-SQL)](https://msdn.microsoft.com/library/ms184391.aspx)를 참조하세요.

*EDITION*     
데이터베이스의 서비스 계층을 지정합니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]의 경우 'datawarehouse'를 사용합니다.

*MAXSIZE*      
기본값은 245,760GB(240TB)입니다.

**적용 대상:** Compute Gen1에 최적화됨

데이터베이스의 최대 허용 크기입니다. 데이터베이스는 MAXSIZE 이상으로 커질 수 없습니다.

**적용 대상:** Compute Gen2에 최적화됨

데이터베이스의 rowstore 데이터에 허용되는 최대 크기입니다. Rowstore 테이블, columnstore 인덱스의 deltastore 또는 클러스터형 columnstore 인덱스의 비클러스터형 인덱스에 저장된 데이터는 MAXSIZE보다 커질 수 없습니다. columnstore 형식으로 압축된 데이터는 크기 제한이 없으며 MAXSIZE에 의해 제한되지 않습니다.

SERVICE_OBJECTIVE     
성능 수준을 지정합니다. SQL Data Warehouse의 서비스 목표에 대한 자세한 내용은 [DWU(데이터 웨어하우스 단위)](https://docs.microsoft.com/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu)를 참조하세요.

## <a name="general-remarks"></a>일반적인 주의 사항
[DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)를 사용하여 데이터베이스 속성을 확인합니다.

나중에 최대 크기, 또는 서비스 목표 값을 변경하려면 [ALTER DATABASE - Azure SQL Data Warehouse](../../t-sql/statements/alter-database-transact-sql.md?view=aps-pdw-2016-au7)를 사용합니다.

SQL Data Warehouse가 COMPATIBILITY_LEVEL 130으로 설정되어 있으며 변경할 수 없습니다. 자세한 내용은 [Azure SQL Database의 호환성 수준 130으로 향상된 쿼리 성능](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)을 참조하세요.

## <a name="permissions"></a>사용 권한
필요한 권한

- 프로비전 프로세스에 의해 생성된 서버 수준 보안 주체 로그인 또는
- `dbmanager` 데이터 베이스 역할의 멤버

## <a name="error-handling"></a>오류 처리

데이터베이스 크기가 MAXSIZE에 도달하면 40544 오류 코드가 나타납니다. 이 경우, 데이터를 삽입 및 업데이트하거나 새 개체(예: 테이블, 저장된 프로시저, 뷰 및 함수)를 만들 수 없습니다. 데이터 읽기 및 삭제, 테이블 자르기, 테이블 및 인덱스 삭제 및 인덱스 다시 작성은 여전히 가능합니다. 그런 다음 MAXSIZE를 현재 데이터베이스 크기보다 큰 값으로 업데이트하거나 일부 데이터를 삭제하여 저장소 공간을 비울 수 있습니다. 새 데이터 삽입까지 최대 15분을 지연시킬 수 있습니다.

## <a name="limitations-and-restrictions"></a>제한 사항

새 데이터베이스를 만들려면 master 데이터베이스에 연결해야 합니다.

`CREATE DATABASE` 문은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리의 유일한 문이어야 합니다.

데이터베이스를 만든 후에는 데이터베이스 데이터 정렬을 변경할 수 없습니다.

## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 

### <a name="a-simple-example"></a>1. 간단한 예
데이터 웨어하우스 데이터베이스를 만드는 간단한 예 그러면 10240 GB의 가장 작은 최대 크기, SQL_Latin1_General_CP1_CI_AS의 기본 데이터 정렬 및 DW100인 가장 작은 컴퓨팅 능력을 가진 데이터베이스가 생성됩니다.

```sql
CREATE DATABASE TestDW
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');
```

### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>2. 모든 옵션을 사용하여 데이터 웨어하우스 데이터베이스 만들기
모든 옵션을 사용하여 10테라바이트 데이터 웨어하우스를 생성하는 예입니다.

```sql
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');
```

## <a name="see-also"></a>참고 항목

- [ALTER DATABASE- Azure SQL Data Warehouse](../../t-sql/statements/alter-database-transact-sql.md?view=aps-pdw-2016-au7)
- [CREATE TABLE- Azure SQL Data Warehouse](../../t-sql/statements/create-table-azure-sql-data-warehouse.md)
- [DROP DATABASE - Transact-SQL](../../t-sql/statements/drop-database-transact-sql.md)

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

> |||||
> |-|-|-|-|
> |[SQL Server](create-database-transact-sql.md?view=sql-server-2017)| [SQL Database<br />단일 데이터베이스/탄력적 풀](create-database-transact-sql.md?view=azuresqldb-current)| [SQL Database<br />관리되는 인스턴스](create-database-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](create-database-transact-sql.md?view=azure-sqldw-latest)|**_\* Analytics Platform<br />System(PDW) \*_** |

&nbsp;

## <a name="analytics-platform-system"></a>분석 플랫폼 시스템

## <a name="overview"></a>개요
Analytics Platform System에서 이 문은 Analytics Platform System 어플라이언스에서 새 데이터베이스를 만드는 데 사용됩니다. 이 문을 사용하여 어플라이언스 데이터베이스와 관련된 모든 파일을 만들고 데이터베이스 테이블 및 트랜잭션 로그에 대한 최대 크기 및 자동 증가 옵션을 설정합니다.

## <a name="syntax"></a>구문

```
CREATE DATABASE database_name
WITH (
    [ AUTOGROW = ON | OFF , ]
    REPLICATED_SIZE = replicated_size [ GB ] ,
    DISTRIBUTED_SIZE = distributed_size [ GB ] ,
    LOG_SIZE = log_size [ GB ] )
[;]
```

## <a name="arguments"></a>인수

*database_name*     
새 데이터베이스의 이름입니다. 허용된 데이터베이스 이름에 대한 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 "개체 명명 규칙" 및 "예약된 데이터베이스 이름"을 참조합니다.

AUTOGROW = ON | **OFF**     
이 데이터베이스에 대한 *replicated_size*, *distributed_size* 및 *log_size* 매개 변수가 지정된 크기를 넘어 필요에 따라 자동으로 증가하는지 여부를 지정합니다. 기본값은 **OFF**입니다.

AUTOGROW가 ON인 경우 *replicated_size*, *distributed_size* 및 *log_size*가 각 데이터 삽입, 업데이트 또는 이미 할당된 것보다 더 많은 스토리지 용량이 필요한 기타 작업의 필요에 따라(지정된 초기 크기의 블록에서가 아니라) 성장하게 됩니다.

AUTOGROW가 OFF이면 크기가 자동으로 증가하지 않습니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 *replicated_size*, *distributed_size* 또는 *log_size*가 지정된 값을 초과하여 성장할 것을 요구하는 작업을 시도할 경우 오류를 반환합니다.

AUTOGROW는 모든 크기에 대해 ON이거나 OFF입니다. 예를 들어 *log_size*에 대해 AUTOGROW를 ON으로 설정하는 것이 가능하지 않지만 *replicated_size*에 대해서는 ON으로 설정하지 않습니다.

*replicated_size* [ GB ]      
양수입니다. *각 컴퓨팅 노드에서* 복제된 테이블과 해당 데이터에 할당된 총 공간에 대한 크기(정수 또는 10진 기가바이트로)를 설정합니다. 최소 및 최대 *replicated_size* 요구 사항은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 "최소 및 최대 값"를 참조합니다.

AUTOGROW가 ON인 경우 복제된 테이블이 이 제한을 초과해 성장하도록 허용됩니다.

AUTOGROW가 OFF인 경우 사용자가 *replicated_size*를 초과하여 크기가 증가하는 식으로 새로 복제된 테이블을 만들고 기존 복제된 테이블에 데이터를 삽입하고 또는 기존 복제된 테이블을 업데이트하려고 하면 오류가 반환됩니다.

*distributed_size* [ GB ]      
양수입니다. *어플라이언스 전반에 걸쳐* 복제된 테이블(및 해당 데이터)에 할당된 총 공간에 대한 정수 또는 10진 기가바이트로 표시된 크기입니다. 최소 및 최대 *distributed_size* 요구 사항은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 "최소 및 최대 값"를 참조합니다.

AUTOGROW가 ON인 경우 분산된 테이블이 이 제한을 초과해 성장하도록 허용됩니다.

AUTOGROW가 OFF인 경우 사용자가 *distributed_size*를 초과하여 크기가 증가하는 식으로 새로 분산된 테이블을 만들고 기존 분산된 테이블에 데이터를 삽입하고 또는 기존 분산된 테이블을 업데이트하려고 하면 오류가 반환됩니다.

*log_size* [ GB ]      
양수입니다. *어플라이언스 전반에 걸친* 트랜잭션 로그에 대한 크기(정수 또는 10진 기가바이트로 표시된)입니다.

최소 및 최대 *log_size* 요구 사항은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 "최소 및 최대 값"를 참조합니다.

AUTOGROW가 ON인 경우 로그 파일은 이 제한을 초과하여 성장하도록 허용됩니다. [DBCC SHRINKLOG(Azure SQL 데이터 웨어하우스)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) 문을 사용하여 로그 파일의 크기를 원래 크기로 줄입니다.

AUTOGROW가 OFF인 경우 *log_size*를 초과한 개별 컴퓨팅 노드에서 로그 크기를 증가시키는 모든 작업에 대해서 사용자에게 오류가 반환됩니다.

## <a name="permissions"></a>사용 권한
master 데이터베이스에서 `CREATE ANY DATABASE` 권한 또는 **sysadmin** 고정 서버 역할에서 멤버자격이 필요합니다.

다음 예에서는 데이터베이스 사용자 Fay에게 데이터베이스를 만들 수 있는 권한을 제공합니다.

```sql
USE master;
GO
GRANT CREATE ANY DATABASE TO [Fay];
GO
```

## <a name="general-remarks"></a>일반적인 주의 사항
[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에 대한 호환성 수준인 데이터베이스 호환성 수준 120으로 데이터베이스를 만듭니다. 이렇게 하면 데이터베이스는 PDW가 사용하는 모든 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 기능을 사용할 수 있습니다.

## <a name="limitations-and-restrictions"></a>제한 사항
명시적 트랜잭션에서는 CREATE DATABASE 문을 사용할 수 없습니다. 자세한 내용은 [문](../../t-sql/statements/statements.md)을 참조하십시오.

데이터베이스에 대한 최소 및 최대 제약 조건에 관한 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 “최소 및 최대 값”을 참조합니다.

데이터베이스를 만들 경우 다음 크기의 총합계를 할당하기 위해 *각 컴퓨팅 노드*에 충분히 사용할 수 있는 여유 공간이 있어야 합니다.

- *replicated_table_size* 크기의 테이블이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.
- (*distributed_table_size* / 컴퓨팅 노드 수) 크기의 테이블이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.
- (*log_size* / 컴퓨팅 노드 수) 크기의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그입니다.

## <a name="locking"></a>잠금
DATABASE 개체에 대한 공유 잠금을 사용합니다.

## <a name="metadata"></a>메타데이터
이 작업이 성공한 후 이 데이터베이스에 대한 항목이 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 및 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 메타데이터 보기에 표시됩니다.

## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 

### <a name="a-basic-database-creation-examples"></a>1. 기본 데이터베이스 만들기 예제
다음 예제에서는 복제된 테이블에 대해 컴퓨팅 노드당 100GB, 분산된 테이블에 대해 어플라이언스당 500GB, 트랜잭션 로그에 대해 어플라이언스당 100GB의 스토리지 용량이 있는 `mytest` 데이터베이스를 만듭니다. 이 예제에서는 AUTOGROW가 기본으로 Off로 설정돼 있습니다.

```sql
CREATE DATABASE mytest
  WITH
    (REPLICATED_SIZE = 100 GB,
    DISTRIBUTED_SIZE = 500 GB,
    LOG_SIZE = 100 GB );
```

다음 예제에서는 AUTOGROW가 켜진 경우를 제외하고 위와 동일한 매개 변수가 있는 `mytest` 데이터베이스를 만듭니다. 이렇게 하면 데이터베이스가 지정된 크기 매개 변수를 벗어나 성장할 수 있습니다.

```sql
CREATE DATABASE mytest
  WITH
    (AUTOGROW = ON,
    REPLICATED_SIZE = 100 GB,
    DISTRIBUTED_SIZE = 500 GB,
    LOG_SIZE = 100 GB);
```

### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>2. 부분 기가바이트 크기를 사용하여 데이터베이스 만들기
다음 예제에서는 복제된 테이블에 대해 컴퓨팅 노드당 1.5GB, 분산된 테이블에 대해 어플라이언스당 5.25GB, 트랜잭션 로그에 대해 어플라이언스당 10GB의 스토리지 용량을 가진 그리고 AUTOGROW가 Off로 설정된 `mytest` 데이터베이스를 만듭니다.

```sql
CREATE DATABASE mytest
  WITH
    (REPLICATED_SIZE = 1.5 GB,
    DISTRIBUTED_SIZE = 5.25 GB,
    LOG_SIZE = 10 GB);
```

## <a name="see-also"></a>참고 항목

- [ALTER DATABASE - Analytics Platform System](../../t-sql/statements/alter-database-transact-sql.md?view=aps-pdw-2016-au7)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)

::: moniker-end
