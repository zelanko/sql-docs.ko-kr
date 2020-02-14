---
title: 'RHEL: SQL Server on Linux의 가용성 그룹 구성'
description: SQL Server용 RHEL(Red Hat Enterprise Linux)을 실행할 때 가용성 그룹을 구성하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 01/23/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.openlocfilehash: be817f1fffd734dcf86f3b35d3215decbc9eb28d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76706293"
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>SQL Server 가용성 그룹에 대해 RHEL 클러스터 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Red Hat Enterprise Linux에서 SQL Server에 대한 3노드 가용성 그룹 클러스터를 만드는 방법에 대해 설명합니다. 고가용성을 위해 Linux의 가용성 그룹에는 세 개의 노드가 필요합니다. [가용성 그룹 구성의 고가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)를 참조하세요. 클러스터링 계층은 [Pacemaker](https://clusterlabs.org/) 위에 빌드된 RHEL(Red Hat Enterprise Linux) [HA 추가 기능](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)을 기반으로 합니다. 

> [!NOTE] 
> Red Hat 전체 설명서에 액세스하려면 유효한 구독이 필요합니다. 

클러스터 구성, 리소스 에이전트 옵션 및 관리에 대한 자세한 내용은 [RHEL 참조 설명서](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)를 참조하세요.

> [!NOTE] 
> SQL Server는 Windows Server 장애 조치(failover) 클러스터링과 통합되는 것처럼 Linux의 Pacemaker와 긴밀하게 통합되지 않습니다. SQL Server 인스턴스는 클러스터를 인식하지 않습니다. Pacemaker는 클러스터 리소스 오케스트레이션을 제공합니다. 또한 가상 네트워크 이름은 Windows Server 장애 조치(failover) 클러스터링에만 해당합니다. Pacemaker에는 해당 이름이 없습니다. 클러스터 정보를 쿼리하는 가용성 그룹 DMV(동적 관리 뷰)는 Pacemaker 클러스터에서 빈 행을 반환합니다. 장애 조치(failover) 후에 투명한 다시 연결을 위한 수신기를 만들려면 가상 IP 리소스를 만드는 데 사용되는 IP를 사용하여 DNS에 수신기 이름을 수동으로 등록합니다. 

다음 섹션에서는 Pacemaker 클러스터를 설정하고 고가용성을 위해 클러스터에서 가용성 그룹을 리소스로 추가하는 단계를 안내합니다.

## <a name="roadmap"></a>로드맵

고가용성을 위해 Linux 서버에서 가용성 그룹을 만드는 단계는 Windows Server 장애 조치(failover) 클러스터의 단계와 다릅니다. 다음 목록에서는 개괄적인 단계를 설명합니다. 

1. [클러스터 노드에서 SQL Server를 구성합니다](sql-server-linux-setup.md).

2. [가용성 그룹을 만듭니다](sql-server-linux-availability-group-configure-ha.md). 

3. Pacemaker와 같은 클러스터 리소스 관리자를 구성합니다. 이러한 지침은 이 문서에 포함되어 있습니다.
   
   클러스터 리소스 관리자를 구성하는 방법은 특정 Linux 배포에 따라 다릅니다. 

   >[!IMPORTANT]
   >프로덕션 환경에는 고가용성을 위한 STONITH와 같은 펜싱 에이전트가 필요합니다. 이 설명서의 데모에서는 펜싱 에이전트를 사용하지 않습니다. 데모는 테스트 및 유효성 검사를 위해서만 제공됩니다.
   
   >Linux 클러스터는 펜싱을 사용하여 클러스터를 알려진 상태로 되돌립니다. 펜싱을 구성하는 방법은 배포 및 환경에 따라 달라집니다. 현재, 일부 클라우드 환경에서는 펜싱을 사용할 수 없습니다. 자세한 내용은 [RHEL 고가용성 클러스터의 지원 정책 - 가상화 플랫폼](https://access.redhat.com/articles/29440)을 참조하세요.

4. [가용성 그룹을 클러스터의 리소스로 추가합니다](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource).  

## <a name="configure-high-availability-for-rhel"></a>RHEL에 대해 고가용성 구성

RHEL에 대해 고가용성을 구성하려면 고가용성 구독을 사용하도록 설정한 다음, Pacemaker를 구성합니다.

### <a name="enable-the-high-availability-subscription-for-rhel"></a>RHEL에 대해 고가용성 구독 사용

클러스터의 각 노드에는 RHEL 및 고가용성 추가 기능에 대한 적절한 구독이 있어야 합니다. [Red Hat Enterprise Linux에서 고가용성 클러스터 패키지를 설치하는 방법](https://access.redhat.com/solutions/45930)에서 요구 사항을 검토하세요. 다음 단계에 따라 구독 및 리포지토리를 구성합니다.

1. 시스템을 등록합니다.

   ```bash
   sudo subscription-manager register
   ```

   사용자 이름 및 암호를 제공합니다.   

1. 등록에 사용할 수 있는 풀을 나열합니다.

   ```bash
   sudo subscription-manager list --available
   ```

   사용 가능한 풀 목록에서 고가용성 구독의 풀 ID를 확인합니다.

1. 다음 스크립트를 업데이트합니다. `<pool id>`를 이전 단계의 고가용성을 위한 풀 ID로 바꿉니다. 스크립트를 실행하여 구독을 연결합니다.

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. 리포지토리를 사용하도록 설정합니다.

   **RHEL 7**

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

   **RHEL 8**

   ```bash
   sudo subscription-manager repos --enable=rhel-8-for-x86_64-highavailability-rpms
   ```

자세한 내용은 [Pacemaker - The Open Source, High Availability Cluster](https://clusterlabs.org/pacemaker/)(Pacemaker - 오픈 소스 고가용성 클러스터)를 참조하세요. 

구독을 구성한 후에는 다음 단계를 완료하여 Pacemaker를 구성합니다.

### <a name="configure-pacemaker"></a>Pacemaker 구성

구독을 등록한 후에는 다음 단계를 완료하여 Pacemaker를 구성합니다.
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

Pacemaker가 구성된 후 `pcs`를 사용하여 클러스터와 상호 작용합니다. 클러스터의 한 노드에서 모든 명령을 실행합니다. 

## <a name="configure-fencing-stonith"></a>펜싱(STONITH) 구성

Pacemaker 클러스터 공급업체는 STONITH를 사용하도록 설정하고 지원되는 클러스터 설정에 대해 펜싱 디바이스를 구성하도록 요구합니다. STONITH는 “shoot the other node in the head”(헤드에 있는 다른 노드 맞추기)의 약어입니다. Cluster Resource Manager가 노드의 상태 또는 노드에 있는 리소스의 상태를 확인할 수 없는 경우에는 펜싱이 클러스터를 알려진 상태로 다시 전환합니다.

STONITH 디바이스는 펜싱 에이전트를 제공합니다. [Azure의 Red Hat Enterprise Linux에서 Pacemaker 설정](/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-pacemaker/#1-create-the-stonith-devices)에서는 Azure의 이 클러스터에 대해 STONITH 디바이스를 만드는 방법을 보여 줍니다. 작업 환경에 맞게 지침을 수정하세요.

리소스 수준 펜싱은 리소스를 구성하여 중단 시 데이터 손상이 발생하지 않도록 합니다. 예를 들어 리소스 수준 펜싱을 사용하여 통신 링크가 가동 중단될 때 노드의 디스크를 오래된 것으로 표시할 수 있습니다. 

노드 수준 펜싱은 노드가 리소스를 실행하지 않도록 합니다. 이 작업은 노드를 다시 설정하여 수행됩니다. Pacemaker는 다양한 펜싱 디바이스를 지원합니다. 예를 들어 서버에 대한 무정전 전원 공급 디바이스 또는 관리 인터페이스 카드가 있습니다.

STONITH 및 펜싱에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Pacemaker Clusters from Scratch](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/index.html)(처음부터 Pacemaker 클러스터)
* [Fencing and STONITH](https://clusterlabs.org/doc/crm_fencing.html)(펜싱 및 STONITH)
* [Red Hat High Availability Add-On with Pacemaker: Fencing](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)(Pacemaker를 사용하는 Red Hat 고가용성 추가 기능: 펜싱)

>[!NOTE]
>노드 수준 펜싱 구성은 사용자 환경에 따라 크게 좌우되므로 이 자습서에서는 사용하지 않도록 설정합니다(나중에 구성할 수 있음). 다음 스크립트는 노드 수준 펜싱을 사용하지 않도록 설정합니다.
>
>```bash
>sudo pcs property set stonith-enabled=false
>``` 
>
>STONITH를 사용하지 않도록 설정하는 기능은 테스트 목적으로만 제공됩니다. 프로덕션 환경에서 Pacemaker를 사용하려는 경우 해당 환경에 따라 STONITH 구현을 계획하고 사용 상태로 유지해야 합니다.

## <a name="set-cluster-property-cluster-recheck-interval"></a>클러스터 속성 cluster-recheck-interval 설정

`cluster-recheck-interval`은 클러스터에서 리소스 매개 변수, 제약 조건 또는 기타 클러스터 옵션의 변경 내용을 확인하는 폴링 간격을 나타냅니다. 복제본의 작동이 중단되면 클러스터는 `failure-timeout` 값과 `cluster-recheck-interval` 값을 통해 바인딩된 간격으로 복제본을 다시 시작하려고 합니다. 예를 들어 `failure-timeout`을 60초로 설정하고 `cluster-recheck-interval`을 120초로 설정한 경우 60초보다 크고 120초보다 작은 간격으로 다시 시작이 시도됩니다. failure-timeout을 60초로 설정하고 cluster-recheck-interval을 60초보다 큰 값으로 설정하는 것이 좋습니다. cluster-recheck-interval을 작은 값으로 설정하는 것을 권장하지 않습니다.

속성 값을 `2 minutes`로 업데이트하려면 다음 명령을 실행합니다.

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 사용 가능한 최신 Pacemaker 패키지 1.1.18-11.el7을 사용하는 모든 배포(RHEL 7.3 및 7.4 포함)에서는 해당 값이 false일 때 start-failure-is-fatal 클러스터 설정의 동작이 변경됩니다. 이 변경 내용은 장애 조치(failover) 워크플로에 영향을 줍니다. 주 복제본이 중단될 경우 클러스터가 사용 가능한 보조 복제본 중 하나로 장애 조치(failover)되어야 합니다. 예상과 달리, 사용자는 클러스터가 실패한 주 복제본을 시작하려고 계속 시도하는 것을 보게 됩니다. 주 복제본이 영구 중단되어 온라인 상태로 전환되지 않는 경우 클러스터도 사용 가능한 다른 보조 복제본으로 장애 조치(failover)되지 않습니다. 이 변경 내용 때문에 start-failure-is-fatal을 설정하는 이전 권장 구성은 더 이상 유효하지 않으며, 설정을 기본값인 `true`로 되돌려야 합니다. 또한 `failover-timeout` 속성이 포함되도록 AG 리소스를 업데이트해야 합니다. 

속성 값을 `true`로 업데이트하려면 다음 명령을 실행합니다.

```bash
sudo pcs property set start-failure-is-fatal=true
```

`ag_cluster` 리소스 속성 `failure-timeout`을 `60s`로 업데이트하려면 다음을 실행합니다.

```bash
pcs resource update ag_cluster meta failure-timeout=60s
```


Pacemaker 클러스터 속성에 대한 자세한 내용은 [Pacemaker Clusters Properties](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html)(Pacemaker 클러스터 속성)를 참조하세요.

## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker용 SQL Server 로그인 만들기

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>가용성 그룹 리소스 만들기

가용성 그룹 리소스를 만들려면 `pcs resource create` 명령을 사용하고 리소스 속성을 설정합니다. 다음 명령은 이름이 `ag1`인 가용성 그룹에 대해 `ocf:mssql:ag` 마스터/슬레이브 유형 리소스를 만듭니다.

**RHEL 7**

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=60s master notify=true
```

**RHEL 8**

**RHEL 8**의 가용성과 함께, 생성 구문이 변경되었습니다. **RHEL 8**을 사용하는 경우 용어 `master`가 `promotable`로 변경되었습니다. 위의 명령 대신 다음의 생성 명령을 사용합니다. 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=60s promotable notify=true
```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>가상 IP 리소스 만들기

가상 IP 주소 리소스를 만들려면 한 노드에서 다음 명령을 실행합니다. 네트워크의 사용 가능한 고정 IP 주소를 사용합니다. `<10.128.16.240>` 사이 IP 주소를 유효한 IP 주소로 바꿉니다.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Pacemaker에는 해당하는 가상 서버 이름이 없습니다. IP 주소 대신 문자열 서버 이름을 가리키는 연결 문자열을 사용하려면 DNS에 가상 IP 리소스 주소와 원하는 가상 서버 이름을 등록합니다. DR 구성의 경우 기본 및 DR 사이트의 DNS 서버에 원하는 가상 서버 이름 및 IP 주소를 등록합니다.

## <a name="add-colocation-constraint"></a>공동 배치 제약 조건 추가

리소스를 실행할 위치 선택과 같은, Pacemaker 클러스터의 거의 모든 결정은 점수 비교를 통해 수행됩니다. 점수는 리소스별로 계산됩니다. Cluster Resource Manager는 특정 리소스에 대해 점수가 가장 높은 노드를 선택합니다. 노드의 리소스 점수가 음수이면 해당 노드에서 리소스를 실행할 수 없습니다.

Pacemaker 클러스터에서 제약 조건을 사용하여 클러스터의 결정을 조작할 수 있습니다. 제약 조건에는 점수가 있습니다. 제약 조건의 점수가 `INFINITY`보다 낮으면 Pacemaker는 이 제약 조건을 권장 사항으로 간주합니다. `INFINITY` 점수는 필수입니다.

주 복제본과 가상 IP 리소스가 동일한 호스트에서 실행되는지 확인하려면 점수가 INFINITY인 공동 배치 제약 조건을 정의합니다. 공동 배치 제약 조건을 추가하려면 한 노드에서 다음 명령을 실행합니다.

### <a name="rhel-7"></a>RHEL 7

RHEL 7에서 `ag_cluster` 리소스를 만들 때 리소스를 `ag_cluster-master`로 만듭니다. RHEL 7의 다음 명령을 사용합니다.

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

### <a name="rhel-8"></a>RHEL 8

RHEL 8에서 `ag_cluster` 리소스를 만들 때 리소스를 `ag_cluster-clone`로 만듭니다. RHEL 8의 다음 명령 형식을 사용합니다.

```bash
sudo pcs constraint colocation add virtualip with master ag_cluster-clone INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>정렬 제약 조건 추가

공동 배치 제약 조건에는 암시적 정렬 제약 조건이 있습니다. 이 제약 조건은 가용성 그룹 리소스를 이동하기 전에 가상 IP 리소스를 이동합니다. 기본적으로 이벤트 시퀀스는 다음과 같습니다.

1. 사용자가 node1에서 node2까지 가용성 그룹 주 복제본에 대해 `pcs resource move`를 실행합니다.
1. 노드 1에서 가상 IP 리소스가 중지됩니다.
1. 노드 2에서 가상 IP 리소스가 시작됩니다.
  
   >[!NOTE]
   >이때 노드 2는 여전히 장애 조치(failover) 전 보조 복제본이지만, IP 주소가 일시적으로 노드 2를 가리킵니다. 
   
1. 노드 1의 가용성 그룹 주 복제본이 보조 복제본으로 수준이 내려갑니다.
1. 노드 2의 가용성 그룹 보조 복제본이 주 복제본으로 수준이 올라갑니다. 

IP 주소가 일시적으로 장애 조치(failover) 이전 보조 복제본이 있는 노드를 가리키지 않도록 하려면 정렬 제약 조건을 추가합니다. 

정렬 제약 조건을 추가하려면 한 노드에서 다음 명령을 실행합니다.

### <a name="rhel-7"></a>RHEL 7

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

### <a name="rhel-8"></a>RHEL 8

```bash
sudo pcs constraint order promote ag_cluster-clone then start virtualip
```

>[!IMPORTANT]
>클러스터를 구성하고 가용성 그룹을 클러스터 리소스로 추가한 후에는 Transact-SQL을 사용하여 가용성 그룹 리소스를 장애 조치(failover)할 수 없습니다. Linux의 SQL Server 클러스터 리소스는 WSFC(Windows Server 장애 조치(failover) 클러스터)에 있을 때처럼 운영 체제와 긴밀하게 결합되지 않습니다. SQL Server 서비스는 클러스터의 현재 상태를 인식하지 못합니다. 모든 오케스트레이션이 클러스터 관리 도구를 통해 수행됩니다. RHEL 또는 Ubuntu에서는 `pcs`를 사용하고 SLES에서는 `crm` 도구를 사용합니다. 

`pcs`를 사용하여 가용성 그룹을 수동으로 장애 조치(failover)합니다. Transact-SQL을 사용하여 장애 조치(failover)를 시작하지 않도록 합니다. 자세한 내용은 [장애 조치(failover)](sql-server-linux-availability-group-failover-ha.md#failover)를 참조하세요.

## <a name="next-steps"></a>다음 단계

[HA 가용성 그룹 작동](sql-server-linux-availability-group-failover-ha.md)
