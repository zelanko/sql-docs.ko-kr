---
title: 끌어오기 구독 동기화 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], synchronizing
- synchronization [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
ms.assetid: 3ca24b23-fdc3-408e-8208-a2ace48fc8e3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c8a7a607221599d599438352eab5add1cc94e5d7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63186236"
---
# <a name="synchronize-a-pull-subscription"></a>끌어오기 구독 동기화
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]복제 에이전트 [또는 RMO(복제 관리 개체)를 사용하여](agents/replication-agents-overview.md)에서 끌어오기 구독을 동기화하는 방법에 대해 설명합니다.  
  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 구독은 배포 에이전트(스냅샷 및 트랜잭션 복제의 경우) 또는 병합 에이전트(병합 복제의 경우)에 의해 동기화됩니다. 에이전트는 지속적으로 실행하거나 수요에 따라 실행하거나 일정에 따라 실행할 수 있습니다. 동기화 일정을 설정하는 방법은 [동기화 일정 지정](specify-synchronization-schedules.md)을 참조하세요.  
  
 **의** 로컬 구독 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]폴더에서 요청 시 구독을 동기화합니다.  
  
#### <a name="to-synchronize-a-pull-subscription-on-demand-in-management-studio"></a>Management Studio에서 요청 시 끌어오기 구독을 동기화하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  동기화할 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 상태 보기**를 클릭합니다.  
  
4.  **동기화 상태 보기 - \<Subscriber>:\<SubscriptionDatabase>** 대화 상자에서 **시작**을 클릭합니다. 동기화가 완료되면 **동기화 완료** 라는 메시지가 표시됩니다.  
  
5.  **닫기**를 클릭합니다.  
  
##  <a name="replication-agents"></a><a name="ReplProg"></a>복제 에이전트  
 끌어오기 구독은 명령 프롬프트에서 적합한 복제 에이전트 실행 파일을 호출하여 프로그래밍 방식으로 요청 시 동기화할 수 있습니다. 호출한 복제 에이전트 실행 파일은 끌어오기 구독이 속한 게시 유형에 따라 달라집니다. 자세한 내용은 [Replication Agents](agents/replication-agents-overview.md)을 참조하세요.  
  
> [!NOTE]  
>  복제 에이전트는 명령 프롬프트에서 에이전트를 시작한 사용자의 Windows 인증 자격 증명을 사용하여 로컬 서버에 연결합니다. 이러한 자격 증명은 Windows 통합 인증을 사용하여 원격 서버에 연결할 때도 사용됩니다.  
  
#### <a name="to-start-the-distribution-agent-from-the-command-prompt-or-from-a-batch-file"></a>명령 프롬프트 또는 배치 파일에서 배포 에이전트를 시작하려면  
  
1.  _명령 프롬프트 또는 배치 파일에서 [distrib.exe](agents/replication-distribution-agent.md) 를 실행하여 **복제 배포 에이전트**를 시작하고 다음 명령줄 인수를 지정합니다.  
  
    -   **-게시자**  
  
    -   **-PublisherDB**  
  
    -   **-배포자**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-구독자**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriptionType** = **1**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 다음 인수도 지정해야 합니다.  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
#### <a name="to-start-the-merge-agent-from-the-command-prompt-or-from-a-batch-file"></a>명령 프롬프트 또는 배치 파일에서 병합 에이전트를 시작하려면  
  
1.  명령 프롬프트 또는 배치 파일에서 [replmerg.exe](agents/replication-merge-agent.md) 를 실행하여 **복제 병합 에이전트**를 시작하고 다음 명령줄 인수를 지정합니다.  
  
    -   **-게시자**  
  
    -   **-PublisherDB**  
  
    -   **-PublisherSecurityMode** = **1**  
  
    -   **-게시**  
  
    -   **-배포자**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-구독자**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType** = **1**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 다음 인수도 지정해야 합니다.  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
