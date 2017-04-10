---
title: "게시자에 대한 정보 보기 및 태스크 수행(복제 모니터) | Microsoft Docs"
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
  - "게시자 [SQL Server 복제], 복제 모니터 태스크"
  - "게시자 정보 보기"
  - "게시자 [SQL Server 복제], 정보 보기"
ms.assetid: 1e777e95-377a-4de3-b965-867464aadaaf
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 게시자에 대한 정보 보기 및 태스크 수행(복제 모니터)
  복제 모니터는 선택한 게시자에 대한 정보를 표시하는 다음 탭을 제공합니다.  
  
-   **게시**  
  
     이 탭에는 선택한 게시자에 있는 모든 게시 정보가 표시됩니다.  
  
-   **구독 조사 목록**  
  
     이 탭에는 오류 또는 경고가 발생하거나 성능이 가장 낮은 선택된 게시자에서 사용 가능한 모든 게시의 구독에 대한 정보가 표시됩니다.  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]이전 버전을 실행하는 배포자의 경우 이 탭이 표시되지 않습니다.  
  
-   **에이전트** 탭  
  
     이 탭에는 모든 복제 유형에 사용되는 에이전트 및 작업에 대한 세부 정보가 표시됩니다. 이 탭에서는 각 에이전트 및 작업을 시작하고 중지할 수 있습니다.  
  
 각 탭의 옵션에 대한 자세한 내용을 보려면 오른쪽 창에서 해당 탭을 클릭한 다음 메뉴 모음에서 **도움말** 을 클릭합니다. 복제 모니터를 시작 하는 방법에 대 한 정보를 참조 하십시오. [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)합니다.  
  
### 게시자에 대한 정보를 보고 태스크를 수행하려면  
  
1.  왼쪽 창에서 게시자 그룹을 확장한 다음 해당 게시자를 클릭합니다.  
  
2.  모든 게시에 대한 정보를 보려면 **게시** 탭을 클릭합니다.  
  
3.  구독에 대한 정보를 보려면 **구독 조사 목록** 탭을 클릭합니다. 다음과 같이 이 탭에서 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다.  
  
    -   구독에 연결 된 에이전트에 대 한 자세한 정보를 보려면 해당 구독을 마우스 오른쪽 단추로 클릭 **세부 정보 보기**합니다.  
  
    -   구독 속성을 보려면 해당 구독을 마우스 오른쪽 단추로 클릭 **속성**합니다.  
  
    -   밀어넣기 구독을 동기화 하려면 해당 구독을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **동기화 시작**합니다.  
  
    -   구독을 다시 초기화 하려면 구독을 마우스 오른쪽 단추로 클릭 **구독 다시 초기화**합니다.  
  
4.  에이전트에 대한 정보를 보려면 **에이전트** 탭을 클릭합니다. 이 탭에서 다음과 같이 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다.  
  
    -   에이전트 (예: 정보 메시지 및 오류 메시지)에 대 한 자세한 정보를 보려면 에이전트를 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음에 **세부 정보 보기**합니다.  
  
    -   (예: 일정, 작업 단계 세부 정보 및 등) 에이전트를 실행 하는 작업에 대 한 자세한 정보를 보려면 에이전트를 마우스 오른쪽 단추로 클릭 **속성**합니다.  
  
    -   에이전트 프로필을 관리 하려면 에이전트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **에이전트 프로필**합니다. 자세한 내용은 참조 [복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)합니다.  
  
    -   실행 하지 않는 에이전트를 시작 하려면 에이전트를 마우스 오른쪽 단추로 클릭 **에이전트 시작**합니다.  
  
    -   실행 중인 에이전트를 중지 하려면 에이전트를 마우스 오른쪽 단추로 클릭 **에이전트 중지**합니다.  
  
## 참고 항목  
 [게시자 및 배포자 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  