---
title: SQL Server에 대 한 공유 클러스터 Red Hat Enterprise Linux 작동 | Microsoft Docs
description: SQL Server에 대 한 Red Hat Enterprise Linux 공유 디스크 클러스터를 구성 하 여 높은 가용성을 구현 합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 075ab7d8-8b68-43f3-9303-bbdf00b54db1
ms.openlocfilehash: e6952c261530fc7773686e94c1c9a462385f4096
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="operate-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Red Hat Enterprise Linux 공유 디스크 클러스터 SQL Server에 대 한 작동

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Red Hat Enterprise Linux를 사용 하 여 공유 디스크 장애 조치 클러스터에서 SQL Server에 대 한 다음 작업을 수행 하는 방법에 설명 합니다.

- 수동으로 장애 조치 클러스터
- 장애 조치 클러스터 SQL Server 서비스를 모니터링 합니다.
- 클러스터 노드 추가
- 클러스터 노드 제거
- SQL Server 리소스를 모니터링 빈도 변경

## <a name="architecture-description"></a>아키텍처 설명

Red Hat Enterprise Linux (RHEL)를 기반으로 클러스터링 레이어 [HA 추가 기능](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) 기반으로 구축 [Pacemaker](http://clusterlabs.org/)합니다. Corosync 및 Pacemaker 클러스터 통신 및 리소스 관리를 조정 합니다. SQL Server 인스턴스는 하나의 노드 또는 다른에서 활성입니다.

다음 다이어그램에서는 SQL Server를 사용 하 여 Linux 클러스터의 구성 요소를 보여 줍니다. 

![Red Hat Enterprise Linux 7 공유 디스크 SQL 클러스터](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

클러스터 구성, 리소스 에이전트 옵션 및 관리에 대 한 자세한 내용은 방문 [RHEL 참조 설명서](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)합니다.

## <a name = "failManual"></a>장애 조치 클러스터를 수동으로

`resource move` 명령에서 대상 노드를 시작 하려면 리소스를 강제로 제약 조건을 만듭니다.  실행 한 후의 `move` 실행 리소스 명령을 `clear` 리소스를 다시 이동 하거나 자동으로 장애 조치 하는 리소스를 사용할 수 있도록 제한이 제거 됩니다. 

```bash
sudo pcs resource move <sqlResourceName> <targetNodeName>  
sudo pcs resource clear <sqlResourceName> 
```

다음 예제에서는 이동는 **mssqlha** 리소스가 이라는 노드로 **sqlfcivm2**, 나중에 리소스를 다른 노드로 이동할 수 있도록 제약 조건을 제거 합니다.  

```bash
sudo pcs resource move mssqlha sqlfcivm2 
sudo pcs resource clear mssqlha 
```

## <a name="monitor-a-failover-cluster-sql-server-service"></a>장애 조치 클러스터 SQL Server 서비스를 모니터링 합니다.

현재 클러스터 상태를 확인 합니다.

```bash
sudo pcs status  
```

클러스터 및 리소스의 실시간 상태 보기:

```bash
sudo crm_mon 
```

리소스 에이전트 로그 보기 `/var/log/cluster/corosync.log`

## <a name="add-a-node-to-a-cluster"></a>클러스터에 노드 추가

1. 각 노드에 대 한 IP 주소를 확인 합니다. 다음 스크립트는 현재 노드의의 IP 주소를 보여 줍니다. 

   ```bash
   ip addr show
   ```

3. 새 노드는 15 자 하는 한 고유 이름을 지정 해야이 있습니다. Red Hat Linux에서 기본적으로 컴퓨터 이름이 `localhost.localdomain`합니다. 이 기본 이름은 고유 되지 않을 수 있습니다 및 너무 깁니다. 새 노드에 다음 컴퓨터 이름을 설정 합니다. 컴퓨터 이름을 추가 하 여 설정 `/etc/hosts`합니다. 다음 스크립트를 사용하면 `/etc/hosts`를 `vi`로 편집할 수 있습니다. 

   ```bash
   sudo vi /etc/hosts
   ```

   다음 예제와 `/etc/hosts` 라는 세 개의 노드에 대 한 추가 내용은 `sqlfcivm1`, `sqlfcivm2`, 및`sqlfcivm3`합니다.

   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1         localhost localhost6 localhost6.localdomain6
   10.128.18.128 fcivm1
   10.128.16.77 fcivm2
   10.128.14.26 fcivm3
    ```
    
   파일의 모든 노드에서 동일 해야 합니다. 

1. 새 노드의 SQL Server 서비스를 중지 합니다.

1. 공유 위치에 데이터베이스 파일 디렉터리를 탑재 하도록 지침을 따르세요.

   NFS 서버에서 설치 `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils 
   ``` 

   클라이언트 및 NFS 서버에 방화벽을 열고 

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

   Mount 명령을 포함 하도록 /etc/fstab 파일을 편집 합니다. 

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr
   ```

   실행 `mount -a` 변경 내용을 적용 하려면에 대 한 합니다.
   
1. 새 노드에서 SQL Server 사용자 이름 및 Pacemaker 로그인 암호를 저장 하기 위해 파일을 만듭니다. 다음 명령은 이 파일을 만들고 채웁니다.

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
   > 기본 제공된 고가용성 구성이 없는 또 다른 방화벽을 사용 중인 경우 Pacemaker가 클러스터의 다른 노드와 통신할 수 있으려면 다음 포트를 열어야 합니다.
   >
   > * TCP: 포트 2224, 3121, 21064
   > * UDP: 포트 5405

1. 새 노드에 Pacemaker 패키지를 설치 합니다.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
 
2. Pacemaker 및 Corosync 패키지를 설치할 때 생성된 기본 사용자의 암호를 설정합니다. 기존 노드와 동일한 암호를 사용 합니다. 

   ```bash
   sudo passwd hacluster
   ```
 
3. `pcsd` 서비스 및 Pacemaker를 사용하도록 설정하고 시작합니다. 따라서 새 노드를 다시 부팅 한 후 클러스터에 다시 연결할 수 있습니다. 새 노드에서 다음 명령을 실행 합니다.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. SQL Server용 FCI 리소스 에이전트를 설치합니다. 새 노드에서 다음 명령을 실행 합니다. 

   ```bash
   sudo yum install mssql-server-ha
   ```

1. 클러스터에서 기존 노드에 새 노드를 인증 하 고 클러스터에 추가 합니다.

    ```bash
    sudo pcs    cluster auth <nodeName3> -u hacluster 
    sudo pcs    cluster node add <nodeName3> 
    ```

    명명 된 노드를 추가 하는 다음 예제에서는 **vm3** 클러스터에 있습니다.

    ```bash
    sudo pcs    cluster auth  
    sudo pcs    cluster start 
    ```

## <a name="remove-nodes-from-a-cluster"></a>클러스터에서 노드를 제거 합니다.

다음 명령을 실행 하는 클러스터에서 노드를 삭제 합니다.

```bash
sudo pcs    cluster node remove <nodeName>  
```

## <a name="change-the-frequency-of-sqlservr-resource-monitoring-interval"></a>Sqlservr 리소스 모니터링 간격의 빈도 변경

```bash
sudo pcs    resource op monitor interval=<interval>s <sqlResourceName> 
```

다음 예제에서는 mssql 리소스에 대 한 2 초를 모니터링 하는 간격을 설정합니다.

```bash
sudo pcs    resource op monitor interval=2s mssqlha 
```
## <a name="troubleshoot-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Red Hat Enterprise Linux 공유 디스크 클러스터 SQL Server에 대 한 문제 해결

클러스터 문제 해결에 세 개의 데몬 함께 클러스터 리소스를 관리 작동 방식을 이해 하려면 도움이 될 합니다. 

| 데몬 | Description 
| ----- | -----
| Corosync | 쿼럼 멤버 자격 및 클러스터 노드 간 메시징을 제공 합니다.
| Pacemaker | Corosync 맨 위에 있는 하 고 리소스에 대 한 상태 시스템을 제공 합니다. 
| PCSD | Pacemaker와 Corosync를 통해 관리 하는 `pcs` 도구

PCSD 사용 하기 위해 실행 해야 `pcs` 도구입니다. 

### <a name="current-cluster-status"></a>현재 클러스터 상태 

`sudo pcs status` 각 노드에 대 한 클러스터, 쿼럼, 노드, 리소스 및 데몬 상태에 대 한 기본 정보를 반환 합니다. 

정상 pacemaker 쿼럼 출력의 예는 다음과 같습니다.

```
Cluster name: MyAppSQL 
Last updated: Wed Oct 31 12:00:00 2016  Last change: Wed Oct 31 11:00:00 2016 by root via crm_resource on sqlvmnode1 
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

예제에서는 `partition with quorum` 노드 과반수 쿼럼 온라인 임을 의미 합니다. 클러스터에서 노드 과반수 쿼럼 손실 되 면 `pcs status` 돌아갑니다 `partition WITHOUT quorum` 않으며 리소스를 모두 중지 됩니다. 

`online: [sqlvmnode1 sqlvmnode2 sqlvmnode3]` 현재 클러스터에 참여 하는 모든 노드의 이름을 반환 합니다. 모든 노드가 참여 하지 않는 경우 `pcs status` 반환 `OFFLINE: [<nodename>]`합니다.

`PCSD Status` 각 노드에 대해 클러스터 상태가 표시 됩니다.

### <a name="reasons-why-a-node-may-be-offline"></a>이유로 노드가 오프 라인 수 수 있습니다.

노드가 오프 라인 상태일 때에 다음 항목을 확인 합니다.

- **방화벽**

    다음 포트가 열려 Pacemaker 통신할 수에 대 한 모든 노드에 있어야 합니다.
    
    - **TCP: 2224, 3121, 21064

- **Pacemaker 또는 Corosync 서비스 실행**

- **노드 통신**

- **노드 이름 매핑**

## <a name="additional-resources"></a>추가 리소스

* [처음부터 클러스터](http://clusterlabs.org/doc/Cluster_from_Scratch.pdf) Pacemaker에서 가이드

## <a name="next-steps"></a>다음 단계

[SQL Server에 대 한 Red Hat Enterprise Linux 공유 디스크 클러스터를 구성 합니다.](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)

