---
title: 아티클 유형 정의(복제 Transact-SQL 프로그래밍) | Microsoft 문서
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- stored procedures [SQL Server replication], publishing
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cfa3710648e381dbd142c57180bf5395d9eee18f
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72904630"
---
# <a name="specify-article-types-replication-transact-sql-programming"></a>아티클 유형 정의(복제 Transact-SQL 프로그래밍)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  복제를 위한 기본 아티클 유형은 테이블 아티클이지만 뷰, 저장 프로시저, 사용자 정의 함수 및 저장 프로시저 실행을 포함한 다른 데이터베이스 개체를 아티클로 게시할 수 있습니다. 아티클을 정의할 때 복제 저장 프로시저를 사용하여 아티클 유형을 프로그래밍 방식으로 지정할 수 있습니다. 사용되는 저장 프로시저는 복제 유형 및 아티클 유형에 따라 다릅니다.  
  
> [!NOTE]  
>  테이블, 뷰 및 저장 프로시저 아티클을 정의하는 경우 스키마 전용 지정은 개체 정의만 복제됨을 나타냅니다.  
  
### <a name="to-publish-a-table-article-in-a-transactional-or-snapshot-publication"></a>트랜잭션 또는 스냅샷 게시에 테이블 아티클을 게시하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 실행합니다. `@type`에 다음 값 중 하나를 지정하여 아티클 유형을 정의합니다.  
  
    -   `logbased` - 로그 기반 테이블 아티클로, 트랜잭션 및 스냅샷 복제의 기본값입니다. 행 필터링에 사용되는 저장 프로시저와 열 필터링된 아티클을 정의하는 뷰가 자동으로 생성됩니다.  
  
    -   `logbased manualfilter` - 행 필터링에 사용되는 저장 프로시저를 사용자가 수동으로 만들어 정의하고 `@filter`에 지정하는 로그 기반의 행 필터링된 아티클입니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)을 참조하세요.  
  
    -  `logbased manualview` - 열 필터링된 아티클을 정의되는 뷰를 사용자가 만들어 정의하고 `@sync_object`에 지정하는 로그 기반의 열 필터링된 아티클입니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 및 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)를 참조하세요.  
  
    -   `logbased manualboth` - 행 필터링에 사용되는 저장 프로시저와 열 필터링된 아티클을 정의하는 뷰를 사용자가 만들어 정의하고 각각 `@filter` 및 `@sync_object`에 지정하는 로그 기반의 행 필터링 및 열 필터링된 아티클입니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 및 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)를 참조하세요.  
  
     게시에 대한 새 아티클을 정의합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
2.  `logbased manualboth` 및 `logbased manualfilter` 아티클의 경우 [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)를 실행하여 행 필터링된 아티클에 대한 필터링 저장 프로시저를 생성합니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)을 참조하세요.  
  
3.  `logbased manualboth`, `logbased manualview` 및 `logbased manualfilter` 아티클의 경우 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)를 실행하여 열 필터링된 아티클을 정의하는 뷰를 생성합니다. 자세한 내용은 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)을 참조하세요.  

### <a name="to-publish-a-view-or-indexed-view-article-in-a-transactional-or-snapshot-publication"></a>트랜잭션 또는 스냅샷 게시에 뷰 또는 인덱싱된 뷰 아티클을 게시하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 실행합니다. `@type`에 다음 값 중 하나를 지정하여 아티클 유형을 정의합니다.  
  
    -   **indexed view logbased** - 로그 기반의 인덱싱된 뷰 아티클입니다. 행 필터링에 사용되는 저장 프로시저와 열 필터링된 아티클을 정의하는 뷰가 자동으로 생성됩니다.  
  
    -   **view schema only** - 스키마 전용 뷰 아티클입니다. 기본 테이블도 복제되어야 합니다.  
  
    -   **indexed view schema only** - 스키마 전용 인덱싱된 뷰 아티클입니다. 기본 테이블도 복제되어야 합니다.  
  
    -   **indexed view logbased manualfilter** - 행 필터링에 사용되는 저장 프로시저를 사용자가 수동으로 만들어 정의하고 `@filter`에 지정하는 로그 기반의 행 필터링된 인덱싱된 뷰 아티클입니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)을 참조하세요.  
  
    -   **indexed view logbased manualview** - 열 필터링된 아티클을 정의하는 뷰를 사용자가 만들어 정의하고 `@sync_object`에 지정하는 로그 기반의 필터링 및 인덱싱된 뷰 아티클입니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 및 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)를 참조하세요.  
  
    -   **indexed view logbased manualboth** - 행 필터링에 사용되는 저장 프로시저와 열 필터링된 아티클을 정의하는 뷰를 사용자가 만들어 정의하고 각각 `@filter` 및 `@sync_object`에 지정하는 로그 기반의 필터링 및 인덱싱된 뷰 아티클입니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 및 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)를 참조하세요.  
  
     게시에 대한 새 아티클을 정의합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
2.  **logbased manualboth** 및 **logbased manualfilter** 아티클의 경우 [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 를 실행하여 행 필터링된 아티클에 대한 필터링 저장 프로시저를 생성합니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)을 참조하세요.  
  
3.  **logbased manualboth**, **logbased manualview**및 **logbased manualfilter** 아티클의 경우 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 를 실행하여 열 필터링된 아티클을 정의하는 뷰를 생성합니다. 자세한 내용은 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)을 참조하세요.  
  
### <a name="to-publish-a-stored-procedure-stored-procedure-execution-or-user-defined-function-article-in-a-transactional-or-snapshot-publication"></a>저장 프로시저, 저장 프로시저 실행 또는 사용자 정의 함수 아티클을 트랜잭션 또는 스냅샷 게시에 게시하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 실행합니다. `@type`에 다음 값 중 하나를 지정하여 아티클 유형을 정의합니다.  
  
    -   **proc schema only** - 스키마 전용 저장 프로시저 아티클입니다.  
  
    -   **proc exec** - 저장 프로시저의 실행을 아티클의 모든 구독자에 복제합니다. 자세한 내용은 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)를 참조하세요.  
  
    -   **serializable proc exec** - 직렬화할 수 있는 트랜잭션 컨텍스트 내에서 실행된 경우에만 저장 프로시저의 실행을 복제합니다. 자세한 내용은 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)를 참조하세요.  
  
    -   **func schema only** - 스키마 전용 사용자 정의 함수 아티클입니다.  
  
     게시에 대한 새 아티클을 정의합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
### <a name="to-publish-a-table-or-view-article-in-a-merge-publication"></a>병합 게시에 테이블 또는 뷰 아티클을 게시하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행합니다. `@type`에 다음 값 중 하나를 지정하여 아티클 유형을 정의합니다.  
  
    -   **table** - 테이블 아티클입니다.  
  
    -   **indexed view schema only** - 스키마 전용 인덱싱된 뷰 아티클입니다.  
  
    -   **view schema only** - 스키마 전용 뷰 아티클입니다.  
  
     게시에 대한 새 아티클을 정의합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
### <a name="to-publish-a-stored-procedure-or-user-defined-function-article-in-a-merge-publication"></a>병합 게시에 저장 프로시저 또는 사용자 정의 함수 아티클을 게시하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행합니다. `@type`에 다음 값 중 하나를 지정하여 아티클 유형을 정의합니다.  
  
    -   **func schema only** - 스키마 전용 사용자 정의 함수 아티클입니다.  
  
    -   **proc schema only** - 스키마 전용 저장 프로시저 아티클입니다.  
  
     게시에 대한 새 아티클을 정의합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
