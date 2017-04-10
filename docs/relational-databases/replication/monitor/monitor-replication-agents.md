---
title: "복제 에이전트 모니터링 | Microsoft Docs"
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
  - "성능 모니터링 [SQL Server 복제], 에이전트"
  - "로그 판독기 에이전트, 모니터링"
  - "복제 모니터, 에이전트"
  - "병합 에이전트, 모니터링"
  - "큐 판독기 에이전트, 모니터링"
  - "스냅숏 에이전트, 모니터링"
  - "에이전트 [SQL Server 복제], 모니터링"
  - "배포 에이전트, 모니터링"
ms.assetid: d06ed24f-82d7-4b9e-9e40-cc9780476a71
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# 복제 에이전트 모니터링
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 모니터는 복제 작업에 대한 구조적 뷰를 제공할 뿐만 아니라 특정 에이전트에서 정보를 간단하게 찾을 수 있게 해줍니다. 다음 목록에는 각 에이전트, 에이전트를 찾을 수 있는 복제 모니터의 탭 및 이러한 탭에 액세스하는 방법을 설명하는 항목에 대한 링크가 포함되어 있습니다.  
  
-   다음 에이전트는 복제 모니터에서 게시와 연결됩니다.  
  
    -   스냅숏 에이전트  
  
    -   로그 판독기 에이전트  
  
    -   큐 판독기 에이전트  
  
     탭을 통해 이러한 에이전트와 관련 된 작업 및 정보 액세스: **에이전트** (각 게시자 및 게시에 대해 사용 가능) 및 **경고** (각 게시에 대해 사용 가능). 자세한 내용은 참조 [정보 보기 및 에이전트 관련 된는 게시 및 #40;에 대 한 작업 수행 복제 모니터 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)합니다.  
  
-   다음 에이전트는 복제 모니터에서 구독과 연결됩니다.  
  
    -   배포 에이전트  
  
    -   병합 에이전트  
  
     탭을 통해 이러한 에이전트와 관련 된 작업 및 정보 액세스: **구독 조사 목록** (각 게시자에 대해 사용 가능) 또는 **모든 구독** 탭 (각 게시에 대해 사용 가능). 자세한 내용은 참조 [정보 보기 및는 에이전트 구독 관련 & #40;에 대 한 작업 수행 복제 모니터 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)합니다.  
  
## SQL Server Management Studio를 사용하여 복제 에이전트 모니터링  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 는 복제 에이전트 모니터링을 위한 다음 대화 상자를 제공합니다.  
  
-   **스냅숏 에이전트 상태 보기** (모든 게시용)  
  
-   **로그 판독기 에이전트 상태 보기** (모든 트랜잭션 게시용)  
  
-   **동기화 상태 보기** (모든 구독용;이 대화 상자에서는 배포 에이전트 및 병합 에이전트에 대 한 액세스)  
  
 복제 모니터는 각 에이전트에 대한 추가 정보를 제공하고 큐 판독기 에이전트 사용 시 해당 에이전트를 모니터링합니다. 자세한 내용은 참조 [정보 보기 및 에이전트 관련 된는 게시 및 #40;에 대 한 작업 수행 복제 모니터 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md), [정보 보기 및 게시 & #40;와 관련 된 에이전트에 대 한 작업을 수행 합니다. 복제 모니터 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md), 및 [정보 보기 및 구독 & #40;와 관련 된 에이전트에 대 한 작업을 수행 합니다. 복제 모니터 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)합니다.  
  
#### 스냅숏 에이전트 및 로그 판독기 에이전트를 모니터링하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  게시를 마우스 오른쪽 단추로 누른 **로그 판독기 에이전트 상태 보기** 또는 **스냅숏 에이전트 상태 보기**합니다.  
  
4.  **로그 판독기 에이전트 상태 보기** 또는 **스냅숏 에이전트 상태 보기** 대화 상자에서 다음을 수행하십시오.  
  
    -   에이전트 상태를 확인합니다.  
  
    -   필요에 맞게 에이전트를 시작 또는 중지합니다.  
  
    -   **모니터** 를 클릭하여 **복제 모니터**를 시작합니다.  
  
5.  **닫기**를 클릭합니다.  
  
#### 게시자에서 배포 에이전트 및 병합 에이전트를 모니터링하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  모니터링할 구독에 대한 게시를 확장합니다.  
  
4.  구독을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **동기화 상태 보기**합니다.  
  
5.  **동기화 상태 보기** 대화 상자에서 다음을 수행하십시오.  
  
    -   에이전트 상태를 확인합니다.  
  
    -   필요에 맞게 에이전트를 시작 또는 중지합니다.  
  
    -   밀어넣기 구독의 경우 **모니터** 를 클릭하여 **복제 모니터**를 시작합니다.  
  
    -   끌어오기 구독의 경우 **작업 기록 보기** 를 클릭하여 에이전트 로그의 출력을 표시하는 **로그 파일 뷰어**를 시작합니다.  
  
6.  **닫기**를 클릭합니다.  
  
#### 구독자에서 배포 에이전트 및 병합 에이전트를 모니터링하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  모니터링 하 고 클릭 하 고 싶은 구독을 마우스 오른쪽 단추로 클릭 **동기화 상태 보기**합니다.  
  
4.  **동기화 상태 보기** 대화 상자에서 다음을 수행하십시오.  
  
    -   에이전트 상태를 확인합니다.  
  
    -   필요에 맞게 에이전트를 시작 또는 중지합니다.  
  
    -   **작업 기록 보기** 를 클릭하여 에이전트 로그의 출력을 표시하는 **로그 파일 뷰어**를 시작합니다.  
  
5.  **닫기**를 클릭합니다.  
  
## 참고 항목  
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [복제 에이전트 개요](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  