---
title: "아티클 속성 보기 및 수정 | Microsoft Docs"
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
  - "sp_changearticle"
  - "sp_helparticle"
  - "복제 속성 보기"
  - "sp_changemergearticle"
  - "sp_helpmergearticle"
  - "복제 속성 수정, 아티클"
  - "아티클 [SQL Server 복제], 수정"
  - "아티클 [SQL Server 복제], 속성"
ms.assetid: e71831fa-3d39-4e4a-9706-4d3a497082cc
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 아티클 속성 보기 및 수정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 에서 아티클 속성을 보고 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 아티클 속성을 보고 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   게시를 만든 다음 일부 속성은 수정할 수 없고, 게시에 대한 구독이 있는 경우에 수정할 수 없는 속성도 있습니다. 수정할 수 없는 속성은 읽기 전용으로 표시됩니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   게시가 생성되면 일부 속성 변경으로 인해 새 스냅숏이 필요합니다. 게시에 구독이 있는 경우에는 이러한 변경 내용으로 인해 모든 구독도 다시 초기화해야 합니다. 자세한 내용은 참조 [변경 게시 및 아티클 속성](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) 및 [기사를 추가 하 고 기존 게시에서 아티클을 삭제할](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 문서 속성 보기 및 수정 된 **게시 속성-\< 게시>** 대화 상자에서 사용할 수 있는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 및 복제 모니터 합니다. 복제 모니터를 시작 하는 방법에 대 한 정보를 참조 하십시오. [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)합니다.  
  
-   **일반** 페이지에는 게시 이름 및 설명, 데이터베이스 이름, 게시 유형 및 구독 만료 설정이 포함되어 있습니다.  
  
-   **아티클** 페이지는 새 게시 마법사의 **아티클** 페이지에 해당합니다. 이 페이지를 사용하여 아티클을 추가 및 삭제하고 아티클의 속성 및 열 필터링을 변경할 수 있습니다.  
  
-   **행 필터** 페이지는 새 게시 마법사의 **테이블 행 필터** 페이지에 해당합니다. 이 페이지를 사용하여 모든 게시 유형에 대해 정적 행 필터를 추가, 편집 및 삭제하고 병합 게시에 대해 매개 변수가 있는 행 필터 및 조인 필터를 추가, 편집 및 삭제할 수 있습니다.  
  
-   **스냅숏** 페이지를 사용하면 스냅숏의 형식 및 위치, 스냅숏의 압축 여부 및 스냅숏이 적용되기 전과 후에 실행할 스크립트를 지정할 수 있습니다.  
  
-    **FTP 스냅숏** 페이지 (스냅숏 및 트랜잭션 게시 및 SQL Server 2005 이전 버전을 실행 하는 게시자에 대 한 병합 게시)을 사용 하면 구독자가 스냅숏 파일을 통해 FTP 파일 전송 프로토콜 ()를 다운로드할 수 있는지 여부를 지정할 수 있습니다.  
  
-    **FTP 스냅숏 및 인터넷** 페이지 (SQL Server 2005 이상을 실행 하는 게시자의 병합 게시)을 사용 하면 구독자가 FTP 통해 스냅숏 파일을 다운로드할 수 있는지 여부와 구독자가 HTTPS 통해 구독 동기화 할 수 있는지 여부를 지정할 수 있습니다.  
  
-   **구독 옵션** 페이지를 사용하면 모든 구독에 적용되는 여러 옵션을 설정할 수 있습니다. 사용할 수 있는 옵션은 게시 유형에 따라 달라집니다.  
  
-   **게시 액세스 목록** 페이지를 사용하면 게시에 액세스할 수 있는 로그인 및 그룹을 지정할 수 있습니다.  
  
-   **에이전트 보안** 페이지를 사용하여 모든 게시에 대한 스냅숏 에이전트, 모든 트랜잭션 게시에 대한 로그 판독기 에이전트, 지연 업데이트 구독을 허용하는 트랜잭션 게시에 대한 큐 판독기 에이전트 등 실행하고 복제 토폴로지의 컴퓨터에 이러한 에이전트를 연결하는 계정에 대한 설정에 액세스할 수 있습니다.  
  
-    **데이터 파티션을** 페이지 (SQL Server 2005 이상을 실행 하는 게시자의 병합 게시)을 사용 하면 매개 변수가 있는 필터로 게시에 대 한 구독자 하나를 사용할 수 없는 경우 스냅숏을 요청할 수 있는지 여부를 지정할 수 있습니다. 또한 하나 이상의 파티션에 대해 스냅숏을 한 번 또는 되풀이되는 일정에 따라 생성할 수 있습니다.  
  
#### 아티클 속성을 보고 수정하려면  
  
1.  에 **문서** 의 페이지는 **게시 속성-\< 게시>** 대화 상자는 문서를 선택 하 고 클릭 **아티클 속성**합니다.  
  
2.  속성 변경 내용을 적용할 아티클을 다음과 같이 선택합니다.  
  
    -   클릭 **설정의 강조 표시 된 속성 \< ObjectType> 문서** 시작 하는 **아티클 속성-\< o b j>** 대화 상자, 속성이 대화 상자에서 변경한 내용을에 포함 된 개체 창에서 강조 표시 하는 개체에만 적용 됩니다는 **문서** 페이지입니다.  
  
    -   클릭 **설정 속성의 모든 \< ObjectType> 문서**, 시작 하는 **모든 속성을 \< ObjectType> 문서** 대화 상자, 속성이 대화 상자에서 변경한 내용을에 개체 창에 있는 해당 유형의 모든 개체에 적용 되는 **문서** 게시에 대 한 선택 하지 않은 것을 포함 하 여 페이지.  
  
        > [!NOTE]  
        >  속성 변경 내용에서 **모든 속성을 \< ObjectType> 문서** 대화 상자에서 이전에 수행 된 모든 재정의 **아티클 속성-\< o b j>** 대화 상자. 예를 들어 특정 개체 유형의 모든 아티클에 대해 여러 기본값을 설정하고 개별 개체에 대해 일부 속성도 설정하려면 먼저 모든 아티클의 기본값을 설정합니다. 그런 다음 개별 개체에 대해 속성을 설정합니다.  
  
3.  필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
4.  클릭 **확인** 에 **게시 속성-\< 게시>** 대화 상자입니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 아티클은 수정할 수 있으며 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 해당 속성을 반환할 수 있습니다. 사용되는 저장 프로시저는 아티클이 속한 게시 유형에 따라 달라집니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 속한 아티클의 속성을 보려면  
  
1.  실행 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md), 에 대 한 게시의 이름을 지정 하는 **@publication** 아티클 이름과 매개 변수는 **@article** 매개 변수입니다. **@article**을 지정하지 않으면 게시의 모든 아티클에 대한 정보가 반환됩니다.  
  
