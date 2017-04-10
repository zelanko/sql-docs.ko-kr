---
title: "구독, 배포되지 않은 명령(트랜잭션 구독, SQL Server 2005 이상) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.subscription.performance.f1"
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 구독, 배포되지 않은 명령(트랜잭션 구독, SQL Server 2005 이상)
  **배포되지 않은 명령** 탭에는 선택한 구독자에 배달되지 않은 배포 데이터베이스의 명령 수와 해당 명령의 예상 배달 시간에 대한 정보가 표시됩니다. 배포 데이터베이스의 명령을 보는 방법에 대 한 정보를 참조 하십시오. [sp_replshowcmds (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)합니다.  
  
## 옵션  
 **이 구독자에 적용되기를 기다리는 배포 데이터베이스의 명령 수**  
 선택한 구독자에 배달되지 않은 배포 데이터베이스의 명령 수. 명령은 하나의 Transact-SQL DML(데이터 조작 언어) 문이나 하나의 DDL(데이터 정의 언어) 문으로 구성됩니다.  
  
 **과거 성능을 기준으로 이 명령 적용에 소요될 예상 시간**  
 명령을 구독자에 배달하는 데 걸리는 예상 시간. 이 값이 스냅숏을 생성하여 구독자에 적용하는 데 필요한 시간 값보다 더 큰 경우 구독자를 다시 초기화하십시오. 자세한 내용은 참조 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)합니다.  
  
## 참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [복제 모니터로 성능 모니터링](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  