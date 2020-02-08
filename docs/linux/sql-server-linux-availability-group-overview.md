---
title: SQL Server on Linux의 가용성 그룹
description: SQL Server on Linux의 Always On 가용성 그룹 특성을 알아봅니다.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 04/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.openlocfilehash: e4979fbb4e2dbbccf7ed11b744051373b0750d1f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558642"
---
# <a name="always-on-availability-groups-on-linux"></a>Linux의 Always On 가용성 그룹

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux 기반 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 설치에서 Always On AG(가용성 그룹)의 특징을 설명합니다. 또한 Linux 및 WSFC(Windows Server 장애 조치(failover) 클러스터) 기반 AG의 차이에 대해 설명합니다. AG는 WSFC를 제외하고 Windows 및 Linux에서 동일하게 작동하므로 AG의 기본 사항에 대해서는 [Windows 기반 설명서](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)를 참조하세요.

개략적으로 Linux의 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에서 가용성 그룹은 WSFC 기반 구현에 있는 것과 동일합니다. 즉, 모든 제한 사항 및 기능이 동일하며 몇 가지 예외가 있습니다. 주요 차이는 다음과 같습니다.

-   Microsoft DTC(Distributed Transaction Coordinator)는 SQL Server 2017 CU16부터 Linux에서 지원됩니다. 하지만, Linux의 가용성 그룹에서는 지원되지 않습니다. 애플리케이션에 분산 트랜잭션을 사용해야 하고 AG가 필요한 경우 Windows에 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 배포합니다.
-   고가용성이 필요한 Linux 기반 배포는 WSFC 대신 Pacemaker를 사용하여 클러스터링합니다.
-   작업 그룹 클러스터 시나리오를 제외하고 Windows에서 AG에 관련된 대부분의 구성과 달리 Pacemaker에는 AD DS(Active Directory Domain Services)가 필요하지 않습니다.
-   한 노드에서 다른 노드로 AG를 장애 조치(failover)하는 방법은 Linux 및 Windows에서 서로 다릅니다.
-   `required_synchronized_secondaries_to_commit` 같은 특정 설정은 Linux에서 Pacemaker를 통해 변경할 수 있지만, WSFC 기반 설치에는 Transact-SQL이 사용됩니다.

## <a name="number-of-replicas-and-cluster-nodes"></a>복제본 및 클러스터 노드 수

[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]의 AG에는 주 복제본 및 가용성 용도로만 사용할 수 있는 보조 복제본을 포함한 총 두 개의 복제본이 있을 수 있습니다. 읽을 수 있는 쿼리와 같은 다른 항목에는 사용할 수 없습니다. [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]의 AG에는 주 복제본 및 최대 8개 보조 복제본을 포함한 복제본이 총 9개까지 있을 수 있으며, 주 복제본을 포함한 최대 세 개의 복제본이 동기적일 수 있습니다. 기본 클러스터를 사용하는 경우 Corosync가 포함되면 최대 16개까지 노드가 있을 수 있습니다. 가용성 그룹은 [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]의 경우 16개 노드 중 최대 9개, [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]의 경우 두 개에 걸쳐 있을 수 있습니다.

다른 복제본으로 자동으로 장애 조치(failover)하는 기능이 필요한 두 개의 복제본 구성에서는 [구성 전용 복제본 및 쿼럼](#configuration-only-replica-and-quorum)에 설명된 대로 구성 전용 복제본을 사용해야 합니다. 구성 전용 복제본은 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] CU1(누적 업데이트 1)에서 도입되었으므로 이 구성을 사용하려면 이 버전 이상을 배포해야 합니다.

Pacemaker를 사용하는 경우 계속 실행되도록 제대로 구성되어 있어야 합니다. 즉, 구성 전용 복제본과 같은 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 요구 사항 외에도 Pacemaker 관점에서 쿼럼 및 STONITH가 제대로 구현되어야 합니다.

읽을 수 있는 보조 복제본은 [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]에서만 지원됩니다.

## <a name="cluster-type-and-failover-mode"></a>클러스터 유형 및 장애 조치(failover) 모드

AG의 클러스터 유형은 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]에 소개된 새로운 기능입니다. Linux의 경우 두 가지 유효한 값은 외부 및 없음입니다. 외부 클러스터 유형은 Pacemaker가 AG 바로 아래에서 사용됨을 의미합니다. 클러스터 유형에 외부를 사용하려면 장애 조치(failover) 모드도 외부로 설정해야 합니다([!INCLUDE[sssql17-md](../includes/sssql17-md.md)]의 새로운 기능). 자동 장애 조치(failover)가 지원되지만, WSFC와 달리 Pacemaker가 사용되는 경우 장애 조치(failover) 모드는 자동이 아닌 외부로 설정됩니다. WSFC와 달리 AG의 Pacemaker 부분은 AG가 구성된 후 생성됩니다.

