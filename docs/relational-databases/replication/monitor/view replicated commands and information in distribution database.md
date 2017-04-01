---
title: "배포 데이터베이스의 복제된 명령 및 기타 정보 보기(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_browsereplcmds"
  - "트랜잭션 복제, 모니터링"
  - "배포 데이터베이스 [SQL Server 복제], 복제된 명령 보기"
  - "복제된 명령 보기"
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 배포 데이터베이스의 복제된 명령 및 기타 정보 보기(복제 Transact-SQL 프로그래밍)
  트랜잭션 복제를 사용하는 경우 트랜잭션 명령은 배포 에이전트에서 해당 명령을 모든 구독자에 전파하거나 구독자의 배포 에이전트에서 변경 내용을 끌어올 때까지 배포 데이터베이스에 저장됩니다. 이와 같이 배포 데이터베이스에서 보류 중인 명령은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 볼 수 있습니다. 자세한 내용은 참조 [복제 저장 프로시저 및 #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)합니다.  
  
### 배포 데이터베이스의 모든 트랜잭션 게시에서 복제된 명령을 보려면  
  
1.  배포 데이터베이스의 배포자에서 실행 [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md)합니다.  
  
### 트랜잭션 복제를 사용하여 게시된 특정 데이터베이스 또는 특정 아티클에서 배포 데이터베이스의 복제된 명령을 보려면  
  
1.  (선택 사항) 게시 데이터베이스의 게시자에서 실행 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)합니다. **@publication** 및 **@article**을 지정합니다. 결과 집합의 **article id** 값을 확인합니다.  
  
2.  배포 데이터베이스의 배포자에서 실행 [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md)합니다. (선택 사항) 문서 ID에 대해 2 단계에서 지정 **@article_id**합니다. (선택 사항) 에 대 한 게시 데이터베이스의 ID를 지정 **@publisher_database_id**, 에서 얻을 수 있습니다는 **database_id** 열에는 [sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰를 사용 합니다.  
  
## 참고 항목  
 [프로그래밍 방식으로 복제 모니터링](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  