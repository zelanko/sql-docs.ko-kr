---
title: Always On 가용성 그룹 SQL Server on Linux의 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.openlocfilehash: 7de4097fdc843097cbd2865e4a4f3986c392ac04
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38045101"
---
# <a name="always-on-availability-groups-on-linux"></a>Always On 가용성 그룹이 linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux 기반에서 Always On 가용성 그룹 (Ag)의 특징을 설명 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 설치 합니다. Linux 및 Windows Server 장애 조치 클러스터 (WSFC) 간의 차이점에 대해서도 설명-Ag를 기반으로 합니다. 참조 된 [Windows 기반 설명서](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) , Ag의 기본 사항에 대 한 Windows 및 Linux WSFC 제외 하 고 동일한 작업 하면서 합니다.

대략적인 관점에서 가용성 그룹에서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux에서와 동일한 WSFC 기반 구현에 있습니다. 즉, 모든 제한 사항 및 기능은 동일 하며 몇 가지 예외 포함 합니다. 주요 차이점은 다음과 같습니다.

-   Microsoft Distributed Transaction Coordinator (DTC)는 Linux에서 지원 되지 않습니다 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]합니다. 분산 트랜잭션의 사용에 필요 하 고 AG를 해야 하는 응용 프로그램, 배포 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Windows에서.
-   Pacemaker는 WSFC 대신 사용 하는 Linux 기반 배포 합니다.
-   작업 그룹 클러스터 시나리오를 제외 하 고 Windows에서 Ag에 대 한 대부분의 구성과 달리 Pacemaker은 필요가 Active Directory Domain Services (AD DS)에 연결 합니다.
-   실패 한 노드에서 다른 AG 방법 Linux 및 Windows 간에 다릅니다.
-   와 같은 특정 설정을 `required_synchronized_secondaries_to_commit` WSFC 기반 설치를 사용 하는 TRANSACT-SQL을 사용 하는 반면 linux에서는 Pacemaker를 통해 변경할만 있습니다.

## <a name="number-of-replicas-and-cluster-nodes"></a>복제본 및 클러스터 노드 수

AG [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] 두 개의 총 복제본 수: 하나의 주 세션과 다른 하나의 보조 가용성 용도로 사용할 수 있는 합니다. 읽을 수 있는 쿼리와 같은 다른 용도로 사용할 수 없습니다. AG [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] 최대 9 개의 복제본을 가질 수 있습니다: 기본 및 최대 3 (기본 포함)는 8 개의 보조를 최대 하나 동기적 일 수 있습니다. 기본 클러스터를 사용 하는 경우 있을 수 있습니다 최대 16 개의 노드로 구성 총 Corosync 관련 된 경우. 가용성 그룹을 사용 하 여 16 노드의 최대 9 개에 걸쳐 있을 수 [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]를 사용 하 여 두 [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]합니다.

에 설명 된 대로 자동으로 다른 복제본으로 장애 조치 하는 기능을 해야 하는 두 개의 복제 구성이 구성 전용 복제본을 사용 해야 합니다 [구성 전용 복제본 및 쿼럼](#configuration-only-replica-and-quorum)합니다. 구성 전용 복제본에 도입 된 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] 누적 업데이트 1 (CU1)는이 구성에 대 한 배포 된 최소 버전 이어야 합니다.

Pacemaker를 사용 하는 경우 올바르게 구성 해야를 실행 상태로 유지 됩니다. 즉,는 쿼럼 및 STONITH 해야 적절 하 게 구현 외에도 Pacemaker 관점에서는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 구성 전용 복제본을 같은 요구 사항입니다.

읽기 가능한 보조 복제본 에서만 지원 됩니다 [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]합니다.

## <a name="cluster-type-and-failover-mode"></a>클러스터 유형 및 장애 조치 모드

새로운 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] Ag에 대 한 클러스터 유형의 도입입니다. Linux의 경우 두 개의 올바른 값: External 및 None입니다. 클러스터 유형이 외부인 Pacemaker AG 아래 사용 됨을 의미 합니다. 클러스터 종류는 장애 조치 모드를 외부로 설정도 필요에 대 한 외부를 사용 하 여 (새로운 항목도 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]). 자동 장애 조치는 지원 되지만 달리 WSFC 장애 조치 모드가 설정 되어 외부, 자동이 아님 Pacemaker 사용 되는 경우. WSFC와 달리 AG의 Pacemaker 부분 AG를 구성한 후 생성 됩니다.

