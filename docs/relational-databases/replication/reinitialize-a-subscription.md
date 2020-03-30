---
title: 구독 다시 초기화 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- initializing subscriptions [SQL Server replication], reinitializing
- subscriptions [SQL Server replication], reinitializing
- reinitializing subscriptions
ms.assetid: ca3625c5-c62e-4ab7-9829-d511f838e385
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 733e63f6dd01c09fd007a7176721533f7a1c57d3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "70846511"
---
# <a name="reinitialize-a-subscription"></a>구독 다시 초기화
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 구독을 다시 초기화하는 방법에 대해 설명합니다. 각 게시를 다시 초기화하도록 표시하여 다음 동기화 중에 새 스냅샷을 적용할 수 있습니다.  
  
[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]


  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 구독을 다시 초기화하는 프로세스는 두 부분으로 구성되어 있습니다.  
  
1.  게시에 대한 단일 구독이나 모든 구독을 다시 초기화하도록 *표시* 합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **로컬 게시** 폴더와 **로컬 구독** 폴더에서 사용할 수 있는 **구독 다시 초기화** 대화 상자에서 다시 초기화할 구독을 표시합니다. 또한 **모든 구독** 탭 및 복제 모니터의 게시 노드에서 구독을 표시할 수 있습니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요. 구독을 다시 초기화하도록 표시할 때는 다음과 같은 옵션을 선택할 수 있습니다.  
  
     **현재 스냅샷 사용**  
     다음에 배포 에이전트 또는 병합 에이전트가 실행될 때 현재 스냅샷을 구독자에 적용하려면 이 옵션을 선택합니다. 유효한 스냅샷이 없으면 이 옵션을 선택할 수 없습니다.  
  
     **새 스냅샷 사용**  
     새 스냅샷으로 구독을 다시 초기화하려면 이 옵션을 선택합니다. 스냅샷 에이전트에 의해 스냅샷이 생성된 후에만 스냅샷을 구독자에 적용할 수 있습니다. 스냅샷 에이전트가 예약 실행되도록 설정한 경우에는 예약된 다음 스냅샷 에이전트가 실행될 때까지 구독이 다시 초기화되지 않습니다. 스냅샷 에이전트를 바로 시작하려면 **지금 새 스냅샷 생성** 을 선택합니다.  
  
     **다시 초기화하기 전에 동기화되지 않은 변경 내용 업로드**  
     병합 복제에 대해서만 사용할 수 있습니다. 구독자의 데이터를 스냅샷으로 덮어쓰기 전에 보류 중인 구독 데이터베이스의 변경 내용을 업로드하려면 이 옵션을 선택합니다.  
  
     매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
2.  구독이 다음에 동기화될 때 다시 초기화됩니다. 배포 에이전트(트랜잭션 복제의 경우) 또는 병합 에이전트(병합 복제의 경우)는 최신 스냅샷을 다시 초기화하도록 표시된 구독이 있는 각 구독자에 적용합니다. 구독 동기화 방법은 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) 및 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)대화 상자에서 다시 초기화할 구독을 표시합니다.  
  
#### <a name="to-mark-a-single-push-or-pull-subscription-for-reinitialization-in-management-studio-at-the-publisher"></a>Management Studio에서 단일 밀어넣기 또는 끌어오기 구독을 다시 초기화하도록 표시하려면(게시자)  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  다시 초기화할 구독이 있는 게시를 확장합니다.  
  
4.  구독을 마우스 오른쪽 단추로 클릭한 다음 **다시 초기화**를 클릭합니다.  
  
5.  **구독 다시 초기화** 대화 상자에서 옵션을 선택한 다음 **다시 초기화 표시**를 클릭합니다.  
  
#### <a name="to-mark-a-single-pull-subscription-for-reinitialization-in-management-studio-at-the-subscriber"></a>Management Studio에서 단일 끌어오기 구독을 다시 초기화하도록 표시하려면(구독자)  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  구독을 마우스 오른쪽 단추로 클릭한 다음 **다시 초기화**를 클릭합니다.  
  
4.  확인 대화 상자가 표시되면 **예**를 클릭합니다.  
  
#### <a name="to-mark-all-subscriptions-for-reinitialization-in-management-studio"></a>Management Studio에서 모든 구독을 다시 초기화하도록 표시하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  다시 초기화할 구독이 있는 게시를 마우스 오른쪽 단추로 클릭한 다음 **모든 구독 다시 초기화**를 클릭합니다.  
  
4.  **구독 다시 초기화** 대화 상자에서 옵션을 선택한 다음 **다시 초기화 표시**를 클릭합니다.  
  
#### <a name="to-mark-a-single-push-or-pull-subscription-for-reinitialization-in-replication-monitor"></a>복제 모니터에서 단일 밀어넣기 또는 끌어오기 구독을 다시 초기화하도록 표시하려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **모든 구독** 탭을 클릭합니다.  
  