클러스터 유형이 없음인 경우에는 Pacemaker에 대한 요구 사항이 없으며 AG가 Pacemaker를 사용하지 않습니다. Pacemaker가 구성된 서버에서도 AG의 클러스터 유형이 없음으로 구성된 경우 Pacemaker는 해당 AG를 보거나 관리하지 않습니다. 클러스터 유형이 없음인 경우에는 주 복제본에서 보조 복제본으로 수동 장애 조치(failover)만 지원합니다. 없음을 사용하여 만든 주로 AG는 업그레이드뿐만 아니라 읽기 확장 시나리오를 대상으로 합니다. 이 AG는 자동 장애 조치(failover)가 필요하지 않은 재해 복구 또는 로컬 가용성과 같은 시나리오에서 작동할 수 있지만 권장되지는 않습니다. 또한 Pacemaker가 없으면 수신기 스토리가 더 복잡해집니다.

클러스터 유형은 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] DMV(동적 관리 뷰) `sys.availability_groups`의 `cluster_type` 및 `cluster_type_desc` 열에 저장됩니다.

## <a name="required_synchronized_secondaries_to_commit"></a>required\_synchronized\_secondaries\_to\_commit

AG에서 사용되는 `required_synchronized_secondaries_to_commit` 설정은 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]의 새로운 기능입니다. 이 기능은 주 복제본과 같은 비율로 증가해야 하는 보조 복제본 수를 AG에 알립니다. 이 기능을 통해 자동 장애 조치(failover) 같은 항목을 사용할 수 있으며(클러스터 유형이 외부이고 Pacemaker와 통합되는 경우에만), 올바른 수의 보조 복제본이 온라인 또는 오프라인인 경우 주 복제본 가용성 같은 항목의 동작을 제어합니다. 작동 방법에 대한 자세한 내용은 [가용성 그룹 구성을 위한 고가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)를 참조하세요. `required_synchronized_secondaries_to_commit` 값이 기본적으로 설정되고 Pacemaker/[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에서 유지 관리됩니다. 이 값은 수동으로 재정의할 수 있습니다.

`required_synchronized_secondaries_to_commit` 및 새 시퀀스 번호(`sys.availability_groups`에 저장됨)의 조합으로 Pacemaker 및 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에 정보를 제공합니다(예: 자동 장애 조치(failover)가 수행될 수 있음). 이 경우 보조 복제본의 시퀀스 번호는 주 복제본과 동일합니다. 즉, 모든 최신 구성 정보를 사용하여 최신 상태로 유지됩니다.

`required_synchronized_secondaries_to_commit`에 대해 설정할 수 있는 세 가지 값은 0, 1 또는 2입니다. 이 값은 복제본을 사용할 수 없게 되는 상황의 동작을 제어합니다. 숫자는 주 복제본과 동기화해야 하는 보조 복제본의 수에 해당합니다. Linux에서 동작은 다음과 같습니다.

-   0 - 보조 복제본이 주 복제본과 동기화될 필요가 없습니다. 그러나 보조 복제본이 동기화되지 않으면 자동 장애 조치(failover)가 수행되지 않습니다. 
-   1 - 하나의 보조 복제본이 주 복제본과 동기화된 상태여야 합니다. 자동 장애 조치(failover)가 가능합니다. 보조 동기 복제본을 사용할 수 있을 때까지 주 데이터베이스를 사용할 수 없습니다.
-   2 - 세 개 이상의 노드 AG 구성에 있는 두 보조 복제본이 모두 주 복제본과 동기화되어야 합니다. 자동 장애 조치(failover)가 가능합니다.

`required_synchronized_secondaries_to_commit`는 동기 복제본을 사용한 장애 조치(failover) 동작뿐만 아니라 데이터 손실도 제어합니다. 값이 1 또는 2이면 보조 복제본은 항상 동기화되어야 하므로 항상 데이터 중복성이 있습니다. 즉, 데이터가 손실되지 않습니다.

`required_synchronized_secondaries_to_commit` 값을 변경하려면 다음 구문을 사용합니다.

>[!NOTE]
>값을 변경하면 리소스가 다시 시작되므로 짧은 중단이 나타납니다. 이 문제를 방지하는 유일한 방법은 리소스가 일시적으로 클러스터에서 관리되지 않도록 설정하는 것입니다.

**RHEL(Red Hat Enterprise Linux) 및 Ubuntu**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server(SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

여기서 *AGResourceName*은 AG에 대해 구성된 리소스 이름이며 *Value*는 0, 1 또는 2입니다. 매개 변수를 관리하는 Pacemaker의 기본값으로 다시 설정하려면 값 없이 동일한 문을 실행합니다.

다음 조건이 충족되면 AG의 자동 장애 조치(failover)를 수행할 수 있습니다.

-   주 복제본과 보조 복제본은 동기 데이터 이동으로 설정됩니다.
-   보조 복제본의 상태가 동기화됨(동기화 중이 아님)입니다. 즉, 두 복제본이 동일한 데이터 요소에 있습니다.
-   클러스터 유형이 외부로 설정됩니다. 클러스터 유형이 없음이면 자동 장애 조치(failover)를 수행할 수 없습니다.
-   주 복제본이 될 보조 복제본의 `sequence_number`에는 가장 높은 시퀀스 번호가 포함됩니다. 즉, 보조 복제본의 `sequence_number`는 원래 주 복제본의 번호와 일치합니다.

이 조건이 충족되고 주 복제본을 호스트하는 서버에서 오류가 발생하면 AG가 동기 복제본에 대한 소유권을 변경합니다. 동기 복제본(주 복제본 하나 및 보조 복제본 두 개로 총 세 걔의 복제본이 있을 수 있음)의 동작은 `required_synchronized_secondaries_to_commit`를 통해 추가로 제어할 수 있습니다. 이 기능은 Windows 및 Linux의 AG에서 작동하지만 완전히 다르게 구성됩니다. Linux에서 값은 AG 리소스 자체의 클러스터에 의해 자동으로 구성됩니다.

## <a name="configuration-only-replica-and-quorum"></a>구성 전용 복제본 및 쿼럼

구성 전용 복제본도 CU1부터 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]의 새로운 기능입니다. 특히 쿼럼 및 STONITH 필요를 고려하는 경우 Pacemaker는 WSFC와 다르기 때문에 AG의 경우 2노드 구성을 포함하는 것만으로는 효과가 없습니다. FCI의 경우 모든 FCI 장애 조치(failover) 중재가 클러스터 계층에서 발생하기 때문에 Pacemaker에서 제공하는 쿼럼 메커니즘이 적절할 수 있습니다. AG의 경우 Linux에서 중재는 모든 메타데이터가 저장되는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에서 발생합니다. 여기에서 구성 전용 복제본이 작동합니다.

다른 것 없이 세 번째 노드와 하나 이상의 동기화된 복제본이 필요합니다. 구성 전용 복제본은 AG 구성의 다른 복제본과 동일하게 master 데이터베이스에 AG 구성을 저장합니다. 구성 전용 복제본에는 AG에 참여하는 사용자 데이터베이스가 없습니다. 구성 데이터는 주 복제본에서 동기적으로 전송됩니다. 그런 다음, 이 구성 데이터는 자동 또는 수동인지 여부에 관계없이 장애 조치(failover) 중에 사용됩니다.

AG에서 쿼럼을 유지 관리하고 클러스터 유형이 외부인 자동 장애 조치(failover)를 사용하도록 설정하려면 다음을 충족해야 합니다.

-   세 개의 동기 복제본이 있거나([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] 전용)
-   구성 전용 복제본 및 두 개의 복제본(주 및 보조)이 있어야 합니다.

AG 구성에 외부 또는 없음 클러스터 유형을 사용하는지 여부에 관계없이 수동 장애 조치(failover)를 수행할 수 있습니다. 구성 전용 복제본은 클러스터 유형이 없음인 AG로 구성할 수 있지만 배포가 복잡해지므로 권장되지 않습니다. 해당 구성의 경우 1 이상의 값을 포함하도록 `required_synchronized_secondaries_to_commit`를 수동으로 수정하면 하나 이상의 동기화된 복제본이 있게 됩니다.

구성 전용 복제본은 [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]를 포함한 모든 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 버전에서 호스트할 수 있습니다. 이렇게 하면 라이선스 비용이 최소화되고 [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]에서 AG와 함께 작동합니다. 이는 세 번째 필수 서버가 AG에 대한 사용자 트랜잭션 트래픽을 수신하지 않으므로 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]의 최소 사양을 충족하면 된다는 것을 의미합니다.

