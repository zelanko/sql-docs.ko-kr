---
title: Linux에서 SQL Server에 대 한 가용성 그룹에 항상 | Microsoft Docs
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
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
---
# <a name="always-on-availability-groups-on-linux"></a>Always On Linux에서 가용성 그룹

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux 기반에서 Always On 가용성 그룹 (Ag)의 특성을 설명 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 설치 합니다. Linux 및 Windows Server 장애 조치 클러스터 (WSFC) 간의 차이점에 대해서도 설명-Ag를 기반으로 합니다. 참조는 [Windows 기반 설명서](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) , Ag의 기본 사항에 대 한 역할을 동일한 Windows 및 Linux를 제외 하 고 WSFC에서 수행 합니다.

가용성 그룹의 상위 수준 관점에서 보면 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux에서와 동일 WSFC 기반으로 하는 구현에는 합니다. 모든 제한 사항 및 기능 같음을, 몇 가지 예외가 것입니다. 주요 차이점은 다음과 같습니다.

-   Linux의 Microsoft Distributed Transaction Coordinator (DTC)를 사용할 수 없습니다 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]합니다. 응용 프로그램 분산된 트랜잭션 사용 해야 하는 AG 필요 하는 경우 배포 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Windows에서 합니다.
-   Linux 기반 배포 대신 WSFC Pacemaker를 사용합니다.
-   작업 그룹 클러스터 시나리오를 제외 하 고 Windows에서 Ag에 대 한 대부분 구성과 달리 Pacemaker Active Directory 도메인 서비스 (AD DS) 필요가 없습니다.
-   한 노드에서 다른 AG 실패 하는 방법 Linux와 Windows 간에 차이가 있습니다.
-   와 같은 특정 설정을 `required_synchronized_secondaries_to_commit` WSFC 기반 설치를 TRANSACT-SQL을 사용 하는 반면 Pacemaker linux를 통해 변경 해야 합니다.

## <a name="number-of-replicas-and-cluster-nodes"></a>복제 데이터베이스와 클러스터 노드

AG에 [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] 두 총 복제본을 가질 수: 하나의 주 파일 그룹 및 가용성 용도로 사용할 수 있는 보조를 두 개 있습니다. 읽을 수 있는 쿼리와 같은 다른 작업에 사용할 수 없습니다. 에 AG [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] 총 복제본을 최대 9 개까지 가질 수: 기본 및 최대 3 (주 포함)는 8 개의 보조를 최대 개 하나 동기적 일 수 있습니다. 기본 클러스터를 사용 하는 경우 있을 수 있습니다는 최대 16 개의 노드로 구성 총 Corosync 관련 된 경우. 최대 9 개에서 16 개의 노드로 구성 된 가용성 그룹 걸쳐 있을 수 [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)], 2 대와 [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]합니다.

자동으로 다른 복제본으로 장애 조치 하는 기능을 필요로 하는 2 복제본 구성을에 설명 된 대로 구성 으로만 이동 가능한 복제본을 사용 해야 [구성 전용 복제 및 쿼럼](#configuration-only-replica-and-quorum)합니다. 구성 전용 복제에 도입 된 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] 누적 업데이트 1 (CU1)을 하는이 구성에 배포 된 최소 버전 이어야 합니다.

Pacemaker 사용 되는 경우 올바르게 구성 해야 실행 중 상태로 유지 됩니다. 즉,는 쿼럼 및 STONITH 해야 적절 하 게 구현 사항이 추가 Pacemaker 관점에서 볼 때 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 구성 전용 복제 등의 요구 사항을 합니다.

읽기 가능한 보조 복제본 에서만 지원 됩니다 [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]합니다.

## <a name="cluster-type-and-failover-mode"></a>클러스터 유형 및 장애 조치 모드

처음 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] Ag에 대 한 점 클러스터 유형입니다. Linux 용은 두 개의 올바른 값: 외부 및 없음입니다. 클러스터 유형의 외부 Pacemaker AG 아래 사용 됨을 의미 합니다. 클러스터 유형 장애 조치 모드도 외부로 설정할 수에 대해 외부를 사용 하 여 (에서 새로 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]). 자동 장애 조치가 지원 되지만 달리는 WSFC 장애 조치 모드가 설정 되어 외부, 자동이 아님 Pacemaker 사용 되는 경우. WSFC, 달리 AG의 Pacemaker 부분 AG 구성 된 후 생성 됩니다.