3.  다시 초기화할 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 다시 초기화**를 클릭합니다.  
  
4.  **구독 다시 초기화** 대화 상자에서 옵션을 선택한 다음 **다시 초기화 표시**를 클릭합니다.  
  
#### <a name="to-mark-all-subscriptions-for-reinitialization-in-replication-monitor"></a>복제 모니터에서 모든 구독을 다시 초기화하도록 표시하려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장한 다음 게시자를 확장합니다.  
  
2.  다시 초기화할 구독이 있는 게시를 마우스 오른쪽 단추로 클릭한 다음 **모든 구독 다시 초기화**를 클릭합니다.  
  
3.  **구독 다시 초기화** 대화 상자에서 옵션을 선택한 다음 **다시 초기화 표시**를 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 게시를 다시 초기화할 수 있습니다. 사용되는 저장 프로시저는 구독의 유형(밀어넣기 또는 끌어오기) 및 구독이 속한 게시의 유형에 따라 다릅니다.  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-transactional-publication"></a>트랜잭션 게시에 대한 끌어오기 구독을 다시 초기화하려면  
  
1.  구독 데이터베이스의 구독자에서 [sp_reinitpullsubscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitpullsubscription-transact-sql.md)을 실행합니다. **\@publisher**, **\@publisher_db** 및 **\@publication**을 지정합니다. 이렇게 하면 다음 배포 에이전트 실행 시 구독을 다시 초기화하도록 표시됩니다.  
  
2.  필요에 따라 구독자에서 배포 에이전트를 시작하여 구독을 동기화합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-transactional-publication"></a>트랜잭션 게시에 대한 밀어넣기 구독을 다시 초기화하려면  
  
1.  게시자에서 [sp_reinitsubscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitsubscription-transact-sql.md)을 실행합니다. **\@publication**, **\@subscriber** 및 **\@destination_db**를 지정합니다. 이렇게 하면 다음 배포 에이전트 실행 시 구독을 다시 초기화하도록 표시됩니다.  
  
2.  필요에 따라 배포자에서 배포 에이전트를 시작하여 구독을 동기화합니다. 자세한 내용은 [밀어넣기 구독 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md)을 참조하세요.  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 대한 끌어오기 구독을 다시 초기화하려면  
  
1.  구독 데이터베이스의 구독자에서 [sp_reinitmergepullsubscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md)을 실행합니다. **\@publisher**, **\@publisher_db** 및 **\@publication**을 지정합니다. 다시 초기화하기 전에 구독자에서 변경 내용을 업로드하려면 **\@upload_first**의 값을 **true**로 지정합니다. 이렇게 하면 다음 병합 에이전트 실행 시 구독을 다시 초기화하도록 표시됩니다.  
  
    > [!IMPORTANT]  
    >  매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
2.  필요에 따라 구독자에서 병합 에이전트를 시작하여 구독을 동기화합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-merge-publication"></a>병합 게시에 대한 밀어넣기 구독을 다시 초기화하려면  
  
1.  게시자에서 [sp_reinitmergesubscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitmergesubscription-transact-sql.md)을 실행합니다. **\@publication**, **\@subscriber** 및 **\@subscriber_db**를 지정합니다. 다시 초기화하기 전에 구독자에서 변경 내용을 업로드하려면 **\@upload_first**의 값을 **true**로 지정합니다. 이렇게 하면 다음 배포 에이전트 실행 시 구독을 다시 초기화하도록 표시됩니다.  
  
    > [!IMPORTANT]  
    >  매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
2.  필요에 따라 배포자에서 병합 에이전트를 시작하여 구독을 동기화합니다. 자세한 내용은 [밀어넣기 구독 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md)을 참조하세요.  
  
#### <a name="to-set-the-reinitialization-policy-when-creating-a-new-merge-publication"></a>새 병합 게시를 만들 때 다시 초기화 정책을 설정하려면  
  
1.  게시 데이터베이스의 게시자에서 **\@automatic_reinitialization_policy**에 다음 중 한 가지 값을 지정하고 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)을 실행합니다.  
  
    -   **1** - 게시의 변경으로 의해 구독이 자동으로 다시 초기화되기 전에 구독자의 변경 내용이 업로드됩니다.  
  
    -   **0** - 게시의 변경으로 인해 구독이 자동으로 다시 초기화될 때 구독자의 변경 내용이 삭제됩니다.  
  
    > [!IMPORTANT]  
    >  매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
     자세한 내용은 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
