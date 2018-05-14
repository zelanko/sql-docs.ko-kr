---
title: CREATE DATABASE(SQL Server Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 212
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 356a00b1c83220e0be211ee0357d2736533a3906
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-database-sql-server-transact-sql"></a>CREATE DATABASE(SQL Server Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  새 데이터베이스, 데이터베이스 저장에 사용되는 파일 및 데이터베이스 스냅숏을 만들거나 이전에 만든 데이터베이스의 분리된 파일에서 데이터베이스를 연결합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  

데이터베이스 만들기    

```  
CREATE DATABASE database_name   
[ CONTAINMENT = { NONE | PARTIAL } ]  
[ ON   
      [ PRIMARY ] <filespec> [ ,...n ]   
      [ , <filegroup> [ ,...n ] ]   
      [ LOG ON <filespec> [ ,...n ] ]   
]   
[ COLLATE collation_name ]  
[ WITH  <option> [,...n ] ]  
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
  
데이터베이스 스냅숏 만들기    

```  
CREATE DATABASE database_snapshot_name   
    ON   
    (  
        NAME = logical_file_name,  
        FILENAME = 'os_file_name'   
    ) [ ,...n ]   
    AS SNAPSHOT OF source_database_name  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 새 데이터베이스의 이름입니다. 데이터베이스 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유해야 하고 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다.  
  
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
 데이터베이스 로그를 저장하는 데 사용하는 디스크 파일인 로그 파일을 명시적으로 정의하도록 지정합니다. LOG ON 다음에는 로그 파일을 정의하는 쉼표로 구분된 \<filespec> 항목의 목록이 옵니다. LOG ON을 지정하지 않은 경우에는 데이터베이스의 모든 데이터 파일 크기를 합한 값의 25% 또는 512KB 중에서 더 큰 값을 갖는 로그 파일 하나가 자동으로 만들어집니다. 이 파일은 기본 로그 파일 위치에 저장됩니다. 이 위치에 대한 자세한 내용은 [데이터 및 로그 파일의 기본 위치 보기 또는 변경&#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)을 참조하세요.  
  
 데이터베이스 스냅숏에는 LOG ON을 지정할 수 없습니다.  
  
 COLLATE *collation_name*  
 데이터베이스의 기본 데이터 정렬을 지정합니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 이 인수를 지정하지 않으면 데이터베이스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 기본 데이터 정렬이 할당됩니다. 데이터베이스 스냅숏에는 데이터 정렬 이름을 지정할 수 없습니다.  
  
 FOR ATTACH 또는 FOR ATTACH_REBUILD_LOG 절을 사용하여 데이터 정렬 이름을 지정할 수 없습니다. 연결된 데이터베이스의 데이터 정렬을 변경하는 방법은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?linkid=16419&kbid=325335)를 참조하세요.  
  
 Windows 및 SQL 데이터 정렬 이름에 대한 자세한 내용은 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)를 참조하세요.  
  
> [!NOTE]  
>  포함된 데이터베이스는 포함되지 않은 데이터베이스와 다른 방식으로 데이터가 정렬됩니다. 자세한 내용은 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)을 참조하세요.  
  
 WITH \<option>  
 -   **\<filestream_options>** 
  
     NON_TRANSACTED_ACCESS = { **OFF** | READ_ONLY | FULL }  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
     데이터베이스에 대한 비트랜잭션 FILESTREAM 액세스 수준을 지정합니다.  
  
    |값|Description|  
    |-----------|-----------------|  
    |OFF|비트랜잭션 액세스는 사용할 수 없습니다.|  
    |READONLY|비트랜잭션 프로세스에서 이 데이터베이스의 FILESTREAM 데이터를 읽을 수 있습니다.|  
    |FULL|FILESTREAM FileTable에 대한 전체 비트랜잭션 액세스를 사용할 수 있습니다.|  
  
     DIRECTORY_NAME = \<directory_name> **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
     Windows 호환 디렉터리 이름입니다. 이 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 Database_Directory 이름 중에서 고유해야 합니다. 고유성 비교는 대/소문자를 구분하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬 설정과 관계가 없습니다. 데이터베이스에 FileTable을 만들기 전에 이 옵션을 설정해야 합니다.  
  
 CONTAINMENT가 PARTIAL로 설정된 경우에만 다음 옵션을 사용할 수 있습니다. CONTAINMENT가 NONE으로 설정되어 있으면 오류가 발생합니다.  
  
