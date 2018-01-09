---
title: "ALTER DATABASE 파일 및 파일 그룹 옵션 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ADD FILE
- ADD_FILE_TSQL
dev_langs: TSQL
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
caps.latest.revision: "61"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 826b8a5abb14ee677f89f1c77956215ec72f90c6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="alter-database-transact-sql-file-and-filegroup-options"></a>ALTER DATABASE (Transact SQL) 파일 및 파일 그룹 옵션 
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스와 연결된 파일 및 파일 그룹을 수정합니다. 데이터베이스의 파일과 파일 그룹을 추가 또는 제거하고 데이터베이스 또는 해당 파일과 파일 그룹의 특성을 변경합니다. 다른 ALTER DATABASE 옵션을 참조 하세요. [ALTER database&#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
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
**\<add_or_modify_files >:: =**
  
 추가, 제거 또는 수정할 파일을 지정합니다.  
  
 *database_name*  
 수정할 데이터베이스의 이름입니다.  
  
 ADD FILE  
 데이터베이스에 파일을 추가합니다.  
  
 파일 그룹으로 { *filegroup_name* }  
 지정된 파일을 추가할 파일 그룹을 지정합니다. 현재 파일 그룹 및 어떤 파일 그룹은 현재 기본값을 표시 하려면 사용 된 [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) 카탈로그 뷰.  
  
 ADD LOG FILE  
 지정된 데이터베이스에 로그 파일을 추가합니다.  
  
 REMOVE FILE *logical_file_name*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 논리적 파일 설명을 제거하고 물리적 파일을 삭제합니다. 파일이 비어 있어야 제거할 수 있습니다.  
  
 *logical_file_name*  
 파일 참조 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 논리적 이름입니다.  
  
> [!WARNING]  
> FILE_SNAPSHOT 있는 데이터베이스 파일을 제거 합니다. 연결 된 백업이 성공 하지만 데이터베이스 파일을 참조 하는 백업 무효화를 방지 하기 위해 연결 된 모든 스냅숏을 삭제 되지 않습니다. 파일을 자를 수 있지만 FILE_SNAPSHOT 백업의 그대로 유지 하기 위해 물리적으로 삭제 되지 않습니다. 자세한 내용은 [Microsoft Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요. **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 MODIFY FILE  
 수정할 파일을 지정합니다. 하나의 \<filespec > 속성은 한 번에 변경할 수 있습니다. 항상 이름에 \<filespec > 수정할 파일을 식별 합니다. SIZE를 지정할 경우 새 크기가 현재 파일 크기보다 커야 합니다.  
  
 데이터 파일이나 로그 파일의 논리적 이름을 수정하려면 `NAME` 절에 이름을 바꿀 논리적 파일 이름을 지정하고 `NEWNAME` 절에 파일의 새 논리적 이름을 지정합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
MODIFY FILE ( NAME = logical_file_name, NEWNAME = new_logical_name )   
```  
  
 데이터 파일 또는 로그 파일을 새 위치로 이동하려면 `NAME` 절에 파일의 현재 논리적 이름을 지정하고 `FILENAME` 절에 새 경로와 운영 체제 파일 이름을 지정합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
MODIFY FILE ( NAME = logical_file_name, FILENAME = ' new_path/os_file_name ' )  
```  
  
 전체 텍스트 카탈로그를 이동하는 경우 FILENAME 절에 새 경로만 지정합니다. 운영 체제 파일 이름은 지정하지 마십시오.  
  
 자세한 내용은 참조 [데이터베이스 파일 이동](../../relational-databases/databases/move-database-files.md)합니다.  
  
 FILESTREAM 파일 그룹의 경우 NAME을 온라인으로 수정할 수 있습니다. FILENAME은 온라인으로 수정할 수 있지만 컨테이너를 물리적으로 재배치하고 서버를 종료한 다음 다시 시작하기 전까지는 변경 내용이 적용되지 않습니다.  
  
 FILESTREAM 파일을 OFFLINE으로 설정할 수 있습니다. FILESTREAM 파일이 오프라인인 경우 부모 파일 그룹이 내부적으로 오프라인으로 표시되므로 해당 파일 그룹 내에서 FILESTREAM 데이터에 대한 모든 액세스가 실패합니다.  
  
> [!NOTE]  
>  \<add_or_modify_files > 옵션은 포함 된 데이터베이스에서 사용할 수 없습니다.
  
 **\<filespec >:: =**  
  
 파일 속성을 제어합니다.  
  
 이름 *logical_file_name*  
 파일의 논리적 이름을 지정합니다.  
  
 *logical_file_name*  
 파일 참조 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 사용하는 논리적 이름입니다.  
  
 NEWNAME *new_logical_file_name*  
 파일의 새 논리적 이름을 지정합니다.  
  
 *new_logical_file_name*  
 기존 논리적 파일 이름을 바꿀 이름입니다. 이름은 데이터베이스 내에서 고유 하 고 규칙을 따라야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다. 이름에 문자나 유니코드 상수, 일반 식별자, 구분 식별자를 지정할 수 있습니다.  
  
 파일 이름 { **'***os_file_name***'** | **'***filestream_path* **'** | **'***memory_optimized_data_path***'**}  
 운영 체제(물리적) 파일 이름을 지정합니다.  
  
 ' *os_file_name* '  
 표준(행) 파일 그룹의 경우 이것은 파일을 만들 때 운영 체제에서 사용한 경로와 파일 이름입니다. 이 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치된 서버에 있어야 합니다. ALTER DATABASE 문을 실행하기 전에 지정된 경로가 존재해야 합니다.  
  
 파일에 UNC 경로가 지정되면 SIZE, MAXSIZE 및 FILEGROWTH 매개 변수를 설정할 수 없습니다.  
  
> [!NOTE]  
> 시스템 데이터베이스는 UNC 공유 디렉터리에 있을 수 없습니다.  
  
 파일이 읽기 전용 보조 파일이 아니거나 데이터베이스가 읽기 전용이 아닌 경우 데이터 파일을 압축 파일 시스템에 저장하지 마십시오. 또한 로그 파일을 압축 파일 시스템에 저장하면 안 됩니다.  
  
 파일이 원시 파티션에 *os_file_name* 기존 원시 파티션의 드라이브 문자만 지정 해야 합니다. 각 원시 파티션에는 한 개의 파일만 저장할 수 있습니다.  
  
 **'** *filestream_path* **'**  
 FILENAME 파일 그룹의 경우 FILENAME은 FILESTREAM 데이터가 저장될 경로를 참조합니다. 따라서 마지막 폴더 바로 위의 경로까지 있어야 하고 마지막 폴더 자체는 있으면 안 됩니다. 예를 들어 C:\MyFiles\MyFilestreamData 경로를 지정하는 경우 ALTER DATABASE를 실행하기 전에 C:\MyFiles 경로가 있어야 하지만 MyFilestreamData 폴더는 있으면 안 됩니다.  
  
 SIZE 및 FILEGROWTH 속성은 FILESTREAM 파일 그룹에 적용되지 않습니다.  
  
 **'** *memory_optimized_data_path* **'**  
 메모리 최적화 파일 그룹에서 FILENAME은 메모리 최적화 데이터가 저장되는 경로를 나타냅니다. 따라서 마지막 폴더 바로 위의 경로까지 있어야 하고 마지막 폴더 자체는 있으면 안 됩니다. 예를 들어 :\MyFiles\MyData 경로를 지정하는 경우 ALTER DATABASE를 실행하기 전에 C:\MyFiles 경로가 있어야 하지만 MyData 폴더는 있으면 안 됩니다.  
  
 파일 그룹과 파일(`<filespec>`)은 같은 문으로 만들어야 합니다.  
  
 SIZE, MAXSIZE 및 FILEGROWTH 속성은 메모리 최적화 파일 그룹에 적용되지 않습니다.  
  
 크기 *크기*  
 파일 크기를 지정합니다. SIZE는 FILESTREAM 파일 그룹에 적용되지 않습니다.  
  
 *size*  
 파일의 크기입니다.  
  
 ADD FILE과 함께 지정 하면 *크기* 파일의 초기 크기입니다. MODIFY FILE이 함께 지정 하면 *크기* 파일에 대해 새 크기와 현재 파일 크기 보다 커야 합니다.  
  
 때 *크기* 주 파일에 대 한 제공 되지 않으면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 주 파일의 크기를 사용 하 여는 **모델** 데이터베이스입니다. 보조 데이터 파일 또는 로그 파일을 지정 하는 경우 하지만 *크기* 파일을 지정 하지 않으면는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 파일을 사용 하면 1MB입니다.  
  
 KB, MB, GB 및 TB 접미사를 사용하여 각각 킬로바이트, 메가바이트, 기가바이트, 테라바이트를 지정할 수 있습니다. 기본값은 MB입니다. 소수점을 포함하지 않은 정수를 지정합니다. 소수로 된 MB 값을 지정하려면 1024를 곱하여 값을 KB로 변환합니다. 예를 들어 1.5MB인 경우 1536KB(1.5 x 1024 = 1536)를 지정합니다.  
  
 MAXSIZE { *max_size*| 무제한}  
 파일을 확장할 수 있는 최대 파일 크기를 지정합니다.  
  
 *max_size*  
 최대 파일 크기입니다. KB, MB, GB 및 TB 접미사를 사용하여 각각 킬로바이트, 메가바이트, 기가바이트, 테라바이트를 지정할 수 있습니다. 기본값은 MB입니다. 소수점을 포함하지 않은 정수를 지정합니다. 경우 *max_size* 을 지정 하지 않으면 디스크가 꽉 찰 때까지 파일 크기가 늘어납니다.  
  
 UNLIMITED  
 디스크가 꽉 찰 때까지 파일 크기가 증가하도록 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 무제한 증가로 지정된 로그 파일의 최대 크기는 2TB이고 데이터 파일의 최대 크기는 16TB입니다. 이 옵션이 FILESTREAM 컨테이너에 지정되면 최대 크기가 없습니다. 디스크가 꽉 찰 때까지 파일이 증가합니다.  
  
 FILEGROWTH *growth_increment*  
 파일의 자동 증분을 지정합니다. 파일의 FILEGROWTH 설정은 MAXSIZE 설정을 초과할 수 없습니다. FILEGROWTH는 FILESTREAM 파일 그룹에 적용되지 않습니다.  
  
 *growth_increment*  
 공간이 새로 필요할 때마다 파일에 추가되는 공간 크기입니다.  
  
 이 값은 MB, KB, GB, TB 또는 %(퍼센트) 단위로 지정할 수 있습니다. MB, KB 또는 % 접미사를 붙이지 않고 숫자를 지정하면 MB가 기본값이 됩니다. %가 지정되면 증분 크기는 파일 크기 증가가 발생하는 시점에서 해당 파일 크기에 대한 특정 비율입니다. 지정한 크기는 64KB 단위로 반올림됩니다.  
  
 값 0은 자동 증가를 사용하지 않고 추가 공간을 허용하지 않음을 나타냅니다.  
  
 FILEGROWTH를 지정 하지 않으면 기본 값은:  
  
|버전 옵션|기본값|  
|-------------|--------------------|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]로 시작|데이터 64MB입니다. 로그 파일 64MB.|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]로 시작|데이터 1MB입니다. 로그 파일 10%입니다.|  
|이전에[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|데이터 10%입니다. 로그 파일 10%입니다.|  
  
 OFFLINE  
 파일을 오프라인으로 설정하고 파일 그룹 내의 모든 개체를 액세스할 수 없도록 합니다.  
  
> [!CAUTION]  
>  파일이 손상되고 복원이 가능한 경우에만 이 옵션을 사용하십시오. OFFLINE으로 설정된 파일은 해당 파일을 백업에서 복원해야만 온라인 상태로 설정할 수 있습니다. 단일 파일 복원 방법은 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)를 참조하세요.  
  
