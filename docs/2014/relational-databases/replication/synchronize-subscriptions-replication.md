---
title: 구독 동기화(복제) | Microsoft 문서
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- synchronization [SQL Server replication], subscriptions
- subscriptions [SQL Server replication], synchronizing
- replication [SQL Server], synchronization
ms.assetid: cbe13120-8dd9-4309-88dd-07a801c68f5f
caps.latest.revision: 34
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 12887f7de8d425722c71049d4103f96f0946b6a6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091473"
---
# <a name="synchronize-subscriptions-replication"></a>구독 동기화(복제)
  구독은 복제 에이전트에 의해 동기화됩니다. 배포 에이전트는 트랜잭션 및 스냅숏 게시에 대한 구독을 동기화하며 병합 에이전트는 병합 게시에 대한 구독을 동기화합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 복제 저장 프로시저 및 RMO(복제 관리 개체)를 사용하여 구독을 동기화하고 동기화 동작을 제어할 수 있습니다. 다음 항목에서는 구독을 동기화하고 동기화 옵션을 지정하는 방법을 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [초기 스냅숏 만들기 및 적용](create-and-apply-the-initial-snapshot.md)  
  
-   [매개 변수가 있는 필터로 병합 게시에 대한 스냅숏 만들기](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [트랜잭션 게시에 대한 백업으로 초기화 설정&#40;SQL Server Management Studio&#41;](enable-initialization-with-backup-for-transactional-publications.md)  
  
-   [백업에서 트랜잭션 구독 초기화&#40;복제 Transact-SQL 프로그래밍&#41;](initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [수동 구독 초기화](initialize-a-subscription-manually.md)  
  
-   [끌어오기 구독 동기화](synchronize-a-pull-subscription.md)  
  
-   [밀어넣기 구독 동기화](synchronize-a-push-subscription.md)  
  
-   [구독 다시 초기화](reinitialize-a-subscription.md)  
  
-   [스냅숏 적용 전후에 스크립트 실행&#40;SQL Server Management Studio&#41;](execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [동기화 중 스크립트 실행&#40;복제 Transact-SQL 프로그래밍&#41;](execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [병합 게시에 대한 데이터 충돌 보기 및 해결&#40;SQL Server Management Studio&#41;](view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   [트랜잭션 게시의 데이터 충돌 확인&#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
-   [Windows 동기화 관리자를 사용하여 구독 동기화&#40;Windows 동기화 관리자&#41;](synchronize-a-subscription-using-windows-synchronization-manager.md)  
  
-   [병합 아티클에 대한 비즈니스 논리 처리기 구현](implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [비즈니스 논리 처리기 디버깅&#40;복제 프로그래밍&#41;](debug-a-business-logic-handler-replication-programming.md)  
  
-   [동기화하는 동안 트리거 및 제약 조건 동작 제어&#40;복제 Transact-SQL 프로그래밍&#41;](control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [병합 아티클용 사용자 지정 충돌 해결 프로그램 구현](implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 동기화](synchronize-data.md)  
  
  