-   **DEFAULT_FULLTEXT_LANGUAGE = \<lcid> | \<language name> | \<language alias>**  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
     See [Configure the default full-text language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) for a full description of this option.  
  
-   **DEFAULT_LANGUAGE = \<lcid> | \<language name> | \<language alias>**  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
     See [Configure the default language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) for a full description of this option.  
  
-   **NESTED_TRIGGERS = { OFF | ON}**  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
     See [Configure the nested triggers Server Configuration Option](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) for a full description of this option.  
  
-   **TRANSFORM_NOISE_WORDS = { OFF | ON}**  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
     See [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)for a full description of this option.  
  
-   **TWO_DIGIT_YEAR_CUTOFF = { 2049 | \<any year between 1753 and 9999> }**  
  
     연도를 나타내는 4자리 숫자입니다. 기본값은 2049입니다. 이 옵션에 대한 자세한 내용은 [Configure the two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 참조하세요.  
  
-   **DB_CHAINING { OFF | ON }**  
  
     ON이 지정되면 데이터베이스가 데이터베이스 간 소유권 체인의 원본 또는 대상이 될 수 있습니다.  
  
     OFF가 지정되면 데이터베이스가 데이터베이스 간 소유권 체인에 참여할 수 없습니다. 기본값은 OFF입니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 cross db ownership chaining 서버 옵션이 0(OFF)일 때 이 설정을 인식할 수 있습니다. cross db ownership chaining이 1(ON)이면 모든 사용자 데이터베이스는 이 옵션 값에 관계없이 데이터베이스 간 소유권 체인에 참여할 수 있습니다. 이 옵션은 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용하여 설정합니다.  
  
     이 옵션을 설정하려면 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다. DB_CHAINING 옵션은 master, model, tempdb 시스템 데이터베이스에서는 설정할 수 없습니다.  
  
-   **TRUSTWORTHY { OFF | ON }**  
  
     ON이 지정되면 뷰, 사용자 정의 함수 또는 저장 프로시저와 같이 가장 컨텍스트를 사용하는 데이터베이스 모듈이 데이터베이스 외부 리소스에 액세스할 수 있습니다.  
  
     OFF가 지정되면 가장 컨텍스트의 데이터베이스 모듈이 데이터베이스 외부의 리소스에 액세스할 수 없습니다. 기본값은 OFF입니다.  
  
     TRUSTWORTHY는 데이터베이스가 연결될 때마다 OFF로 설정됩니다.  
  
     기본적으로 msdb 데이터베이스를 제외한 모든 시스템 데이터베이스는 TRUSTWORTHY가 OFF로 설정되어 있습니다. model 및 tempdb 데이터베이스에 대해서는 이 값을 변경할 수 없습니다. master 데이터베이스의 경우 TRUSTWORTHY 옵션을 ON으로 설정하지 않는 것이 좋습니다.  
  
     이 옵션을 설정하려면 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다.  
  
 FOR ATTACH [ WITH \< attach_database_option > ] 기존 운영 체제 파일 집합을 [연결](../../relational-databases/databases/database-detach-and-attach-sql-server.md)하여 데이터베이스를 만들도록 지정합니다. 여기에는 주 파일을 지정하는 \<filespec> 항목이 반드시 필요합니다. 또한 데이터베이스를 처음 만들었거나 마지막으로 연결했을 때 경로가 다른 파일에 대한 \<filespec> 항목이 필요합니다. 이러한 파일에는 반드시 \<filespec> 항목을 지정해야 합니다.  
  
 FOR ATTACH를 사용하려면 다음과 같은 조건을 충족해야 합니다.  
  
-   모든 데이터 파일(MDF 및 NDF)을 사용할 수 있어야 합니다.  
  
-   로그 파일이 여러 개 있는 경우 해당 파일을 모두 사용할 수 있어야 합니다.  
  
 읽기/쓰기 데이터베이스에 현재 사용할 수 없는 로그 파일이 하나 있고 연결 작업 이전에 사용자 또는 열린 트랜잭션 없이 데이터베이스가 종료된 경우 FOR ATTACH를 사용하면 자동으로 로그 파일이 다시 작성되고 주 파일이 업데이트됩니다. 반면에 읽기 전용 데이터베이스의 경우에는 주 파일을 업데이트할 수 없으므로 로그를 다시 작성할 수 없습니다. 따라서 사용할 수 없는 로그와 읽기 전용 데이터베이스를 연결할 때는 로그 파일 또는 FOR ATTACH 절 내의 파일을 제공해야 합니다.  
  
> [!NOTE]  
>  최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 만든 데이터베이스를 이전 버전에서 연결할 수 없습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 연결 중인 데이터베이스에 속한 모든 전체 텍스트 파일이 데이터베이스에 연결됩니다. 전체 텍스트 카탈로그의 새 경로를 지정하려면 전체 텍스트 운영 체제 파일 이름을 제외한 새 위치를 지정합니다. 자세한 내용은 예 섹션을 참조하십시오.  
  
 "Directory name"이 있는 FILESTREAM 옵션을 포함하는 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 Database_Directory 이름이 고유한지 확인하라는 메시지가 표시됩니다. 고유하지 않으면 연결 작업이 실패하고 "FILESTREAM Database_Directory 이름 \<name>이(가) 이 SQL Server 인스턴스에서 고유하지 않습니다"와 같은 오류 메시지가 표시됩니다. 이 오류를 방지하려면 선택적 매개 변수 *directory_name*이 이 작업에 전달되어야 합니다.  
  
 데이터베이스 스냅숏에는 FOR ATTACH를 지정할 수 없습니다.  
  
 FOR ATTACH에 RESTRICTED_USER 옵션을 지정할 수 있습니다. RESTRICTED_USER는 db_owner 고정 데이터베이스 역할 및 dbcreator와 sysadmin 고정 서버 역할의 멤버만 데이터베이스로의 연결을 허용하지만 연결되는 수는 제한하지 않습니다. 자격이 없는 사용자의 연결 시도는 거부됩니다.  
  
 데이터베이스에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용하는 경우 다음과 같이 FOR ATTACH 절에 WITH \<service_broker_option>을 사용합니다. 
  
 \<service_broker_option> 데이터베이스에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 배달 및 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자를 제어합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 옵션은 FOR ATTACH 절을 사용할 때만 지정할 수 있습니다.  
  
 ENABLE_BROKER  
 지정된 데이터베이스에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용할 수 있도록 지정합니다. 즉, 메시지 배달이 시작되고 sys.databases 카탈로그 뷰에서 is_broker_enabled가 True로 설정됩니다. 데이터베이스에 기존 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자가 유지됩니다.  
  
 NEW_BROKER  
 sys.databases와 복원된 데이터베이스 둘 다에서 새 service_broker_guid 값을 만들고 정리 작업을 통해 모든 대화 끝점을 끝냅니다. 이때 Service Broker가 설정되지만 원격 대화 끝점에 메시지가 전송되지 않습니다. 이전 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자를 참조하는 경로는 새 식별자로 다시 만들어야 합니다.  
  
 ERROR_BROKER_CONVERSATIONS  
 데이터베이스가 연결 또는 복원되었다는 오류 메시지를 표시하고 모든 대화를 끝냅니다. Service Broker는 이 작업이 완료될 때까지 해제된 후 설정됩니다. 데이터베이스에 기존 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자가 유지됩니다.  
  
 분리되지 않고 복사된 복제 데이터베이스를 연결하는 경우에는 다음 사항을 고려합니다.  
  
-   데이터베이스를 원래 데이터베이스와 동일한 서버 인스턴스 및 버전에 연결하는 경우에는 추가 작업이 필요하지 않습니다.  
  
-   데이터베이스를 동일한 서버 인스턴스의 업그레이드된 버전에 연결하는 경우에는 연결 작업이 완료된 다음, [sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md)을 실행하여 복제를 업그레이드해야 합니다.  
  
-   데이터베이스를 버전에 관계없이 다른 서버 인스턴스에 연결하는 경우에는 연결 작업이 완료된 다음, [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 실행하여 복제를 제거해야 합니다.  
  
> [!NOTE]  
> **vardecimal** 저장소 형식으로 연결 작업을 수행할 수는 있지만 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서비스 팩 2 이상으로 업그레이드해야 합니다. vardecimal 저장소 형식을 사용하는 데이터베이스는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 수 없습니다. **vardecimal** 저장소 형식에 대한 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하십시오.  
  
 데이터베이스가 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 처음으로 연결되거나 복원될 때 데이터베이스 마스터 키(서비스 마스터 키로 암호화됨)의 복사본은 서버에 아직 저장되지 않은 상태입니다. 데이터베이스 마스터 키를 암호 해독하려면 **OPEN MASTER KEY** 문을 사용해야 합니다. DMK를 암호 해독한 후에는 **ALTER MASTER KEY REGENERATE** 문을 사용하여 SMK(서비스 마스터 키)로 암호화된 DMK의 복사본을 서버에 프로비전함으로써 앞으로 자동 암호 해독을 사용하도록 설정할 수 있습니다. 데이터베이스가 이전 버전에서 업그레이드되지 않은 경우에는 DMK를 다시 생성해야 최신 AES 알고리즘을 사용할 수 있습니다. DMK를 다시 생성하는 방법은 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)를 참조하세요. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 데 소요되는 시간은 DMK에서 보호하는 개체 수에 따라 달라집니다. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 작업은 한 번만 필요하며 키 회전 전략의 일부로 이후에 수행하는 다시 생성 작업에 영향을 주지 않습니다. 연결을 사용하여 데이터베이스를 업그레이드하는 방법은 [분리 및 연결을 사용하여 데이터베이스 업그레이드&#40;Transact-SQL&#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md)를 참조하세요.  
  
> [!IMPORTANT]  
> 출처를 알 수 없거나 신뢰할 수 없는 데이터베이스는 연결하지 않는 것이 좋습니다. 이러한 데이터베이스에 포함된 악성 코드가 의도하지 않은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 실행하거나 스키마 또는 물리적 데이터베이스 구조를 수정하여 오류가 발생할 수 있습니다. 알 수 없거나 신뢰할 수 없는 소스의 데이터베이스를 사용하기 전에 비프로덕션 서버의 데이터베이스에서 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)를 실행하여 데이터베이스에서 코드(예: 저장 프로시저 또는 다른 사용자 정의 코드)를 시험해 보세요.  
  
> [!NOTE]  
> 데이터베이스를 연결할 때 **TRUSTWORTHY** 및 **DB_CHAINING** 옵션은 영향도 주지 않습니다.  
  
 FOR ATTACH_REBUILD_LOG  
 기존 운영 체제 파일 집합을 연결하여 데이터베이스를 만들도록 지정합니다. 이 옵션은 읽기/쓰기 데이터베이스로 제한됩니다. 주 파일을 지정하는 *\<filespec>* 항목이 있어야 합니다. 하나 이상의 트랜잭션 로그 파일이 없으면 로그 파일이 다시 작성됩니다. ATTACH_REBUILD_LOG는 1MB의 새 로그 파일을 자동으로 만듭니다. 이 파일은 기본 로그 파일 위치에 저장됩니다. 이 위치에 대한 자세한 내용은 [데이터 및 로그 파일의 기본 위치 보기 또는 변경&#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)을 참조하세요.  
  
> [!NOTE]  
>  로그 파일이 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 로그 파일을 다시 작성하지 않고 해당 파일을 사용합니다.  
  
 FOR ATTACH_REBUILD_LOG를 사용하려면 다음과 같은 조건을 충족해야 합니다.  
  
-   데이터베이스가 완전하게 종료된 상태여야 합니다.  
  
-   모든 데이터 파일(MDF 및 NDF)을 사용할 수 있어야 합니다.  
  
> [!IMPORTANT]  
> 이 작업을 실행하면 로그 백업 체인이 끊어집니다. 따라서 작업이 완료된 후 전체 데이터베이스 백업을 수행하는 것이 좋습니다. 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)을 참조하세요.  
  
 일반적으로 FOR ATTACH_REBUILD_LOG는 로그 크기가 큰 읽기/쓰기 데이터베이스를 복사본이 주로 읽기 작업에만 사용되어 원본 데이터베이스에 비해 로그 공간이 덜 필요한 다른 서버에 복사할 때 사용됩니다.  
  
 데이터베이스 스냅숏에는 FOR ATTACH_REBUILD_LOG를 지정할 수 없습니다.  
  
 데이터베이스를 연결 및 분리하는 방법은 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)을 참조하십시오.  
  
 \<filespec>  
 파일 속성을 제어합니다.  
  
 NAME *logical_file_name*  
 파일의 논리적 이름을 지정합니다. FOR ATTACH 절 중 하나를 지정하는 경우가 아니면 FILENAME이 지정될 때 NAME이 필요합니다. FILESTREAM 파일 그룹 이름은 PRIMARY로 지정할 수 없습니다.  
  
 *logical_file_name*  
 파일 참조 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 논리적 이름입니다. *Logical_file_name*은 데이터베이스에서 고유해야 하며 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다. 이 이름은 문자 상수, 유니코드 상수, 일반 식별자 또는 구분 식별자가 될 수 있습니다.  
  
 FILENAME { **'***os_file_name***'** | **'***filestream_path***'** }  
 운영 체제(물리적) 파일 이름을 지정합니다.  
  
 **'** *os_file_name* **'**  
 파일을 만들 때 운영 체제에서 사용한 경로와 파일 이름입니다. 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치된 로컬 서버, SAN(저장 영역 네트워크) 또는 iSCSI 기반 네트워크 중 하나의 장치에 있어야 합니다. 지정한 경로는 CREATE DATABASE 문을 실행하기 전에 반드시 존재해야 합니다. 자세한 내용은 주의 사항 섹션의 "데이터베이스 파일 및 파일 그룹"을 참조하십시오.  
  
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
  
 *size*  
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
 파일 그룹 속성을 제어합니다. 데이터베이스 스냅숏에는 파일 그룹을 지정할 수 없습니다.  
  
 FILEGROUP *filegroup_name*  
 파일 그룹의 논리적 이름입니다.  
  
 *filegroup_name*  
 *filegroup_name*은 데이터베이스 내에서 고유해야 하고 시스템에서 제공한 이름인 PRIMARY 및 PRIMARY_LOG일 수 없습니다. 이 이름은 문자 상수, 유니코드 상수, 일반 식별자 또는 구분 식별자가 될 수 있습니다. 이 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.  
  
 CONTAINS FILESTREAM  
 파일 그룹이 FILESTREAM BLOB(Binary Large Object)를 파일 시스템에 저장하도록 지정합니다.  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
 파일 그룹이 memory_optimized 데이터를 파일 시스템에 저장하도록 지정합니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요. 데이터베이스당 MEMORY_OPTIMIZED_DATA 파일 그룹이 하나만 허용됩니다. 메모리 최적화 데이터를 저장하기 위해 파일 그룹을 만드는 코드 샘플은 [메모리 최적화 테이블 및 고유하게 컴파일된 저장 프로시저 만들기](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)를 참조하세요.  
  
 DEFAULT  
 명명한 파일 그룹이 데이터베이스의 기본 파일 그룹임을 지정합니다.  
  
 *database_snapshot_name*  
 새 데이터베이스 스냅숏의 이름입니다. 데이터베이스 스냅숏 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유해야 하며 식별자에 대한 규칙을 따라야 합니다. *database_snapshot_name*은 최대 128자까지 가능합니다.  
  
 ON **(** NAME **=***logical_file_name***,** FILENAME **='***os_file_name***')** [ **,**... *n* ]  
 데이터베이스 스냅숏을 만들기 위해 원본 데이터베이스의 파일 목록을 지정합니다. 스냅숏이 동작하려면 모든 데이터 파일을 개별적으로 지정해야 합니다. 그러나 데이터베이스 스냅숏에는 로그 파일이 허용되지 않습니다. FILESTREAM 파일 그룹은 데이터베이스 스냅숏에서 지원되지 않습니다. FILESTREAM 데이터 파일이 CREATE DATABASE ON 절에 포함되어 있으면 문이 실패하고 오류가 발생합니다.  
  
 NAME, FILENAME 및 각 값에 대한 내용은 해당하는 \<filespec> 값의 설명을 참조하십시오.  
  
