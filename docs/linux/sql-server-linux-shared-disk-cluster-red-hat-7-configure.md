---
title: SQL Server on Linux의 RHEL FCI 구성
description: SQL Server on Linux 고가용성을 위해 RHEL(Red Hat Enterprise Linux) 공유 디스크 FCI(장애 조치 클러스터 인스턴스)를 구성하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: dcc0a8d3-9d25-4208-8507-a5e65d2a9a15
ms.openlocfilehash: 3ff0c862e93cd3b552b29c4eec8ab91931c809c7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75656630"
---
# <a name="configure-rhel-failover-cluster-instance-fci-cluster-for-sql-server"></a>SQL Server의 RHEL FCI(장애 조치 클러스터 인스턴스) 클러스터 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 가이드에서는 Red Hat Enterprise Linux에서 SQL Server의 2노드 공유 디스크 장애 조치 클러스터를 만들기 위한 지침을 제공합니다. 클러스터링 계층은 [Pacemaker](https://clusterlabs.org/) 위에 빌드된 RHEL(Red Hat Enterprise Linux) [HA 추가 기능](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)을 기반으로 합니다. SQL Server 인스턴스는 두 노드 중 하나에서 활성화됩니다.

> [!NOTE] 
> Red Hat HA 추가 기능 및 설명서에 액세스하려면 구독이 필요합니다. 

다음 다이어그램에 표시된 대로 스토리지는 두 개의 서버에 제공됩니다. 클러스터링 구성 요소인 Corosync와 Pacemaker는 통신 및 리소스 관리를 조정합니다. 서버 중 하나에는 스토리지 리소스 및 SQL Server에 대한 활성 연결이 있습니다. Pacemaker가 오류를 탐지하면 클러스터링 구성 요소는 리소스를 다른 노드로 이동하는 작업을 관리합니다.  

