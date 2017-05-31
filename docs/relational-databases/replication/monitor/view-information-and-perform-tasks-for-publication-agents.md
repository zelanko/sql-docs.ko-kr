---
title: "게시 에이전트에 대한 정보 보기 및 태스크 수행 | Microsoft 문서"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- agents [SQL Server replication], viewing information
- viewing replication agent information
- agents [SQL Server replication], tasks in Replication Monitor
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3d2896e84ecfba28325f559da8e9391315c21046
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="view-information-and-perform-tasks-for-publication-agents"></a>게시 에이전트에 대한 정보 보기 및 태스크 수행
  복제 모니터에는 선택한 게시와 연결된 에이전트에 대한 정보가 포함된 **에이전트** 탭이 있습니다. 배포 에이전트 및 병합 에이전트는 구독과 연결됩니다. 자세한 내용은 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
 이 탭에는 다음 에이전트에 대한 정보가 표시됩니다.  
  
-   스냅숏 에이전트 - 모든 게시에서 사용  
  
-   로그 판독기 에이전트 - 모든 트랜잭션 게시에서 사용  
  
-   큐 판독기 에이전트 - 지연 업데이트 구독이 활성화된 트랜잭션 게시에서 사용  
  
 이 탭의 옵션에 대한 자세한 내용을 보려면 메뉴 모음의 **도움말** 을 클릭하세요. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-publication"></a>게시와 연결된 에이전트에 대한 정보를 보고 태스크를 수행하려면  
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **에이전트** 탭을 클릭하여 에이전트에 대한 정보를 봅니다. 이 탭에서 다음과 같이 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다.  
  
    -   에이전트에 대한 자세한 정보(예: 정보 메시지 및 오류 메시지)를 보려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다.  
  
    -   에이전트를 실행하는 작업에 대한 자세한 정보(예: 일정, 자세한 작업 단계 정보 등)를 보려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
    -   에이전트에 대한 프로필을 관리하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 프로필**을 클릭합니다. 자세한 내용은 [복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)을 참조하세요.  
  
    -   실행 중이지 않은 에이전트를 시작하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 시작**을 클릭합니다.  
  
    -   실행 중인 에이전트를 중지하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 중지**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 모니터에 임계값 및 경고 설정](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)   
 [게시에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [복제 에이전트 관리](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