None 클러스터 유형에 대 한 요구 사항은 없습니다 또는 AG ´ ֲ, Pacemaker 의미 합니다. Pacemaker 구성 서버에도 AG이 none 인 클러스터 유형으로 구성 된 Pacemaker 됩니다 참조 하거나 관리 하지 않으므로 해당 AG 합니다. None 클러스터 종류는 보조 복제본에 주에서 수동 장애 조치만 지원합니다. None을 사용 하 여 만든 AG는 주로 읽기-확장 시나리오 뿐 아니라 업그레이드에 대 한 대상 합니다. 자동 장애 조치가 필요한 인 로컬 가용성 또는 재해 복구와 같은 시나리오에서 작동할 수 하는 동안 권장 되지 않습니다. 수신기 스토리 Pacemaker 하지 않고 보다 복잡 한 이기도합니다.

클러스터 유형에 저장 됩니다는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 동적 관리 뷰 (DMV) `sys.availability_groups`, 열에 `cluster_type` 및 `cluster_type_desc`합니다.

## <a name="requiredsynchronizedsecondariestocommit"></a>필수\_동기화\_보조\_를\_커밋

처음 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] Ag 호출에서 사용 되는 설정은 `required_synchronized_secondaries_to_commit`합니다. 이렇게 하면 AG 주와 록스텝에 있어야 하는 보조 복제본의 수입니다. 자동 장애 조치 (경우에 외부 클러스터 유형 Pacemaker와 통합 됨), 같은 있으며 온라인 또는 오프 라인 보조 복제본의 수는 경우 주 가용성 등의 동작을 제어 합니다. 이 과정에 대 한 자세한을 이해 하려면 참조 [가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)합니다. `required_synchronized_secondaries_to_commit` 값은 기본적으로 설정 되 고 Pacemaker에서 유지 관리 /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. 이 값을 직접 재정의할 수 있습니다.

조합의 `required_synchronized_secondaries_to_commit` 새 시퀀스 번호 (에 저장 되어 `sys.availability_groups`) Pacemaker 알립니다 및 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] , 예를 들어 자동 장애 조치가 발생할 수 있습니다. 이 경우 보조 복제본에 시퀀스 번호가 같은 기본 최신 모든 구성 정보가 최신 상태로 않음 것입니다.

에 대해 설정할 수 있는 값이 세 가지 `required_synchronized_secondaries_to_commit`: 0, 1 또는 2입니다. 복제 데이터베이스를 사용할 수 없게 하는 경우의 동작을 제어 합니다. 숫자 주와 동기화 해야 하는 보조 복제본의 수를 나타냅니다. Linux의 동작은 다음과 같습니다.

-   0 – 보조 복제본이 없는 동기화 할 필요 하기 때문 없는 자동 장애 조치가 가능 합니다. 주 데이터베이스를 항상 사용할 수 있습니다.
-   1 – 하나의 보조 복제본이 주;와 동기화 된 상태에서 여야 합니다. 자동 장애 조치가 가능 합니다. 동기 보조 복제본 사용 가능할 때까지 주 데이터베이스를 사용할 수 없는 경우
-   2-3 개 이상의 노드 AG 구성의 두 보조 복제본을 주;와 동기화 되어야 합니다. 자동 장애 조치가 가능 합니다.

`required_synchronized_secondaries_to_commit` 뿐만 아니라 데이터 손실을 동기 복제본으로 장애 조치의 동작을 제어 합니다. 1 또는 2의 값으로 보조 복제본은 항상 동기화 할 필요 이므로 데이터 중복 됩니다. 즉, 데이터가 손실 되지 않습니다.

값을 변경 하려면 `required_synchronized_secondaries_to_commit`, 다음 구문을 사용 합니다.

>[!NOTE]
>값을 변경 하면 일시적인 가동 중지 의미를 다시 시작 하려면 리소스를 하면 됩니다. 이 문제를 방지 하는 유일한 방법은 리소스를 관리 하지는 클러스터에 의해 일시적으로 설정 하는 합니다.

