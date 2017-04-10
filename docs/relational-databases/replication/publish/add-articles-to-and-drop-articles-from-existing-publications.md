---
title: "기존 게시에 대한 아티클 추가 및 삭제 | Microsoft Docs"
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
  - "아티클 [SQL Server 복제], 삭제"
  - "아티클 삭제"
  - "아티클 제거"
  - "아티클 삭제"
  - "아티클 추가"
  - "복제 관리, 아티클"
  - "게시 [SQL Server 복제], 아티클 추가 및 삭제"
  - "아티클 [SQL Server 복제], 추가"
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
caps.latest.revision: 48
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# 기존 게시에 대한 아티클 추가 및 삭제
  게시가 생성된 후에는 아티클을 추가 및 삭제할 수 있습니다. 아티클 추가 작업은 언제든지 수행할 수 있지만 아티클 삭제에 필요한 동작은 복제 유형과 아티클 삭제 시기에 따라 다릅니다.  
  
## 아티클 추가  
 아티클을 추가하려면 아티클을 게시에 추가하고, 게시에 대한 새 스냅숏을 만들고, 구독을 동기화하여 새 아티클에 대한 스키마 및 데이터를 적용해야 합니다.  
  
> [!NOTE]  
>  사용 하 여 두 아티클의 처리 순서를 지정 해야 병합 게시에 아티클을 추가 하는 경우 새 문서에 기존 아티클에 따라 달라 집니다는 **@processing_order** 의 매개 변수 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 및 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)합니다. 다음과 같은 시나리오를 고려해 보십시오. 테이블을 게시하지만 테이블이 참조하는 함수는 게시하지 않는 경우가 있습니다. 함수를 게시하지 않을 경우 구독자에서 테이블을 만들 수 없습니다. 게시에 함수를 추가 하면: 값을 지정 **1** 에 대 한는 **@processing_order** 의 매개 변수 **sp_addmergearticle**;의 값을 지정 하 고 **2** 에 대 한는 **@processing_order** 의 매개 변수 **sp_changemergearticle**, 매개 변수는 테이블 이름을 지정 **@article**합니다. 이 처리 순서를 사용하면 함수에 종속된 테이블이 생성되기 전에 해당 함수가 구독자에서 생성됩니다. 함수 번호가 테이블 번호보다 낮은 경우 각 아티클에 다른 번호를 사용할 수 있습니다.  
  
