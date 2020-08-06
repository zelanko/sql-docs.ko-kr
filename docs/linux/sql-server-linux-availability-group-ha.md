---
title: 가용성 그룹 배포 패턴 - SQL Server on Linux
description: Linux 서버의 SQL Server Always On 가용성 그룹에 대해 지원되는 배포 구성을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 04/17/2019
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.openlocfilehash: a7a6ce8832db85d54ad9513d8258af2863dab2e5
ms.sourcegitcommit: 4b775a3ce453b757c7435cc2a4c9b35d0c5a8a9e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/31/2020
ms.locfileid: "87472424"
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>가용성 그룹 구성의 고가용성 및 데이터 보호

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 Linux 서버의 SQL Server Always On 가용성 그룹에 대해 지원되는 배포 구성을 제공합니다. 가용성 그룹은 고가용성 및 데이터 보호를 지원합니다. 자동 오류 탐지, 자동 장애 조치(failover) 및 장애 조치(failover) 후의 투명한 재연결은 고가용성을 제공합니다. 동기화된 복제본은 데이터 보호를 제공합니다. 

WSFC(Windows Server 장애 조치(failover) 클러스터)에서 고가용성을 위한 일반적인 구성은 동기 복제본 2개와 세 번째 서버 또는 파일 공유를 사용하여 쿼럼을 제공합니다. 파일 공유 감시는 동기화 상태 및 복제본 역할과 같은 가용성 그룹 구성의 유효성을 검사합니다. 이 구성은 장애 조치(failover) 대상으로 선택된 보조 복제본에 최신 데이터 및 가용성 그룹 구성 변경 내용이 포함되어 있는지 확인합니다. 

WSFC는 가용성 그룹 복제본과 파일 공유 감시 간의 장애 조치(failover) 조정을 위해 구성 메타데이터를 동기화합니다. 가용성 그룹이 WSFC에 있지 않은 경우 SQL Server 인스턴스는 master 데이터베이스에 구성 메타데이터를 저장합니다.

예를 들어 Linux 클러스터의 가용성 그룹에 `CLUSTER_TYPE = EXTERNAL`이 있습니다. 따라서 장애 조치(failover)를 조정할 WSFC가 없습니다. 이 경우에는 SQL Server 인스턴스가 구성 메타데이터를 관리하고 유지합니다. 클러스터에 미러링 모니터 서버가 없기 때문에 세 번째 SQL Server 인스턴스가 구성 상태 메타데이터를 저장해야 합니다. 세 개의 SQL Server 인스턴스가 모두 결합되어 클러스터의 분산 메타데이터 스토리지를 제공합니다. 

클러스터 관리자는 가용성 그룹의 SQL Server 인스턴스를 쿼리하고 장애 조치(failover)를 오케스트레이션하여 고가용성을 유지 관리할 수 있습니다. Linux 클러스터에서는 Pacemaker가 클러스터 관리자입니다. 

SQL Server 2017 CU 1에서는 동기 복제본 2개와 구성 전용 복제본 1개의 `CLUSTER_TYPE = EXTERNAL`을 사용하여 가용성 그룹의 고가용성을 설정합니다. 구성 전용 복제본은 SQL Server Express 버전을 비롯한 SQL Server 2017 CU1 이상 버전에서 호스트할 수 있습니다. 구성 전용 복제본은 master 데이터베이스에서 가용성 그룹 구성 정보를 유지 관리하지만, 가용성 그룹의 사용자 데이터베이스는 포함하지 않습니다. 

## <a name="how-the-configuration-affects-default-resource-settings"></a>구성이 기본 리소스 설정에 미치는 영향

