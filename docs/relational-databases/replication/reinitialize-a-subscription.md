---
title: "구독 다시 초기화 | Microsoft Docs"
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
  - "구독 초기화 [SQL Server 복제], 다시 초기화"
  - "구독 [SQL Server 복제], 다시 초기화"
  - "구독 다시 초기화"
ms.assetid: ca3625c5-c62e-4ab7-9829-d511f838e385
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 구독 다시 초기화
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 구독을 다시 초기화하는 방법에 대해 설명합니다. 각 게시를 다시 초기화하도록 표시하여 다음 동기화 중에 새 스냅숏을 적용할 수 있습니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 구독을 다시 초기화하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 구독을 다시 초기화하는 프로세스는 두 부분으로 구성되어 있습니다.  
  
1.  게시에 대한 단일 구독이나 모든 구독을 다시 초기화하도록 *표시* 합니다. 구독에서 다시 초기화 되도록 표시는 **구독 다시 초기화** 에서 사용할 수 있는 대화 상자는 **로컬 게시** 폴더 및 **로컬 구독** 폴더에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다. 또한 **모든 구독** 탭 및 복제 모니터의 게시 노드에서 구독을 표시할 수 있습니다. 복제 모니터를 시작 하는 방법에 대 한 정보를 참조 하십시오. [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)합니다. 구독을 다시 초기화하도록 표시할 때는 다음과 같은 옵션을 선택할 수 있습니다.  
  
     **현재 스냅숏 사용**  
     다음에 배포 에이전트 또는 병합 에이전트가 실행될 때 현재 스냅숏을 구독자에 적용하려면 이 옵션을 선택합니다. 유효한 스냅숏이 없으면 이 옵션을 선택할 수 없습니다.  
  
     **새 스냅숏 사용**  
     새 스냅숏으로 구독을 다시 초기화하려면 이 옵션을 선택합니다. 스냅숏 에이전트에 의해 스냅숏이 생성된 후에만 스냅숏을 구독자에 적용할 수 있습니다. 스냅숏 에이전트가 예약 실행되도록 설정한 경우에는 예약된 다음 스냅숏 에이전트가 실행될 때까지 구독이 다시 초기화되지 않습니다. 스냅숏 에이전트를 바로 시작하려면 **지금 새 스냅숏 생성** 을 선택합니다.  
  
     **다시 초기화하기 전에 동기화되지 않은 변경 내용 업로드**  
     병합 복제에 대해서만 사용할 수 있습니다. 구독자의 데이터를 스냅숏으로 덮어쓰기 전에 보류 중인 구독 데이터베이스의 변경 내용을 업로드하려면 이 옵션을 선택합니다.  
  
     매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
2.  구독이 다음에 동기화될 때 다시 초기화됩니다. 배포 에이전트(트랜잭션 복제의 경우) 또는 병합 에이전트(병합 복제의 경우)는 최신 스냅숏을 다시 초기화하도록 표시된 구독이 있는 각 구독자에 적용합니다. 구독을 동기화 하는 방법에 대 한 자세한 내용은 참조 [밀어넣기 구독을 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md) 및 [끌어오기 구독을 동기화](../../relational-databases/replication/synchronize-a-pull-subscription.md)합니다.  
  
#### Management Studio에서 단일 밀어넣기 또는 끌어오기 구독을 다시 초기화하도록 표시하려면(게시자)  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  다시 초기화할 구독이 있는 게시를 확장합니다.  
  
4.  구독을 마우스 오른쪽 단추로 누른 **다시 초기화**합니다.  
  
5.  에 **구독 다시 초기화** 대화 상자에서 옵션을 선택한 다음 클릭 **다시 초기화 되도록 표시**합니다.  
  
#### Management Studio에서 단일 끌어오기 구독을 다시 초기화하도록 표시하려면(구독자)  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  구독을 마우스 오른쪽 단추로 누른 **다시 초기화**합니다.  
  
4.  확인 대화 상자가 표시되면 **예**를 클릭합니다.  
  
#### Management Studio에서 모든 구독을 다시 초기화하도록 표시하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  구독을 다시 초기화 하 고 클릭 한 다음을 사용 하 여 게시를 마우스 오른쪽 단추로 클릭 **모든 구독 다시 초기화**합니다.  
  
4.  에 **구독 다시 초기화** 대화 상자에서 옵션을 선택한 다음 클릭 **다시 초기화 되도록 표시**합니다.  
  
#### 복제 모니터에서 단일 밀어넣기 또는 끌어오기 구독을 다시 초기화하도록 표시하려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **모든 구독** 탭을 클릭합니다.  
  
