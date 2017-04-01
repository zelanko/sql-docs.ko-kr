---
title: "복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정(SQL Server Management Studio) | Microsoft Docs"
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
  - "에이전트 [SQL Server 복제], 명령 프롬프트 매개 변수"
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정(SQL Server Management Studio)
  복제 에이전트는 명령줄 매개 변수를 받는 실행 파일입니다. 기본적으로 에이전트에서 실행 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 작업 단계, 이러한 매개 변수를 볼 수 있으며 사용 하 여 수정 하므로 **작업 속성-\< 작업>** 대화 상자입니다. 이 대화 상자는 **의** 작업 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 폴더 및 복제 모니터의 **에이전트** 탭에서 사용할 수 있습니다. 복제 모니터를 시작 하는 방법에 대 한 정보를 참조 하십시오. [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)합니다.  
  
> [!NOTE]  
>  에이전트 매개 변수에 대한 변경 사항은 다음에 에이전트가 시작될 때 적용됩니다. 에이전트가 연속적으로 실행되는 경우에는 에이전트를 중단했다가 다시 시작해야 합니다.  
  
 매개 변수를 직접 수정할 수도 있지만 에이전트 프로필을 통해 수정하는 것이 일반적입니다. 자세한 내용은 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)을(를) 참조하세요.  
  
 **작업** 폴더에서 에이전트 작업에 액세스할 경우 다음 표를 사용하여 에이전트 작업 이름 및 각 에이전트에 사용 가능한 매개 변수를 확인합니다.  
  
|에이전트|작업 이름|매개 변수 목록 참조|  
|-----------|--------------|------------------------------------|  
|스냅숏 에이전트|**\< 게시자>-\< PublicationDatabase>-\< 게시>-\< 정수>**|[복제 스냅숏 에이전트](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|병합 게시 파티션에 대한 스냅숏 에이전트|**Dyn_ \< 게시자>-\< PublicationDatabase>-\< 게시>-\< GUID>**|[복제 스냅숏 에이전트](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|로그 판독기 에이전트|**\< 게시자>-\< PublicationDatabase>-\< 정수>**|[복제 로그 판독기 에이전트](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|  
|끌어오기 구독에 대한 병합 에이전트|**\< 게시자>-\< PublicationDatabase>-\< 게시>-\< 구독자>-\< SubscriptionDatabase>-\< 정수>**|[복제 병합 에이전트](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|밀어넣기 구독에 대한 병합 에이전트|**\< 게시자>-\< PublicationDatabase>-\< 게시>-\< 구독자>-\< 정수>**|[복제 병합 에이전트](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|밀어넣기 구독에 대한 배포 에이전트|**\< 게시자>-\< PublicationDatabase>-\< 게시>-\< 구독자>-\< 정수>***|[복제 배포 에이전트](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|끌어오기 구독에 대한 배포 에이전트|**\< 게시자>-\< PublicationDatabase>-\< 게시>-\< 구독자>-\< SubscriptionDatabase>-\< GUID>***\*|[복제 배포 에이전트](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|SQL Server 이외 구독자의 밀어넣기 구독에 대한 배포 에이전트|**\< 게시자>-\< PublicationDatabase>-\< 게시>-\< 구독자>-\< 정수>**|[복제 배포 에이전트](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|큐 판독기 에이전트|**[\< 배포자>]. \< 정수>**|[복제 큐 판독기 에이전트](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|  
  
 \*Oracle 게시에 밀어넣기 구독의 경우 **\< 게시자>-\< 게시자**> 보다는 **\< 게시자>-\< PublicationDatabase>**  
  
 \*\*Oracle 게시에 끌어오기 구독의 경우 **\< 게시자>-\< DistributionDatabase**> 보다는 **\< 게시자>-\< PublicationDatabase>**  
  
### Management Studio에서 복제 에이전트 명령줄 매개 변수를 확인한 다음 수정하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 적절한 컴퓨터에 연결한 다음 해당 서버 노드를 확장합니다.  
  
    -   끌어오기 구독에 대한 배포 에이전트 및 병합 에이전트의 경우 구독자에 연결합니다.  
  
    -   그 외의 모든 에이전트의 경우 배포자에 연결합니다.  
  
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **작업** 폴더를 확장합니다.  
  
3.  작업을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **속성**합니다.  
  
4.  에 **단계** 의 페이지는 **작업 속성-\< 작업>** 대화 상자에서 단계를 선택 하 **에이전트를 실행**, 를 클릭 하 고 **편집**합니다.  
  
5.  에 **작업 단계 속성-에이전트 실행** 대화 상자에서 편집는 **명령** 필드입니다.  
  
6.  두 대화 상자에서 **확인** 을 클릭합니다.  
  
### 복제 모니터에서 배포 에이전트 및 병합 에이전트 명령줄 매개 변수를 확인한 다음 수정하려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **모든 구독** 탭을 클릭합니다.  
  
3.  구독을 마우스 오른쪽 단추로 누른 **세부 정보 보기**합니다.  
  
4.  에 **구독 \< SubscriptionName >** 창 클릭 **작업**, 를 클릭 하 고 **\< AgentName> 작업 속성**.  
  
5.  에 **단계** 의 페이지는 **작업 속성-\< 작업>** 대화 상자에서 단계를 선택 하 **에이전트를 실행**, 를 클릭 하 고 **편집**합니다.  
  
6.  에 **작업 단계 속성-에이전트 실행** 대화 상자에서 편집는 **명령** 필드입니다.  
  
7.  두 대화 상자에서 **확인** 을 클릭합니다.  
  
### 복제 모니터에서 스냅숏 에이전트, 로그 판독기 에이전트 및 큐 판독기 에이전트 명령줄 매개 변수를 확인한 다음 수정하려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **에이전트** 탭을 클릭합니다.  
  
3.  눈금에서 에이전트를 마우스 오른쪽 단추로 누른 **속성**합니다.  
  
4.  에 **단계** 의 페이지는 **작업 속성-\< 작업>** 대화 상자에서 단계를 선택 하 **에이전트를 실행**, 를 클릭 하 고 **편집**합니다.  
  
5.  에 **작업 단계 속성-에이전트 실행** 대화 상자에서 편집는 **명령** 필드입니다.  
  
6.  두 대화 상자에서 **확인** 을 클릭합니다.  
  
## 참고 항목  
 [복제 에이전트 관리](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [복제 에이전트 개요](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  