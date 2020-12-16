---
title: 게시 속성 보기 및 수정 | Microsoft 문서
description: SQL Server Management Studio, Transact-SQL 또는 복제 관리 개체를 사용하여 SQL Server에서 게시 속성을 보고 수정하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing replication properties
- modifying replication properties, articles
- articles [SQL Server replication], modifying
- publications [SQL Server replication], properties
- articles [SQL Server replication], properties
- modifying replication properties, publications
- publications [SQL Server replication], modifying
ms.assetid: 27d72ea4-bcb6-48f2-b4aa-eb1410da7efc
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 83b1d20afdc123359f3b34de90875e7977d7b541
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468894"
---
# <a name="view-and-modify-publication-properties"></a>게시 속성 보기 및 수정
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 게시 속성을 보고 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
-   **게시 속성을 보고 수정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   게시를 만든 다음 일부 속성은 수정할 수 없고, 게시에 대한 구독이 있는 경우에 수정할 수 없는 속성도 있습니다. 수정할 수 없는 속성은 읽기 전용으로 표시됩니다.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   게시가 생성되면 일부 속성 변경으로 인해 새 스냅샷이 필요합니다. 게시에 구독이 있는 경우에는 이러한 변경 내용으로 인해 모든 구독도 다시 초기화해야 합니다. 자세한 내용은 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) 및 [기존 게시에 대한 아티클 추가 및 삭제](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 및 복제 모니터에서 사용할 수 있는 **게시 속성 - \<Publication>** 대화 상자에서 게시 속성을 확인하고 수정할 수 있습니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
 **게시 속성 - \<Publication>** 대화 상자에는 다음 페이지가 포함되어 있습니다.  
  
-   **일반** 페이지에는 게시 이름 및 설명, 데이터베이스 이름, 게시 유형 및 구독 만료 설정이 포함되어 있습니다.  
  
-   **아티클** 페이지는 새 게시 마법사의 **아티클** 페이지에 해당합니다. 이 페이지를 사용하여 아티클을 추가 및 삭제하고 아티클의 속성 및 열 필터링을 변경할 수 있습니다.  
  
-   **행 필터** 페이지는 새 게시 마법사의 **테이블 행 필터** 페이지에 해당합니다. 이 페이지를 사용하여 모든 게시 유형에 대해 정적 행 필터를 추가, 편집 및 삭제하고 병합 게시에 대해 매개 변수가 있는 행 필터 및 조인 필터를 추가, 편집 및 삭제할 수 있습니다.  
  
-   **스냅샷** 페이지를 사용하면 스냅샷의 형식 및 위치, 스냅샷의 압축 여부 및 스냅샷이 적용되기 전과 후에 실행할 스크립트를 지정할 수 있습니다.  
  
-   **FTP 스냅샷** 페이지(SQL Server 2005 이전 버전을 실행하는 게시자에 대한 병합 게시와 스냅샷 및 트랜잭션 게시의 경우)를 사용하면 구독자가 FTP(파일 전송 프로토콜)를 통해 스냅샷 파일을 다운로드할 수 있는지 여부를 지정할 수 있습니다.  
  
-   **FTP 스냅샷 및 인터넷** 페이지(SQL Server 2005 이후 버전을 실행하는 게시자에 대한 병합 게시의 경우)를 사용하면 구독자가 FTP를 통해 스냅샷 파일을 다운로드할 수 있는지 여부와 구독자가 HTTPS를 통해 구독을 동기화할 수 있는지 여부를 지정할 수 있습니다.  
  
-   **구독 옵션** 페이지를 사용하면 모든 구독에 적용되는 여러 옵션을 설정할 수 있습니다. 사용할 수 있는 옵션은 게시 유형에 따라 달라집니다.  
  
-   **게시 액세스 목록** 페이지를 사용하면 게시에 액세스할 수 있는 로그인 및 그룹을 지정할 수 있습니다.  
  
-   **에이전트 보안** 페이지를 사용하여 모든 게시에 대한 스냅샷 에이전트, 모든 트랜잭션 게시에 대한 로그 판독기 에이전트, 지연 업데이트 구독을 허용하는 트랜잭션 게시에 대한 큐 판독기 에이전트 등 실행하고 복제 토폴로지의 컴퓨터에 이러한 에이전트를 연결하는 계정에 대한 설정에 액세스할 수 있습니다.  
  
-   **데이터 파티션** 페이지(SQL Server 2005 이후 버전을 실행하는 게시자의 병합 게시의 경우)를 사용하면 매개 변수가 있는 필터가 있는 게시에 대한 구독자가 스냅샷을 사용할 수 없는 경우 스냅샷을 요청할 수 있는지 여부를 지정할 수 있습니다. 또한 하나 이상의 파티션에 대해 스냅샷을 한 번 또는 되풀이되는 일정에 따라 생성할 수 있습니다.  
  
#### <a name="to-view-and-modify-publication-properties-in-management-studio"></a>Management Studio에서 게시 속성을 보고 수정하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  게시를 마우스 오른쪽 단추로 클릭한 다음 **속성** 을 클릭합니다.  
  
4.  필요한 경우 속성을 수정한 다음 **확인** 을 클릭합니다.  

#### <a name="to-view-and-modify-publication-properties-in-replication-monitor"></a>복제 모니터에서 게시 속성을 보고 수정하려면  
  
1.  복제 모니터의 왼쪽 창에서 게시자 그룹을 확장한 다음 게시자를 확장합니다.  
  
2.  게시를 마우스 오른쪽 단추로 클릭한 다음 **속성** 을 클릭합니다.  
  
3.  필요한 경우 속성을 수정한 다음 **확인** 을 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 게시는 수정할 수 있으며 게시 속성은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 반환할 수 있습니다. 사용하는 저장 프로시저는 게시 유형에 따라 달라집니다.  
  
#### <a name="to-view-the-properties-of-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시의 속성을 확인하려면  
  
1.  **\@publication** 매개 변수에 게시 이름을 지정하여 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행합니다. 이 매개 변수를 지정하지 않으면 게시자에 있는 모든 게시에 대한 정보가 반환됩니다.  
  
#### <a name="to-change-the-properties-of-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시의 속성을 변경하려면  
  
1.  **\@property** 매개 변수에 변경할 게시 속성, **\@value** 매개 변수에 이 속성의 새 값을 지정하여 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)을 실행합니다.  
  
    > [!NOTE]  
    >  변경 시 새 스냅샷을 생성해야 하는 경우 **\@force_invalidate_snapshot** 값도 **1** 로 지정해야 합니다. 변경 시 구독자를 초기화해야 하는 경우 **\@force_reinit_subscription** 에 값 **1** 을 지정해야 합니다. 변경된 경우 새 스냅샷 또는 다시 초기화가 필요한 속성에 대한 자세한 내용은 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
