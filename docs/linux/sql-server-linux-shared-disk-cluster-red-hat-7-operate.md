---
title: SQL Server on Linux의 RHEL FCI 작동
description: FCI 수동 장애 조치, 클러스터에 노드 추가 또는 제거와 같은 고가용성을 위해 SQL Server용 RHEL(Red Hat Enterprise Linux) 공유 디스크 FCI(장애 조치 클러스터 인스턴스)를 작동하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 075ab7d8-8b68-43f3-9303-bbdf00b54db1
ms.openlocfilehash: 76c59c6c7b821bfcc9eb76ca3a694a1c69095ce1
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558528"
---
# <a name="operate-rhel-failover-cluster-instance-fci-for-sql-server"></a>SQL Server의 RHEL FCI(장애 조치 클러스터 인스턴스) 작동

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Red Hat Enterprise Linux를 사용하여 공유 디스크 장애 조치(failover) 클러스터에서 SQL Server에 대해 다음 작업을 수행 하는 방법을 설명합니다.

- 수동으로 클러스터 장애 조치(failover)
- 장애 조치(failover) 클러스터 SQL Server 서비스 모니터링
- 클러스터 노드 추가
- 클러스터 노드 제거
- SQL Server 리소스 모니터링 빈도 변경

## <a name="architecture-description"></a>아키텍처 설명

