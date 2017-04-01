---
title: "Oracle 게시자에 대한 트랜잭션 세트 작업 구성(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
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
  - "sp_publisherproperty"
  - "Oracle 게시 [SQL Server 복제], 구성"
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Oracle 게시자에 대한 트랜잭션 세트 작업 구성(복제 Transact-SQL 프로그래밍)
  **Xactset** 작업은 로그 판독기 에이전트가 Oracle 게시자에 연결되어 있지 않을 때 해당 게시자에서 트랜잭션 세트를 만들기 위해 실행되는 복제를 통해 만들어지는 Oracle 데이터베이스 작업입니다. 배포자에서 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 이 작업을 사용하도록 설정하고 구성할 수 있습니다. 자세한 내용은 참조 [Oracle 게시자에 대 한 성능 튜닝](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)합니다.  
  
### 트랜잭션 세트 작업을 사용하도록 설정하려면  
  
1.  Oracle 게시자에서 설정 된 **job_queue_processes** Xactset 작업을 실행 하려면 충분 한 값으로 초기화 매개 변수입니다. 이 매개 변수에 대한 자세한 내용은 Oracle 게시자의 데이터베이스 설명서를 참조하십시오.  
  
2.  배포자에서 실행 [sp_publisherproperty (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)합니다. **@publisher**에 대해 Oracle 게시자의 이름, **@propertyname** 에 대해 값 **xactsetbatching**, **@propertyvalue** 에 대해 값 **enabled**를 지정합니다.  
  
3.  배포자에서 실행 [sp_publisherproperty (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)합니다. **@publisher**에 대해 Oracle 게시자의 이름, **@propertyname** 에 대해 값 **xactsetjobinterval**, **@propertyvalue**에 대해 작업 간격(분)을 지정합니다.  
  
4.  배포자에서 실행 [sp_publisherproperty (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)합니다. **@publisher**에 대해 Oracle 게시자의 이름, **@propertyname** 에 대해 값 **xactsetjob**, **@propertyvalue** 에 대해 값 **enabled**를 지정합니다.  
  
### 트랜잭션 세트 작업을 구성하려면  
  
1.  (선택 사항) 배포자에서 실행 [sp_publisherproperty (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)합니다. **@publisher**에 대해 Oracle 게시자의 이름을 지정합니다. 이렇게 하면 게시자에서 **Xactset** 작업의 속성이 반환됩니다.  
  
2.  배포자에서 실행 [sp_publisherproperty (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)합니다. **@publisher**에 대해 Oracle 게시자의 이름, **@propertyname**에 대해 설정할 Xactset 작업 속성의 이름, **@propertyvalue**에 대해 새 설정을 지정합니다.  
  
3.  (옵션) 설정할 각 Xactset 작업 속성에 대해 2단계를 반복합니다. **xactsetjobinterval** 속성을 변경하는 경우 Oracle 게시자의 작업을 다시 시작해야 새 간격이 적용됩니다.  
  
### 트랜잭션 세트 작업의 속성을 보려면  
  
1.  배포자에서 실행 [sp_helpxactsetjob](../../../relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql.md)합니다. **@publisher**에 대해 Oracle 게시자의 이름을 지정합니다.  
  
### 트랜잭션 세트 작업을 사용하지 않도록 설정하려면  
  
1.  배포자에서 실행 [sp_publisherproperty (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)합니다. **@publisher**에 대해 Oracle 게시자의 이름, **@propertyname** 에 대해 값 **xactsetjob**, **@propertyvalue** 에 대해 값 **disabled**를 지정합니다.  
  
## 예제  
 다음 예제에서는 `Xactset` 작업을 사용하도록 설정하고 실행 간격을 3분으로 설정합니다.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../relational-databases/replication/codesnippet/tsql/configure the transactio_1.sql)]  
  
## 참고 항목  
 [Oracle 게시자를 위한 성능 튜닝](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)   
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  