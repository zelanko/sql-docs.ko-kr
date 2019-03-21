---
title: SQL Server에 대 한 Red Hat Enterprise Linux 공유 클러스터 구성 | Microsoft Docs
description: SQL Server에 대 한 Red Hat Enterprise Linux 공유 디스크 클러스터를 구성 하 여 고가용성을 구현 합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: dcc0a8d3-9d25-4208-8507-a5e65d2a9a15
ms.openlocfilehash: 1801551b179cf7040f1eb5cbaa05d8eb3bebc564
ms.sourcegitcommit: 7d4a3fc0f2622cbc6930d792be4a9b3fcac4c4b6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2019
ms.locfileid: "58306041"
---
# <a name="configure-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>SQL Server에 대 한 Red Hat Enterprise Linux 공유 디스크 클러스터 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 가이드는 Red Hat Enterprise Linux에서 SQL Server에 대 한 2 노드 공유 디스크 클러스터를 만드는 지침을 제공 합니다. 클러스터링 계층은 Red Hat Enterprise Linux (RHEL) 기반 [HA 추가 기능](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) 기반으로 구축 [Pacemaker](https://clusterlabs.org/)합니다. SQL Server 인스턴스는 하나의 노드 또는 다른 활성입니다.

> [!NOTE] 
> Red Hat HA 추가 기능 및 설명서에 대 한 액세스는 구독이 필요 합니다. 

다음 다이어그램에서 알 수 있듯이, 저장소는 두 서버에 표시 됩니다. -Corosync 및 Pacemaker-클러스터링 구성 요소 통신 및 리소스 관리를 조정합니다. 저장소 리소스 및 SQL Server에 활성 연결이 서버 중 하나입니다. Pacemaker 오류를 발견 하면 클러스터링 구성 요소 관리 리소스를 다른 노드로 이동 합니다.  