구성 전용 복제본을 사용하는 경우 다음과 같이 동작합니다.

-   기본적으로 `required_synchronized_secondaries_to_commit`는 0으로 설정됩니다. 필요한 경우 수동으로 1로 수정할 수 있습니다.
-   주 복제본에서 오류가 발생하고 `required_synchronized_secondaries_to_commit`가 0이면 보조 복제본은 새로운 주 복제본이 되며 읽기와 쓰기에 둘 다 사용할 수 있습니다. 값이 1이면 자동 장애 조치(failover)가 수행되지만 다른 복제본이 온라인 상태가 될 때까지 새 트랜잭션을 수락하지 않습니다.
-   보조 복제본에서 오류가 발생하고 `required_synchronized_secondaries_to_commit`가 0이면 주 복제본은 여전히 트랜잭션을 수락하지만, 이때 주 복제본에서 오류가 발생하면 보조 복제본을 사용할 수 없기 때문에 데이터 보호 및 가능한 장애 조치(failover)(수동 또는 자동)가 없습니다.
-   구성 전용 복제본에서 오류가 발생하면 AG가 정상적으로 작동하지만 자동 장애 조치(failover)를 수행할 수 없습니다.
-   동기 보조 복제본 및 구성 전용 복제본에서 둘 다 오류가 발생하면 주 복제본은 트랜잭션을 수락할 수 없으며 주 복제본을 장애 조치(failover)할 곳이 없습니다.

