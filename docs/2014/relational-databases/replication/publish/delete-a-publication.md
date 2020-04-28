---
title: 게시 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing publications
- publications [SQL Server replication], deleting
- articles [SQL Server replication], deleting
- deleting publications
ms.assetid: 408a1360-12ee-4896-ac94-482ae839593b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fa08a7f84cd413f1212cc73d4242b5da70fd33eb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73882285"
---
# <a name="delete-a-publication"></a>게시 삭제
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 게시를 삭제하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **게시를 삭제하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **의** 로컬 게시 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]폴더에서 게시를 삭제합니다.  
  
#### <a name="to-delete-a-publication"></a>게시를 삭제하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  삭제할 게시를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 게시를 삭제할 수 있습니다. 사용하는 저장 프로시저는 삭제하려는 게시의 유형에 따라 달라집니다.  
  
> [!NOTE]  
>  게시를 삭제해도 게시 데이터베이스의 게시된 개체 또는 구독 데이터베이스의 해당 개체는 제거되지 않습니다. 필요한 경우 `DROP <object>` 명령을 사용하여 이러한 개체를 수동으로 제거할 수 있습니다.  
  
#### <a name="to-delete-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시를 삭제하려면  
  
1.  다음 중 하나를 수행합니다.  
  
    -   단일 게시를 삭제하려면 게시 데이터베이스의 게시자에서 [sp_droppublication](/sql/relational-databases/system-stored-procedures/sp-droppublication-transact-sql) 을 실행합니다.  
  
    -   모든 게시를 삭제하고 게시된 데이터베이스에서 모든 복제 개체를 제거하려면 게시자에서 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) 을 실행합니다. `tran` ** \@형식**에 값을 지정 합니다. (옵션) 배포자에 액세스할 수 없거나 데이터베이스의 상태가 주의 대상 또는 오프라인인 경우 **\@force**에 값 **1**을 지정합니다. (옵션) 게시 데이터베이스에서 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)이 실행되지 않은 경우 **\@dbname**에 데이터베이스 이름을 지정합니다.  
  
        > [!NOTE]  
        >  **\@force**에 값 **1**을 지정하면 데이터베이스에 복제 관련 게시 개체가 남을 수 있습니다.  
  
2.  (선택 사항) 이 데이터베이스에 다른 게시가 없으면 [sp_replicationdboption&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)을 실행하여 스냅샷 또는 트랜잭션 복제를 통해 현재 데이터베이스를 게시할 수 없도록 해제합니다.  
  
3.  (옵션) 구독 데이터베이스의 구독자에서 [sp_subscription_cleanup](/sql/relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql) 을 실행하여 구독 데이터베이스에 남은 모든 복제 메타데이터를 제거합니다.  
  
#### <a name="to-delete-a-merge-publication"></a>병합 게시를 삭제하려면  
  
1.  다음 중 하나를 수행합니다.  
  
    -   단일 게시를 삭제하려면 게시 데이터베이스의 게시자에서 [sp_dropmergepublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql)을 실행합니다.  
  
    -   모든 게시를 삭제하고 게시된 데이터베이스에서 모든 복제 개체를 제거하려면 게시자에서 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) 을 실행합니다. `merge` ** \@형식**에 값을 지정 합니다. (옵션) 배포자에 액세스할 수 없거나 데이터베이스의 상태가 주의 대상 또는 오프라인인 경우 **\@force**에 값 **1**을 지정합니다. (옵션) 게시 데이터베이스에서 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)이 실행되지 않은 경우 **\@dbname**에 데이터베이스 이름을 지정합니다.  
  
        > [!NOTE]  
        >  **\@force**에 값 **1**을 지정하면 데이터베이스에 복제 관련 게시 개체가 남을 수 있습니다.  
  
2.  (선택 사항) 이 데이터베이스에 다른 게시가 없으면 [sp_replicationdboption&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)을 실행하여 병합 복제를 통해 현재 데이터베이스를 게시할 수 없도록 해제합니다.  
  
