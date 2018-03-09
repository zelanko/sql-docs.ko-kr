---
title: "끌어오기 구독 동기화 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pull subscriptions [SQL Server replication], synchronizing
- synchronization [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
ms.assetid: 3ca24b23-fdc3-408e-8208-a2ace48fc8e3
caps.latest.revision: "45"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb2902fc5b2e1c380ce9d31dab8a5f50f5ec8a2c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="synchronize-a-pull-subscription"></a>끌어오기 구독 동기화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [복제 에이전트](../../relational-databases/replication/agents/replication-agents-overview.md) 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 끌어오기 구독을 동기화하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **끌어오기 구독을 동기화하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Replication Agents](#ReplProg)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 구독은 배포 에이전트(스냅숏 및 트랜잭션 복제의 경우) 또는 병합 에이전트(병합 복제의 경우)에 의해 동기화됩니다. 에이전트는 지속적으로 실행하거나 수요에 따라 실행하거나 일정에 따라 실행할 수 있습니다. 동기화 일정을 설정하는 방법은 [동기화 일정 지정](../../relational-databases/replication/specify-synchronization-schedules.md)을 참조하세요.  
  
 **의** 로컬 구독 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]폴더에서 요청 시 구독을 동기화합니다.  
  
#### <a name="to-synchronize-a-pull-subscription-on-demand-in-management-studio"></a>Management Studio에서 요청 시 끌어오기 구독을 동기화하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  동기화할 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 상태 보기**를 클릭합니다.  
  
4.  **동기화 상태 보기 - \<Subscriber>:\<SubscriptionDatabase>** 대화 상자에서 **시작**을 클릭합니다. 동기화가 완료되면 **동기화 완료** 라는 메시지가 표시됩니다.  
  
5.  **닫기**를 클릭합니다.  
  
##  <a name="ReplProg"></a> Replication Agents  
 끌어오기 구독은 명령 프롬프트에서 적합한 복제 에이전트 실행 파일을 호출하여 프로그래밍 방식으로 요청 시 동기화할 수 있습니다. 호출한 복제 에이전트 실행 파일은 끌어오기 구독이 속한 게시 유형에 따라 달라집니다. 자세한 내용은 [Replication Agents](../../relational-databases/replication/agents/replication-agents.md)을 참조하세요.  
  
> [!NOTE]  
>  복제 에이전트는 명령 프롬프트에서 에이전트를 시작한 사용자의 Windows 인증 자격 증명을 사용하여 로컬 서버에 연결합니다. 이러한 자격 증명은 Windows 통합 인증을 사용하여 원격 서버에 연결할 때도 사용됩니다.  
  
#### <a name="to-start-the-distribution-agent-from-the-command-prompt-or-from-a-batch-file"></a>명령 프롬프트 또는 배치 파일에서 배포 에이전트를 시작하려면  
  
1.  _명령 프롬프트 또는 배치 파일에서 [distrib.exe](../../relational-databases/replication/agents/replication-distribution-agent.md) 를 실행하여 **복제 배포 에이전트**를 시작하고 다음 명령줄 인수를 지정합니다.  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Distributor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriptionType** = **1**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 다음 인수도 지정해야 합니다.  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **@publisher_security_mode**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
#### <a name="to-start-the-merge-agent-from-the-command-prompt-or-from-a-batch-file"></a>명령 프롬프트 또는 배치 파일에서 병합 에이전트를 시작하려면  
  
1.  명령 프롬프트 또는 배치 파일에서 [replmerg.exe](../../relational-databases/replication/agents/replication-merge-agent.md) 를 실행하여 **복제 병합 에이전트**를 시작하고 다음 명령줄 인수를 지정합니다.  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-PublisherSecurityMode** = **1**  
  
    -   **-Publication**  
  
    -   **-Distributor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType** = **1**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 다음 인수도 지정해야 합니다.  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **@publisher_security_mode**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