1.  다음 방법 중 하나를 사용하여 하나 이상의 아티클을 추가합니다.  
  
    -   [추가 및 삭제 게시 & #40;에서 SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [아티클 정의](../../../relational-databases/replication/publish/define-an-article.md)  
  
2.  아티클을 게시에 추가한 후에는 게시에 대한 새 스냅숏을 만들어야 합니다. 매개 변수가 있는 필터가 포함된 병합 게시인 경우에는 파티션도 모두 만들어야 합니다. 그러면 배포 에이전트 또는 병합 에이전트가 새 아티클에 대한 스키마 및 데이터를 구독자로 복사합니다. 이때 전체 게시를 다시 초기화하지는 않습니다.  
  
    -   새 스냅숏을 만들려면 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하십시오.  
  
    -   참조 매개 변수가 있는 필터로 병합 게시에 대 한 새 스냅숏을 만들려면 [매개 변수가 있는 필터로 병합 게시에 대 한 스냅숏을 만들](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)합니다.  
  
3.  스냅숏이 생성된 후에 구독을 동기화하여 새 아티클에 대한 스키마 및 데이터를 복사합니다.  
  
    -   밀어넣기 구독을 동기화하려면 [Synchronize a Push Subscription](../../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하십시오.  
  
    -   끌어오기 구독을 동기화하려면 [Synchronize a Pull Subscription](../../../relational-databases/replication/synchronize-a-pull-subscription.md)를 참조하십시오.  
  
## 아티클 삭제  
 언제든지 아티클을 게시에서 삭제할 수 있지만 다음 동작을 고려해야 합니다.  
  
-   게시에서 아티클을 삭제해도 해당 개체가 게시 데이터베이스에서 삭제되거나 구독 데이터베이스의 해당 개체가 삭제되지 않습니다. DROP 사용 하 여 \< 개체> 필요한 경우 이러한 개체를 제거 합니다. 외래 키 제약 조건을 통해 다른 게시 된 아티클과 관련 된 아티클을 삭제 하면 수동으로 또는 요청 시 스크립트 실행을 사용 하 여 구독자에서 테이블을 삭제 하는 것이 좋습니다: 적절 한 DROP을 포함 하는 스크립트를 지정 합니다. \< 개체> 문입니다. 자세한 내용은 참조 [동기화 중 스크립트 실행 & #40; 복제 TRANSACT-SQL 프로그래밍 & #41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)합니다.  
  
-   호환성 수준이 90RTM 이상인 병합 게시의 경우에는 언제든지 아티클을 삭제할 수 있지만 새 스냅숏이 필요합니다. 또한 다음 작업도 수행해야 합니다.  
  
    -   아티클이 조인 필터 또는 논리적 레코드 관계에서 부모 아티클인 경우에는 해당 관계를 먼저 삭제해야 하므로 재초기화가 필요합니다.  
  
    -   게시에서 아티클에 매개 변수가 있는 마지막 필터가 있는 경우에는 구독을 다시 초기화해야 합니다.  
  
-   호환성 수준이 90RTM 이하인 병합 게시의 경우에는 구독의 초기 동기화 이전에 특별한 고려 사항 없이 아티클을 삭제할 수 있습니다. 하나 이상의 구독이 동기화된 후에 아티클을 삭제하면 해당 구독을 삭제한 뒤 다시 만들고 동기화해야 합니다.  
  
-   스냅숏 또는 트랜잭션 게시의 경우에는 구독을 만들기 전에 특별한 고려 사항 없이 아티클을 삭제할 수 있습니다. 하나 이상의 구독이 생성된 후에 아티클을 삭제하면 해당 구독을 삭제한 뒤 다시 만들고 동기화해야 합니다. 구독을 삭제 하는 방법에 대 한 자세한 내용은 참조 [게시를 구독할](../../../relational-databases/replication/subscribe-to-publications.md) 및 [sp_dropsubscription (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)합니다. **sp_dropsubscription** 전체 구독 대신 구독에서 단일 아티클을 삭제할 수 있습니다.  
  
1.  게시에서 아티클을 삭제하려면 아티클을 삭제하고 게시에 대한 새 스냅숏을 만들어야 합니다. 아티클을 삭제하면 현재 스냅숏이 무효화되므로 새 스냅숏을 만들어야 합니다.  
  
    -   게시에서 아티클을 삭제 하려면 참조 [에 대 한 아티클 추가 및 게시 & #40;에서 문서 삭제 SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md) 또는 [아티클을 삭제](../../../relational-databases/replication/publish/delete-an-article.md)합니다.  
  
2.  게시에서 아티클을 삭제한 후에는 게시에 대한 새 스냅숏을 만들어야 합니다. 매개 변수가 있는 필터가 포함된 병합 게시인 경우에는 파티션도 모두 만들어야 합니다.  
  
    -   새 스냅숏을 만들려면 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하십시오.  
  
    -   참조 매개 변수가 있는 필터로 병합 게시에 대 한 새 스냅숏을 만들려면 [매개 변수가 있는 필터로 병합 게시에 대 한 스냅숏을 만들](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)합니다.  
  
 위에서 언급한 대로 경우에 따라서는 아티클을 삭제하면 구독을 삭제한 뒤 다시 만들고 동기화해야 합니다. 자세한 내용은 참조 [게시를 구독할](../../../relational-databases/replication/subscribe-to-publications.md) 및 [데이터 동기화](../../../relational-databases/replication/synchronize-data.md)합니다.  
  
## 참고 항목  
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [게시 데이터베이스의 스키마 변경](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  