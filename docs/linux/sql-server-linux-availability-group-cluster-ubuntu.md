---
title: "SQL Server 가용성 그룹에 클러스터를 Ubuntu 구성 | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.workload: Inactive
ms.openlocfilehash: 797cc24d46fc5a51f514508dd35226d07cda74f4
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>Ubuntu 클러스터와 가용성 그룹 리소스 구성

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 문서에서는 ubuntu 3 개 노드 클러스터를 만들고 이전에 만든된 가용성 그룹에 클러스터 리소스로 추가 하는 방법을 설명 합니다. 고가용성을 위해 Linux에서 가용성 그룹에 노드가 3 개 필요-참조 [가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)합니다.

> [!NOTE] 
> 이 시점에서 linux Pacemaker와 SQL Server의 통합 Windows에서 WSFC와으로으로 결합 된 않습니다. sql에서 클러스터의 존재에 대 한 지식이 없는, 외부 모든 오케스트레이션은 되며 서비스는 독립 실행형 인스턴스로 Pacemaker에 의해 제어 됩니다. 또한 가상 네트워크 이름은 WSFC 관련, Pacemaker에는 동일한 동등한 옵션이 없습니다. Always On 동적 관리 뷰 클러스터 정보를 쿼리 하는 빈 행을 반환 합니다. 장애 조치 후 투명 하 게 다시 연결에 사용할 수신기를 만들 수 있지만 (아래 설명 됨) 가상 IP 리소스를 만드는 데 IP와 함께 DNS 서버에서 수신기 이름은 수동으로 등록 해야 합니다.

다음 섹션에서는 장애 조치 클러스터 솔루션을 설정 하는 단계를 안내 합니다. 

## <a name="roadmap"></a>로드맵

고가용성을 위해 Linux 서버에 가용성 그룹을 만드는 단계는 Windows Server 장애 조치 클러스터에는 단계와에서 다릅니다. 다음 목록에서는 고급 단계를 설명합니다. 

1. [SQL Server 클러스터 노드에서 구성](sql-server-linux-setup.md)합니다.

2. [가용성 그룹 만들기](sql-server-linux-availability-group-configure-ha.md)합니다. 