2.  실행 [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) 에 대 한 테이블 아티클의 기본 테이블에서 사용할 수 있는 모든 열을 나열 합니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 속한 아티클의 속성을 수정하려면  
  
1.  실행 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md), 에서 변경 되는 문서 속성을 지정 하는 **@property** 에서이 속성의 새 값 및 매개 변수는 **@value** 매개 변수입니다.  
  
    > [!NOTE]  
    >  값도 지정 해야 변경이 필요한 경우 새 스냅숏 생성, **1** 에 대 한 **@force_invalidate_snapshot**, 그리고 값도 지정 해야 변경 내용을 구독자를 초기화 해야 데이터 필요로 하는 경우 **1** 에 대 한 **@force_reinit_subscription**합니다. 속성에 대 한 자세한 내용은 그 변경 되 면 필요한 새 스냅숏 또는 재초기화, 참조 [변경 게시 및 아티클 속성](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)합니다.  
  
#### 병합 게시에 속한 아티클의 속성을 보려면  
  
1.  실행 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md), 에 대 한 게시의 이름을 지정 하는 **@publication** 아티클 이름과 매개 변수는 **@article** 매개 변수입니다. 이러한 매개 변수를 지정하지 않으면 게시 또는 게시자에 있는 모든 아티클에 대한 정보가 반환됩니다.  
  
