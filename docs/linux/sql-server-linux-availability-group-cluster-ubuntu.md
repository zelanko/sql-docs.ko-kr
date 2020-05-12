---
title: 가용성 그룹의 Ubuntu 클러스터 구성
titleSuffix: SQL Server on Linux
description: Ubuntu에서 3노드 클러스터를 만들고 이전에 만든 가용성 그룹 리소스를 클러스터에 추가하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.openlocfilehash: a42d031ee66ee455af91dbcce233140a7ab0a171
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "83001103"
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>Ubuntu 클러스터 및 가용성 그룹 리소스 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Ubuntu에서 3개 노드 클러스터를 만들고 이전에 만든 가용성 그룹을 클러스터의 리소스로 추가하는 방법을 설명합니다. 고가용성을 위해 Linux의 가용성 그룹에는 세 개의 노드가 필요합니다. [가용성 그룹 구성의 고가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)를 참조하세요.

> [!NOTE] 
> 이때 Linux의 Pacemaker와 SQL Server의 통합은 Windows의 WSFC와 같이 결합되지 않습니다. SQL 내에 클러스터의 존재 여부에 대한 정보는 없으며, 모든 오케스트레이션은 외부에서 진행되고, 서비스는 Pacemaker에서 독립 실행형 인스턴스로 제어됩니다. 또한 가상 네트워크 이름은 WSFC에만 해당되며, Pacemaker에는 동일한 항목이 없습니다. 클러스터 정보를 쿼리하는 Always On 동적 관리 뷰는 빈 행을 반환합니다. 장애 조치(failover) 후에도 수신기를 만들어 투명한 재연결에 계속 사용할 수 있지만, 다음 섹션에서 설명하는 것처럼 가상 IP 리소스를 만드는 데 사용되는 IP에 DNS 서버의 수신기 이름을 수동으로 등록해야 합니다.

다음 섹션에서는 장애 조치(failover) 클러스터 솔루션을 설정하는 단계를 안내합니다. 

## <a name="roadmap"></a>로드맵

고가용성을 위해 Linux 서버에서 가용성 그룹을 만드는 단계는 Windows Server 장애 조치(failover) 클러스터의 단계와 다릅니다. 다음 목록에서는 개괄적인 단계를 설명합니다. 

1. [클러스터 노드에서 SQL Server를 구성합니다](sql-server-linux-setup.md).

2. [가용성 그룹을 만듭니다](sql-server-linux-availability-group-configure-ha.md). 

