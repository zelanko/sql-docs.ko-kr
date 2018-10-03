---
title: SQL Server Always On 가용성 그룹 배포 패턴 | Microsoft Docs
ms.custom: sql-linux
ms.date: 10/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: linux
ms.topic: conceptual
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 22178bb26309bba1529189e728bde3e5a26bab0e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798941"
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux 서버의 SQL Server Always On 가용성 그룹에 대 한 지원 되는 배포 구성을 표시합니다. 가용성 그룹에는 고가용성 및 데이터 보호 지원합니다. 자동 실패 감지, 자동 장애 조치 및 장애 조치 후 투명 하 게 다시 연결할 고가용성을 제공 합니다. 동기화 된 복제본 데이터 보호를 제공합니다. 

에 서버 장애 조치 클러스터 (WSFC (Windows), 고가용성에 대 한 일반적인 구성을 사용 하 여 두 개의 동기 복제본 및 세 번째 서버 또는 파일 공유 쿼럼 제공. 파일 공유 감시를 예를 들어 가용성 그룹 구성-복제본의 역할 및 동기화의 상태를 확인합니다. 이 구성 되도록 보조 복제본으로 장애 조치 대상에 가용성 그룹에 대 한 구성 변경 내용을 확인 하 고 최신 데이터를 선택 합니다. 

WSFC는 가용성 그룹 복제본 및 파일 공유 미러링 모니터 서버 간의 장애 조치 중재에 대 한 구성 메타 데이터를 동기화합니다. 가용성 그룹을 WSFC에 없는 경우 SQL Server 인스턴스에 master 데이터베이스에서 구성 메타 데이터를 저장 합니다.

예를 들어 Linux 클러스터에서 가용성 그룹에 `CLUSTER_TYPE = EXTERNAL`입니다. 없는 WSFC 장애 조치를 조정 하지 있습니다. 이 경우 구성 메타 데이터를 관리 되 고 SQL Server 인스턴스에 의해 유지 관리 합니다. 이 클러스터에 미러링 모니터 서버가 없기 이기 때문에 세 번째 SQL Server 인스턴스 구성 상태 메타 데이터를 저장할 필요 합니다. 함께 모든 세 개의 SQL Server 인스턴스가 클러스터에 대 한 분산 된 메타 데이터 저장소를 제공합니다. 

클러스터 관리자의 가용성 그룹에서 SQL Server 인스턴스의 쿼리하고 고가용성을 유지 하기 위해 장애 조치를 오케스트레이션 할 수 있습니다. Linux 클러스터에서 Pacemaker는 클러스터 관리자를 사용 합니다. 

사용 하 여 가용성 그룹에 대 한 고가용성을 활성화 하는 SQL Server 2017 CU 1 `CLUSTER_TYPE = EXTERNAL` 두 동기 복제 및 구성 전용 복제본에 대 한 합니다. SQL Server Express edition 포함 하 여 모든 버전의 SQL Server 2017 CU1 또는 나중에 구성 전용 복제본을 호스팅할 수 있습니다. 구성 전용 복제본 master 데이터베이스에서 가용성 그룹에 대 한 구성 정보를 유지 관리 하지만 가용성 그룹에서 사용자 데이터베이스를 포함 하지 않습니다. 

## <a name="how-the-configuration-affects-default-resource-settings"></a>구성을 기본 리소스 설정에 미치는 영향

SQL Server 2017 소개를 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 클러스터 리소스 설정이 있습니다. 이 설정은 트랜잭션 데이터는 주 복제본에 각 트랜잭션을 커밋하기 전에 로그 지정된 된 개수의 보조 복제본의 쓰기를 보장 합니다. 외부 클러스터 관리자를 사용 하면이 설정은 높은 가용성 및 데이터 보호에도 영향을 줍니다. 기본값 설정에 대 한 클러스터 리소스를 만들 때 아키텍처에 따라 달라 집니다. -SQL Server 리소스 에이전트를 설치할 때 `mssql-server-ha` -가용성 그룹에 대 한 클러스터 리소스 만들기, 클러스터 관리자를 검색 된 가용성 그룹 구성 및 설정 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 적절 하 게 합니다. 

리소스 에이전트 매개 변수 구성에 의해 지원 되는 경우 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 높은 가용성 및 데이터 보호를 제공 하는 값으로 설정 됩니다. 자세한 내용은 [pacemaker 용 SQL Server 이해 리소스 에이전트](#pacemakerNotify)합니다.

다음 섹션에서는 클러스터 리소스에 대 한 기본 동작을 설명 합니다. 

고가용성, 데이터 보호 및 읽기-배율에 대 한 특정 비즈니스 요구 사항을 충족 하도록 가용성 그룹 디자인을 선택 합니다.

다음 구성을 가용성 그룹 디자인 패턴 및 각 패턴의 기능을 설명합니다. 이러한 디자인 패턴 사용 하 여 가용성 그룹에 적용할 `CLUSTER_TYPE = EXTERNAL` 고가용성 솔루션에 대 한 합니다. 

- **세 개의 동기 복제본**
- **두 개의 동기 복제본**
- **두 개의 동기 복제본 및 구성 전용 복제본**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>동기 복제본 3

이 구성은 세 개의 동기 복제본으로 구성 됩니다. 기본적으로 높은 가용성 및 데이터 보호를 제공합니다. 읽기-배율을 제공할 수도 있습니다.

![세 개의 복제본][3]

가용성 그룹 동기 복제본 3 개 읽기-배율, 고가용성 및 데이터 보호를 제공할 수 있습니다. 다음 표에서 가용성 문제를 설명합니다. 

| |읽기-배율|고가용성 & </br> 데이터 보호 | 데이터 보호
|:---|---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>*</sup>|2
|주 중단 | 수동 장애 조치(failover). 데이터 손실이 있을 수 있습니다. 새 주 복제본은 R / W. |자동 장애 조치(failover). 새 주 복제본은 R / W. |자동 장애 조치(failover). 이전의 주 데이터베이스를 복구 하 고 보조로 가용성 그룹에 조인 될 때까지 새 기본 사용자 트랜잭션에 대 한 사용할 수 없는 경우 
|1개 보조 복제본 중단  | 기본 R은 / W. 기본 경우 자동 장애 조치가 실패 합니다. |기본 R은 / W. 기본 경우 자동 장애 조치가 실패 합니다. | 기본은 사용자 트랜잭션에 대 한 제공 되지 않습니다. 
<sup>*</sup> 기본

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>두 개의 동기 복제본

이 구성에서는 데이터 보호를 수 있습니다. 다른 가용성 그룹 구성을 같은 읽기-배율 가능 합니다. 두 개의 동기 복제본 구성을 자동 고가용성을 제공 하지 않습니다. 

![두 개의 동기 복제본][1]

두 개의 동기 복제본을 사용 하 여 가용성 그룹을 읽기-배율 및 데이터 보호를 제공합니다. 다음 표에서 가용성 문제를 설명합니다. 

| |읽기-배율 |데이터 보호
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|주 중단 | 수동 장애 조치(failover). 데이터 손실이 있을 수 있습니다. 새 주 복제본은 R / W.| 자동 장애 조치(failover). 이전의 주 데이터베이스를 복구 하 고 보조로 가용성 그룹에 조인 될 때까지 새 기본 사용자 트랜잭션에 대 한 사용할 수 없는 경우
|1개 보조 복제본 중단  |기본은 읽기/쓰기, 데이터 손실 위험에 노출 실행 합니다. |보조 복제본이 복구 될 때까지 기본 사용자 트랜잭션에 대 한 제공 되지 않습니다.
<sup>*</sup> 기본

>[!NOTE]
>앞의 시나리오에는 SQL Server 2017 CU 1 하기 전에 동작입니다. 

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>두 개의 동기 복제본 및 구성 전용 복제본

가용성 그룹 동기 복제본이 두 개 (이상) 및 구성 전용 복제본을 사용 하 여 데이터 보호를 제공 하며 고가용성을 제공할 수도 있습니다. 다음 다이어그램은이 아키텍처를 나타냅니다.

![구성 전용 가용성 그룹][2]

1. 보조 복제본에 대 한 사용자 데이터의 동기 복제 합니다. 가용성 그룹 구성 메타 데이터도를 포함 됩니다.
2. 가용성 그룹 구성 메타 데이터의 동기 복제 합니다. 사용자 데이터는 포함 되지 않습니다.

다이어그램은 가용성 그룹 주 복제본 구성 전용 복제본 및 보조 복제본에 구성 데이터를 푸시합니다. 보조 복제본은 또한 사용자 데이터를 받습니다. 구성 전용 복제본에서 사용자 데이터를 수신 하지 않습니다. 보조 복제본을 동기 가용성 모드입니다. 구성 전용 복제본에서 가용성 그룹-가용성 그룹에 대 한 메타 데이터만의 데이터베이스를 포함 하지 않습니다. 구성 전용 복제본의 구성 데이터가 동기적으로 커밋 되었습니다.

>[!NOTE]
>구성 전용 복제본을 사용 하 여 availabilility 그룹을 SQL Server 2017 CU1에 대 한 새로운 기능입니다. SQL Server 가용성 그룹의 모든 인스턴스는 SQL Server 2017 CU1 해야 이상. 

에 대 한 기본값 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 은 0입니다. 다음 표에서 가용성 문제를 설명합니다. 

| |고가용성 & </br> 데이터 보호 | 데이터 보호
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|주 중단 | 자동 장애 조치(failover). 새 주 복제본은 R / W. | 자동 장애 조치(failover). 새 기본 사용자 트랜잭션에 대 한 제공 되지 않습니다. 
|보조 복제본 중단 | 주 복제본이 읽기/쓰기를 (기본 실패 하 고 복구할 수 없는) 경우 데이터 손실 위험에 노출 실행입니다. 기본 경우 자동 장애 조치가 실패 합니다. | 기본은 사용자 트랜잭션에 대 한 제공 되지 않습니다. 장애 조치 하는 경우 주 복제본이 없는 실패 합니다. 
|구성 전용 복제본 중단 | 기본 R은 / W. 기본 경우 자동 장애 조치가 실패 합니다. | 기본 R은 / W. 기본 경우 자동 장애 조치가 실패 합니다. 
|동기 보조 + 구성만 복제본 중단| 기본은 사용자 트랜잭션에 대 한 제공 되지 않습니다. 자동 장애 조치 합니다. | 기본은 사용자 트랜잭션에 대 한 제공 되지 않습니다. 복제본이 없는 경우 장애 조치에도 기본 실패 합니다. 
<sup>*</sup> 기본

>[!NOTE]
>구성 전용 복제본을 호스팅하는 SQL Server 인스턴스의 다른 데이터베이스를 호스팅할 수도 있습니다. 이 둘 이상의 가용성 그룹에 대 한 구성만 데이터베이스로 참여할 수 있습니다. 

## <a name="requirements"></a>요구 사항

* 구성 전용 복제본을 사용 하 여 가용성 그룹의 모든 복제본에는 SQL Server 2017 CU 1 이상 이어야 합니다.
* 모든 버전의 SQL Server는 SQL Server Express를 비롯 한 구성 전용 복제본을 호스팅할 수 있습니다. 
* 가용성 그룹에 보조 복제본이 하나 이상-주 복제본 하는 것 외에도 필요합니다.
* 구성 전용 복제본 SQL Server 인스턴스당 복제본의 최대 수를 계산 되지 않습니다. 최대 3 개의 복제본을 허용 하는 SQL Server standard edition, SQL Server Enterprise Edition에는 최대 9 수 있습니다.

## <a name="considerations"></a>고려 사항

* 가용성 그룹당 둘 이상의 구성 전용 복제본입니다. 
* 구성 전용 복제본은 주 복제본 일 수 없습니다.
* 구성 전용 복제본의 가용성 모드를 수정할 수 없습니다. 구성 전용 복제본에서 동기 또는 비동기 보조 복제본을 변경 하려면 구성 전용 복제본을 제거 하 고 필요한 가용성 모드를 사용 하 여 보조 복제본을 추가 합니다. 
* 구성 전용 복제본을 가용성 그룹 메타 데이터를 사용 하 여 동기화 됩니다. 사용자 데이터가 없습니다. 
* 하나의 주 복제본 및 하나의 구성 전용 복제본에 있지만 보조 복제본을 사용 하 여 가용성 그룹 올바르지 않습니다. 
* SQL Server Express edition의 인스턴스에서 가용성 그룹을 만들 수 없습니다. 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>Pacemaker 용 SQL Server 리소스 에이전트 이해

추가 하는 SQL Server 2017 CTP 1.4 `sequence_number` 에 `sys.availability_groups` 얼마나 최신 보조 데이터베이스를 식별 하는 Pacemaker를 허용 하도록 복제본이 주 복제본을 사용 하 여 합니다. `sequence_number` 로컬 가용성 그룹 복제본이 얼마나 최신 상태 인지를 나타내는 단조롭게 증가 BIGINT입니다. Pacemaker 업데이트는 `sequence_number` 각 가용성 그룹 구성 변경 합니다. 구성 변경의 예로 장애 조치, 복제본 추가 또는 제거를 들 수 있습니다. 이 숫자는 주 서버, 업데이트 하 고 보조 복제본에 복제 합니다. 따라서 최신 구성을 포함 하는 보조 복제본에 주 동일한 시퀀스 번호입니다. 

Pacemaker를 주 복제본을 승격 하기로 하면 먼저 보냅니다를 *수준 올리기 전* 모든 복제본에는 알림입니다. 복제본에 일련 번호를 반환 합니다. 다음으로, 실제로 Pacemaker는 복제본을 주 복제본을 승격 하려고, 복제본만 수준이 올라가고 해당 시퀀스 번호가 모든 일련 번호 중 가장 높은 경우. 시퀀스 번호는 고유한 시퀀스 번호가 가장 높은 일치 하지 않는 경우 복제본에는 승격 작업이 거부 합니다. 이 방법에서는 일련 번호가 가장 높은 복제본만 주 복제본으로 승격될 수 있으므로 데이터가 손실되지 않습니다. 

이 프로세스는 이전 주 동일한 시퀀스 번호를 사용 하 여 프로 모션에 대 한 사용 가능한 복제본이 하나 이상 필요합니다. Pacemaker 리소스 에이전트 집합 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 는 동기 보조 복제본이 하나 이상 최신 이며 기본적으로 자동 장애 조치의 대상이 될 수 있습니다. 각 모니터링 작업의 값을 사용 하 여 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 계산 (및 필요한 경우 업데이트 됨). `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 값은 '동기 복제본 수' 2로 나눈 값입니다. 장애 조치 시 리소스 에이전트가 필요 (`total number of replicas`  -  `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 복제본)에 응답 하는 수준 올리기 전 알림에 합니다. 가장 높은 복제본 `sequence_number` 은 주 복제본으로 승격 합니다. 

예를 들어 동기 복제본 3-하나의 주 복제본과 두 개의 동기 보조 복제본을 사용 하 여 가용성 그룹입니다.

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 1 이며, (3-> 1 2 /).

- 필요한 복제본 수준 올리기 전 작업에 응답할 수는 2입니다. (3-1 = 2). 

이 시나리오에서는 두 개의 복제본을 장애 조치를 트리거할 수에 대 한 응답 해야 합니다. 주 복제본 중단 후 성공적으로 자동 장애 조치를 보조 복제본 모두 최신 상태 여야 하 고 응답할 해야는 수준 올리기 전 알림에 합니다. 온라인 상태이 고 동기 인 있는지 동일한 시퀀스 번호입니다. 가용성 그룹 중 하나를 승격합니다. 경우에 응답 하는 보조 복제본 중 하나는 수준 올리기 전 작업, 리소스 에이전트는 응답 하는 보조 복제본에는 가장 높은 sequence_number 및 장애 조치는 트리거되지 않습니다 보장할 수 없습니다.

>[!IMPORTANT]
>`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`이 0이면 데이터가 손실될 위험이 있습니다. 주 복제본을 작동 중단 시 리소스 에이전트가 자동으로 장애 조치를 트리거하지 않습니다. 기본 사이트를 복구에 대 한 대기 하거나 수동으로 장애 조치를 사용 하 여 `FORCE_FAILOVER_ALLOW_DATA_LOSS`입니다.

기본 동작을 재정의 하 고 설정에서 가용성 그룹 리소스를 방지 하도록 선택할 수 있습니다 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 자동으로 합니다.

다음 스크립트 집합 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 라는 가용성 그룹에는 0으로 `<**ag1**>`입니다. 실행하기 전에 `<**ag1**>`을 가용성 그룹의 이름으로 바꿉니다.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

실행 하는 가용성 그룹 구성에 따라 기본값 되돌리려면:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>이전 명령은 실행 하면 주 복제본이 일시적으로 강등 보조 다시 승격 한 다음. 리소스 업데이트 하면 모든 복제본을 중지 했다가 다시 시작 합니다. 에 대 한 새 값을`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 복제본이 다시 시작, 즉시 없습니다만 설정 됩니다.

## <a name="see-also"></a>참고자료

[Linux의 가용성 그룹](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
