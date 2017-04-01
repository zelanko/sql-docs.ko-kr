---
title: "게시에 대한 정보 보기 및 태스크 수행(복제 모니터) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "게시 정보 보기"
  - "게시 [SQL Server 복제], 정보 보기"
  - "게시 [SQL Server 복제], 복제 모니터 태스크"
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 게시에 대한 정보 보기 및 태스크 수행(복제 모니터)
  복제 모니터에는 선택한 게시에 대한 정보를 포함하는 다음과 같은 탭이 있습니다.  
  
-   **모든 구독**  
  
     이 탭에는 선택한 게시에 대한 모든 구독 정보가 표시됩니다.  
  
-   **에이전트**  
  
     이 탭에는 게시에 사용되는 모든 에이전트에 대한 정보가 표시됩니다.  
  
    -   스냅숏 에이전트 - 모든 게시에서 사용  
  
    -   로그 판독기 에이전트 - 모든 트랜잭션 게시에서 사용  
  
    -   큐 판독기 에이전트 - 지연 업데이트 구독이 있는 트랜잭션 게시에서 사용  
  
-   **경고** (실행 하는 배포자에 대 한 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상)  
  
    -   이 탭에서는 에이전트에 대한 경고를 지정할 수 있습니다.  
  
-   **추적 프로그램 토큰** (트랜잭션 복제를 실행 하는 배포자에만 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상)  
  
     이 탭에서는 대기 시간(게시자에서 커밋될 트랜잭션과 구독자에서 상응하는 커밋될 트랜잭션 사이에 경과된 시간)을 측정할 수 있습니다.  
  
 각 탭의 옵션에 대한 자세한 내용을 보려면 오른쪽 창에서 해당 탭을 클릭한 다음 메뉴 모음에서 **도움말** 을 클릭합니다. 복제 모니터를 시작 하는 방법에 대 한 정보를 참조 하십시오. [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)합니다.  
  
### 게시에 대한 정보를 보고 태스크를 수행하려면  
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  보기 및 게시 속성을 수정 하려면 해당 게시를 마우스 오른쪽 단추로 클릭 **속성**합니다.  
  
3.  구독에 대한 정보를 보려면 **모든 구독** 탭을 클릭합니다.  
  
     를 확인 하 고 구독 속성을 수정할 해당 구독을 마우스 오른쪽 단추로 클릭 **속성**합니다. 이 탭에서 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다. 자세한 내용은 참조 [정보 보기 및는 에이전트 구독 관련 & #40;에 대 한 작업 수행 복제 모니터 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)합니다.  
  
4.  에이전트에 대한 정보를 보려면 **에이전트** 탭을 클릭합니다. 이 탭에서 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다. 자세한 내용은 참조 [정보 보기 및 에이전트 관련 된는 게시 및 #40;에 대 한 작업 수행 복제 모니터 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)합니다.  
  
5.  에이전트 경고 및 임계값에 대한 정보를 보려면 **경고** 탭을 클릭합니다. 자세한 내용은 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)을 참조하세요.  
  
6.  추적 프로그램 토큰에 대한 정보를 보려면 **추적 프로그램 토큰** 탭을 클릭합니다. 추적 프로그램 토큰 사용 방법은 [Measure Latency and Validate Connections for Transactional Replication](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)를 참조하십시오.  
  
## 참고 항목  
 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  