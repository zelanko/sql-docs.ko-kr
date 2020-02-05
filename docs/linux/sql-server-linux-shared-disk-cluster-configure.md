---
title: FCI 구성 - SQL Server on Linux(RHEL)
description: SQL Server용 RHEL(Red Hat Enterprise Linux)에서 FCI(장애 조치 클러스터 인스턴스)를 구성하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 61fe5d7ffb5dfc6ec98f6d5350eff396deaa0312
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558328"
---
# <a name="configure-failover-cluster-instance---sql-server-on-linux-rhel"></a>장애 조치(failover) 클러스터 인스턴스 구성 - SQL Server on Linux(RHEL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 2노드 공유 디스크 장애 조치(failover) 클러스터 인스턴스는 고가용성을 위해 서버 수준 중복성을 제공합니다. 이 자습서에서는 SQL Server on Linux의 2노드 장애 조치(failover) 클러스터 인스턴스를 만드는 방법을 알아봅니다. 수행하는 구체적인 단계는 다음과 같습니다.

> [!div class="checklist"]
> * Linux 설정 및 구성
> * SQL Server 설치 및 구성
> * hosts 파일 구성
> * 공유 스토리지 구성 및 데이터베이스 파일 이동
> * 각 클러스터 노드에 Pacemaker 설치 및 구성
> * 장애 조치(failover) 클러스터 인스턴스 구성

이 문서에서는 SQL Server의 2노드 공유 디스크 FCI(장애 조치(failover) 클러스터 인스턴스)를 만드는 방법을 설명합니다. 이 문서에는 RHEL(Red Hat Enterprise Linux)에 대한 지침과 스크립트 예제가 포함되어 있습니다. Ubuntu 배포는 RHEL과 유사하므로, 이 스크립트 예제는 일반적으로 Ubuntu에서도 작동합니다. 

개념 정보는 [Linux의 SQL Server FCI(장애 조치(failover) 클러스터 인스턴스)](sql-server-linux-shared-disk-cluster-concepts.md)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

다음 엔드투엔드 시나리오를 완료하려면 2노드 클러스터를 배포할 머신 2대와 스토리지에 사용할 또 다른 서버가 필요합니다. 아래 단계에서는 이러한 서버를 구성하는 방법을 간략하게 설명합니다.

## <a name="set-up-and-configure-linux"></a>Linux 설정 및 구성

첫 번째 단계는 클러스터 노드에서 운영 체제를 구성하는 것입니다. 클러스터의 각 노드에서 Linux 배포를 구성합니다. 두 노드에서 동일한 배포와 버전을 사용합니다. 다음 배포 중 하나를 사용합니다.
    
* HA 추가 기능을 위한 유효한 구독이 있는 RHEL

## <a name="install-and-configure-sql-server"></a>SQL Server 설치 및 구성

1. 두 노드에서 SQL Server를 설치하고 설정합니다.  자세한 내용은 [SQL Server on Linux 설치](sql-server-linux-setup.md)를 참조하세요.
1. 구성의 목적을 위해 노드 하나를 주 노드로 지정하고 다른 노드를 보조 노드로 지정합니다. 이 용어는 가이드 전체에서 사용됩니다.  
1. 보조 노드에서 SQL Server를 중지하고 사용하지 않도록 설정합니다.
    다음 예제에서는 SQL Server를 중지하고 사용하지 않도록 설정합니다. 
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE] 
    > 설정 시 SQL Server 인스턴스의 서버 마스터 키가 생성되어 `var/opt/mssql/secrets/machine-key`에 저장됩니다. Linux에서 SQL Server는 항상 mssql이라는 로컬 계정으로 실행됩니다. 이 계정은 로컬 계정이므로 해당 ID가 노드 간에 공유되지 않습니다. 따라서 각 로컬 mssql 계정이 서버 마스터 키의 암호 해독을 위해 액세스할 수 있도록 주 노드에서 각 보조 노드로 암호화 키를 복사해야 합니다. 

1.  주 노드에서 Pacemaker용 SQL Server 로그인을 만들고 `sp_server_diagnostics` 실행 권한을 로그인에 부여합니다. Pacemaker는 이 계정을 사용하여 SQL Server를 실행 중인 노드를 확인합니다. 

    ```bash
    sudo systemctl start mssql-server
    ```
   
   sa 계정을 사용하여 SQL Server `master` 데이터베이스에 연결하고 다음 명령을 실행합니다.

   ```sql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```

   또는 더 세부적인 수준에서 권한을 설정할 수 있습니다. Pacemaker 로그인은 `VIEW SERVER STATE`를 통해 sp_server_diagnostics에서 성능 상태를 쿼리하고, `setupadmin` 및 `ALTER ANY LINKED SERVER`를 통해 sp_dropserver 및 sp_addserver를 실행하여 FCI 인스턴스 이름을 리소스 이름으로 업데이트해야 합니다. 