> [!NOTE]  
> 데이터베이스 스냅숏을 만들 때는 다른 \<filespec> 옵션 및 PRIMARY 키워드를 사용할 수 없습니다.  
  
 AS SNAPSHOT OF *source_database_name*  
 만들고 있는 데이터베이스가 *source_database_name*에 지정된 원본 데이터베이스의 데이터베이스 스냅숏임을 지정합니다. 스냅숏 및 원본 데이터베이스는 같은 인스턴스에 있어야 합니다.  
  
 자세한 내용은 주의 사항 섹션의 "데이터베이스 스냅숏"을 참조하십시오.  
  
## <a name="remarks"></a>Remarks  
 사용자 데이터베이스를 생성, 수정 또는 삭제할 때마다 [마스터 데이터베이스](../../relational-databases/databases/master-database.md)를 백업해야 합니다.  
  
 CREATE DATABASE 문은 기본 트랜잭션 관리 모드인 자동 커밋 모드에서 실행해야 하며 명시적 또는 암시적 트랜잭션에서는 허용되지 않습니다.  
  
 CREATE DATABASE 문 하나를 사용하여 데이터베이스 및 해당 데이터베이스를 저장하는 파일을 만들 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 다음과 같은 단계로 CREATE DATABASE 문을 구현합니다.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [model 데이터베이스](../../relational-databases/databases/model-database.md)의 복사본을 사용하여 데이터베이스 및 해당 메타데이터를 초기화합니다.  
  
