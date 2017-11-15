---
title: "데이터베이스 파일 및 파일 그룹 | Microsoft 문서"
ms.custom: 
ms.date: 10/11/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 73fde10c6cf318e5cd5c7eaa52a55a36f4d82001
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="database-files-and-filegroups"></a>데이터베이스 파일 및 파일 그룹
  모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에는 최소한 두 개의 운영 체제 파일인 데이터 파일과 로그 파일이 있습니다. 데이터 파일은 테이블, 인덱스, 저장 프로시저 및 뷰 등의 개체와 데이터를 포함합니다. 로그 파일은 데이터베이스의 모든 트랜잭션을 복구하는 데 필요한 정보를 포함합니다. 데이터 파일은 할당 및 관리를 간편하게 수행하기 위해 파일 그룹으로 그룹화할 수 있습니다.  
  
## <a name="database-files"></a>데이터베이스 파일  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에는 다음 표에 설명된 것처럼 세 가지 유형의 파일이 있습니다.  
  
|파일|설명|  
|----------|-----------------|  
|주|주 데이터 파일은 데이터베이스의 시작 정보를 포함하며 데이터베이스의 나머지 파일을 가리킵니다. 사용자 데이터와 개체를 이 파일에 저장하거나 보조 데이터 파일에 저장할 수 있습니다. 모든 데이터베이스에는 하나의 주 데이터 파일이 있습니다. 권장되는 주 데이터 파일 확장명은 .mdf입니다.|  
|보조|보조 데이터 파일은 선택적으로 사용하는 사용자 정의 데이터 파일이며 사용자 데이터를 저장합니다. 보조 파일은 각 파일을 서로 다른 디스크 드라이브에 배치하여 데이터를 여러 디스크에 분산시키는 데 사용할 수 있습니다. 또한 데이터베이스가 단일 Windows 파일의 최대 크기를 초과할 경우 보조 데이터 파일을 사용하여 데이터베이스 크기를 계속해서 늘릴 수 있습니다.<br /><br /> 권장되는 보조 데이터 파일 확장명은 .ndf입니다.|  
|트랜잭션 로그|트랜잭션 로그 파일은 데이터베이스 복구에 사용되는 로그 정보를 저장합니다. 데이터베이스마다 최소한 하나의 로그 파일이 있어야 합니다. 권장되는 트랜잭션 로그 파일 확장명은 .ldf입니다.|  
  
 예를 들어 모든 데이터와 개체를 하나의 주 파일에 저장하고 트랜잭션 로그 정보를 로그 파일에 저장하는 **Sales** 라는 단순한 데이터베이스를 만들 수 있습니다. 또는 한 개의 주 파일과 5개의 보조 파일을 포함하는 **Orders** 라는 더 복잡한 데이터베이스를 만들 수도 있습니다. 데이터베이스 내의 데이터와 개체는 6개의 파일에 분산되고 트랜잭션 로그 정보는 4개의 로그 파일에 포함됩니다.  
  
 기본적으로 데이터와 트랜잭션 로그는 동일한 드라이브와 경로에 배치됩니다. 이것은 단일 디스크 시스템의 경우에 해당하며 프로덕션 환경에서는 최적이 아닐 수도 있습니다. 데이터와 로그 파일은 서로 다른 디스크에 배치하는 것이 좋습니다.  

### <a name="logical-and-physical-file-names"></a>논리적 파일 이름과 물리적 파일 이름

SQL Server 파일은 다음과 같은 두 가지 이름을 갖습니다. 

**logical_file_name:**  logical_file_name은 모든 Transact-SQL 문에서 물리적 파일을 참조하는 데 사용되는 이름입니다. 논리적 파일 이름은 SQL Server 식별자 규칙을 따라야 하고 데이터베이스의 논리적 파일 이름 사이에서 고유해야 합니다.

**os_file_name:** os_file_name은 디렉터리 경로를 포함하는 물리적 파일의 이름입니다. 이 이름은 운영 체제 파일 이름의 규칙을 따라야 합니다.

FAT 또는 NTFS 파일 시스템에 SQL Server 데이터 파일 및 로그 파일을 배치할 수 있습니다. 보안상 NTFS 파일 시스템을 사용하는 것이 좋습니다. 읽기/쓰기 데이터 파일 그룹과 로그 파일은 NTFS 압축 파일 시스템에 배치할 수 없습니다. 읽기 전용 데이터베이스와 읽기 전용 보조 파일 그룹만 NTFS 압축 파일 시스템에 배치할 수 있습니다.

