---
title: "끌어오기 구독 삭제 | Microsoft Docs"
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
  - "구독 제거"
  - "구독 삭제"
  - "끌어오기 구독 [SQL Server 복제], 삭제"
  - "구독 [SQL Server 복제], 끌어오기"
ms.assetid: 997c0b8e-d8d9-4eed-85b1-6baa1f8594ce
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 끌어오기 구독 삭제
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 끌어오기 구독을 삭제하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 끌어오기 구독을 삭제하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 게시자에서 끌어오기 구독 삭제 (에서 **로컬 게시** 폴더에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) 또는 구독자 (에서 **로컬 구독** 폴더). 구독을 삭제해도 구독에서 개체나 데이터가 제거되지는 않으며 개체나 데이터는 수동으로 제거해야 합니다.  
  
#### 게시자에서 끌어오기 구독을 삭제하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  삭제할 구독과 연결된 게시를 확장합니다.  
  
4.  구독을 마우스 오른쪽 단추로 누른 **삭제**합니다.  
  
5.  확인 대화 상자에서 구독 정보를 삭제할 구독자에 연결할지 여부를 선택합니다. **구독자에 연결** 확인란의 선택을 취소한 경우 나중에 구독자에 연결하여 해당 정보를 삭제해야 합니다.  
  
#### 구독자에서 끌어오기 구독을 삭제하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  구독을 삭제 하 고 클릭 한 다음 마우스 오른쪽 단추로 클릭 **삭제**합니다.  
  
4.  확인 대화 상자에서 구독 정보를 삭제할 게시자에 연결할지 여부를 선택합니다. **게시자에 연결** 확인란의 선택을 취소한 경우 나중에 게시자에 연결하여 해당 정보를 삭제해야 합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 끌어오기 구독은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 삭제할 수 있습니다. 사용되는 저장 프로시저는 구독이 속한 게시 유형에 따라 달라집니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 대한 끌어오기 구독을 삭제하려면  
  
1.  구독 데이터베이스의 구독자에서 실행 [sp_droppullsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)합니다. 지정 **@publication**, **@publisher**, 및 **@publisher_db**합니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_dropsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)합니다. **@publication** 및 **@subscriber**를 지정합니다. **@article** 에 **all**값을 지정합니다. (선택 사항) 배포자에 액세스할 수 없는 경우 값을 지정 **1** 에 대 한 **@ignore_distributor** 배포자에서 관련된 개체를 제거 하지 않고 구독을 삭제 합니다.  
  
#### 병합 게시에 대한 끌어오기 구독을 삭제하려면  
  
1.  구독 데이터베이스의 구독자에서 실행 [sp_dropmergepullsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)합니다. 지정 **@publication**, **@publisher**, 및 **@publisher_db**합니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_dropmergesubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)합니다. 지정 **@publication**, **@subscriber**, 및 **@subscriber_db**합니다. 값을 지정 **끌어오기** 에 대 한 **@subscription_type**합니다. (선택 사항) 배포자에 액세스할 수 없는 경우 값을 지정 **1** 에 대 한 **@ignore_distributor** 배포자에서 관련된 개체를 제거 하지 않고 구독을 삭제 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음은 트랜잭션 게시에 대한 끌어오기 구독을 삭제하는 예입니다. 첫 번째 일괄 처리는 구독자에서 실행되고 두 번째 일괄 처리는 게시자에서 실행됩니다.  
  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_1.sql)]  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_2.sql)]  
  
 다음은 병합 게시에 대한 끌어오기 구독을 삭제하는 예입니다. 첫 번째 일괄 처리는 구독자에서 실행되고 두 번째 일괄 처리는 게시자에서 실행됩니다.  
  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_3.sql)]  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_4.sql)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 끌어오기 구독을 삭제할 수 있습니다. 끌어오기 구독을 삭제하는 데 사용되는 RMO 클래스는 끌어오기 구독이 구독하는 게시의 유형에 따라 다릅니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 대한 끌어오기 구독을 삭제하려면  
  
1.  사용 하 여 구독자와 게시자 모두에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 클래스 및 설정는 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, 및 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 속성입니다. 1 단계의 구독자 연결을 사용 하 여 설정 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성입니다.  
  
3.  확인 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 구독이 있는지 확인 하는 속성입니다. 이 속성의 값이 **false**이면 2단계에서 구독 속성이 올바르게 정의되지 않았거나 구독이 없는 것입니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> 메서드.  
  
5.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransPublication> 1 단계에서 만든 게시자 연결을 사용 하 여 클래스입니다. 지정 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 및 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>합니다.  
  
6.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드. 이 메서드가 **false**를 반환하는 경우 5단계에서 지정한 속성이 올바르지 않거나 서버에 게시가 없는 것입니다.  
  
7.  호출 된 <xref:Microsoft.SqlServer.Replication.TransPublication.RemovePullSubscription%2A> 메서드. *subscriber* 및 *subscriberDB* 매개 변수에 구독자의 이름과 구독 데이터베이스를 지정합니다.  
  
#### 병합 게시에 대한 끌어오기 구독을 삭제하려면  
  
1.  사용 하 여 구독자와 게시자 모두에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 클래스 및 설정는 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, 및 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 속성입니다. 1 단계에서 연결을 사용 하 여 설정 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성입니다.  
  
3.  확인 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 구독이 있는지 확인 하는 속성입니다. 이 속성의 값이 **false**이면 2단계에서 구독 속성이 올바르게 정의되지 않았거나 구독이 없는 것입니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> 메서드.  
  
5.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergePublication> 1 단계에서 만든 게시자 연결을 사용 하 여 클래스입니다. 지정 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 및 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>합니다.  
  
6.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드. 이 메서드가 **false**를 반환하는 경우 5단계에서 지정한 속성이 올바르지 않거나 서버에 게시가 없는 것입니다.  
  
7.  호출 된 <xref:Microsoft.SqlServer.Replication.MergePublication.RemovePullSubscription%2A> 메서드. *subscriber* 및 *subscriberDB* 매개 변수에 구독자의 이름과 구독 데이터베이스를 지정합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 이 예에서는 트랜잭션 게시에 대한 끌어오기 구독을 삭제하고 게시자에서 구독 등록을 제거합니다.  
  
 [!code-csharp[HowTo#rmo_DropTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpullsub)]  
  
 이 예에서는 병합 게시에 대한 끌어오기 구독을 삭제하고 게시자에서 구독 등록을 제거합니다.  
  
 [!code-csharp[HowTo#rmo_DropMergePullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropmergepullsub)]  
  
## 참고 항목  
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  