> [!NOTE]  
> \<filespec > 옵션은 포함 된 데이터베이스에서 사용할 수 없습니다.  
  
 **\<add_or_modify_filegroups >:: =**  
  
 데이터베이스의 파일 그룹을 추가, 수정 또는 제거합니다.  
  
 파일 그룹 추가 *filegroup_name*  
 데이터베이스에 파일 그룹을 추가합니다.  
  
 CONTAINS FILESTREAM  
 파일 그룹이 FILESTREAM BLOB(Binary Large Object)를 파일 시스템에 저장하도록 지정합니다.  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])
  
 파일 그룹이 메모리 액세스에 최적화된 데이터를 파일 시스템에 저장하도록 지정합니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요. 데이터베이스당 MEMORY_OPTIMIZED_DATA 파일 그룹이 하나만 허용됩니다. 메모리 액세스에 최적화된 테이블을 만들기 위해서는 파일 그룹을 비워 둘 수 없습니다. 적어도 한 개의 파일이 있어야 합니다. *filegroup_name* 경로를 가리킵니다. 따라서 마지막 폴더 바로 위의 경로까지 있어야 하고 마지막 폴더 자체는 있으면 안 됩니다.  
  
 다음 예에서는 xtp_db 데이터베이스에 추가된 파일 그룹을 만들고 파일을 이 파일 그룹에 추가합니다. 파일 그룹은 memory_optimized 데이터를 저장합니다.  
  
