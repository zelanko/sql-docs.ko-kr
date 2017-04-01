---
title: "아티클 삭제 | Microsoft Docs"
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
  - "아티클 [SQL Server 복제], 삭제"
  - "sp_droparticle"
  - "sp_dropmergearticle"
  - "아티클 삭제"
  - "아티클 제거"
  - "아티클 삭제"
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# 아티클 삭제
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 아티클을 삭제하는 방법에 대해 설명합니다. 아티클을 삭제할 수 및 필요한 지 여부 아티클을 삭제 하면 새 스냅숏 또는 구독을 다시 초기화에서 조건에 대 한 정보를 참조 하십시오. [기사를 추가 하 고 기존 게시에서 아티클을 삭제할](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)합니다.  
  
 **항목 내용**  
  
-   **아티클을 삭제하려면:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 아티클은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 삭제할 수 있습니다. 사용되는 저장 프로시저는 아티클이 속한 게시 유형에 따라 달라집니다.  
  
#### 스냅숏 또는 트랜잭션 게시에서 아티클을 삭제하려면  
  
1.  실행 [sp_droparticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md) 지정 된 아티클을 삭제 하려면 **@article**, 지정 된 게시에서 **@publication**합니다. 값을 지정 **1** 에 대 한 **@force_invalidate_snapshot**합니다.  
  
2.  (옵션) 게시된 개체를 데이터베이스에서 완전히 제거하려면 게시 데이터베이스의 게시자에서 `DROP <objectname>` 명령을 실행합니다.  
  
#### 병합 게시에서 아티클을 삭제하려면  
  
1.  실행 [sp_dropmergearticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) 지정 된 아티클을 삭제 하려면 **@article**, 지정 된 게시에서 **@publication**합니다. 필요한 경우 값을 지정 **1** 에 대 한 **@force_invalidate_snapshot** 값 **1** 에 대 한 **@force_reinit_subscription**합니다.  
  
2.  (옵션) 게시된 개체를 데이터베이스에서 완전히 제거하려면 게시 데이터베이스의 게시자에서 `DROP <objectname>` 명령을 실행합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 트랜잭션 게시에서 아티클을 삭제합니다. 이 값이 기존 스냅숏이 무효화 되므로 **1** 에 대해 지정 된는 **@force_invalidate_snapshot** 매개 변수입니다.  
  
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
  
 다음 예에서는 병합 게시에서 두 개의 아티클을 삭제합니다. 값이 기존 스냅숏이 무효화 되므로 **1** 에 대해 지정 된 **@force_invalidate_snapshot** 매개 변수.  
  
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
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 아티클을 삭제할 수 있습니다. 아티클을 삭제하는 데 사용하는 RMO 클래스는 아티클이 속한 게시 유형에 따라 달라집니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 속한 아티클을 삭제하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransArticle> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, 및 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 속성입니다.  
  
4.  설정에 대해 1 단계에서 만든 연결의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성입니다.  
  
5.  확인 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 문서 있는지 확인 하는 속성입니다. 이 속성의 값이 **false**이면 3단계에서 아티클 속성이 올바르게 정의되지 않았거나 아티클이 없는 것입니다.  
  
6.  호출 된 <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> 메서드.  
  
7.  모든 연결을 닫습니다.  
  
#### 병합 게시에 속한 아티클을 삭제하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergeArticle> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, 및 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 속성입니다.  
  
4.  설정에 대해 1 단계에서 만든 연결의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성입니다.  
  
5.  확인 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 문서 있는지 확인 하는 속성입니다. 이 속성의 값이 **false**이면 3단계에서 아티클 속성이 올바르게 정의되지 않았거나 아티클이 없는 것입니다.  
  
6.  호출 된 <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> 메서드.  
  
7.  모든 연결을 닫습니다.  
  
## 참고 항목  
 [기존 게시에 대한 아티클 추가 및 삭제](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  