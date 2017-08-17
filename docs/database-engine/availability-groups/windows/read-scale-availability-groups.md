---
title: "읽기-배율 가용성 그룹 | Microsoft Docs"
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6dfa046a07b9fd5a3eddbe474b5ea63c1163c26c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="read-scale-availability-groups"></a>읽기-배율 가용성 그룹
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

가용성 그룹은 SQL Server를 위해 최상의 HA 기능을 제공할 뿐만 아니라 통합된 크기 조정 솔루션도 제공하는 포괄적인 솔루션입니다. 일반적인 데이터베이스 응용 프로그램에는 다양한 유형의 워크로드를 실행하는 여러 클라이언트가 있으며,리소스 제약 조건으로 인해 병목 현상을 유발할 수 있는 경우가 있습니다. 리소스를 확보하고 OLTP 워크로드에 대한 처리량을 높이거나 읽기 전용 작업에 더 높은 성능과 확장성을 제공할 수 있습니다. 이는 SQL Server에 대한 가장 빠른 복제 기술을 활용하여 달성할 수 있습니다. 즉 복제된 데이터베이스 그룹을 만들어 보고 및 분석 워크로드를 읽기 전용 복제본으로 오프로드할 수 있습니다. 

가용성 그룹을 사용하면 보조 데이터베이스에 대한 읽기 전용 액세스를 지원하기 위해 하나 이상의 보조 복제본을 구성할 수 있습니다.

분석 또는 보고 워크로드를 실행하는 클라이언트 응용 프로그램에서 보조 데이터베이스에 직접 연결할 수 있습니다. 또는 고객이 읽기 전용 라우팅 목록을 설정하고 라운드 로빈 방식으로 라우팅 목록의 보조 복제본 각각에 연결 요청을 전달하는 주 데이터베이스에 연결할 수 있습니다.

## <a name="read-scale-availability-groups-without-cluster"></a>클러스터가 없는 읽기-배율 가용성 그룹

[!INCLUDE[sssql15-md](..\..\..\includes\sssql15-md.md)] 이전에는 모든 가용성 그룹에 클러스터가 필요했습니다. 클러스터는 비즈니스 연속성, 즉 고가용성 및 HADR(재해 복구)을 제공했습니다. 또한 보조 복제본은 읽기 작업에 대해 구성할 수 있었습니다. 클러스터를 구성하고 운영하는 것은 HA가 목표가 아닌 경우 많은 운영 오버헤드로 간주되었습니다. SQL Server 2017에서는 클러스터가 없는 읽기-배율 가용성 그룹이 도입되었습니다. 

비즈니스 요구 사항이 주 복제본에서 실행되는 중요 업무용 워크로드를 위한 리소스를 절약하는 것이면, 사용자가 클러스터링 기술과의 통합에 의존하지 않고 읽기 전용 라우팅을 사용하거나 읽기 가능한 보조 복제본에 직접 연결할 수 있습니다. 이러한 새 기능은 Windows 및 Linux 플랫폼 모두에서 실행되는 SQL Server 2017에 사용할 수 있습니다.

>[!IMPORTANT]
>고가용성 설정이 아닙니다. 오류 검색 및 자동 장애 조치를 모니터링하고 조정할 수 있는 인프라가 없습니다. HADR 기능이 필요한 사용자는 클러스터 관리자(Windows의 경우 WSFC 또는 Linux의 경우 Pacemaker)를 사용하세요. 

## <a name="use-distributed-availability-groups-for-geographic-read-scale"></a>지리적 읽기-배율에 분산 가용성 그룹 사용

지리적으로 분리된 솔루션은 분산 가용성 그룹을 사용하여 읽기-배율 솔루션을 구현할 수 있습니다. 이렇게 하면 읽기 작업의 원본에 더 가까운 사이트의 읽기 가능한 보조 복제본으로 주 복제본의 읽기 작업을 오프로드할 수 있습니다. 이 경우 주 복제본의 리소스 사용률을 줄일 뿐만 아니라 네트워크 대기 시간을 줄이고 전용 리소스를 활용하여 읽기 처리량에도 도움이 됩니다.

단일 분산 가용성 그룹에는 최대 17개의 읽기 가능한 보조 복제본이 있을 수 있습니다. 확장된 크기 조정 기능을 위해 여러 가용성 그룹을 데이지 체인으로 연결하고 읽기 가능한 복제본의 수를 더 늘립니다. 또한 지리적으로 분산된 환경에서 짧은 대기 시간 읽기를 위해 동일한 가용성 그룹에서 두 개의 분산 가용성 그룹을 배포할 수도 있습니다.




## <a name="next-steps"></a>다음 단계 

[Linux에서 읽기-배율 가용성 그룹 구성](../../../linux/sql-server-linux-availability-group-configure-rs.md)

## <a name="see-also"></a>관련 항목:  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  