```sql  
ALTER DATABASE xtp_db ADD FILEGROUP xtp_fg CONTAINS MEMORY_OPTIMIZED_DATA;  
GO  
ALTER DATABASE xtp_db ADD FILE (NAME='xtp_mod', FILENAME='d:\data\xtp_mod') TO FILEGROUP xtp_fg;  
```  
  
 파일 그룹 제거 *filegroup_name*  
 데이터베이스에서 파일 그룹을 제거합니다. 파일 그룹은 비어 있어야 제거할 수 있습니다. 먼저 파일 그룹에서 모든 파일을 제거합니다. 자세한 내용은 참조 하십시오. "파일 제거 *logical_file_name*,"이이 항목의에서 앞부분입니다.  
  
> [!NOTE]  
> FILESTREAM 가비지 수집기가 FILESTREAM 컨테이너에서 모든 파일을 제거하지 않은 경우 FILESTREAM 컨테이너를 제거하기 위한 ALTER DATABASE REMOVE FILE 작업이 실패하고 오류를 반환합니다. 이 항목의 뒷부분에 나오는 주의에서 "FILESTREAM 컨테이너 제거" 섹션을 참조하십시오.  
  
파일 그룹 수정 *filegroup_name* { \<filegroup_updatability_option > | 기본 | 이름  **=**  *new_filegroup_name* }를 READ_ONLY 또는 READ_WRITE를 만드는 파일 그룹의 데이터베이스에 대 한 기본 파일 그룹의 상태를 설정 하 여 파일 그룹을 수정 하거나 파일 그룹 이름을 변경 합니다.  
  
 \<filegroup_updatability_option >  
 파일 그룹에 대한 읽기 전용 또는 읽기/쓰기 속성을 설정합니다.  
  
 DEFAULT  
 기본 데이터베이스 파일 그룹을 변경 *filegroup_name*합니다. 데이터베이스에서 한 개의 파일 그룹만 기본 파일 그룹이 될 수 있습니다. 자세한 내용은 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)을 참조하세요.  
  
 이름 = *new_filegroup_name*  
 에 파일 그룹 이름을 변경 하는 *new_filegroup_name*합니다.  
  
 AUTOGROW_SINGLE_FILE  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])
  
 파일 그룹의 파일 자동 증가 임계값을 충족할 경우 해당 파일에만 증가 합니다. 기본값입니다.  
  
 AUTOGROW_ALL_FILES  

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])
  
 파일 그룹의 파일 자동 증가 임계값을 충족할 때 파일 그룹의 모든 파일이 증가 합니다.  
  
 **\<filegroup_updatability_option >:: =**  
  
 파일 그룹에 대한 읽기 전용 또는 읽기/쓰기 속성을 설정합니다.  
  
 READ_ONLY | READONLY  
 파일 그룹을 읽기 전용으로 지정합니다. 해당 파일 그룹의 개체를 업데이트할 수 없습니다. 주 파일 그룹은 읽기 전용으로 만들 수 없습니다. 이 상태를 변경하려면 데이터베이스에 대해 배타적 액세스 권한이 있어야 합니다. 자세한 내용은 SINGLE_USER 절을 참조하십시오.  
  
 읽기 전용 데이터베이스는 데이터 수정을 허용하지 않기 때문에 다음과 같은 특성을 포함합니다.  
  