![Red Hat Enterprise Linux 7 공유 디스크 SQL 클러스터](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

클러스터 구성, 리소스 에이전트 옵션 및 관리에 대 한 자세한 내용은 방문 [RHEL 참조 설명서](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)합니다.


> [!NOTE] 
> 이 시점에서 Pacemaker 사용 하 여 SQL Server의 통합은 Windows의 경우 WSFC를 사용 하 여으로 결합 없습니다. 내의 SQL에는 클러스터의 현재 상태에 대해 모든 오케스트레이션 외부에서 이며 서비스는 독립 실행형 인스턴스로 Pacemaker에 의해 제어 됩니다. 또한 예를 들어, 클러스터 dmv sys.dm_os_cluster_nodes 및 sys.dm_os_cluster_properties는 레코드가 없습니다.
문자열 서버 이름으로 가리키는 연결 문자열을 사용 하 고 IP를 사용 하지를 선택한 서버 이름 (다음 섹션에서 설명)으로 가상 IP 리소스를 만드는 데 IP을 해당 DNS 서버에 등록 해야 합니다.

다음 섹션에서는 장애 조치 클러스터 솔루션을 설정 하는 단계를 안내 합니다. 

## <a name="prerequisites"></a>사전 요구 사항

다음 종단 간 시나리오를 완료 하려면 두 개의 머신을 두 노드 클러스터와 NFS 서버를 구성 하려면 다른 서버를 배포 해야 합니다. 아래 단계는이 서버를 구성 하는 방법을 간략하게 설명 합니다.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>설정 하 고 각 클러스터 노드의 운영 체제를 구성 합니다.

먼저는 클러스터 노드의 운영 체제를 구성 하는 것입니다. 이 연습에서는 HA 추가 기능에 대 한 RHEL을 유효한 구독을 사용 하 여 사용 합니다. 

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>설치 하 고 각 클러스터 노드에서 SQL Server 구성

1. 설치 하 고 두 노드에서 모두 SQL Server를 설치 합니다.  자세한 지침은 [Linux의 SQL Server 설치](sql-server-linux-setup.md)합니다.

1. 기본 및 보조 구성의 목적으로 다른 노드 하나를 지정 합니다. 이러한 용어를 사용 하 여 다음에 대 한이 가이드입니다.  

1. 보조 노드를 중지 하 고 SQL Server를 사용 하지 않도록 설정 합니다.

   다음 예에서는 중지 하 고 SQL Server를 사용 하지 않도록 설정 합니다. 

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl disable mssql-server
   ```
> [!NOTE] 
> 설치 시 서버 마스터 키를 SQL Server 인스턴스에 대해 생성 되며에 배치 `/var/opt/mssql/secrets/machine-key`합니다. Linux에서 SQL Server mssql 라는 로컬 계정으로 항상 실행 됩니다. 로컬 계정 이기 때문에 해당 id는 노드 간에 공유 되지 않습니다. 따라서 서버 마스터 키를 해독 하도록 각 로컬 mssql 계정에 액세스할 수 있도록 각 보조 노드에 주 노드에서 암호화 키를 복사 해야 합니다. 

1. 주 노드에서 Pacemaker 용 SQL server 로그인 만들기 및 실행에 로그인 권한을 부여 `sp_server_diagnostics`합니다. Pacemaker는 노드는 SQL Server를 실행 중인지 확인 하려면이 계정을 사용 합니다. 

   ```bash
   sudo systemctl start mssql-server
   ```

   SQL Server에 연결할 `master` sa 계정을 사용 하 여 데이터베이스에 있으며 다음을 실행 합니다.

   ```bashsql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'

   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```
   또는 더 세부적인 수준에서 권한을 설정할 수 있습니다. Pacemaker 로그인에 필요 `VIEW SERVER STATE` sp_server_diagnostics 사용 하 여 상태를 쿼리 하 `setupadmin` 및 `ALTER ANY LINKED SERVER` sp_dropserver 및 sp_addserver 실행 하 여 FCI 인스턴스 이름을 리소스 이름으로 업데이트 합니다. 

1. 주 노드를 중지 하 고 SQL Server를 사용 하지 않도록 설정 합니다. 

1. 각 클러스터 노드에 대 한 호스트 파일을 구성 합니다. 호스트 파일에는 IP 주소 및 모든 클러스터 노드의 이름이 포함 되어야 합니다. 

    각 노드에 대 한 IP 주소를 확인 합니다. 다음 스크립트를 현재 노드의 IP 주소를 보여 줍니다. 

   ```bash
   sudo ip addr show
   ```

   각 노드의 컴퓨터 이름을 설정 합니다. 각 노드는 고유한 이름을 15 자 이하의 합니다. 컴퓨터 이름을 추가 하 여 설정 `/etc/hosts`합니다. 다음 스크립트를 사용하면 `/etc/hosts`를 `vi`로 편집할 수 있습니다. 

   ```bash
   sudo vi /etc/hosts
   ```
   다음 예와 `/etc/hosts` 라는 두 노드에 대 한 추가 기능을 사용 하 여 `sqlfcivm1` 고 `sqlfcivm2`입니다.

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

다음 섹션에서 공유 저장소를 구성 하 고 해당 저장소에 데이터베이스 파일을 이동 합니다. 

## <a name="configure-shared-storage-and-move-database-files"></a>공유 저장소를 구성 하 고 데이터베이스 파일 이동 

공유 저장소를 제공 하기 위한 솔루션도 여러 가지가 있습니다. 이 연습에서는 NFS를 사용 하 여 공유 저장소를 구성 하는 방법을 보여 줍니다. 모범 사례를 따르고 Kerberos를 사용 하 여 NFS를 보호 하는 것이 좋습니다 (여기에 있는 예제를 찾을 수 있습니다: https://www.certdepot.net/rhel7-use-kerberos-control-access-nfs-network-shares/)합니다. 

>[!Warning]
>NFS를 보호 하지 않으면 SQL 노드의 IP 주소를 스푸핑 하 고 네트워크에 액세스할 수 있는 모든 사용자가 됩니다 데이터 파일에 액세스할 수 있습니다. 늘 그렇듯이 위협을 하면 프로덕션 환경에서 사용 하기 전에 시스템을 모델링 해야 합니다. 또 다른 저장소 옵션 SMB 파일 공유를 사용 하는 것입니다.

### <a name="configure-shared-storage-with-nfs"></a>NFS를 사용 하 여 공유 저장소 구성

> [!IMPORTANT] 
> 버전을 사용 하 여 NFS 서버에서 데이터베이스 파일을 호스트 < 4이 릴리스에서 지원 되지 않습니다. 공유 디스크 장애 조치 클러스터 되지 않은 인스턴스에서 데이터베이스 뿐만 아니라 클러스터링에 대 한 NFS를 사용 하는 것이 여기 있습니다. 노력 하 고 이후 릴리스에서 다른 NFS 서버 버전을 사용 하도록 설정 합니다. 

NFS 서버에서 다음을 수행합니다.

1. `nfs-utils` 설치

   ```bash
   sudo yum -y install nfs-utils
   ```

1. 설정 및 시작 `rpcbind`

   ```bash
   sudo systemctl enable rpcbind && sudo systemctl start rpcbind
   ```

1. 설정 및 시작 `nfs-server`
 
   ```bash
   sudo systemctl enable nfs-server && sudo systemctl start nfs-server
   ```
 
1.  편집 `/etc/exports` 공유 하려는 디렉터리를 내보내려면 합니다. 각 공유에 대 한 1 줄이 필요 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다. 

   ```bash
   /mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)
   ```

1. 공유 내보내기

   ```bash
   sudo exportfs -rav
   ```

1. 경로 공유/내보낸, NFS 서버에서 실행 확인

   ```bash
   sudo showmount -e
   ```

1. SELinux에서 예외를 추가 합니다.

   ```bash
   sudo setsebool -P nfs_export_all_rw 1
   ```
   
1. 서버 방화벽을 엽니다.

   ```bash 
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>NFS 공유 저장소에 연결 하려면 모든 클러스터 노드 구성

