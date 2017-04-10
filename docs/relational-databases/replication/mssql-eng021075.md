---
title: "MSSQL_ENG021075 | Microsoft Docs"
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
  - "MSSQL_ENG021075 오류"
ms.assetid: c8c29543-d1f6-49d5-b6c8-e8c3aa373090
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG021075
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21075|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|게시 '%s'의 초기 스냅숏을 사용할 수 없습니다.|  
  
## 설명  
 MSSQL_ENG021075 오류는 스냅숏 에이전트가 스냅숏 생성을 완료하기 전에 배포 에이전트 또는 병합 에이전트를 시작한 경우 발생합니다.  
  
## 사용자 동작  
 구독이 생성된 후 게시에 대한 스냅숏 에이전트가 시작되지 않았거나 마지막으로 구독을 다시 초기화한 이후 스냅숏 에이전트가 시작되지 않은 경우 스냅숏 에이전트를 시작하고 완료될 때까지 기다린 다음 배포 에이전트 또는 병합 에이전트를 시작합니다. 자세한 내용은 참조 [의 스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-snapshot.md)합니다.  
  
 스냅숏 에이전트가 완료되지 않는 경우 스냅숏 에이전트 기록에서 오류를 확인한 후 해결합니다. 복제 모니터에서 에이전트 상태 및 오류 정보를 보는 방법에 대 한 정보를 참조 하십시오. [정보 보기 및 에이전트 관련 된는 게시 및 #40;에 대 한 작업 수행 복제 모니터 & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)합니다.  
  
 오류가 계속 발생하면 에이전트의 로깅을 늘리고 해당 로그의 출력 파일을 지정하십시오. 오류의 컨텍스트에 따라 이러한 작업을 수행하면 오류 및/또는 추가 오류 메시지가 발생할 수 있습니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  