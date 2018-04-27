---
title: 장애 조치 클러스터 인스턴스-Linux (RHEL)에서 SQL Server 구성 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.workload: Inactive
ms.openlocfilehash: 57f8f5d3881262ed96dcf84295b6c2a21dddc35d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="configure-failover-cluster-instance---sql-server-on-linux-rhel"></a>장애 조치 클러스터 인스턴스-Linux (RHEL)에서 SQL Server 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 공유 디스크 2 개 노드 장애 조치 클러스터 인스턴스의 가용성을 높이기 위한 서버 수준 중복을 제공합니다. 이 자습서에서는 Linux에서 SQL Server의 2 개 노드 장애 조치 클러스터 인스턴스를 만들려고 하는 방법에 설명 합니다. 작업을 완성 하는 구체적인 단계는 다음과 같습니다.

> [!div class="checklist"]
> * 설정 및 Linux 구성
> * SQL Server 설치 및 구성
> * 호스트 파일 구성
> * 공유 저장소를 구성 하 고 데이터베이스 파일 이동
> * 설치 하 고 각 클러스터 노드에서 Pacemaker 구성
> * 장애 조치 클러스터 인스턴스 구성

이 문서에서는 SQL Server에 대 한 공유 디스크 2 개 노드 장애 조치 클러스터 인스턴스 (FCI)를 만드는 방법을 설명 합니다. 문서는 Red Hat Enterprise Linux (RHEL)에 대 한 지침과 스크립트 예제 포함합니다. 스크립트 예제는 일반적으로 하므로 Ubuntu 분포는 RHEL 비슷합니다 Ubuntu 에서도 작동 합니다. 

개념 정보를 참조 하십시오. [SQL Server 장애 조치 클러스터 인스턴스 (FCI) linux](sql-server-linux-shared-disk-cluster-concepts.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소

다음과 같은 종단 간 시나리오를 완료 하려면 두 노드 클러스터와 저장소에 대 한 다른 서버를 배포 하는 두 개의 컴퓨터가 필요 합니다. 아래 단계 이러한 서버는 구성 하는 방법에 대해 간략하게 설명 합니다.

## <a name="set-up-and-configure-linux"></a>설정 및 Linux 구성

클러스터 노드에서 운영 체제를 구성 하는 첫 번째 단계가입니다. 클러스터의 각 노드에서 linux 배포를 구성 합니다. 두 노드에서 모두 같은 배포 및 버전을 사용 합니다. 하나 또는 다음 배포의 다른 사용 됩니다.
    
* HA 추가 기능에 대 한 유효한 구독으로 RHEL

## <a name="install-and-configure-sql-server"></a>SQL Server 설치 및 구성

1. 설치 하 고 두 노드에서 모두 SQL Server를 설정 합니다.  자세한 내용은 참조 [Linux에서 SQL Server 설치](sql-server-linux-setup.md)합니다.
1. 주 서버와 구성의 목적을 위해 보조로 다른으로 노드 하나를 지정 합니다. 다음에 대 한 이러한 용어를 사용 하 여이 가이드입니다.  
1. 보조 노드에서 중지 하 고 SQL Server를 사용 하지 않도록 설정 합니다.
    다음 예제에서는 중지 하 고 SQL Server를 사용 하지 않도록 설정 합니다. 
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE] 
    > 시간 설정, 서버 마스터 키를 SQL Server 인스턴스에 대 한 생성 했으며에 `var/opt/mssql/secrets/machine-key`합니다. Linux에서 SQL Server는 항상 mssql 라는 로컬 계정으로 실행 됩니다. 로컬 계정을 이기 때문에 해당 id 노드 간에 공유 되지 않습니다. 따라서 서버 마스터 키를 해독 하 여 각 로컬 mssql 계정에 액세스할 수 있도록 암호화 키를 주 노드에서 각 보조 노드로 복사 해야 합니다. 

1.  주 노드에서 Pacemaker에 대 한 SQL server 로그인을 만들고 실행에 로그인 권한을 부여 `sp_server_diagnostics`합니다. SQL Server를 실행 하는 노드를 확인 하려면이 계정을 사용 하는 pacemaker 합니다. 

    ```bash
    sudo systemctl start mssql-server
    ```
   
   SQL Server에 연결 `master` sa 계정을 사용 하 여 데이터베이스에 있으며 다음 실행:

   ```sql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```

   또는 더 세부적인 수준에서 권한을 설정할 수 있습니다. Pacemaker 로그인 필요 `VIEW SERVER STATE` sp_server_diagnostics와 쿼리 상태에 `setupadmin` 및 `ALTER ANY LINKED SERVER` sp_dropserver 및 sp_addserver 실행 하 여 리소스 이름으로의 FCI 인스턴스 이름을 업데이트 합니다. 

1. 주 노드에서 중지 하 고 SQL Server를 사용 하지 않도록 설정 합니다. 

## <a name="configure-the-hosts-file"></a>호스트 파일 구성