#### <a name="to-change-the-reinitialization-policy-for-an-existing-merge-publication"></a>기존 병합 게시에 대한 다시 초기화 정책을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 **\@property**에 **automatic_reinitialization_policy**를 지정하고 **\@value**에는 다음 값 중 하나를 지정하여 [sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)을 실행합니다.  
  
    -   **1** - 게시의 변경으로 의해 구독이 자동으로 다시 초기화되기 전에 구독자의 변경 내용이 업로드됩니다.  
  
    -   **0** - 게시의 변경으로 인해 구독이 자동으로 다시 초기화될 때 구독자의 변경 내용이 삭제됩니다.  
  
    > [!IMPORTANT]  
    >  매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
     자세한 내용은 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 각 게시를 다시 초기화하도록 표시하여 다음 동기화 중에 새 스냅샷을 적용할 수 있습니다. RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 구독을 다시 초기화할 수 있습니다. 사용되는 클래스는 구독이 속한 게시의 유형과 구독의 유형(밀어넣기 또는 끌어오기 구독)에 따라 다릅니다.  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-transactional-publication"></a>트랜잭션 게시에 대한 끌어오기 구독을 다시 초기화하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 클래스의 인스턴스를 만들고, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>및 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>에 대해 1단계에서 만든 연결을 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다.  
  
    > [!NOTE]  
    >  이 메서드가 **false**를 반환하는 경우 2단계에서 구독 속성이 올바르게 정의되지 않았거나 끌어오기 구독이 없는 것입니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription.Reinitialize%2A> 메서드를 호출합니다. 이 메서드는 구독을 다시 초기화하도록 표시합니다.  
  
5.  끌어오기 구독을 동기화합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-transactional-publication"></a>트랜잭션 게시에 대한 밀어넣기 구독을 다시 초기화하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransSubscription> 클래스의 인스턴스를 만들고, <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>및 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>에 대해 1단계에서 만든 연결을 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다.  
  
    > [!NOTE]  
    >  이 메서드가 **false**를 반환하는 경우 2단계에서 구독 속성이 올바르게 정의되지 않았거나 밀어넣기 구독이 없는 것입니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.TransSubscription.Reinitialize%2A> 메서드를 호출합니다. 이 메서드는 구독을 다시 초기화하도록 표시합니다.  
  
5.  밀어넣기 구독을 동기화합니다. 자세한 내용은 [밀어넣기 구독 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md)을 참조하세요.  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 대한 끌어오기 구독을 다시 초기화하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 클래스의 인스턴스를 만들고, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>및 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>에 대해 1단계에서 만든 연결을 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다.  
  
    > [!NOTE]  
    >  이 메서드가 **false**를 반환하는 경우 2단계에서 구독 속성이 올바르게 정의되지 않았거나 끌어오기 구독이 없는 것입니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription.Reinitialize%2A> 메서드를 호출합니다. 다시 초기화하기 전에 구독자의 변경 내용을 업로드하려면 **true** 값을 전달하고, 다시 초기화할 때 보류 중인 모든 변경 내용을 무시하려면 **false** 를 전달합니다. 이 메서드는 구독을 다시 초기화하도록 표시합니다.  
  
    > [!NOTE]  
    >  구독이 만료되면 변경 내용을 업로드할 수 없습니다. 자세한 내용은 [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)을 참조하세요.  
  
5.  끌어오기 구독을 동기화합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-merge-publication"></a>병합 게시에 대한 밀어넣기 구독을 다시 초기화하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeSubscription> 클래스의 인스턴스를 만들고, <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>및 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>에 대해 1단계에서 만든 연결을 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다.  
  
    > [!NOTE]  
    >  이 메서드가 **false**를 반환하는 경우 2단계에서 구독 속성이 올바르게 정의되지 않았거나 밀어넣기 구독이 없는 것입니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.MergeSubscription.Reinitialize%2A> 메서드를 호출합니다. 다시 초기화하기 전에 구독자의 변경 내용을 업로드하려면 **true** 값을 전달하고, 다시 초기화할 때 보류 중인 모든 변경 내용을 무시하려면 **false** 를 전달합니다. 이 메서드는 구독을 다시 초기화하도록 표시합니다.  
  
    > [!NOTE]  
    >  구독이 만료되면 변경 내용을 업로드할 수 없습니다. 자세한 내용은 [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)을 참조하세요.  
  
5.  밀어넣기 구독을 동기화합니다. 자세한 내용은 [밀어넣기 구독 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md)을 참조하세요.  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> 예(RMO)  
 다음 예에서는 트랜잭션 게시에 대한 끌어오기 구독을 다시 초기합니다.  
  
 [!code-cs[HowTo#rmo_ReinitTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinittranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinittranpullsub)]  
  
 다음 예에서는 구독자에서 보류 중인 변경 내용을 먼저 업로드한 다음 병합 게시에 대한 끌어오기 구독을 다시 초기화합니다.  
  
 [!code-cs[HowTo#rmo_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinitmergepullsub_withupload)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinitmergepullsub_withupload)]  
  
## <a name="see-also"></a>참고 항목  
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