-   시스템 시작 시 자동 복원을 하지 않습니다.  
-   데이터베이스 축소가 불가능합니다.  
-   읽기 전용 데이터베이스에서는 잠금이 발생하지 않습니다. 따라서 쿼리 성능은 더 향상될 수 있습니다.  
  
> [!NOTE]  
>  읽기 전용의 이후 버전에서 제거 됩니다 키워드 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 향후 개발 작업에서는 READONLY를 사용하지 않도록 하고 현재 READONLY를 사용하는 응용 프로그램은 수정하십시오. 대신 READ_ONLY를 사용하십시오.  
  
 READ_WRITE | READWRITE  
 파일 그룹을 READ_WRITE로 지정합니다. 해당 파일 그룹의 개체를 업데이트할 수 있습니다. 이 상태를 변경하려면 데이터베이스에 대해 배타적 액세스 권한이 있어야 합니다. 자세한 내용은 SINGLE_USER 절을 참조하십시오.  
  
> [!NOTE]  
>  키워드 `READWRITE` 의 이후 버전에서 제거 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 사용 하지 않도록 `READWRITE` 새 개발에서 작업, 및 현재 사용 하는 응용 프로그램은 수정 `READWRITE` 사용할 `READ_WRITE` 대신 합니다.  
  
 이 옵션의 상태를 검사 하 여 확인할 수 있습니다는 **is_read_only** 열에는 **sys.databases** 카탈로그 뷰 또는 **Updateability** 는 의속성`DATABASEPROPERTYEX` 함수입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여 데이터베이스의 크기를 줄이려면 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)합니다.  
  