###  <a name="examples-replication-agents"></a><a name="TsqlExample"></a> 예(복제 에이전트)  
 다음 예에서는 배포 에이전트를 시작하여 끌어오기 구독을 동기화합니다. 모든 연결은 Windows 인증을 사용하여 만듭니다.  
  
 [!code-sql[HowTo#bat_synctranpullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/synctranpullsub_10.bat)]  
  
 다음 예에서는 병합 에이전트를 시작하여 끌어오기 구독을 동기화합니다. 모든 연결은 Windows 인증을 사용하여 만듭니다.  
  
 [!code-sql[HowTo#bat_syncmergepullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/syncmergepullsub_10.bat)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 RMO(복제 관리 개체) 및 관리 코드 액세스를 사용하여 복제 에이전트 기능에 프로그래밍 방식으로 끌어오기 구독을 동기화할 수 있습니다. 끌어오기 구독을 동기화하는 데 사용하는 클래스는 구독이 속한 게시 유형에 따라 달라집니다.  
  
> [!NOTE]  
>  동기화가 애플리케이션에 영향을 미치지 않고 자율적으로 실행하도록 하려면 에이전트를 비동기적으로 시작합니다. 그러나 진행률 표시줄을 표기하기 위해 동기화 프로세스 동안 동기화 결과를 모니터링하고 에이전트에서 콜백을 받으려면 에이전트를 동기적으로 시작해야 합니다. For [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 구독자의 경우 에이전트를 동기적으로 시작해야 합니다.  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시에 끌어오기 구독을 동기화하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 클래스의 인스턴스를 만들고 다음 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>에 대한 구독 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>에 대해 구독이 속한 게시 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>에 대한 게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>에 대한 게시자 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>에 대해 1단계에서 만든 연결  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 나머지 구독 속성을 얻습니다. 이 메서드가 `false`를 반환하는 경우 구독이 있는지 확인합니다.  
  
4.  다음 방법 중 하나로 구독자에서 배포 에이전트를 시작합니다.  
  
    -   2단계에서 만든 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizeWithJob%2A> 의 인스턴스에서 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 메서드를 호출합니다. 이 메서드는 배포 에이전트를 비동기적으로 시작하고 에이전트 작업이 실행되는 동안 애플리케이션에 대한 반환을 즉시 제어합니다. [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 구독자인 경우 또는 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A>에 `false` 값(기본값)을 사용하여 구독을 만든 경우 이 메서드를 호출할 수 없습니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> 속성에서 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> 클래스의 인스턴스를 가져오고 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> 메서드를 호출합니다. 이 메서드는 에이전트를 동기적으로 시작하고 실행 중인 에이전트 작업에 대한 제어는 그대로 유지됩니다. 동기화 실행 중에는 에이전트를 실행하면서 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> 이벤트를 처리할 수 있습니다.  
  
        > [!NOTE]  
        >  `false` 끌어오기 구독을 만들 때에 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> 값 (기본값)을 지정한 경우에는, <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Distributor%2A> <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorSecurityMode%2A>및 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorLogin%2A> 도 지정 해야 합니다. 구독에 대 한 에이전트 작업 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorPassword%2A> 관련 메타 데이터는 [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql)에서 사용할 수 없기 때문입니다.  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 끌어오기 구독을 동기화하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 클래스의 인스턴스를 만들고 다음 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>에 대한 구독 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>에 대해 구독이 속한 게시 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>에 대한 게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>에 대한 게시자 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>에 대해 1단계에서 만든 연결  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 나머지 구독 속성을 얻습니다. 이 메서드가 `false`를 반환하는 경우 구독이 있는지 확인합니다.  
  
4.  다음 방법 중 하나로 구독자에서 병합 에이전트를 시작합니다.  
  
    -   2단계에서 만든 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizeWithJob%2A> 의 인스턴스에서 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 메서드를 호출합니다. 이 메서드는 병합 에이전트를 비동기적으로 시작하고 에이전트 작업이 실행되는 동안 애플리케이션에 대한 반환을 즉시 제어합니다. [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 구독자인 경우 또는 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A>에 `false` 값(기본값)을 사용하여 구독을 만든 경우 이 메서드를 호출할 수 없습니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> 속성에서 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> 클래스의 인스턴스를 가져오고 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> 메서드를 호출합니다. 이 메서드는 병합 에이전트를 동기적으로 시작하고 실행 중인 에이전트 작업에 대한 제어는 그대로 유지됩니다. 동기화 실행 중에는 에이전트를 실행하면서 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> 이벤트를 처리할 수 있습니다.  
  
        > [!NOTE]  
        >  끌어오기 구독을 만들 때 `false` 에 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> 값 (기본값)을 지정한 경우에는,,,,, 및를 지정 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Distributor%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.HostName%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriptionType%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.ExchangeType%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorLogin%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorPassword%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherLogin%2A>해야 합니다. 구독에 대 한 에이전트 작업 관련 메타 데이터 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherPassword%2A> 는 [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql)에서 사용할 수 없기 때문입니다.  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a>예 (RMO)  
 다음은 트랜잭션 게시에 끌어오기 구독을 동기화하는 예로, 에이전트 작업을 사용하여 에이전트를 비동기적으로 시작합니다.  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub_withjob)]  
  
 다음은 트랜잭션 게시에 끌어오기 구독을 동기화하는 예로, 에이전트를 동기적으로 시작합니다.  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub)]  
  
 다음은 병합 게시에 끌어오기 구독을 동기화하는 예로, 에이전트 작업을 사용하여 에이전트를 비동기적으로 시작합니다.  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_withjob)]  
  
 다음은 병합 게시에 끌어오기 구독을 동기화하는 예로, 에이전트를 동기적으로 시작합니다.  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub)]  
  
 다음은 웹 동기화를 사용하여 병합 게시에 끌어오기 구독을 동기화하는 예입니다. 에이전트 작업 및 관련 구독 메타데이터를 사용하지 않고 구독을 만들었으므로 에이전트를 동기적으로 시작한 다음 추가 구독 정보를 제공해야 합니다.  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_NoJobWebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_nojobwebsync)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_NoJobWebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_nojobwebsync)]  
  
## <a name="see-also"></a>참고 항목  
 [데이터 동기화](synchronize-data.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [복제 보안을 위한 최선의 구현 방법](security/replication-security-best-practices.md)  
  
  
