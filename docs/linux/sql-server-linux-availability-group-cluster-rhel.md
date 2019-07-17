---
title: SQL Server 가용성 그룹에 대 한 RHEL 클러스터 구성
titleSuffix: SQL Server
description: Red Hat Enterprise Linux (RHEL)를 실행 하는 경우 가용성 그룹 클러스터에 알아봅니다
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/12/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.openlocfilehash: 086138fc1df6245de33b348c529e56e606c3ddc9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027318"
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>SQL Server 가용성 그룹에 대 한 RHEL 클러스터 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Red Hat Enterprise Linux에서 SQL Server에 대 한 3 개 노드의 가용성 그룹 클러스터를 만드는 방법을 설명 합니다. 고가용성을 위해 Linux에서 가용성 그룹을 필요한 3 개의 노드가-참조 [가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)합니다. 클러스터링 계층은 Red Hat Enterprise Linux (RHEL) 기반 [HA 추가 기능](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) 기반으로 구축 [Pacemaker](https://clusterlabs.org/)합니다. 

> [!NOTE] 
> Red Hat 전체 설명서에 대 한 액세스는 유효한 구독이 필요합니다. 

클러스터 구성, 리소스 에이전트 옵션 및 관리에 대 한 자세한 내용은 방문 [RHEL 참조 설명서](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)합니다.

> [!NOTE] 
> SQL Server는 통합 되지 않습니다와 긴밀 하 게 Linux의 Pacemaker를 사용 하 여 Windows Server 장애 조치 클러스터링 된. SQL Server 인스턴스를 클러스터의 인식 아닙니다. Pacemaker는 클러스터 리소스 오케스트레이션을 제공 합니다. 또한 가상 네트워크 이름은 Windows Server 장애 조치 클러스터링에 특정-Pacemaker에 해당 항목이 없습니다. 가용성 그룹 동적 관리 뷰 (Dmv) 클러스터 정보를 쿼리 하는 Pacemaker 클러스터에서 빈 행을 반환 합니다. 장애 조치 후 투명 하 게 다시 연결에 대 한 수신기를 만들려면 가상 IP 리소스를 만드는 데 사용 된 IP 사용 하 여 DNS에서 수신기 이름을 수동으로 등록 합니다. 

다음 섹션에서는 Pacemaker 클러스터를 설정 하 고 고가용성을 위해 클러스터의 리소스와 가용성 그룹을 추가 하는 단계를 안내 합니다.

## <a name="roadmap"></a>로드맵

고가용성을 위해 Linux 서버에서 가용성 그룹을 만드는 단계는 Windows Server 장애 조치 클러스터에 대 한 단계와 다릅니다. 다음과 같은 단계를 간략히 설명 합니다. 

1. [SQL Server 클러스터 노드에서 구성](sql-server-linux-setup.md)합니다.

2. [가용성 그룹을 만들](sql-server-linux-availability-group-configure-ha.md)합니다. 

3. Pacemaker와 같은 클러스터 리소스 관리자를 구성 합니다. 이러한 지침은이 문서에 있습니다.
   
   클러스터 리소스 관리자를 구성 하는 방법은 특정 Linux 배포에 따라 달라 집니다. 

   >[!IMPORTANT]
   >프로덕션 환경에 같은 고가용성에 대 한 STONITH는 펜싱 에이전트가 필요합니다. 이 문서의 데모는 펜싱 에이전트를 사용 하지 마세요. 데모 테스트 및 유효성 검사에만 됩니다. 
   
   >Linux 클러스터는 클러스터를 알려진된 상태로 반환할 펜싱을 사용 합니다. 펜스를 구성 하는 방법은 배포 및 환경에 따라 달라 집니다. 현재 펜스는 일부 클라우드 환경에서 사용할 수 없습니다. 자세한 내용은 [RHEL 높은 가용성 클러스터-가상화 플랫폼에 대 한 지원 정책을](https://access.redhat.com/articles/29440)합니다.

5. [가용성 그룹에 클러스터 리소스로 추가](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)합니다.  

## <a name="configure-high-availability-for-rhel"></a>RHEL에 대 한 고가용성 구성

RHEL에 대 한 고가용성을 구성 하려면 항상 사용 가능한 구독을 사용 하도록 설정 하 고 Pacemaker를 구성 합니다.

### <a name="enable-the-high-availability-subscription-for-rhel"></a>Rhel 고가용성 구독 사용

클러스터의 각 노드 RHEL 및 높은 가용성 추가 대 한 적절 한 구독이 가져야 합니다. 요구 사항을 검토 [Red Hat Enterprise Linux에서 고가용성 클러스터 패키지를 설치 하는 방법](https://access.redhat.com/solutions/45930)합니다. 구독 및 리포지토리를 구성 하려면 다음이 단계를 수행 합니다.

1. 시스템을 등록 합니다.

   ```bash
   sudo subscription-manager register
   ```

   사용자 이름 및 암호를 제공 합니다.   

1. 등록에 대 한 사용 가능한 풀을 나열 합니다.

   ```bash
   sudo subscription-manager list --available
   ```

   사용 가능한 풀의 목록에서 항상 사용 가능한 구독에 대 한 풀 ID를 note 합니다.

1. 다음 스크립트를 업데이트 합니다. 대체 `<pool id>` 이전 단계에서 고가용성을 위한 풀 ID를 사용 하 여 합니다. 구독을 연결 하는 스크립트를 실행 합니다.

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. 리포지토리를 사용 합니다.

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

자세한 내용은 [Pacemaker-The 오픈 소스, 높은 가용성 클러스터](https://clusterlabs.org/pacemaker/)합니다. 

구독을 구성한 후 Pacemaker를 구성 하려면 다음 단계를 완료 합니다.

### <a name="configure-pacemaker"></a>Pacemaker를 구성 합니다.

구독을 등록 하면 Pacemaker를 구성 하려면 다음 단계를 완료 합니다.
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

사용 하 여 Pacemaker를 구성한 후 `pcs` 클러스터와 상호 작용할 수 있습니다. 클러스터에서 노드 하나에서 모든 명령을 실행 합니다. 

## <a name="configure-fencing-stonith"></a>펜싱 (STONITH) 구성

Pacemaker 클러스터 공급 업체는 STONITH를 사용 하도록 설정 및 지원 되는 클러스터 설치를 구성 하는 펜싱 장치에 필요 합니다. STONITH는 "헤드에 있는 다른 노드를 해결 합니다." Cluster resource manager는 노드 또는 노드 리소스의 상태를 확인할 수 없습니다, 하는 경우 펜스 다시 알려진 상태로 클러스터를 제공 합니다.

리소스 수준 펜싱 리소스를 구성 하 여 가동 중지 시에도 데이터 손상이 없는지 확인 합니다. 디스크를 표시 하려면 리소스 수준 펜싱을 사용할 수는 예를 들어, 통신 링크 중단 오래 된 경우 처럼 노드에서 합니다. 

노드 수준 펜싱 노드 리소스 실행 되지 않도록 보장 합니다. 이 노드를 다시 설정 하 여 이루어집니다. Pacemaker는 다양 한 장치 펜싱을 지원 합니다. 예제 서버는 무정전 전원 공급 장치 또는 관리 인터페이스 카드를 포함합니다.

STONITH를 및 펜싱에 대 한 내용은 다음 문서를 참조 합니다.

* [부터 pacemaker 클러스터](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/index.html)
* [펜싱 및 STONITH](https://clusterlabs.org/doc/crm_fencing.html)
* [Pacemaker 사용 하 여 Red Hat 고가용성 추가 기능: 펜싱](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

구성 펜싱 노드 수준 환경에 따라 크게 달라 집니다, 때문에 (구성할 수 있습니다 나중)이이 자습서에 대 한 비활성화 합니다. 다음 스크립트는 노드 수준 펜스를 비활성화합니다.

```bash
sudo pcs property set stonith-enabled=false
```
  
>[!IMPORTANT]
>STONITH를 사용 하지 않도록 설정 하는 것은 테스트 목적에 대해서만 합니다. 프로덕션 환경에서 Pacemaker를 사용 하려는 경우 환경에 따라 STONITH 구현 계획을 계속 사용 합니다. RHEL 모든 클라우드 환경 (Azure 포함) 또는 Hyper-v에 대 한 펜스 에이전트를 제공 하지 않습니다. 검사가 클러스터 공급 업체는 이러한 환경에서 실행 중인 프로덕션 클러스터에 대 한 지원을 제공 하지 않습니다. 이후 릴리스에서 제공 되는이 간격에 대 한 솔루션을 제작 하는 합니다.

## <a name="set-cluster-property-cluster-recheck-interval"></a>클러스터 속성 클러스터-다시 확인-간격 설정

`cluster-recheck-interval` 리소스 매개 변수, 제약 조건 또는 다른 클러스터 옵션에 대 한 변경 내용에 대 한 클러스터 확인 하는 폴링 간격을 나타냅니다. 클러스터를 연결 된 간격으로 복제본을 다시 시작 하려고 복제본이 다운 되 면 합니다 `failure-timeout` 값 및 `cluster-recheck-interval` 값입니다. 예를 들어 경우 `failure-timeout` 60 초로 설정 됩니다 및 `cluster-recheck-interval` 설정 120 초 이내 60 초 보다 큰 간격을 120 초로 다시 시작 시도 됩니다. 오류 제한 60s와 클러스터-다시 확인-간격은 60 초 보다 큰 값으로 설정 하는 것이 좋습니다. 클러스터 다시 확인 간격을 작은 값으로 설정 하는 것은 좋지 않습니다.

속성 값을 업데이트 하려면 `2 minutes` 실행:

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 해당 값이 false (RHEL 7.3, 7.4 등)는 최신 사용 가능한 Pacemaker 패키지 1.1.18-11.el7를 사용 하는 모든 배포 시작 실패-는-치명적이 지 클러스터 설정에 대 한 동작 변경을 소개 합니다. 이 변경에 장애 조치 워크플로 적용 합니다. 주 복제본 중단이 발생 하는 경우 클러스터는 사용 가능한 보조 복제본 중 하나에 장애 조치 해야 합니다. 대신 사용자 클러스터 유지 실패 한 주 복제본을 시작 하는 것을 알 수 있습니다. 해당 기본 되지 온라인 상태가 되 면 (때문에 영구 작동 중단)를 클러스터 하지 장애 조치 다른 사용 가능한 보조 복제본으로 합니다. 이러한 변경으로 인해 시작 실패-는-치명적이 지 설정 하려면 이전에 권장 되는 구성이 더 이상 유효 하며 설정의 기본 값으로 다시 되돌릴 `true`합니다. AG 리소스를 포함 하도록 업데이트 해야 하는 또한는 `failover-timeout` 속성입니다. 

속성 값을 업데이트 하려면 `true` 실행:

```bash
sudo pcs property set start-failure-is-fatal=true
```

업데이트 하는 `ag_cluster` 리소스 속성 `failure-timeout` 에 `60s` 실행:

```bash
pcs resource update ag_cluster meta failure-timeout=60s
```


Pacemaker 클러스터 속성에 대 한 자세한 내용은 [Pacemaker 클러스터 속성](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html)합니다.

## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker 용 SQL Server 로그인 만들기

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>가용성 그룹 리소스 만들기

가용성 그룹 리소스를 만들려면 사용 하 여 `pcs resource create` 명령 및 리소스 속성을 설정 합니다. 다음 명령은 만듭니다는 `ocf:mssql:ag` 형식 리소스 이름의 가용성 그룹에 대 한 마스터/슬레이브 `ag1`합니다.

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=60s master notify=true
``` 

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>가상 IP 리소스 만들기

가상 IP 주소 리소스를 만들려면 노드 하나에서 다음 명령을 실행 합니다. 네트워크에서 사용 가능한 정적 IP 주소를 사용 합니다. 사이의 IP 주소를 대체 `<10.128.16.240>` 유효한 IP 주소를 사용 합니다.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Pacemaker에서 해당 가상 서버 이름이 없습니다. 문자열 서버 이름 대신 IP 주소를 가리키는 연결 문자열을 사용 하려면 DNS에서 원하는 가상 서버 이름과 가상 ip 리소스를 등록 합니다. DR 구성에 대 한 기본 및 DR 사이트에서 DNS 서버를 사용 하 여 원하는 가상 서버 이름 및 IP 주소를 등록 합니다.

## <a name="add-colocation-constraint"></a>공동 배치 제약 조건 추가

Pacemaker 클러스터에서 리소스를 실행할 위치를 선택 하는 등 거의 모든 의사 결정은 점수를 비교 하 여 수행 됩니다. 점수는 리소스 당 계산 됩니다. Cluster resource manager는 특정 리소스에 대 한 점수가 가장 높은 노드를 선택합니다. 노드는 리소스에 대 한 음수 점수에 리소스는 해당 노드에서 실행할 수 없습니다.

Pacemaker 클러스터에서 제약 조건 사용 하 여 클러스터의 결정을 조작할 수 있습니다. 제한에는 점수는. 제약 조건에는 점수 보다 낮은 경우 `INFINITY`, Pacemaker 권장 사항으로 간주 합니다. 점수는 `INFINITY` 반드시 필요 합니다.

주 복제본과 가상 ip 리소스를 동일한 호스트에서 실행 되도록 무한대의 점수를 사용 하 여 공동 배치 제약 조건을 정의 합니다. 공동 배치 제약 조건을 추가할 노드 하나에서 다음 명령을 실행 합니다.

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>정렬 제약 조건을 추가 합니다.

공동 배치 제약 조건을 암시적 순서 제약 조건이 있습니다. 가용성 그룹 리소스를 이동 하기 전에 가상 IP 리소스를 이동 합니다. 기본적으로 이벤트 순서는:

1. 사용자 문제 `pcs resource move` 가용성 그룹에 주 노드 1에서 노드 2로 합니다.
1. 가상 IP 리소스를 노드 1에서 중지합니다.
1. 가상 IP 리소스를 노드 2에서 시작합니다.
  
   >[!NOTE]
   >이 시점에서 IP 주소 일시적으로 노드 2에는 지점 2 노드는 여전히 이전 장애 조치 하는 동안 보조 합니다. 
   
1. 노드 1의 기본 가용성 그룹 보조 복제본이 강등 합니다.
1. 노드 2에서 보조 가용성 그룹은 기본으로 승격 됩니다. 

IP 주소를 사전 장애 조치 보조 노드를 일시적으로 가리키는 방지 하려면 정렬 제약 조건을 추가 합니다. 

정렬 제약 조건을 추가할 노드 하나에서 다음 명령을 실행 합니다.

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>클러스터를 구성 하 고를 클러스터 리소스로 가용성 그룹을 추가한 후에 가용성 그룹 리소스를 장애 조치할 Transact SQL을 사용할 수 없습니다. Linux의 SQL Server 클러스터 리소스 연계 되지 않습니다와 긴밀 하 게 운영 체제에는 서버 장애 조치 클러스터 (WSFC (Windows) 같습니다. SQL Server 서비스를 클러스터의 현재 상태 인식 없습니다. 모든 오케스트레이션은 클러스터 관리 도구를 통해 수행 됩니다. RHEL 또는 Ubuntu에서 사용 하 여 `pcs` SLES 사용 `crm` 도구입니다. 

수동으로 가용성 그룹 장애 조치할 `pcs`합니다. TRANSACT-SQL을 사용 하 여 장애 조치를 시작 하지 않습니다. 자세한 내용은 [장애 조치](sql-server-linux-availability-group-failover-ha.md#failover)합니다.

## <a name="next-steps"></a>다음 단계

[HA 가용성 그룹을 작동](sql-server-linux-availability-group-failover-ha.md)