**Red Hat Enterprise Linux (RHEL) 및 Ubuntu**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server(SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

여기서 *AGResourceName* AG에 대해 구성 된 리소스의 이름 및 *값* 0, 1 또는 2가 있습니다. 매개 변수를 관리 하는 Pacemaker 기본값으로 다시 설정, 값이 없는 동일한 문을 실행 합니다.

다음 조건이 충족 되 면 AG의 자동 장애 조치 된 있습니다.

-   주 복제본과 보조 복제본은 동기 데이터 이동으로 설정 됩니다.
-   보조 동기화 (동기화 하지 않는) 동일한 데이터 요소에서 두 가지 의미의 상태를 있습니다.
-   클러스터 유형 외부로 설정 됩니다. 자동 장애 조치 none 클러스터 유형 수는 없습니다.
-   `sequence_number` 되도록 보조 복제본의 주에 시퀀스 번호가 가장 높은 – 즉, 보조 복제본의 `sequence_number` 원래 주 복제본에서 것과 일치 합니다.

이러한 조건이 충족 될 경우 주 복제본을 호스팅하는 서버 오류가 발생 하면 AG 동기 복제본 소유권을 변경 됩니다. 동기 복제본에 대 한 동작 (있는 있을 수 3의 총: 하나의 주 파일 그룹 및 두 개의 보조 복제본)를 통해 추가로 제어할 수 `required_synchronized_secondaries_to_commit`합니다. 이 Windows와 Linux 모두에서 Ag와 작동 하지만 완전히 다른 방식으로 구성 됩니다. Linux에서 값 자체 AG 리소스에서 클러스터에 의해 자동으로 구성 됩니다.

## <a name="configuration-only-replica-and-quorum"></a>구성 가능한 및 쿼럼

새로 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] c u 1을 기준으로 구성 으로만 이동 가능한 복제본입니다. Pacemaker WSFC 다르기 때문에 쿼럼 및 STONITH를 요구 하는 경우에 특히 더 2 노드 구성을 방금 작동 하지 않습니다 AG에 관한. FCI에 대 한 클러스터 계층에서 발생 하는 모든 FCI 장애 조치 중재 하기 때문에 Pacemaker에서 제공 하는 쿼럼 메커니즘 괜찮아 수 있습니다. AG에 대 한 linux 중재에서 발생 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 모든 메타 데이터가 저장 됩니다. 구성 전용 복제에 발생 하는 위치입니다.

다른 항목 없이 세 번째 노드 및 동기화 된 복제본이 하나 이상 필요한 것입니다. 이 작동 하지 않는 [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]이므로 두 개의 복제본 AG의 참여를 하나만 사용할 수 있습니다. 구성 전용 복제본 AG 구성의 다른 복제본과 동일 master 데이터베이스에서 AG 구성을 저장합니다. 구성 전용 복제본 AG에 참여 하는 사용자 데이터베이스는 수 없습니다. 구성 데이터는 주 데이터베이스에서 동기적으로 전송 됩니다. 이 구성 데이터가 든 상관 없이 자동 또는 수동 장애 조치 하는 동안 사용 됩니다.

쿼럼을 유지 관리 하 고 외부의 클러스터 유형 자동 장애 조치를 사용 하도록 설정 하려면 AG, 하거나 다음 조건을 충족 해야 합니다.

-   동기 복제본이 3 개 포함 ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] 만); 또는
-   두 개의 복제본 (주 및 보조) 뿐 아니라 구성 유일한 복제본을 포함 합니다.

외부 사용 하는지에 관계 없이 수동 장애 조치가 발생할 수 있습니다 또는 None 클러스터 AG 구성에 대 한 종류입니다. None 클러스터 형식을 갖는 AG와 구성 전용 복제본을 구성할 수 있지만는 것, 배포로 인해 복잡 하기 때문입니다. 해당 구성에 대해 수동으로 수정 `required_synchronized_secondaries_to_commit` 하나 이상의 동기화 복제본이 있도록 값이 1 이상 있어야 합니다.

구성 전용 복제본의 모든 버전에서 호스팅될 수 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 포함 하 여 [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]합니다. 따라서 라이선스 비용 최소화을 Ag에서 함께 작동 [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]합니다. 즉, 세 번째 서버에 대 한 최소 사양을 충족 해야 방금 필요 함을 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]이므로 AG에 대 한 사용자 트랜잭션 트래픽을 받고 있지 않습니다.