#### <a name="to-view-the-properties-of-a-merge-publication"></a>병합 게시의 속성을 확인하려면  
  
1.  **\@publication** 매개 변수에 게시 이름을 지정하여 [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)을 실행합니다. 이 매개 변수를 지정하지 않으면 게시자에 있는 모든 게시에 대한 정보가 반환됩니다.  
  
#### <a name="to-change-the-properties-of-a-merge-publication"></a>병합 게시의 속성을 변경하려면  
  
1.  **\@property** 매개 변수에 변경할 게시 속성, **\@value** 매개 변수에 이 속성의 새 값을 지정하여 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)을 실행합니다.  
  
    > [!NOTE]  
    >  변경 시 새 스냅샷을 생성해야 하는 경우 **\@force_invalidate_snapshot** 값도 **1** 로 지정해야 합니다. 변경 시 구독자를 초기화해야 하는 경우 **\@force_reinit_subscription** 에 값 **1** 을 지정해야 합니다. 변경 시 새 스냅샷 또는 재초기화가 필요한 속성에 관한 자세한 내용은 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
#### <a name="to-view-the-properties-of-a-snapshot"></a>스냅샷의 속성을 확인하려면  
  
1.  **\@publication** 매개 변수에 게시 이름을 지정하여 [sp_helppublication_snapshot](../../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md)을 실행합니다.  
  
#### <a name="to-change-the-properties-of-a-snapshot"></a>스냅샷의 속성을 변경하려면  
  
