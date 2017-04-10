---
title: "밀어넣기 구독 삭제 | Microsoft Docs"
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
  - "밀어넣기 구독 [SQL Server 복제], 삭제"
  - "구독 삭제"
  - "구독 [SQL Server 복제], 밀어넣기"
ms.assetid: 3c4847e2-aed9-4488-b45d-8164422bdb10
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 밀어넣기 구독 삭제
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 밀어넣기 구독을 삭제하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **밀어넣기 구독을 삭제하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 게시자에서 밀어넣기 구독 삭제 (에서 **로컬 게시** 폴더에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) 또는 구독자 (에서 **로컬 구독** 폴더). 구독을 삭제해도 구독에서 개체나 데이터가 제거되지는 않으며 개체나 데이터는 수동으로 제거해야 합니다.  
  
#### 게시자에서 밀어넣기 구독을 삭제하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  삭제할 구독과 연결된 게시를 확장합니다.  
  
4.  구독을 마우스 오른쪽 단추로 누른 **삭제**합니다.  
  
5.  확인 대화 상자에서 구독 정보를 삭제할 구독자에 연결할지 여부를 선택합니다. **구독자에 연결** 확인란의 선택을 취소한 경우 나중에 구독자에 연결하여 해당 정보를 삭제해야 합니다.  
  
#### 구독자에서 밀어넣기 구독을 삭제하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  구독을 삭제 하 고 클릭 한 다음 마우스 오른쪽 단추로 클릭 **삭제**합니다.  
  
4.  확인 대화 상자에서 구독 정보를 삭제할 게시자에 연결할지 여부를 선택합니다. **게시자에 연결** 확인란의 선택을 취소한 경우 나중에 게시자에 연결하여 해당 정보를 삭제해야 합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 밀어넣기 구독은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 삭제할 수 있습니다. 사용되는 저장 프로시저는 구독이 속한 게시 유형에 따라 달라집니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 대한 밀어넣기 구독을 삭제하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_dropsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)합니다. **@publication** 및 **@subscriber**를 지정합니다. **@article** 에 **all**값을 지정합니다. (선택 사항) 배포자에 액세스할 수 없는 경우 값을 지정 **1** 에 대 한 **@ignore_distributor** 배포자에서 관련된 개체를 제거 하지 않고 구독을 삭제 합니다.  
  
2.  구독 데이터베이스의 구독자에서 실행 [sp_subscription_cleanup (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) 구독 데이터베이스에서 복제 메타 데이터를 제거 합니다.  
  
#### 병합 게시에 대한 밀어내기 구독을 삭제하려면  
  
1.  게시자에서 실행 [sp_dropmergesubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md), 로 지정 하 여 **@publication**, **@subscriber** 및 **@subscriber_db**합니다. (선택 사항) 배포자에 액세스할 수 없는 경우 값을 지정 **1** 에 대 한 **@ignore_distributor** 배포자에서 관련된 개체를 제거 하지 않고 구독을 삭제 합니다.  
  
2.  구독 데이터베이스의 구독자에서 실행 [sp_mergesubscription_cleanup (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)합니다. 지정 **@publisher**, **@publisher_db**, 및 **@publication**합니다. 이렇게 하면 구독 데이터베이스에서 병합 메타데이터가 제거됩니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예에서는 트랜잭션 게시에 대한 밀어넣기 구독을 삭제합니다.  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_1.sql)]  
  
 이 예에서는 병합 게시에 대한 밀어넣기 구독을 삭제합니다.  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 밀어넣기 구독을 삭제하는 데 사용되는 RMO 클래스는 밀어넣기 구독이 구독하는 게시의 유형에 따라 달라집니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 대한 밀어넣기 구독을 삭제하려면  
  
1.  사용 하 여 구독자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransSubscription> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, 및 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> 속성입니다.  
  
4.  설정의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 대해 1 단계에서 만든는 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성입니다.  
  
5.  확인 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 구독이 있는지 확인 하는 속성입니다. 이 속성의 값이 **false**이면 2단계에서 구독 속성이 올바르게 정의되지 않았거나 구독이 없는 것입니다.  
  
6.  호출 된 <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> 메서드.  
  
#### 병합 게시에 대한 밀어내기 구독을 삭제하려면  
  
1.  사용 하 여 구독자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, 및 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> 속성입니다.  
  
4.  설정의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 대해 1 단계에서 만든는 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성입니다.  
  
5.  확인 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 구독이 있는지 확인 하는 속성입니다. 이 속성의 값이 **false**이면 2단계에서 구독 속성이 올바르게 정의되지 않았거나 구독이 없는 것입니다.  
  
6.  호출 된 <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> 메서드.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 밀어넣기 구독을 삭제할 수 있습니다.  
  
 [!code-csharp[HowTo#rmo_DropTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpushsub)]  
  
## 참고 항목  
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  