###  <a name="TsqlExample"></a> 예(복제 에이전트)  
 다음 예에서는 배포 에이전트를 시작하여 끌어오기 구독을 동기화합니다. 모든 연결은 Windows 인증을 사용하여 만듭니다.  
  
```  
 -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks  
SET SubscriptionDB=AdventureWorksReplica   
SET Publication=AdvWorksProductsTran  
  
-- Start the Distribution Agent.  
-- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\100\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 1;  
```  
  
 다음 예에서는 병합 에이전트를 시작하여 끌어오기 구독을 동기화합니다. 모든 연결은 Windows 인증을 사용하여 만듭니다.  
  
```  
-- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks  
SET SubscriptionDB=AdventureWorksReplica   
SET Publication=AdvWorksSalesOrdersMerge  
  
--Start the Merge Agent with concurrent upload and download processes.  
-- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\100\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
```  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 RMO(복제 관리 개체) 및 관리 코드 액세스를 사용하여 복제 에이전트 기능에 프로그래밍 방식으로 끌어오기 구독을 동기화할 수 있습니다. 끌어오기 구독을 동기화하는 데 사용하는 클래스는 구독이 속한 게시 유형에 따라 달라집니다.  
  
> [!NOTE]  
>  동기화가 응용 프로그램에 영향을 미치지 않고 자율적으로 실행하도록 하려면 에이전트를 비동기적으로 시작합니다. 그러나 진행률 표시줄을 표기하기 위해 동기화 프로세스 동안 동기화 결과를 모니터링하고 에이전트에서 콜백을 받으려면 에이전트를 동기적으로 시작해야 합니다. For [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 구독자의 경우 에이전트를 동기적으로 시작해야 합니다.  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 끌어오기 구독을 동기화하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 클래스의 인스턴스를 만들고 다음 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>에 대한 구독 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>에 대해 구독이 속한 게시 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>에 대한 게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>에 대한 게시자 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>에 대해 1단계에서 만든 연결  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 나머지 구독 속성을 얻습니다. 이 메서드가 **false**를 반환하는 경우 구독이 있는지 확인합니다.  
  
4.  다음 방법 중 하나로 구독자에서 배포 에이전트를 시작합니다.  
  
    -   2단계에서 만든 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizeWithJob%2A> 의 인스턴스에서 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 메서드를 호출합니다. 이 메서드는 배포 에이전트를 비동기적으로 시작하고 에이전트 작업이 실행되는 동안 응용 프로그램에 대한 반환을 즉시 제어합니다. [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 구독자인 경우 또는 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A>에 **false** 값(기본값)을 사용하여 구독을 만든 경우 이 메서드를 호출할 수 없습니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> 속성에서 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> 클래스의 인스턴스를 가져오고 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> 메서드를 호출합니다. 이 메서드는 에이전트를 동기적으로 시작하고 실행 중인 에이전트 작업에 대한 제어는 그대로 유지됩니다. 동기화 실행 중에는 에이전트를 실행하면서 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> 이벤트를 처리할 수 있습니다.  
  
        > [!NOTE]  
        >  [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)에서는 구독에 대한 에이전트 작업 관련 메타데이터를 사용할 수 없으므로 끌어오기 구독을 만들 때 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A>에 **false** 값(기본값)을 지정한 경우 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Distributor%2A>, <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorSecurityMode%2A>도 지정해야 하며 필요에 따라서는 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorPassword%2A> 도 지정해야 합니다.  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 끌어오기 구독을 동기화하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 클래스의 인스턴스를 만들고 다음 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>에 대한 구독 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>에 대해 구독이 속한 게시 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>에 대한 게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>에 대한 게시자 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>에 대해 1단계에서 만든 연결  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 나머지 구독 속성을 얻습니다. 이 메서드가 **false**를 반환하는 경우 구독이 있는지 확인합니다.  
  
4.  다음 방법 중 하나로 구독자에서 병합 에이전트를 시작합니다.  
  
    -   2단계에서 만든 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizeWithJob%2A> 의 인스턴스에서 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 메서드를 호출합니다. 이 메서드는 병합 에이전트를 비동기적으로 시작하고 에이전트 작업이 실행되는 동안 응용 프로그램에 대한 반환을 즉시 제어합니다. [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 구독자인 경우 또는 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A>에 **false** 값(기본값)을 사용하여 구독을 만든 경우 이 메서드를 호출할 수 없습니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> 속성에서 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> 클래스의 인스턴스를 가져오고 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> 메서드를 호출합니다. 이 메서드는 병합 에이전트를 동기적으로 시작하고 실행 중인 에이전트 작업에 대한 제어는 그대로 유지됩니다. 동기화 실행 중에는 에이전트를 실행하면서 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> 이벤트를 처리할 수 있습니다.  
  
        > [!NOTE]  
        >  [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)에서는 구독에 대한 에이전트 작업 관련 메타데이터를 사용할 수 없으므로 끌어오기 구독을 만들 때 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A>에 **false** 값(기본값)을 지정한 경우 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Distributor%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.HostName%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriptionType%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.ExchangeType%2A>도 지정해야 하며 필요에 따라서는 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorLogin%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorPassword%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherPassword%2A>도 지정해야 합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 다음은 트랜잭션 게시에 끌어오기 구독을 동기화하는 예로, 에이전트 작업을 사용하여 에이전트를 비동기적으로 시작합니다.  
  
```csharp  
// Define server, publication, and database names.  
String subscriberName = subscriberInstance;  
String publisherName = publisherInstance;  
String publicationName = "AdvWorksProductTran";  
String publicationDbName = "AdventureWorks";  
String subscriptionDbName = "AdventureWorksReplica";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
TransPullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define subscription properties.  
    subscription = new TransPullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription and the job exists, start the agent job.  
    if (subscription.LoadProperties() && subscription.AgentJobId != null)  
    {  
        subscription.SynchronizeWithJob();  
    }  
    else  
    {  
        // Do something here if the subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exists on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Do appropriate error handling here.  
    throw new ApplicationException("The subscription could not be synchronized.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksProductTran"  
Dim publicationDbName As String = "AdventureWorks"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As TransPullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define subscription properties.  
    subscription = New TransPullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription and the job exists, start the agent job.  
    If subscription.LoadProperties() And Not subscription.AgentJobId Is Nothing Then  
        subscription.SynchronizeWithJob()  
    Else  
        ' Do something here if the subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exists on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Do appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be synchronized.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
 다음은 트랜잭션 게시에 끌어오기 구독을 동기화하는 예로, 에이전트를 동기적으로 시작합니다.  
  
```csharp  
// Define the server, publication, and database names.  
string subscriberName = subscriberInstance;  
string publisherName = publisherInstance;  
string publicationName = "AdvWorksProductTran";  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
TransPullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define the pull subscription.  
    subscription = new TransPullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription exists, then start the synchronization.  
    if (subscription.LoadProperties())  
    {  
        // Check that we have enough metadata to start the agent.  
        if (subscription.PublisherSecurity != null)  
        {  
            // Synchronously start the Distribution Agent for the subscription.  
            subscription.SynchronizationAgent.Synchronize();  
        }  
        else  
        {  
            throw new ApplicationException("There is insufficent metadata to " +  
                "synchronize the subscription. Recreate the subscription with " +  
                "the agent job or supply the required agent properties at run time.");  
        }  
    }  
    else  
    {  
        // Do something here if the pull subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exist on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement appropriate error handling here.  
    throw new ApplicationException("The subscription could not be " +  
        "synchronized. Verify that the subscription has " +  
        "been defined correctly.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define the server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksProductTran"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As TransPullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define the pull subscription.  
    subscription = New TransPullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription exists, then start the synchronization.  
    If subscription.LoadProperties() Then  
        ' Check that we have enough metadata to start the agent.  
        If Not subscription.PublisherSecurity Is Nothing Then  
  
            ' Write agent output to a log file.  
            subscription.SynchronizationAgent.Output = "distagent.log"  
            subscription.SynchronizationAgent.OutputVerboseLevel = 2  
  
            ' Synchronously start the Distribution Agent for the subscription.  
            subscription.SynchronizationAgent.Synchronize()  
        Else  
            Throw New ApplicationException("There is insufficent metadata to " + _  
             "synchronize the subscription. Recreate the subscription with " + _  
             "the agent job or supply the required agent properties at run time.")  
        End If  
    Else  
        ' Do something here if the pull subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exist on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Implement appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be " + _  
     "synchronized. Verify that the subscription has " + _  
     "been defined correctly.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
 다음은 병합 게시에 끌어오기 구독을 동기화하는 예로, 에이전트 작업을 사용하여 에이전트를 비동기적으로 시작합니다.  
  
```csharp  
// Define server, publication, and database names.  
String subscriberName = subscriberInstance;  
String publisherName = publisherInstance;  
String publicationName = "AdvWorksSalesOrdersMerge";  
String publicationDbName = "AdventureWorks";  
String subscriptionDbName = "AdventureWorksReplica";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define subscription properties.  
    subscription = new MergePullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription and the job exists, start the agent job.  
    if (subscription.LoadProperties() && subscription.AgentJobId != null)  
    {  
        subscription.SynchronizeWithJob();  
    }  
    else  
    {  
        // Do something here if the subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exists on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Do appropriate error handling here.  
    throw new ApplicationException("The subscription could not be synchronized.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim publicationDbName As String = "AdventureWorks"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define subscription properties.  
    subscription = New MergePullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription and the job exists, start the agent job.  
    If subscription.LoadProperties() And Not subscription.AgentJobId Is Nothing Then  
        subscription.SynchronizeWithJob()  
    Else  
        ' Do something here if the subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exists on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Do appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be synchronized.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
 다음은 병합 게시에 끌어오기 구독을 동기화하는 예로, 에이전트를 동기적으로 시작합니다.  
  
```csharp  
// Define the server, publication, and database names.  
string subscriberName = subscriberInstance;  
string publisherName = publisherInstance;  
string publicationName = "AdvWorksSalesOrdersMerge";  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define the pull subscription.  
    subscription = new MergePullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription exists, then start the synchronization.  
    if (subscription.LoadProperties())  
    {  
        // Check that we have enough metadata to start the agent.  
        if (subscription.PublisherSecurity != null || subscription.DistributorSecurity != null)  
        {  
            // Synchronously start the Merge Agent for the subscription.  
            subscription.SynchronizationAgent.Synchronize();  
        }  
        else  
        {  
            throw new ApplicationException("There is insufficent metadata to " +  
                "synchronize the subscription. Recreate the subscription with " +  
                "the agent job or supply the required agent properties at run time.");  
        }  
    }  
    else  
    {  
        // Do something here if the pull subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exist on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement appropriate error handling here.  
    throw new ApplicationException("The subscription could not be " +  
        "synchronized. Verify that the subscription has " +  
        "been defined correctly.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define the server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define the pull subscription.  
    subscription = New MergePullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription exists, then start the synchronization.  
    If subscription.LoadProperties() Then  
        ' Check that we have enough metadata to start the agent.  
        If Not subscription.PublisherSecurity Is Nothing Or subscription.DistributorSecurity Is Nothing Then  
  
            ' Output agent messages to the console.   
            subscription.SynchronizationAgent.OutputVerboseLevel = 1  
            subscription.SynchronizationAgent.Output = ""  
  
            ' Synchronously start the Merge Agent for the subscription.  
            subscription.SynchronizationAgent.Synchronize()  
        Else  
            Throw New ApplicationException("There is insufficent metadata to " + _  
             "synchronize the subscription. Recreate the subscription with " + _  
             "the agent job or supply the required agent properties at run time.")  
        End If  
    Else  
        ' Do something here if the pull subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exist on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Implement appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be " + _  
     "synchronized. Verify that the subscription has " + _  
     "been defined correctly.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
 다음은 웹 동기화를 사용하여 병합 게시에 끌어오기 구독을 동기화하는 예입니다. 에이전트 작업 및 관련 구독 메타데이터를 사용하지 않고 구독을 만들었으므로 에이전트를 동기적으로 시작한 다음 추가 구독 정보를 제공해야 합니다.  
  
```csharp  
// Define the server, publication, and database names.  
string subscriberName = subscriberInstance;  
string publisherName = publisherInstance;  
string distributorName = distributorInstance;  
string publicationName = "AdvWorksSalesOrdersMerge";  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
string hostname = @"adventure-works\garrett1";  
string webSyncUrl = "https://" + publisherInstance + "/SalesOrders/replisapi.dll";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
MergePullSubscription subscription;  
MergeSynchronizationAgent agent;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define the pull subscription.  
    subscription = new MergePullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription exists, then start the synchronization.  
    if (subscription.LoadProperties())  
    {  
        // Get the agent for the subscription.  
        agent = subscription.SynchronizationAgent;  
  
        // Check that we have enough metadata to start the agent.  
        if (agent.PublisherSecurityMode == null)  
        {  
            // Set the required properties that could not be returned  
            // from the MSsubscription_properties table.   
            agent.PublisherSecurityMode = SecurityMode.Integrated;  
            agent.DistributorSecurityMode = SecurityMode.Integrated;  
            agent.Distributor = publisherName;  
            agent.HostName = hostname;  
  
            // Set optional Web synchronization properties.  
            agent.UseWebSynchronization = true;  
            agent.InternetUrl = webSyncUrl;  
            agent.InternetSecurityMode = SecurityMode.Standard;  
            agent.InternetLogin = winLogin;  
            agent.InternetPassword = winPassword;  
        }  
        // Enable agent output to the console.  
        agent.OutputVerboseLevel = 1;  
        agent.Output = "";  
  
        // Synchronously start the Merge Agent for the subscription.  
        agent.Synchronize();  
    }  
    else  
    {  
        // Do something here if the pull subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exist on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement appropriate error handling here.  
    throw new ApplicationException("The subscription could not be " +  
        "synchronized. Verify that the subscription has " +  
        "been defined correctly.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define the server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
Dim hostname As String = "adventure-works\garrett1"  
Dim webSyncUrl As String = "https://" + publisherInstance + "/SalesOrders/replisapi.dll"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As MergePullSubscription  
Dim agent As MergeSynchronizationAgent  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define the pull subscription.  
    subscription = New MergePullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription exists, then start the synchronization.  
    If subscription.LoadProperties() Then  
        ' Get the agent for the subscription.  
        agent = subscription.SynchronizationAgent  
  
        ' Check that we have enough metadata to start the agent.  
        If agent.PublisherSecurityMode = Nothing Then  
            ' Set the required properties that could not be returned  
            ' from the MSsubscription_properties table.   
            agent.PublisherSecurityMode = SecurityMode.Integrated  
            agent.Distributor = publisherInstance  
            agent.DistributorSecurityMode = SecurityMode.Integrated  
            agent.HostName = hostname  
  
            ' Set optional Web synchronization properties.  
            agent.UseWebSynchronization = True  
            agent.InternetUrl = webSyncUrl  
            agent.InternetSecurityMode = SecurityMode.Standard  
            agent.InternetLogin = winLogin  
            agent.InternetPassword = winPassword  
        End If  
  
        ' Enable agent logging to the console.  
        agent.OutputVerboseLevel = 1  
        agent.Output = ""  
  
        ' Synchronously start the Merge Agent for the subscription.  
        agent.Synchronize()  
    Else  
        ' Do something here if the pull subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exist on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Implement appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be " + _  
     "synchronized. Verify that the subscription has " + _  
     "been defined correctly.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 동기화](../../relational-databases/replication/synchronize-data.md)   
 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
