---
title: "게시 삭제 | Microsoft Docs"
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
  - "게시 제거"
  - "게시 [SQL Server 복제], 삭제"
  - "아티클 [SQL Server 복제], 삭제"
  - "게시 삭제"
ms.assetid: 408a1360-12ee-4896-ac94-482ae839593b
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 게시 삭제
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 게시를 삭제하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **게시를 삭제하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **의** 로컬 게시 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]폴더에서 게시를 삭제합니다.  
  
#### 게시를 삭제하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  삭제 하 고 클릭 한 다음 원하는 게시를 마우스 오른쪽 단추로 클릭 **삭제**합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 게시를 삭제할 수 있습니다. 사용하는 저장 프로시저는 삭제하려는 게시의 유형에 따라 달라집니다.  
  
> [!NOTE]  
>  게시를 삭제해도 게시 데이터베이스의 게시된 개체 또는 구독 데이터베이스의 해당 개체는 제거되지 않습니다. 필요한 경우 `DROP <object>` 명령을 사용하여 이러한 개체를 수동으로 제거할 수 있습니다.  
  
#### 스냅숏 또는 트랜잭션 게시를 삭제하려면  
  
1.  다음 중 하나를 수행합니다.  
  
    -   단일 게시를 삭제 하려면 실행 [sp_droppublication](../../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md) 게시 데이터베이스의 게시자에서.  
  
    -   모든 게시를 삭제 한 다음 게시 된 데이터베이스에서 모든 복제 개체를 제거 하려면 실행 [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 게시자입니다. **@type** 에 값 **tran**를 지정합니다. (선택 사항) 배포자에 액세스할 수 없는 경우 또는 데이터베이스의 상태가 주의 대상 또는 오프 라인의 값을 지정 합니다. **1** 에 대 한 **@force**합니다. (선택 사항) 에 대 한 데이터베이스의 이름을 지정 **@dbname** 경우 [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 게시 데이터베이스에서 실행 되지 않습니다.  
  
        > [!NOTE]  
        >  값을 지정 하면 **1** 에 대 한 **@force** 복제 관련 게시 개체가 데이터베이스에 남아 있을 수 있습니다.  
  
2.  (선택 사항) 이 데이터베이스에 다른 게시가 없으면, 실행 [sp_replicationdboption (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 스냅숏 또는 트랜잭션 복제를 사용 하 여 현재 데이터베이스의 게시를 사용 하지 않도록 설정 합니다.  
  
3.  (선택 사항) 구독 데이터베이스의 구독자에서 실행 [sp_subscription_cleanup](../../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) 구독 데이터베이스에 남은 모든 복제 메타 데이터를 제거 합니다.  
  
#### 병합 게시를 삭제하려면  
  
1.  다음 중 하나를 수행합니다.  
  
    -   단일 게시를 삭제 하려면 실행 [sp_dropmergepublication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md) 게시 데이터베이스의 게시자입니다.  
  
    -   모든 게시를 삭제 한 다음 게시 된 데이터베이스에서 모든 복제 개체를 제거 하려면 실행 [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 게시자입니다. **@type** 에 값 **merge**를 지정합니다. (선택 사항) 배포자에 액세스할 수 없는 경우 또는 데이터베이스의 상태가 주의 대상 또는 오프 라인의 값을 지정 합니다. **1** 에 대 한 **@force**합니다. (선택 사항) 에 대 한 데이터베이스의 이름을 지정 **@dbname** 경우 [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 게시 데이터베이스에서 실행 되지 않습니다.  
  
        > [!NOTE]  
        >  값을 지정 하면 **1** 에 대 한 **@force** 복제 관련 게시 개체가 데이터베이스에 남아 있을 수 있습니다.  
  
2.  (선택 사항) 이 데이터베이스에 다른 게시가 없으면, 실행 [sp_replicationdboption (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 병합 복제를 사용 하 여 현재 데이터베이스의 게시 하지 않으려면 합니다.  
  
3.  (선택 사항) 구독 데이터베이스의 구독자에서 실행 [sp_mergesubscription_cleanup (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md) 구독 데이터베이스에 남은 모든 복제 메타 데이터를 제거 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 트랜잭션 게시를 제거하고 데이터베이스에 대한 트랜잭션 게시를 해제하는 방법을 보여 줍니다. 이 예에서는 모든 구독이 이전에 제거되었다고 가정합니다. 자세한 내용은 [Delete a Pull Subscription](../../../relational-databases/replication/delete-a-pull-subscription.md) 또는 [Delete a Push Subscription](../../../relational-databases/replication/delete-a-push-subscription.md)를 참조하세요.  
  
 [!code-sql[HowTo#sp_droppublication](../../../relational-databases/replication/codesnippet/tsql/delete-a-publication_1.sql)]  
  
 다음 예에서는 병합 게시를 제거하고 데이터베이스에 대한 병합 게시를 해제하는 방법을 보여 줍니다. 이 예에서는 모든 구독이 이전에 제거되었다고 가정합니다. 자세한 내용은 [Delete a Pull Subscription](../../../relational-databases/replication/delete-a-pull-subscription.md) 또는 [Delete a Push Subscription](../../../relational-databases/replication/delete-a-push-subscription.md)를 참조하세요.  
  
 [!code-sql[HowTo#sp_dropmergepublication](../../../relational-databases/replication/codesnippet/tsql/delete-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 게시를 삭제할 수 있습니다. 게시를 제거하는 데 사용하는 RMO 클래스는 제거하는 게시 유형에 따라 달라집니다.  
  
#### 스냅숏 또는 트랜잭션 게시를 제거하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 게시 및 설정에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1 단계에서 만든 연결 합니다.  
  
4.  확인 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 속성을 통해 게시가 존재 하는지 확인 합니다. 이 속성의 값이 **false**이면 3단계의 게시 속성이 올바르게 정의되지 않았거나 게시가 없는 것입니다.  
  
5.  호출 된 <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> 메서드.  
  
6.  (옵션) 이 데이터베이스에 대한 다른 트랜잭션 게시가 없는 경우 다음과 같이 트랜잭션 게시에 대해 데이터베이스를 비활성화할 수 있습니다.  
  
    1.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 의 인스턴스에 대 한 속성 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 만든 합니다.  
  
    2.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드. 이 메서드가 **false**를 반환할 경우 데이터베이스가 있는지 확인합니다.  
  
    3.  설정의 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> 속성을 **false**합니다.  
  
    4.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드.  
  
7.  연결을 닫습니다.  
  
#### 병합 게시를 제거하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 게시 및 설정에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1 단계에서 만든 연결 합니다.  
  
4.  확인 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 속성을 통해 게시가 존재 하는지 확인 합니다. 이 속성의 값이 **false**이면 3단계의 게시 속성이 올바르게 정의되지 않았거나 게시가 없는 것입니다.  
  
5.  호출 된 <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> 메서드.  
  
6.  (옵션) 이 데이터베이스에 대한 다른 병합 게시가 없는 경우 다음과 같이 병합 게시에 대해 데이터베이스를 비활성화할 수 있습니다.  
  
    1.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 의 인스턴스에 대 한 속성 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서에서.  
  
    2.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드. 이 메서드가 **false**를 반환하면 데이터베이스가 있는지 확인합니다.  
  
    3.  설정의 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 속성을 **false**합니다.  
  
    4.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드.  
  
7.  연결을 닫습니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 다음 예에서는 트랜잭션 게시를 삭제합니다. 이 데이터베이스에 대한 다른 트랜잭션 게시가 없으면 트랜잭션 게시도 비활성화됩니다.  
  
 [!code-csharp[HowTo#rmo_DropTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpub)]  
  
 다음 예에서는 병합 게시를 삭제합니다. 이 데이터베이스에 대한 다른 병합 게시가 없으면 병합 게시도 비활성화됩니다.  
  
 [!code-csharp[HowTo#rmo_DropMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropmergepub)]  
  
## 참고 항목  
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  