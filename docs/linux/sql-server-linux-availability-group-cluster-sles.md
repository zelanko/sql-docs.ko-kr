---
title: 'SUSE: SQL Server on Linux의 가용성 그룹 구성'
titleSuffix: SQL Server
description: SLES(SUSE Linux Enterprise Server)에서 SQL Server의 가용성 그룹 클러스터를 만드는 방법을 알아봅니다.
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.openlocfilehash: efa93b1d85e0aec5be7ea62ce76cb0270c68178f
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784875"
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>SQL Server 가용성 그룹에 대해 SLES 클러스터 구성

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 가이드에서는 SLES(SUSE Linux Enterprise Server) 12 SP2에서 SQL Server의 3노드 클러스터를 만드는 방법을 설명합니다. 고가용성을 위해 Linux의 가용성 그룹에는 세 개의 노드가 필요합니다. [가용성 그룹 구성의 고가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)를 참조하세요. 클러스터링 계층은 [Pacemaker](https://clusterlabs.org/)를 토대로 빌드된 SUSE [HAE(고가용성 확장)](https://www.suse.com/products/highavailability)를 기반으로 합니다. 

클러스터 구성, 리소스 에이전트 옵션, 관리, 모범 사례 및 권장 사항에 대한 자세한 내용은 [SUSE Linux Enterprise High Availability Extension 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)를 참조하세요.

>[!NOTE]
>이때 Linux의 Pacemaker와 SQL Server의 통합은 Windows의 WSFC와 같이 결합되지 않습니다. Linux의 SQL Server 서비스는 클러스터를 인식하지 못합니다. Pacemaker가 가용성 그룹 리소스를 포함하여 클러스터 리소스의 모든 오케스트레이션을 제어합니다. Linux에서는 sys.dm_hadr_cluster와 같은 클러스터 정보를 제공하는 Always On 가용성 그룹 DMV(동적 관리 뷰)를 사용하지 않아야 합니다. 또한 가상 네트워크 이름은 WSFC에만 해당되며, Pacemaker에는 동일한 항목이 없습니다. 수신기를 만들어 장애 조치(failover) 후의 투명한 재연결에 사용할 수는 있지만, 다음 섹션에서 설명하는 것처럼 가상 IP 리소스를 만드는 데 사용되는 IP와 함께 수신기 이름을 DNS 서버에 수동으로 등록해야 합니다.

[!INCLUDE [bias-sensitive-term-t](../includes/bias-sensitive-term-t.md)]

## <a name="roadmap"></a>로드맵

고가용성을 위한 가용성 그룹을 만드는 절차는 Linux 서버와 Windows Server 장애 조치(failover) 클러스터 간에 차이가 있습니다. 다음 목록에서는 개괄적인 단계를 설명합니다. 

1. [클러스터 노드에서 SQL Server를 구성합니다](sql-server-linux-setup.md).

2. [가용성 그룹을 만듭니다](sql-server-linux-availability-group-failover-ha.md). 

3. Pacemaker와 같은 클러스터 리소스 관리자를 구성합니다. 이러한 지침은 이 문서에 포함되어 있습니다.
   
   클러스터 리소스 관리자를 구성하는 방법은 특정 Linux 배포에 따라 다릅니다. 

   >[!IMPORTANT]
   >프로덕션 환경에는 고가용성을 위한 STONITH와 같은 펜싱 에이전트가 필요합니다. 이 문서의 예제에서는 펜싱 에이전트를 사용하지 않습니다. 예제는 테스트 및 유효성 검사를 위해서만 제공됩니다. 
   
   >Pacemaker 클러스터는 펜싱을 사용하여 클러스터를 알려진 상태로 되돌립니다. 펜싱을 구성하는 방법은 배포 및 환경에 따라 달라집니다. 현재, 일부 클라우드 환경에서는 펜싱을 사용할 수 없습니다. [SUSE Linux Enterprise 고가용성 확장](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)을 참조하세요.

5. [가용성 그룹을 클러스터의 리소스로 추가합니다](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server). 

## <a name="prerequisites"></a>필수 구성 요소

다음 엔드투엔드 시나리오를 완료하려면 3노드 클러스터를 배포할 머신 3대가 필요합니다. 다음 단계에서는 이러한 서버를 구성하는 방법을 간략하게 설명합니다.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>각 클러스터 노드에서 운영 체제 설정 및 구성 

첫 번째 단계는 클러스터 노드에서 운영 체제를 구성하는 것입니다. 이 연습에서는 HA 추가 기능을 위한 유효한 구독이 있는 SLES 12 SP2를 사용합니다.

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>각 클러스터 노드에서 SQL Server 서비스 설치 및 구성

1. 모든 노드에서 SQL Server 서비스를 설치하고 설정합니다. 자세한 내용은 [SQL Server on Linux 설치](sql-server-linux-setup.md)를 참조하세요.

1. 한 노드를 주 노드로, 다른 노드를 보조 노드로 지정합니다. 이 용어는 가이드 전체에서 사용됩니다.

1. 클러스터에 포함하려는 노드가 서로 통신할 수 있는지 확인합니다.

   다음 예제에서는 SLES1, SLES2, SLES3이라는 세 노드의 정보가 추가된 `/etc/hosts`를 보여 줍니다.

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   모든 클러스터 노드는 SSH를 통해 서로 액세스할 수 있어야 합니다. `hb_report` 또는 `crm_report`(문제 해결용), Hawk의 History Explorer와 같은 도구에는 노드 간에 암호 없는 SSH 액세스가 필요합니다. 액세스 권한이 없으면 현재 노드에서만 데이터를 수집할 수 있습니다. 표준이 아닌 SSH 포트를 사용하는 경우 -X 옵션을 사용합니다(`man` 페이지 참조). 예를 들어 SSH 포트가 3479이면 다음을 사용하여 `crm_report`를 호출합니다.

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   자세한 내용은 [SLES Administration Guide - Miscellaneous](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)(SLES 관리 가이드 - 기타) 섹션을 참조하세요.


## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker용 SQL Server 로그인 만들기

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>Always On 가용성 그룹 구성

Linux 서버에서 가용성 그룹을 구성한 다음, 클러스터 리소스를 구성합니다. 가용성 그룹을 구성하려면 [SQL Server on Linux에 대해 Always On 가용성 그룹 구성](sql-server-linux-availability-group-configure-ha.md)을 참조하세요.

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>각 클러스터 노드에 Pacemaker 설치 및 구성

1. 고가용성 확장을 설치합니다.

   참조는 [SUSE Linux Enterprise Server 및 고가용성 확장 설치](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)를 참조하세요.

1. 두 노드에서 모두 SQL Server 리소스 에이전트 패키지를 설치합니다.

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>첫 번째 노드 설정

   [SLES 설치 지침](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)을 참조하세요.

1. 클러스터 노드로 사용할 물리적 머신 또는 가상 머신에 `root`로 로그인합니다.
2. 다음 명령을 실행하여 부트스트랩 스크립트를 시작합니다.
   ```bash
   sudo ha-cluster-init
   ```

   NTP가 부팅 시 시작되도록 구성되지 않은 경우 메시지가 표시됩니다. 

   계속하기로 결정하면 스크립트에서 자동으로 SSH 액세스 및 Csync2 동기화 도구용 키를 생성하고 둘 다에 필요한 서비스를 시작합니다. 

3. 클러스터 통신 계층(Corosync)을 구성합니다. 

   a. 바인딩할 네트워크 주소를 입력합니다. 기본적으로 스크립트는 네트워크 주소 eth0을 제안합니다. 또는 다른 네트워크 주소(예: 주소 bond0)를 입력합니다. 

   b. 멀티캐스트 주소를 입력합니다. 스크립트에서 사용할 수 있는 임의 주소를 기본값으로 제안합니다. 

   다. 멀티캐스트 포트를 입력합니다. 스크립트는 5405를 기본값으로 제안합니다. 

   d. `SBD ()`를 구성하려면 SBD에 사용하려는 블록 디바이스 파티션의 영구 경로를 입력합니다. 이 경로는 클러스터의 모든 노드에서 일치해야 합니다. 
   마지막으로, 스크립트는 Pacemaker 서비스를 시작하여 1노드 클러스터를 온라인 상태로 전환하고 웹 관리 인터페이스 Hawk2를 사용하도록 설정합니다. Hawk2에 사용할 URL이 화면에 표시됩니다. 

4. 설정 프로세스에 대한 자세한 내용은 `/var/log/sleha-bootstrap.log`를 참조하세요. 이제 1노드 클러스터가 실행되고 있습니다. crm status를 사용하여 클러스터 상태를 확인합니다.

   ```bash
   sudo crm status
   ```

   `crm configure show xml` 또는 `crm configure show`를 사용하여 클러스터 구성을 확인할 수도 있습니다.

5. 부트스트랩 절차에서는 암호가 linux인 hacluster라는 Linux 사용자를 만듭니다. 가능한 한 빨리 기본 암호를 안전한 암호로 바꿉니다. 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>기존 클러스터에 노드 추가

하나 이상의 노드가 포함된 클러스터를 실행 중인 경우 ha-cluster-join 부트스트랩 스크립트를 사용하여 클러스터 노드를 더 추가합니다. 스크립트에 기존 클러스터 노드에 대한 액세스 권한만 있으면 현재 머신에서 기본 설정을 자동으로 완료합니다. 다음 단계를 사용합니다.

`YaST` 클러스터 모듈을 사용하여 기존 클러스터 노드를 구성한 경우 `ha-cluster-join`을 실행하기 전에 다음 필수 조건이 충족되었는지 확인합니다.
- 기존 노드의 루트 사용자에게 암호 없는 로그인을 위한 SSH 키가 있습니다. 
- 기존 노드에서 `Csync2`가 구성되었습니다. 자세한 내용은 YaST를 사용하여 Csync2 구성을 참조하세요. 

1. 클러스터에 참가해야 하는 물리적 머신 또는 가상 머신에 루트로 로그인합니다. 
2. 다음 명령을 실행하여 부트스트랩 스크립트를 시작합니다. 

   ```bash
   sudo ha-cluster-join
   ```

   NTP가 부팅 시 시작되도록 구성되지 않은 경우 메시지가 표시됩니다. 

3. 계속하기로 결정하면 기존 노드의 IP 주소를 입력하라는 메시지가 표시됩니다. IP 주소를 입력합니다. 

4. 두 머신 간에 암호 없는 SSH 액세스를 아직 구성하지 않은 경우 기존 노드의 루트 암호를 입력하라는 메시지가 표시됩니다. 

   지정된 노드에 로그인하면 스크립트에서 Corosync 구성을 복사하고 SSH 및 `Csync2`를 구성한 다음, 현재 머신을 온라인 상태로 전환하고 새 클러스터 노드로 표시합니다. 그 외에도 Hawk에 필요한 서비스를 시작합니다. `OCFS2`를 사용하여 공유 스토리지를 구성한 경우 `OCFS2` 파일 시스템의 탑재 지점 디렉터리도 자동으로 생성됩니다. 

5. 클러스터에 추가하려는 모든 머신에 대해 이전 단계를 반복합니다. 

6. 프로세스에 대한 자세한 내용은 `/var/log/ha-cluster-bootstrap.log`를 참조하세요. 

1. `sudo crm status`를 사용하여 클러스터 상태를 확인합니다. 두 번째 노드를 성공적으로 추가한 경우 출력이 다음과 같이 표시됩니다.

   ```bash
   sudo crm status
   
   3 nodes configured
   1 resource configured
   Online: [ SLES1 SLES2 SLES3]
   Full list of resources:   
   admin_addr     (ocf::heartbeat:IPaddr2):       Started node1
   ```

   >[!NOTE]
   >`admin_addr`은 최초 1노드 클러스터 설정 중에 구성된 가상 IP 클러스터 리소스입니다.

모든 노드를 추가한 후에 전역 클러스터 옵션에서 no-quorum-policy를 조정해야 하는지 확인합니다. 이 작업은 2노드 클러스터에서 특히 중요합니다. 자세한 내용은 섹션 4.1.2, no-quorum-policy 옵션을 참조하세요. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>클러스터 속성 cluster-recheck-interval 설정

`cluster-recheck-interval`은 클러스터에서 리소스 매개 변수, 제약 조건 또는 기타 클러스터 옵션의 변경 내용을 확인하는 폴링 간격을 나타냅니다. 복제본의 작동이 중단되면 클러스터는 `failure-timeout` 값과 `cluster-recheck-interval` 값을 통해 바인딩된 간격으로 복제본을 다시 시작하려고 합니다. 예를 들어 `failure-timeout`을 60초로 설정하고 `cluster-recheck-interval`을 120초로 설정한 경우 60초보다 크고 120초보다 작은 간격으로 다시 시작이 시도됩니다. failure-timeout을 60초로 설정하고 cluster-recheck-interval을 60초보다 큰 값으로 설정하는 것이 좋습니다. cluster-recheck-interval을 작은 값으로 설정하는 것을 권장하지 않습니다.

속성 값을 `2 minutes`로 업데이트하려면 다음 명령을 실행합니다.

```bash
crm configure property cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Pacemaker 클러스터에서 관리하는 가용성 그룹 리소스가 이미 있는 경우 사용 가능한 최신 Pacemaker 패키지 1.1.18-11.el7을 사용하는 모든 배포에서 값이 false인 경우의 start-failure-is-fatal 클러스터 설정 동작이 변경된 것을 확인합니다. 이 변경 내용은 장애 조치(failover) 워크플로에 영향을 줍니다. 주 복제본이 중단될 경우 클러스터가 사용 가능한 보조 복제본 중 하나로 장애 조치(failover)되어야 합니다. 예상과 달리, 사용자는 클러스터가 실패한 주 복제본을 시작하려고 계속 시도하는 것을 보게 됩니다. 주 복제본이 영구 중단되어 온라인 상태로 전환되지 않는 경우 클러스터도 사용 가능한 다른 보조 복제본으로 장애 조치(failover)되지 않습니다. 이 변경 내용 때문에 start-failure-is-fatal을 설정하는 이전 권장 구성은 더 이상 유효하지 않으며, 설정을 기본값인 `true`로 되돌려야 합니다. 또한 `failover-timeout` 속성이 포함되도록 AG 리소스를 업데이트해야 합니다. 
>
>속성 값을 `true`로 업데이트하려면 다음 명령을 실행합니다.
>
>```bash
>crm configure property start-failure-is-fatal=true
>```
>
>기존 AG 리소스 속성 `failure-timeout`을 `60s`로 업데이트하려면 다음 명령을 실행합니다(`ag1`을 해당 가용성 그룹 리소스의 이름으로 바꿈). 
>
>```bash
>crm configure edit ag1
># In the text editor, add `meta failure-timeout=60s` after any `param`s and before any `op`s
>```

Pacemaker 클러스터 속성에 대한 자세한 내용은 [클러스터 리소스 구성](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html)을 참조하세요.

## <a name="configure-fencing-stonith"></a>펜싱(STONITH) 구성
Pacemaker 클러스터 공급업체는 STONITH를 사용하도록 설정하고 지원되는 클러스터 설정에 대해 펜싱 디바이스를 구성하도록 요구합니다. Cluster Resource Manager가 노드 상태 또는 노드의 리소스 상태를 확인할 수 없는 경우 펜싱을 사용하여 클러스터를 알려진 상태로 다시 전환합니다.

리소스 수준 펜싱은 주로 리소스를 구성하여 중단 시 데이터 손상이 발생하지 않도록 합니다. 예를 들어 DRBD(Distributed Replicated Block Device)에서 리소스 수준 펜싱을 사용하여 통신 링크의 작동이 중단될 경우 노드의 디스크를 오래된 것으로 표시할 수 있습니다.

노드 수준 펜싱은 노드가 리소스를 실행하지 않도록 합니다. 노드를 다시 설정하여 이 작업을 수행하며, 해당 Pacemaker 구현을 STONITH(“shoot the other node in the head”의 약어)라고 합니다. Pacemaker는 서버에 대해 무정전 전원 공급 디바이스 또는 관리 인터페이스 카드와 같은 다양한 펜싱 디바이스를 지원합니다.

자세한 내용은 다음을 참조하세요.

- [Pacemaker Clusters from Scratch](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/)(처음부터 Pacemaker 클러스터)
- [펜싱 및 STONITH](https://clusterlabs.org/doc/crm_fencing.html)
- [SUSE HA 설명서: 펜싱 및 STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html)

클러스터 초기화 시 구성이 검색되지 않으면 STONITH가 사용하지 않도록 설정됩니다. 나중에 다음 명령을 실행하여 사용하도록 설정할 수 있습니다.

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>STONITH를 사용하지 않도록 설정하는 기능은 테스트 목적으로만 제공됩니다. 프로덕션 환경에서 Pacemaker를 사용하려는 경우 해당 환경에 따라 STONITH 구현을 계획하고 사용 상태로 유지해야 합니다. SUSE는 클라우드 환경(Azure 포함) 또는 Hyper-V용 펜싱 에이전트를 제공하지 않습니다. 따라서 클러스터 공급업체도 이러한 환경에서 프로덕션 클러스터를 실행하기 위한 지원을 제공하지 않습니다. 이 문제의 해결 방법을 개발 중이며, 이후 릴리스에서 제공될 예정입니다.

## <a name="configure-the-cluster-resources-for-sql-server"></a>SQL Server의 클러스터 리소스 구성

[SLES 관리 Guid](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)를 참조하세요.

## <a name="enable-pacemaker"></a>Pacemaker 사용

Pacemaker를 사용하도록 설정하여 자동으로 시작합니다.

클러스터의 모든 노드에서 다음 명령을 실행합니다.

```bash
systemctl enable pacemaker
```

### <a name="create-availability-group-resource"></a>가용성 그룹 리소스 만들기

다음 명령은 가용성 그룹 [ag1] 복제본 3개의 가용성 그룹 리소스를 만들고 구성합니다. 모니터링 작업 및 시간 제한은 SLES에서 명시적으로 지정해야 합니다. 시간 제한은 워크로드에 따라 큰 차이가 있으며 각 배포에 맞게 신중하게 조정해야 합니다.
클러스터의 노드 중 하나에서 명령을 실행합니다.

1. `crm configure`를 실행하여 crm 프롬프트를 엽니다.

   ```bash
   sudo crm configure 
   ```

1. crm 프롬프트에서 다음 명령을 실행하여 리소스 속성을 구성합니다.

   ```bash
   primitive ag_cluster \
      ocf:mssql:ag \
      params ag_name="ag1" \
      meta failure-timeout=60s \
      op start timeout=60s \
      op stop timeout=60s \
      op promote timeout=60s \
      op demote timeout=10s \
      op monitor timeout=60s interval=10s \
      op monitor timeout=60s interval=11s role="Master" \
      op monitor timeout=60s interval=12s role="Slave" \
      op notify timeout=60s
   ms ms-ag_cluster ag_cluster \
      meta master-max="1" master-node-max="1" clone-max="3" \
     clone-node-max="1" notify="true" \
   commit
      ```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

### <a name="create-virtual-ip-resource"></a>가상 IP 리소스 만들기

`ha-cluster-init`를 실행할 때 가상 IP 리소스를 만들지 않은 경우 지금 이 리소스를 만들 수 있습니다. 다음 명령은 가상 IP 리소스를 만듭니다. `<**0.0.0.0**>`을 네트워크에서 사용 가능한 주소로 바꾸고, `<**24**>`를 CIDR 서브넷 마스크의 비트 수로 바꿉니다. 한 노드에서 다음 명령을 실행합니다.

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>공동 배치 제약 조건 추가
리소스를 실행할 위치 선택과 같은, Pacemaker 클러스터의 거의 모든 결정은 점수 비교를 통해 수행됩니다. 점수는 리소스별로 계산되며, Cluster Resource Manager는 특정 리소스에 대해 점수가 가장 높은 노드를 선택합니다. 노드의 리소스 점수가 음수이면 해당 노드에서 리소스를 실행할 수 없습니다. 제약 조건을 사용하여 클러스터의 결정을 조작할 수 있습니다. 제약 조건에는 점수가 있습니다. 제약 조건의 점수가 INFINITY보다 낮으면 권장 사항일 뿐입니다. 점수가 INFINITY이면 필수 항목입니다. 가용성 그룹의 주 복제본과 가상 IP 리소스가 동일한 호스트에서 실행되도록 하기 위해 점수가 INFINITY인 공동 배치 제약 조건을 정의합니다. 

마스터와 동일한 노드에서 실행되도록 가상 IP에 대해 공동 배치 제약 조건을 설정하려면 한 노드에서 다음 명령을 실행합니다.

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>정렬 제약 조건 추가
공동 배치 제약 조건에는 암시적 정렬 제약 조건이 있습니다. 이 제약 조건은 가용성 그룹 리소스를 이동하기 전에 가상 IP 리소스를 이동합니다. 기본적으로 이벤트 시퀀스는 다음과 같습니다. 

1. 사용자가 노드 1에서 노드 2로의 리소스 마이그레이션을 가용성 그룹 마스터에 실행합니다.
2. 노드 1에서 가상 IP 리소스가 중지됩니다.
3. 노드 2에서 가상 IP 리소스가 시작됩니다. 이때 노드 2는 여전히 장애 조치(failover) 전 보조 복제본이지만, IP 주소가 일시적으로 노드 2를 가리킵니다. 
4. 노드 1의 가용성 그룹 마스터가 수준이 내려갑니다.
5. 노드 2의 가용성 그룹이 마스터로 수준이 올라갑니다. 

IP 주소가 일시적으로 장애 조치(failover) 이전 보조 복제본이 있는 노드를 가리키지 않도록 하려면 정렬 제약 조건을 추가합니다. 정렬 제약 조건을 추가하려면 한 노드에서 다음 명령을 실행합니다. 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>클러스터를 구성하고 가용성 그룹을 클러스터 리소스로 추가한 후에는 Transact-SQL을 사용하여 가용성 그룹 리소스를 장애 조치(failover)할 수 없습니다. Linux의 SQL Server 클러스터 리소스는 WSFC(Windows Server 장애 조치(failover) 클러스터)에 있을 때처럼 운영 체제와 긴밀하게 결합되지 않습니다. SQL Server 서비스는 클러스터의 현재 상태를 인식하지 못합니다. 모든 오케스트레이션이 클러스터 관리 도구를 통해 수행됩니다. SLES에서는 `crm`을 사용합니다. 

`crm`를 사용하여 가용성 그룹을 수동으로 장애 조치(failover)합니다. Transact-SQL을 사용하여 장애 조치(failover)를 시작하지 않도록 합니다. 자세한 내용은 [장애 조치(failover)](sql-server-linux-availability-group-failover-ha.md#failover)를 참조하세요.


자세한 내용은 다음을 참조하세요.
- [Managing cluster resources](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm)(클러스터 리소스 관리)   
- [HA Concepts](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)(HA 개념)
- [Pacemaker 빠른 참조](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>다음 단계

[HA 가용성 그룹 작동](sql-server-linux-availability-group-failover-ha.md)
