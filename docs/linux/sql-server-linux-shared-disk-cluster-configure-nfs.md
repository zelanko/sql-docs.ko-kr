---
title: 장애 조치 클러스터 인스턴스 저장소 NFS-Linux에서 SQL Server 구성 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 62cce3bc883321df820a6f5b9eb45e7359498e24
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>장애 조치 클러스터 인스턴스-NFS-Linux에서 SQL Server 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서는 Linux에서 장애 조치 클러스터 인스턴스 (FCI)에 대 한 NFS 저장소를 구성 하는 방법을 설명 합니다. 

NFS 또는 네트워크 파일 시스템은 Linux 세계 있지만 Windows 하나 하지의 디스크를 공유 하는 데 일반적인 방법입니다. ISCSI와 마찬가지로, NFS 구성할 수 있습니다 일종의 어플라이언스 또는 저장 장치 또는 서버에서 SQL Server에 대 한 저장소 요구를 충족 합니다.

## <a name="important-nfs-server-information"></a>중요 한 NFS 서버 정보

NFS (Linux 서버 또는 다른 요소)를 호스트 하는 소스를 사용 하 여/준수 해야 4.2 이상 버전으로 있습니다. 이전 버전 Linux에서 SQL Server와 함께 작동 하지 않습니다.

NFS 서버에서 공유 하는 폴더를 구성할 때 이러한 지침 일반 옵션에 따라 있는지 확인 합니다.
- `rw` 폴더 되도록 할 수에서 읽고 쓸 수를
- `sync` 폴더에 대 한 쓰기를 보장 하려면
- 사용 하지 마십시오 `no_root_squash` ; 옵션으로 보안 위험으로 간주 됩니다
- 폴더에 대 한 모든 권한 (777) 적용 되었는지 확인

에 액세스 하기 위한 보안 표준을 적용 되도록 확인 합니다. 폴더를 구성 해야 하는 FCI에 참여 하는 서버만 NFS 폴더를 표시 되어야 합니다. Linux 기반 NFS 솔루션에 대해 수정 된 /etc/exports의 예로 폴더의 FCIN1와 FCIN2에만 다음과 같습니다.

![05 nfsacl][1]

## <a name="instructions"></a>Instructions

1. FCI 구성에 참여 하는 서버 중 하나를 선택 합니다. 어떤 것은 중요 하지 않습니다. 

2. 서버는 mount(s) NFS 서버에서 볼 수 있는지 확인 합니다.

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer >는 사용 하고자 하는 NFS 서버의 IP 주소입니다.

3. 시스템 데이터베이스 또는 기본 데이터 위치에 저장 된 모든 항목에 대해 다음이 단계를 수행 합니다. 그렇지 않은 경우 4 단계로 건너뜁니다.
 
   * SQL Server에서 작업 하는 서버에서 중지 되었는지 확인 합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * 스위치는 superuser를 완벽 하 게 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    sudo -i
    ```

   * Mssql 사용자 전환 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    su mssql
    ```

   * SQL Server 데이터를 저장 및 로그 파일을 임시 디렉터리를 만듭니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > 폴더의 이름입니다. 다음 예제에서는 /var/opt/mssql/tmp 라는 폴더를 만듭니다.

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * SQL Server 데이터 및 로그 파일을 임시 디렉터리에 복사 합니다. 성공 하는 경우에 승인을 받지 못합니다.
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir >의 이전 단계에서 폴더의 이름입니다.

   * 파일 디렉터리에 있는지 확인 합니다.

    ```bash
    ls TempDir
    ```

    \<TempDir > d 단계에 있는 폴더의 이름입니다.

   * 기존 SQL Server 데이터 디렉터리에서 파일을 삭제 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   * 파일 삭제를 확인 합니다. 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * 루트 사용자로 다시 전환 하려면 exit를 입력 합니다.

   * NFS 공유 SQL Server 데이터 폴더에 탑재 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer >는 사용 하고자 하는 NFS 서버의 IP 주소 

    \<FolderOnNFSServer > NFS 공유 이름입니다. 다음 예에서는 구문을 2 단계에서에서 NFS 정보를 찾습니다.

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * 스위치 없이 탑재를 실행 하 여 탑재 성공 했음을 확인 합니다.

    ```bash
    mount
    ```

    ![10 mountnoswitches][2]

   * Mssql 사용자로 전환 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    su mssql
    ```

   * 임시 디렉터리 /var/opt/mssql/data에서 파일을 복사 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * 파일이 있는지 확인 합니다.

    ```bash
    ls /var/opt/mssql/data
    ```

   * 종료 되지 않고 mssql를 입력 합니다. 
    
   * 종료 되지 않고 루트를 입력 합니다.

   * SQL Server를 시작 합니다. 모든 항목이 올바르게 복사 하 고 적용 된 보안 올바르게 SQL Server 해야 표시 시작 될 때입니다.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * 보안 제대로 설정 되어 있는지를 테스트 하려면 데이터베이스를 만듭니다. 다음 예제에서는 TRANSACT-SQL을 통해 수행 되 고 SSMS를 통해 수행할 수 있습니다.
 
    ![CreateTestdatabase][3]

   * SQL Server를 중지 하 고 종료 되었는지 확인 합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * 다른 NFS 탑재를 만들지 않는 경우 공유를 마운트 해제 합니다. 인 경우 해제 하지 않습니다.

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer >는 사용 하고자 하는 NFS 서버의 IP 주소

    \<FolderOnNFSServer > NFS 공유의 이름

    \<FolderMountedIn >는 이전 단계에서 만든 폴더입니다. 

4. 사용자 데이터베이스 또는 백업 등의 시스템 데이터베이스가 아닌 다른 항목에 대 한 다음이 단계를 수행 합니다. 기본 위치를 사용 하 여만 5 단계로 건너뜁니다.

   * 전환의 superuser 이어야 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    sudo -i
    ```

   * SQL Server에서 사용 될 폴더를 만듭니다. 

    ```bash
    mkdir <FolderName>
    ```

    \<폴더 이름 > 폴더의 이름입니다. 폴더의 전체 경로 지정 해야 합니다. 올바른 위치에 없는 경우. 다음 예제에서는 /var/opt/mssql/userdata 라는 폴더를 만듭니다.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * NFS 공유 이전 단계에서 만든 폴더에 탑재 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer >는 사용 하고자 하는 NFS 서버의 IP 주소

    \<FolderOnNFSServer > NFS 공유의 이름

    \<FolderToMountIn >는 이전 단계에서 만든 폴더입니다. 다음은 예제입니다. 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * 스위치 없이 탑재를 실행 하 여 탑재 성공 했음을 확인 합니다.
  
   * 더 이상 수는 superuser exit를 입력 합니다.

   * 를 테스트 하려면 해당 폴더에 데이터베이스를 만듭니다. 다음 예제에서는 sqlcmd를 사용 하 여 데이터베이스를 만들, 컨텍스트를 전환할 OS 수준에 있는 파일과 임시 위치를 삭제 한 다음 확인 합니다. SSMS를 사용할 수 있습니다.

    ![15 createtestdatabase][4]
 
   * 공유를 마운트 해제 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer >는 사용 하고자 하는 NFS 서버의 IP 주소
    
    \<FolderOnNFSServer > NFS 공유의 이름

    \<FolderMountedIn >는 이전 단계에서 만든 폴더입니다. 다음은 예제입니다. 
 
5. 다른 노드에서에서 단계를 반복 합니다.


## <a name="next-steps"></a>다음 단계

[장애 조치 클러스터 인스턴스-Linux에서 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
