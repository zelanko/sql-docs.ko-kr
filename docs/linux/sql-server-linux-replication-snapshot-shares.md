---
title: 스냅샷 폴더 공유 구성
titleSuffix: SQL Server on Linux
description: Linux에서 스냅샷 폴더 공유 SQL Server 복제를 구성하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c5deaf7fbe62b30140f476a37ad096d080e00c49
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558358"
---
# <a name="configure-replication-snapshot-folder-with-shares"></a>공유를 사용하여 복제 스냅샷 폴더 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

스냅샷 폴더는 공유로 지정한 디렉터리이며 이 폴더에 읽기/쓰기 작업을 수행하려면 에이전트에게 충분한 액세스 권한이 있어야 합니다.

![복제 다이어그램][1]

### <a name="replication-snapshot-folder-share-explained"></a>복제 스냅샷 폴더 공유 설명

예제에 앞서, SQL Server가 복제에 samba 공유를 사용 하는 방법을 살펴보겠습니다. 이 방법이 작동하는 방식의 기본 예제는 다음과 같습니다.

1. Samba 공유는 게시자의 복제 에이전트가 `/local/path1`에 쓴 파일을 구독자가 볼 수 있도록 구성됩니다.
2. 배포 서버에서 게시자를 설정할 때 공유 경로를 사용하도록 SQL Server가 구성되므로 모든 인스턴스가 `//share/path`를 볼 수 있습니다.
3. SQL Server는 `//share/path`에서 로컬 경로를 찾아 파일을 찾을 위치를 파악합니다.
4. SQL Server는 samba 공유에서 지원하는 로컬 경로에 읽고 씁니다.


## <a name="configure-a-samba-share-for-the-snapshot-folder"></a>스냅샷 폴더의 samba 공유 구성 

복제 에이전트는 다른 컴퓨터의 스냅샷 폴더에 액세스하기 위해 복제 호스트 간에 공유 디렉터리가 필요합니다. 예를 들어, 트랜잭션 끌어오기 복제에서 배포 에이전트는 구독자에 상주하며, 아티클을 가져오기 위해 배포자에 액세스해야 합니다. 이 섹션에서는 두 개의 복제 호스트에서 samba 공유를 구성하는 방법의 예를 살펴보겠습니다.


## <a name="steps"></a>단계

예를 들어, Samba를 사용하여 호스트 1(배포자)의 스냅샷 폴더를 호스트 2(구독자)와 공유하도록 구성합니다. 

### <a name="install-and-start-samba-on-both-machines"></a>두 컴퓨터에서 Samba 설치 및 시작 

Ubuntu:

```bash
sudo apt-get -y install samba
sudo service smbd restart
```

RHEL:

```bash
sudo yum install samba
sudo service smb start
sudo service smb status
```

### <a name="on-host-1-distributor-set-up-the-samba-share"></a>호스트 1(배포자)에서 Samba 공유 설정 

1. samba의 사용자 및 암호를 설정합니다.

  ```bash
  sudo smbpasswd -a mssql 
  ```

1. 다음 항목을 포함하도록 `/etc/samba/smb.conf`를 편집하고 *share_name* 및 *path* 필드를 입력합니다.
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

### <a name="on-host-2-subscriber--mount-the-samba-share"></a>호스트 2(구독자)에서 Samba 공유 탑재

올바른 경로를 사용하여 명령을 편집하고 machine2에서 다음 명령을 실행합니다.

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

### <a name="on-both-hosts--configure-sql-server-on-linux-instances-to-use-snapshot-share"></a>두 호스트에서 스냅샷 공유를 사용하도록 Linux의 SQL Server 인스턴스 구성

두 컴퓨터의 `mssql.conf`에 다음 섹션을 추가합니다. //share/path에 대해 samba 공유를 사용합니다. 이 예제에서는 `//host1/mssql_data`입니다.

  ```bash
  [uncmapping]
  //share/path = /local/path/on/hosts/
  ```

  **예제**

  host1:

  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/1
  ```

  host2:
  
  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/2
  ```

### <a name="configuring-publisher-with-shared-paths"></a>공유 경로를 사용하여 게시자 구성

* 복제를 설정할 때 공유 경로를 사용합니다(예: `//host1/mssql_data`).
* `//host1/mssql_data`를 로컬 디렉터리와 `mssql.conf`에 추가된 매핑에 매핑합니다.

## <a name="next-steps"></a>다음 단계

[개념: Linux의 SQL Server 복제](sql-server-linux-replication.md)

[복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)

[1]: ./media/sql-server-linux-replication-snapshot-shares/image1.png