CU1에는 `mssql-server-ha`를 통해 생성된 corosync.log 파일의 로깅에 알려진 버그가 있습니다. 사용 가능한 필수 복제본 수로 인해 보조 복제본이 주 복제본이 될 수 없는 경우 현재 메시지에는 “시퀀스 번호 1이 수신되어야 하지만 2만 수신되었습니다. 로컬 복제본을 안전하게 승격할 온라인 복제본이 충분하지 않습니다.”라고 표시됩니다. 번호는 역방향이어야 하며 “시퀀스 번호 2를 수신해야 하지만 1만 수신되었습니다. 로컬 복제본을 안전하게 승격할 온라인 복제본이 충분하지 않습니다.”라고 표시됩니다. 

## <a name="multiple-availability-groups"></a>여러 가용성 그룹 

Pacemaker 클러스터 또는 서버 세트당 AG를 두 개 이상 만들 수 있습니다. 유일한 제한 사항은 시스템 리소스입니다. AG 소유권은 master에 의해 표시됩니다. 노드별로 서로 다른 AG를 소유할 수 있으며 AG가 모두 동일한 노드에서 실행되고 있을 필요는 없습니다.

## <a name="drive-and-folder-location-for-databases"></a>데이터베이스의 드라이브 및 폴더 위치