추가 하거나 제거 하는 동안 파일은 `BACKUP` 문을 실행 합니다.  
  
각 데이터베이스에 최대 32,767개의 파일과 32,767개의 파일 그룹을 지정할 수 있습니다.  
  
부터는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], 데이터베이스 파일 (예를 들어, 온라인 또는 오프 라인)의 상태는 데이터베이스의 상태에서 독립적으로 유지 됩니다. 자세한 내용은 참조 [파일 상태](../../relational-databases/databases/file-states.md)합니다. 
-  전체 파일 그룹의 가용성은 파일 그룹 내 파일의 상태에 따라 결정됩니다. 파일 그룹을 사용하려면 파일 그룹 내의 모든 파일이 온라인 상태여야 합니다. 
-  파일 그룹이 오프라인 상태인 경우 SQL 문을 사용한 파일 그룹 액세스 시도는 오류가 발생하며 실패하게 됩니다. 에 대 한 쿼리 계획을 작성할 때 `SELECT` 문, 쿼리 최적화 프로그램에서는 비클러스터형 인덱스와 오프 라인 파일 그룹에 상주 하는 인덱싱된 뷰 사용 합니다. 이러한 문이 성공하도록 합니다. 그러나 오프 라인 파일 그룹에 힙 또는 클러스터형된 인덱스는 대상 테이블의 경우, 고 `SELECT` 문이 실패 합니다. 또한 모든 `INSERT`, `UPDATE`, 또는 `DELETE` 오프 라인 파일 그룹의 모든 인덱스가 있는 테이블을 수정 하는 문이 실패 합니다.  
  
