---
title: "피어 투 피어 토폴로지 관리(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "트랜잭션 복제, 피어 투 피어 복제"
ms.assetid: 4d0fa941-f9ea-4a14-aed9-34df593fc6f2
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 피어 투 피어 토폴로지 관리(복제 Transact-SQL 프로그래밍)
  피어 투 피어 토폴로지를 관리하는 것은 일반적인 트랜잭션 복제 토폴로지를 관리하는 것과 비슷하지만 특별히 고려해야 하는 영역도 많이 있습니다. 피어 투 피어 토폴로지 관리에서 주요한 차이점은 일부 변경 내용이 시스템을는 *정지*합니다. 시스템 정지 과정에서는 모든 노드에서 게시된 테이블에 대한 작업을 중지하고 각 노드가 다른 모든 노드의 변경 내용을 받았는지 확인합니다. 자세한 내용은 참조 [정지 복제 토폴로지 및 #40; 복제 TRANSACT-SQL 프로그래밍 & #41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)합니다.  
  
> [!NOTE]  
>  피어 투 피어 토폴로지에서는 배포자가 끌어오기 구독자보다 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용할 수 없습니다.  
  
### 기존 구성에 아티클을 추가하려면  
  
1.  시스템을 정지합니다.  
  
2.  토폴로지의 각 노드에서 배포 에이전트를 중지합니다. 자세한 내용은 참조 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) 또는 [시작 및 중지 복제 에이전트 & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)합니다.  
  
3.  CREATE TABLE 문을 실행하여 토폴로지의 각 노드에 새 테이블을 추가합니다.  
  
4.  [bcp 유틸리티](../../../tools/bcp-utility.md)를 사용하여 새 테이블의 데이터를 모든 노드에 수동으로 대량 복사합니다.  
  
5.  실행 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 토폴로지의 각 노드에 새 아티클을 만드는 데 있습니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
    > [!NOTE]  
    >  후 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 가 실행 하 복제 토폴로지에서 구독 문서 자동으로 추가 합니다.  
  
6.  토폴로지의 각 노드에서 배포 에이전트를 다시 시작합니다.  
  
### 게시 데이터베이스의 스키마를 변경하려면  
  
1.  시스템을 정지합니다.  
  
2.  DDL(데이터 정의 언어) 문을 실행하여 게시된 테이블의 스키마를 수정합니다. 지원 되는 스키마 변경에 대 한 자세한 내용은 참조 [게시 데이터베이스에 스키마 변경을 확인](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)합니다.  
  
3.  게시된 테이블에 대한 작업을 다시 시작하기 전에 시스템을 다시 정지합니다. 이렇게 하면 새 데이터 변경 내용을 복제하기 전에 모든 노드에서 스키마 변경 내용을 받도록 할 수 있습니다.  
  
## 예제  
 다음 예제에서는 두 개의 노드가 있는 기존 피어 투 피어 복제 토폴로지에 새 테이블 아티클을 추가하는 방법을 보여 줍니다.  
  
 [!code-sql[HowTo#sp_addp2particle_createtables](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_1.sql)]  
  
 [!code-sql[HowTo#sp_addp2particle_cmdline](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_2.sql)]  
  
 [!code-sql[HowTo#sp_addp2particle_createarticle](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_3.sql)]  
  
## 참고 항목  
 [관리 및 #40입니다. 복제 및 #41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [SQL Server 데이터베이스 백업 및 복원](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [피어 투 피어 트랜잭션 복제](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  