2.  데이터베이스에 Service Broker GUID가 할당됩니다.  
  
3.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 데이터베이스 내의 공간 사용 방법을 기록하는 내부 데이터가 포함된 페이지를 제외하고 데이터베이스의 나머지 부분을 빈 페이지로 채웁니다.  
  
 하나의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스당 최대 32,767개의 데이터베이스를 지정할 수 있습니다.  
  
 각 데이터베이스에는 해당 데이터베이스에서 특수한 작업을 수행할 수 있는 소유자가 있습니다. 소유자는 데이터베이스를 만든 사용자입니다. [sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)를 사용하여 데이터베이스 소유자를 변경할 수 있습니다.  

일부 데이터베이스 기능은 파일 시스템의 기능이 있어야 데이터베이스의 모든 기능을 사용할 수 있습니다. 파일 시스템 기능 집합이 필요한 일부 기능의 예를 들면 다음과 같습니다.
- DBCC CHECKDB
- FileStream
- VSS 및 파일 스냅샷을 이용한 온라인 백업
- 데이터베이스 스냅숏 생성
- 메모리 최적화 데이터 파일 그룹
   
## <a name="database-files-and-filegroups"></a>데이터베이스 파일 및 파일 그룹  
 모든 데이터베이스에는 *주 파일*과 *트랜잭션 로그 파일*이라는 2개의 파일과 하나 이상의 파일 그룹이 있습니다. 각 데이터베이스에 최대 32,767개의 파일과 32,767개의 파일 그룹을 지정할 수 있습니다.  
  
 데이터베이스를 만들 때는 데이터베이스에서 예상되는 최대 데이터 크기를 고려하여 데이터 파일을 가능한 한 크게 만드는 것이 좋습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 성능과 안정성을 최적화하는 구성을 위해 SAN(저장 영역 네트워크), iSCSI 기반 네트워크 또는 로컬로 연결된 디스크에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 파일을 저장하는 것이 좋습니다.  
  