클러스터 유형이 None에 대 한 요구 사항은 없습니다 나 AG를 사용 하는 Pacemaker를 의미 합니다. Pacemaker 구성 되어 있는 서버 에서도 AG 이면 클러스터 유형이 none, 구성 Pacemaker 되거나 되지 않습니다 참조는 AG를 관리 합니다. 클러스터 유형이 없음인는 보조 복제본으로 주 복제본에서 수동 장애 조치만 지원합니다. None을 사용 하 여 만든 AG 주로 대상으로 하는 읽기 확장 시나리오 뿐만 아니라 업그레이드 합니다. 자동 장애 조치가 필요한 인 로컬 가용성 또는 재해 복구와 같은 시나리오에서 작동할 수 있지만 권장 되지 않습니다. 수신기 스토리 Pacemaker 없이 더 복잡 한 이기도합니다.

클러스터 형식에 저장 됩니다는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 동적 관리 뷰 (DMV) `sys.availability_groups`, 열의 `cluster_type` 및 `cluster_type_desc`합니다.

## <a name="requiredsynchronizedsecondariestocommit"></a>필요한\_동기화\_보조\_하려면\_커밋

접하는 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] Ag 호출에서 사용 되는 설정은 `required_synchronized_secondaries_to_commit`합니다. 이렇게 하면 AG를 주 데이터베이스와 연장선 상에 해야 하는 보조 복제본의 수입니다. 자동 장애 조치 (경우에 클러스터 유형이 외부인 Pacemaker와 통합 됨) 등이 있으며 온라인 또는 오프 라인 적절 한 수의 보조 복제본 인 경우 주 가용성 등의 동작을 제어 합니다. 이 방식에 대해 자세히 알아보려면 [가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)합니다. 합니다 `required_synchronized_secondaries_to_commit` 값이 기본적으로 설정 되 고 Pacemaker에서 유지 관리 /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. 수동으로이 값을 재정의할 수 있습니다.

조합 `required_synchronized_secondaries_to_commit` 새 시퀀스 번호 (에 저장 되 `sys.availability_groups`) Pacemaker 알립니다 및 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] , 예를 들어, 자동 장애 조치가 발생할 수 있습니다. 이 경우 보조 복제본에 동일한 시퀀스 번호를 주, 즉 모든 최신 구성 정보를 사용 하 여 최신 상태로 해야 합니다.

세 가지 값을 설정할 수 있는 `required_synchronized_secondaries_to_commit`: 0, 1 또는 2입니다. 이러한 복제본을 사용할 수 없게 하는 경우의 동작을 제어 합니다. 숫자는 주 데이터베이스와 동기화 해야 하는 보조 복제본의 수에 해당 합니다. Linux는 동작은 다음과 같습니다.

-   0 – 자동 장애 조치가 불가능 보조 복제본이 없는 동기화 할 필요 하기 때문입니다. 주 데이터베이스를 항상 사용할 수 있습니다.
-   1 – 하나의 보조 복제본 주를 사용 하 여 동기화 된 상태에 있어야 합니다. 자동 장애 조치가 불가능 합니다. 보조 동기 복제본을 찾을 때까지 주 데이터베이스를 사용할 수 없는 경우
-   2-3 개 이상의 노드 AG 구성의 보조 복제본을 주와 동기화 되어야 합니다. 자동 장애 조치가 불가능 합니다.

`required_synchronized_secondaries_to_commit` 뿐만 아니라 동기 복제본 같지만 데이터 손실 장애 조치의 동작을 제어 합니다. 값이 1 또는 2 인를 사용 하 여 보조 복제본 이므로 항상 동기화 되어야 하는 데 필요한 데이터 중복성은 항상 있습니다. 즉, 데이터가 손실 되지 않습니다.

값을 변경 하려면 `required_synchronized_secondaries_to_commit`, 다음 구문을 사용 합니다.

>[!NOTE]
>값 변경에 일시적인 중단 의미를 다시 시작 하려면 리소스가 하면 됩니다. 이 문제를 방지 하는 유일한 방법은 관리 되지 클러스터에서 일시적으로 리소스를 설정 하는 것입니다.

