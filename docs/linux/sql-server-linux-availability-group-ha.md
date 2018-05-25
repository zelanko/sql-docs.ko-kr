---
title: SQL Server Always On 가용성 그룹 배포 방법 | Microsoft Docs
ms.custom: sql-linux
ms.date: 10/16/2017
ms.prod: sql
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: linux
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 36115370063292f3a3302dac4596222bb513fb67
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux 서버에 SQL Server Always On 가용성 그룹에 대 한 지원 되는 배포 구성을 제공 합니다. 가용성 그룹에는 고가용성 및 데이터 보호 지원합니다. 자동 실패 감지, 자동 장애 조치 및 장애 조치 후 투명 하 게 다시 연결할 고가용성을 제공합니다. 동기화 된 복제본 데이터 보호를 제공합니다. 

에 장애 조치 클러스터 WSFC (Windows Server), 고가용성에 대 한 일반적인 구성에서는 2 개의 동기 복제본 및 세 번째 서버 또는 파일 공유 쿼럼에 있도록 합니다. 파일 공유 감시는 예를 들어의 동기화 상태 및 복제본의 역할이 가용성 그룹 구성-를 확인합니다. 이 구성 하면 보조 복제본에서 장애 조치 대상에 가용성 그룹에 대 한 구성 변경 내용을 확인 하 고 최신 데이터를 선택 합니다. 

WSFC는 가용성 그룹 복제본 및 파일 공유 미러링 모니터 서버 간의 장애 조치 중재에 대 한 구성 메타 데이터를 동기화합니다. 가용성 그룹 WSFC에 없는 경우 SQL Server 인스턴스의 master 데이터베이스에 구성 메타 데이터를 저장 합니다.

예를 들어 Linux 클러스터에서 가용성 그룹에 `CLUSTER_TYPE = EXTERNAL`합니다. 없는 WSFC 장애 조치를 조정 하지 않습니다. 이 경우 구성 메타 데이터 관리 되 고 SQL Server 인스턴스에 의해 유지 관리 합니다. 이 클러스터에 미러링 모니터 서버가 없는 있기 때문에 세 번째 SQL Server 인스턴스 구성 상태 메타 데이터를 저장할 필요 합니다. 함께 모든 세 개의 SQL Server 인스턴스가 클러스터에 대 한 분산 된 메타 데이터 저장소를 제공합니다. 

클러스터 관리자 가용성 그룹에서 SQL Server의 인스턴스를 쿼리 하 고 고가용성을 유지 하기 위해 장애 조치를 조정할 수 있습니다. Linux 클러스터 Pacemaker 클러스터 관리자를입니다. 

SQL Server 2017 CU 1이 있는 가용성 그룹에 대 한 고가용성을 사용 하면 `CLUSTER_TYPE = EXTERNAL` 2 개의 동기 복제본와 구성 유일한 복제 합니다. SQL Server Express edition 포함 하 여 SQL Server 2017 c u 1 이상-모든 버전에서 구성 유일한 복제본을 호스팅할 수 있습니다. 구성 유일한 복제 master 데이터베이스에서 가용성 그룹에 대 한 구성 정보를 유지 관리 하지만 가용성 그룹의 사용자 데이터베이스를 포함 하지 않습니다. 

## <a name="how-the-configuration-affects-default-resource-settings"></a>구성 기본 리소스 설정에 미치는 영향

SQL Server 2017 소개는 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 클러스터 리소스 설정이 있습니다. 이 설정은 지정된 된 수의 보조 복제본 쓰기 전에 주 복제본 커밋한 각 트랜잭션을 기록 하도록 트랜잭션 데이터를 보장 합니다. 외부 클러스터 관리자를 사용 하면 고가용성 및 데이터 보호를 모두이 설정이 적용 됩니다. 기본값 설정에 대 한 클러스터 리소스를 만들 때 아키텍처에 따라 달라 집니다. SQL Server 리소스 에이전트-를 설치할 때 `mssql-server-ha` -가용성 그룹에 대 한 클러스터 리소스를 만듭니다, 클러스터 관리자에서 사용 가능 여부를 검색 하 고 그룹 구성 및 설정 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 적절 하 게 합니다. 

