---
title: NFS 스토리지 FCI 구성 - SQL Server on Linux
description: SQL Server on Linux에 NFS 스토리지를 사용하여 FCI(장애 조치 클러스터 인스턴스)를 구성하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 06cd2218a2a194ab3345fc9ed00ae40e17f0141d
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784880"
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>장애 조치(failover) 클러스터 인스턴스 구성 - NFS - SQL Server on Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 Linux에서 FCI(장애 조치(failover) 클러스터 인스턴스)에 NFS 스토리지를 구성하는 방법을 설명합니다. 

NFS(네트워크 파일 시스템)는 Linux 환경에서 디스크를 공유하는 일반적인 방법이지만, Windows 환경에서는 그렇지 않습니다. iSCSI와 비슷하게 NFS는 SQL Server에 대한 스토리지 요구 사항을 충족하는 경우 서버 또는 일종의 어플라이언스나 스토리지 단위에서 구성할 수 있습니다.

## <a name="important-nfs-server-information"></a>중요한 NFS 서버 정보

원본 호스팅 NFS(Linux 서버 또는 기타)는 버전 4.2 이상을 사용 중이거나 이 버전의 규격이어야 합니다. 이전 버전은 SQL Server on Linux에서 작동하지 않습니다.

NFS 서버에서 공유할 폴더를 구성하는 경우 이 지침의 일반 옵션을 따라야 합니다.
- `rw` - 폴더를 읽고 쓸 수 있는지 확인합니다.
- `sync` - 폴더에 대한 쓰기가 보장되는지 확인합니다.
- `no_root_squash`를 옵션으로 사용하지 마세요. 보안 위험으로 간주됩니다.
- 폴더에 전체 권한(777)이 적용되었는지 확인합니다.

액세스에 보안 표준이 적용되는지 확인합니다. 폴더를 구성하는 경우 FCI에 참여하는 서버에서만 NFS 폴더를 볼 수 있는지 확인합니다. Linux 기반 NFS 솔루션에 대한 수정된 /etc/exports의 예는 다음과 같이 표시됩니다. 여기서 폴더는 FCIN1 및 FCIN2로 제한됩니다.

![05-nfsacl][1]

## <a name="instructions"></a>Instructions

1. FCI 구성에 참여할 서버 중 하나를 선택합니다. 어떤 서버를 선택하든 상관이 없습니다. 

2. 서버에서 NFS 서버의 탑재를 볼 수 있는지 확인합니다.

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer>는 사용하려는 NFS 서버의 IP 주소입니다.

3. 시스템 데이터베이스 또는 기본 데이터 위치에 저장된 항목의 경우 다음 단계를 수행합니다. 그렇지 않은 경우 4단계로 건너뜁니다.
 
   * 작업 중인 서버에서 SQL Server가 중지되었는지 확인합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * 슈퍼 사용자로 완전히 전환합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    sudo -i
    ```

   * mssql 사용자로 전환합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    su mssql
    ```

   * SQL Server 데이터와 로그 파일을 저장할 임시 디렉터리를 만듭니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir>는 폴더 이름입니다. 다음 예제에서는 /var/opt/mssql/tmp라는 폴더를 만듭니다.

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * SQL Server 데이터와 로그 파일을 임시 디렉터리에 복사합니다. 성공하는 경우 승인이 수신되지 않습니다.
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir>는 이전 단계의 폴더 이름입니다.

   * 파일이 디렉터리에 있는지 확인합니다.

    ```bash
    ls TempDir
    ```

    \<TempDir>는 d 단계의 폴더 이름입니다.

   * 기존 SQL Server 데이터 디렉터리에서 파일을 삭제합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   * 파일이 삭제되었는지 확인합니다. 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * exit를 입력하여 다시 루트 사용자로 전환합니다.

   * SQL Server 데이터 폴더에 NFS 공유를 탑재합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer>는 사용하려는 NFS 서버의 IP 주소입니다. 

    \<FolderOnNFSServer>는 NFS 공유의 이름입니다. 다음 예제 구문은 2단계의 NFS 정보와 일치합니다.

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * 스위치 없이 mount를 실행하여 탑재에 성공했는지 확인합니다.

    ```bash
    mount
    ```

    ![10-mountnoswitches][2]

   * mssql 사용자로 전환합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    su mssql
    ```

   * 임시 디렉터리 /var/opt/mssql/data에서 파일을 복사합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * 파일이 있는지 확인합니다.

    ```bash
    ls /var/opt/mssql/data
    ```

   * exit를 입력하여 mssql을 종료합니다. 
    
   * exit를 입력하여 루트를 종료합니다.

   * SQL Server를 시작합니다. 모든 항목이 올바르게 복사되고 보안이 올바르게 적용된 경우 SQL Server가 시작됨으로 표시되어야 합니다.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * 데이터베이스를 만들어 보안이 제대로 설정되었는지 테스트합니다. 다음 예제에서는 Transact-SQL을 통해 수행되는 작업을 보여 줍니다. SSMS를 통해 수행할 수 있습니다.
 
    ![CreateTestdatabase][3]

   * SQL Server를 중지하고 종료되었는지 확인합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * 다른 NFS 탑재를 만들지 않는 경우 공유를 분리합니다. 만드는 경우에는 분리하지 마세요.

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer>는 사용하려는 NFS 서버의 IP 주소입니다.

    \<FolderOnNFSServer>는 NFS 공유의 이름입니다.

    \<FolderMountedIn>은 이전 단계에서 만든 폴더입니다. 

4. 시스템 데이터베이스가 아닌 사용자 데이터베이스 또는 백업과 같은 항목의 경우 다음 단계를 수행합니다. 기본 위치만 사용하는 경우에는 5단계로 건너뜁니다.

   * 슈퍼 사용자로 전환합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    sudo -i
    ```

   * SQL Server에서 사용할 폴더를 만듭니다. 

    ```bash
    mkdir <FolderName>
    ```

    \<FolderName>은 폴더 이름입니다. 올바른 위치에 없으면 폴더의 전체 경로를 지정해야 합니다. 다음 예제에서는 /var/opt/mssql/userdata라는 폴더를 만듭니다.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * 이전 단계에서 만든 폴더에 NFS 공유를 탑재합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer>는 사용하려는 NFS 서버의 IP 주소입니다.

    \<FolderOnNFSServer>는 NFS 공유의 이름입니다.

    \<FolderToMountIn>은 이전 단계에서 만든 폴더입니다. 예를 들면 다음과 같습니다. 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * 스위치 없이 mount를 실행하여 탑재에 성공했는지 확인합니다.
  
   * exit를 입력하여 슈퍼 사용자를 종료합니다.

   * 테스트하려면 해당 폴더에 데이터베이스를 만듭니다. 다음 예제에서는 sqlcmd를 사용하여 데이터베이스를 만들고 컨텍스트를 해당 데이터베이스로 전환한 다음, 파일이 OS 수준에 있는지 확인하고 임시 위치를 삭제합니다. SSMS를 사용할 수 있습니다.

    ![15-createtestdatabase][4]
 
   * 공유를 분리합니다. 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer>는 사용하려는 NFS 서버의 IP 주소입니다.
    
    \<FolderOnNFSServer>는 NFS 공유의 이름입니다.

    \<FolderMountedIn>은 이전 단계에서 만든 폴더입니다. 예를 들면 다음과 같습니다. 
 
5. 다른 노드에 대해 단계를 반복합니다.


## <a name="next-steps"></a>다음 단계

[장애 조치(failover) 클러스터 인스턴스 구성 - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