2.  실행 [sp_helpmergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-helpmergearticlecolumn-transact-sql.md) 에 대 한 테이블 아티클의 기본 테이블에서 사용할 수 있는 모든 열을 나열 합니다.  
  
#### 병합 게시에 속한 아티클의 속성을 수정하려면  
  
1.  실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), 에서 변경 되는 문서 속성을 지정 하는 **@property** 에서이 속성의 새 값 및 매개 변수는 **@value** 매개 변수입니다.  
  
    > [!NOTE]  
    >  값도 지정 해야 변경이 필요한 경우 새 스냅숏 생성, **1** 에 대 한 **@force_invalidate_snapshot**, 그리고 값도 지정 해야 변경 내용을 구독자를 초기화 해야 데이터 필요로 하는 경우 **1** 에 대 한 **@force_reinit_subscription**합니다. 속성에 대 한 자세한 내용은 그 변경 되 면 필요한 새 스냅숏 또는 재초기화, 참조 [변경 게시 및 아티클 속성](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 트랜잭션 복제 예에서는 게시된 아티클의 속성을 반환합니다.  
  
 [!code-sql[HowTo#sp_helptranarticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_1.sql)]  
  
 이 트랜잭션 복제 예에서는 게시된 아티클에 대한 스키마 옵션을 변경합니다.  
  
 [!code-sql[HowTo#sp_changetranarticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_2.sql)]  
  
 이 병합 복제 예에서는 게시된 아티클의 속성을 반환합니다.  
  
 [!code-sql[HowTo#sp_helpmergearticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_3.sql)]  
  
 이 병합 복제 예에서는 게시된 아티클에 대한 충돌 검색 설정을 변경합니다.  
  
 [!code-sql[HowTo#sp_changemergearticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_4.sql)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 아티클을 수정하고 해당 속성에 액세스할 수 있습니다. 아티클 속성을 보거나 수정하는 데 사용되는 RMO 클래스는 아티클이 속한 게시 유형에 따라 달라집니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 속하는 아티클의 속성을 보거나 수정하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransArticle> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, 및 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 속성입니다.  
  
4.  설정에 대해 1 단계에서 만든 연결의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성입니다.  
  
5.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 3단계에서 아티클 속성이 올바르게 정의되지 않았거나 아티클이 없습니다.  
  
6.  (선택 사항) 속성을 변경 하려면 중 하나에 대 한 새 값을 설정 된 <xref:Microsoft.SqlServer.Replication.TransArticle> 속성을 설정할 수 있습니다.  
  
7.  (선택 사항) 값을 지정한 경우 **true** 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, 호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 서버에 변경 내용을 적용 합니다. 값을 지정한 경우 **false** 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (기본값) 이면 변경 내용이 서버에 즉시 보내집니다.  
  
#### 병합 게시에 속하는 아티클의 속성을 보거나 수정하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergeArticle> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, 및 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 속성입니다.  
  
4.  설정에 대해 1 단계에서 만든 연결의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성입니다.  
  
5.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 3단계에서 아티클 속성이 올바르게 정의되지 않았거나 아티클이 없습니다.  
  
6.  (선택 사항) 속성을 변경 하려면 중 하나에 대 한 새 값을 설정 된 <xref:Microsoft.SqlServer.Replication.MergeArticle> 속성을 설정할 수 있습니다.  
  
7.  (선택 사항) 값을 지정한 경우 **true** 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, 호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 서버에 변경 내용을 적용 합니다. 값을 지정한 경우 **false** 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (기본값) 이면 변경 내용이 서버에 즉시 보내집니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 다음 예에서는 병합 아티클을 변경하여 아티클에서 사용하는 비즈니스 논리 처리기를 지정합니다.  
  
 [!code-csharp[HowTo#rmo_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## 참고 항목  
 [병합 아티클에 대한 비즈니스 논리 처리기 구현](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [고급 병합 복제 충돌 감지 및 해결](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  