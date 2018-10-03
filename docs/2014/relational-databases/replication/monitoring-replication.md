---
title: 모니터링(복제) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
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
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 34d88a90890ac047913e1973b37a2a40e831dd01
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48111043"
---
# <a name="monitoring-replication"></a>모니터링(복제)
  복제 토폴로지의 모니터링은 복제 배포의 중요한 부분입니다. 복제 작업이 배포되므로 복제에 관련된 모든 컴퓨터에서 활동 및 상태를 추적해야 합니다. 다음 도구를 사용하여 복제를 모니터링할 수 있습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] Replication Monitor  
  
     복제 모니터는 복제를 모니터링하기 위한 가장 중요한 도구이며 모두 복제 작업을 게시자 관점으로 볼 수 있도록 합니다. 자세한 내용은 [복제 모니터링](monitor/monitoring-replication-overview.md)합니다.  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssManStudioFull-md.md)]  
  
     [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 는 복제 모니터에 대한 액세스를 제공합니다. 또한 로그 판독기 에이전트, 스냅숏 에이전트, 병합 에이전트 및 배포 에이전트에 의해 기록된 현재 상태 및 마지막 메시지를 보고 각 에이전트를 시작 및 중지할 수 있도록 합니다. 자세한 내용은 [Monitor Replication Agents](agents/replication-agents.md)을 참조하세요.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 RMO(복제 관리 개체)  
  
     두 인터페이스 모두 배포자의 모든 복제 유형을 모니터링할 수 있도록 합니다. 또한 병합 복제는 구독자의 복제를 모니터링하는 기능을 제공합니다.  
  
-   복제 에이전트 이벤트에 대한 경고  
  
     복제는 복제 에이전트 이벤트에 대해 미리 정의된 다양한 경고를 제공하고 필요한 경우 추가 경고를 만들 수 있습니다. 경고를 사용하여 이벤트에 대한 자동 응답을 수행하거나 관리자에게 이벤트 상태를 알릴 수 있습니다. 자세한 내용은 [복제 에이전트 이벤트에 대한 경고 사용](agents/use-alerts-for-replication-agent-events.md)을 참조하세요.  
  
-   시스템 모니터  
  
     시스템 모니터는 복제에 대한 카운터 수를 제공하여 성능을 모니터링하는 데 유용할 수 있습니다. 자세한 내용은 [Monitoring Replication with System Monitor](monitor/monitoring-replication-with-system-monitor.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [관리&#40;복제&#41;](administration/administration-replication.md)   
 [Best Practices for Replication Administration](administration/best-practices-for-replication-administration.md)   
 [복제 모니터링](monitor/monitoring-replication-overview.md)  
  
  
