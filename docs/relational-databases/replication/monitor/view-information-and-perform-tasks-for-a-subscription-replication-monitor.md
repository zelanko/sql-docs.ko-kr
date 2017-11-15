---
title: "구독에 대한 정보 보기 및 태스크 수행(복제 모니터) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [SQL Server replication], viewing information
- subscriptions [SQL Server replication], Replication Monitor tasks
- viewing subscription information
ms.assetid: 54aac83b-6f29-40d7-8901-cf059749867f
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dd4cf532b03adc9379084700b4296bacd64ae091
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="view-information-and-perform-tasks-for-a-subscription-replication-monitor"></a>구독에 대한 정보 보기 및 태스크 수행(복제 모니터)
  복제 모니터는 구독에 대한 정보가 들어 있는 다음 탭을 제공합니다.  
  
-   **모든 구독**  
  
     이 탭에는 선택한 게시에 대한 모든 구독 정보가 표시됩니다.  
  
-   **구독 조사 목록**  
  
     이 탭에는 오류 또는 경고가 발생하거나 성능이 가장 낮은 선택된 게시자에서 사용 가능한 모든 게시의 구독에 대한 정보가 표시됩니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]이전 버전을 실행하는 배포자의 경우 이 탭이 표시되지 않습니다.  
  
 각 탭의 옵션에 대한 자세한 내용을 보려면 오른쪽 창에서 해당 탭을 클릭한 다음 메뉴 모음에서 **도움말** 을 클릭합니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-all-subscriptions-tab"></a>모든 구독 탭의 구독에 대한 정보를 보고 태스크를 수행하려면  
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  구독에 대한 정보를 보려면 **모든 구독** 탭을 클릭합니다. '동기화 중'과 같은 특정 상태에 있는 구독만 보려면 **표시** 드롭다운 목록에서 옵션을 선택합니다.  
  
3.  구독 속성을 보고 수정하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 이 탭에서 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다. 자세한 내용은 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-subscription-watch-list-tab"></a>구독 조사 목록 탭의 구독에 대한 정보를 보고 태스크를 수행하려면  
  
1.  왼쪽 창에서 게시자 그룹을 확장한 다음 해당 게시자를 클릭합니다.  
  
2.  구독에 대한 정보를 보려면 **구독 조사 목록** 탭을 클릭합니다.  
  
3.  **\<SubscriptionType> 구독 표시** 드롭다운 목록에서 표시할 구독 유형을 선택합니다. '동기화 중'과 같은 특정 상태에 있는 구독만 보려면 **표시** 드롭다운 목록에서 옵션을 선택합니다.  
  
4.  구독 속성을 보고 수정하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 이 탭에서 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다. 자세한 내용은 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [밀어넣기 구독 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [끌어오기 구독 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
