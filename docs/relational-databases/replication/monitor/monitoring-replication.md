---
title: 모니터링(복제) | Microsoft 문서
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], about monitoring replication
- transactional replication, monitoring
- monitoring [SQL Server replication]
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
- replication [SQL Server], monitoring
- administering replication, monitoring
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: b35b7ecc21497e7b8c458b6d0e46c410f96d5d21
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68767134"
---
# <a name="monitoring-replication"></a>모니터링(복제)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  복제 토폴로지의 모니터링은 복제 배포의 중요한 부분입니다. 복제 작업이 배포되므로 복제에 관련된 모든 컴퓨터에서 활동 및 상태를 추적해야 합니다. 다양한 모니터링 도구를 사용하여 다음과 같은 일반적인 질문에 대답할 수 있습니다. 

-   복제 시스템이 정상적으로 작동 중인가?
-   어떤 구독이 느린가?
-   트랜잭션 구독이 얼마나 오래 되었나?
-   트랜잭션 복제 시 지금 커밋된 트랜잭션이 구독자에 도달하기까지 얼마나 걸리는가?
-   내 병합 구독이 왜 느린가?
-   에이전트가 실행되지 않는 이유는 무엇인가?  
  

다음 도구를 사용하여 복제를 모니터링할 수 있습니다.  
  
-   **SQL Server 복제 모니터** - 모든 복제에 대한 게시자 중심의 관점을 제공하기 위한 가장 중요한 도구입니다. 자세한 내용은 [Monitoring Replication](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)을 참조하세요. 
-   **SQL Server Management Studio** - 복제 모니터에 대한 액세스를 제공합니다. 또한 로그 판독기 에이전트, 스냅샷 에이전트, 병합 에이전트 및 배포 에이전트에 의해 기록된 현재 상태 및 마지막 메시지를 보고 각 에이전트를 시작 및 중지할 수 있도록 합니다. 자세한 내용은 [Monitor Replication Agents](../../../relational-databases/replication/monitor/monitor-replication-agents.md)을 참조하세요.  
  
-   **T-SQL(Transact-SQL) 및 RMO(복제 관리 개체)** - 두 인터페이스 모두를 사용하면 배포자에서 모든 유형의 복제를 모니터링할 수 있습니다. 또한 병합 복제는 구독자의 복제를 모니터링하는 기능을 제공합니다.  
  
-   **복제 에이전트 이벤트에 대한 경고** - 복제는 복제 에이전트 이벤트에 대해 미리 정의된 다양한 경고를 제공하고 필요한 경우 추가 경고를 만들 수 있습니다. 경고를 사용하여 이벤트에 대한 자동 응답을 수행하거나 관리자에게 이벤트 상태를 알릴 수 있습니다. 자세한 내용은 [복제 에이전트 이벤트에 대한 경고 사용](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)을 참조하세요.  
  
-   **시스템 모니터** - 복제에 대한 카운터 수를 제공하여 성능을 모니터링하는 데 유용할 수 있습니다. 자세한 내용은 [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md)을 참조하세요.  
  

## <a name="see-also"></a>참고 항목  
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   

  
  
