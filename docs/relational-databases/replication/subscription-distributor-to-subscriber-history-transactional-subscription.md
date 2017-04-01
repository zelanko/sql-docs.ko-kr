---
title: "구독, 배포자에서 구독자로의 연결 기록(트랜잭션 구독) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.subscription.disttosub.f1"
ms.assetid: 1aad5b82-592e-4907-92f7-b90794175be5
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 구독, 배포자에서 구독자로의 연결 기록(트랜잭션 구독)
  **배포자에서 구독자로의 연결 기록** 탭은 상태, 기록, 정보 메시지, 모든 오류 메시지 등 배포 에이전트에 대한 자세한 정보를 표시합니다.  
  
## 옵션  
 **보기** 메뉴에서 보려는 배포 에이전트 세션을 선택한 다음 **배포 에이전트의 세션**표에서 특정 세션을 선택합니다. **선택한 세션의 동작**표에 이 세션에 대한 자세한 정보가 표시됩니다. 선택한 세션이 오류로 인해 종료될 경우 **선택한 세션에 대한 오류 정보 또는 메시지** 라는 텍스트 영역 또한 표시됩니다.  
  
 **보기**  
 확인할 배포 에이전트 세션을 선택합니다. 배포 에이전트는 일반적으로 계속 실행되므로 확인할 세션이 하나만 있을 수 있습니다.  
  
 **상태**  
 배포 에이전트의 상태입니다. 다음 목록에서는 가능한 상태 값을 보여 줍니다.  
  
-   오류  
  
-   완료  
  
-   다시 시도 중  
  
-   실행 중  
  
 **Start Time**  
 세션의 시작 시간입니다.  
  
 **종료 시간**  
 세션의 종료 시간입니다. 에이전트가 중지되지 않은 경우 이 필드는 비어 있습니다.  
  
 **기간**  
 이 세션에서 배포 에이전트가 실행된 시간입니다. 에이전트가 현재 실행되고 있는 경우 이 시간은 경과된 시간을 나타내고 에이전트 세션이 종료된 경우에는 총 세션 시간을 나타냅니다.  
  
 **오류 메시지**  
 세션이 오류로 인해 종료된 경우 이 필드는 배포 에이전트가 기록한 마지막 오류 메시지를 표시합니다. 세션이 오류 없이 종료된 경우에는 필드가 비어 있습니다.  
  
 **동작 메시지**  
 선택한 세션 중에 배포 에이전트가 기록한 모든 정보 메시지 및 오류 메시지입니다.  
  
 **동작 시간**  
 에 설명 된 작업을 시간은 **동작 메시지** 열 수행 되었습니다.  
  
 **선택한 세션에 대한 오류 정보 또는 메시지**  
 선택한 세션의 값을 표시 하는 경우에 표시 **오류** 에 **상태** 열입니다. 이 텍스트 영역은 오류 발생 시 시도한 명령과 자세한 오류 정보를 표시합니다. 오류와 관련된 추가 내용으로 연결되는 링크도 포함되어 있습니다.  
  
## 참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [정보 보기 및 구독 & #40;와 관련 된 에이전트에 대 한 작업을 수행 합니다. 복제 모니터 & #41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [복제 에이전트 개요](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  