1. 주 노드에서 SQL Server를 중지하고 사용하지 않도록 설정합니다. 

## <a name="configure-the-hosts-file"></a>hosts 파일 구성

각 클러스터 노드에서 hosts 파일을 구성합니다. hosts 파일은 모든 클러스터 노드의 IP 주소와 이름을 포함해야 합니다.

1. 각 노드의 IP 주소를 확인합니다. 다음 스크립트는 현재 노드의 IP 주소를 보여 줍니다. 

    ```bash
    sudo ip addr show
    ```

1. 각 노드에서 컴퓨터 이름을 설정합니다. 각 노드에 15자 이하의 고유 이름을 지정합니다. 컴퓨터 이름을 `/etc/hosts`에 추가하여 설정합니다. 다음 스크립트를 사용하면 `/etc/hosts`를 `vi`로 편집할 수 있습니다. 

   ```bash
   sudo vi /etc/hosts
   ```
   다음 예제에서는 `/etc/hosts` 및 `sqlfcivm1`라는 두 노드의 정보가 추가된 `sqlfcivm2`를 보여 줍니다.

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

## <a name="configure-storage--move-database-files"></a>스토리지 구성 및 데이터베이스 파일 이동  

두 노드에서 모두 액세스할 수 있는 스토리지를 제공해야 합니다. iSCSI, NFS 또는 SMB를 사용할 수 있습니다. 스토리지를 구성하고 클러스터 노드에 스토리지를 제공한 다음, 데이터베이스 파일을 새 스토리지로 이동합니다. 다음 문서에서는 각 스토리지 유형의 단계를 설명합니다.

