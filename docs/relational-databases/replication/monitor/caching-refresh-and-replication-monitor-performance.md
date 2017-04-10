---
title: "캐싱, 새로 고침 및 복제 모니터 성능 | Microsoft Docs"
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
  - "성능 모니터링 [SQL Server 복제], 복제 모니터링"
  - "캐시 [SQL Server], 복제"
  - "복제 모니터, 캐싱"
  - "데이터 새로 고침"
  - "복제 모니터, 새로 고침"
ms.assetid: a2d8b666-ed41-4f86-b2b8-c8e118416ab7
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# 캐싱, 새로 고침 및 복제 모니터 성능
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 모니터는 프로덕션 시스템 내의 많은 컴퓨터를 효율적으로 모니터링하도록 설계되었습니다. 계산을 수행하고 데이터를 수집하기 위해 복제 모니터가 사용하는 쿼리는 정기적으로 캐시되며 새로 고쳐집니다. 캐싱을 사용하면 복제 모니터에서 여러 페이지를 볼 때 필요한 쿼리 및 계산의 수를 줄일 수 있고 여러 사용자에 대해 모니터링을 확장할 수 있습니다.  
  
 캐시 새로 고침은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 작업, 즉 **배포에 대한 복제 모니터링 리프레셔**로 처리됩니다. 이 작업은 계속 실행되지만 캐시 새로 고침 일정은 이전 새로 고침 후 일정 시간 동안 대기한 다음 실행됩니다.  
  
-   마지막으로 캐시를 만든 이후에 에이전트 기록을 변경한 경우 대기 시간은 최소 4초 또는 이전 캐시를 만드는 데 소요된 시간입니다.  
  
-   마지막으로 캐시를 만든 이후에 에이전트 기록을 변경하지 않은 경우(다른 변경 내용은 있을 수 있음) 대기 시간은 최대 30초 또는 이전 캐시를 만드는 데 소요된 시간입니다.  
  
## 복제 모니터 사용자 인터페이스 새로 고침  
 다음과 같은 방법으로 복제 모니터 사용자 인터페이스를 새로 고칠 수 있습니다.  
  
-   기본적으로 주 복제 모니터 창(모든 탭 포함)은 자동으로 5초마다 새로 고쳐집니다. 자동 새로 고침으로 인해 캐시가 새로 고쳐지지는 않으며 사용자 인터페이스는 캐시에서 가장 최신 버전의 데이터를 표시합니다. 게시자 설정을 편집하여 게시자와 연결된 모든 창에 사용되는 새로 고침 빈도를 사용자 지정할 수 있습니다. 또한 게시자에 대한 자동 새로 고침을 해제할 수 있습니다.  
  
-   복제 모니터에 표시되는 세부 정보 창은 동기화를 수행 중인 병합 구독에 관련된 창을 제외하고 기본적으로 자동 새로 고침되지 않습니다. 세부 정보 창이 자동으로 새로 고쳐지도록 지정한 경우 이 창은 주 복제 모니터 창과 같은 일정으로 새로 고쳐집니다.  
  
-   모든 창을 수동으로 새로 고칠 수 f5 키를 눌러 또는 복제 모니터 트리의 노드를에서 마우스 오른쪽 단추로 클릭 하 여 **새로 고침**합니다. 수동으로 새로 고침을 수행하면 캐시도 새로 고쳐집니다.  
  
 자세한 내용은 참조 [복제 모니터에서 데이터 새로 고침](../../../relational-databases/replication/monitor/refresh-data-in-replication-monitor.md)합니다.  
  
## 성능 고려 사항  
 복제 모니터는 효율적으로 실행되도록 설계되었지만 다음 사항에 유의하는 것이 좋습니다.  
  
-   게시 또는 구독의 수가 많은 경우 사용자 인터페이스에 대한 자동 새로 고침 횟수를 줄이십시오.  
  
-   여러 복제 모니터 인스턴스를 동시에 실행하지 마십시오.  
  
-   많은 배포자를 등록한 다음 복제 모니터가 자동으로 이러한 모든 배포자에 연결하도록 설정하지 마십시오.  
  
## 참고 항목  
 [복제 유지 관리 작업 및 #40; 실행 SQL Server Management Studio & #41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  