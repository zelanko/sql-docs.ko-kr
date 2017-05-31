---
title: "구독 에이전트에 대한 정보 보기 및 태스크 수행 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
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
ms.assetid: fbb59d31-2424-4552-9195-0da8d83e755f
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e6d7c3133037182042e365e852d7dc8381705e1c
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="view-information-and-perform-tasks-for-subscription-agents"></a>구독 에이전트에 대한 정보 보기 및 태스크 수행
  복제 모니터에서는 구독과 연결된 에이전트 정보에 액세스할 수 있는 두 가지 탭을 제공합니다.  
  
-   **모든 구독**  
  
     이 탭에는 선택한 게시에 대한 모든 구독 정보가 표시됩니다.  
  
-   **구독 조사 목록**  
  
     이 탭에는 오류 또는 경고가 발생하거나 성능이 가장 낮은 선택된 게시자에서 사용 가능한 모든 게시의 구독에 대한 정보가 표시됩니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]이전 버전을 실행하는 배포자의 경우 이 탭이 표시되지 않습니다.  
  
 각 탭의 옵션에 대한 자세한 내용을 보려면 오른쪽 창에서 해당 탭을 클릭한 다음 메뉴 모음에서 **도움말** 을 클릭합니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-all-subscriptions-tab"></a>구독과 연결된 에이전트에 대한 정보를 보고 태스크를 수행하려면(모든 구독 탭)  
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **모든 구독** 탭을 클릭하여 구독에 대한 정보를 봅니다. 이 탭에서 다음과 같이 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다.  
  
    -   구독과 연결된 에이전트에 대한 자세한 내용을 보려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다. 자세한 정보에는 에이전트 기록과 오류 메시지, 트랜잭션 복제에 대한 성능 통계 및 병합 복제에 대한 아티클 수준의 동기화 통계가 포함됩니다.  
  
         시작된 세부 정보 창의 탭은 구독 유형에 따라 다릅니다. 스냅숏 구독의 경우 **배포자에서 구독자로의 연결 기록**탭이고, 트랜잭션 구독의 경우 **게시자에서 배포자로의 연결 기록**탭, **배포자에서 구독자로의 연결 기록**탭 및 **배포되지 않은 명령**탭이고, 병합 구독의 경우 **동기화 기록**탭입니다.  
  
    -   밀어넣기 구독을 동기화하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 시작**을 클릭합니다.  
  
    -   구독을 다시 초기화하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 다시 초기화**를 클릭합니다.  
  
    -   단일 병합 구독의 유효성을 검사하려면 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사**를 클릭합니다. 병합 게시에 대한 모든 구독의 유효성을 검사하려면 해당 게시를 마우스 오른쪽 단추로 클릭한 다음 **모든 구독 유효성 검사**를 클릭합니다. 트랜잭션 게시에 대한 모든 구독의 유효성을 검사하려면 해당 게시를 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사**를 클릭합니다.  
  
    -   에이전트에 대한 프로필을 관리하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 프로필**을 클릭합니다. 자세한 내용은 [복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)을 참조하세요.  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-subscription-watch-list-tab"></a>구독과 관련된 에이전트에 대한 정보를 보고 태스크를 수행하려면(구독 조사 목록 탭)  
  
1.  왼쪽 창에서 게시자 그룹을 확장한 다음 해당 게시자를 클릭합니다.  
  
2.  **구독 조사 목록** 탭을 클릭하여 구독에 대한 정보를 봅니다. 이 탭에서 다음과 같이 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다.  
  
    -   구독과 연결된 에이전트에 대한 자세한 내용을 보려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다. 자세한 정보에는 에이전트 기록과 오류 메시지, 트랜잭션 복제에 대한 성능 통계 및 병합 복제에 대한 아티클 수준의 동기화 통계가 포함됩니다.  
  
         시작된 세부 정보 창의 탭은 구독 유형에 따라 다릅니다. 스냅숏 구독의 경우 **배포자에서 구독자로의 연결 기록**탭이고, 트랜잭션 구독의 경우 **게시자에서 배포자로의 연결 기록**탭, **배포자에서 구독자로의 연결 기록**탭 및 **성능**탭이고, 병합 구독의 경우 **동기화 기록**탭입니다.  
  
    -   밀어넣기 구독을 동기화하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 시작**을 클릭합니다.  
  
    -   구독을 다시 초기화하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 다시 초기화**를 클릭합니다.  
  
    -   단일 병합 구독의 유효성을 검사하려면 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사**를 클릭합니다. 병합 게시에 대한 모든 구독의 유효성을 검사하려면 해당 게시를 마우스 오른쪽 단추로 클릭한 다음 **모든 구독 유효성 검사**를 클릭합니다. 트랜잭션 게시에 대한 모든 구독의 유효성을 검사하려면 해당 게시를 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사**를 클릭합니다.  
  
    -   에이전트에 대한 프로필을 관리하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 프로필**을 클릭합니다. 자세한 내용은 [복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [구독에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