## <a name="database-snapshots"></a>데이터베이스 스냅숏  
 CREATE DATABASE 문을 사용하여 *원본 데이터베이스*의 읽기 전용 정적 뷰인 *데이터베이스 스냅숏*을 만들 수 있습니다. 데이터베이스 스냅숏은 스냅숏을 만들었을 당시의 원본 데이터베이스와 트랜잭션 측면에서 일관성을 가집니다. 원본 데이터베이스 하나에 스냅숏이 여러 개 있을 수 있습니다.  
  
> [!NOTE]  
> 데이터베이스 스냅숏을 만드는 경우 CREATE DATABASE 문은 로그 파일, 오프라인 파일, 복원 파일 및 존재하지 않는 파일을 참조할 수 없습니다.  
  
 데이터베이스 스냅숏 만들기에 실패한 경우 해당 스냅숏은 주의 대상이 되며 삭제해야 합니다. 자세한 내용은 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)를 참조하세요.  
  
 각 스냅숏은 DROP DATABASE를 사용하여 삭제할 때까지 그대로 유지됩니다.  
  
 자세한 내용은 [데이터베이스 스냅숏&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)을 참조하세요.  
  
## <a name="database-options"></a>데이터베이스 옵션  
 데이터베이스를 만들 때마다 몇 가지 데이터베이스 옵션이 자동으로 설정됩니다. 이러한 옵션에 대한 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  
