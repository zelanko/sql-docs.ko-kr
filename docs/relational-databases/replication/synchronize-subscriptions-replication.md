---
title: "구독 동기화(복제) | Microsoft Docs"
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
  - "동기화 [SQL Server 복제], 구독"
  - "구독 [SQL Server 복제], 동기화"
  - "복제 [SQL Server], 동기화"
ms.assetid: cbe13120-8dd9-4309-88dd-07a801c68f5f
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 구독 동기화(복제)
  구독은 복제 에이전트에 의해 동기화됩니다. 배포 에이전트는 트랜잭션 및 스냅숏 게시에 대한 구독을 동기화하며 병합 에이전트는 병합 게시에 대한 구독을 동기화합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 복제 저장 프로시저 및 RMO(복제 관리 개체)를 사용하여 구독을 동기화하고 동기화 동작을 제어할 수 있습니다. 다음 항목에서는 구독을 동기화하고 동기화 옵션을 지정하는 방법을 설명합니다.  
  
## 섹션 내용  
  
-   [초기 스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [매개 변수가 있는 필터로 병합 게시에 대한 스냅숏 만들기](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [트랜잭션 게시 및 #40;에 대 한 백업으로 초기화를 사용 하도록 설정 SQL Server Management Studio & #41;](../../relational-databases/replication/enable initialization with backup for transactional publications.md)  
  
-   [백업 & #40;에서 트랜잭션 구독 초기화 복제 TRANSACT-SQL 프로그래밍 & #41;](../../relational-databases/replication/initialize a transactional subscription from a backup.md)  
  
-   [수동 구독 초기화](../../relational-databases/replication/initialize-a-subscription-manually.md)  
  
-   [끌어오기 구독 동기화](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [밀어넣기 구독 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
-   [구독 다시 초기화](../../relational-databases/replication/reinitialize-a-subscription.md)  
  
-   [전후 스냅숏을 적용 하는 스크립트를 실행 (& a) #40; SQL Server Management Studio & #41;](../../relational-databases/replication/execute scripts before and after a snapshot is applied.md)  
  
-   [동기화 & #40; 중 스크립트 실행 복제 TRANSACT-SQL 프로그래밍 & #41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [보기 및 병합 게시 및 #40;에 대 한 데이터 충돌 해결 SQL Server Management Studio & #41;](../../relational-databases/replication/view and resolve data conflicts for merge publications.md)  
  
-   [트랜잭션 게시 및 #40;에 대 한 데이터 충돌 보기 SQL Server Management Studio & #41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
-   [Windows 동기화 관리자 & #40;를 사용 하 여 구독 동기화 Windows 동기화 관리자 & #41;](../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md)  
  
-   [병합 아티클에 대한 비즈니스 논리 처리기 구현](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [비즈니스 논리 처리기를 & #40; 디버그 복제 프로그래밍 및 #41;](../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)  
  
-   [동기화 & #40; 하는 동안 트리거 및 제약 조건 동작을 제어 합니다. 복제 TRANSACT-SQL 프로그래밍 & #41;](../../relational-databases/replication/control behavior of triggers and constraints in synchronization.md)  
  
-   [병합 아티클용 사용자 지정 충돌 해결 프로그램 구현](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## 참고 항목  
 [데이터 동기화](../../relational-databases/replication/synchronize-data.md)  
  
  