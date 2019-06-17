---
title: 가용성 그룹이 포함된 읽기-배율 사용
description: 'Always On 가용성 그룹을 사용하는 경우 읽기-배율을 달성하는 방법에 대한 설명입니다. '
ms.custom: seodec18
ms.date: 10/24/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: ''
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 3e7c367acff65aa61e43f2ea00cde98a54d5cc94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67131820"
---
# <a name="use-read-scale-with-always-on-availability-groups"></a>Always On 가용성 그룹이 포함된 읽기-배율 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

가용성 그룹은 SQL Server에 고가용성 기능을 제공하고 통합된 확장 솔루션을 제공하는 포괄적인 솔루션입니다. 일반적인 데이터베이스 애플리케이션에서는 여러 클라이언트가 다양한 유형의 작업을 실행합니다. 경우에 따라 리소스 제약으로 인해 병목 현상이 발생할 수 있습니다. 리소스를 확보하고 OLTP 워크로드의 처리량을 높일 수 있습니다. 또한 읽기 전용 작업 부하에서 더 높은 성능과 확장성을 제공할 수 있습니다. SQL Server에 대한 가장 빠른 복제 기술을 활용하여 복제된 데이터베이스 그룹을 만들어 보고 및 분석 워크로드를 읽기 전용 복제본으로 오프로드합니다.

가용성 그룹을 사용하면 보조 데이터베이스에 대한 읽기 전용 액세스를 지원하기 위해 하나 이상의 보조 복제본을 구성할 수 있습니다.

분석 또는 보고 워크로드를 실행하는 클라이언트 애플리케이션에서 보조 데이터베이스에 직접 연결할 수 있습니다. 또한 읽기 전용 라우팅 목록을 설정하고 주 데이터베이스에 연결할 수 있습니다. 그런 다음 연결 요청을 라운드 로빈 방식으로 라우팅 목록에서 각 보조 복제본으로 전달합니다.

## <a name="read-scale-availability-groups-without-cluster"></a>클러스터가 없는 읽기-배율 가용성 그룹

[!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] 이전에는 모든 가용성 그룹에 클러스터가 필요했습니다. 클러스터는 고가용성 및 HADR(재해 복구)을 위해 비즈니스 연속성을 제공했습니다. 또한 보조 복제본은 읽기 작업에 대해 구성되었습니다. 고가용성이 목표가 아니라면 상당한 운영 오버 헤드가 클러스터 구성 및 운영에 소요되었습니다. SQL Server 2017에서는 클러스터가 없는 읽기-배율 가용성 그룹이 도입되었습니다. 

비즈니스 요구 사항이 주 복제본에서 실행되는 중요 업무용 워크로드를 위한 리소스를 절약하는 것이라면 읽기 전용 라우팅을 사용하거나 읽을 수 있는 보조 복제본에 직접 연결할 수 있습니다. 클러스터링 기술과의 통합에 의존할 필요가 없습니다. 이러한 새 기능은 Windows 및 Linux 플랫폼 모두에서 실행되는 SQL Server 2017에 사용할 수 있습니다.

>[!IMPORTANT]
>고가용성 설정이 아닙니다. 오류 검색 및 자동 장애 조치를 모니터링하고 조정할 수 있는 인프라가 없습니다. 클러스터가 없으면 SQL Server는 자동화된 고가용성 솔루션이 제공하는 낮은 RTO(복구 시간 목표)를 제공할 수 없습니다. 고가용성 기능이 필요한 경우 클러스터 관리자(Windows의 경우 Windows Server 장애 조치(Failover) 클러스터 또는 Linux의 경우 Pacemaker)를 사용합니다.
>
>읽기 확장 가용성 그룹은 재해 복구 기능을 제공할 수 있습니다. 읽기 전용 복제본이 동기 커밋 모드에 있을 경우 0의 RPO(복구 지점 목표)를 제공합니다. 읽기 확장 가용성 그룹을 장애 조치하려면 [읽기 확장 가용성 그룹에서 주 복제본 장애 조치](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md#ReadScaleOutOnly)를 참조하세요.

## <a name="use-distributed-availability-groups-for-geographic-read-scale"></a>지리적 읽기-배율에 분산 가용성 그룹 사용

지리적으로 분리된 솔루션은 분산 가용성 그룹을 사용하여 읽기-배율 솔루션을 구현할 수 있습니다. 이를 사용하면 읽기 작업의 원본에 더 가까운 사이트의 읽기 가능한 보조 복제본으로 주 복제본의 읽기 작업을 오프로드할 수 있습니다. 분산된 가용성 그룹은 주 복제본의 리소스 사용률을 줄입니다. 또한 네트워크 대기 시간을 줄이고 전용 리소스를 활용하여 읽기 처리량을 지원합니다.

단일 분산 가용성 그룹에는 최대 17개의 읽기 가능한 보조 복제본이 있을 수 있습니다. 확장된 크기 조정 기능을 위해 여러 가용성 그룹을 데이지 체인으로 연결하여 읽기 가능한 복제본의 수를 더 늘립니다. 또한 지리적으로 분산된 환경에서 짧은 대기 시간 읽기를 위해 동일한 가용성 그룹에서 두 개의 분산 가용성 그룹을 배포할 수도 있습니다.




## <a name="next-steps"></a>다음 단계

[Linux에서 읽기-배율 가용성 그룹 구성](../../../linux/sql-server-linux-availability-group-configure-rs.md)

[Windows에서 읽기-배율 가용성 그룹 구성](../../../database-engine/availability-groups/windows/configure-read-scale-availability-groups.md)

## <a name="see-also"></a>관련 항목:

 [AlwaysOn 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