3.  을 다시 초기화 하 고 다음을 클릭 하 고 싶은 구독을 마우스 오른쪽 단추로 클릭 **구독 다시 초기화**합니다.  
  
4.  에 **구독 다시 초기화** 대화 상자에서 옵션을 선택한 다음 클릭 **다시 초기화 되도록 표시**합니다.  
  
#### 복제 모니터에서 모든 구독을 다시 초기화하도록 표시하려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장한 다음 게시자를 확장합니다.  
  
2.  구독을 다시 초기화 하 고 클릭 한 다음을 사용 하 여 게시를 마우스 오른쪽 단추로 클릭 **모든 구독 다시 초기화**합니다.  
  
3.  에 **구독 다시 초기화** 대화 상자에서 옵션을 선택한 다음 클릭 **다시 초기화 되도록 표시**합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 게시를 다시 초기화할 수 있습니다. 사용되는 저장 프로시저는 구독의 유형(밀어넣기 또는 끌어오기) 및 구독이 속한 게시의 유형에 따라 다릅니다.  
  
#### 트랜잭션 게시에 대한 끌어오기 구독을 다시 초기화하려면  
  
1.  구독 데이터베이스의 구독자에서 실행 [sp_reinitpullsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-reinitpullsubscription-transact-sql.md)합니다. 지정 **@publisher**, **@publisher_db**, 및 **@publication**합니다. 이렇게 하면 다음 배포 에이전트 실행 시 구독을 다시 초기화하도록 표시됩니다.  
  
2.  필요에 따라 구독자에서 배포 에이전트를 시작하여 구독을 동기화합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
#### 트랜잭션 게시에 대한 밀어넣기 구독을 다시 초기화하려면  
  
1.  게시자에서 실행 [sp_reinitsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-reinitsubscription-transact-sql.md)합니다. 지정 **@publication**, **@subscriber**, 및 **@destination_db**합니다. 이렇게 하면 다음 배포 에이전트 실행 시 구독을 다시 초기화하도록 표시됩니다.  
  
2.  필요에 따라 배포자에서 배포 에이전트를 시작하여 구독을 동기화합니다. 자세한 내용은 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)을 참조하세요.  
  
#### 병합 게시에 대한 끌어오기 구독을 다시 초기화하려면  
  
1.  구독 데이터베이스의 구독자에서 실행 [sp_reinitmergepullsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md)합니다. 지정 **@publisher**, **@publisher_db**, 및 **@publication**합니다. 다시 초기화 하기 전에 구독자에서 변경 내용을 업로드 하려면의 값을 지정 **true** 에 대 한 **@upload_first**합니다. 이렇게 하면 다음 병합 에이전트 실행 시 구독을 다시 초기화하도록 표시됩니다.  
  
    > [!IMPORTANT]  
    >  매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
2.  필요에 따라 구독자에서 병합 에이전트를 시작하여 구독을 동기화합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
#### 병합 게시에 대한 밀어넣기 구독을 다시 초기화하려면  
  
1.  게시자에서 실행 [sp_reinitmergesubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-reinitmergesubscription-transact-sql.md)합니다. 지정 **@publication**, **@subscriber**, 및 **@subscriber_db**합니다. 다시 초기화 하기 전에 구독자에서 변경 내용을 업로드 하려면의 값을 지정 **true** 에 대 한 **@upload_first**합니다. 이렇게 하면 다음 배포 에이전트 실행 시 구독을 다시 초기화하도록 표시됩니다.  
  
    > [!IMPORTANT]  
    >  매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
2.  필요에 따라 배포자에서 병합 에이전트를 시작하여 구독을 동기화합니다. 자세한 내용은 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)을 참조하세요.  
  
#### 새 병합 게시를 만들 때 다시 초기화 정책을 설정하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), 는 다음 값 중 하나에 대 한 지정 **@automatic_reinitialization_policy**:  
  
    -   **1** -구독이 자동으로 전에 구독자에서 변경 내용이 업로드 게시에 대 한 변경 하 여 필요에 따라 합니다.  
  
    -   **0** -구독을 자동으로 다시 초기화 될 때 구독자에서 변경 내용이 삭제 되는 게시에 대 한 변경 하 여 필요에 따라 합니다.  
  
    > [!IMPORTANT]  
    >  매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
     자세한 내용은 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)을 참조하세요.  
  