## <a name="the-model-database-and-creating-new-databases"></a>새 데이터베이스 만들기 및 model 데이터베이스  
 [model 데이터베이스](../../relational-databases/databases/model-database.md)에 있는 모든 사용자 정의 개체는 새로 만든 데이터베이스에 복사됩니다. 테이블, 뷰, 저장 프로시저, 데이터 형식 등의 모든 개체를 model 데이터베이스에 추가하여 새로 만든 모든 데이터베이스에 포함할 수 있습니다.  
  
 크기 매개 변수를 추가하지 않고 CREATE DATABASE *database_name* 문을 지정하면 model 데이터베이스의 주 파일과 크기가 같은 주 데이터 파일이 만들어집니다.  
  
 FOR ATTACH를 지정하지 않은 경우 모든 새 데이터베이스는 model 데이터베이스에서 데이터베이스 옵션 설정을 상속합니다. 예를 들어 자동 축소와 같은 데이터베이스 옵션은 model 데이터베이스와 새로 만드는 모든 데이터베이스에서 **true**로 설정됩니다. model 데이터베이스에서 옵션을 변경하면 새로 만드는 모든 데이터베이스에 이러한 새 옵션 설정이 사용됩니다. 기존 데이터베이스는 model 데이터베이스 변경 내용의 영향을 받지 않습니다. CREATE DATABASE 문에 FOR ATTACH를 지정하는 경우 새 데이터베이스는 원본 데이터베이스의 데이터베이스 옵션 설정을 상속합니다.  
  
