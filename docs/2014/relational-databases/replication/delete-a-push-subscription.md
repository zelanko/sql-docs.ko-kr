---
title: 밀어넣기 구독 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing subscriptions
- push subscriptions [SQL Server replication], deleting
- deleting subscriptions
- subscriptions [SQL Server replication], push
ms.assetid: 3c4847e2-aed9-4488-b45d-8164422bdb10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 75e5953d8f7ef9af1134db56f7061261eee2c0fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721426"
---
# <a name="delete-a-push-subscription"></a>밀어넣기 구독 삭제
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 밀어넣기 구독을 삭제하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **밀어넣기 구독을 삭제하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 게시자( **의** 로컬 게시 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]폴더 사용) 또는 구독자( **로컬 구독** 폴더 사용)에서 밀어넣기 구독을 삭제합니다. 구독을 삭제해도 구독에서 개체나 데이터가 제거되지는 않으며 개체나 데이터는 수동으로 제거해야 합니다.  
  
#### <a name="to-delete-a-push-subscription-at-the-publisher"></a>게시자에서 밀어넣기 구독을 삭제하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  삭제할 구독과 연결된 게시를 확장합니다.  
  
4.  구독을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
5.  확인 대화 상자에서 구독 정보를 삭제할 구독자에 연결할지 여부를 선택합니다. **구독자에 연결** 확인란의 선택을 취소한 경우 나중에 구독자에 연결하여 해당 정보를 삭제해야 합니다.  
  
#### <a name="to-delete-a-push-subscription-at-the-subscriber"></a>구독자에서 밀어넣기 구독을 삭제하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  삭제할 구독을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
4.  확인 대화 상자에서 구독 정보를 삭제할 게시자에 연결할지 여부를 선택합니다. **게시자에 연결** 확인란의 선택을 취소한 경우 나중에 게시자에 연결하여 해당 정보를 삭제해야 합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 밀어넣기 구독은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 삭제할 수 있습니다. 사용되는 저장 프로시저는 구독이 속한 게시 유형에 따라 달라집니다.  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 대한 밀어넣기 구독을 삭제하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_dropsubscription&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql)을 실행합니다. 이때 **@publication** 및 **@subscriber**에서 사용 가능합니다. **@article**에 **all** 값을 지정합니다. (옵션) 배포자에 액세스할 수 없으면 **@ignore_distributor** 에 **@ignore_distributor** 을 지정하여 배포자에서 관련 개체를 제거하지 않고 구독을 삭제합니다.  
  
2.  구독 데이터베이스의 구독자에서 [sp_subscription_cleanup&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql)을 실행하여 구독 데이터베이스에 있는 복제 메타데이터를 제거합니다.  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>병합 게시에 대한 밀어내기 구독을 삭제하려면  
  
1.  게시자에서 **@publication**, **@subscriber** 및 **@subscriber_db**를 지정하여 [sp_dropmergesubscription&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql)을 실행합니다. (옵션) 배포자에 액세스할 수 없으면 **@ignore_distributor** 에 **@ignore_distributor** 을 지정하여 배포자에서 관련 개체를 제거하지 않고 구독을 삭제합니다.  
  
2.  구독 데이터베이스의 구독자에서 [sp_mergesubscription_cleanup&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql)을 실행합니다. **@publisher**, **@publisher_db** 및 **@publication**을 지정합니다. 이렇게 하면 구독 데이터베이스에서 병합 메타데이터가 제거됩니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예에서는 트랜잭션 게시에 대한 밀어넣기 구독을 삭제합니다.  
  
 [!code-sql[HowTo#sp_droptransubscription](../../snippets/tsql/SQL15/replication/howto/tsql/droptranpullsub.sql#sp_droptransubscription)]  
  
 이 예에서는 병합 게시에 대한 밀어넣기 구독을 삭제합니다.  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepullsub.sql#sp_dropmergesubscription)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 밀어넣기 구독을 삭제하는 데 사용되는 RMO 클래스는 밀어넣기 구독이 구독하는 게시의 유형에 따라 달라집니다.  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 대한 밀어넣기 구독을 삭제하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransSubscription> 클래스의 인스턴스를 만듭니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>및 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> 속성을 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 속성을 1단계의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 으로 설정합니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 속성을 확인하여 구독이 존재하는지 확인합니다. 이 속성의 값이 `false`이면 2단계에서 구독 속성이 올바르게 정의되지 않았거나 구독이 없는 것입니다.  
  
6.  <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> 메서드를 호출합니다.  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>병합 게시에 대한 밀어내기 구독을 삭제하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeSubscription> 클래스의 인스턴스를 만듭니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>및 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> 속성을 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 속성을 1단계의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 으로 설정합니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 속성을 확인하여 구독이 존재하는지 확인합니다. 이 속성의 값이 `false`이면 2단계에서 구독 속성이 올바르게 정의되지 않았거나 구독이 없는 것입니다.  
  
6.  <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> 메서드를 호출합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 밀어넣기 구독을 삭제할 수 있습니다.  
  
 [!code-csharp[HowTo#rmo_DropTranPushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_droptranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_droptranpushsub)]  
  
## <a name="see-also"></a>관련 항목  
 [게시 구독](subscribe-to-publications.md)   
 [복제 보안을 위한 최선의 구현 방법](security/replication-security-best-practices.md)  
  
  