1.  적절한 스냅샷 매개 변수에 하나 이상의 새 스냅샷 속성을 지정하여 [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)을 실행합니다.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 트랜잭션 복제 예에서는 게시 속성을 반환합니다.  
  
 [!code-sql[HowTo#sp_helppublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_1.sql)]  
  
 다음 트랜잭션 복제 예에서는 게시에 대한 스키마 복제를 해제합니다.  
  
 [!code-sql[HowTo#sp_changepublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_2.sql)]  
  
 다음 병합 복제 예에서는 게시 속성을 반환합니다.  
  
 [!code-sql[HowTo#sp_helpmergepublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_3.sql)]  
  
 다음 병합 복제 예에서는 게시에 대한 스키마 복제를 해제합니다.  
  
 [!code-sql[HowTo#sp_changemergepublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_4.sql)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 게시를 수정하고 해당 속성에 액세스할 수 있습니다. 게시 속성을 보거나 수정하는 데 사용되는 RMO 클래스는 게시의 유형에 따라 달라집니다.  
  
#### <a name="to-view-or-modify-properties-of-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시의 속성을 보거나 수정하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 만들고 게시에 대한 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정한 다음, 1단계에서 만든 연결에 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 **false** 를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  (옵션) 속성을 변경하려면 설정할 수 있는 한 개 이상의 속성에 대해 새 값을 설정합니다. 논리 AND 연산자(Microsoft Visual C#에서는 **&** , Microsoft Visual Basic에서는 **And** )를 사용하여 지정된 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 값이 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 속성에 대해 설정되어 있는지 확인할 수 있습니다. 포함 논리 OR 연산자(Visual C#에서는 **|** , Visual Basic에서는 **Or** ) 및 배타적 논리 OR 연산자(Visual C#에서는 **^** , Visual Basic에서는 **Xor** )를 사용하여 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 속성에 대한 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 속성에 대해 설정되어 있는지 확인할 수 있습니다.  
  
5.  (옵션) **P:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges** 값도 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>값을 지정했으면 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 호출하여 서버의 변경 내용을 커밋합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>에 대해 **false** 값(기본값)을 지정했으면 변경 내용이 즉시 서버로 전송됩니다.  
  
#### <a name="to-view-or-modify-properties-of-a-merge-publication"></a>병합 게시의 속성을 보거나 수정하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만들고 게시에 대한 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정한 다음, 1단계에서 만든 연결에 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 **false** 를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  (옵션) 속성을 변경하려면 설정할 수 있는 한 개 이상의 속성에 대해 새 값을 설정합니다. 논리 AND 연산자(Microsoft Visual C#에서는 **&** , Visual Basic에서는 **And** )를 사용하여 지정된 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 값이 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 속성에 대해 설정되어 있는지 확인할 수 있습니다. 포함 논리 OR 연산자(Visual C#에서는 **|** , Visual Basic에서는 **Or** ) 및 배타적 논리 OR 연산자(Visual C#에서는 **^** , Visual Basic에서는 **Xor** )를 사용하여 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 속성에 대한 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 속성에 대해 설정되어 있는지 확인할 수 있습니다.  
  
5.  (옵션) **P:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges** 값도 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>값을 지정했으면 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 호출하여 서버의 변경 내용을 커밋합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>에 대해 **false** 값(기본값)을 지정했으면 변경 내용이 즉시 서버로 전송됩니다.  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> 예(RMO)  
 이 예에서는 트랜잭션 게시에 대한 게시 특성을 설정합니다. 변경 내용은 명시적으로 서버로 전송될 때까지 캐시됩니다.  
  
 [!code-cs[HowTo#rmo_ChangeTranPub_cached](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changetranpub_cached)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeTranPub_cached](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changetranpub_cached)]  
  
 이 예에서는 병합 게시에 대한 DDL 복제를 해제합니다.  
  
 [!code-cs[HowTo#rmo_ChangeMergePub_ddl](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergepub_ddl)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergePub_ddl](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergepub_ddl)]  
  
## <a name="see-also"></a>참고 항목  
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [게시 데이터베이스의 스키마 변경](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [게시에 대한 아티클 추가 및 삭제&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)   
 [복제 모니터를 사용하여 정보 보기 및 태스크 수행](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [아티클 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  