## <a name="viewing-database-information"></a>데이터베이스 정보 보기  
 카탈로그 뷰, 시스템 함수 및 시스템 저장 프로시저를 사용하여 데이터베이스, 파일 및 파일 그룹에 대한 정보를 반환할 수 있습니다. 자세한 내용은 [시스템 뷰&#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 CREATE DATABASE, CREATE ANY DATABASE 또는 ALTER ANY DATABASE 권한이 필요합니다.  
  
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
 다음 예에서는 `mytest` 데이터베이스를 만들고 해당 주 파일 및 트랜잭션 로그 파일을 만듭니다. 문에 \<filespec> 항목이 없으므로 주 데이터베이스 파일의 크기는 model 데이터베이스 주 파일의 크기와 같습니다. 트랜잭션 로그는 512KB와 주 데이터 파일 크기의 25% 중 더 큰 값으로 설정됩니다. MAXSIZE를 지정하지 않았으므로 사용 가능한 디스크 공간을 모두 채울 때까지 파일 크기가 증가할 수 있습니다. 이 예에서는 `mytest` 데이터베이스를 만들기 전에 `mytest`라는 데이터베이스(있는 경우)를 삭제하는 방법도 보여 줍니다.  
  
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
  
### <a name="c-creating-a-database-by-specifying-multiple-data-and-transaction-log-files"></a>3. 데이터 파일 및 트랜잭션 로그 파일을 여러 개 지정하여 데이터베이스 만들기  
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
  
### <a name="d-creating-a-database-that-has-filegroups"></a>4. 파일 그룹이 있는 데이터베이스 만들기  
 다음 예에서는 아래에 나열된 파일 그룹을 포함하는 `Sales` 데이터베이스를 만듭니다.  
  
-   `Spri1_dat` 및 `Spri2_dat` 파일을 포함하는 주 파일 그룹. 이러한 파일의 FILEGROWTH 증가분은 `15%`로 지정됩니다.  
  
-   `SalesGroup1` 및 `SGrp1Fi1` 파일을 포함하는 `SGrp1Fi2` 파일 그룹  
  
-   `SalesGroup2` 및 `SGrp2Fi1` 파일을 포함하는 `SGrp2Fi2` 파일 그룹  
  
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
  
### <a name="e-attaching-a-database"></a>5. 데이터베이스 연결  
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
  
### <a name="f-creating-a-database-snapshot"></a>6. 데이터베이스 스냅숏 만들기  
 다음 예에서는 `sales_snapshot0600` 데이터베이스 스냅숏을 만듭니다. 데이터베이스 스냅숏은 읽기 전용이므로 로그 파일을 지정할 수 없습니다. 구문에 맞게 원본 데이터베이스의 모든 파일을 지정하며 파일 그룹은 지정하지 않습니다.  
  
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
  
### <a name="g-creating-a-database-and-specifying-a-collation-name-and-options"></a>7. 데이터베이스 만들기 및 데이터 정렬 이름과 옵션 지정  
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
  
### <a name="h-attaching-a-full-text-catalog-that-has-been-moved"></a>8. 이동된 전체 텍스트 카탈로그 연결  
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
  
-   `FileStreamDB_data`는 행 데이터를 포함합니다. 여기에는 기본 경로가 지정된 `FileStreamDB_data.mdf` 파일 하나가 포함됩니다.  
  
-   `FileStreamPhotos`는 FILESTREAM 데이터를 포함합니다. 여기에는 두 개의 FILESTREAM 데이터 컨테이너가 포함됩니다. 하나는 `FSPhotos`에 있는 `C:\MyFSfolder\Photos`이고 다른 하나는 `FSPhotos2`에 있는 `D:\MyFSfolder\Photos`입니다. 이 그룹은 기본 FILESTREAM 파일 그룹으로 표시됩니다.  
  
-   `FileStreamResumes`는 FILESTREAM 데이터를 포함합니다. 여기에는 `FSResumes`에 있는 FILESTREAM 데이터 컨테이너 `C:\MyFSfolder\Resumes`가 포함됩니다.  
  
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
  
### <a name="j-creating-a-database-that-has-a-filestream-filegroup-with-multiple-files"></a>10. 여러 파일이 포함된 FILESTREAM 파일 그룹이 있는 데이터베이스 만들기  
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
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_changedbowner&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_detach_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_removedbreplication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)   
 [데이터베이스 스냅숏&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [데이터베이스 파일 이동](../../relational-databases/databases/move-database-files.md)   
 [데이터베이스](../../relational-databases/databases/databases.md)   
 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  