여러 SQL Server 인스턴스가 단일 시스템에서 실행될 때 각 인스턴스는 해당 인스턴스에서 생성된 데이터베이스에 대한 파일을 보관할 수 있는 서로 다른 기본 디렉터리를 받습니다. 자세한 내용은 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)참조하세요.

### <a name="data-file-pages"></a>데이터 파일 페이지

SQL Server 데이터 파일의 페이지는 첫째 페이지가 0으로 시작하여 순차적으로 번호가 매겨집니다. 데이터베이스의 파일마다 고유한 파일 ID 번호가 있습니다. 데이터베이스에서 페이지를 고유하게 식별하려면 해당 파일 ID와 페이지 번호가 모두 필요합니다. 다음 예에서는 4MB의 주 데이터 파일과 1MB의 보조 데이터 파일이 있는 데이터베이스의 페이지 번호를 보여 줍니다.

![data_file_pages](../../relational-databases/databases/media/data-file-pages.gif)

각 파일의 첫 페이지는 파일의 특성에 대한 정보를 포함하는 파일 헤더 페이지입니다. 또한 파일 시작 부분의 다른 여러 페이지에도 할당 맵과 같은 시스템 정보가 포함됩니다. 주 데이터 파일과 첫 번째 로그 파일에 모두 저장되는 시스템 페이지 중 하나는 데이터베이스의 특성에 대한 정보를 포함하는 데이터 부팅 페이지입니다. 페이지 및 페이지 유형에 대한 자세한 내용은 페이지 및 익스텐트 이해를 참조하세요.

### <a name="file-size"></a>파일 크기

SQL Server 파일은 원래 지정된 크기에서 자동으로 증가할 수 있습니다. 파일을 정의할 때 특정 증분을 지정할 수 있습니다. 파일이 가득 찰 때마다 증분에 따라 크기가 늘어납니다. 한 파일 그룹에 여러 파일이 있을 경우 모든 파일이 가득 찰 때까지 파일은 자동으로 증가하지 않습니다. 이 경우 라운드 로빈 방식으로 증가합니다.

각 파일의 최대 크기를 지정할 수도 있습니다. 최대 크기를 지정하지 않으면 파일은 디스크에서 사용 가능한 공간을 모두 사용할 때까지 계속 증가할 수 있습니다. 이 기능은 사용자가 시스템 관리자에 편리하게 액세스할 수 없는 응용 프로그램에 포함된 데이터베이스로 SQL Server를 사용할 때 특히 유용합니다. 사용자는 필요에 따라 파일이 자동으로 증가하게 하여 데이터베이스의 사용 가능한 공간을 모니터링하고 추가 공간을 수동으로 할당하는 관리 작업을 줄일 수 있습니다. 


## <a name="database-snapshot-files"></a>데이터베이스 스냅숏 파일

데이터베이스 스냅숏에서 쓰기 시 복사 데이터를 저장하기 위해 사용하는 파일 형식은 사용자가 스냅숏을 만들었는지 또는 스냅숏이 내부적으로 사용되는지에 따라 달라집니다.

* 사용자가 만든 데이터베이스 스냅숏은 하나 이상의 스파스 파일에 데이터를 저장합니다. 스파스 파일 기술은 NTFS 파일 시스템의 기능입니다. 처음에는 스파스 파일에 사용자 데이터가 없으며 사용자 데이터에 대한 디스크 공간이 스파스 파일에 할당되어 있지 않습니다. 데이터베이스 스냅숏의 스파스 파일 사용 및 데이터베이스 스냅숏 증가 방법에 대한 자세한 내용은 [데이터베이스 스냅숏 스파스 파일의 크기 보기](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)를 참조하세요. 
* 데이터베이스 스냅숏은 특정 DBCC 명령에 의해 내부적으로 사용됩니다. 이러한 명령에는 DBCC CHECKDB, DBCC CHECKTABLE, DBCC CHECKALLOC, DBCC CHECKFILEGROUP 등이 있습니다. 내부 데이터베이스 스냅숏은 원래 데이터베이스 파일의 스파스 대체 데이터 스트림을 사용합니다. 스파스 파일과 마찬가지로 대체 데이터 스트림은 NTFS 파일 시스템의 기능입니다. 스파스 대체 데이터 스트림을 사용하면 파일 크기나 볼륨 통계에 영향을 주지 않고 여러 데이터 할당을 하나의 파일 또는 폴더와 연결할 수 있습니다. 


  
## <a name="filegroups"></a>파일 그룹  
 모든 데이터베이스에는 주 파일 그룹이 한 개씩 있습니다. 주 파일 그룹은 주 데이터 파일과 다른 파일 그룹에 배치되지 않은 보조 파일을 포함합니다. 사용자 정의 파일 그룹을 만들어 데이터 파일을 그룹화함으로써 관리, 데이터 할당 및 배치를 간편하게 수행할 수 있습니다.  
  
 예를 들어 3개의 파일(Data1.ndf, Data2.ndf 및 Data3.ndf)을 3개의 디스크 드라이브에 하나씩 만들어서 **fgroup1**이라는 파일 그룹에 할당할 수 있습니다. 그런 다음 **fgroup1**파일 그룹에 한 개의 테이블을 만들 수 있습니다. 이렇게 하면 해당 테이블의 데이터에 대한 쿼리가 3개의 디스크로 분산되므로 성능이 향상됩니다. RAID(Redundant Array of Independent Disks) 스트라이프 세트에 단일 파일을 만들어 사용해도 이와 동일한 수준으로 성능이 향상될 수 있습니다. 그러나 파일과 파일 그룹을 사용하면 새 디스크에 새 파일을 쉽게 추가할 수 있습니다.  
  
 모든 데이터 파일은 다음 표에 나열된 파일 그룹에 저장됩니다.  
  