각 클러스터 노드의 호스트 파일을 구성 합니다. 호스트 파일은 IP 주소 및 모든 클러스터 노드의 이름이 포함 되어야 합니다.

1. 각 노드에 대 한 IP 주소를 확인 합니다. 다음 스크립트는 현재 노드의의 IP 주소를 보여 줍니다. 

    ```bash
    sudo ip addr show
    ```

1. 각 노드에서 다음 컴퓨터 이름을 설정 합니다. 각 노드의 고유한 이름을 15 자 이하인 합니다. 컴퓨터 이름을 추가 하 여 설정 `/etc/hosts`합니다. 다음 스크립트를 사용하면 `/etc/hosts`를 `vi`로 편집할 수 있습니다. 

   ```bash
   sudo vi /etc/hosts
   ```
   다음 예제와 `/etc/hosts` 라는 두 개의 노드에 대 한 추가 내용은 `sqlfcivm1` 및 `sqlfcivm2`합니다.

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

## <a name="configure-storage--move-database-files"></a>저장소를 구성 및 데이터베이스 파일 이동  

두 노드에서 액세스할 수 있는 저장소를 제공 해야 합니다. ISCSI, NFS 또는 SMB를 사용할 수 있습니다. 저장소 구성, 저장소는 클러스터 노드를 표시 하 고 새 저장소에 데이터베이스 파일을 이동 합니다. 다음 문서에서는 각 저장소 형식에 대 한 단계를 설명합니다.