3. Pacemaker와 같은 클러스터 리소스 관리자를 구성합니다. 이러한 지침은 이 문서에 포함되어 있습니다.
   
   클러스터 리소스 관리자를 구성하는 방법은 특정 Linux 배포에 따라 다릅니다. 

   >[!IMPORTANT]
   >프로덕션 환경에는 고가용성을 위한 STONITH와 같은 펜싱 에이전트가 필요합니다. 이 설명서의 데모에서는 펜싱 에이전트를 사용하지 않습니다. 데모는 테스트 및 유효성 검사를 위해서만 제공됩니다. 
   >
   >Linux 클러스터는 펜싱을 사용하여 클러스터를 알려진 상태로 되돌립니다. 펜싱을 구성하는 방법은 배포 및 환경에 따라 달라집니다. 현재, 일부 클라우드 환경에서는 펜싱을 사용할 수 없습니다. 자세한 내용은 [RHEL 고가용성 클러스터의 지원 정책 - 가상화 플랫폼](https://access.redhat.com/articles/29440)을 참조하세요.
   >
   >펜싱은 일반적으로 운영 체제에서 구현되며 환경에 따라 달라집니다. 운영 체제 배포자 문서에서 펜싱 지침을 확인합니다.

5.  [가용성 그룹을 클러스터의 리소스로 추가합니다](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource). 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>각 클러스터 노드에 Pacemaker 설치 및 구성

1. 모든 노드에서 방화벽 포트를 엽니다. Pacemaker 고가용성 서비스, SQL Server 인스턴스 및 가용성 그룹 엔드포인트에 대한 포트를 엽니다. SQL Server 실행 서버의 기본 TCP 포트는 1433입니다.  

   ```bash
   sudo ufw allow 2224/tcp
   sudo ufw allow 3121/tcp
   sudo ufw allow 21064/tcp
   sudo ufw allow 5405/udp
        
   sudo ufw allow 1433/tcp # Replace with TDS endpoint
   sudo ufw allow 5022/tcp # Replace with DATA_MIRRORING endpoint
        
   sudo ufw reload
   ```
   
   또는 방화벽을 사용하지 않도록 설정할 수 있습니다.
        
   ```bash
   sudo ufw disable
   ```

1. Pacemaker 패키지를 설치합니다. 모든 노드에서 다음 명령을 실행합니다.

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. Pacemaker 및 Corosync 패키지를 설치할 때 생성된 기본 사용자의 암호를 설정합니다. 모든 노드에서 같은 암호를 사용합니다. 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>pcsd 서비스 및 Pacemaker 사용 및 시작

다음 명령은 pcsd 서비스 및 pacemaker를 사용하도록 설정하고 시작합니다. 모든 노드에서 실행합니다. 이렇게 하면 다시 부팅된 후 노드가 클러스터에 다시 조인할 수 있습니다. 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>Enable pacemaker 명령은 'pacemaker Default-Start contains no runlevels, aborting' 오류를 발생하며 완료될 수 있습니다. 이 오류는 무해하므로 클러스터 구성을 계속할 수 있습니다. 

## <a name="create-the-cluster"></a>클러스터 만들기

1. 모든 노드에서 기존 클러스터 구성을 제거합니다. 

   'sudo apt-get install pcs'를 실행하면 pacemaker, corosync 및 pcs가 동시에 설치되고 3개의 서비스가 모두 실행되기 시작합니다.  corosync를 시작하면 템플릿 '/etc/cluster/corosync.conf' 파일이 생성됩니다.  다음 단계를 성공적으로 진행하려면 이 파일이 없어야 합니다. 따라서 해결 방법은 pacemaker / corosync를 중지하고 '/etc/cluster/corosync.conf'를 삭제하는 것입니다. 그러면 다음 단계가 성공적으로 완료됩니다. 'pcs cluster destroy'는 동일한 작업을 수행하며, 일회성 초기 클러스터 설정 단계로 사용할 수 있습니다.
   
   다음 명령은 기존 클러스터 구성 파일을 제거하고 모든 클러스터 서비스를 중지합니다. 이렇게 하면 클러스터가 영구적으로 삭제됩니다. 이 명령을 사전 프로덕션 환경에서 첫 번째 단계로 실행합니다. 'pcs cluster destroy'가 pacemaker 서비스를 사용하지 않도록 설정했으므로 다시 사용하도록 설정해야 합니다. 모든 노드에서 다음 명령을 실행합니다.
   
   >[!WARNING]
   >이 명령은 기존 클러스터 리소스를 모두 삭제합니다.

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. 클러스터를 만듭니다. 

   >[!WARNING]
   >클러스터링 공급업체에서 조사 중인 알려진 문제로 인해, 클러스터를 시작하면('pcs cluster start') 다음 오류를 발생하며 실패합니다. 이것은 클러스터 설치 명령이 실행될 때 생성된 /etc/corosync/corosync.conf에 구성된 로그 파일이 잘못되었기 때문입니다. 이 문제를 해결하려면 로그 파일을 /var/log/corosync/corosync.log로 변경합니다. 또는 /var/log/cluster/corosync.log 파일을 만들 수 있습니다.
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
다음 명령은 3개 노드 클러스터를 만듭니다. 스크립트를 실행하기 전에 `< ... >` 사이의 값을 바꿉니다. 주 노드에서 다음 명령을 실행합니다. 

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2...> <node3>
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >이전에 같은 노드에서 클러스터를 구성한 경우 'pcs cluster setup'을 실행할 때 '--force' 옵션을 사용해야 합니다. 이 방법은 'pcs cluster destroy'를 실행하는 것과 같고 'sudo systemctl enable pacemaker'를 사용하여 Pacemaker 서비스를 다시 사용하도록 설정해야 합니다.


## <a name="configure-fencing-stonith"></a>펜싱(STONITH) 구성

Pacemaker 클러스터 공급업체는 STONITH를 사용하도록 설정하고 지원되는 클러스터 설정에 대해 펜싱 디바이스를 구성하도록 요구합니다. Cluster Resource Manager가 노드 상태 또는 노드의 리소스 상태를 확인할 수 없는 경우 펜싱을 사용하여 클러스터를 알려진 상태로 다시 전환합니다. 리소스 수준 펜싱은 주로 리소스를 구성하여 중단 시 데이터 손상이 발생하지 않도록 합니다. 예를 들어 DRBD(Distributed Replicated Block Device)에서 리소스 수준 펜싱을 사용하여 통신 링크의 작동이 중단될 경우 노드의 디스크를 오래된 것으로 표시할 수 있습니다. 노드 수준 펜싱은 노드가 리소스를 실행하지 않도록 합니다. 노드를 다시 설정하여 이 작업을 수행하며, 해당 Pacemaker 구현을 STONITH(“shoot the other node in the head”의 약어)라고 합니다. Pacemaker는 서버에 대한 무정전 전원 공급 장치 또는 관리 인터페이스 카드와 같은 다양한 펜싱 디바이스를 지원합니다. 자세한 내용은 [Pacemaker 클러스터 기초](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/) 및 [펜싱 및 Stonith](https://clusterlabs.org/doc/crm_fencing.html)를 참조하세요. 

노드 수준 펜싱 구성은 사용자 환경에 따라 크게 좌우되므로 이 자습서에서는 사용하지 않도록 설정합니다(나중에 구성할 수 있음). 주 노드에서 다음 스크립트를 실행합니다. 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>STONITH를 사용하지 않도록 설정하는 기능은 테스트 목적으로만 제공됩니다. 프로덕션 환경에서 Pacemaker를 사용하려는 경우 해당 환경에 따라 STONITH 구현을 계획하고 사용 상태로 유지해야 합니다. 특정 배포의 펜싱 에이전트에 대한 자세한 내용은 운영 체제 공급업체에 문의하세요. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>클러스터 속성 cluster-recheck-interval 설정

`cluster-recheck-interval`은 클러스터에서 리소스 매개 변수, 제약 조건 또는 기타 클러스터 옵션의 변경 내용을 확인하는 폴링 간격을 나타냅니다. 복제본의 작동이 중단되면 클러스터는 `failure-timeout` 값과 `cluster-recheck-interval` 값을 통해 바인딩된 간격으로 복제본을 다시 시작하려고 합니다. 예를 들어 `failure-timeout`을 60초로 설정하고 `cluster-recheck-interval`을 120초로 설정한 경우 60초보다 크고 120초보다 작은 간격으로 다시 시작이 시도됩니다. failure-timeout을 60초로 설정하고 cluster-recheck-interval을 60초보다 큰 값으로 설정하는 것이 좋습니다. cluster-recheck-interval을 작은 값으로 설정하는 것을 권장하지 않습니다.

속성 값을 `2 minutes`로 업데이트하려면 다음 명령을 실행합니다.

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Pacemaker 클러스터에서 관리하는 가용성 그룹 리소스가 이미 있는 경우 사용 가능한 최신 Pacemaker 패키지 1.1.18-11.el7을 사용하는 모든 배포에서 값이 false인 경우의 start-failure-is-fatal 클러스터 설정 동작이 변경된 것을 확인합니다. 이 변경 내용은 장애 조치(failover) 워크플로에 영향을 줍니다. 주 복제본이 중단될 경우 클러스터가 사용 가능한 보조 복제본 중 하나로 장애 조치(failover)되어야 합니다. 예상과 달리, 사용자는 클러스터가 실패한 주 복제본을 시작하려고 계속 시도하는 것을 보게 됩니다. 주 복제본이 영구 중단되어 온라인 상태로 전환되지 않는 경우 클러스터도 사용 가능한 다른 보조 복제본으로 장애 조치(failover)되지 않습니다. 이 변경 내용 때문에 start-failure-is-fatal을 설정하는 이전 권장 구성은 더 이상 유효하지 않으며, 설정을 기본값인 `true`로 되돌려야 합니다. 또한 `failover-timeout` 속성이 포함되도록 AG 리소스를 업데이트해야 합니다. 
>
>속성 값을 `true`로 업데이트하려면 다음 명령을 실행합니다.
>
>```bash
>sudo pcs property set start-failure-is-fatal=true
>```
>
>기존 AG 리소스 속성 `failure-timeout`을 `60s`로 업데이트하려면 다음 명령을 실행합니다(`ag1`을 해당 가용성 그룹 리소스의 이름으로 바꿈).
>
>```bash
>pcs resource update ag1 meta failure-timeout=60s
>```

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>Pacemaker와 연결하기 위해 SQL Server 리소스 에이전트 설치

모든 노드에서 다음 명령을 실행합니다. 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker용 SQL Server 로그인 만들기

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>가용성 그룹 리소스 만들기

가용성 그룹 리소스를 만들려면 `pcs resource create` 명령을 사용하고 리소스 속성을 설정합니다. 아래 명령은 이름이 `ag1`인 가용성 그룹에 대해 `ocf:mssql:ag` 마스터/슬레이브 유형 리소스를 만듭니다. 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>가상 IP 리소스 만들기

가상 IP 주소 리소스를 만들려면 한 노드에서 다음 명령을 실행합니다. 네트워크의 사용 가능한 고정 IP 주소를 사용합니다. 스크립트를 실행하기 전에 `< ... >` 사이의 값을 유효한 IP 주소로 바꿉니다.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Pacemaker에는 해당하는 가상 서버 이름이 없습니다. 문자열 서버 이름을 가리키며 IP 주소를 사용하지 않는 연결 문자열을 사용하려면 DNS에 IP 리소스 주소와 원하는 가상 서버 이름을 등록합니다. DR 구성의 경우 기본 및 DR 사이트의 DNS 서버에 원하는 가상 서버 이름 및 IP 주소를 등록합니다.

## <a name="add-colocation-constraint"></a>공동 배치 제약 조건 추가

리소스를 실행할 위치 선택과 같은, Pacemaker 클러스터의 거의 모든 결정은 점수 비교를 통해 수행됩니다. 점수는 리소스별로 계산되며, Cluster Resource Manager는 특정 리소스에 대해 점수가 가장 높은 노드를 선택합니다. 노드의 리소스 점수가 음수이면 해당 노드에서 리소스를 실행할 수 없습니다. 제약 조건을 사용하여 클러스터의 결정을 구성합니다. 제약 조건에는 점수가 있습니다. 제약 조건의 점수가 INFINITY보다 낮으면 권장 사항일 뿐입니다. INFINITY 점수는 필수 항목임을 의미합니다. 주 복제본과 가상 IP 리소스가 동일한 호스트에 있는지 확인하려면 점수가 INFINITY인 공동 배치 제약 조건을 정의합니다. 공동 배치 제약 조건을 추가하려면 한 노드에서 다음 명령을 실행합니다. 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>정렬 제약 조건 추가

공동 배치 제약 조건에는 암시적 정렬 제약 조건이 있습니다. 이 제약 조건은 가용성 그룹 리소스를 이동하기 전에 가상 IP 리소스를 이동합니다. 기본적으로 이벤트 시퀀스는 다음과 같습니다.

1. 사용자가 node1에서 node2까지 가용성 그룹 주 복제본에 대해 `pcs resource move`를 실행합니다.
1. 가상 IP 리소스가 node1에서 중지됩니다.
1. 가상 IP 리소스가 node2에서 시작됩니다.

   >[!NOTE]
   >이때 node2가 여전히 장애 조치(failover) 이전 보조 복제본이지만, IP 주소는 일시적으로 node2를 가리킵니다. 
   
1. node1의 가용성 그룹 기본 복제본이 보조로 강등됩니다.
1. node2의 가용성 그룹 보조 복제본이 기본으로 승격됩니다. 

IP 주소가 일시적으로 장애 조치(failover) 이전 보조 복제본이 있는 노드를 가리키지 않도록 하려면 정렬 제약 조건을 추가합니다. 

정렬 제약 조건을 추가하려면 한 노드에서 다음 명령을 실행합니다.

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>클러스터를 구성하고 가용성 그룹을 클러스터 리소스로 추가한 후에는 Transact-SQL을 사용하여 가용성 그룹 리소스를 장애 조치(failover)할 수 없습니다. Linux의 SQL Server 클러스터 리소스는 WSFC(Windows Server 장애 조치(failover) 클러스터)에 있을 때처럼 운영 체제와 긴밀하게 결합되지 않습니다. SQL Server 서비스는 클러스터의 현재 상태를 인식하지 못합니다. 모든 오케스트레이션이 클러스터 관리 도구를 통해 수행됩니다. RHEL 또는 Ubuntu에서 `pcs`를 사용합니다. 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>다음 단계

[HA 가용성 그룹 작동](sql-server-linux-availability-group-failover-ha.md)

