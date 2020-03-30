---
title: 아티클 추가 및 삭제(기존 게시)
description: SQL Server용 기존 게시에 아티클을 추가하고 삭제하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- removing articles
- dropping articles
- adding articles
- administering replication, articles
- publications [SQL Server replication], adding and dropping articles
- articles [SQL Server replication], adding
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 1bd5e9d25a2f45718e7ac03de1edced942702198
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76286537"
---
# <a name="add-articles-to-and-drop-articles-from-existing-publications"></a>기존 게시에 대한 아티클 추가 및 삭제
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  게시가 생성된 후에는 아티클을 추가 및 삭제할 수 있습니다. 아티클 추가 작업은 언제든지 수행할 수 있지만 아티클 삭제에 필요한 동작은 복제 유형과 아티클 삭제 시기에 따라 다릅니다.  
  
## <a name="adding-articles"></a>아티클 추가  
 아티클을 추가하려면 아티클을 게시에 추가하고, 게시에 대한 새 스냅샷을 만들고, 구독을 동기화하여 새 아티클에 대한 스키마 및 데이터를 적용해야 합니다.  
  
> [!NOTE]
>  병합 게시에 아티클을 추가하고 기존 아티클이 새 아티클에 종속된 경우 **sp_addmergearticle\@ 및** sp_changemergearticle[의 ](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)[processing_order](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 매개 변수를 사용하여 두 아티클의 처리 순서를 지정해야 합니다. 다음과 같은 시나리오를 고려해 보십시오. 테이블을 게시하지만 테이블이 참조하는 함수는 게시하지 않는 경우가 있습니다. 함수를 게시하지 않을 경우 구독자에서 테이블을 만들 수 없습니다. 게시에 함수를 추가할 경우에는 **sp_addmergearticle**의 **\@processing_order** 매개 변수에 값 **1**을 지정하고 **sp_changemergearticle**의 **\@processing_order** 매개 변수에 값 **2**를 지정하며 **\@article** 매개 변수에는 테이블 이름을 지정합니다. 이 처리 순서를 사용하면 함수에 종속된 테이블이 생성되기 전에 해당 함수가 구독자에서 생성됩니다. 함수 번호가 테이블 번호보다 낮은 경우 각 아티클에 다른 번호를 사용할 수 있습니다.  
  
1.  다음 방법 중 하나를 사용하여 하나 이상의 아티클을 추가합니다.  
  
    -   [게시에 대한 아티클 추가 및 삭제&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [아티클 정의](../../../relational-databases/replication/publish/define-an-article.md)  
  
2.  아티클을 게시에 추가한 후에는 게시에 대한 새 스냅샷을 만들어야 합니다. 매개 변수가 있는 필터가 포함된 병합 게시인 경우에는 파티션도 모두 만들어야 합니다. 그러면 배포 에이전트 또는 병합 에이전트가 새 아티클에 대한 스키마 및 데이터를 구독자로 복사합니다. 이때 전체 게시를 다시 초기화하지는 않습니다.  
  
    -   새 스냅샷을 만들려면 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하십시오.  
  
    -   매개 변수가 있는 필터로 병합 게시에 대한 새 스냅샷을 만들려면 [매개 변수가 있는 필터로 병합 게시에 대한 스냅샷 만들기](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)를 참조하세요.  
  
3.  스냅샷이 생성된 후에 구독을 동기화하여 새 아티클에 대한 스키마 및 데이터를 복사합니다.  

    -   밀어넣기 구독을 동기화하려면 [Synchronize a Push Subscription](../../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하십시오.  
  
    -   끌어오기 구독을 동기화하려면 [Synchronize a Pull Subscription](../../../relational-databases/replication/synchronize-a-pull-subscription.md)를 참조하십시오.  
  
## <a name="dropping-articles"></a>아티클 삭제  
 언제든지 아티클을 게시에서 삭제할 수 있지만 다음 동작을 고려해야 합니다.  
  
-   게시에서 아티클을 삭제해도 해당 개체가 게시 데이터베이스에서 삭제되거나 구독 데이터베이스의 해당 개체가 삭제되지 않습니다. 필요한 경우 DROP \<Object>를 사용하여 이러한 개체를 제거합니다. 외래 키 제약 조건을 통해 다른 게시된 아티클과 관련된 아티클을 삭제하는 경우에는 테이블을 구독자에서 수동으로 삭제하거나, 적절한 DROP \<Object> 문이 포함된 스크립트를 지정하고 요청 시 실행하여 테이블을 삭제하는 것이 좋습니다. 자세한 내용은 [동기화 중 스크립트 실행&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)을 참조하세요.  
  
-   호환성 수준이 90RTM 이상인 병합 게시의 경우에는 언제든지 아티클을 삭제할 수 있지만 새 스냅샷이 필요합니다. 또한 다음 작업도 수행해야 합니다.  
  
    -   아티클이 조인 필터 또는 논리적 레코드 관계에서 부모 아티클인 경우에는 해당 관계를 먼저 삭제해야 하므로 재초기화가 필요합니다.  
  
    -   게시에서 아티클에 매개 변수가 있는 마지막 필터가 있는 경우에는 구독을 다시 초기화해야 합니다.  
  
-   호환성 수준이 90RTM 이하인 병합 게시의 경우에는 구독의 초기 동기화 이전에 특별한 고려 사항 없이 아티클을 삭제할 수 있습니다. 하나 이상의 구독이 동기화된 후에 아티클을 삭제하면 해당 구독을 삭제한 뒤 다시 만들고 동기화해야 합니다.  
  
-   스냅샷 또는 트랜잭션 게시의 경우에는 구독을 만들기 전에 특별한 고려 사항 없이 아티클을 삭제할 수 있습니다. 하나 이상의 구독이 생성된 후에 아티클을 삭제하면 해당 구독을 삭제한 뒤 다시 만들고 동기화해야 합니다. 구독 삭제에 대한 자세한 내용은 [게시 구독](../../../relational-databases/replication/subscribe-to-publications.md) 및 [sp_dropsubscription&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)을 참조하세요. **sp_dropsubscription** 을 사용하면 전체 구독 대신 구독에서 단일 아티클을 삭제할 수 있습니다.  
  
1.  게시에서 아티클을 삭제하려면 아티클을 삭제하고 게시에 대한 새 스냅샷을 만들어야 합니다. 아티클을 삭제하면 현재 스냅샷이 무효화되므로 새 스냅샷을 만들어야 합니다.  
  
    -   게시에서 아티클을 삭제하려면 [게시에 대한 아티클 추가 및 삭제&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md) 또는 [아티클 삭제](../../../relational-databases/replication/publish/delete-an-article.md)를 참조하세요.  
  
2.  게시에서 아티클을 삭제한 후에는 게시에 대한 새 스냅샷을 만들어야 합니다. 매개 변수가 있는 필터가 포함된 병합 게시인 경우에는 파티션도 모두 만들어야 합니다.  
  
    -   새 스냅샷을 만들려면 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하십시오.  
  
    -   매개 변수가 있는 필터로 병합 게시에 대한 새 스냅샷을 만들려면 [매개 변수가 있는 필터로 병합 게시에 대한 스냅샷 만들기](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)를 참조하세요.  
  
 위에서 언급한 대로 경우에 따라서는 아티클을 삭제하면 구독을 삭제한 뒤 다시 만들고 동기화해야 합니다. 자세한 내용은 [게시 구독](../../../relational-databases/replication/subscribe-to-publications.md) 및 [데이터 동기화](../../../relational-databases/replication/synchronize-data.md)를 참조하세요.  
 
 > [!NOTE]
 > **[!INCLUDE[ssSQL15](../../../includes/sssql14-md.md)] 서비스 팩 2** 이상 및 **[!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] 서비스 팩 1** 이상에서는 트랜잭션 복제에 참여하는 아티클에 대한 **DROP TABLE** DLL 명령을 사용한 테이블 삭제를 지원합니다. 게시에서 DROP TABLE DDL이 지원되면 DROP TABLE 작업은 게시 및 데이터베이스에서 테이블을 삭제합니다. 로그 판독기 에이전트는 삭제된 테이블의 배포 데이터베이스에 대해 정리 명령을 게시하고 게시자 메타데이터를 정리합니다. 로그 판독기가 삭제된 테이블을 참조하는 일부 로그 레코드를 처리하지 않은 경우에는 삭제된 테이블과 연결된 새 명령을 무시합니다. 이미 처리된 레코드는 배포 데이터베이스로 전달됩니다. 로그 판독기가 오래된(삭제된) 아티클을 정리하기 전에 배포 에이전트가 이 레코드를 처리할 경우 이 레코드는 구독자 데이터베이스에 적용될 수 있습니다. 모든 트랜잭션 복제 게시에 대한 **기본** 설정은 DROP TABLE DLL을 지원하지 않는 것입니다. [KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1)에서 이 향상된 기능을 자세히 설명합니다.

  
## <a name="see-also"></a>참고 항목  
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [게시 데이터베이스의 스키마 변경](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