구성 전용 복제를 사용 하면 다음과 같은 동작이 있습니다.

-   기본적으로 `required_synchronized_secondaries_to_commit` 0으로 설정 됩니다. 이 수정할 수 있습니다 수동으로 1에 필요 합니다.
-   기본 실패 하는 경우 및 `required_synchronized_secondaries_to_commit` 은 0, 보조 복제본은 새로운 주 해 져 서 읽기 및 쓰기 모두에 사용할 수 있습니다. 값이 1 이면 자동 장애 조치가 발생 하지만 다른 복제본이 온라인 상태가 될 때까지 새 트랜잭션을 허용 하지 않습니다.
-   보조 복제본이 실패 하는 경우 및 `required_synchronized_secondaries_to_commit` 0, 주 복제본에는 여전히 트랜잭션을, 허용 있지만 (수동 또는 자동) 데이터 또는 가능한 장애 조치에 대 한 보호는이 시점에서 주에 실패 하면 보조 복제본을 사용할 수 없기 때문입니다.
-   구성 전용 복제에 실패 하면 AG는 정상적으로 작동 하지만 자동 장애 조치가 가능 합니다.
-   기본 트랜잭션 받아들일 수 없습니다 및 장소가 동기 보조 복제본과 구성 으로만 이동 가능한 복제본이 모두 실패 하지 않아야 기본에 대 한 합니다.

C u 1에서 알려진된 버그가 있습니다를 통해 생성 되는 corosync.log 파일에 로깅에서 `mssql-server-ha`합니다. 현재 메시지 있다고 "1 시퀀스 번호를 받을 것으로 예상 하지만 수신만 2 보조 복제본에 사용할 수 있는 필수 복제본 수에 따라 기본 수 없는 경우. 부족 합니다. 복제본은 온라인으로 안전 하 게 로컬 복제본을 승격 합니다. " 숫자가 반대로 바꿈을, 및 "2 시퀀스 번호를 수신 하려고 하는데만 1을 받았습니다이 필드. 부족 합니다. 복제본은 온라인으로 안전 하 게 로컬 복제본을 승격 합니다. " 

## <a name="multiple-availability-groups"></a>여러 가용성 그룹 

둘 이상의 AG Pacemaker 클러스터 또는 서버 집합을 만들 수 있습니다. 시스템 리소스입니다. AG 소유권 마스터도 표시 됩니다. 다른 Ag 서로 다른 노드에; 소유할 수 있습니다. 일부 필요가 동일한 노드에서 실행 중 이어야 합니다.

## <a name="drive-and-folder-location-for-databases"></a>데이터베이스에 대 한 드라이브 및 폴더 위치

