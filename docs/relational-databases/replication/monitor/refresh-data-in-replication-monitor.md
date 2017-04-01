---
title: "복제 모니터에서 데이터 새로 고침 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "데이터 새로 고침"
ms.assetid: e9582244-7d00-45f4-be16-020a65c76a5e
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# 복제 모니터에서 데이터 새로 고침
  복제 모니터에서는 주 창 및 세부 정보 창(주 창에서 시작되는 창)을 자동으로 또는 수동으로 새로 고칠 수 있습니다. 창을 수동으로 새로 고치려면 F5 키를 누르면 됩니다. 기본적으로 주 창은 5분마다 자동으로 새로 고쳐집니다. 이러한 새로 고침 빈도는 게시자별로 사용자 지정할 수 있습니다.  
  
 복제 모니터에 표시 되는 데이터 쿼리를 캐시 합니다. 복제 모니터를 새로 고치는 중 고 캐시 간의 관계에 대 한 정보를 참조 하십시오. [캐싱, 새로 고침 및 복제 모니터 성능](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)합니다. 복제 모니터를 시작 하는 방법에 대 한 정보를 참조 하십시오. [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)합니다.  
  
### 복제 모니터에 대한 새로 고침 옵션을 설정하려면  
  
1.  복제 모니터의 왼쪽된 창에서 게시자를 마우스 오른쪽 단추로 누른 **게시자 설정**합니다.  
  
2.  **게시자 설정** 대화 상자에서 **자동 새로 고침** 및 **새로 고침 빈도** 옵션을 설정합니다. **자동 새로 고침** 설정은 복제 모니터의 주 창에 영향을 줍니다.  **새로 고침 빈도** 설정도 영향을 줌 자동으로 새로 고치도록 설정 된 모든 세부 정보 창 (만 설정 변경 하면 변경 후 열린 세부 정보 창은 영향을).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### 세부 정보 창이 자동으로 새로 고쳐지도록 지정하려면  
  
1.  다음과 같이 예를 들어  
  
    1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
    2.  **모든 구독** 탭을 클릭합니다.  
  
    3.  구독을 마우스 오른쪽 단추로 누른 **세부 정보 보기**합니다.  
  
2.  에 **구독 \< SubscriptionName>** 세부 정보 창에서 클릭 **작업**, 를 클릭 하 고 **자동 새로 고침**합니다. 새로 고침 빈도는 **게시자 설정** 대화 상자의 **새로 고침 빈도** 설정에 의해 결정됩니다.  
  
## 참고 항목  
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  