**Ubuntu 및 Red Hat Enterprise Linux (RHEL)**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server(SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

여기서 *AGResourceName* AG에 대해 구성 된 리소스의 이름 및 *값* 은 0, 1 또는 2입니다. 매개 변수를 관리 하는 Pacemaker의 기본값으로 다시 설정, 값이 없는 동일한 문을 실행 합니다.

다음 조건이 충족 되 면 자동 장애 조치는 AG의이 가능 합니다.

-   주 복제본과 보조 복제본은 동기 데이터 이동으로 설정 됩니다.
-   보조 동기화 (0(not synchronizing) 동일한 데이터 지점에 두 가지 의미의 상태를 있습니다.
-   클러스터 유형은 외부로 설정 됩니다. 자동 장애 조치 클러스터 유형이 없음인 불가능합니다.
-   합니다 `sequence_number` 되도록 보조 복제본의 주에 가장 높은 시퀀스 번호가 – 즉, 보조 복제본의 `sequence_number` 원래 주 복제본에서 값과 일치 합니다.

이러한 조건이 충족 될 경우 주 복제본을 호스팅하는 서버 실패 AG를 동기 복제본 소유권을 변경 됩니다. 동기 복제본에 대 한 동작 (있습니다 수 있는 세 가지의 총: 하나의 주 복제본과 두 보조 복제본) 추가 하 여 제어할 수 있습니다 `required_synchronized_secondaries_to_commit`합니다. 이 Windows와 Linux 모두에서 Ag와 작동 하지만 완전히 다른 방식으로 구성 됩니다. Linux에서 값 자체 AG 리소스에서 클러스터에 의해 자동으로 구성 됩니다.

## <a name="configuration-only-replica-and-quorum"></a>구성 전용 복제본 및 쿼럼

새로운 기능 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] CU1부터 구성 전용 복제본입니다. Pacemaker는 WSFC 다르기 때문에 쿼럼 및 STONITH를 요구 하는 경우에 특히 방금 2-노드 구성이 작동 하지 않습니다 AG에 있어. Fci의 경우 Pacemaker에서 제공 하는 쿼럼 메커니즘 모든 FCI 장애 조치 중재 클러스터 계층에서 이루어지기 때문에 좋지만 수 있습니다. Linux에서 중재 진행을 AG에 대해 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]모든 메타 데이터 저장, 합니다. 구성 전용 복제본을 고려해 야 하는 위치입니다.

다른 항목 없이 세 번째 노드와 동기화 된 복제본이 하나 이상 필요한 것입니다. 이 대 한 작동 하지 않습니다 [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]가 AG에 참여 하는 두 개의 복제본만 가질 수 있습니다. 구성 전용 복제본 AG 구성의 다른 복제본과 같은 master 데이터베이스에서 된 AG 구성을 저장합니다. 구성 전용 복제본을 AG에 참여 하는 사용자 데이터베이스에 없습니다. 주 데이터베이스에서 구성 데이터를 동기적으로 보내집니다. 이 구성 데이터가 든 상관 없이 자동 또는 수동 장애 조치 하는 동안 사용 됩니다.

쿼럼을 유지 하 고 클러스터 유형이 외부인을 사용 하 여 자동 장애 조치를 사용 하도록 설정 하는 AG에 대 한 것 중 하나 수행 해야 합니다.

-   동기 복제본 3 개 ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] 만); 또는
-   구성 전용 복제본 뿐만 아니라 두 개의 복제본 (주 및 보조)가 있습니다.

None 클러스터 유형 AG 구성 또는 수동 장애 조치 외부를 사용 하 든 발생할 수 있습니다. 클러스터 유형이 없음인 있는 AG를 사용 하 여 구성 전용 복제본을 구성할 수 있지만, 좋지 않습니다, 배포 까다롭다는 때문입니다. 이러한 구성의 경우 수동으로 수정 `required_synchronized_secondaries_to_commit` 에 하나 이상의 동기화 복제본 되도록 적어도 1의 값입니다.

구성 전용 복제본의 모든 버전에서 호스팅할 수 있습니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]등 [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]합니다. 이 라이선스 비용을 최소화 하는 및에서 Ag를 사용 하 여 작동 [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]합니다. 즉, 세 번째 서버에 대 한 최소 사양을 충족 하도록 하기만 필요 함을 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]AG에 대해 사용자 트랜잭션 트래픽을 수신 하지는 때문입니다.

