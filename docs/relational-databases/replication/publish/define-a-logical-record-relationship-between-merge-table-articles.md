---
title: "병합 테이블 아티클 간의 논리적 레코드 관계 정의 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "병합 복제 논리적 레코드 [SQL Server 복제]"
  - "아티클, [SQL Server 복제], 논리적 레코드"
  - "논리적 레코드 [SQL Server 복제]"
ms.assetid: ff847b3a-c6b0-4eaf-b225-2ffc899c5558
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 병합 테이블 아티클 간의 논리적 레코드 관계 정의
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 테이블 아티클 간 논리적 레코드 관계를 정의하는 방법에 대해 설명합니다.  
  
 병합 복제를 사용하면 서로 다른 테이블에 있는 관련 행 간의 관계를 정의할 수 있습니다. 그러면 동기화 중에 이러한 행을 하나의 트랜잭션 단위로 처리할 수 있습니다. 논리적 레코드는 조인 필터 관계가 있는지 여부와 관계없이 두 아티클 간에 정의할 수 있습니다. 자세한 내용은 참조 [그룹 변경 내용을 논리적 레코드와 관련 된 행에](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
-   **다음을 사용하여 병합 테이블 아티클 간의 논리적 레코드 관계를 정의하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   게시에 대한 구독이 초기화된 후 논리적 레코드를 추가, 수정 또는 삭제한 경우에는 변경 내용을 적용한 후에 새 스냅숏을 생성하고 모든 구독을 다시 초기화해야 합니다. 속성 변경에 대 한 요구 사항에 대 한 자세한 내용은 참조 [변경 게시 및 아티클 속성](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 논리적 레코드를 정의 **조인 추가** 새 게시 마법사에서 사용할 수 있는 대화 상자 및 **게시 속성-\< 게시>** 대화 상자입니다. 마법사를 사용 하 고 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [게시를 만들](../../../relational-databases/replication/publish/create-a-publication.md) 및 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
 논리적 레코드가 병합 게시의 조인 필터에 적용되고 게시가 사전 계산 파티션을 사용하기 위한 요구 사항을 따르는 경우에만 **조인 추가** 대화 상자에서 논리적 레코드를 정의할 수 있습니다. 조인 필터에 적용되지 않는 논리적 레코드를 정의하고 논리적 레코드 수준에서 충돌 감지 및 해결을 설정하려면 저장 프로시저를 사용해야 합니다.  
  
#### 논리적 레코드 관계를 정의하려면  
  
1.  에 **테이블 행 필터** 새 게시 마법사의 페이지 또는 **행 필터** 의 페이지는 **게시 속성-\< 게시>** 대화 상자에서 행 필터를 **필터링 된 테이블** 창입니다.  
  
     논리적 레코드 관계는 조인 필터와 연결된 행 필터를 확장합니다. 따라서 조인 필터로 확장하기 전에 행 필터를 정의한 다음 논리적 레코드 관계를 적용해야 합니다. 한 조인 필터를 정의한 후에 다른 조인 필터를 사용하여 이 조인 필터를 확장할 수 있습니다. 조인 필터 정의 방법은 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)을 참조하세요.  
  
2.  **추가**를 클릭한 다음 **선택한 필터 확장을 위해 조인 추가**를 클릭합니다.  
  
3.  **조인 추가** 대화 상자에서 조인 필터를 정의한 다음 **논리적 레코드**확인란을 선택합니다.  
  
4.  있는 경우는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **확인** 저장 하 고 대화 상자를 닫습니다.  
  
#### 논리적 레코드 관계를 삭제하려면  
  
-   논리적 레코드 관계만 삭제하거나 논리적 레코드 관계 및 이와 관련된 조인 필터를 함께 삭제합니다.  
  
     논리적 레코드 관계만 삭제하려면  
  
    1.  에 **행 필터** 새 게시 마법사의 페이지 또는 **행 필터** 의 페이지는 **게시 속성-\< 게시>** 대화 상자에서 논리적 레코드 관계와 관련 된 조인 필터는 **필터링 된 테이블** 창과 클릭 한 다음 **편집**합니다.  
  
    2.  **조인 편집** 대화 상자에서 **논리적 레코드**확인란 선택을 취소합니다.  
  
    3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     논리적 레코드 관계 및 이와 관련된 조인 필터를 함께 삭제하려면  
  
    -   에 **행 필터** 새 게시 마법사의 페이지 또는 **게시 속성-\< 게시>** 대화 상자, 필터를는 **필터링 된 테이블** 창과 클릭 한 다음 **삭제**합니다. 삭제하는 조인 필터가 다른 조인에 의해 확장된 경우 해당 조인 또한 삭제됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 아티클 간 논리적 레코드 관계를 프로그래밍 방식으로 지정할 수 있습니다.  
  
#### 관련된 조인 필터 없이 논리적 레코드 관계를 정의하려면  
  
1.  게시 된 필터링 된 아티클이 있으면 실행 [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), 의 값을 확인 하 고 **use_partition_groups** 결과 집합에서.  
  
    -   이 값이 **1**이면 사전 계산 파티션이 이미 사용되고 있는 것입니다.  
  
    -   값이 **0**, 다음 실행 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 게시 데이터베이스의 게시자에서. 값을 지정 **use_partition_groups** 에 대 한 **@property** 값 **true** 에 대 한 **@value**합니다.  
  
        > [!NOTE]  
        >  게시에서 사전 계산 파티션을 지원하지 않으면 논리적 레코드를 사용할 수 없습니다. 자세한 내용은 항목에서 사전 계산 파티션을 사용에 대 한 요구 사항을 참조 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)합니다.  
  
    -   이 값이 NULL이면 스냅숏 에이전트를 실행하여 게시에 대한 초기 스냅숏을 생성해야 합니다.  
  
