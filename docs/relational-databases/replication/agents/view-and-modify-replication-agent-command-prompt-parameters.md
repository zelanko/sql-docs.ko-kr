---
title: 복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], command prompt parameters
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ed2ffecb1f73cdafcd00bf12866a852047e5e266
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516913"
---
# <a name="view-and-modify-replication-agent-command-prompt-parameters"></a>복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  복제 에이전트는 명령줄 매개 변수를 받는 실행 파일입니다. 기본적으로 에이전트는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 작업 단계에서 실행되므로 **작업 속성 - \<Job>** 대화 상자를 사용하여 이러한 매개 변수를 확인한 다음 수정할 수 있습니다. 이 대화 상자는 **의** 작업 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 폴더 및 복제 모니터의 **에이전트** 탭에서 사용할 수 있습니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
> [!NOTE]  
>  에이전트 매개 변수에 대한 변경 사항은 다음에 에이전트가 시작될 때 적용됩니다. 에이전트가 연속적으로 실행되는 경우에는 에이전트를 중단했다가 다시 시작해야 합니다.  
  
 매개 변수를 직접 수정할 수도 있지만 에이전트 프로필을 통해 수정하는 것이 일반적입니다. 자세한 내용은 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)을(를) 참조하세요.  
  
 **작업** 폴더에서 에이전트 작업에 액세스할 경우 다음 표를 사용하여 에이전트 작업 이름 및 각 에이전트에 사용 가능한 매개 변수를 확인합니다.  
  
|에이전트|작업 이름|매개 변수 목록은 다음을 참조하세요.|  
|-----------|--------------|------------------------------------|  
|스냅숏 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<integer>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|병합 게시 파티션에 대한 스냅숏 에이전트|**Dyn_\<Publisher>-\<PublicationDatabase>-\<Publication>-\<GUID>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|로그 판독기 에이전트|**\<Publisher>-\<PublicationDatabase>-\<integer>**|[복제 로그 판독기 에이전트](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|  
|끌어오기 구독에 대한 병합 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<integer>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|밀어넣기 구독에 대한 병합 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|밀어넣기 구독에 대한 배포 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>***|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|끌어오기 구독에 대한 배포 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<GUID>***\*|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|SQL Server 이외 구독자의 밀어넣기 구독에 대한 배포 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|큐 판독기 에이전트|**[\<Distributor>].\<integer>**|[Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|  
  
 \*Oracle 게시에서 밀어넣기 구독의 경우 **\<Publisher>-\<PublicationDatabase>가 아닌 **\<Publisher>-\<Publisher**>입니다.**  
  
 \*\*Oracle 게시에서 끌어오기 구독에 대한 작업 이름은 **\<Publisher>-\<PublicationDatabase>가 아닌 **\<Publisher>-\<DistributionDatabase**>입니다.**  
  
### <a name="to-view-and-modify-replication-agent-command-line-parameters-from-management-studio"></a>Management Studio에서 복제 에이전트 명령줄 매개 변수를 확인한 다음 수정하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 적절한 컴퓨터에 연결한 다음 해당 서버 노드를 확장합니다.  
  
    -   끌어오기 구독에 대한 배포 에이전트 및 병합 에이전트의 경우 구독자에 연결합니다.  
  
    -   그 외의 모든 에이전트의 경우 배포자에 연결합니다.  
  
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **작업** 폴더를 확장합니다.  
  
3.  작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **작업 속성 - \<Job>** 대화 상자의 **단계** 페이지에서 **에이전트 실행** 단계를 선택한 다음 **편집**을 클릭합니다.  
  
5.  **작업 단계 속성 - 에이전트를 실행합니다** 대화 상자에서 **명령** 필드를 편집합니다.  
  
6.  두 대화 상자에서 **확인** 을 클릭합니다.  
  
### <a name="to-view-and-modify-distribution-agent-and-merge-agent-command-line-parameters-from-replication-monitor"></a>복제 모니터에서 배포 에이전트 및 병합 에이전트 명령줄 매개 변수를 확인한 다음 수정하려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **모든 구독** 탭을 클릭합니다.  
  
3.  구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다.  
  
4.  **구독 <SubscriptionName>** 창에서 **작업**을 클릭하고 **\<AgentName> 작업 속성**을 클릭합니다.  
  
5.  **작업 속성 - \<Job>** 대화 상자의 **단계** 페이지에서 **에이전트 실행** 단계를 선택한 다음 **편집**을 클릭합니다.  
  
6.  **작업 단계 속성 - 에이전트를 실행합니다** 대화 상자에서 **명령** 필드를 편집합니다.  
  
7.  두 대화 상자에서 **확인** 을 클릭합니다.  
  
### <a name="to-view-and-modify-snapshot-agent-log-reader-agent-and-queue-reader-agent-command-line-parameters-from-replication-monitor"></a>복제 모니터에서 스냅숏 에이전트, 로그 판독기 에이전트 및 큐 판독기 에이전트 명령줄 매개 변수를 확인한 다음 수정하려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **에이전트** 탭을 클릭합니다.  
  
3.  표에서 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **작업 속성 - \<Job>** 대화 상자의 **단계** 페이지에서 **에이전트 실행** 단계를 선택한 다음 **편집**을 클릭합니다.  
  
5.  **작업 단계 속성 - 에이전트를 실행합니다** 대화 상자에서 **명령** 필드를 편집합니다.  
  
6.  두 대화 상자에서 **확인** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 에이전트 관리](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Replication Agents Overview](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