![Red Hat Enterprise Linux 7 공유 디스크 SQL 클러스터](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

클러스터 구성, 리소스 에이전트 옵션 및 관리에 대한 자세한 내용은 [RHEL 참조 설명서](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)를 참조하세요.


> [!NOTE] 
> 이때 Pacemaker와 SQL Server의 통합은 Windows의 WSFC와 같이 결합되지 않습니다. SQL 내에 클러스터의 현재 상태 정보가 없으며, 모든 오케스트레이션이 외부에서 수행되고, 서비스는 Pacemaker에서 독립 실행형 인스턴스로 제어됩니다. 예를 들어 클러스터 DMV sys.dm_os_cluster_nodes 및 sys.dm_os_cluster_properties에 레코드가 없습니다.
문자열 서버 이름을 가리키는 연결 문자열을 사용하고 IP를 사용하지 않으려면 선택된 서버 이름을 사용하여 다음 섹션에 설명된 대로 가상 IP 리소스를 만드는 데 사용된 IP를 DNS 서버에 등록해야 합니다.

다음 섹션에서는 장애 조치(failover) 클러스터 솔루션을 설정하는 단계를 안내합니다. 

## <a name="prerequisites"></a>사전 요구 사항

다음 엔드투엔드 시나리오를 완료하려면 2노드 클러스터를 배포할 머신 2대와 NFS 서버를 구성할 또 다른 서버가 필요합니다. 아래 단계에서는 이러한 서버를 구성하는 방법을 간략하게 설명합니다.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>각 클러스터 노드에서 운영 체제 설정 및 구성

첫 번째 단계는 클러스터 노드에서 운영 체제를 구성하는 것입니다. 이 연습에서는 HA 추가 기능을 위한 유효한 구독이 있는 RHEL을 사용합니다. 

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>각 클러스터 노드에서 SQL Server 설치 및 구성

1. 두 노드에서 모두 SQL Server를 설치하고 설정합니다.  자세한 내용은 [SQL Server on Linux 설치](sql-server-linux-setup.md)를 참조하세요.

1. 구성의 목적을 위해 노드 하나를 주 노드로 지정하고 다른 노드를 보조 노드로 지정합니다. 이 용어는 가이드 전체에서 사용됩니다.  

1. 보조 노드에서 SQL Server를 중지하고 사용하지 않도록 설정합니다.

   다음 예제에서는 SQL Server를 중지하고 사용하지 않도록 설정합니다. 

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl disable mssql-server
   ```
> [!NOTE] 
> 설정 시 SQL Server 인스턴스의 서버 마스터 키가 생성되어 `/var/opt/mssql/secrets/machine-key`에 저장됩니다. Linux에서 SQL Server는 항상 mssql이라는 로컬 계정으로 실행됩니다. 이 계정은 로컬 계정이므로 해당 ID가 노드 간에 공유되지 않습니다. 따라서 각 로컬 mssql 계정이 서버 마스터 키의 암호 해독을 위해 액세스할 수 있도록 주 노드에서 각 보조 노드로 암호화 키를 복사해야 합니다. 

1. 주 노드에서 Pacemaker용 SQL Server 로그인을 만들고 `sp_server_diagnostics` 실행 권한을 로그인에 부여합니다. Pacemaker는 이 계정을 사용하여 SQL Server를 실행 중인 노드를 확인합니다. 

   ```bash
   sudo systemctl start mssql-server
   ```

   sa 계정을 사용하여 SQL Server `master` 데이터베이스에 연결하고 다음 명령을 실행합니다.

   ```bashsql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'

   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```
   또는 더 세부적인 수준에서 권한을 설정할 수 있습니다. Pacemaker 로그인은 `VIEW SERVER STATE`를 통해 sp_server_diagnostics에서 성능 상태를 쿼리하고, `setupadmin` 및 `ALTER ANY LINKED SERVER`를 통해 sp_dropserver 및 sp_addserver를 실행하여 FCI 인스턴스 이름을 리소스 이름으로 업데이트해야 합니다. 

1. 주 노드에서 SQL Server를 중지하고 사용하지 않도록 설정합니다. 

1. 각 클러스터 노드의 hosts 파일을 구성합니다. hosts 파일은 모든 클러스터 노드의 IP 주소와 이름을 포함해야 합니다. 

    각 노드의 IP 주소를 확인합니다. 다음 스크립트는 현재 노드의 IP 주소를 보여 줍니다. 

   ```bash
   sudo ip addr show
   ```

   각 노드에서 컴퓨터 이름을 설정합니다. 각 노드에 15자 이하의 고유 이름을 지정합니다. 컴퓨터 이름을 `/etc/hosts`에 추가하여 설정합니다. 다음 스크립트를 사용하면 `/etc/hosts`를 `vi`로 편집할 수 있습니다. 

   ```bash
   sudo vi /etc/hosts
   ```
   다음 예제에서는 `sqlfcivm1` 및 `sqlfcivm2`라는 두 노드의 정보가 추가된 `/etc/hosts`를 보여 줍니다.

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

다음 섹션에서는 공유 스토리지를 구성하고 데이터베이스 파일을 해당 스토리지로 이동합니다. 

## <a name="configure-shared-storage-and-move-database-files"></a>공유 스토리지 구성 및 데이터베이스 파일 이동 

공유 스토리지를 제공하는 다양한 솔루션이 있습니다. 이 연습에서는 NFS를 사용하여 공유 스토리지를 구성하는 방법을 보여 줍니다. 모범 사례를 따르고 Kerberos를 사용하여 NFS를 보호하는 것이 좋습니다(예제는 https://www.certdepot.net/rhel7-use-kerberos-control-access-nfs-network-shares/) 에서 확인할 수 있음). 

>[!Warning]
>NFS의 보안을 유지하지 않으면 네트워크에 액세스하고 SQL 노드의 IP 주소를 스푸핑할 수 있는 누구든지 데이터 파일에 액세스할 수 있습니다. 언제나와 마찬가지로, 프로덕션 환경에서 사용하기 전에 시스템의 위협을 모델링해야 합니다. 또 다른 스토리지 옵션은 다음과 같이 SMB 파일 공유를 사용하는 것입니다.

### <a name="configure-shared-storage-with-nfs"></a>NFS를 사용하여 공유 스토리지 구성

> [!IMPORTANT] 
> 이 릴리스에서는 버전 4 이전 NFS 서버에서 데이터베이스 파일을 호스트할 수 없습니다. 여기에는 비클러스터형 인스턴스의 데이터베이스뿐만 아니라 공유 디스크 장애 조치(failover) 클러스터링에 NFS를 사용하는 기능이 포함됩니다. 이후 릴리스에서는 다른 NFS 서버 버전을 사용할 수 있도록 개발 중입니다. 

NFS 서버에서 다음 작업을 수행합니다.

1. `nfs-utils` 설치

   ```bash
   sudo yum -y install nfs-utils
   ```

1. `rpcbind`를 사용하도록 설정하고 시작합니다.

   ```bash
   sudo systemctl enable rpcbind && sudo systemctl start rpcbind
   ```

1. `nfs-server`를 사용하도록 설정하고 시작합니다.
 
   ```bash
   sudo systemctl enable nfs-server && sudo systemctl start nfs-server
   ```
 
1.  `/etc/exports`를 편집하여 공유하려는 디렉터리를 내보냅니다. 원하는 각 공유를 1줄로 입력합니다. 다음은 그 예입니다. 

   ```bash
   /mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)
   ```

1. 공유를 내보냅니다.

   ```bash
   sudo exportfs -rav
   ```

1. 경로가 공유/내보내졌는지 확인합니다. NFS 서버에서 다음 명령을 실행합니다.

   ```bash
   sudo showmount -e
   ```

1. SELinux에서 예외를 추가합니다.

   ```bash
   sudo setsebool -P nfs_export_all_rw 1
   ```
   
1. 서버에서 방화벽을 엽니다.

   ```bash 
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>NFS 공유 스토리지에 연결하도록 모든 클러스터 노드를 구성합니다.