|파일 그룹|설명|  
|---------------|-----------------|  
|주|주 파일을 포함하는 파일 그룹. 주 파일 그룹에는 모든 시스템 테이블이 할당됩니다.|  
|사용자 정의|사용자가 데이터베이스를 처음 만들 때 또는 나중에 수정할 때 만드는 파일 그룹|  
  
### <a name="default-filegroup"></a>기본 파일 그룹  
 데이터베이스에서 개체를 만들 때 어떤 파일 그룹에 속하는지 지정하지 않으면 기본 파일 그룹에 할당됩니다. 언제든지 정확하게 하나의 파일 그룹이 기본 파일 그룹으로 지정됩니다. 기본 파일 그룹의 파일은 다른 파일 그룹에 할당되지 않은 모든 새로운 개체를 보관할 수 있을 만큼 크기가 커야 합니다.  
  
 PRIMARY 파일 그룹은 ALTER DATABASE 문을 사용하여 변경하지 않으면 기본 파일 그룹입니다. 시스템 개체 및 테이블에 대한 할당은 새 기본 파일 그룹이 아니라 PRIMARY 파일 그룹에 남게 됩니다.  

### <a name="file-and-filegroup-example"></a>파일 및 파일 그룹 예

다음 예에서는 SQL Server 인스턴스에서 데이터베이스를 만듭니다. 데이터베이스에는 주 데이터 파일, 사용자 정의 파일 그룹 및 로그 파일이 있습니다. 주 데이터 파일은 주 파일 그룹에 있으며 사용자 정의 파일 그룹에는 보조 데이터 파일이 두 개 있습니다. ALTER DATABASE 문을 통해 사용자 정의 그룹 파일이 기본 파일 그룹으로 지정됩니다. 그런 다음 사용자 정의 파일 그룹을 지정하여 테이블이 생성됩니다. (이 예에서는 일반 경로 `c:\Program Files\Microsoft SQL Server\MSSQL.1` 을 사용하여 SQL Server 버전 지정을 방지합니다.)

```
USE master;
GO
-- Create the database with the default data
-- filegroup and a log file. Specify the
-- growth increment and the max size for the
-- primary data file.
CREATE DATABASE MyDB
ON PRIMARY
  ( NAME='MyDB_Primary',
    FILENAME=
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_Prm.mdf',
    SIZE=4MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
FILEGROUP MyDB_FG1
  ( NAME = 'MyDB_FG1_Dat1',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_1.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
  ( NAME = 'MyDB_FG1_Dat2',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_2.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB)
LOG ON
  ( NAME='MyDB_log',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB.ldf',
    SIZE=1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB);
GO
ALTER DATABASE MyDB 
  MODIFY FILEGROUP MyDB_FG1 DEFAULT;
GO

-- Create a table in the user-defined filegroup.
USE MyDB;
CREATE TABLE MyTable
  ( cola int PRIMARY KEY,
    colb char(8) )
ON MyDB_FG1;
GO
```

다음 그림에서는 위 예제의 결과를 요약하여 보여 줍니다.

![filegroup_example](../../relational-databases/databases/media/filegroup-example.gif)
  
## <a name="related-content"></a>관련 내용  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
 [ALTER DATABASE 파일 및 파일 그룹 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
  
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