2.  논리적 레코드를 구성 하는 문서가 존재 하지 않는 경우 실행 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 게시 데이터베이스의 게시자에서. 논리적 레코드에 대해 다음 충돌 감지 및 해결 옵션 중 하나를 지정합니다.  
  
    -   찾아 논리적 레코드의 관련된 행 내에서 발생 하는 충돌을 해결 하는 값을 지정 **true** 에 대 한 **@logical_record_level_conflict_detection** 및 **@logical_record_level_conflict_resolution**합니다.  
  
    -   표준 행 또는 열 수준의 충돌 감지 및 해결을 사용 하려면 값을 지정 **false** 에 대 한 **@logical_record_level_conflict_detection** 및 **@logical_record_level_conflict_resolution**, 기본값입니다.  
  
3.  논리적 레코드를 구성하는 각 아티클에 대해 2단계를 반복합니다. 논리적 레코드의 각 아티클에 대해 동일한 충돌 감지 및 해결 옵션을 사용해야 합니다. 자세한 내용은 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md)을 참조하세요.  
  
4.  게시 데이터베이스의 게시자에서 실행 [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)합니다. 지정 **@publication**, 문서에 대 한 관계의 이름을 **@article**, 에 대 한 두 번째 아티클의 이름을 **@join_articlename**, 에 대 한 관계에 대 한 이름을 **@filtername**, 둘 사이의 관계를 정의 하는 절에 대 한 문서 **@join_filterclause**, 에 대 한 조인 유형을 **@join_unique_key** 는 다음 값 중 하나에 대 한 고 **@filter_type**:  
  
    -   **2** -논리적 관계를 정의 합니다.  
  
    -   **3** -조인 필터와 논리적 관계를 정의 합니다.  
  
    > [!NOTE]  
    >  조인 필터를 사용하지 않는 경우 두 아티클 간의 관계 방향은 중요하지 않습니다.  
  
5.  게시에서 남은 각각의 논리적 레코드 관계에 대해 2단계를 반복합니다.  
  
#### 논리적 레코드에 대한 충돌 감지 및 해결을 변경하려면  
  
1.  논리적 레코드의 관련 행 내에서 발생하는 충돌을 감지하고 해결하려면 다음을 수행합니다.  
  
    -   게시 데이터베이스의 게시자에서 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)합니다. 값을 지정 **logical_record_level_conflict_detection** 에 대 한 **@property** 값 **true** 에 대 한 **@value**합니다. 값을 지정 **1** 에 대 한 **@force_invalidate_snapshot** 및 **@force_reinit_subscription**합니다.  
  
    -   게시 데이터베이스의 게시자에서 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)합니다. 값을 지정 **logical_record_level_conflict_resolution** 에 대 한 **@property** 값 **true** 에 대 한 **@value**합니다. 값을 지정 **1** 에 대 한 **@force_invalidate_snapshot** 및 **@force_reinit_subscription**합니다.  
  
2.  표준 행 수준 또는 열 수준의 충돌 감지 및 해결을 사용하려면 다음을 수행합니다.  
  
    -   게시 데이터베이스의 게시자에서 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)합니다. 값을 지정 **logical_record_level_conflict_detection** 에 대 한 **@property** 값 **false** 에 대 한 **@value**합니다. 값을 지정 **1** 에 대 한 **@force_invalidate_snapshot** 및 **@force_reinit_subscription**합니다.  
  
    -   게시 데이터베이스의 게시자에서 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)합니다. 값을 지정 **logical_record_level_conflict_resolution** 에 대 한 **@property** 값 **false** 에 대 한 **@value**합니다. 값을 지정 **1** 에 대 한 **@force_invalidate_snapshot** 및 **@force_reinit_subscription**합니다.  
  
#### 논리적 레코드 관계를 제거하려면  
  