3.  (선택 사항) 구독 데이터베이스의 구독자에서 [sp_mergesubscription_cleanup&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql)을 실행하여 구독 데이터베이스에 남은 모든 복제 메타데이터를 제거합니다.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 트랜잭션 게시를 제거하고 데이터베이스에 대한 트랜잭션 게시를 해제하는 방법을 보여 줍니다. 이 예에서는 모든 구독이 이전에 제거되었다고 가정합니다. 자세한 내용은 [Delete a Pull Subscription](../delete-a-pull-subscription.md) 또는 [Delete a Push Subscription](../delete-a-push-subscription.md)를 참조하세요.  
  
 [!code-sql[HowTo#sp_droppublication](../../../snippets/tsql/SQL15/replication/howto/tsql/droptranpub.sql#sp_droppublication)]  
  
 다음 예에서는 병합 게시를 제거하고 데이터베이스에 대한 병합 게시를 해제하는 방법을 보여 줍니다. 이 예에서는 모든 구독이 이전에 제거되었다고 가정합니다. 자세한 내용은 [Delete a Pull Subscription](../delete-a-pull-subscription.md) 또는 [Delete a Push Subscription](../delete-a-push-subscription.md)를 참조하세요.  
  
 [!code-sql[HowTo#sp_dropmergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepub.sql#sp_dropmergepublication)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 게시를 삭제할 수 있습니다. 게시를 제거하는 데 사용하는 RMO 클래스는 제거하는 게시 유형에 따라 달라집니다.  
  
#### <a name="to-remove-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시를 제거하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 만듭니다.  
  
3.  게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 속성을 통해 게시가 존재하는지 확인합니다. 이 속성의 값이 `false`이면 3단계의 게시 속성이 올바르게 정의되지 않았거나 게시가 없는 것입니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> 메서드를 호출합니다.  
  
6.  (옵션) 이 데이터베이스에 대한 다른 트랜잭션 게시가 없는 경우 다음과 같이 트랜잭션 게시에 대해 데이터베이스를 비활성화할 수 있습니다.  
  
    1.  <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 인스턴스로 설정합니다.  
  
    2.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. 이 메서드가 `false`를 반환할 경우 데이터베이스가 있는지 확인합니다.  
  
    3.  <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> 속성을 `false`으로 설정합니다.  
  
    4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 호출합니다.  
  
7.  연결을 닫습니다.  
  
#### <a name="to-remove-a-merge-publication"></a>병합 게시를 제거하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만듭니다.  
  
3.  게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 속성을 통해 게시가 존재하는지 확인합니다. 이 속성의 값이 `false`이면 3단계의 게시 속성이 올바르게 정의되지 않았거나 게시가 없는 것입니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> 메서드를 호출합니다.  
  
6.  (옵션) 이 데이터베이스에 대한 다른 병합 게시가 없는 경우 다음과 같이 병합 게시에 대해 데이터베이스를 비활성화할 수 있습니다.  
  
    1.  <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 인스턴스로 설정합니다.  
  
    2.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. 이 메서드가 `false`를 반환하면 데이터베이스가 있는지 확인합니다.  
  
    3.  <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 속성을 `false`으로 설정합니다.  
  
    4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 호출합니다.  
  
7.  연결을 닫습니다.  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> 예(RMO)  
 다음 예에서는 트랜잭션 게시를 삭제합니다. 이 데이터베이스에 대한 다른 트랜잭션 게시가 없으면 트랜잭션 게시도 비활성화됩니다.  
  
 [!code-csharp[HowTo#rmo_DropTranPub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_droptranpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_droptranpub)]  
  
 다음 예에서는 병합 게시를 삭제합니다. 이 데이터베이스에 대한 다른 병합 게시가 없으면 병합 게시도 비활성화됩니다.  
  
 [!code-csharp[HowTo#rmo_DropMergePub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropmergepub)]  
  
## <a name="see-also"></a>참고 항목  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [데이터 및 데이터베이스 개체 게시](publish-data-and-database-objects.md)  
  
  
