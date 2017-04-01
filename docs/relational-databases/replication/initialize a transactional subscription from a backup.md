---
title: "백업에서 트랜잭션 구독 초기화(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
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
  - "수동 구독 초기화 [SQL Server 복제]"
  - "구독 [SQL Server 복제], 초기화"
  - "구독 초기화 [SQL Server 복제], 스냅숏 없음"
  - "트랜잭션 복제, 백업 및 복원"
  - "백업 [SQL Server 복제], 트랜잭션 복제"
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 백업에서 트랜잭션 구독 초기화(복제 Transact-SQL 프로그래밍)
  일반적으로 트랜잭션 게시에 대한 구독은 스냅숏을 사용하여 초기화하지만 복제 저장 프로시저를 사용하여 백업에서 구독을 초기화할 수도 있습니다. 자세한 내용은 참조 [초기화는 Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)합니다.  
  
### 백업에서 트랜잭션 구독자를 초기화하려면  
  
1.  기존 게시에 대 한 게시를 실행 하 여 백업에서 초기화 하는 기능을 지원 하는지 확인 하십시오 [sp_helppublication (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) 게시 데이터베이스의 게시자입니다. 값을 확인 **allow_initialize_from_backup** 결과 집합에 있습니다.  
  
    -   값이 **1**이면 게시에서 이 기능을 지원하는 것입니다.  
  
    -   값이 **0**, 실행 [sp_changepublication (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) 게시 데이터베이스의 게시자입니다. 값을 지정 **allow_initialize_from_backup** 에 대 한 **@property** 값 **true** 에 대 한 **@value**합니다.  
  
2.  새 게시의 경우에 대해 실행 [sp_addpublication (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 게시 데이터베이스의 게시자입니다. 값을 지정 **true** 에 대 한 **allow_initialize_from_backup**합니다. 자세한 내용은 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)을 참조하세요.  
  
    > [!WARNING]  
    >  사용 하는 경우 구독자 데이터 손실을 방지 하려면 **sp_addpublication** 와 `@allow_initialize_from_backup = N'true'`, 항상 사용 하 여 `@immediate_sync = N'true'`합니다.  
  
3.  사용 하 여 게시 데이터베이스 백업 만들기는 [백업 & #40; TRANSACT-SQL & #41;](../../t-sql/statements/backup-transact-sql.md) 문입니다.  
  
4.  사용 하 여 구독자에서 백업을 복원는 [복원 & #40; TRANSACT-SQL & #41;](../Topic/RESTORE%20\(Transact-SQL\).md) 문입니다.  
  
5.  게시 데이터베이스의 게시자에서 저장된 프로시저를 실행 [sp_addsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 다음 매개 변수를 지정합니다.  
  
    -   **@sync_type** -값 **백업으로 초기화**합니다.  
  
    -   **@backupdevicetype** -백업 장치의 유형: **논리** (기본값) 이면 **디스크**, 또는 **테이프**합니다.  
  
    -   **@backupdevicename** -복원에 사용할 논리적 또는 물리적 백업 장치입니다.  
  
         논리적 장치에 대 한 경우 지정 된 백업 장치의 이름을 지정 **sp_addumpdevice** 장치를 만드는 데 사용 합니다.  
  
         물리적 장치의 경우 `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\BACKUP\Mybackup.dat'` 또는 `TAPE = '\\.\TAPE0'`과 같이 전체 경로와 파일 이름을 지정합니다.  
  
    -   (선택 사항) **@password** -백업 세트를 만들 때 제공한 암호입니다.  
  
    -   (선택 사항) **@mediapassword** -미디어 세트를 포맷할 때 제공한 암호입니다.  
  
    -   (선택 사항) **@fileidhint** -백업 세트를 복원할 수에 대 한 식별자입니다. 예를 들어 **1** 을 지정하면 백업 미디어의 첫 번째 백업 세트를 나타내고 **2** 를 지정하면 두 번째 백업 세트를 나타냅니다.  
  
    -   (테이프 장치에 대 한 선택 사항) **@unload** -값을 지정 **1** 복원이 완료 된 후 테이프 드라이브에서 언로드할 수 해야 하는 경우 (기본값) 및 **0** 언로드된 하지 않아야 하는 경우.  
  
6.  (선택 사항) 끌어오기 구독에 대 한 실행 [sp_addpullsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) 및 [sp_addpullsubscription_agent (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) 구독자에서 구독 데이터베이스입니다. 자세한 내용은 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)을 참조하세요.  
  
7.  (옵션) 배포 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 또는 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
## 참고 항목  
 [백업 및 복원으로 데이터베이스 복사](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  