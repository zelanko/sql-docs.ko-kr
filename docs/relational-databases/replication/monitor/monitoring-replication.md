---
title: "모니터링(복제) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "성능 모니터링 [SQL Server 복제], 복제 모니터링 정보"
  - "트랜잭션 복제, 모니터링"
  - "모니터링 [SQL Server 복제]"
  - "병합 복제 모니터링 [SQL Server 복제]"
  - "스냅숏 복제 [SQL Server], 모니터링"
  - "복제 [SQL Server], 모니터링"
  - "복제 관리, 모니터링"
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 모니터링(복제)
  복제 토폴로지의 모니터링은 복제 배포의 중요한 부분입니다. 복제 작업이 배포되므로 복제에 관련된 모든 컴퓨터에서 활동 및 상태를 추적해야 합니다. 다음 도구를 사용하여 복제를 모니터링할 수 있습니다.  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 모니터  
  
     복제 모니터는 복제를 모니터링하기 위한 가장 중요한 도구이며 모두 복제 작업을 게시자 관점으로 볼 수 있도록 합니다. 자세한 내용은 [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)을 참조하세요.  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]  
  
     [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 는 복제 모니터에 대한 액세스를 제공합니다. 또한 로그 판독기 에이전트, 스냅숏 에이전트, 병합 에이전트 및 배포 에이전트에 의해 기록된 현재 상태 및 마지막 메시지를 보고 각 에이전트를 시작 및 중지할 수 있도록 합니다. 자세한 내용은 [Monitor Replication Agents](../../../relational-databases/replication/monitor/monitor-replication-agents.md)을 참조하세요.  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] 및 복제 관리 개체 (RMO)  
  
     두 인터페이스 모두 배포자의 모든 복제 유형을 모니터링할 수 있도록 합니다. 또한 병합 복제는 구독자의 복제를 모니터링하는 기능을 제공합니다.  
  
-   복제 에이전트 이벤트에 대한 경고  
  
     복제는 복제 에이전트 이벤트에 대해 미리 정의된 다양한 경고를 제공하고 필요한 경우 추가 경고를 만들 수 있습니다. 경고를 사용하여 이벤트에 대한 자동 응답을 수행하거나 관리자에게 이벤트 상태를 알릴 수 있습니다. 자세한 내용은 참조 [복제 에이전트 이벤트에 대 한 경고를 사용 하 여](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)합니다.  
  
-   시스템 모니터  
  
     시스템 모니터는 복제에 대한 카운터 수를 제공하여 성능을 모니터링하는 데 유용할 수 있습니다. 자세한 내용은 [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md)을 참조하세요.  
  
## 참고 항목  
 [관리 및 #40입니다. 복제 및 #41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [최선의 복제 관리 방법](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  