모든 클러스터 노드에서 다음 단계를 수행 합니다.

1.  `nfs-utils` 설치

   ```bash
   sudo yum -y install nfs-utils
   ```

1. 클라이언트 및 NFS 서버에서 방화벽 열기

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

1. 클라이언트 컴퓨터에서 NFS 공유를 볼 수 있는지 확인

   ```bash
   sudo showmount -e <IP OF NFS SERVER>
   ```

1. 모든 클러스터 노드에서 이러한 단계를 반복 합니다.

NFS를 사용 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

* [NFS 서버 및 firewalld | 스택 교환](https://unix.stackexchange.com/questions/243756/nfs-servers-and-firewalld)
* [NFS 볼륨을 탑재 | Linux 네트워크 관리자 가이드](https://www.tldp.org/LDP/nag2/x-087-2-nfs.mountd.html)
* [NFS 서버 구성 | Red Hat 고객 포털](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/storage_administration_guide/nfs-serverconfig)

### <a name="mount-database-files-directory-to-point-to-the-shared-storage"></a>공유 저장소를 가리키도록 데이터베이스 파일 디렉터리를 탑재 합니다.

1.  **주 노드에서**, 데이터베이스 파일을 임시 위치에 저장 합니다. 다음 스크립트를 새 임시 디렉터리를 만듭니다, 그리고 데이터베이스 파일을 새 디렉터리를 복사 및 이전 데이터베이스 파일을 제거 합니다. SQL Server mssql 로컬 사용자로 실행 되 면 후 탑재 된 공유에 데이터 전송, 로컬 사용자에 공유에 대 한 읽기 / 쓰기 액세스 있는지 확인 해야 합니다. 

   ``` 
   $ sudo su mssql
   $ mkdir /var/opt/mssql/tmp
   $ cp /var/opt/mssql/data/* /var/opt/mssql/tmp
   $ rm /var/opt/mssql/data/*
   $ exit
   ``` 

1.  모든 클러스터 노드에서 편집 `/etc/fstab` 탑재 명령을 포함 하는 파일입니다.  

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr 
   ```
   
   다음 스크립트를 편집의 예를 보여 줍니다.  

   ``` 
   10.8.8.0:/mnt/nfs /var/opt/mssql/data nfs timeo=14,intr 
   ``` 
> [!NOTE] 
>파일 시스템 (FS) 리소스를 권장 사항에 따라 여기에 사용 하는 경우 /etc/fstab에 탑재 명령을 유지 하려면 않아도가 됩니다. Pacemaker는 폴더를 탑재 하는 FS 클러스터 리소스를 시작 될 때 주의 합니다. 펜싱을 사용 하 여 FS에는 두 번 탑재 되지 않도록 합니다. 

1.  실행 `mount -a` 탑재 경로 업데이트 하려면 시스템에 대 한 명령입니다.  

1.  에 저장 된 데이터베이스 및 로그 파일을 복사 `/var/opt/mssql/tmp` 새로 탑재 된 공유에 `/var/opt/mssql/data`입니다. 이 수행 해야 **주 노드에서**합니다. 'Mssql' 로컬 사용자 읽기 / 쓰기 권한을 부여 하는 있는지 확인 합니다.

   ``` 
   $ sudo chown mssql /var/opt/mssql/data
   $ sudo chgrp mssql /var/opt/mssql/data
   $ sudo su mssql
   $ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/
   $ rm /var/opt/mssql/tmp/*
   $ exit
   ``` 
 
1.  SQL Server의 새 파일 경로 사용 하 여 성공적으로 시작 하는 유효성을 검사 합니다. 각 노드에서이 작업을 수행 합니다. 이 시점에서 한 번에 하나의 노드만 SQL Server를 실행 해야 합니다. 실행할 수 없습니다 둘 다 동시에는 모두 데이터 파일에 동시에 (을 실수로 두 노드에서 모두 SQL Server를 시작 하지 않도록 클러스터 파일 시스템 리소스를 사용 하 여 다른 노드에 의해 두 번 공유를 탑재 되지 않은 되도록) 액세스를 시도 하기 때문입니다. SQL Server 시작한 상태를 확인 한 다음 SQL Server를 중지 하는 다음 명령을 합니다.
 
   ```bash
   sudo systemctl start mssql-server
   sudo systemctl status mssql-server
   sudo systemctl stop mssql-server
   ```
 
이 시점에서 SQL Server의 두 인스턴스는 공유 저장소에 있는 데이터베이스 파일을 사용 하 여 실행 하도록 구성 됩니다. Pacemaker 용 SQL Server를 구성 하려면 다음 단계가입니다. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>설치 하 고 각 클러스터 노드에서 Pacemaker 구성


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

   > 다음 포트 pacemaker 클러스터의 다른 노드와 통신할 수를 열어야 할 기본 제공 고가용성 구성 되지 않은 다른 방화벽을 사용 하는 경우
   >
   > * TCP: 2224 3121, 21064 포트
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

## <a name="create-the-cluster"></a>클러스터 만들기 

1. 노드 중 하나에서 클러스터를 만듭니다.

   ```bash
   sudo pcs cluster auth <nodeName1 nodeName2 ...> -u hacluster
   sudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 ...>
   sudo pcs cluster start --all
   ```

   > RHEL HA 추가 기능 KVM 및 VMWare에 대 한 에이전트 펜싱에 있습니다. 펜스는 다른 모든 하이퍼바이저에 서 사용할 수 없게 해야 합니다. 펜싱 에이전트를 사용 하지 않도록 설정 프로덕션 환경에서는 권장 되지 않습니다. 시간을 기준으로 HyperV 또는 클라우드 환경에 대 한 펜스 에이전트가 있습니다. 이러한 구성 중 하나를 실행 중인 경우에 펜싱을 사용 하지 않도록 설정 해야 합니다. \**이 프로덕션 시스템에서 권장 되지 않습니다.**

   다음 명령을 펜스 에이전트를 사용 하지 않도록 설정 합니다.

   ```bash
   sudo pcs property set stonith-enabled=false
   sudo pcs property set start-failure-is-fatal=false
   ```

2. SQL Server, 파일 시스템 및 가상 IP 리소스에 대 한 클러스터 리소스를 구성 하 고 클러스터 구성을 푸시하십시오. 다음과 같은 정보가 필요합니다.

   - **SQL Server 리소스 이름**: 클러스터형된 SQL Server 리소스의 이름입니다. 
   - **부동 IP 리소스 이름**: 가상 IP 주소 리소스에 대 한 이름입니다.
   - **IP 주소**: SQL Server의 클러스터형된 인스턴스에 연결 하려면 클라이언트에서 사용할 IP 주소입니다. 
   - **파일 시스템 리소스 이름**: 파일 시스템 리소스의 이름입니다.
   - **device**: NFS 공유 경로
   - **device**: 공유에 탑재 되는 로컬 경로
   - **fstype**: 파일 공유 형식 (예: nfs)

   사용자 환경에 대 한 다음 스크립트에서 값을 업데이트 합니다. 구성 및 클러스터 된 서비스를 시작 하려면 하나의 노드에서 실행 합니다.  

   ```bash
   sudo pcs cluster cib cfg 
   sudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fci
   sudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>
   sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>
   sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>
   sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName> 
   sudo pcs cluster cib-push cfg
   ```

   예를 들어, 다음 스크립트 라는 클러스터형 SQL Server 리소스를 만듭니다 `mssqlha`, 및 IP 주소를 사용 하 여 부동 IP 리소스를 `10.0.0.99`입니다. 또한 파일 시스템 리소스를 만들고 모든 리소스는 SQL 리소스와 동일한 노드에 배치 제약 조건을 추가 합니다. 

   ```bash
   sudo pcs cluster cib cfg
   sudo pcs -f cfg resource create mssqlha ocf:mssql:fci
   sudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99
   sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"
   sudo pcs -f cfg constraint colocation add virtualip mssqlha
   sudo pcs -f cfg constraint colocation add fs mssqlha
   sudo pcs cluster cib-push cfg
   ```

   구성으로 푸시 후 한 노드에서 SQL Server가 시작 됩니다. 

3. SQL Server가 시작 되었는지 확인 합니다. 

   ```bash
   sudo pcs status 
   ```

   다음 예제에서는 Pacemaker SQL Server의 클러스터형된 인스턴스를 성공적으로 시작 하는 경우 결과 보여 줍니다. 

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

* [부터 클러스터](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf) Pacemaker에서 가이드

## <a name="next-steps"></a>다음 단계

[Red Hat Enterprise Linux 공유 디스크 클러스터에서 SQL Server를 작동](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