SQL Server 2017에서는 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 클러스터 리소스 설정이 도입되었습니다. 이 설정은 주 복제본이 각 트랜잭션을 커밋하기 전에 지정된 개수의 보조 복제본이 트랜잭션 데이터를 로그에 쓰도록 보장합니다. 외부 클러스터 관리자를 사용하는 경우 이 설정은 고가용성 및 데이터 보호에 모두 영향을 줍니다. 설정의 기본값은 클러스터 리소스가 생성되는 시점의 아키텍처에 따라 다릅니다. SQL Server 리소스 에이전트(`mssql-server-ha`)를 설치하고 가용성 그룹의 클러스터 리소스를 만들 때, 클러스터 관리자는 가용성 그룹 구성을 검색하고 그에 따라 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`을 설정합니다. 

구성에서 지원되는 경우, 리소스 에이전트 매개 변수 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`은 고가용성 및 데이터 보호를 제공하는 값으로 설정됩니다. 자세한 내용은 [pacemaker용 SQL Server 리소스 에이전트 이해](#pacemakerNotify)를 참조하세요.

다음 섹션에서는 클러스터 리소스의 기본 동작을 설명합니다. 

고가용성, 데이터 보호 및 읽기 확장에 대한 특정 비즈니스 요구 사항을 충족하는 가용성 그룹 디자인을 선택합니다.

다음 구성에서는 가용성 그룹 디자인 패턴 및 각 패턴의 기능을 설명합니다. 이러한 디자인 패턴은 고가용성 솔루션을 위해 `CLUSTER_TYPE = EXTERNAL`을 사용하는 가용성 그룹에 적용됩니다. 

- **동기 복제본 3개**
- **동기 복제본 2개**
- **동기 복제본 2개와 구성 전용 복제본 1개**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>동기 복제본 3개

이 구성은 동기 복제본 3개로 이루어져 있습니다. 기본적으로 고가용성 및 데이터 보호 기능을 제공합니다. 읽기 확장도 제공할 수 있습니다.

![복제본 3개][3]

동기 복제본 3개가 있는 가용성 그룹은 읽기 확장, 고가용성 및 데이터 보호를 제공할 수 있습니다. 다음 표에서는 가용성 동작을 설명합니다. 

|가용성 동작 |읽기 확장|고가용성 및 </br> 데이터 보호 | 데이터 보호|
|:---|---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>\*</sup>|2|
|주 중단 |자동 장애 조치(failover). 새로운 주 복제본은 읽기/쓰기입니다. |자동 장애 조치(failover). 새로운 주 복제본은 읽기/쓰기입니다. |자동 장애 조치(failover). 이전 주 복제본이 복구되어 가용성 그룹에 보조 복제본으로 참가할 때까지 새로운 주 복제본을 사용자 트랜잭션에 사용할 수 없습니다. |
|1개 보조 복제본 중단  | 주 복제본은 읽기/쓰기입니다. 주 복제본도 실패하는 경우 자동 장애 조치(failover)가 수행되지 않습니다. |주 복제본은 읽기/쓰기입니다. 주 복제본도 실패하는 경우 자동 장애 조치(failover)가 수행되지 않습니다. | 주 복제본을 사용자 트랜잭션에 사용할 수 없습니다. |

<sup>\*</sup> 기본값

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>동기 복제본 2개

이 구성을 사용하면 데이터를 보호할 수 있습니다. 다른 가용성 그룹 구성과 마찬가지로 읽기 확장을 사용하도록 설정할 수 있습니다. 동기 복제본 2개로 이루어진 구성은 자동 고가용성을 제공하지 않습니다. 복제본 2개로 이루어진 구성은 SQL Server 2017 RTM에만 적용할 수 있으며, SQL Server 2017 CU1 및 이후 버전에서는 더 이상 지원되지 않습니다.

![동기 복제본 2개][1]

동기 복제본 2개가 있는 가용성 그룹은 읽기 확장 및 데이터 보호를 제공합니다. 다음 표에서는 가용성 동작을 설명합니다. 

|가용성 동작 |읽기 확장 |데이터 보호|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|주 중단 | 수동 장애 조치(failover). 데이터 손실이 있을 수 있습니다. 새로운 주 복제본은 읽기/쓰기입니다.| 자동 장애 조치(failover). 이전 주 복제본이 복구되어 가용성 그룹에 보조 복제본으로 참가할 때까지 새로운 주 복제본을 사용자 트랜잭션에 사용할 수 없습니다.|
|1개 보조 복제본 중단  |주 복제본은 읽기/쓰기이고, 데이터 손실 위험에 공개됩니다. |보조 복제본이 복구될 때까지 주 복제본을 사용자 트랜잭션에 사용할 수 없습니다.|

<sup>\*</sup> 기본값

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>동기 복제본 2개와 구성 전용 복제본 1개

둘 이상의 동기 복제본과 구성 전용 복제본 1개가 있는 가용성 그룹은 데이터 보호 기능을 제공하며 고가용성을 제공할 수도 있습니다. 다음 다이어그램은 이 아키텍처를 나타냅니다.

![구성 전용 가용성 그룹][2]

1. 보조 복제본에 사용자 데이터 동기 복제. 가용성 그룹 구성 메타데이터도 포함합니다.
2. 가용성 그룹 구성 메타데이터 동기 복제. 사용자 데이터는 포함하지 않습니다.

가용성 그룹 다이어그램에서 주 복제본은 보조 복제본과 구성 전용 복제본에 모두 구성 데이터를 밀어넣습니다. 보조 복제본은 사용자 데이터도 받습니다. 구성 전용 복제본은 사용자 데이터를 받지 않습니다. 보조 복제본은 동기 가용성 모드입니다. 구성 전용 복제본은 가용성 그룹의 데이터베이스를 포함하지 않고 가용성 그룹에 대한 메타데이터만 포함합니다. 구성 전용 복제본의 구성 데이터는 동기적으로 커밋됩니다.

> [!NOTE]
> 구성 전용 복제본이 있는 가용성 그룹은 SQL Server 2017 CU1의 새로운 기능입니다. 가용성 그룹의 모든 SQL Server 인스턴스는 SQL Server 2017 CU1 이상이어야 합니다. 

`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`의 기본값은 0입니다. 다음 표에서는 가용성 동작을 설명합니다. 

|가용성 동작 |고가용성 및 </br> 데이터 보호 | 데이터 보호|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|주 중단 | 자동 장애 조치(failover). 새로운 주 복제본은 읽기/쓰기입니다. | 자동 장애 조치(failover). 새로운 주 복제본을 사용자 트랜잭션에 사용할 수 없습니다. |
|보조 복제본 중단 | 주 복제본은 읽기/쓰기이고, 데이터 손실 위험에 공개됩니다(주 복제본이 실패하고 복구할 수 없는 경우). 주 복제본도 실패하는 경우 자동 장애 조치(failover)가 수행되지 않습니다. | 주 복제본을 사용자 트랜잭션에 사용할 수 없습니다. 주 복제본도 실패하는 경우 장애 조치(failover) 할 복제본이 없습니다. |
|구성 전용 복제본 중단 | 주 복제본은 읽기/쓰기입니다. 주 복제본도 실패하는 경우 자동 장애 조치(failover)가 수행되지 않습니다. | 주 복제본은 읽기/쓰기입니다. 주 복제본도 실패하는 경우 자동 장애 조치(failover)가 수행되지 않습니다. |
|동기 보조 복제본 + 구성 전용 복제본 중단| 주 복제본을 사용자 트랜잭션에 사용할 수 없습니다. 자동 장애 조치(failover)가 수행되지 않습니다. | 주 복제본을 사용자 트랜잭션에 사용할 수 없습니다. 주 복제본도 실패하는 경우 장애 조치(failover)할 복제본이 없습니다. |

<sup>\*</sup> 기본값

> [!NOTE]
> 구성 전용 복제본을 호스트하는 SQL Server 인스턴스에서 다른 데이터베이스도 호스트할 수 있습니다. 둘 이상의 가용성 그룹에 대해 구성 전용 데이터베이스로 참여할 수도 있습니다. 

## <a name="requirements"></a>요구 사항

- 구성 전용 복제본이 있는 가용성 그룹의 모든 복제본은 SQL Server 2017 CU 1 이상이어야 합니다.
- SQL Server Express를 비롯한 모든 SQL Server 버전에서 구성 전용 복제본을 호스트할 수 있습니다. 
- 가용성 그룹에는 주 복제본 외에 하나 이상의 보조 복제본이 필요합니다.
- 구성 전용 복제본은 SQL Server 인스턴스당 최대 복제본 수에 계산되지 않습니다. SQL Server Standard Edition에서는 최대 3개의 복제본이 허용되고, SQL Server Enterprise Edition에서는 최대 9개까지 허용됩니다.

## <a name="considerations"></a>고려 사항

- 가용성 그룹당 구성 전용 복제본 수는 1개 이하입니다. 
- 구성 전용 복제본은 주 복제본이 될 수 없습니다.
- 구성 전용 복제본의 가용성 모드는 수정할 수 없습니다. 구성 전용 복제본에서 동기 또는 비동기 보조 복제본으로 변경하려면 구성 전용 복제본을 제거하고 필요한 가용성 모드의 보조 복제본을 추가합니다. 
- 구성 전용 복제본은 가용성 그룹 메타데이터와 동기화됩니다. 사용자 데이터는 없습니다. 
- 주 복제본 1개와 구성 전용 복제본 1개가 있고 보조 복제본이 없는 가용성 그룹은 유효하지 않습니다. 
- SQL Server Express Edition 인스턴스에는 가용성 그룹을 만들 수 없습니다. 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>pacemaker용 SQL Server 리소스 에이전트 이해

SQL Server 2017 CTP 1.4에서는 `sys.availability_groups`에 `sequence_number`가 추가되어, Pacemaker에서 보조 복제본이 주 복제본을 기준으로 얼마나 최신 상태인지를 확인할 수 있습니다. `sequence_number`는 로컬 가용성 그룹 복제본이 얼마나 최신 상태인지를 나타내는 단조롭게 증가하는 BIGINT입니다. Pacemaker는 가용성 그룹 구성이 변경될 때마다 `sequence_number`를 업데이트합니다. 구성 변경의 예로는 장애 조치(failover), 복제본 추가, 제거 등이 있습니다. 이 번호는 주 복제본에서 업데이트된 다음, 보조 복제본에 복제됩니다. 따라서 최신 구성이 포함된 보조 복제본은 주 복제본과 시퀀스 번호가 같습니다. 

Pacemaker는 복제본 수준을 주 복제본으로 올리기로 결정한 경우 먼저 모든 복제본에 ‘수준 올리기 전’ 알림을 보냅니다. 복제본이 시퀀스 번호를 반환합니다. 그다음에 Pacemaker가 실제로 복제본 수준을 주 복제본으로 올리려고 할 때 시퀀스 번호가 모든 시퀀스 번호 중 가장 높은 경우에만 복제본 수준이 올라갑니다. 시퀀스 번호가 가장 높은 시퀀스 번호와 일치하지 않는 복제본의 수준 올리기 작업은 거부됩니다. 이 방법에서는 일련 번호가 가장 높은 복제본만 주 복제본으로 승격될 수 있으므로 데이터가 손실되지 않습니다. 

이 프로세스를 수행하려면 이전 주 복제본과 시퀀스 번호가 같고 수준을 올릴 수 있는 복제본이 하나 이상 있어야 합니다. Pacemaker 리소스 에이전트는 하나 이상의 동기 보조 복제본이 최신 상태이고 기본적으로 자동 장애 조치(failover)의 대상이 될 수 있도록 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`을 설정합니다. 각 모니터링 작업에서 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 값은 계산됩니다(필요한 경우 업데이트됨). `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 값은 ‘동기 복제본 수’를 2로 나눈 값입니다. 장애 조치(failover) 시 리소스 에이전트가 수준 올리기 전 알림에 응답하려면 (`total number of replicas` - `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 복제본)이 필요합니다. `sequence_number`가 가장 높은 복제본이 주 복제본으로 수준이 올라갑니다. 

예를 들어 가용성 그룹에 동기 복제본 3개(주 복제본 1개, 동기 보조 복제본 2개)가 있다고 가정합니다.

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`은 1입니다(3 / 2 -> 1).

- 수준 올리기 전 작업에 응답하는 데 필요한 복제본 수는 2입니다(3 - 1 = 2). 

이 시나리오에서 장애 조치(failover)가 트리거되려면 두 개의 복제본이 응답해야 합니다. 주 복제본이 중단된 후 자동 장애 조치(failover)에 성공하려면 두 보조 복제본이 모두 최신 상태여야 하고 수준 올리기 전 알림에 응답해야 합니다. 온라인 상태이고 동기화된 경우에는 시퀀스 번호가 동일합니다. 가용성 그룹이 두 복제본 중 하나의 수준을 올립니다. 보조 복제본 중 하나만 수준 올리기 전 작업에 응답할 경우 리소스 에이전트에서 응답한 보조 복제본의 sequence_number가 가장 높다고 보장할 수 없으므로 장애 조치(failover)가 트리거되지 않습니다.

> [!IMPORTANT]
> `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`이 0이면 데이터가 손실될 위험이 있습니다. 주 복제본이 중단된 동안에는 리소스 에이전트가 장애 조치(failover)를 자동으로 트리거하지 않습니다. 주 복제본이 복구될 때까지 기다리거나, `FORCE_FAILOVER_ALLOW_DATA_LOSS`를 사용하여 수동으로 장애 조치(failover)할 수 있습니다.

기본 동작을 재정의하여 가용성 그룹 리소스가 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`을 자동으로 설정하지 못하도록 방지할 수 있습니다.

다음 스크립트에서는 `<**ag1**>` 가용성 그룹의 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`을 0으로 설정합니다. 실행하기 전에 `<**ag1**>`을 가용성 그룹의 이름으로 바꿉니다.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

가용성 그룹 구성에 따라 기본값으로 되돌리려면 다음 명령을 실행합니다.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

> [!NOTE]
> 위 명령을 실행하면 주 복제본이 일시적으로 보조 복제본으로 수준이 내려간 후에 다시 올라갑니다. 리소스를 업데이트하면 모든 복제본이 중지되었다가 다시 시작됩니다. `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`의 새 값은 즉시 설정되지 않고, 복제본을 다시 시작한 후에만 설정됩니다.

## <a name="see-also"></a>참고 항목

[Linux의 가용성 그룹](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