리소스 에이전트 매개 변수 구성에 의해 지원 되는 경우 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 높은 가용성 및 데이터 보호를 제공 하는 값으로 설정 됩니다. 자세한 내용은 참조 [pacemaker에 대 한 SQL Server 이해 리소스 에이전트](#pacemakerNotify)합니다.

다음 섹션에서는 클러스터 리소스에 대 한 기본 동작을 설명 합니다. 

고가용성, 데이터 보호 및 읽기 확장성이에 대 한 특정 비즈니스 요구 사항을 충족 하는 가용성 그룹 디자인을 선택 합니다.

다음과 같은 구성을 가용성 그룹 디자인 패턴 및 각 패턴의 기능에 설명 합니다. 이러한 디자인 패턴으로 가용성 그룹에 적용 `CLUSTER_TYPE = EXTERNAL` 고가용성 솔루션에 대 한 합니다. 

- **세 개의 동기 복제본**
- **2 개의 동기 복제본**
- **2 개의 동기 복제본과 구성만 복제본**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>세 개의 동기 복제본

이 구성은 세 개의 동기 복제본이 됩니다. 기본적으로 높은 가용성 및 데이터 보호를 제공합니다. 읽기 규모를 제공할 수도 있습니다.

![세 개의 복제본][3]

세 개의 동기 복제본이 포함 된 가용성 그룹 읽기 확장성, 고가용성 및 데이터 보호를 제공할 수 있습니다. 다음 표에서 가용성 문제를 설명합니다. 

| |읽기 비율|고가용성 & </br> 데이터 보호 | 데이터 보호
|:---|---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>*</sup>|2
|주 중단 | 수동 장애 조치(failover). 데이터 손실이 있을 수 있습니다. 새 주 파일 그룹은 R /w |자동 장애 조치(failover). 새 주 파일 그룹은 R /w |자동 장애 조치(failover). 새로운 주 이전의 주 복구 하 고 보조로 가용성 그룹에 조인 될 때까지 사용자 트랜잭션에 사용할 수 없는 경우 
|1개 보조 복제본 중단  | 기본 R은 /w 기본 경우 자동 장애 조치가 실패 합니다. |기본 R은 /w 기본 경우 자동 장애 조치가 실패 합니다. | 기본은 사용자 트랜잭션에 대 한 공간이 없습니다. 
<sup>*</sup> 기본값

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>2 개의 동기 복제본

이러한 구성을 통해 데이터 보호 합니다. 다른 가용성 그룹 구성와 같은 읽기 확장성이 가능 합니다. 2 개의 동기 복제본 구성 자동 고가용성을 제공 하지 않습니다. 

![2 개의 동기 복제본][1]

2 개의 동기 복제본이 포함 된 가용성 그룹 읽기 규모 및 데이터 보호를 제공합니다. 다음 표에서 가용성 문제를 설명합니다. 

| |읽기 비율 |데이터 보호
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1.
|주 중단 | 수동 장애 조치(failover). 데이터 손실이 있을 수 있습니다. 새 주 파일 그룹은 R /w| 자동 장애 조치(failover). 새로운 주 이전의 주 복구 하 고 보조로 가용성 그룹에 조인 될 때까지 사용자 트랜잭션에 사용할 수 없는 경우
|1개 보조 복제본 중단  |기본 R/W, 데이터 손실에 노출 실행 중입니다. |주 보조 복구 될 때까지 사용자 트랜잭션에 사용할 수 없는 경우
<sup>*</sup> 기본값

>[!NOTE]
>위 시나리오는 SQL Server 2017 CU 1 전에 동작 합니다. 

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>2 개의 동기 복제본과 구성만 복제본

구성만 복제본과 두 개 이상의 동기 복제본이 포함 된 가용성 그룹 데이터 보호 기능을 제공 하며 고가용성도 수도 있습니다. 다음 다이어그램은이 아키텍처를 나타냅니다.

![전용 가용성 그룹 구성][2]

1. 보조 복제본에 대 한 사용자 데이터의 동기 복제 합니다. 가용성 그룹 구성 메타 데이터도를 포함 됩니다.
2. 가용성 그룹 구성 메타 데이터의 동기 복제 합니다. 사용자 데이터는 포함 되지 않습니다.

가용성 그룹 다이어그램에서 주 복제본 구성만 복제 데이터베이스와 보조 복제본에 구성 데이터를 푸시합니다. 보조 복제본은 또한 사용자 데이터를 받습니다. 구성 유일한 복제 사용자 데이터를 받지 않습니다. 보조 복제본이 동기 가용성 모드입니다. 구성 유일한 복제본 데이터베이스의 가용성 그룹-가용성 그룹에 대 한 메타 데이터만 포함 되지 않습니다. 구성만 복제본에 대 한 구성 데이터는 동기적으로 다하고 있습니다.

>[!NOTE]
>복제 구성 있는 availabilility 그룹은 SQL Server 2017 c u 1에 대 한 새로운 기능입니다. 모든 가용성 그룹에 SQL Server 인스턴스의 SQL Server 2017 c u 1 이어야 합니다. 이후 버전입니다. 

에 대 한 기본값 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 은 0입니다. 다음 표에서 가용성 문제를 설명합니다. 

| |고가용성 & </br> 데이터 보호 | 데이터 보호
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1.
|주 중단 | 자동 장애 조치(failover). 새 주 파일 그룹은 R /w | 자동 장애 조치(failover). 사용자 트랜잭션에 대 한 새로운 주 ´ ù. 
|보조 복제본의 작동 중단 | 주 파일 그룹은 R/W, (기본 실패 하 고 복구할 수 없습니다) 경우 데이터 손실에 노출 실행 합니다. 기본 경우 자동 장애 조치가 실패 합니다. | 기본은 사용자 트랜잭션에 대 한 공간이 없습니다. 장애 조치할 경우 주 복제본도 실패 합니다. 
|구성만 복제본 중단 | 기본 R은 /w 기본 경우 자동 장애 조치가 실패 합니다. | 기본 R은 /w 기본 경우 자동 장애 조치가 실패 합니다. 
|동기 보조 데이터베이스 + 구성만 복제본 중단| 기본은 사용자 트랜잭션에 대 한 공간이 없습니다. 자동 장애 조치 없습니다. | 기본은 사용자 트랜잭션에 대 한 공간이 없습니다. 복제본이 없는 경우 장애 조치가 가능 하도록 기본 실패 하 게 합니다. 
<sup>*</sup> 기본값

>[!NOTE]
>구성만 복제본을 호스팅하는 SQL Server 인스턴스의 다른 데이터베이스를 호스트할 수 있습니다. 여러 가용성 그룹에 대 한 구성만 데이터베이스로 참여할 수 있습니다. 

## <a name="requirements"></a>요구 사항

* 구성만 복제 데이터베이스와 가용성 그룹에 있는 모든 복제본에는 SQL Server 2017 CU 1 이상 이어야 합니다.
* 모든 버전의 SQL Server SQL Server Express를 포함 하 여 구성 유일한 복제본을 호스팅할 수 있습니다. 
* 가용성 그룹에 보조 복제본이 하나 이상-주 복제본 외에도 필요합니다.
* SQL Server 인스턴스당 복제본의 최대 수 복제 구성만 포함 되지 않습니다. SQL Server standard edition에서는 최대 3 개의 복제본 허용, SQL Server Enterprise Edition 최대 9를 허용 합니다.

## <a name="considerations"></a>고려 사항

* 유일한 복제본 가용성 그룹당 둘 이상의 구성 합니다. 
* 구성 유일한 복제본은 주 복제본 일 수 없습니다.
* 구성만 복제본의 가용성 모드를 수정할 수 없습니다. 구성 유일한 복제에서 동기 또는 비동기 보조 복제본을 변경 하려면 구성만 복제를 제거 하 고 필요한 가용성 모드와 보조 복제본을 추가 합니다. 
* 구성 유일한 복제본 가용성 그룹 메타 데이터와 동기화 됩니다. 사용자 데이터가 없습니다. 
* 하나의 주 복제본 및 하나의 구성만 복제본 있지만 보조 복제본이 포함 된 가용성 그룹 올바르지 않습니다. 
* SQL Server Express edition의 인스턴스에서 가용성 그룹을 만들 수 없습니다. 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>SQL Server 리소스 에이전트 pacemaker에 대 한 이해

SQL Server 2017 CTP 1.4 추가 `sequence_number` 를 `sys.availability_groups` Pacemaker 얼마나 최신 보조 데이터베이스를 식별할 수 있도록 복제본은 주 복제본과 합니다. `sequence_number` 가 로컬 가용성 그룹 복제본을 얼마나 최신 상태 인지를 나타내는 단조 증가 BIGINT는입니다. Pacemaker 업데이트는 `sequence_number` 각 가용성 그룹 구성 변경 합니다. 구성 변경의 예로 장애 조치, 복제본 추가 또는 제거를 들 수 있습니다. 수는 주 서버, 업데이트 한 다음 보조 복제본에 복제 합니다. 따라서 최신 구성을 포함 하는 보조 복제본에 주 동일한 시퀀스 번호가 있습니다. 

먼저 보냅니다 Pacemaker를 주 복제본을 결정 하는 경우는 *미리 승격* 모든 복제본에는 알림입니다. 복제본의 시퀀스 번호를 반환합니다. 다음으로 Pacemaker 실제로 주 복제본을 하려고 복제본만 승격 자체의 시퀀스 번호가 가장 높은 모든 시퀀스 번호의 경우 합니다. 고유한 시퀀스 번호가 가장 높은 시퀀스 번호와 일치 하지 않으면 복제본 수준 올리기 작업을 거부 합니다. 이 방법에서는 일련 번호가 가장 높은 복제본만 주 복제본으로 승격될 수 있으므로 데이터가 손실되지 않습니다. 

이 프로세스는 이전 주 데이터베이스에 동일한 시퀀스 번호가 가장 프로 모션 사용할 수 있는 복제본이 하나 이상 필요합니다. Pacemaker 리소스 에이전트 집합 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 되도록 동기 보조 복제본이 하나 이상가 기본적으로 자동 장애 조치의 대상이 될 수 있는 최신 상태입니다. 각 모니터링 작업의 값으로 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 계산 (및 필요한 경우 업데이트) 합니다. `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 값은 '동기 복제본의 숫자' 2로 나눈 값입니다. 리소스 에이전트 장애 조치 시 필요 (`total number of replicas`  -  `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 복제본)에 응답 하는 미리 알림을 승격 합니다. 순위가 가장 높은 복제본 `sequence_number` primary로 승격 됩니다. 