## <a name="moving-files"></a>파일 이동  
FILENAME에 새 위치를 지정하여 시스템 또는 사용자 정의 데이터 및 로그 파일을 이동할 수 있습니다. 이는 다음과 같은 시나리오에서 유용합니다.  
  
-   오류 복구. 예를 들어 데이터베이스가 주의 대상 모드이거나 하드웨어 오류로 인해 종료된 경우입니다.  
-   계획된 재배치  
-   예약된 디스크 유지 관리를 위한 재배치  
  
자세한 내용은 참조 [데이터베이스 파일 이동](../../relational-databases/databases/move-database-files.md)합니다.  
  
## <a name="initializing-files"></a>파일 초기화  
기본적으로 데이터 및 로그 파일은 사용자가 다음 작업 중 하나를 수행할 때 0으로 채워져 초기화됩니다.  
  
-   데이터베이스를 만듭니다.   
-   기존 데이터베이스에 파일 추가   
-   기존 파일의 크기 증가   
-   데이터베이스 또는 파일 그룹을 복원합니다.   
  
데이터 파일을 즉시 초기화할 수 있습니다. 이를 통해 이와 같은 파일 작업을 신속히 실행할 수 있습니다. 자세한 내용은 [데이터베이스 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)를 참조하세요. 
  