- [장애 조치 클러스터 인스턴스-iSCSI-Linux에서 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [장애 조치 클러스터 인스턴스-NFS-Linux에서 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [SMB-Linux에서 SQL Server 장애 조치 클러스터 인스턴스-를 구성 합니다.](sql-server-linux-shared-disk-cluster-configure-smb.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>설치 하 고 각 클러스터 노드에서 Pacemaker 구성

1. 두 클러스터 노드에서 모두 Pacemaker 로그인을 위한 SQL Server 사용자 이름 및 암호를 저장할 파일을 만듭니다. 

    다음 명령은 이 파일을 만들고 채웁니다.

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd    
    ```

1. 두 클러스터 노드에서 모두 Pacemaker 방화벽 포트를 엽니다. `firewalld`를 사용하여 이러한 포트를 열려면 다음 명령을 실행합니다.

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > 기본 제공된 고가용성 구성이 없는 또 다른 방화벽을 사용 중인 경우 Pacemaker가 클러스터의 다른 노드와 통신할 수 있으려면 다음 포트를 열어야 합니다.
   >
   > * TCP: 포트 2224, 3121, 21064
   > * UDP: 포트 5405

1. 각 노드에 Pacemaker 패키지를 설치합니다.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
1. Pacemaker 및 Corosync 패키지를 설치할 때 생성된 기본 사용자의 암호를 설정합니다. 두 노드에서 모두 같은 암호를 사용합니다. 

   ```bash
   sudo passwd hacluster
   ```
1. `pcsd` 서비스 및 Pacemaker를 사용하도록 설정하고 시작합니다. 이렇게 하면 다시 시작된 후 노드가 클러스터에 다시 조인할 수 있습니다. 두 노드에서 모두 다음 명령을 실행합니다.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

1. SQL Server용 FCI 리소스 에이전트를 설치합니다. 두 노드에서 모두 다음 명령을 실행합니다. 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="configure-the-failover-cluster-instance"></a>장애 조치 클러스터 인스턴스 구성

FCI는 리소스 그룹에 생성 됩니다. 이 리소스 그룹 제약 조건에 대 한 필요성을 줄여 줍니다. 때문에 좀 더 쉽습니다. 그러나 시작 해야 하는 순서로 리소스 그룹에 리소스를 추가 합니다. 시작 하는 순서는. 

1. 저장소 리소스
2. 네트워크 리소스
3. 응용 프로그램 리소스

이 예제에서는 NewLinFCIGrp 그룹에 FCI 만들어집니다. 리소스 그룹의 이름을 Pacemaker에서 만든 모든 리소스에서 고유 해야 합니다.

1.  디스크 리소스를 만듭니다. 문제가 없는 경우에 다시 응답을 받습니다. 디스크 리소스를 만들 수 있는 방법은 저장소 형식에 따라 달라 집니다. 다음은 각 저장소 형식에 대 한 예입니다. 클러스터 된 저장소에 대 한 저장소 형식에 적용 되는 예제를 사용 합니다.

    **iSCSI**

    ```bash
    sudo pcs resource create <iSCSIDiskResourceName> Filesystem device="/dev/<VolumeGroupName>/<LogicalVolumeName>" directory="<FolderToMountiSCSIDisk>" fstype="<FileSystemType>" --group RGName
    ```

    \<iSCSIDIskResourceName > iSCSI 디스크와 연결 된 리소스의 이름

    \<VolumeGroupName > 볼륨 그룹의 이름  

    \<LogicalVolumeName > 만든 논리 볼륨의 이름  

    \<FolderToMountiSCSIDIsk > 디스크를 탑재 하는 폴더 (시스템 데이터베이스와 기본 위치에 대 한 것 /var/opt/mssql/data)

    \<FileSystemType > 작업의 형식을 지정 된 방법 및 어떤 분포 지원에 따라 EXT4 또는 XFS 것입니다. 

    **NFS**

    ```bash
    sudo pcs resource create <NFSDiskResourceName> Filesystem device="<IPAddressOfNFSServer>:<FolderOnNFSServer>" directory="<FolderToMountNFSShare>" fstype=nfs4 options=" nfsvers=4.2,timeo=14,intr" --group RGName
    mount -t nfs4 IPAddressOfNFSServer:FolderOnNFSServer /var/opt/mssql/data -o 
    ```

    \<NFSDIskResourceName > NFS 공유와 연결 된 리소스의 이름

    \<IPAddressOfNFSServer >는 사용 하고자 하는 NFS 서버의 IP 주소

    \<FolderOnNFSServer > NFS 공유의 이름

    \<FolderToMountNFSShare > 디스크를 탑재 하는 폴더 (시스템 데이터베이스와 기본 위치에 대 한 것 /var/opt/mssql/data)

    예는 다음과 같습니다.

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    **SMB**

    ```bash
    sudo pcs resource create SMBDiskResourceName Filesystem device="//<ServerName>/<ShareName>" directory="<FolderName>" fstype=cifs options="vers=3.0,username=<UserName>,password=<Password>,domain=<ADDomain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777" --group <RGName>
    ```

    \<서버 이름 >은 SMB 공유를 사용 하 여 서버 이름

    \<공유 이름 > 공유의 이름

    \<폴더 이름 > 마지막 단계에서 만든 폴더의 이름
    
    \<사용자 이름 > 공유에 액세스 하려면 사용자의 이름

    \<암호 > 사용자에 대 한 암호

    \<ADDomain >은 AD DS 도메인 (해당 하는 경우 Windows Server 기반 SMB 공유를 사용 하는 경우)

    \<mssqlUID > mssql 사용자 UID은

    \<mssqlGID > mssql 사용자 GID은

    \<RGName > 리소스 그룹의 이름
 
2.  FCI에서 사용할 IP 주소를 만듭니다. 문제가 없는 경우에 다시 응답을 받습니다.

    ```bash
    sudo pcs resource create <IPResourceName> ocf:heartbeat:IPaddr2 ip=<IPAddress> nic=<NetworkCard> cidr_netmask=<NetMask> --group <RGName>
    ```

    \<IPResourceName >은 IP 주소와 연결 된 리소스의 이름

    \<Ip 주소 >은 FCI에 대 한 IP 주소

    \<NetworkCard > (예: eth0) 서브넷에 연결 된 네트워크 카드

    \<네트워크 마스크 >은 서브넷 (즉, 24)의 네트워크 마스크

    \<RGName > 리소스 그룹의 이름
 
3.  FCI 리소스를 만듭니다. 문제가 없는 경우에 다시 응답을 받습니다.

    ```bash
    sudo pcs resource create FCIResourceName ocf:mssql:fci op defaults timeout=60s --group RGName
    ```

    \<FCIResourceName >는 리소스의 이름 뿐만 아니라 FCI와 연결 된 이름이 됩니다. 어떤 사용자와 응용 프로그램이 연결 하기 위해 사용할입니다. 

    \<RGName > 리소스 그룹의 이름입니다.
 
4.  명령을 실행 `sudo pcs resource`합니다. FCI는 온라인 상태 여야 합니다.
 
5.  SSMS 또는 sqlcmd FCI의 DNS/리소스 이름을 사용 하 여 FCI에 연결 합니다.

6.  문을 실행 `SELECT @@SERVERNAME`합니다. FCI의 이름을 반환 합니다.

7.  문을 실행 `SELECT SERVERPROPERTY('ComputerNamePhysicalNetBIOS')`합니다. FCI에서 실행 되는 노드의 이름을 반환 합니다.

8.  FCI에 다른 노드를 수동으로 실패 합니다. 지침 참조 [Operate 장애 조치 클러스터 인스턴스-Linux에서 SQL Server](sql-server-linux-shared-disk-cluster-operate.md)합니다.

9.  마지막으로 다시 원래 노드를 FCI 실패 하 고 공동 배치 제약 조건을 제거 합니다.

<!---
|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)
-->
## <a name="summary"></a>요약

이 자습서에서는 다음 작업을 완료 합니다.

> [!div class="checklist"]
> * 설정 및 Linux 구성
> * SQL Server 설치 및 구성
> * 호스트 파일 구성
> * 공유 저장소를 구성 하 고 데이터베이스 파일 이동
> * 설치 하 고 각 클러스터 노드에서 Pacemaker 구성
> * 장애 조치 클러스터 인스턴스 구성

## <a name="next-steps"></a>다음 단계

- [장애 조치 클러스터 인스턴스에 SQL Server Linux에서 작동 합니다.](sql-server-linux-shared-disk-cluster-operate.md)

<!--Image references-->
