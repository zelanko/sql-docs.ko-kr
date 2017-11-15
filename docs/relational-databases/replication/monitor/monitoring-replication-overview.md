---
title: "복제 모니터링 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- Replication Monitor, about Replication Monitor
ms.assetid: 81f596d2-27a5-489d-bf8d-0f4361decd02
caps.latest.revision: "37"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 47eb736bd150252f9081184ba589b8033b750c7f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="monitoring-replication-overview"></a>모니터링(복제)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Monitor is a graphical tool that allows you to monitor the overall health of a replication topology. 복제 모니터는 다음과 같은 일반적인 질문에 대한 답을 제공하는 게시 및 구독의 상태와 성능에 대한 자세한 정보를 제공합니다.  
  
-   복제 시스템이 정상적으로 작동 중인가?  
  
-   어떤 구독이 느린가?  
  
-   트랜잭션 구독이 얼마나 오래 되었나?  
  
-   트랜잭션 복제 시 지금 커밋된 트랜잭션이 구독자에 도달하기까지 얼마나 걸리는가?  
  
-   내 병합 구독이 왜 느린가?  
  
-   에이전트가 실행되지 않는 이유는 무엇인가?  
  
 복제를 모니터링하려면 사용자가 배포자에서 **sysadmin** 고정 서버 역할의 멤버이거나 배포 데이터베이스에서 **replmonitor** 고정 데이터베이스 역할의 멤버여야 합니다. 시스템 관리자는 사용자를 **replmonitor** 역할에 추가할 수 있으며 이렇게 하면 해당 사용자가 복제 모니터에서 복제 작업을 볼 수 있습니다. 이때 사용자가 복제를 관리할 수는 없습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에서는 복제 모니터 기능에 대한 정보를 제공합니다.  
  
 [복제 모니터 인터페이스 개요](../../../relational-databases/replication/monitor/overview-of-the-replication-monitor-interface.md)  
 복제 모니터에 있는 각 창과 탭을 설명하고 위에 나열된 질문의 답을 얻는 방법에 대한 정보를 제공합니다.  
  
 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)  
 복제 모니터를 시작하는 방법에 대해 설명합니다.  
  
 [비관리자의 복제 모니터 사용 허용](../../../relational-databases/replication/monitor/allow-non-administrators-to-use-replication-monitor.md)  
 관리자가 아닌 사용자에게 복제 모니터를 사용할 수 있도록 사용 권한을 할당하는 방법에 대해 설명합니다.  
  
 [복제 모니터에서 게시자 추가 및 제거](../../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md)  
 복제 모니터에서 게시자를 추가하거나 제거하는 방법에 대해 설명합니다.  
  
 [복제 모니터에서 데이터 새로 고침](../../../relational-databases/replication/monitor/refresh-data-in-replication-monitor.md)  
 복제 모니터에서 데이터를 새로 고치는 방법에 대해 설명합니다.  
  
 [복제 모니터로 성능 모니터링](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)  
 성능 임계값 설정에 대한 정보를 비롯하여 복제 모니터에서 성능을 모니터링하는 방법을 설명합니다. 자세한 처리 내용을 제공하는 병합 복제의 아티클 수준 통계에 대한 정보도 들어 있습니다.  
  
 [트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
 트랜잭션 복제 토폴로지의 성능을 측정할 수 있는 추적 프로그램 토큰을 설명합니다.  
  
 [복제 에이전트 모니터링](../../../relational-databases/replication/monitor/monitor-replication-agents.md)  
 각 복제 에이전트에 대한 정보를 찾는 방법을 설명합니다.  
  
 [복제 모니터에 임계값 및 경고 설정](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
 복제 모니터에서 설정할 수 있는 경고 및 임계값을 설명합니다. 토폴로지에 대한 경고를 활성화하여 상태 및 성능 정보를 적시에 받아보는 것이 좋습니다.  
  
 [캐싱, 새로 고침 및 복제 모니터 성능](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)  
 복제 모니터가 성능 향상을 위해 데이터 및 계산을 캐시하는 방법을 설명하고 사용자 인터페이스의 새로 고침이 캐시의 새로 고침과 어떻게 관련되는지를 설명합니다.  
  
 [복제 모니터에서 게시 및 구독 상태 보기](../../../relational-databases/replication/monitor/view-publication-and-subscription-status-in-replication-monitor.md)  
 복제 모니터를 사용하여 게시 또는 구독 상태 정보를 보는 방법에 대해 설명합니다.  
  
 [게시자에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)  
 복제 모니터를 사용하여 게시자에 대한 정보를 보고 태스크를 수행하는 방법에 대해 설명합니다.  
  
 [게시에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)  
 복제 모니터를 사용하여 게시에 대한 정보를 보고 태스크를 수행하는 방법에 대해 설명합니다.  
  
 [게시 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)  
 복제 모니터를 사용하여 게시와 관련된 에이전트에 대한 정보를 보고 태스크를 수행하는 방법에 대해 설명합니다.  
  
 [구독에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)  
 복제 모니터를 사용하여 구독에 대한 정보를 보고 태스크를 수행하는 방법에 대해 설명합니다.  
  
 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)  
 복제 모니터를 사용하여 구독과 관련된 에이전트에 대한 정보를 보고 태스크를 수행하는 방법에 대해 설명합니다.  
  
  