1.  게시 데이터베이스의 게시자에서 다음 쿼리를 실행하여 지정된 게시에 대해 정의된 모든 논리적 레코드 관계 정보를 반환합니다.  
  
     [!code-sql[HowTo#sp_ReturnMergeLogicalRecords](../../../relational-databases/replication/codesnippet/tsql/define-a-logical-record-_1.sql)]  
  
     결과 집합의 **filtername** 열에서 제거되고 있는 논리적 레코드 관계의 이름을 확인합니다.  
  
    > [!NOTE]  
    >  이 쿼리는 동일한 정보를 반환 합니다. [sp_helpmergefilter](../../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md); 하지만이 시스템 저장 프로시저도 조인 필터는 논리적 레코드 관계에 대 한 정보를 반환 합니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_dropmergefilter](../../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)합니다. **@publication**을 지정하고 **@article**에 대해 관계 구성 아티클 중 하나의 이름을, **@filtername**에 대해 1단계에서 사용된 관계의 이름을 지정합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예에서는 기존 게시에 사전 계산 파티션을 사용하고 `SalesOrderHeader` 및 `SalesOrderDetail` 테이블에 대한 두 개의 새 아티클을 구성하는 논리적 레코드를 만듭니다.  
  
 [!code-sql[HowTo#sp_AddMergeLogicalRecord](../../../relational-databases/replication/codesnippet/tsql/define-a-logical-record-_2.sql)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
  
> [!NOTE]  
>  병합 복제를 사용하면 충돌을 추적하고 논리적 레코드 수준에서 충돌을 해결하도록 지정할 수도 있지만 RMO를 사용하는 경우에는 이러한 옵션을 설정할 수 없습니다.  
  
#### 관련된 조인 필터 없이 논리적 레코드 관계를 정의하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스를 설정는 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 게시 및 설정에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1 단계에서 만든 연결 합니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  하는 경우는 <xref:Microsoft.SqlServer.Replication.MergePublication.PartitionGroupsOption%2A> 속성이 <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.False>, 를로 설정 <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.True>합니다.  
  
5.  논리적 레코드를 구성 하는 아티클이 존재 하지 않는 경우의 인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergeArticle> 클래스를 다음 속성을 설정 합니다.  
  
    -   에 대 한 아티클의 이름을 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>합니다.  
  
    -   에 대 한 게시의 이름 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>합니다.  
  
    -   (선택 사항) 아티클이 행 필터링 되는 경우에 대 한 행 필터 절을 지정 된 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 속성입니다. 이 속성을 사용하여 정적 또는 매개 변수가 있는 행 필터를 지정합니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)을 참조하세요.  
  
     자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
6.  호출 된 <xref:Microsoft.SqlServer.Replication.Article.Create%2A> 메서드.  
  
7.  논리적 레코드를 구성하는 각 아티클별로 5단계와 6단계를 반복합니다.  
  
8.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 아티클 간의 논리적 레코드 관계를 정의 하는 클래스입니다. 그런 후 다음 속성을 설정합니다.  
  
    -   에 대 한 논리적 레코드 관계의 자식 아티클의 이름을 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.ArticleName%2A> 속성입니다.  
  
    -   논리적 레코드 관계에 대 한 기존 상위 아티클 이름은 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinArticleName%2A> 속성입니다.  
  
    -   에 대 한 논리적 레코드 관계에 대 한 이름을 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterName%2A> 속성입니다.  
  
    -   에 대 한 관계를 정의 하는 식의 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinFilterClause%2A> 속성입니다.  
  
    -   값이 <xref:Microsoft.SqlServer.Replication.FilterTypes.LogicalRecordLink> 에 대 한는 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterTypes%2A> 속성입니다. 논리적 레코드 관계는 조인 필터 이기도 한 경우이 값을 지정 <xref:Microsoft.SqlServer.Replication.FilterTypes.JoinFilterAndLogicalRecordLink> 이 속성에 대 한 합니다. 자세한 내용은 참조 [그룹 변경 내용을 논리적 레코드와 관련 된 행에](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)합니다.  
  
9. 호출의 <xref:Microsoft.SqlServer.Replication.MergeArticle.AddMergeJoinFilter%2A> 관계의 하위 아티클을 나타내는 개체 메서드를 호출 합니다. 전달 된 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 관계를 정의 하는 8 단계에서 개체입니다.  
  
10. 게시의 나머지 논리적 레코드 관계별로 8단계와 9단계를 반복합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 이 예제에서는 `SalesOrderHeader` 및 `SalesOrderDetail` 테이블의 새 아티클 두 개를 구성하는 논리적 레코드를 만듭니다.  
  
 [!code-csharp[HowTo#rmo_CreateLogicalRecord](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createlogicalrecord)]  
  
 [!code-vb[HowTo#rmo_vb_CreateLogicalRecord](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createlogicalrecord)]  
  
## 참고 항목  
 [병합 아티클 사이에서 조인 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [정적 행 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)   
 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)   
 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)  
  
  