## <a name="removing-a-filestream-container"></a>FILESTREAM 컨테이너 제거  
 "DBCC SHRINKFILE" 작업을 사용하여 FILESTREAM 컨테이너를 비웠어도 데이터베이스에서 여러 가지 시스템 유지 관리상의 이유로 삭제된 파일에 대한 참조를 보존해야 하는 경우가 있습니다. [sp_filestream_force_garbage_collection&#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) 안전 하 게 되었을 때 이러한 파일을 제거 하려면 FILESTREAM 가비지 수집기가 실행 됩니다. FILESTREAM 가비지 수집기가 FILESTREAM 컨테이너에서 모든 파일을 제거하지 않은 경우 FILESTREAM 컨테이너를 제거하기 위한 ALTER DATABASEREMOVE FILE 작업이 실패하고 오류를 반환합니다. 다음 프로세스를 사용하여 FILESTREAM 컨테이너를 제거하는 것이 좋습니다.  
  
1.  실행 [DBCC shrinkfile&#40; Transact SQL &#41; ](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) 이 컨테이너의 활성 내용을 다른 컨테이너로 이동 하려면 EMPTYFILE 옵션을 사용 합니다.  
  
2.  FULL 또는 BULK_LOGGED 복구 모델에서 로그 백업이 수행되었는지 확인합니다.  
  
3.  복제 로그 판독기 작업이 실행되었는지 확인합니다(해당되는 경우).  
  
4.  실행 [sp_filestream_force_garbage_collection &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) 이 컨테이너에 더 이상 필요 없는 모든 파일을 삭제 하 여 가비지 수집기를 합니다.  
  
5.  ALTER DATABASE를 REMOVE FILE 옵션과 함께 실행하여 이 컨테이너를 제거합니다.  
  
6.  2-4단계를 두 번 이상 반복하여 가비지 수집을 완료합니다.  
  
7.  ALTER Database...REMOVE FILE을 사용하여 이 컨테이너를 제거합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-adding-a-file-to-a-database"></a>1. 데이터베이스에 파일 추가  
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
  
### <a name="b-adding-a-filegroup-with-two-files-to-a-database"></a>2. 데이터베이스에 두 개의 파일이 포함된 파일 그룹 추가  
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
  
### <a name="c-adding-two-log-files-to-a-database"></a>3. 데이터베이스에 두 개의 로그 파일 추가  
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
  
### <a name="d-removing-a-file-from-a-database"></a>4. 데이터베이스에서 파일 제거  
 다음 예에서는 2번 예에서 추가한 파일 중 하나를 제거합니다.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4;  
GO  
```  
  
### <a name="e-modifying-a-file"></a>5. 파일 수정  
다음 예에서는 2번 예에서 추가한 파일 중 하나의 크기를 늘립니다.  
 ALTER DATABASE MODIFY FILE 명령 사용 하 여만 파일 크기를 더 크게 만들 수, 되므로 더 작은 파일 크기를 확인 해야 하는 경우 DBCC SHRINKFILE을 사용 해야 합니다.  
  
```sql  
USE master;  
GO
  
ALTER DATABASE AdventureWorks2012   
MODIFY FILE  
(NAME = test1dat3,  
SIZE = 200MB);  
GO  
```

이 예제에서는 100 MB을 데이터 파일의 크기를 축소 하 고이 금액에 크기를 지정 합니다. 

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
 
  
### <a name="f-moving-a-file-to-a-new-location"></a>6. 파일을 새 위치로 이동  
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
  
### <a name="g-moving-tempdb-to-a-new-location"></a>7. tempdb를 새 위치로 이동  
 다음 예에서는 `tempdb`를 디스크의 현재 위치에서 다른 디스크 위치로 이동합니다. MSSQLSERVER 서비스를 시작할 때마다 `tempdb`가 다시 생성되므로 데이터와 로그 파일을 물리적으로 이동할 필요는 없습니다. 3단계에서 서비스를 다시 시작할 때 파일이 생성됩니다. 서비스를 다시 시작하기 전까지는 `tempdb`가 기존의 위치에서 작업을 수행합니다.  
  
1.  `tempdb` 데이터베이스의 논리적 파일 이름 및 디스크에서 현재 위치를 결정합니다.  
  
    ```sql  
    SELECT name, physical_name  
    FROM sys.master_files  
    WHERE database_id = DB_ID('tempdb');  
    GO  
    ```  
  
2.  `ALTER DATABASE`를 사용하여 각 파일의 위치를 변경합니다.  
  
    ```sql  
    USE master;  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');  
    GO  
    ALTER DATABASE  tempdb   
    MODIFY FILE (NAME = templog, FILENAME = 'E:\SQLData\templog.ldf');  
    GO  
    ```  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 중지한 후 다시 시작합니다.  
  
4.  파일 변경 내용을 확인합니다.  
  
    ```sql  
    SELECT name, physical_name  
    FROM sys.master_files  
    WHERE database_id = DB_ID('tempdb');  
    ```  
  
5.  tempdb.mdf 및 templog.ldf 파일을 원래 위치에서 삭제합니다.  
  
### <a name="h-making-a-filegroup-the-default"></a>8. 기본 파일 그룹 설정  
 다음 예제에서는 `Test1FG1` 기본 파일 그룹 B의 예제에서 만든 파일 그룹입니다. 그 다음 `PRIMARY` 파일 그룹을 기본 파일 그룹으로 다시 설정합니다. `PRIMARY`는 대괄호 또는 따옴표로 구분해야 합니다.  
  
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
  
### <a name="i-adding-a-filegroup-using-alter-database"></a>9. ALTER DATABASE를 사용하여 파일 그룹 추가  
 다음 예에서는 `FILEGROUP` 절을 포함하는 `FILESTREAM`을 `FileStreamPhotoDB` 데이터베이스에 추가합니다.  
  
```sql  
--Create and add a FILEGROUP that CONTAINS the FILESTREAM clause to  
--the FileStreamPhotoDB database.  
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
        
### <a name="j-change-filegroup-so-that-when-a-file-in-the-filegroup-meets-the-autogrow-threshold-all-files-in-the-filegroup-grow"></a>10. 파일 그룹을 변경 하는 파일 그룹의 파일이 자동 증가 임계값을 충족할 때에서는 파일 그룹의 모든 파일이 증가
 다음 예제에서는 필요한 `ALTER DATABASE` 으로 읽기 / 쓰기 파일 그룹을 수정 하는 문을 `AUTOGROW_ALL_FILES` 설정 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [sp_spaceused&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.data_spaces &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Binary Large Object &#40;Blob&#41; 데이터 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [DBCC SHRINKFILE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)   
 [sp_filestream_force_garbage_collection&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)  
 [데이터베이스 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)    
  
  
