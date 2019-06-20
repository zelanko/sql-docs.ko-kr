---
title: Linux에서 스냅숏 폴더 공유 SQL Server 복제 구성 | Microsoft Docs
description: 이 문서에서는 Linux에서 스냅숏 폴더 공유 SQL Server 복제를 구성 하는 방법을 설명 합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7569eaf92484038e998595405df42dd1f2d31b3d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718159"
---
# <a name="configure-replication-snapshot-folder-with-shares"></a>복제 스냅숏 폴더를 공유로 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

공유;로 지정한 디렉터리가 스냅숏 폴더 이 폴더에서 읽고 있는 에이전트에 액세스할 수 있는 권한이 있어야 합니다.

![복제 다이어그램][1]

### <a name="replication-snapshot-folder-share-explained"></a>복제 스냅숏 폴더 공유 설명

예 전에 SQL Server 복제에서 samba 공유를 사용 하는 방법을 통해 확인해 보겠습니다. 다음은이 과정의 기본적인 예입니다.

1. Samba 공유 되는 구성 파일에 기록 `/local/path1` 복제 하 여 게시자에 에이전트에서 확인할 수 있습니다 구독자
2. SQL Server가 모든 인스턴스를 확인할 수 있도록 배포 서버에 게시자를 설정 하는 경우 공유 경로 사용 하도록 구성 합니다 `//share/path`
3. SQL Server의 로컬 경로 찾습니다는 `//share/path` 파일을 검색할 수 있는 위치를 알아야
4. Samba 공유에서 지원 되는 로컬 경로에 SQL Server 읽기/쓰기


## <a name="configure-a-samba-share-for-the-snapshot-folder"></a>스냅숏 폴더에 대 한 samba 공유를 구성 합니다. 

복제 에이전트는 다른 컴퓨터에 스냅숏 폴더에 액세스할 수 있는 복제 호스트 사이 공유 디렉터리를 해야 합니다. 예를 들어 트랜잭션 끌어오기 복제에서 문서를 가져오기 위해 배포자에 대 한 액세스를 해야 하는 구독자에서 배포 에이전트가 상주 합니다. 이 섹션에서는 두 복제 호스트 samba 공유를 구성 하는 방법의 예제를 통해 살펴보겠습니다.


## <a name="steps"></a>단계

예를 들어 Samba를 사용 하 여 호스트 2 (구독자)를 사용 하 여 공유 하도록 호스트 1 (배포자)에서 스냅숏 폴더를 구성 합니다. 

### <a name="install-and-start-samba-on-both-machines"></a>설치 하 고 두 컴퓨터 모두에서 Samba 시작 

Ubuntu:

```bash
sudo apt-get -y install samba
sudo service smbd restart
```

RHEL의 경우:

```bash
sudo yum install samba
sudo service smb start
sudo service smb status
```

### <a name="on-host-1-distributor-set-up-the-samba-share"></a>Samba 공유 호스트 1 (배포자) 설정에서 

1. 사용자 설정 및 samba에 대 한 암호:

  ```bash
  sudo smbpasswd -a mssql 
  ```

1. 편집 된 `/etc/samba/smb.conf` 다음 항목을 포함 하 여 입력 합니다 *공유 이름* 및 *경로* 필드
 ```bash
  <[share_name]>
  path = </local/path/on/host/1>
  writable = yes
  create mask = 770
  directory mask 
  valid users = mssql 
  ```

  **예제**

  ```bash
  [mssql_data]    <- Name of the shared directory
  path = /var/opt/mssql/repldata <- location of directory we wish to share
  writable = yes  <- determines if the share is writable from other hosts
  create mask = 770  <- Linux permissions for files created 
  directory mask = 770 <- Linux permissions for directories created
  valid users = mssql   <- list of users who can login to this share
  ```

### <a name="on-host-2-subscriber--mount-the-samba-share"></a>2 (구독자) 호스트에서 Samba 공유를 탑재 합니다.

올바른 경로 사용 하 여 명령을 편집한 machine2에서 다음 명령을 실행 합니다.

  ```bash
  sudo mount //<name_of_host_1>/<share_name> </local/path/on/host/2> -o user=mssql,uid=mssql,gid=mssql
  ```

  **예제**

  ```bash
  mount //host1/mssql_data /var/opt/mssql/repldata_shared -o user=mssql,uid=mssql,gid=mssql

  user=mssql <- sets the login name for samba
  uid=mssql   <- makes the mssql user as the owner of the mounted directory
  gid=mssql   <- sets the mssql group as the owner of the mounted directory
  ```

### <a name="on-both-hosts--configure-sql-server-on-linux-instances-to-use-snapshot-share"></a>모두 호스트 구성의 SQL server 스냅숏 공유를 사용 하도록 Linux 인스턴스

다음 섹션을 추가 `mssql.conf` 두 컴퓨터 모두에서 합니다. 아무 곳에 나 사용 하 여 / / 공유/경로 대 한 samba 공유 합니다. 이 예에서 것 `//host1/mssql_data`

  ```bash
  [uncmapping]
  //share/path = /local/path/on/hosts/
  ```

  **예제**

  Host1에서:

  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/1
  ```

  Host2에:
  
  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/2
  ```

### <a name="configuring-publisher-with-shared-paths"></a>공유 경로 사용 하 여 게시자 구성

* 복제를 설정할 때 사용 하 여 공유 경로 (예: `//host1/mssql_data`
* 지도 `//host1/mssql_data` 로컬 디렉터리를 추가할 매핑을 `mssql.conf`합니다.

## <a name="next-steps"></a>다음 단계

[개념: Linux에서 SQL Server 복제](sql-server-linux-replication.md)

[복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)합니다.

[1]: ./media/sql-server-linux-replication-snapshot-shares/image1.png