#### 기존 병합 게시에 대한 다시 초기화 정책을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), 로 지정 하 여 **automatic_reinitialization_policy** 에 대 한 **@property** 는 다음 값 중 하나에 대 한 고 **@value**:  
  
    -   **1** -구독이 자동으로 전에 구독자에서 변경 내용이 업로드 게시에 대 한 변경 하 여 필요에 따라 합니다.  
  
    -   **0** -구독을 자동으로 다시 초기화 될 때 구독자에서 변경 내용이 삭제 되는 게시에 대 한 변경 하 여 필요에 따라 합니다.  
  
    > [!IMPORTANT]  
    >  매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
     자세한 내용은 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 각 게시를 다시 초기화하도록 표시하여 다음 동기화 중에 새 스냅숏을 적용할 수 있습니다. RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 구독을 다시 초기화할 수 있습니다. 사용되는 클래스는 구독이 속한 게시의 유형과 구독의 유형(밀어넣기 또는 끌어오기 구독)에 따라 다릅니다.  
  
#### 트랜잭션 게시에 대한 끌어오기 구독을 다시 초기화하려면  
  
1.  사용 하 여 구독자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 클래스를 설정 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>, 및에 1 단계의 연결 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>합니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다.  
  
    > [!NOTE]  
    >  이 메서드가 반환 하는 경우 **false**, 2 단계에서 구독 속성이 올바르게 정의 되지 또는 끌어오기 구독이 존재 하지 않습니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.Reinitialize%2A> 메서드. 이 메서드는 구독을 다시 초기화하도록 표시합니다.  
  
5.  끌어오기 구독을 동기화합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
#### 트랜잭션 게시에 대한 밀어넣기 구독을 다시 초기화하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransSubscription> 클래스를 설정 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, 및에 1 단계의 연결 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>합니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다.  
  
    > [!NOTE]  
    >  이 메서드가 반환 하는 경우 **false**, 2 단계에서 구독 속성이 올바르게 정의 되지 또는 밀어넣기 구독이 존재 하지 않습니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.TransSubscription.Reinitialize%2A> 메서드. 이 메서드는 구독을 다시 초기화하도록 표시합니다.  
  
5.  밀어넣기 구독을 동기화합니다. 자세한 내용은 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)을 참조하세요.  
  
#### 병합 게시에 대한 끌어오기 구독을 다시 초기화하려면  
  
1.  사용 하 여 구독자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 클래스를 설정 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>, 및에 1 단계의 연결 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>합니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다.  
  
    > [!NOTE]  
    >  이 메서드가 반환 하는 경우 **false**, 2 단계에서 구독 속성이 올바르게 정의 되지 또는 끌어오기 구독이 존재 하지 않습니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.Reinitialize%2A> 메서드. 다시 초기화하기 전에 구독자의 변경 내용을 업로드하려면 **true** 값을 전달하고, 다시 초기화할 때 보류 중인 모든 변경 내용을 무시하려면 **false** 를 전달합니다. 이 메서드는 구독을 다시 초기화하도록 표시합니다.  
  
    > [!NOTE]  
    >  구독이 만료되면 변경 내용을 업로드할 수 없습니다. 자세한 내용은 [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)을 참조하세요.  
  
5.  끌어오기 구독을 동기화합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
#### 병합 게시에 대한 밀어넣기 구독을 다시 초기화하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 클래스를 설정 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, 및에 1 단계의 연결 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>합니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다.  
  
    > [!NOTE]  
    >  이 메서드가 반환 하는 경우 **false**, 2 단계에서 구독 속성이 올바르게 정의 되지 또는 밀어넣기 구독이 존재 하지 않습니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.MergeSubscription.Reinitialize%2A> 메서드. 다시 초기화하기 전에 구독자의 변경 내용을 업로드하려면 **true** 값을 전달하고, 다시 초기화할 때 보류 중인 모든 변경 내용을 무시하려면 **false** 를 전달합니다. 이 메서드는 구독을 다시 초기화하도록 표시합니다.  
  
    > [!NOTE]  
    >  구독이 만료되면 변경 내용을 업로드할 수 없습니다. 자세한 내용은 [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)을 참조하세요.  
  
5.  밀어넣기 구독을 동기화합니다. 자세한 내용은 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)을 참조하세요.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 다음 예에서는 트랜잭션 게시에 대한 끌어오기 구독을 다시 초기합니다.  
  
 [!code-csharp[HowTo#rmo_ReinitTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinittranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinittranpullsub)]  
  
 다음 예에서는 구독자에서 보류 중인 변경 내용을 먼저 업로드한 다음 병합 게시에 대한 끌어오기 구독을 다시 초기화합니다.  
  
 [!code-csharp[HowTo#rmo_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinitmergepullsub_withupload)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinitmergepullsub_withupload)]  
  
## 참고 항목  
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [복제 관리 개체 개념](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  