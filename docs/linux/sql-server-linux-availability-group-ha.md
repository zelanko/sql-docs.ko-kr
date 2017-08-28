---
title: "SQL Server Always On 가용성 그룹 배포 방법 | Microsoft Docs"
ms.custom: 
ms.date: 06/16/2017
ms.prod: sql-linux
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 353e7cf5cef8430303e3ee6fbefc92db08f5f733
ms.contentlocale: ko-kr
ms.lasthandoff: 08/28/2017

---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 문서에서는 Linux 서버에 SQL Server Always On 가용성 그룹에 대 한 지원 되는 배포 구성을 제공 합니다. 가용성 그룹에는 고가용성 및 데이터 보호 지원합니다. 자동 실패 감지, 자동 장애 조치 및 장애 조치 후 투명 하 게 다시 연결할 고가용성을 제공합니다. 동기화 된 복제본 데이터 보호를 제공합니다. 

>[!NOTE]
>고가용성 및 데이터 보호 기능 외에도 가용성 그룹 수 재해 복구를 제공, 간 플랫폼 마이그레이션 있고 읽기 확장 합니다. 이 문서에는 주로 높은 가용성 및 데이터 보호에 대 한 구현을 설명합니다. 

Windows Server 장애 조치 클러스터링, 일반적인 구성 2 개의 동기 복제본을 사용 하는 고가용성 및 [파일 공유 감시](http://technet.microsoft.com/library/cc731739.aspx)합니다. 파일 공유 감시는 예를 들어의 동기화 상태 및 복제본의 역할이 가용성 그룹 구성-를 확인합니다. 이 구성 하면 보조 복제본에서 장애 조치 대상에 가용성 그룹에 대 한 구성 변경 내용을 확인 하 고 최신 데이터를 선택 합니다. 

Linux 용 현재 고가용성 솔루션에는 Windows Server 장애 조치 클러스터에서 파일 공유 감시와 같은 외부 된 미러링 모니터가 적용 되지 않습니다. Windows Server 장애 조치 클러스터에 없는 경우 가용성 그룹 구성은 참여 SQL Server 인스턴스에서 master 데이터베이스에 저장 됩니다. 따라서 가용성 그룹 높은 가용성 및 데이터 보호에 대 한 동기 복제본이 3 개 이상 필요합니다. Linux 서버에 가용성 그룹을 만든 후에 클러스터 리소스를 만듭니다. 클러스터 리소스 설정을 고가용성에 대 한 구성을 결정합니다.

가용성 그룹 설계를 사용 하 여 높은 가용성, 데이터 보호에 대 한 특정 비즈니스 요구 사항을 충족 하 고 확장을 읽을를 선택 합니다.

>[!IMPORTANT]
>다음과 같은 구성을 가용성 그룹 디자인 패턴 및 각 패턴의 기능에 설명 합니다. 이러한 디자인 패턴으로 가용성 그룹에 적용 `CLUSTER_TYPE = EXTERNAL` 고가용성 솔루션에 대 한 합니다. 

디자인 패턴은 두 개의 가용성 그룹 구성. 구성은 다음과 같습니다.

- **세 개의 동기 복제본**

- **2 개의 동기 복제본**

## <a name="how-the-configuration-affects-default-resource-settings"></a>구성 기본 리소스 설정에 미치는 영향

클러스터 리소스 설정을 `required_synchronized_secondaries_to_commit` 주 복제본에서 트랜잭션을 커밋하기 전에 각 트랜잭션 로그를 보조 복제본의 최소 수에 작성 되도록 보장 합니다. 이 설정은 높은 가용성 및 구성에 따라 데이터 보호에 영향을 줄 수 있습니다. SQL Server 리소스 에이전트-를 설치할 때 `mssql-server-ha` -가용성 그룹에 대 한 클러스터 리소스를 만듭니다, 클러스터 관리자에서 사용 가능 여부를 검색 하 고 그룹 구성 및 설정 `required_synchronized_secondaries_to_commit` 적절 하 게 합니다. 

리소스 에이전트 매개 변수 구성에 의해 지원 되는 경우 `required_synchronized_secondaries_to_commit` 높은 가용성 및 데이터 보호를 제공 하는 값으로 설정 됩니다. 자세한 내용은 참조 [pacemaker에 대 한 SQL Server 이해 리소스 에이전트](#pacemakerNotify)합니다.

다음 섹션에서는 클러스터 리소스에 대 한 기본 동작을 설명 합니다. 

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>세 개의 동기 복제본

이 구성은 세 개의 동기 복제본이 됩니다. 기본적으로 높은 가용성 및 데이터 보호를 제공합니다. 읽기 확장을 제공할 수도 있습니다.

![세 개의 복제본][3]

다음 표에서 세 개의 동기 복제본이 포함 된 가용성 그룹에 대 한 설정에 따라의 높은 가용성 및 데이터 보호 동작을 설명 합니다. 

|`required_synchronized_secondaries_to_commit`|0 |1 \*|2
| --- |:---:|:---:|:---:
|자동 장애 조치 후 주 복제본 중단| |✔| 
|하나의 보조 복제본 중단 후 사용 가능한 주 복제본|✔|✔| 
|두 개의 보조 복제본의 작동 중단 후 사용 가능한 주 복제본|✔| |
|수동 장애 조치 후 데이터가 손실 될 수-주 복제본 중단|✔| | 

\*기본 가용성 그룹에 클러스터 리소스로 추가 되 면을 설정 합니다.

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>2 개의 동기 복제본

이러한 구성을 통해 데이터 보호 합니다. 다른 가용성 그룹 구성와 같은 읽기 확장 가능 합니다. 2 개의 동기 복제본 구성 자동 고가용성을 제공 하지 않습니다. 

![2 개의 동기 복제본][1]

이 구성은 두 서버가 필요 합니다. 이러한 서버는 주 복제본과 보조 복제본의 역할을 입력합니다. 

데이터에 대 한 최적화 된 2 개의 동기 복제본 구성을 보호 하 고 데이터베이스에 대 한 읽기 작업을 배포 합니다. 기본적으로 리소스는 데이터 보호를 위해 구성 됩니다. 이 구성의 SQL Server의 인스턴스 하나가 실패 하면 데이터베이스를 완전 하 게 사용할 수 없는 경우 또는 데이터 손실의 위험이 때문에 고가용성을 제공 하지 않습니다. 

다음 표에서 2 개의 동기 복제본이 포함 된 가용성 그룹에 대 한 가능한 값에 따라 데이터 보호 동작을 설명합니다. 

|`required_synchronized_secondaries_to_commit`|0 \*|1. 
| --- |:---|:---
|자동 장애 조치 후 주 복제본 중단| |✔ \*\* | 
|주 복제본을 보조 복제본 중단 이후에 사용 가능|✔| |

\*기본 가용성 그룹에 클러스터 리소스로 추가 되 면을 설정 합니다.

\*\*이 구성에서는 한 후 주 복제본 중단이 발생 가용성 그룹 자동 장애 조치 합니다. 응용 프로그램은 주 복제본이 온라인-이제 보조 복제본으로 가용성 그룹에 연결할 수 없습니다. 

두 서버에 SQL Server의 두 인스턴스만 필요 하기 때문에 2 개의 동기 복제본 구성 가장 경제적 수 있습니다.

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>SQL Server 리소스 에이전트 pacemaker에 대 한 이해

SQL Server 2017 CTP 1.4 추가 `sequence_number` 를 `sys.availability_groups` Pacemaker 얼마나 최신 보조 데이터베이스를 식별할 수 있도록 복제본은 주 복제본과 합니다. `sequence_number`가 로컬 가용성 그룹 복제본을 얼마나 최신 상태 인지를 나타내는 단조 증가 BIGINT는입니다. Pacemaker 업데이트는 `sequence_number` 각 가용성 그룹 구성 변경 합니다. 구성 변경의 예로 장애 조치, 복제본 추가 또는 제거를 들 수 있습니다. 수는 주 서버, 업데이트 한 다음 보조 복제본에 복제 합니다. 따라서 최신 구성을 포함 하는 보조 복제본에 주 동일한 시퀀스 번호가 있습니다. 

먼저 보냅니다 Pacemaker를 주 복제본을 결정 하는 경우는 *미리 승격* 모든 복제본에는 알림입니다. 복제본의 시퀀스 번호를 반환합니다. 다음으로 Pacemaker 실제로 주 복제본을 하려고 복제본만 승격 자체의 시퀀스 번호가 가장 높은 모든 시퀀스 번호의 경우 합니다. 고유한 시퀀스 번호가 가장 높은 시퀀스 번호와 일치 하지 않으면 복제본 수준 올리기 작업을 거부 합니다. 이 방법에서는 일련 번호가 가장 높은 복제본만 주 복제본으로 승격될 수 있으므로 데이터가 손실되지 않습니다. 

이 프로세스는 이전 주 데이터베이스에 동일한 시퀀스 번호가 가장 프로 모션 사용할 수 있는 복제본이 하나 이상 필요합니다. Pacemaker 리소스 에이전트 집합 `required_synchronized_secondaries_to_commit` 되도록 동기 보조 복제본이 하나 이상가 기본적으로 자동 장애 조치의 대상이 될 수 있는 최신 상태입니다. 각 모니터링 작업의 값으로 `required_synchronized_secondaries_to_commit` 계산 (및 필요한 경우 업데이트) 합니다. `required_synchronized_secondaries_to_commit` 값은 '동기 복제본의 숫자' 2로 나눈 값입니다. 리소스 에이전트 장애 조치 시 필요 (`total number of replicas`  -  `required_synchronized_secondaries_to_commit` 복제본)에 응답 하는 미리 알림을 승격 합니다. 순위가 가장 높은 복제본 `sequence_number` primary로 승격 됩니다. 

예를 들어 세 개의 동기 복제본-하나의 주 복제본과 2 개의 동기 보조 복제본으로 가용성 그룹입니다.

- `required_synchronized_secondaries_to_commit`1 이며, (3 / 2-1 >).

- 필요한 수의 작업을 미리 승격에 응답 하는 복제본은 2입니다. (3-1 = 2). 

이 시나리오에서는 두 개의 복제본 시작 옵션으로 장애 조치에 대 한 응답 해야 합니다. 성공의 자동 장애 조치는 주 복제본 중지 한 후 보조 복제본을 모두를 최신 상태로 유지할 수 한에 응답 해야는 미리 알림을 승격 합니다. 온라인 상태이 고 동기 인 경우 시퀀스 번호가 같은 있는데 가용성 그룹 둘 중 하나를 승격합니다. 경우에 보조 복제본 중 하나에 응답 하는 작업을 미리 승격 리소스 에이전트 응답 보조가 가장 높은 sequence_number 및 장애 조치는 트리거되지 않습니다 보장할 수 없습니다.

>[!IMPORTANT]
>`required_synchronized_secondaries_to_commit`이 0이면 데이터가 손실될 위험이 있습니다. 주 복제본 비활성 동안 리소스 에이전트가 자동으로 장애 조치를 트리거하지 않습니다. 를 복구 하려면 기본에 대 한 대기 하거나 수동으로 장애 조치를 사용 하 여 `FORCE_FAILOVER_ALLOW_DATA_LOSS`합니다.

기본 동작을 재정의 하 고 설정에서 가용성 그룹 리소스를 방지 하도록 선택할 수 있습니다 `required_synchronized_secondaries_to_commit` 자동으로 합니다.

다음 스크립트 집합 `required_synchronized_secondaries_to_commit` 이라는 가용성 그룹에 있는 0에 `<**ag1**>`합니다. Replace를 실행 하기 전에 `<**ag1**>` 가용성 그룹의 이름으로 합니다.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

실행 하는 가용성 그룹 구성에 따라 기본값 되돌리려면:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>이전 명령을 실행 하면 주 일시적으로 강등 차, 한 다음 다시 승격 합니다. 리소스 업데이트 하면 모든 복제본 중지 했다가 다시 시작 합니다. 에 대 한 새 값`required_synchronized_secondaries_to_commit` 은 복제본 다시 시작 되 고 즉시 하지 되 면만 설정 됩니다.

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
