---
title: 아티클 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], dropping
- sp_droparticle
- sp_dropmergearticle
- deleting articles
- removing articles
- dropping articles
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: d03b0e8d21414101940e4eb653e8f9a7fa3d2d30
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76287685"
---
# <a name="delete-an-article"></a>아티클 삭제
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 에서 아티클을 삭제하는 방법에 대해 설명합니다. 아티클을 삭제할 수 있는 조건 및 아티클 삭제로 인해 새 스냅샷 또는 구독 다시 초기화가 필요한지 여부에 대한 자세한 내용은 [기존 게시에 대한 아티클 추가 및 삭제](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
 **항목 내용**  
  
-   **아티클을 삭제하려면:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 아티클은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 삭제할 수 있습니다. 사용되는 저장 프로시저는 아티클이 속한 게시 유형에 따라 달라집니다.  
  
#### <a name="to-delete-an-article-from-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시에서 아티클을 삭제하려면  
  
1.  [sp_droparticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)을 실행하여 **\@publication**로 지정된 게시에서 **\@article**으로 지정된 아티클을 삭제합니다. **\@force_invalidate_snapshot** 값을 **1**로 지정합니다.  
  
2.  (옵션) 게시된 개체를 데이터베이스에서 완전히 제거하려면 게시 데이터베이스의 게시자에서 `DROP <objectname>` 명령을 실행합니다.  

#### <a name="to-delete-an-article-from-a-merge-publication"></a>병합 게시에서 아티클을 삭제하려면  
  
1.  [sp_dropmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)을 실행하여 **\@publication**로 지정된 게시에서 **\@article**으로 지정된 아티클을 삭제합니다. 필요한 경우 **\@force_invalidate_snapshot**에 값 **1**을 지정하고 **\@force_reinit_subscription**에 값 **1**을 지정합니다.  
  
2.  (옵션) 게시된 개체를 데이터베이스에서 완전히 제거하려면 게시 데이터베이스의 게시자에서 `DROP <objectname>` 명령을 실행합니다.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 트랜잭션 게시에서 아티클을 삭제합니다. 이로 인해 기존 스냅샷이 무효화되므로 **\@force_invalidate_snapshot** 매개 변수 값이 **1**로 지정됩니다.  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article AS sysname;  
SET @publication = N'AdvWorksProductTran';   
SET @article = N'Product';   
  
-- Drop the transactional article.  
USE [AdventureWorks]  
EXEC sp_droparticle   
  @publication = @publication,   
  @article = @article,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
 다음 예에서는 병합 게시에서 두 개의 아티클을 삭제합니다. 이로 인해 기존 스냅샷이 무효화되므로 **\@force_invalidate_snapshot** 매개 변수 값이 **1**로 지정됩니다.  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article1 AS sysname;  
DECLARE @article2 AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @article1 = N'SalesOrderDetail';   
SET @article2 = N'SalesOrderHeader';   
  
-- Remove articles from a merge publication.  
USE [AdventureWorks]  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article1,  
  @force_invalidate_snapshot = 1;  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article2,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 아티클을 삭제할 수 있습니다. 아티클을 삭제하는 데 사용하는 RMO 클래스는 아티클이 속한 게시 유형에 따라 달라집니다.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시에 속한 아티클을 삭제하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransArticle> 클래스의 인스턴스를 만듭니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>및 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 속성을 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성에 대해 1단계에서 만든 연결을 설정합니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 속성을 확인하여 아티클이 존재하는지 확인합니다. 이 속성의 값이 **false**이면 3단계에서 아티클 속성이 올바르게 정의되지 않았거나 아티클이 없는 것입니다.  
  
6.  <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> 메서드를 호출합니다.  
  
7.  모든 연결을 닫습니다.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-merge-publication"></a>병합 게시에 속한 아티클을 삭제하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeArticle> 클래스의 인스턴스를 만듭니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>및 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 속성을 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성에 대해 1단계에서 만든 연결을 설정합니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 속성을 확인하여 아티클이 존재하는지 확인합니다. 이 속성의 값이 **false**이면 3단계에서 아티클 속성이 올바르게 정의되지 않았거나 아티클이 없는 것입니다.  
  
6.  <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> 메서드를 호출합니다.  
  
7.  모든 연결을 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
 [기존 게시에 대한 아티클 추가 및 삭제](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