3. Pacemaker 같은 클러스터 리소스 관리자를 구성 합니다. 이러한 지침은이 문서에 나와 있습니다.
   
   클러스터 리소스 관리자를 구성 하는 방법은 특정 Linux 배포에 따라 달라 집니다. 

   >[!IMPORTANT]
   >프로덕션 환경에서는 고가용성을 위해 STONITH 같은 펜스 에이전트를 해야 합니다. 이 설명서에서 데모 펜싱 에이전트를 사용 하지 마십시오. 데모는 테스트 및 유효성 검사에만 적용 됩니다. 
   
   >Linux 클러스터 펜싱을 사용 하 여 알려진 상태로 클러스터를 반환 합니다. 펜싱을 구성 하는 방법은 배포 및 환경에 따라 달라 집니다. 이때 펜싱 일부 클라우드 환경에서 사용할 수 없는 경우 참조 [RHEL 높은 가용성 클러스터-가상화 플랫폼에 대 한 지원 정책을](https://access.redhat.com/articles/29440) 자세한 정보에 대 한 합니다.

5.  [가용성 그룹에 클러스터 리소스로 추가](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)합니다. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>설치 하 고 각 클러스터 노드에서 Pacemaker 구성

1. 모든 노드에서 방화벽 포트를 엽니다. Pacemaker 가용성이 높은 서비스, SQL Server 인스턴스 및 가용성 그룹 끝점에 대 한 포트를 엽니다. SQL Server를 실행 하는 서버에 대 한 기본 TCP 포트는 1433입니다.  

   ```bash
   sudo ufw allow 2224/tcp
   sudo ufw allow 3121/tcp
   sudo ufw allow 21064/tcp
   sudo ufw allow 5405/udp
        
   sudo ufw allow 1433/tcp # Replace with TDS endpoint
   sudo ufw allow 5022/tcp # Replace with DATA_MIRRORING endpoint
        
   sudo ufw reload
   ```
   
   또는 방화벽을 해제할 수 있습니다.
        
   ```bash
   sudo ufw disable
   ```

1. Pacemaker 패키지를 설치 합니다. 모든 노드에서 다음 명령을 실행 합니다.

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. Pacemaker 및 Corosync 패키지를 설치할 때 생성된 기본 사용자의 암호를 설정합니다. 모든 노드에서 같은 암호를 사용합니다. 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>사용 하도록 설정 하 고 pcsd 서비스 및 Pacemaker 시작

다음 명령을 사용 하도록 설정 하 고 pcsd 서비스 및 pacemaker를 시작 합니다. 모든 노드에서 실행 됩니다. 따라서 노드를를 다시 부팅 한 후 클러스터에 다시 연결할 수 있습니다. 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>'기본 시작 pacemaker 중단 없는 runlevels를 포함 합니다.' 사용 pacemaker 명령을 오류와 함께 완료 됩니다. 이 무시 해도, 클러스터 구성을 계속 수 있습니다. 우리는 다음과 같습니다. 클러스터 공급 업체와이 문제를 해결 합니다.

## <a name="create-the-cluster"></a>클러스터 만들기

1. 모든 노드의 모든 기존 클러스터를 구성을 제거 합니다. 

   실행 중인 'sudo apt get 설치 pc' pacemaker, corosync, 및 pc를 동시에 설치 하 고 서비스의 모든 3을 실행을 시작 합니다.  템플릿이 생성 corosync 시작 ' / etc/cluster/corosync.conf' 파일입니다.  다음 단계가 성공이 파일에 존재할 수 없는 – pacemaker 중지 하려면이 문제를 해결 하도록 / corosync 삭제 ' / etc/cluster/corosync.conf', 다음 단계 성공적으로 완료 됩니다. 동일한 작업을 수행 pc 클러스터 destroy 하 고 한으로 사용할 수 있습니다 시간 초기 클러스터 설치 단계입니다.
   
   다음 명령은 기존 클러스터 구성 파일을 제거 하 고 모든 클러스터 서비스를 중지 합니다. 이 클러스터를 영구적으로 제거합니다. 사전 프로덕션 환경에서 첫 번째 단계로 실행 합니다. 참고로 'pc 클러스터 손상' pacemaker 서비스와 다시 활성화할 수 있습니다에 사용할 수 없습니다. 모든 노드에서 다음 명령을 실행합니다.
   
   >[!WARNING]
   >이 명령은 모든 기존 클러스터 리소스 삭제 됩니다.

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. 클러스터를 만듭니다. 

   >[!WARNING]
   >클러스터링 공급 업체는 조사 하 고, 시작 하는 알려진된 문제로 인해 클러스터 ('pc 클러스터 start') 아래의 오류 하면서 실패 합니다. 해당 하는 클러스터 설치 명령을 실행 하는 때 만들어지는 잘못 /etc/corosync/corosync.conf에 구성 된 로그 파일 때문입니다. 이 문제를 해결 하려면 로그 파일을 변경할: /var/log/corosync/corosync.log 합니다. 또는 /var/log/cluster/corosync.log 파일을 만들 수 있습니다.
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
다음 명령은 세 개 노드 클러스터를 만듭니다. 스크립트를 실행하기 전에 `**< ... >**` 사이의 값을 바꿉니다. 주 노드에서 다음 명령을 실행 합니다. 

   ```bash
   sudo pcs cluster auth **<node1>** **<node2>** **<node3>** -u hacluster -p **<password for hacluster>**
   sudo pcs cluster setup --name **<clusterName>** **<node1>** **<node2…>** **<node3>**
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >이전에 같은 노드에서 클러스터를 구성한 경우 'pcs cluster setup'을 실행할 때 '--force' 옵션을 사용해야 합니다. 이 방법은 'pcs cluster destroy'를 실행하는 것과 같고 'sudo systemctl enable pacemaker'를 사용하여 Pacemaker 서비스를 다시 사용하도록 설정해야 합니다.


## <a name="configure-fencing-stonith"></a>펜스 (STONITH) 구성

Pacemaker 클러스터 공급 업체를 사용 하도록 설정할 STONITH와 지원 되는 클러스터 설치에 대해 구성 된 펜싱 장치에 필요 합니다. 클러스터 리소스 관리자 상태 노드 또는 노드에 있는 리소스의을 확인할 수 없는 경우 펜싱 클러스터도 알려진 상태로 다시 전환 하는 데 사용 됩니다. 리소스 수준 펜싱 하면 주로 리소스를 구성 하 여 중단 시 데이터 손상 되지 않습니다. 리소스 수준 펜싱을 사용할 수 있습니다 예를 들어, 오래 된 경우 처럼 노드에서 디스크를 표시 하려면 (복제 블록 장치 Distributed) DRBD와 통신 링크의 작동이 중지 합니다. 노드 수준 펜싱 하면 노드 모든 리소스를 실행 하지 않습니다. 노드를 다시 설정 하 여 이렇게 및는 Pacemaker 구현의 STONITH (있음 "헤드에 있는 다른 노드가 해결"에 대 한 의미) 라고 합니다. 예를 들어 무정전 전원 공급 장치 또는 관리 서버에 대 한 카드 인터페이스, pacemaker 매우 다양 한 펜싱 장치를 지원 합니다. 자세한 내용은 참조 하십시오. [처음부터 Pacemaker 클러스터](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html) 및 [펜싱 및 Stonith](http://clusterlabs.org/doc/crm_fencing.html) 

노드 수준 구성 방어 사용자 환경에 따라 크게 달라 집니다, 때문에 중이지만 (구성할 수 있습니다는 나중에)이이 자습서에 대 한 비활성화 됩니다. 주 노드에서 다음 스크립트를 실행 합니다. 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>테스트 목적으로 하는 데 않습니다 STONITH를 사용 하지 않도록 설정 합니다. Pacemaker 프로덕션 환경에서 사용 하려는 경우 환경에 따라 STONITH 구현을 계획 하 고 사용 하도록 설정 유지 해야 합니다. 이 시점에서 펜스 에이전트가 없는 모든 클라우드 환경 (Azure 포함) 또는 Hyper-v에 대 한 참고 합니다. 검사가 클러스터 공급 업체는 이러한 환경에서 실행 중인 프로덕션 클러스터에 대 한 지원을 제공 하지 않습니다. 제작 하는 이후 릴리스에서 사용할 수 있는 이러한 차이 대 한 솔루션입니다.

## <a name="set-cluster-property-start-failure-is-fatal-to-false"></a>클러스터 속성을 false 시작 실패-은-치명적이 지 설정

`start-failure-is-fatal`노드의 리소스를 시작 하지 해당 노드에서 시작 시도 하면 추가 하는지 여부를 나타냅니다. 로 설정 하면 `false`, 클러스터 리소스의 현재 오류 개수 및 마이그레이션 임계값에 따라 다시 동일한 노드에서 시작을 시도할 것인지 결정 합니다. 따라서 장애 조치 발생 후 Pacemaker로 다시 시작의 가용성 그룹 리소스가 이전에 기본 SQL 인스턴스를 사용할 수 있는 합니다. Pacemaker 보조 복제본 내리고 가용성 그룹 자동으로 다시 연결 됩니다. 

속성 값을 업데이트 하려면 `false` 다음 스크립트를 실행 합니다.

```bash
sudo pcs property set start-failure-is-fatal=false
```


>[!WARNING]
>자동 장애 조치 후 때 `start-failure-is-fatal = true` 리소스 관리자 리소스를 시작 하려고 합니다. 수동으로 실행 해야 하는 첫 번째 시도에 실패 하면 `pcs resource cleanup <resourceName>` 정리 리소스 오류 발생 횟수 및 구성 다시 설정 합니다.

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>Pacemaker와 통합에 대 한 SQL Server 리소스 에이전트를 설치 합니다.

모든 노드에서 다음 명령을 실행합니다. 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker에 대 한 SQL Server 로그인 만들기

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>가용성 그룹 리소스 만들기

가용성 그룹 리소스를 만들려면 사용 `pcs resource create` 명령 및 리소스 속성을 설정 합니다. 아래의 명령을 만듭니다는 `ocf:mssql:ag` 형식 리소스 이름의 가용성 그룹에 대 한 마스터/슬레이브 `ag1`합니다. 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>가상 IP 리소스 만들기

가상 IP 주소 리소스를 만들려면 노드 하나에서 다음 명령을 실행 합니다. 네트워크에서 사용 가능한 고정 IP 주소를 사용 합니다. 스크립트를 실행 하기 전에 사이의 값을 대체 `**< ... >**` 유효한 IP 주소입니다.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=**<10.128.16.240>**
```

Pacemaker에서 지정 된 동일한 가상 서버 이름이 없습니다. 문자열 서버 이름이를 가리키는 연결 문자열을 사용 하는 IP 주소를 사용 하지 IP 리소스 주소와 원하는 가상 서버 이름이 DNS에 등록 합니다. DR 구성에 대 한 주 데이터베이스와 DR 사이트 모두에서 DNS 서버와 함께 원하는 가상 서버 이름 및 IP 주소를 등록 합니다.

## <a name="add-colocation-constraint"></a>공동 배치 제약 조건 추가

Pacemaker 클러스터에서 리소스를 실행할 위치를 선택 하는 등 거의 모든 의사 결정은 점수를 비교 하 여 수행 됩니다. 리소스 당 점수가 계산 되 고 클러스터 리소스 관리자가 특정 리소스에 대 한 점수가 가장 높은 있는 노드를 선택 합니다. (한 노드에 리소스에 대 한 음수 점수 있으면 리소스 실행할 수 없습니다 해당 노드에서.) 제약 조건 사용 하 여 클러스터의 결정을 조작할 수 있습니다. 제한에는 점수는. 제약 조건에 무한대 보다 낮은 점수를 경우만 권장 사항입니다. 무한대의 점수는 필수 사항 의미 합니다. 원하는 실행 되도록 하기 위해 주 가용성 그룹 및 가상 ip 리소스는 동일한 호스트에 있으므로 무한대의 점수는 공동 배치 제약 조건을 정의 합니다. 공동 배치 제약 조건에 추가 하려면 노드 하나에서 다음 명령을 실행 합니다. 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>순서 지정 제약 조건 추가

공동 배치 제약 조건을는 암시적 순서 지정 제약 합니다. 가용성 그룹 리소스를 이동 하기 전에 가상 IP 리소스를 이동 합니다. 기본적으로 이벤트의 순서는 같습니다.

1. 사용자 문제 `pcs resource move` 가용성 그룹에 주 노드 1에서 노드 2로 합니다.
1. 노드 1에 가상 IP 리소스를 중지합니다.
1. 가상 IP 리소스 노드 2에서 시작합니다.

   >[!NOTE]
   >이 시점에서 IP 주소 일시적으로 node2 가리키는 node2는 여전히 이전 장애 조치 하는 동안 보조 합니다. 
   
1. 노드 1에서 기본 가용성 그룹 보조로 강등 됩니다.
1. 노드 2에서 보조 가용성 그룹 주 승격 됩니다. 

IP 주소를 장애 조치 이전 보조 서버와 노드를 가리키는 일시적으로 방지 하려면 정렬 제약 조건을 추가 합니다. 

정렬 제약을 추가 하려면 노드 하나에서 다음 명령을 실행 합니다.

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>클러스터를 구성 하 고를 클러스터 리소스로 가용성 그룹을 추가한 후 TRANSACT-SQL 장애 조치할 가용성 그룹 리소스를 사용할 수 없습니다. Linux에서 SQL Server 클러스터 리소스 Windows Server 장애 조치 클러스터 (WSFC)에 운영 체제와 엄격히 결합 되지 됩니다. SQL Server 서비스가 클러스터의 사용 여부 인식 하지 않습니다. 모든 오케스트레이션 클러스터 관리 도구를 통해 수행 됩니다. RHEL 또는 Ubuntu에서 사용 하 여 `pcs`합니다. 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>다음 단계

[HA 가용성 그룹 동작](sql-server-linux-availability-group-failover-ha.md)