모든 클러스터 노드에서 다음 단계를 수행합니다.

1.  `nfs-utils` 설치

   ```bash
   sudo yum -y install nfs-utils
   ```

1. 클라이언트 및 NFS 서버에서 방화벽을 엽니다.

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

1. 클라이언트 컴퓨터에서 NFS 공유를 볼 수 있는지 확인합니다.

   ```bash
   sudo showmount -e <IP OF NFS SERVER>
   ```

1. 모든 클러스터 노드에서 이 단계를 반복합니다.

NFS 사용 방법에 대한 자세한 내용은 다음 리소스를 참조하세요.

* [NFS servers and firewalld | Stack Exchange](https://unix.stackexchange.com/questions/243756/nfs-servers-and-firewalld)(NFS 서버 및 firewalld | 스택 교환)
* [Mounting an NFS Volume | Linux Network Administrators Guide](https://www.tldp.org/LDP/nag2/x-087-2-nfs.mountd.html)(NFS 볼륨 탑재 | Linux 네트워크 관리자 가이드)
* [NFS server configuration | Red Hat Customer Portal](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/storage_administration_guide/nfs-serverconfig)(NFS 서버 구성 | Red Hat 고객 포털)

### <a name="mount-database-files-directory-to-point-to-the-shared-storage"></a>공유 스토리지를 가리키도록 데이터베이스 파일 디렉터리 탑재

1.  **주 노드에서만** 데이터베이스 파일을 임시 위치에 저장합니다. 다음 스크립트는 새 임시 디렉터리를 만들고 데이터베이스 파일을 새 디렉터리에 복사한 다음, 이전 데이터베이스 파일을 제거합니다. SQL Server는 로컬 사용자 mssql로 실행되므로, 탑재된 공유로 데이터가 전송된 후 로컬 사용자에게 공유에 대한 읽기/쓰기 권한이 있는지 확인해야 합니다. 

   ``` 
   $ sudo su mssql
   $ mkdir /var/opt/mssql/tmp
   $ cp /var/opt/mssql/data/* /var/opt/mssql/tmp
   $ rm /var/opt/mssql/data/*
   $ exit
   ``` 

1.  모든 클러스터 노드에서 `/etc/fstab` 파일을 편집하여 mount 명령을 포함합니다.  

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr 
   ```
   
   다음 스크립트는 편집의 예를 보여 줍니다.  

   ``` 
   10.8.8.0:/mnt/nfs /var/opt/mssql/data nfs timeo=14,intr 
   ``` 
> [!NOTE] 
>여기서 권장하는 대로 FS(파일 시스템) 리소스를 사용하는 경우에는 mount 명령을 /etc/fstab에 유지할 필요가 없습니다. Pacemaker가 FS 클러스터형 리소스를 시작할 때 폴더 탑재를 처리합니다. 펜싱을 사용하면 FS가 두 번 탑재되지 않도록 보장할 수 있습니다. 

1.  시스템에 대해 `mount -a` 명령을 실행하여 탑재된 경로를 업데이트합니다.  

1.  `/var/opt/mssql/tmp`에 저장한 데이터베이스 및 로그 파일을 새로 탑재된 공유 `/var/opt/mssql/data`에 복사합니다. 이 작업은 **주 노드에서만** 수행하면 됩니다. ‘mssql’ 로컬 사용자에게 읽기/쓰기 권한을 부여해야 합니다.

   ``` 
   $ sudo chown mssql /var/opt/mssql/data
   $ sudo chgrp mssql /var/opt/mssql/data
   $ sudo su mssql
   $ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/
   $ rm /var/opt/mssql/tmp/*
   $ exit
   ``` 
 
1.  SQL Server가 새 파일 경로를 사용하여 성공적으로 시작되는지 확인합니다. 각 노드에서 이 작업을 수행합니다. 이때 한 번에 하나의 노드에서만 SQL Server를 실행해야 합니다. 두 노드 모두 데이터 파일에 동시에 액세스하려고 하므로 동시에 실행할 수 없습니다. 우연히 두 노드에서 모두 SQL Server를 시작하는 경우를 방지하려면 파일 시스템 클러스터 리소스를 사용하여 각기 다른 노드에서 공유가 두 번 탑재되지 않도록 합니다. 다음 명령은 SQL Server를 시작하고 상태를 확인한 다음, SQL Server를 중지합니다.
 
   ```bash
   sudo systemctl start mssql-server
   sudo systemctl status mssql-server
   sudo systemctl stop mssql-server
   ```
 
이때 SQL Server의 두 인스턴스는 모두 공유 스토리지의 데이터베이스 파일을 사용하여 실행되도록 구성되어 있습니다. 다음 단계는 Pacemaker에 대해 SQL Server를 구성하는 것입니다. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>각 클러스터 노드에 Pacemaker 설치 및 구성


2. 두 클러스터 노드에서 모두 Pacemaker 로그인을 위한 SQL Server 사용자 이름 및 암호를 저장할 파일을 만듭니다. 다음 명령은 이 파일을 만들고 채웁니다.

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   echo '<loginName>' | sudo tee -a /var/opt/mssql/secrets/passwd
   echo '<loginPassword>' | sudo tee -a /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. 두 클러스터 노드에서 모두 Pacemaker 방화벽 포트를 엽니다. `firewalld`를 사용하여 이러한 포트를 열려면 다음 명령을 실행합니다.

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

    

2. Pacemaker 및 Corosync 패키지를 설치할 때 생성된 기본 사용자의 암호를 설정합니다. 두 노드에서 모두 같은 암호를 사용합니다. 

   ```bash
   sudo passwd hacluster
   ```

    

3. `pcsd` 서비스 및 Pacemaker를 사용하도록 설정하고 시작합니다. 이렇게 하면 다시 시작된 후 노드가 클러스터에 다시 조인할 수 있습니다. 두 노드에서 모두 다음 명령을 실행합니다.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. SQL Server용 FCI 리소스 에이전트를 설치합니다. 두 노드에서 모두 다음 명령을 실행합니다. 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="configure-fencing-agent"></a>펜싱 에이전트 구성

STONITH 디바이스는 펜싱 에이전트를 제공합니다. [Azure의 Red Hat Enterprise Linux에서 Pacemaker 설정](/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-pacemaker/#1-create-the-stonith-devices)에서는 Azure의 이 클러스터에 대해 STONITH 디바이스를 만드는 방법을 보여 줍니다. 작업 환경에 맞게 지침을 수정하세요.

## <a name="create-the-cluster"></a>클러스터 만들기 

1. 노드 중 하나에서 클러스터를 만듭니다.

   ```bash
   sudo pcs cluster auth <nodeName1 nodeName2 ...> -u hacluster
   sudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 ...>
   sudo pcs cluster start --all
   ```

2. SQL Server, 파일 시스템 및 가상 IP 리소스에 대해 클러스터 리소스를 구성하고 클러스터에 구성을 밀어넣습니다. 다음 정보가 필요합니다.

   - **SQL Server 리소스 이름**: 클러스터형 SQL Server 리소스의 이름입니다. 
   - **부동 IP 리소스 이름**: 가상 IP 주소 리소스의 이름입니다.
   - **IP 주소**: 클라이언트가 클러스터된 SQL Server 인스턴스에 연결하는 데 사용하는 IP 주소입니다. 
   - **파일 시스템 리소스 이름**: 파일 시스템 리소스의 이름입니다.
   - **device**: NFS 공유 경로입니다.
   - **device**: 공유에 탑재된 로컬 경로입니다.
   - **fstype**: 파일 공유 유형(예: nfs)입니다.

   다음 스크립트의 값을 환경에 맞게 업데이트합니다. 한 노드에서 실행하여 클러스터형 서비스를 구성하고 시작합니다.  

   ```bash
   sudo pcs cluster cib cfg 
   sudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fci
   sudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>
   sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>
   sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>
   sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName> 
   sudo pcs cluster cib-push cfg
   ```

   예를 들어 다음 스크립트는 `mssqlha`라는 SQL Server 클러스터형 리소스와 IP 주소가 `10.0.0.99`인 부동 IP 리소스를 만듭니다. 또한 파일 시스템 리소스를 만들고 모든 리소스가 SQL 리소스와 동일한 노드에 공동 배치되도록 제약 조건을 추가합니다. 

   ```bash
   sudo pcs cluster cib cfg
   sudo pcs -f cfg resource create mssqlha ocf:mssql:fci
   sudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99
   sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"
   sudo pcs -f cfg constraint colocation add virtualip mssqlha
   sudo pcs -f cfg constraint colocation add fs mssqlha
   sudo pcs cluster cib-push cfg
   ```

   구성을 밀어넣으면 SQL Server가 한 노드에서 시작됩니다. 

3. SQL Server가 시작되었는지 확인합니다. 

   ```bash
   sudo pcs status 
   ```

   다음 예제에서는 Pacemaker가 클러스터된 SQL Server 인스턴스를 성공적으로 시작한 경우의 결과를 보여 줍니다. 

   ```
   fs     (ocf::heartbeat:Filesystem):    Started sqlfcivm1
   virtualip     (ocf::heartbeat:IPaddr2):      Started sqlfcivm1
   mssqlha  (ocf::mssql:fci): Started sqlfcivm1
   
   PCSD Status:
    slqfcivm1: Online
    sqlfcivm2: Online
   
   Daemon Status:
    corosync: active/disabled
    pacemaker: active/enabled
    pcsd: active/enabled
   ```

## <a name="additional-resources"></a>추가 리소스

* Pacemaker의 [Cluster from Scratch](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf)(처음부터 클러스터) 가이드

## <a name="next-steps"></a>다음 단계

[Red Hat Enterprise Linux 공유 디스크 클러스터에서 SQL Server 작동](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