구성 전용 복제본을 사용 하면 다음과 같은 동작이 있습니다.

-   기본적으로 `required_synchronized_secondaries_to_commit` 0으로 설정 됩니다. 이 수동으로 수정할 수 1을 원하는 경우.
-   주 복제본이 실패 하 고 `required_synchronized_secondaries_to_commit` 0 인 보조 복제본을 새로운 주 데이터베이스가 되며 모두 읽기 및 쓰기에 사용할 수 있습니다. 값이 1 이면 자동 장애 조치가 발생 하지만 다른 복제본이 온라인 상태가 될 때까지 새 트랜잭션을 허용 하지 않습니다.
-   보조 복제본이 실패 하는 경우 및 `required_synchronized_secondaries_to_commit` 가 0, 주 복제본에는 여전히 트랜잭션을 허용 하지만 시점에서 주 복제본이 실패 합니다 (수동 또는 자동) 데이터도 가능한 장애 조치에 대 한 보호 보조 복제본을 사용할 수 없기 때문입니다.
-   구성 전용 복제본에 실패 하면 AG를 정상적으로 작동 하지만 자동 장애 조치가 가능 합니다.
-   기본 트랜잭션 받아들일 수 없습니다 및 장소가 동기 보조 복제본과 구성 전용 복제본이 모두 실패 하면 장애를 주에 대 한 합니다.

CU1에서 알려진된 버그가 있습니다를 통해 생성 되는 corosync.log 파일에 로깅을 `mssql-server-ha`합니다. 보조 복제본을 사용할 수 있는 필요한 복제본 수로 인해 주 데이터베이스가 되도록 수 없는 경우 현재 메시지 표시 되는데 "1 시퀀스 번호를 받을 것으로 예상만 2를 수신 합니다. 부족 복제본이 온라인 안전 하 게 로컬 복제본을 승격 합니다. " 숫자는 되돌릴 수 및 "2 시퀀스 번호를 받을 것으로 예상 하는데만 1을 받았습니다 나타나야. 부족 복제본이 온라인 안전 하 게 로컬 복제본을 승격 합니다. " 

## <a name="multiple-availability-groups"></a>여러 가용성 그룹 

Pacemaker 클러스터 또는 서버 집합 당 둘 이상의 AG은 만들 수 있습니다. 유일한 제한은 시스템 리소스를 보여 줍니다. 마스터에서 AG 소유권 표시 됩니다. 다른 Ag는 서로 다른 노드에; 소유할 수 있습니다. 일부 필요가 동일한 노드에서 실행 중 이어야 합니다.

## <a name="drive-and-folder-location-for-databases"></a>데이터베이스에 대 한 드라이브 및 폴더 위치