- [장애 조치(failover) 클러스터 인스턴스 구성 - iSCSI - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [장애 조치(failover) 클러스터 인스턴스 구성 - NFS - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [장애 조치(failover) 클러스터 인스턴스 구성 - SMB - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>각 클러스터 노드에 Pacemaker 설치 및 구성

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

   > 기본 제공된 고가용성 구성이 없는 또 다른 방화벽을 사용하는 경우 Pacemaker가 클러스터의 다른 노드와 통신할 수 있으려면 다음 포트를 열어야 합니다.
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

## <a name="configure-the-failover-cluster-instance"></a>장애 조치(failover) 클러스터 인스턴스 구성

FCI는 리소스 그룹에 만들어집니다. 리소스 그룹을 사용하면 제약 조건이 덜 필요하므로 구성 작업이 좀 더 간편합니다. 그러나 시작되어야 하는 순서대로 리소스를 리소스 그룹에 추가합니다. 시작되어야 하는 순서는 다음과 같습니다. 

1. 스토리지 리소스
2. 네트워크 리소스
3. 애플리케이션 리소스

이 예제에서는 NewLinFCIGrp 그룹에 FCI를 만듭니다. 리소스 그룹의 이름은 Pacemaker에 생성된 모든 리소스에서 고유해야 합니다.

1.  디스크 리소스를 만듭니다. 문제가 없으면 응답이 반환되지 않습니다. 디스크 리소스를 만드는 방법은 스토리지 유형에 따라 다릅니다. 다음은 각 스토리지 유형의 예제입니다. 해당 클러스터형 스토리지의 스토리지 유형에 적용되는 예제를 사용합니다.

    **iSCSI**

    ```bash
    sudo pcs resource create <iSCSIDiskResourceName> Filesystem device="/dev/<VolumeGroupName>/<LogicalVolumeName>" directory="<FolderToMountiSCSIDisk>" fstype="<FileSystemType>" --group RGName
    ```

    \<iSCSIDIskResourceName>은 iSCSI 디스크와 연결된 리소스의 이름입니다.

    \<VolumeGroupName>은 볼륨 그룹의 이름입니다.  

    \<LogicalVolumeName>은 생성된 논리 볼륨의 이름입니다.  

    \<FolderToMountiSCSIDIsk>는 디스크를 탑재할 폴더입니다(시스템 데이터베이스와 기본 위치의 경우 /var/opt/mssql/data임).

    \<FileSystemType>은 항목에 지정된 형식과 배포에서 지원하는 항목에 따라 EXT4 또는 XFS가 됩니다. 

    **NFS**

    ```bash
    sudo pcs resource create <NFSDiskResourceName> Filesystem device="<IPAddressOfNFSServer>:<FolderOnNFSServer>" directory="<FolderToMountNFSShare>" fstype=nfs4 options=" nfsvers=4.2,timeo=14,intr" --group RGName
    mount -t nfs4 IPAddressOfNFSServer:FolderOnNFSServer /var/opt/mssql/data -o 
    ```

    \<NFSDIskResourceName>은 NFS 공유와 연결된 리소스의 이름입니다.

    \<IPAddressOfNFSServer>는 사용하려는 NFS 서버의 IP 주소입니다.

    \<FolderOnNFSServer>는 NFS 공유의 이름입니다.

    \<FolderToMountNFSShare>는 디스크를 탑재할 폴더입니다(시스템 데이터베이스와 기본 위치의 경우 /var/opt/mssql/data임).

    예는 다음과 같습니다.

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    **SMB**

    ```bash
    sudo pcs resource create SMBDiskResourceName Filesystem device="//<ServerName>/<ShareName>" directory="<FolderName>" fstype=cifs options="vers=3.0,username=<UserName>,password=<Password>,domain=<ADDomain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777" --group <RGName>
    ```

    \<ServerName>은 SMB 공유가 있는 서버의 이름입니다.

    \<ShareName>은 공유의 이름입니다.

    \<FolderName>은 마지막 단계에서 만든 폴더의 이름입니다.
    
    \<UserName>은 공유에 액세스할 사용자의 이름입니다.

    \<Password>는 사용자의 암호입니다.

    \<ADDomain>은 AD DS 도메인입니다(Windows Server 기반 SMB 공유를 사용할 때 해당되는 경우).

    \<mssqlUID>는 mssql 사용자의 UID입니다.

    \<mssqlGID>는 mssql 사용자의 GID입니다.

    \<RGName>은 리소스 그룹의 이름입니다.
 
2.  FCI에서 사용할 IP 주소를 만듭니다. 문제가 없으면 응답이 반환되지 않습니다.

    ```bash
    sudo pcs resource create <IPResourceName> ocf:heartbeat:IPaddr2 ip=<IPAddress> nic=<NetworkCard> cidr_netmask=<NetMask> --group <RGName>
    ```

    \<IPResourceName>은 IP 주소와 연결된 리소스의 이름입니다.

    \<IPAddress>는 FCI의 IP 주소입니다.

    \<NetworkCard>는 서브넷과 연결된 네트워크 카드(즉, eth0)입니다.

    \<NetMask>는 서브넷의 네트워크 마스크(즉, 24)입니다.

    \<RGName>은 리소스 그룹의 이름입니다.
 
3.  FCI 리소스를 만듭니다. 문제가 없으면 응답이 반환되지 않습니다.

    ```bash
    sudo pcs resource create FCIResourceName ocf:mssql:fci op defaults timeout=60s --group RGName
    ```

    \<FCIResourceName>은 리소스 이름뿐 아니라 FCI와 연결된 이름입니다. 사용자와 애플리케이션은 이 이름을 사용하여 연결합니다. 

    \<RGName>은 리소스 그룹의 이름입니다.
 
4.  `sudo pcs resource` 명령을 실행합니다. FCI가 온라인 상태여야 합니다.
 
5.  FCI의 DNS/리소스 이름을 사용하여 SSMS 또는 sqlcmd를 통해 FCI에 연결합니다.

6.  `SELECT @@SERVERNAME` 문을 실행합니다. FCI의 이름이 반환됩니다.

7.  `SELECT SERVERPROPERTY('ComputerNamePhysicalNetBIOS')` 문을 실행합니다. FCI를 실행하는 노드의 이름이 반환됩니다.

8.  수동으로 FCI를 다른 노드로 장애 조치(failover)합니다. [장애 조치(failover) 클러스터 인스턴스 작동 - SQL Server on Linux](sql-server-linux-shared-disk-cluster-operate.md) 아래의 지침을 참조하세요.

9.  마지막으로, FCI를 원래 노드로 장애 복구(failback)하고 공동 배치 제약 조건을 제거합니다.

<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

-->
## <a name="summary"></a>요약

이 자습서에서는 다음 작업을 완료했습니다.

> [!div class="checklist"]
> * Linux 설정 및 구성
> * SQL Server 설치 및 구성
> * hosts 파일 구성
> * 공유 스토리지 구성 및 데이터베이스 파일 이동
> * 각 클러스터 노드에 Pacemaker 설치 및 구성
> * 장애 조치(failover) 클러스터 인스턴스 구성

## <a name="next-steps"></a>다음 단계

- [장애 조치(failover) 클러스터 인스턴스 작동 - SQL Server on Linux](sql-server-linux-shared-disk-cluster-operate.md)

<!--Image references-->