예를 들어 세 개의 동기 복제본-하나의 주 복제본과 2 개의 동기 보조 복제본으로 가용성 그룹입니다.

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 1 이며, (3 / 2-1 >).

- 필요한 수의 작업을 미리 승격에 응답 하는 복제본은 2입니다. (3-1 = 2). 

이 시나리오에서는 두 개의 복제본 시작 옵션으로 장애 조치에 대 한 응답 해야 합니다. 성공의 자동 장애 조치는 주 복제본 중지 한 후 보조 복제본을 모두를 최신 상태로 유지할 수 한에 응답 해야는 미리 알림을 승격 합니다. 온라인 상태이 고 동기 인 경우 시퀀스 번호가 같은 있는데 가용성 그룹 둘 중 하나를 승격합니다. 경우에 보조 복제본 중 하나에 응답 하는 작업을 미리 승격 리소스 에이전트 응답 보조가 가장 높은 sequence_number 및 장애 조치는 트리거되지 않습니다 보장할 수 없습니다.

>[!IMPORTANT]
>`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`이 0이면 데이터가 손실될 위험이 있습니다. 주 복제본 비활성 동안 리소스 에이전트가 자동으로 장애 조치를 트리거하지 않습니다. 를 복구 하려면 기본에 대 한 대기 하거나 수동으로 장애 조치를 사용 하 여 `FORCE_FAILOVER_ALLOW_DATA_LOSS`합니다.

기본 동작을 재정의 하 고 설정에서 가용성 그룹 리소스를 방지 하도록 선택할 수 있습니다 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 자동으로 합니다.

다음 스크립트 집합 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 이라는 가용성 그룹에 있는 0에 `<**ag1**>`합니다. 실행하기 전에 `<**ag1**>`을 가용성 그룹의 이름으로 바꿉니다.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

실행 하는 가용성 그룹 구성에 따라 기본값 되돌리려면:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>이전 명령을 실행 하면 주 일시적으로 강등 차, 한 다음 다시 승격 합니다. 리소스 업데이트 하면 모든 복제본 중지 했다가 다시 시작 합니다. 에 대 한 새 값`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 은 복제본 다시 시작 되 고 즉시 하지 되 면만 설정 됩니다.

## <a name="see-also"></a>참고 항목

[Linux에서 가용성 그룹](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