AG에 참여 하는 사용자 데이터베이스에 대 한 드라이브 및 폴더 구조는 Windows 기반 Ag에서 동일 해야 합니다. 예를 들어, 사용자 데이터베이스의 경우 `/var/opt/mssql/userdata` 서버 A에서 Server B에서 같은 폴더 있어야 유일한 예외는 섹션에서 설명한 [Windows 기반 가용성 그룹 및 복제본과의 상호 운용성](#interoperability-with-windows-based-availability-groups-and-replicas)합니다.

## <a name="the-listener-under-linux"></a>Linux에서 수신기

수신기는 AG에 대 한 선택적 기능입니다. 응용 프로그램 및 최종 사용자에 게 필요가 없습니다 서버 데이터를 호스팅하는 알 수 있도록 모든 연결 (읽기/쓰기 주 복제본 및/또는 읽기 전용 보조 복제본)에 대 한 단일 지점의 항목을 제공 합니다. WSFC DNS와 네트워크 이름 리소스 및 다음 AD DS (필요한 경우)에 등록 되는 IP 리소스의 조합입니다. 자체 AG 리소스와 함께에서 해당 추상화를 제공합니다. 수신기에 대 한 자세한 내용은 참조 하세요. [수신기, 클라이언트 연결 및 응용 프로그램 장애 조치](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)합니다.

Linux에서 수신기를 다르게 구성 되었지만 해당 기능이 동일 합니다. Pacemaker에 네트워크 이름 리소스의 개념은도 개체 만들어집니다 AD DS; 노드 중 하나에서 실행할 수 있는 Pacemaker에서 만든 IP 주소 리소스만 있습니다. "이름"을 사용 하 여 DNS에서 수신기에 대 한 IP 리소스와 연결 된 항목을 만들 수 해야 합니다. 수신기에 대 한 IP 리소스를 해당 가용성 그룹의 주 복제본을 호스팅하는 서버에서 활성화 됩니다.

Pacemaker는 수신기와 연결 된 IP 주소 리소스를 만들어질 경우 됩니다 일시적인 중단 IP 주소는 하나 이상의 서버에서 중지 하 고 다른에서 시작 하는 대로 자동 또는 수동 장애 조치 인지 합니다. 단일 이름 및 IP 주소를 조합 하 여 추상화를 제공 하는 동안 해당 마스킹하지는 않습니다 중단 합니다. 응용 프로그램은 일종의 기능을이 감지 하 고 다시 연결 하 여 연결 해제를 처리할 수 있어야 합니다.

DNS 이름 및 IP 주소를 조합 것 인데, 여전히 부족 합니다. 보조 복제본에 대 한 읽기 전용 라우팅 등 WSFC에서 수신기를 제공 하는 모든 기능을 제공 합니다. AG를 구성할 때 "수신기"도 구성 해야에서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. TRANSACT-SQL 구문 뿐만 아니라 마법사에서이 볼 수 있습니다. 두 가지 방법으로 Windows에서와 동일한 함수를 구성할 수 있습니다.

-   클러스터 유형이 외부인 AG, IP 주소에서 만든 "수신기"를 사용 하 여 관련 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Pacemaker에서 만든 리소스의 IP 주소 여야 합니다.
-   클러스터 유형이 None을 사용 하 여 만든 AG를 주 복제본과 연결 된 IP 주소를 사용 합니다.

그런 다음 제공된 된 IP 주소를 사용 하 여 연결 된 인스턴스는 응용 프로그램의 읽기 전용 라우팅 요청 등을 위해 코디네이터 됩니다.

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>Windows 기반 가용성 그룹 및 복제본과의 상호 운용성 

외부 또는 wsfc 클러스터 유형이 있는 AG는 플랫폼 간 복제본을 가질 수 없습니다. 이 true 인지 여부입니다 AG [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] 또는 [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]합니다. 기본 클러스터와 함께 일반적인 AG 구성에서 즉, 하나의 복제본을 WSFC와 Pacemaker 사용 하 여 Linux에서 다른에 있을 수 없습니다.

클러스터 유형이 없음인 AG 동일한 AG에서 하는 Linux 및 Windows 기반 복제본 모두 있을 수 있으므로 OS 경계를 교차 하는 해당 복제본을 가질 수 있습니다. 예로 주 복제본 인 Windows 기반 Linux 배포판 중 하나에서 보조 데이터베이스는 다음과 같습니다.

![하이브리드 없음](./media/sql-server-linux-availability-group-overview/image1.png)

분산된 AG를 OS 경계를 넘나들 수도 있습니다. 기본 Ag 구성 방법,와 같은 외부 되 고 사용 하 여 구성에 대 한 규칙에 의해 바인딩된은 Linux 전용 WSFC를 사용 하 여에 가입 된 AG를 구성할 수 없습니다. 다음 예를 살펴 보십시오.

![하이브리드 배포 AG](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article “x”].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>다음 단계
[Linux의 SQL Server에 대 한 가용성 그룹 구성](sql-server-linux-availability-group-configure-ha.md)

[Linux의 SQL Server에 대 한 읽기-배율 가용성 그룹 구성](sql-server-linux-availability-group-configure-rs.md)

[RHEL에서 가용성 그룹 클러스터 리소스를 추가 합니다.](sql-server-linux-availability-group-cluster-rhel.md)

[SLES의 가용성 그룹 클러스터 리소스를 추가 합니다.](sql-server-linux-availability-group-cluster-sles.md)

[Ubuntu에서 가용성 그룹 클러스터 리소스 추가](sql-server-linux-availability-group-cluster-ubuntu.md)

[플랫폼 간 가용성 그룹 구성](sql-server-linux-availability-group-cross-platform.md)

