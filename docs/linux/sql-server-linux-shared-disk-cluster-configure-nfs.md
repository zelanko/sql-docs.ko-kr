---
title: 장애 조치 클러스터 인스턴스 저장소 NFS-Linux의 SQL Server 구성 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 63ebce5a8e78829cbdad8dede0be7cb9285c7c37
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788461"
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>장애 조치 클러스터 인스턴스-NFS-Linux의 SQL Server 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux에서 장애 조치 클러스터 인스턴스 (FCI)에 대 한 NFS 저장소를 구성 하는 방법에 설명 합니다. 

NFS 또는 네트워크 파일 시스템에는 Linux 분야 에서만 하나 Windows 없습니다 디스크를 공유 하는 것에 대 한 일반적인 메서드입니다. ISCSI와 마찬가지로, NFS 구성할 수 있습니다 서버 또는 일종의 어플라이언스 또는 저장 단위에 SQL Server에 대 한 저장소 요구 사항을 충족 하기만 합니다.

## <a name="important-nfs-server-information"></a>중요 한 NFS 서버 정보

NFS (Linux 서버 또는 다른)를 호스트 하는 소스를 사용 하 여/호환 4.2 이상 버전 이어야 합니다. 이전 버전 SQL Server on Linux 사용 하 여 작동 하지 않습니다.

NFS 서버에서 공유에 폴더를 구성할 때 이러한 지침의 일반 옵션을 따르는 있는지 확인 합니다.
- `rw` 폴더 되도록 수에서 읽고 쓸
- `sync` 보장 된 쓰기 폴더를 확인 하려면
- 사용 하지 않는 `no_root_squash` ; 옵션으로 보안 위험으로 간주 됩니다
- 폴더에 대 한 모든 권한 (777) 적용 되었는지 확인

에 액세스 하기 위한 보안 표준을 사항이 적용 되도록 확인 합니다. 폴더를 구성 해야 하는 경우 FCI에 참여 하는 서버 에서만 NFS 폴더를 표시 됩니다. NFS Linux 기반 솔루션에서 수정 된 /etc/exports의 예는 폴더의 FCIN1 FCIN2를 제한 하는 다음과 같습니다.

![05 nfsacl][1]

## <a name="instructions"></a>Instructions

1. FCI 구성에 참여 하는 서버 중 하나를 선택 합니다. 어떤 것은 중요 하지 않습니다. 

2. 서버는 mount(s) NFS 서버에서 볼 수 있는지 확인 합니다.

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer >는 사용 하고자 하는 NFS 서버의 IP 주소입니다.

3. 시스템 데이터베이스 또는 기본 데이터 위치에 저장 된 모든 것에 대해 다음이 단계를 수행 합니다. 그렇지 않을 경우 4 단계로 건너뜁니다.
 
   * SQL Server에서 작업 하는 서버에서 중지 되었는지 확인 합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * Superuser를 완벽 하 게 전환 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    sudo -i
    ```

   * Mssql 사용자 전환 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    su mssql
    ```

   * SQL Server 데이터를 저장 하 고 로그 파일을 임시 디렉터리를 만듭니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > 폴더의 이름입니다. 다음 예제에서는 /var/opt/mssql/tmp 라는 폴더를 만듭니다.

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * SQL Server 데이터 및 로그 파일을 임시 디렉터리에 복사 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > 이전 단계에서 폴더의 이름입니다.

   * 파일 디렉터리 인지 확인 합니다.

    ```bash
    ls TempDir
    ```

    \<TempDir > d 단계에 있는 폴더의 이름입니다.

   * 기존 SQL Server 데이터 디렉터리에서 파일을 삭제 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   * 파일이 삭제 되었는지 확인 합니다. 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * 루트 사용자로 다시 전환 하려면 exit를 입력 합니다.

   * SQL Server 데이터 폴더에 NFS 공유를 탑재 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer >는 사용 하고자 하는 NFS 서버의 IP 주소 

    \<FolderOnNFSServer > NFS 공유의 이름입니다. 2 단계에서에서 NFS 정보와 일치 하는 다음 예제 구문입니다.

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * 스위치 없이 탑재를 실행 하 여 탑재 되었는지 확인 합니다.

    ```bash
    mount
    ```

    ![10 mountnoswitches][2]

   * Mssql 사용자로 전환 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    su mssql
    ```

   * 임시 디렉터리 /var/opt/mssql/data에서 파일을 복사 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * 파일 위치에 있는지 확인 합니다.

    ```bash
    ls /var/opt/mssql/data
    ```

   * 종료 되지 않고 mssql를 입력 합니다. 
    
   * 종료 되지 않고 루트를 입력 합니다.

   * SQL Server를 시작 합니다. 모든 항목이 올바르게 복사 되었는지 하 고 적용 하는 보안 올바르게 SQL Server 해야 표시 시작 합니다.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * 보안 제대로 설정 되어 있는지를 테스트 하려면 데이터베이스를 만듭니다. 다음 예제에서는 TRANSACT-SQL;를 통해 수행 되는 SSMS를 통해 수행할 수 있습니다.
 
    ![CreateTestdatabase][3]

   * SQL Server를 중지 하 고 종료 하는 것이 것을 확인 합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * 다른 NFS 탑재를 만들지 않는 경우 공유를 마운트 해제 합니다. 인 경우 분리 하지 않도록 합니다.

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer >는 사용 하고자 하는 NFS 서버의 IP 주소

    \<FolderOnNFSServer > NFS 공유의 이름

    \<FolderMountedIn >는 이전 단계에서 만든 폴더입니다. 

4. 사용자 데이터베이스 백업 등의 시스템 데이터베이스 이외의 항목에 대 한 다음이 단계를 수행 합니다. 기본 위치를 사용 하는 경우 5 단계로 건너뜁니다.

   * Superuser를 스위치입니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

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

   * 이전 단계에서 만든 폴더에 NFS 공유를 탑재 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer >는 사용 하고자 하는 NFS 서버의 IP 주소

    \<FolderOnNFSServer > NFS 공유의 이름

    \<FolderToMountIn >는 이전 단계에서 만든 폴더입니다. 예제는 다음과 같습니다. 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * 스위치 없이 탑재를 실행 하 여 탑재 되었는지 확인 합니다.
  
   * Superuser를 더 이상 exit를 입력 합니다.

   * 를 테스트 하려면 해당 폴더에 데이터베이스를 만듭니다. 다음 예제에서는 sqlcmd를 사용 하 여 데이터베이스 만들기, 컨텍스트 전환, OS 수준에 있는 파일과 다음 임시 위치를 삭제를 확인 합니다. SSMS를 사용할 수 있습니다.

    ![15 createtestdatabase][4]
 
   * 공유 마운트 해제 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer >는 사용 하고자 하는 NFS 서버의 IP 주소
    
    \<FolderOnNFSServer > NFS 공유의 이름

    \<FolderMountedIn >는 이전 단계에서 만든 폴더입니다. 예제는 다음과 같습니다. 
 
5. 다른 노드에 대 한 단계를 반복 합니다.


## <a name="next-steps"></a>다음 단계

[장애 조치 클러스터 인스턴스-Linux의 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