클러스터링 계층은 [Pacemaker](https://clusterlabs.org/) 위에 빌드된 RHEL(Red Hat Enterprise Linux) [HA 추가 기능](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)을 기반으로 합니다. Corosync 및 Pacemaker는 통신 및 리소스 관리를 조정합니다. SQL Server 인스턴스는 두 노드 중 하나에서 활성화됩니다.

다음 다이어그램에서는 SQL Server를 사용하는 Linux 클러스터의 구성 요소를 보여 줍니다. 

![Red Hat Enterprise Linux 7 공유 디스크 SQL 클러스터](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

클러스터 구성, 리소스 에이전트 옵션 및 관리에 대한 자세한 내용은 [RHEL 참조 설명서](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)를 참조하세요.

## <a name = "failManual"></a>수동으로 클러스터 장애 조치(failover)

`resource move` 명령은 대상 노드에서 리소스를 강제로 시작하는 제약 조건을 만듭니다.  `move` 명령을 실행한 후 `clear` 리소스를 실행하면 제약 조건이 제거되므로 리소스를 다시 이동하거나 리소스를 자동으로 장애 조치(failover)할 수 있습니다. 

```bash
sudo pcs resource move <sqlResourceName> <targetNodeName>  
sudo pcs resource clear <sqlResourceName> 
```

다음 예제에서는 **mssqlha** 리소스를 **sqlfcivm2**라는 노드로 이동한 후 제약 조건을 제거하므로 리소스가 나중에 다른 노드로 이동할 수 있습니다.  

```bash
sudo pcs resource move mssqlha sqlfcivm2 
sudo pcs resource clear mssqlha 
```

## <a name="monitor-a-failover-cluster-sql-server-service"></a>장애 조치(failover) 클러스터 SQL Server 서비스 모니터링

현재 클러스터 상태 보기:

```bash
sudo pcs status  
```

클러스터 및 리소스의 라이브 상태 보기:

```bash
sudo crm_mon 
```

`/var/log/cluster/corosync.log`에서 리소스 에이전트 로그 보기

## <a name="add-a-node-to-a-cluster"></a>클러스터에 노드 추가

1. 각 노드의 IP 주소를 확인합니다. 다음 스크립트는 현재 노드의 IP 주소를 보여 줍니다. 

   ```bash
   ip addr show
   ```

3. 새 노드에는 15자 이하의 고유한 이름 필요합니다. 기본적으로 Red Hat Linux에서 컴퓨터 이름은 `localhost.localdomain`입니다. 이 기본 이름은 고유하지 않을 수 있으며 너무 깁니다. 컴퓨터 이름을 새 노드로 설정합니다. 컴퓨터 이름을 `/etc/hosts`에 추가하여 설정합니다. 다음 스크립트를 사용하면 `/etc/hosts`를 `vi`로 편집할 수 있습니다. 

   ```bash
   sudo vi /etc/hosts
   ```

   다음 예제에서는 `sqlfcivm1`, `sqlfcivm2` 및 `sqlfcivm3`이라는 세 개의 노드가 추가된 `/etc/hosts`를 보여 줍니다.

   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1         localhost localhost6 localhost6.localdomain6
   10.128.18.128 fcivm1
   10.128.16.77 fcivm2
   10.128.14.26 fcivm3
    ```
    
   이 파일은 모든 노드에서 동일해야 합니다. 

1. 새 노드에서 SQL Server 서비스를 중지합니다.

1. 지침에 따라 데이터베이스 파일 디렉터리를 공유 위치에 탑재합니다.

   NFS 서버에서 `nfs-utils`를 설치합니다.

   ```bash
   sudo yum -y install nfs-utils 
   ``` 

   클라이언트 및 NFS 서버에서 방화벽을 엽니다. 

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

   /etc/fstab 파일을 편집하여 mount 명령을 포함합니다. 

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr
   ```

   변경 내용을 적용하려면 `mount -a`를 실행합니다.
   
1. 새 노드에서 Pacemaker 로그인을 위한 SQL Server 사용자 이름 및 암호를 저장할 파일을 만듭니다. 다음 명령은 이 파일을 만들고 채웁니다.

   ```bash
   sudo touch /var/opt/mssql/passwd
   sudo echo "<loginName>" >> /var/opt/mssql/secrets/passwd
   sudo echo "<loginPassword>" >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/passwd
   sudo chmod 600 /var/opt/mssql/passwd
   ```

3. 새 노드에서 Pacemaker 방화벽 포트를 엽니다. `firewalld`를 사용하여 이러한 포트를 열려면 다음 명령을 실행합니다.

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > [!NOTE]
   > 기본 제공된 고가용성 구성이 없는 또 다른 방화벽을 사용하는 경우 Pacemaker가 클러스터의 다른 노드와 통신할 수 있으려면 다음 포트를 열어야 합니다.
   >
   > * TCP: 포트 2224, 3121, 21064
   > * UDP: 포트 5405

1. 새 노드에 Pacemaker 패키지를 설치합니다.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
 
2. Pacemaker 및 Corosync 패키지를 설치할 때 생성된 기본 사용자의 암호를 설정합니다. 기존 노드와 동일한 암호를 사용합니다. 

   ```bash
   sudo passwd hacluster
   ```
 
3. `pcsd` 서비스 및 Pacemaker를 사용하도록 설정하고 시작합니다. 이렇게 하면 다시 부팅된 후 새 노드가 클러스터에 다시 조인할 수 있습니다. 새 노드에서 다음 명령을 실행합니다.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. SQL Server용 FCI 리소스 에이전트를 설치합니다. 새 노드에서 다음 명령을 실행합니다. 

   ```bash
   sudo yum install mssql-server-ha
   ```

1. 클러스터의 기존 노드에서 새 노드를 인증하고 클러스터에 추가합니다.

    ```bash
    sudo pcs    cluster auth <nodeName3> -u hacluster 
    sudo pcs    cluster node add <nodeName3> 
    ```

    다음 예제에서는 **vm3**이라는 노드를 클러스터에 추가합니다.

    ```bash
    sudo pcs    cluster auth  
    sudo pcs    cluster start 
    ```

## <a name="remove-nodes-from-a-cluster"></a>클러스터에서 노드 제거

클러스터에서 노드를 제거하려면 다음 명령을 실행합니다.

```bash
sudo pcs    cluster node remove <nodeName>  
```

## <a name="change-the-frequency-of-sqlservr-resource-monitoring-interval"></a>sqlservr 리소스 모니터링 간격의 빈도 변경

```bash
sudo pcs    resource op monitor interval=<interval>s <sqlResourceName> 
```

다음 예제에서는 mssql 리소스의 모니터링 간격을 2초로 설정합니다.

```bash
sudo pcs    resource op monitor interval=2s mssqlha 
```
## <a name="troubleshoot-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>SQL Server에 대한 Red Hat Enterprise Linux 공유 디스크 클러스터 문제 해결

클러스터 문제를 해결할 때 세 개의 디먼이 함께 작동하여 클러스터 리소스를 관리하는 방법을 이해하는 데 도움이 될 수 있습니다. 

| 데몬 | Description 
| ----- | -----
| Corosync | 클러스터 노드 간에 쿼럼 멤버 자격 및 메시징을 제공합니다.
| Pacemaker | Corosync의 맨 위에 있으며 리소스에 대한 상태 머신을 제공합니다. 
| PCSD | `pcs` 도구를 통해 Pacemaker 및 Corosync를 모두 관리합니다.

`pcs` 도구를 사용하려면 PCSD가 실행되고 있어야 합니다. 

### <a name="current-cluster-status"></a>현재 클러스터 상태 

`sudo pcs status`는 각 노드의 클러스터, 쿼럼, 노드, 리소스 및 디먼 상태에 대한 기본 정보를 반환합니다. 

정상 pacemaker 쿼럼 출력의 예는 다음과 같습니다.

```
Cluster name: MyAppSQL 
Last updated: Wed Oct 31 12:00:00 2016  Last change: Wed Oct 31 11:00:00 2016 by root via crm_resource on sqlvmnode1 
Stack: corosync 
Current DC: sqlvmnode1  (version 1.1.13-10.el7_2.4-44eb2dd) - partition with quorum 
3 nodes and 1 resource configured 

Online: [ sqlvmnode1 sqlvmnode2 sqlvmnode3] 

Full list of resources: 

mssqlha (ocf::sql:fci): Started sqlvmnode1 

PCSD Status: 
sqlvmnode1: Online 
sqlvmnode2: Online 
sqlvmnode3: Online 

Daemon Status: 
corosync: active/disabled 
pacemaker: active/enabled 
```

이 예제에서 `partition with quorum`은 노드의 과반수 쿼럼이 온라인 상태임을 의미합니다. 클러스터가 노드의 과반수 쿼럼을 잃은 경우 `pcs status`는 `partition WITHOUT quorum`을 반환하며 모든 리소스가 중지됩니다. 

`online: [sqlvmnode1 sqlvmnode2 sqlvmnode3]`는 현재 클러스터에 참여하는 모든 노드의 이름을 반환합니다. 노드가 참여 중이 아니면 `pcs status`는 `OFFLINE: [<nodename>]`를 반환합니다.

`PCSD Status`는 각 노드의 클러스터 상태를 표시합니다.

### <a name="reasons-why-a-node-may-be-offline"></a>노드가 오프라인일 수 있는 이유

노드가 오프라인일 경우 다음 항목을 확인합니다.

- **방화벽**

    Pacemaker가 통신할 수 있으려면 모든 노드에서 다음 포트가 열려 있어야 합니다.
    
    - **TCP: 2224, 3121, 21064

- **Pacemaker 또는 Corosync 서비스 실행**

- **노드 통신**

- **노드 이름 매핑**

## <a name="additional-resources"></a>추가 리소스

* Pacemaker의 [Cluster from Scratch](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf)(처음부터 클러스터) 가이드

## <a name="next-steps"></a>다음 단계

[SQL Server용 Red Hat Enterprise Linux 공유 디스크 클러스터 구성](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)