AG에 참여 하는 사용자 데이터베이스에 대 한 드라이브 및 폴더 구조는 Windows 기반 Ag에서와 동일 해야 합니다. 예를 들어, 사용자 데이터베이스는 `/var/opt/mssql/userdata` 서버 A에서 Server B에서은 같은 폴더 있어야 유일한 예외는 섹션에서 설명한 [Windows 기반 가용성 그룹 및 복제본과의 상호 운용성](#interoperability-with-windows-based-availability-groups-and-replicas)합니다.

## <a name="the-listener-under-linux"></a>Linux 수신기

수신기가 AG에 대 한 선택적 기능입니다. 응용 프로그램 및 최종 사용자가 데이터를 호스팅하는 서버에 알아야 않아도 있도록 모든 연결 (읽기/쓰기 주 복제본 및/또는 읽기 전용 보조 복제본)에 대 한 항목의 단일 지점을 제공 합니다. WSFC에서 DNS 뿐 아니라 네트워크 이름 리소스와 다음 AD DS (필요한 경우)에 등록 되어 있는 IP 리소스의 조합입니다. AG 리소스 자체와 함께, 해당 추상화를 제공합니다. 수신기에 대 한 자세한 내용은 참조 하십시오. [수신기, 클라이언트 연결 및 응용 프로그램 장애 조치](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)합니다.

Linux 수신기가 다르게 구성 되어 있지만 해당 기능은 동일 합니다. Pacemaker에서 네트워크 이름 리소스의 개념이 없습니다 또는 AD DS;에 생성 하는 개체 노드 중 하나에서 실행할 수 있는 Pacemaker에서 만든 IP 주소 리소스만 있습니다. "이름"으로 DNS에서 수신기에 대 한 IP 리소스와 관련 된 항목을 만들어야 합니다. 수신기 IP 리소스는만 해당 가용성 그룹에 대 한 주 복제본을 호스팅하는 서버에서 활성화 됩니다.

Pacemaker을 사용 하는 경우 수신기와 연결 된 IP 주소 리소스 만들어집니다 됩니다 일시적인 가동 중지 한 서버에서 중지 하 고 다른에서 시작 하는 IP 주소 처럼 자동 또는 수동 장애 조치 인지 합니다. 단일 이름 및 IP 주소 조합 하 여 추상화를 제공이 중단을 마스킹하지 않습니다. 응용 프로그램은 어떤 종류의 기능이를 감지 하 여 다시 연결 하 여 연결 해제를 처리할 수 있어야 합니다.

그러나 DNS 이름 및 IP 주소는 여전히 부족 합니다. 보조 복제본에 대 한 읽기 전용 라우팅 등 WSFC에 수신기를 제공 하는 모든 기능을 제공 합니다. AG를 구성할 때 "수신기"는 여전히에서 구성할 수을 해야 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. 마법사 뿐만 아니라 TRANSACT-SQL 구문에서이 볼 수 있습니다. 두 가지 방법으로 Windows에서와 동일 하 게 작동 하도록 구성할 수 있습니다.

-   만든 "수신기"와 연결 된 IP 주소가 외부 클러스터 유형 AG에 대 한 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Pacemaker에서 만들어진 리소스의 IP 주소 여야 합니다.
-   None 클러스터 종류를 사용 하 여 만든 AG에 대 한 주 복제본과 연결 된 IP 주소를 사용 합니다.

그런 다음 제공 된 IP 주소와 연결 된 인스턴스가 응용 프로그램의 읽기 전용 라우팅 요청 등을 위한 코디네이터 됩니다.

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>Windows 기반 가용성 그룹 및 복제본과의 상호 운용성 

외부 웹 서비스 또는 WSFC 즉의 클러스터 형식을 갖는 AG 플랫폼 크로스 해당 복제본을 가질 수 없습니다. 이러한 사항은 AG 인지 [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] 또는 [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]합니다. 기본 클러스터와 기존의 AG 구성에서 즉, 하나의 복제본 WSFC 오류 코드 및 기타 Pacemaker와 linux에 있을 수 없습니다.

None 클러스터 유형 AG의 복제본이 있으므로 동일한 AG의 Linux 및 Windows 기반 복제본을 모두 수 OS 경계를 교차를 가질 수 있습니다. 예로 여기서 주 복제본은 Windows 기반 보조 Linux 배포판 중 하나에 다음과 같습니다.

![하이브리드 없음](./media/sql-server-linux-availability-group-overview/image1.png)

분산된 AG OS 경계를 넘을 수 수도 있습니다. 기본 Ag 구성 방법, 예: 외부 되 고 사용 하 여 구성에 대 한 규칙에 의해 바인딩된 Linux 전용 이지만 AG에 가입 된 WSFC를 사용 하 여 구성할 수 없습니다. 다음 예를 살펴 보십시오.

![하이브리드 Dist AG](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article “x”].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>다음 단계
[Linux에서 SQL Server에 대 한 가용성 그룹을 구성 합니다.](sql-server-linux-availability-group-configure-ha.md)

[Linux에서 SQL Server에 대 한 읽기 확장성이 가용성 그룹을 구성 합니다.](sql-server-linux-availability-group-configure-rs.md)

[RHEL에서 가용성 그룹 클러스터 리소스를 추가 합니다.](sql-server-linux-availability-group-cluster-rhel.md)

[SLES에 가용성 그룹 클러스터 리소스를 추가 합니다.](sql-server-linux-availability-group-cluster-sles.md)

[Ubuntu 가용성 그룹 클러스터 리소스를 추가 합니다.](sql-server-linux-availability-group-cluster-ubuntu.md)

[플랫폼 간 가용성 그룹 구성](sql-server-linux-availability-group-cross-platform.md)