Windows 기반 AG처럼 AG에 참여하는 사용자 데이터베이스의 드라이브 및 폴더 구조는 동일해야 합니다. 예를 들어 사용자 데이터베이스가 서버 A의 `/var/opt/mssql/userdata`에 있는 경우 서버 B에 동일한 폴더가 있어야 합니다. 이에 대한 유일한 예외는 [Windows 기반 가용성 그룹 및 복제본과 상호 운용성](#interoperability-with-windows-based-availability-groups-and-replicas) 섹션에 나와 있습니다.

## <a name="the-listener-under-linux"></a>Linux의 수신기

수신기는 AG에 대한 선택적 기능입니다. 수신기는 모든 연결(주 복제본에 대한 읽기/쓰기 및/또는 보조 복제본에 대한 읽기 전용)에 대한 단일 진입점을 제공하므로 애플리케이션 및 최종 사용자가 데이터를 호스트하는 서버를 알 필요가 없습니다. WSFC에서 수신기는 네트워크 이름 리소스와 IP 리소스의 조합이며, 나중에 DNS 및 AD DS(필요한 경우)에 등록됩니다. AG 리소스 자체와 결합되어 해당 추상화를 제공합니다. 수신기에 대한 자세한 내용은 [수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)를 참조하세요.

Linux의 수신기는 다르게 구성되지만 해당 기능은 동일합니다. Pacemaker에는 네트워크 이름 리소스의 개념이 없고 AD DS에서 생성된 개체도 없습니다. 모든 노드에서 실행할 수 있는 Pacemaker에서 만든 IP 주소 리소스만 있습니다. “이름”을 사용하여 DNS에서 수신기의 IP 리소스와 연결된 항목을 만들어야 합니다. 수신기의 IP 리소스는 해당 가용성 그룹의 주 복제본을 호스트하는 서버에서만 활성화됩니다.

Pacemaker가 사용되고 수신기와 연결된 IP 주소 리소스가 생성되면 자동 또는 수동 장애 조치(failover)인지 여부에 관계없이 한 서버에서 IP 주소가 중지되고 다른 서버에서 시작될 때 짧은 중단이 나타납니다. 이 기능은 단일 이름과 IP 주소의 조합을 통해 추상화를 제공하지만 중단을 마스크 처리하지 않습니다. 애플리케이션은 이 중단을 감지하고 다시 연결하는 기능을 포함하여 연결 해제를 처리할 수 있어야 합니다.

그러나 DNS 이름과 IP 주소의 조합은 WSFC의 수신기가 제공하는 모든 기능(예: 보조 복제본에 대한 읽기 전용 라우팅)을 제공하기에는 충분하지 않습니다. AG를 구성할 때 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에서 “수신기”도 구성해야 합니다. 이 수신기는 Transact-SQL 구문 및 마법사에서 확인할 수 있습니다. Windows와 동일하게 작동하도록 구성할 수 있는 두 가지 방법이 있습니다.

-   외부 클러스터 유형을 사용하는 AG의 경우 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에서 생성된 “수신기”와 연결된 IP 주소는 Pacemaker에서 생성된 리소스의 IP 주소여야 합니다.
-   없음 클러스터 유형을 사용하는 AG의 경우 주 복제본과 연결된 IP 주소를 사용합니다.

그런 다음, 제공된 IP 주소와 연결된 인스턴스는 애플리케이션의 읽기 전용 라우팅 요청과 같은 항목에 대한 코디네이터가 됩니다.

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>Windows 기반 가용성 그룹 및 복제본과 상호 운용성 

외부 클러스터 유형을 사용하는 AG 또는 WSFC인 AG의 복제본은 플랫폼에 걸쳐 있을 수 없습니다. 이 내용은 AG가 [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] 또는 [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]인지 여부에 관계없이 모두 적용됩니다. 즉, 기본 클러스터를 사용하는 기존 AG 구성의 경우 한 복제본은 WSFC에 있고 다른 복제본은 Pacemaker를 사용하는 Linux에 있을 수 없습니다.

없음 클러스터 유형을 사용하는 AG의 복제본은 OS 경계에 걸쳐 있을 수 있으므로 Linux 및 Windows 기반 복제본이 둘 다 동일한 AG에 있을 수 있습니다. 주 복제본은 Windows 기반이지만 보조 복제본은 Linux 배포 중 하나에 있는 예제가 제공됩니다.

![하이브리드 없음](./media/sql-server-linux-availability-group-overview/image1.png)

분산 AG는 OS 경계에 걸쳐 있을 수도 있습니다. 기본 AG에는 Linux 전용이 되는 외부로 구성된 AG와 같이 구성 방식에 대한 규칙이 적용되지만, 조인되는 AG는 WSFC를 사용하여 구성할 수 있습니다. 다음과 같은 예제를 참조하세요.

![하이브리드 배포 AG](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article "x"].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>다음 단계
[SQL Server on Linux에 대해 가용성 그룹 구성](sql-server-linux-availability-group-configure-ha.md)

[SQL Server on Linux에 대해 읽기 확장 가용성 그룹 구성](sql-server-linux-availability-group-configure-rs.md)

[RHEL에서 가용성 그룹 클러스터 리소스 추가](sql-server-linux-availability-group-cluster-rhel.md)

[SLES에서 가용성 그룹 클러스터 리소스 추가](sql-server-linux-availability-group-cluster-sles.md)

[Ubuntu에서 가용성 그룹 클러스터 리소스 추가](sql-server-linux-availability-group-cluster-ubuntu.md)

[플랫폼 간 가용성 그룹 구성](sql-server-linux-availability-group-cross-platform.md)

