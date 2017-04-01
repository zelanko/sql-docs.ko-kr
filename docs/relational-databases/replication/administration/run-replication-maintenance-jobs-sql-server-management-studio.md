---
title: "복제 유지 관리 작업 실행(SQL Server Management Studio) | Microsoft Docs"
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
  - "작업 [SQL Server 복제]"
ms.assetid: 0dc485a0-5a50-41eb-a29d-f2b2fb920174
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 복제 유지 관리 작업 실행(SQL Server Management Studio)
  복제는 다음 유지 관리 작업을 사용합니다.  
  
-   **데이터 유효성 검사에 실패한 구독 다시 초기화**  
  
-   **에이전트 기록 정리: 배포**  
  
-   **배포에 대한 복제 모니터링 리프레셔**  
  
-   **복제 에이전트 점검**  
  
-   **배포 기록 정리: 배포**  
  
-   **만료된 구독 정리**  
  
 이러한 작업의 시작 및 중지는 **작업** 폴더에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 에서 **에이전트** 복제 모니터의 탭 합니다. 복제 모니터를 시작 하는 방법에 대 한 정보를 참조 하십시오. [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)합니다. 각 작업의 속성 보기 및 수정 된 **작업 속성-\< 작업>** 동일한 폴더와 탭에서 사용할 수 있는 대화 상자입니다.  
  
### Management Studio에서 복제 유지 관리 작업을 시작하거나 중지하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **작업** 폴더를 확장합니다.  
  
3.  작업을 마우스 오른쪽 단추로 누른 **작업 시작** 또는 **작업 중지**합니다.  
  
### 복제 모니터에서 복제 유지 관리 작업을 시작하거나 중지하려면  
  
1.  복제 모니터에서 게시자 그룹을 확장한 다음 해당 게시자를 선택합니다.  
  
2.  **에이전트** 탭을 클릭합니다.  
  
3.  표에서 작업을 마우스 오른쪽 단추로 누른 **작업 시작** 또는 **작업 중지**합니다.  
  
### Management Studio에서 복제 유지 관리 작업의 속성을 보고 수정하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **작업** 폴더를 확장합니다.  
  
3.  작업을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **속성**합니다.  
  
4.  에 **작업 속성-\< 작업>** 대화 상자에서 필요한 경우 모든 속성을 수정 하 고 클릭 한 다음 **확인**합니다.  
  
### 복제 모니터에서 복제 유지 관리 작업의 속성을 보고 수정하려면  
  
1.  복제 모니터에서 게시자 그룹을 확장한 다음 해당 게시자를 선택합니다.  
  
2.  **에이전트** 탭을 클릭합니다.  
  
3.  표에서 작업을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **속성**합니다.  
  
4.  에 **작업 속성-\< 작업>** 대화 상자에서 필요한 경우 모든 속성을 수정 하 고 클릭 한 다음 **확인**합니다.  
  
## 참고 항목  
 [시작 및 중지 복제 에이전트 & #40입니다. SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [정보 보기 및 게시자 및 #40;에 대 한 작업을 수행 합니다. 복제 모니터 & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [복제 에이전트 관리](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  