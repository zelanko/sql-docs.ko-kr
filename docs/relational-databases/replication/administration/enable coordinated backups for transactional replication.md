---
title: "트랜잭션 복제에 대해 통합 백업 사용(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
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
  - "트랜잭션 복제, 백업 및 복원"
  - "sp_replicationdboption"
  - "백업으로 동기화 [SQL Server 복제]"
  - "통합 백업 [SQL Server 복제]"
  - "백업 [SQL Server 복제], 트랜잭션 복제"
ms.assetid: 73a914ba-8b2d-4f4d-ac1b-db9bac676a30
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 트랜잭션 복제에 대해 통합 백업 사용(복제 Transact-SQL 프로그래밍)
  트랜잭션 복제에 데이터베이스를 사용할 경우 모든 트랜잭션을 배포 데이터베이스에 배달하기 전에 반드시 백업하도록 지정할 수 있습니다. 배포자에 전파된 트랜잭션이 백업될 때까지 게시 데이터베이스의 트랜잭션 로그가 잘리지 않도록 배포 데이터베이스에 통합 백업을 사용할 수도 있습니다. 자세한 내용은 [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)을 참조하세요.  
  
### 트랜잭션 복제를 사용하여 게시된 데이터베이스에 대해 통합 백업을 사용하도록 설정하려면  
  
1.  게시자에서 사용 하 여는 [DATABASEPROPERTYEX (& a) #40; TRANSACT-SQL & #41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) 함수를 반환 하는 **IsSyncWithBackup** 게시 데이터베이스의 속성입니다. 해당 함수에서 **1**을 반환하면 게시된 데이터베이스에 대해 통합 백업이 이미 사용되고 있는 것입니다.  
  
2.  1 단계에서 함수를 반환 하는 경우 **0**, 실행 [sp_replicationdboption (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 게시 데이터베이스의 게시자입니다. **@optname** 에 **sync with backup**값을 지정하고 **@value** 에 **true**값을 지정합니다.  
  
    > [!NOTE]  
    >  **sync with backup** 옵션을 **false**로 변경하면 로그 판독기 에이전트가 실행된 후 또는 한 번의 간격이 지난 후(로그 판독기 에이전트가 계속 실행되는 경우) 게시 데이터베이스의 잘린 부분이 업데이트됩니다. 최대 간격에 의해 제어 되는 **– MessageInterval** 에이전트 매개 변수 (의 기본값은 30 초)입니다.  
  
### 배포 데이터베이스에 통합 백업을 사용하도록 설정하려면  
  
1.  배포자에서 사용 하 여는 [DATABASEPROPERTYEX (& a) #40; TRANSACT-SQL & #41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) 함수를 반환 하는 **IsSyncWithBackup** 배포 데이터베이스의 속성입니다. 해당 함수에서 **1**을 반환하면 배포 데이터베이스에 대해 통합 백업이 이미 사용되고 있는 것입니다.  
  
2.  1 단계에서 함수를 반환 하는 경우 **0**, 실행 [sp_replicationdboption (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 배포 데이터베이스의 배포자입니다. **@optname** 에 **sync with backup** 값을 지정하고 **@value** 에 **true**값을 지정합니다.  
  
### 통합 백업을 사용하지 않도록 설정하려면  
  
1.  게시 데이터베이스의 게시자 또는 배포 데이터베이스의 배포자에서 실행 [sp_replicationdboption (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)합니다. **@optname** 에 **sync with backup** 값을 지정하고 **@value** 에 **false**값을 지정합니다.  
  
  