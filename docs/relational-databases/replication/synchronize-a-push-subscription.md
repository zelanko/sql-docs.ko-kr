---
title: "밀어넣기 구독 동기화 | Microsoft Docs"
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
  - "동기화 [SQL Server 복제], 밀어넣기 구독"
  - "구독 [SQL Server 복제], 밀어넣기"
  - "밀어넣기 구독 [SQL Server 복제], 동기화"
ms.assetid: 0cfa7ae5-91d3-4a4f-9edf-a852d45783b5
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# 밀어넣기 구독 동기화
  이 항목에서 밀어넣기 구독을 동기화 하는 방법에 설명 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용 하 여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [복제 에이전트](../../relational-databases/replication/agents/replication-agents-overview.md), 또는 관리 개체 RMO (복제).  
  
 **항목 내용**  
  
-   **밀어넣기 구독을 동기화하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [복제 에이전트](#ReplProg)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 구독은 배포 에이전트(스냅숏 및 트랜잭션 복제의 경우) 또는 병합 에이전트(병합 복제의 경우)에 의해 동기화됩니다. 에이전트는 지속적으로 실행하거나 수요에 따라 실행하거나 일정에 따라 실행할 수 있습니다. 동기화 일정을 지정 하는 방법에 대 한 자세한 내용은 참조 [동기화 일정 지정](../../relational-databases/replication/specify-synchronization-schedules.md)합니다.  
  
 요청 시 구독을 동기화는 **로컬 게시** 및 **로컬 구독** 폴더에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 **모든 구독** 복제 모니터의 탭 합니다. Oracle 게시에 대한 구독은 구독자에서 요청 시 동기화할 수 없습니다. 복제 모니터를 시작 하는 방법에 대 한 정보를 참조 하십시오. [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)합니다.  
  
#### Management Studio에서 요청 시 밀어넣기 구독을 동기화하려면(게시자)  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  구독을 동기화할 게시를 확장합니다.  
  
4.  동기화를 클릭 하 고 싶은 구독을 마우스 오른쪽 단추로 클릭 **동기화 상태 보기**합니다.  
  
5.  에 **동기화 상태 보기-\< 구독자>: \< SubscriptionDatabase>** 대화 상자를 클릭 하 여 **시작**합니다. 동기화가 완료되면 **동기화 완료** 라는 메시지가 표시됩니다.  
  
6.  **닫기**를 클릭합니다.  
  
#### Management Studio에서 요청 시 밀어넣기 구독을 동기화하려면(구독자)  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  동기화를 클릭 하 고 싶은 구독을 마우스 오른쪽 단추로 클릭 **동기화 상태 보기**합니다.  
  
4.  배포자 연결 설정에 대한 메시지가 표시됩니다. **확인**을 클릭합니다.  
  
5.  에 **동기화 상태 보기-\< 구독자>: \< SubscriptionDatabase>** 대화 상자를 클릭 하 여 **시작**합니다. 동기화가 완료되면 **동기화 완료** 라는 메시지가 표시됩니다.  
  
6.  **닫기**를 클릭합니다.  
  
#### 복제 모니터에서 요청 시 밀어넣기 구독을 동기화하려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **모든 구독** 탭을 클릭합니다.  
  
3.  동기화를 클릭 하 고 싶은 구독을 마우스 오른쪽 단추로 클릭 **동기화 시작**합니다.  
  
4.  동기화 진행률을 보려면, 구독을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **세부 정보 보기**합니다.  
  
##  <a name="ReplProg"></a> 복제 에이전트 사용  
 밀어넣기 구독은 명령 프롬프트에서 적합한 복제 에이전트 실행 파일을 호출하여 프로그래밍 방식으로 요청 시 동기화할 수 있습니다. 호출한 복제 에이전트 실행 파일은 밀어넣기 구독이 속한 게시 유형에 따라 달라집니다.  
  
#### 배포 에이전트를 시작하여 트랜잭션 게시에 밀어넣기 구독을 동기화하려면  
  
1.  배포자의 명령 프롬프트나 배치 파일에서 **distrib.exe**를 실행하고 다음 명령줄 인수를 지정합니다.  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Distributor**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType = 0**  
  
     SQL Server 인증을 사용하는 경우 다음 인수도 지정해야 합니다.  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode = 0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode = 0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode = 0**  
  
        > [!IMPORTANT]  
        >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
#### 병합 에이전트를 시작하여 병합 게시에 밀어넣기 구독을 동기화하려면  
  
1.  배포자의 명령 프롬프트나 배치 파일에서 **replmerg.exe**를 실행하고 다음 명령줄 인수를 지정합니다.  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Publication**  
  
    -   **-Distributor**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType = 0**  
  
     SQL Server 인증을 사용하는 경우 다음 인수도 지정해야 합니다.  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode = 0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode = 0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode = 0**  
  
        > [!IMPORTANT]  
        >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
###  <a name="TsqlExample"></a> 예(복제 에이전트)  
 다음 예에서는 배포 에이전트를 시작하여 밀어넣기 구독을 동기화합니다.  
  
```  
  
REM -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks2012  
SET SubscriptionDB=AdventureWorks2012Replica   
SET Publication=AdvWorksProductsTran  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4  
  
```  
  
 다음 예에서는 병합 에이전트를 시작하여 밀어넣기 구독을 동기화합니다.  
  
```  
  
REM -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks2012  
SET SubscriptionDB=AdventureWorks2012Replica   
SET Publication=AdvWorksSalesOrdersMerge  
  
REM -- Start the Merge Agent.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE"  -Publisher %Publisher%   
-Subscriber  %Subscriber%  -Distributor %Publisher% -PublisherDB  %PublicationDB%   
-SubscriberDB %SubscriptionDB% -Publication %Publication% -PublisherSecurityMode 1   
-OutputVerboseLevel 3  -Output -SubscriberSecurityMode 1  -SubscriptionType 0   
-DistributorSecurityMode 1  
  
```  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 RMO(복제 관리 개체) 및 관리 코드 액세스를 사용하여 복제 에이전트 기능에 프로그래밍 방식으로 밀어넣기 구독을 동기화할 수 있습니다. 밀어넣기 구독을 동기화하는 데 사용하는 클래스는 구독이 속한 게시 유형에 따라 달라집니다.  
  
> [!NOTE]  
>  동기화가 응용 프로그램에 영향을 미치지 않고 자율적으로 실행하도록 하려면 에이전트를 비동기적으로 시작합니다. 그러나 진행률 표시줄을 표시하기 위해 동기화 프로세스 동안 동기화 결과를 모니터링하고 에이전트에서 콜백을 받으려면 에이전트를 동기적으로 시작해야 합니다. For [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 구독자의 경우 에이전트를 동기적으로 시작해야 합니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 밀어넣기 구독을 동기화하려면  
  
1.  사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransSubscription> 클래스 및 다음 속성을 설정 합니다.  
  
    -   게시 데이터베이스 이름에 대 한 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>합니다.  
  
    -   구독에 속한 게시의 이름 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>합니다.  
  
    -   에 대 한 구독 데이터베이스의 이름을 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>합니다.  
  
    -   에 대 한 구독자의 이름을 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>합니다.  
  
    -   에 대해 1 단계에서 만든 연결 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>합니다.  
  
3.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 를 나머지 구독 속성을 가져오는 메서드입니다. 이 메서드가 **false**를 반환하는 경우 구독이 있는지 확인합니다.  
  
4.  다음 방법 중 하나로 배포자에서 배포 에이전트를 시작합니다.  
  
    -   호출 된 <xref:Microsoft.SqlServer.Replication.TransSubscription.SynchronizeWithJob%2A> 메서드 인스턴스의 <xref:Microsoft.SqlServer.Replication.TransSubscription> 2 단계에서 합니다. 이 메서드는 배포 에이전트를 비동기적으로 시작하고 에이전트 작업이 실행되는 동안 응용 프로그램에 대한 반환을 즉시 제어합니다. 값이 구독을 만든 경우에이 메서드를 호출할 수 없습니다 **false** 에 대 한 <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A>합니다.  
  
    -   인스턴스를 가져올는 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> 에서 클래스는 <xref:Microsoft.SqlServer.Replication.TransSubscription.SynchronizationAgent%2A> 속성과 호출의 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> 메서드. 이 메서드는 에이전트를 동기적으로 시작하고 실행 중인 에이전트 작업에 대한 제어는 그대로 유지됩니다. 동기 실행 하는 동안 처리할 수는 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> 에이전트가 실행 되는 동안 이벤트입니다.  
  
#### 병합 게시에 밀어넣기 구독을 동기화하려면  
  
1.  사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 클래스를 다음 속성을 설정 합니다.  
  
    -   게시 데이터베이스 이름에 대 한 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>합니다.  
  
    -   구독에 속한 게시의 이름 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>합니다.  
  
    -   에 대 한 구독 데이터베이스의 이름을 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>합니다.  
  
    -   에 대 한 구독자의 이름을 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>합니다.  
  
    -   에 대해 1 단계에서 만든 연결 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>합니다.  
  
3.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 를 나머지 구독 속성을 가져오는 메서드입니다. 이 메서드가 **false**를 반환하는 경우 구독이 있는지 확인합니다.  
  
4.  다음 방법 중 하나로 배포자에서 병합 에이전트를 시작합니다.  
  
    -   호출 된 <xref:Microsoft.SqlServer.Replication.MergeSubscription.SynchronizeWithJob%2A> 메서드 인스턴스의 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 2 단계에서 합니다. 이 메서드는 병합 에이전트를 비동기적으로 시작하고 에이전트 작업이 실행되는 동안 응용 프로그램에 대한 반환을 즉시 제어합니다. 값이 구독을 만든 경우에이 메서드를 호출할 수 없습니다 **false** 에 대 한 <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A>합니다.  
  
    -   인스턴스를 가져올는 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> 에서 클래스는 <xref:Microsoft.SqlServer.Replication.MergeSubscription.SynchronizationAgent%2A> 속성과 호출의 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> 메서드. 이 메서드는 병합 에이전트를 동기적으로 시작하고 실행 중인 에이전트 작업에 대한 제어는 그대로 유지됩니다. 동기 실행 하는 동안 처리할 수는 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> 에이전트가 실행 되는 동안 이벤트입니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 다음은 트랜잭션 게시에 밀어넣기 구독을 동기화하는 예로, 에이전트 작업을 사용하여 에이전트를 비동기적으로 시작합니다.  
  
 [!code-csharp[HowTo#rmo_SyncTranPushSub_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_synctranpushsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPushSub_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_synctranpushsub_withjob)]  
  
 다음은 트랜잭션 게시에 밀어넣기 구독을 동기화하는 예로, 에이전트를 동기적으로 시작합니다.  
  
 [!code-csharp[HowTo#rmo_SyncTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_synctranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_synctranpushsub)]  
  
 다음은 병합 게시에 밀어넣기 구독을 동기화하는 예로, 에이전트 작업을 사용하여 에이전트를 비동기적으로 시작합니다.  
  
 [!code-csharp[HowTo#rmo_SyncMergePushSub_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_syncmergepushsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePushSub_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_syncmergepushsub_withjob)]  
  
 다음은 병합 게시에 밀어넣기 구독을 동기화하는 예로, 에이전트를 동기적으로 시작합니다.  
  
 [!code-csharp[HowTo#rmo_SyncMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_syncmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_syncmergepushsub)]  
  
## 참고 항목  
 [복제 관리 개체 개념](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [데이터 동기화](../../relational-databases/replication/synchronize-data.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  