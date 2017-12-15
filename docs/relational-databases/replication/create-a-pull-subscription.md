---
title: "끌어오기 구독 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/17/2017
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
- pull subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 41d1886d-59c9-41fc-9bd6-a59b40e0af6e
caps.latest.revision: "46"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bca4071c25a248b235b59e71957f7ecbe0149de1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="create-a-pull-subscription"></a>끌어오기 구독 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 끌어오기 구독을 만드는 방법에 대해 설명합니다.  
  
 P2P 복제에 대한 끌어오기 구독 설정은 스크립트를 통해서는 가능하지만 마법사를 통해서는 사용할 수 없습니다.  
 
  ##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 구독 마법사를 사용하여 게시자나 구독자에서 끌어오기 구독을 만듭니다. 마법사의 페이지에 따라 다음을 수행하세요.  
  
-   게시자와 게시를 지정합니다.  
  
-   복제 에이전트가 실행될 위치를 선택합니다. 끌어오기 구독의 경우 게시 유형에 따라 **배포 에이전트 위치** 페이지나 **병합 에이전트 위치** 페이지에서 **각 에이전트를 해당 구독자(끌어오기 구독)에서 실행** 을 선택합니다.  
  
-   구독자와 구독 데이터베이스를 지정합니다.  
  
-   복제 에이전트에서 설정한 연결에 사용할 로그인과 암호를 지정합니다.  
  
    -   스냅숏 및 트랜잭션 게시에 대한 구독의 경우 **배포 에이전트 보안** 페이지에서 자격 증명을 지정합니다.  
  
    -   병합 게시에 대한 구독의 경우 **병합 에이전트 보안** 페이지에서 자격 증명을 지정합니다.  
  
     각 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)를 참조하세요.  
  
-   동기화 일정과 구독자의 초기화 시기를 지정합니다.  
  
-   구독 유형, 매개 변수가 있는 필터링에 대한 값, 게시에 웹 동기화를 사용할 수 있는 경우 HTTPS를 통한 동기화 정보 등 병합 게시에 대한 추가 옵션을 지정합니다.  
  
-   구독자가 게시자의 변경 내용을 즉시 커밋할지 아니면 큐에 쓸지 여부, 구독자에서 게시자로 연결하는 데 사용할 자격 증명 등, 트랜잭션 게시에 대해 구독 업데이트를 허용하는 추가 옵션을 지정합니다.  
  
-   경우에 따라 구독을 스크립팅합니다.  
  
#### <a name="to-create-a-pull-subscription-from-the-publisher"></a>게시자에서 끌어오기 구독을 만들려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  하나 이상의 구독을 만들 게시를 마우스 오른쪽 단추로 클릭한 다음 **새 구독**을 클릭합니다.  
  
4.  새 구독 마법사의 페이지를 완료합니다.  
  
#### <a name="to-create-a-pull-subscription-from-the-subscriber"></a>구독자에서 끌어오기 구독을 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장합니다.  
  
3.  **로컬 구독** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 구독**을 클릭합니다.  
  
4.  새 구독 마법사의 **게시** 페이지에 있는 **게시자** 드롭다운 목록에서 **\<SQL Server 게시자 찾기>** 또는 **\<Oracle 게시자 찾기>**를 선택합니다.  
  
5.  **서버에 연결** 대화 상자에서 게시자에 연결합니다.  
  
6.  **게시** 페이지에서 게시를 선택합니다.  
  
7.  새 구독 마법사의 페이지를 완료합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 끌어오기 구독은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 만들 수 있습니다. 사용되는 저장 프로시저는 구독이 속한 게시 유형에 따라 달라집니다.  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 끌어오기 구독을 만들려면  
  
1.  게시자에서 [sp_helppublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행하여 게시에서 끌어오기 구독을 지원하는지 확인합니다.  
  
    -   결과 집합의 **allow_pull** 값이 **1**이면 게시에서 끌어오기 구독을 지원합니다.  
  
    -   **allow_pull**의 값이 **0**이면 **@property**에 **allow_pull**을, **@value**에 **true**를 지정하여 [sp_changepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)을 실행합니다.  
  
2.  구독자에서 [sp_addpullsubscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)을 실행합니다. **@publisher** 및 **@publication**을 지정합니다. 구독 업데이트에 대한 자세한 내용은 [Create an Updatable Subscription to a Transactional Publication](https://msdn.microsoft.com/library/ms152769.aspx)을 참조하세요.   
  
3.  구독자에서 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)를 실행합니다. 다음을 지정합니다.  
  
    -   구독자에서 배포 에이전트가 실행되는 **@publisher**또는 RMO(복제 관리 개체)를 사용하여 **@publisher_db**및 **@publication** 매개 변수  
  
    -   구독자에서 배포 에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] @job_login **@job_login** 을 지정하고 **@job_password**를 참조하세요.  
  
        > [!NOTE]  
        >  Windows 통합 인증을 사용하여 만든 연결은 항상 **@job_login** 을 지정하고 **@job_password**를 참조하세요. 배포 에이전트는 항상 Windows 통합 인증을 사용하여 구독자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 배포자에 연결합니다.  
  
    -   (선택 사항) **@distributor_security_mode**에 대한 **0** 값과, **@distributor_login** 및 **@distributor_password**에 대한 SQL Server 로그인 정보(배포자에 연결할 때 SQL Server 인증을 사용해야 하는 경우).  
  
    -   이 구독에 대한 배포 에이전트 작업 일정. 자세한 내용은 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)을 참조하세요.  
  
4.  게시자에서 [sp_addsubscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)을 실행하여 끌어오기 구독을 등록합니다. **@publication**, **@subscriber**및 **@destination_db**를 지정합니다. **@subscription_type**에 **pull** 값을 지정합니다.  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 끌어오기 구독을 만들려면  
  
1.  게시자에서 [sp_helpmergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)을 실행하여 게시에서 끌어오기 구독을 지원하는지 확인합니다.  
  
    -   결과 집합의 **allow_pull** 값이 **1**이면 게시에서 끌어오기 구독을 지원합니다.  
  
    -   **allow_pull**의 값이 **0**이면 **@property**에 **allow_pull**을, **@value**에 **true**를 지정하여 [sp_changemergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)을 실행합니다.  
  
2.  구독자에서 [sp_addmergepullsubscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)을 실행합니다. **@publisher**, **@publisher_db**, **@publication**과 다음 매개 변수를 지정합니다.  
  
    -   **@subscriber_type** - 클라이언트 구독에 **local** 을 지정하고 서버 구독에 **global** 을 지정합니다.  
  
    -   **@subscription_priority** - 구독의 우선 순위를 지정합니다(**0.00** ~ **99.99**). 이 지정은 서버 구독에만 필요합니다.  
  
         자세한 내용은 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)을 참조하세요.  
  
3.  구독자에서 [sp_addmergepullsubscription_agent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)를 실행합니다. 다음 매개 변수를 지정합니다.  
  
    -   **@publisher**또는 RMO(복제 관리 개체)를 사용하여 **@publisher_db**및 **@publication**를 참조하세요.  
  
    -   **@job_login** 및 **@job_password**에 대해 구독자에서 배포 에이전트가 실행되는 Windows 자격 증명을 지정합니다.  
  
        > [!NOTE]  
        >  Windows 통합 인증을 사용하여 만든 연결은 항상 **@job_login** 및 **@job_password**에서 SQL Server 이외 구독자에 대한 구독을 만드는 방법에 대해 설명합니다. 병합 에이전트는 항상 Windows 통합 인증을 사용하여 구독자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 배포자 및 게시자에 연결합니다.  
  
    -   (옵션) 배포자에 연결할 때 **0** 에 **@distributor_security_mode** 0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] @distributor_login **@distributor_login** 을 지정하고 **@distributor_password**에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 정보 지정  
  
    -   (옵션) 배포자에 연결할 때 **0** 에 **@publisher_security_mode** 0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] @distributor_login **@publisher_login** 을 지정하고 **@publisher_password**에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 정보 지정  
  
    -   이 구독에 대한 병합 에이전트 작업 일정. 자세한 내용은 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)을 참조하세요.  
  
4.  게시자에서 [sp_addmergesubscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)을 실행합니다. 이때 **@publication**, **@subscriber**, **@subscriber_db**, **@subscription_type**에 값 **pull**을 지정합니다. 끌어오기 구독이 등록됩니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음은 트랜잭션 게시에 끌어오기 구독을 만드는 예입니다. 구독자에서 첫 번째 일괄 처리가 실행되고 두 번째 일괄 처리는 게시자에서 실행됩니다. 로그인 및 암호 값은 sqlcmd 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Execute this batch at the Subscriber.  
DECLARE @publication AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @publicationDB AS sysname;  
SET @publication = N'AdvWorksProductTran';  
SET @publisher = $(PubServer);  
SET @publicationDB = N'AdventureWorks';  
  
-- At the subscription database, create a pull subscription   
-- to a transactional publication.  
USE [AdventureWorksReplica]  
EXEC sp_addpullsubscription   
  @publisher = @publisher,   
  @publication = @publication,   
  @publisher_db = @publicationDB;  
  
-- Add an agent job to synchronize the pull subscription.  
EXEC sp_addpullsubscription_agent   
  @publisher = @publisher,   
  @publisher_db = @publicationDB,   
  @publication = @publication,   
  @distributor = @publisher,   
  @job_login = $(Login),   
  @job_password = $(Password);  
GO  
```  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Execute this batch at the Publisher.  
DECLARE @publication AS sysname;  
DECLARE @subscriber AS sysname;  
DECLARE @subscriptionDB AS sysname;  
SET @publication = N'AdvWorksProductTran';  
SET @subscriber = $(SubServer);  
SET @subscriptionDB = N'AdventureWorksReplica';  
  
-- At the Publisher, register the subscription, using the defaults.  
EXEC sp_addsubscription   
  @publication = @publication,   
  @subscriber = @subscriber,   
  @destination_db = @subscriptionDB,   
  @subscription_type = N'pull',  
  @status = N'subscribed';  
GO  
  
```  
  
 다음은 병합 게시에 끌어오기 구독을 만드는 예입니다. 구독자에서 첫 번째 일괄 처리가 실행되고 두 번째 일괄 처리는 게시자에서 실행됩니다. 로그인 및 암호 값은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Execute this batch at the Subscriber.  
DECLARE @publication AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @publicationDB AS sysname;  
DECLARE @hostname AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @publisher = $(PubServer);  
SET @publicationDB = N'AdventureWorks';  
SET @hostname = N'adventure-works\david8';  
  
-- At the subscription database, create a pull subscription   
-- to a merge publication.  
USE [AdventureWorksReplica]  
EXEC sp_addmergepullsubscription   
  @publisher = @publisher,   
  @publication = @publication,   
  @publisher_db = @publicationDB;  
  
-- Add an agent job to synchronize the pull subscription.   
EXEC sp_addmergepullsubscription_agent   
  @publisher = @publisher,   
  @publisher_db = @publicationDB,   
  @publication = @publication,   
  @distributor = @publisher,   
  @job_login = $(Login),   
  @job_password = $(Password),  
  @hostname = @hostname;  
GO  
```  
  
```  
-- Execute this batch at the Publisher.  
DECLARE @myMergePub  AS sysname;  
DECLARE @mySub       AS sysname;  
DECLARE @mySubDB     AS sysname;  
  
SET @myMergePub = N'AdvWorksSalesOrdersMerge';  
SET @mySub = N'MYSUBSERVER';  
SET @mySubDB = N'AdventureWorksReplica';  
  
-- At the Publisher, register the subscription, using the defaults.  
USE [AdventureWorks]  
EXEC sp_addmergesubscription @publication = @myMergePub,   
@subscriber = @mySub, @subscriber_db = @mySubDB,   
@subscription_type = N'pull';  
GO  
```  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 끌어오기 구독을 만드는 데 사용되는 RMO 클래스는 구독이 속한 게시 유형에 따라 달라집니다.  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 끌어오기 구독을 만들려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 및 게시자 모두에 대한 연결을 만듭니다.  
  
2.  1단계에서 만든 게시자 연결을 사용하여 <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 및 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>를 지정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 지정한 속성이 올바르지 않거나 서버에 게시가 없는 것입니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 속성과 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull> 사이에서 비트 논리 AND(Visual C#의 **&** 및 Visual Basic의 **And**)를 수행합니다. 결과가 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>이면 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 와**|** 속성과 **Or** 및 Visual Basic의 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 를 지정하고 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>를 참조하세요. 그런 다음 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 를 호출하여 끌어오기 구독을 설정합니다.  
  
5.  구독 데이터베이스가 없는 경우 <xref:Microsoft.SqlServer.Management.Smo.Database> 클래스를 사용하여 만듭니다. 자세한 내용은 [데이터베이스 생성, 변경 및 제거](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)를 참조하세요.  
  
6.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 클래스의 인스턴스를 만듭니다.  
  
7.  다음 구독 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 대해 1단계에서 만든 구독자에 대한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>에 대한 구독 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>에 대한 게시자 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>에 대한 게시 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>에 대한 게시 이름  
  
    -   구독자에서 배포 에이전트가 실행되는 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 을 지정하고 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 필드와 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 필드. 이 계정은 Windows 인증을 사용하여 구독자에 대한 로컬 연결 및 원격 연결을 만드는 데 사용됩니다.  
  
        > [!NOTE]  
        >  **sysadmin** 고정 서버 역할의 멤버가 구독을 만들 때 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>를 설정할 필요는 없지만 설정해 두는 것이 좋습니다. 이 경우 에이전트는 SQL Server 에이전트 계정을 가장합니다. 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
    -   (옵션) 배포자에 연결할 때 **@value** 에 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> 값. **false**(기본값)를 지정한 경우 구독을 프로그래밍 방식으로만 동기화할 수 있으므로 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> 속성에서 이 개체에 액세스할 때 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent>의 추가 속성을 지정해야 합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
        > [!NOTE]  
        >  일부 버전의 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요. Express 구독자에 대해 **true** 값을 지정한 경우 에이전트 작업은 만들어지지 않습니다. 그러나 중요한 구독 관련 메타데이터는 구독자에 저장됩니다.  
  
    -   (옵션) SQL Server 인증을 사용하여 배포자에 연결할 때 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 의 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드와 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 또는 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 필드  
  
8.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 메서드를 호출합니다.  
  
9. 2단계에서 만들어진 <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 사용하여 <xref:Microsoft.SqlServer.Replication.TransPublication.MakePullSubscriptionWellKnown%2A> 메서드를 호출한 다음 끌어오기 구독을 게시자로 등록합니다. 이 등록이 이미 존재하는 경우 예외가 발생합니다.  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 끌어오기 구독을 만들려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 및 게시자 모두에 대한 연결을 만듭니다.  
  
2.  1단계에서 만든 게시자 연결을 사용하여 <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>및 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>를 지정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 지정한 속성이 올바르지 않거나 서버에 게시가 없는 것입니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 속성과 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull> 사이에서 비트 논리 AND(Visual C#의 **&** 및 Visual Basic의 **And**)를 수행합니다. 결과가 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>이면 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 와**|** 속성과 **Or** 및 Visual Basic의 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 를 지정하고 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>를 참조하세요. 그런 다음 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 를 호출하여 끌어오기 구독을 설정합니다.  
  
5.  구독 데이터베이스가 없는 경우 <xref:Microsoft.SqlServer.Management.Smo.Database> 클래스를 사용하여 만듭니다. 자세한 내용은 [데이터베이스 생성, 변경 및 제거](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)를 참조하세요.  
  
6.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 클래스의 인스턴스를 만듭니다.  
  
7.  다음 구독 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 대해 1단계에서 만든 구독자에 대한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>에 대한 구독 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>에 대한 게시자 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>에 대한 게시 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>에 대한 게시 이름  
  
    -   구독자에서 배포 에이전트가 실행되는 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 을 지정하고 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 필드와 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 필드. 이 계정은 Windows 인증을 사용하여 구독자에 대한 로컬 연결 및 원격 연결을 만드는 데 사용됩니다.  
  
        > [!NOTE]  
        >  **sysadmin** 고정 서버 역할의 멤버가 구독을 만들 때 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>를 설정할 필요는 없지만 설정해 두는 것이 좋습니다. 이 경우 에이전트는 SQL Server 에이전트 계정을 가장합니다. 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
    -   (옵션) 배포자에 연결할 때 **@value** 에 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> 값. **false**(기본값)를 지정한 경우 구독을 프로그래밍 방식으로만 동기화할 수 있으므로 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> 속성에서 이 개체에 액세스할 때 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent>의 추가 속성을 지정해야 합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
    -   (옵션) SQL Server 인증을 사용하여 배포자에 연결할 때 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 의 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드와 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 또는 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 필드  
  
    -   (옵션) SQL Server 인증을 사용하여 게시자에 연결할 때 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 의 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드와 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 또는 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 필드  
  
8.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 메서드를 호출합니다.  
  
9. 2단계에서 만들어진 <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 사용하여 <xref:Microsoft.SqlServer.Replication.MergePublication.MakePullSubscriptionWellKnown%2A> 메서드를 호출한 다음 끌어오기 구독을 게시자로 등록합니다. 이 등록이 이미 존재하는 경우 예외가 발생합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 다음은 트랜잭션 게시에 끌어오기 구독을 만드는 예입니다. 배포 에이전트 작업을 만드는 데 사용되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정 자격 증명은 런타임에 전달됩니다.  
  
```csharp  
// Define the Publisher, publication, and databases.  
string publicationName = "AdvWorksProductTran";  
string publisherName = publisherInstance;  
string subscriberName = subscriberInstance;  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
  
//Create connections to the Publisher and Subscriber.  
ServerConnection subscriberConn = new ServerConnection(subscriberName);  
ServerConnection publisherConn = new ServerConnection(publisherName);  
  
// Create the objects that we need.  
TransPublication publication;  
TransPullSubscription subscription;  
  
try  
{  
    // Connect to the Publisher and Subscriber.  
    subscriberConn.Connect();  
    publisherConn.Connect();  
  
    // Ensure that the publication exists and that   
    // it supports pull subscriptions.  
    publication = new TransPublication();  
    publication.Name = publicationName;  
    publication.DatabaseName = publicationDbName;  
    publication.ConnectionContext = publisherConn;  
  
    if (publication.IsExistingObject)  
    {  
        if ((publication.Attributes & PublicationAttributes.AllowPull) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowPull;  
        }  
  
        // Define the pull subscription.  
        subscription = new TransPullSubscription();  
        subscription.ConnectionContext = subscriberConn;  
        subscription.PublisherName = publisherName;  
        subscription.PublicationName = publicationName;  
        subscription.PublicationDBName = publicationDbName;  
        subscription.DatabaseName = subscriptionDbName;  
  
        // Specify the Windows login credentials for the Distribution Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin;  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword;  
  
        // Make sure that the agent job for the subscription is created.  
        subscription.CreateSyncAgentByDefault = true;  
  
        // By default, subscriptions to transactional publications are synchronized   
        // continuously, but in this case we only want to synchronize on demand.  
        subscription.AgentSchedule.FrequencyType = ScheduleFrequencyType.OnDemand;  
  
        // Create the pull subscription at the Subscriber.  
        subscription.Create();  
  
        Boolean registered = false;  
  
        // Verify that the subscription is not already registered.  
        foreach (TransSubscription existing  
            in publication.EnumSubscriptions())  
        {  
            if (existing.SubscriberName == subscriberName  
                && existing.SubscriptionDBName == subscriptionDbName)  
            {  
                registered = true;  
            }  
        }  
        if (!registered)  
        {  
            // Register the subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown(  
                subscriberName, subscriptionDbName,  
                SubscriptionSyncType.Automatic,  
                TransSubscriberType.ReadOnly);  
        }  
    }  
    else  
    {  
        // Do something here if the publication does not exist.  
        throw new ApplicationException(String.Format(  
            "The publication '{0}' does not exist on {1}.",  
            publicationName, publisherName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement the appropriate error handling here.  
    throw new ApplicationException(String.Format(  
        "The subscription to {0} could not be created.", publicationName), ex);  
}  
finally  
{  
    subscriberConn.Disconnect();  
    publisherConn.Disconnect();  
}  
  
```  
  
```vb  
' Define the Publisher, publication, and databases.  
Dim publicationName As String = "AdvWorksProductTran"  
Dim publisherName As String = publisherInstance  
Dim subscriberName As String = subscriberInstance  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
  
'Create connections to the Publisher and Subscriber.  
Dim subscriberConn As ServerConnection = New ServerConnection(subscriberName)  
Dim publisherConn As ServerConnection = New ServerConnection(publisherName)  
  
' Create the objects that we need.  
Dim publication As TransPublication  
Dim subscription As TransPullSubscription  
  
Try  
    ' Connect to the Publisher and Subscriber.  
    subscriberConn.Connect()  
    publisherConn.Connect()  
  
    ' Ensure that the publication exists and that   
    ' it supports pull subscriptions.  
    publication = New TransPublication()  
    publication.Name = publicationName  
    publication.DatabaseName = publicationDbName  
    publication.ConnectionContext = publisherConn  
  
    If publication.IsExistingObject Then  
        If (publication.Attributes And PublicationAttributes.AllowPull) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowPull  
        End If  
  
        ' Define the pull subscription.  
        subscription = New TransPullSubscription()  
        subscription.ConnectionContext = subscriberConn  
        subscription.PublisherName = publisherName  
        subscription.PublicationName = publicationName  
        subscription.PublicationDBName = publicationDbName  
        subscription.DatabaseName = subscriptionDbName  
        subscription.Description = "Pull subscription to " + publicationDbName _  
        + " on " + subscriberName + "."  
  
        ' Specify the Windows login credentials for the Distribution Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword  
  
        ' Make sure that the agent job for the subscription is created.  
        subscription.CreateSyncAgentByDefault = True  
  
        ' By default, subscriptions to transactional publications are synchronized   
        ' continuously, but in this case we only want to synchronize on demand.  
        subscription.AgentSchedule.FrequencyType = ScheduleFrequencyType.OnDemand  
  
        ' Create the pull subscription at the Subscriber.  
        subscription.Create()  
  
        Dim registered As Boolean = False  
  
        ' Verify that the subscription is not already registered.  
        For Each existing As TransSubscription In publication.EnumSubscriptions()  
            If existing.SubscriberName = subscriberName And _  
                existing.SubscriptionDBName = subscriptionDbName Then  
                registered = True  
            End If  
        Next existing  
        If Not registered Then  
            ' Register the subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown( _  
             subscriberName, subscriptionDbName, _  
             SubscriptionSyncType.Automatic, _  
             TransSubscriberType.ReadOnly)  
        End If  
    Else  
        ' Do something here if the publication does not exist.  
        Throw New ApplicationException(String.Format( _  
         "The publication '{0}' does not exist on {1}.", _  
         publicationName, publisherName))  
    End If  
Catch ex As Exception  
    ' Implement the appropriate error handling here.  
    Throw New ApplicationException(String.Format( _  
        "The subscription to {0} could not be created.", publicationName), ex)  
Finally  
    subscriberConn.Disconnect()  
    publisherConn.Disconnect()  
End Try  
  
```  
  
 다음은 병합 게시에 끌어오기 구독을 만드는 예입니다. 병합 에이전트 작업을 만드는 데 사용되는 Windows 계정 자격 증명은 런타임에 전달됩니다.  
  
```cpp#  
// Define the Publisher, publication, and databases.  
string publicationName = "AdvWorksSalesOrdersMerge";  
string publisherName = publisherInstance;  
string subscriberName = subscriberInstance;  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
string hostname = @"adventure-works\garrett1";  
  
//Create connections to the Publisher and Subscriber.  
ServerConnection subscriberConn = new ServerConnection(subscriberName);  
ServerConnection publisherConn = new ServerConnection(publisherName);  
  
// Create the objects that we need.  
MergePublication publication;  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    subscriberConn.Connect();  
  
    // Ensure that the publication exists and that   
    // it supports pull subscriptions.  
    publication = new MergePublication();  
    publication.Name = publicationName;  
    publication.DatabaseName = publicationDbName;  
    publication.ConnectionContext = publisherConn;  
  
    if (publication.LoadProperties())  
    {  
        if ((publication.Attributes & PublicationAttributes.AllowPull) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowPull;  
        }  
  
        // Define the pull subscription.  
        subscription = new MergePullSubscription();  
        subscription.ConnectionContext = subscriberConn;  
        subscription.PublisherName = publisherName;  
        subscription.PublicationName = publicationName;  
        subscription.PublicationDBName = publicationDbName;  
        subscription.DatabaseName = subscriptionDbName;  
        subscription.HostName = hostname;  
  
        // Specify the Windows login credentials for the Merge Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin;  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword;  
  
        // Make sure that the agent job for the subscription is created.  
        subscription.CreateSyncAgentByDefault = true;  
  
        // Create the pull subscription at the Subscriber.  
        subscription.Create();  
  
        Boolean registered = false;  
  
        // Verify that the subscription is not already registered.  
        foreach (MergeSubscription existing  
            in publication.EnumSubscriptions())  
        {  
            if (existing.SubscriberName == subscriberName  
                && existing.SubscriptionDBName == subscriptionDbName  
                && existing.SubscriptionType == SubscriptionOption.Pull)  
            {  
                registered = true;  
            }  
        }  
        if (!registered)  
        {  
            // Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown(  
                subscriberName, subscriptionDbName,  
                SubscriptionSyncType.Automatic,  
                MergeSubscriberType.Local, 0);  
        }  
    }  
    else  
    {  
        // Do something here if the publication does not exist.  
        throw new ApplicationException(String.Format(  
            "The publication '{0}' does not exist on {1}.",  
            publicationName, publisherName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement the appropriate error handling here.  
    throw new ApplicationException(String.Format(  
        "The subscription to {0} could not be created.", publicationName), ex);  
}  
finally  
{  
    subscriberConn.Disconnect();  
    publisherConn.Disconnect();  
}  
  
```  
  
```vb  
' Define the Publisher, publication, and databases.  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim publisherName As String = publisherInstance  
Dim subscriberName As String = subscriberInstance  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
Dim hostname As String = "adventure-works\garrett1"  
  
'Create connections to the Publisher and Subscriber.  
Dim subscriberConn As ServerConnection = New ServerConnection(subscriberName)  
Dim publisherConn As ServerConnection = New ServerConnection(publisherName)  
  
' Create the objects that we need.  
Dim publication As MergePublication  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    subscriberConn.Connect()  
  
    ' Ensure that the publication exists and that   
    ' it supports pull subscriptions.  
    publication = New MergePublication()  
    publication.Name = publicationName  
    publication.DatabaseName = publicationDbName  
    publication.ConnectionContext = publisherConn  
  
    If publication.LoadProperties() Then  
        If (publication.Attributes And PublicationAttributes.AllowPull) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowPull  
        End If  
  
        ' Define the pull subscription.  
        subscription = New MergePullSubscription()  
        subscription.ConnectionContext = subscriberConn  
        subscription.PublisherName = publisherName  
        subscription.PublicationName = publicationName  
        subscription.PublicationDBName = publicationDbName  
        subscription.DatabaseName = subscriptionDbName  
        subscription.HostName = hostname  
  
        ' Specify the Windows login credentials for the Merge Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword  
  
        ' Make sure that the agent job for the subscription is created.  
        subscription.CreateSyncAgentByDefault = True  
  
        ' Create the pull subscription at the Subscriber.  
        subscription.Create()  
  
        Dim registered As Boolean = False  
  
        ' Verify that the subscription is not already registered.  
        For Each existing As MergeSubscription In _  
        publication.EnumSubscriptions()  
            If existing.SubscriberName = subscriberName Then  
                registered = True  
            End If  
        Next  
        If Not registered Then  
            ' Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown( _  
             subscriberName, subscriptionDbName, _  
             SubscriptionSyncType.Automatic, _  
             MergeSubscriberType.Local, 0)  
        End If  
    Else  
        ' Do something here if the publication does not exist.  
        Throw New ApplicationException(String.Format( _  
         "The publication '{0}' does not exist on {1}.", _  
         publicationName, publisherName))  
    End If  
Catch ex As Exception  
    ' Implement the appropriate error handling here.  
    Throw New ApplicationException(String.Format( _  
        "The subscription to {0} could not be created.", publicationName), ex)  
Finally  
    subscriberConn.Disconnect()  
    publisherConn.Disconnect()  
End Try  
```  
  
 다음은 [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)에서 관련된 에이전트 작업 및 구독 메타데이터를 만들지 않고 병합 게시에 끌어오기 구독을 만드는 예입니다. 병합 에이전트 작업을 만드는 데 사용되는 Windows 계정 자격 증명은 런타임에 전달됩니다.  
  
```csharp  
// Define the Publisher, publication, and databases.  
string publicationName = "AdvWorksSalesOrdersMerge";  
string publisherName = publisherInstance;  
string subscriberName = subscriberInstance;  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
  
//Create connections to the Publisher and Subscriber.  
ServerConnection subscriberConn = new ServerConnection(subscriberName);  
ServerConnection publisherConn = new ServerConnection(publisherName);  
  
// Create the objects that we need.  
MergePublication publication;  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    subscriberConn.Connect();  
  
    // Ensure that the publication exists and that   
    // it supports pull subscriptions.  
    publication = new MergePublication();  
    publication.Name = publicationName;  
    publication.DatabaseName = publicationDbName;  
    publication.ConnectionContext = publisherConn;  
  
    if (publication.LoadProperties())  
    {  
        if ((publication.Attributes & PublicationAttributes.AllowPull) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowPull;  
        }  
  
        // Define the pull subscription.  
        subscription = new MergePullSubscription();  
        subscription.ConnectionContext = subscriberConn;  
        subscription.PublisherName = publisherName;  
        subscription.PublicationName = publicationName;  
        subscription.PublicationDBName = publicationDbName;  
        subscription.DatabaseName = subscriptionDbName;  
  
        // Specify that an agent job not be created for this subscription. The  
        // subscription can only be synchronized by running the Merge Agent directly.  
        // Subscripition metadata stored in MSsubscription_properties will not  
        // be available and must be specified at run time.  
        subscription.CreateSyncAgentByDefault = false;  
  
        // Create the pull subscription at the Subscriber.  
        subscription.Create();  
  
        Boolean registered = false;  
  
        // Verify that the subscription is not already registered.  
        foreach (MergeSubscription existing  
            in publication.EnumSubscriptions())  
        {  
            if (existing.SubscriberName == subscriberName  
                && existing.SubscriptionDBName == subscriptionDbName  
                && existing.SubscriptionType == SubscriptionOption.Pull)  
            {  
                registered = true;  
            }  
        }  
        if (!registered)  
        {  
            // Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown(  
                subscriberName, subscriptionDbName,  
                SubscriptionSyncType.Automatic,  
                MergeSubscriberType.Local, 0);  
        }  
    }  
    else  
    {  
        // Do something here if the publication does not exist.  
        throw new ApplicationException(String.Format(  
            "The publication '{0}' does not exist on {1}.",  
            publicationName, publisherName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement the appropriate error handling here.  
    throw new ApplicationException(String.Format(  
        "The subscription to {0} could not be created.", publicationName), ex);  
}  
finally  
{  
    subscriberConn.Disconnect();  
    publisherConn.Disconnect();  
}  
```  
  
```vb  
' Define the Publisher, publication, and databases.  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim publisherName As String = publisherInstance  
Dim subscriberName As String = subscriberInstance  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
  
'Create connections to the Publisher and Subscriber.  
Dim subscriberConn As ServerConnection = New ServerConnection(subscriberName)  
Dim publisherConn As ServerConnection = New ServerConnection(publisherName)  
  
' Create the objects that we need.  
Dim publication As MergePublication  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    subscriberConn.Connect()  
  
    ' Ensure that the publication exists and that   
    ' it supports pull subscriptions.  
    publication = New MergePublication()  
    publication.Name = publicationName  
    publication.DatabaseName = publicationDbName  
    publication.ConnectionContext = publisherConn  
  
    If publication.LoadProperties() Then  
        If (publication.Attributes And PublicationAttributes.AllowPull) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowPull  
        End If  
  
        ' Define the pull subscription.  
        subscription = New MergePullSubscription()  
        subscription.ConnectionContext = subscriberConn  
        subscription.PublisherName = publisherName  
        subscription.PublicationName = publicationName  
        subscription.PublicationDBName = publicationDbName  
        subscription.DatabaseName = subscriptionDbName  
  
        ' Specify that an agent job not be created for this subscription. The  
        ' subscription can only be synchronized by running the Merge Agent directly.  
        ' Subscripition metadata stored in MSsubscription_properties will not  
        ' be available and must be specified at run time.  
        subscription.CreateSyncAgentByDefault = False  
  
        ' Create the pull subscription at the Subscriber.  
        subscription.Create()  
  
        Dim registered As Boolean = False  
  
        ' Verify that the subscription is not already registered.  
        For Each existing As MergeSubscription In _  
        publication.EnumSubscriptions()  
            If existing.SubscriberName = subscriberName Then  
                registered = True  
            End If  
        Next  
        If Not registered Then  
            ' Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown( _  
             subscriberName, subscriptionDbName, _  
             SubscriptionSyncType.Automatic, _  
             MergeSubscriberType.Local, 0)  
        End If  
    Else  
        ' Do something here if the publication does not exist.  
        Throw New ApplicationException(String.Format( _  
         "The publication '{0}' does not exist on {1}.", _  
         publicationName, publisherName))  
    End If  
Catch ex As Exception  
    ' Implement the appropriate error handling here.  
    Throw New ApplicationException(String.Format( _  
     "The subscription to {0} could not be created.", publicationName), ex)  
Finally  
    subscriberConn.Disconnect()  
    publisherConn.Disconnect()  
End Try  
```  
  
 다음은 웹 동기화를 사용하여 인터넷을 통해 동기화할 수 있는 병합 게시에 끌어오기 구독을 만드는 예입니다. 병합 에이전트 작업을 만드는 데 사용되는 Windows 계정 자격 증명은 런타임에 전달됩니다. 자세한 내용은 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)을 참조하세요.  
  
```csharp  
// Define the Publisher, publication, and databases.  
string publicationName = "AdvWorksSalesOrdersMerge";  
string publisherName = publisherInstance;  
string subscriberName = subscriberInstance;  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
string hostname = @"adventure-works\garrett1";  
string webSyncUrl = "https://" + publisherInstance + "/WebSync/replisapi.dll";  
  
//Create connections to the Publisher and Subscriber.  
ServerConnection subscriberConn = new ServerConnection(subscriberName);  
ServerConnection publisherConn = new ServerConnection(publisherName);  
  
// Create the objects that we need.  
MergePublication publication;  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    subscriberConn.Connect();  
  
    // Ensure that the publication exists and that   
    // it supports pull subscriptions and Web synchronization.  
    publication = new MergePublication();  
    publication.Name = publicationName;  
    publication.DatabaseName = publicationDbName;  
    publication.ConnectionContext = publisherConn;  
  
    if (publication.LoadProperties())  
    {  
        if ((publication.Attributes & PublicationAttributes.AllowPull) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowPull;  
        }  
        if ((publication.Attributes & PublicationAttributes.AllowWebSynchronization) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowWebSynchronization;  
        }  
  
        // Define the pull subscription.  
        subscription = new MergePullSubscription();  
        subscription.ConnectionContext = subscriberConn;  
        subscription.PublisherName = publisherName;  
        subscription.PublicationName = publicationName;  
        subscription.PublicationDBName = publicationDbName;  
        subscription.DatabaseName = subscriptionDbName;  
        subscription.HostName = hostname;  
  
        // Specify the Windows login credentials for the Merge Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin;  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword;  
  
        // Enable Web synchronization.  
        subscription.UseWebSynchronization = true;  
        subscription.InternetUrl = webSyncUrl;  
  
        // Specify the same Windows credentials to use when connecting to the  
        // Web server using HTTPS Basic Authentication.  
        subscription.InternetSecurityMode = AuthenticationMethod.BasicAuthentication;  
        subscription.InternetLogin = winLogin;  
        subscription.InternetPassword = winPassword;  
  
        // Ensure that we create a job for this subscription.  
        subscription.CreateSyncAgentByDefault = true;  
  
        // Create the pull subscription at the Subscriber.  
        subscription.Create();  
  
        Boolean registered = false;  
  
        // Verify that the subscription is not already registered.  
        foreach (MergeSubscription existing  
            in publication.EnumSubscriptions())  
        {  
            if (existing.SubscriberName == subscriberName  
                && existing.SubscriptionDBName == subscriptionDbName  
                && existing.SubscriptionType == SubscriptionOption.Pull)  
            {  
                registered = true;  
            }  
        }  
        if (!registered)  
        {  
            // Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown(  
                subscriberName, subscriptionDbName,  
                SubscriptionSyncType.Automatic,  
                MergeSubscriberType.Local, 0);  
        }  
    }  
    else  
    {  
        // Do something here if the publication does not exist.  
        throw new ApplicationException(String.Format(  
            "The publication '{0}' does not exist on {1}.",  
            publicationName, publisherName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement the appropriate error handling here.  
    throw new ApplicationException(String.Format(  
        "The subscription to {0} could not be created.", publicationName), ex);  
}  
finally  
{  
    subscriberConn.Disconnect();  
    publisherConn.Disconnect();  
}  
```  
  
```vb  
' Define the Publisher, publication, and databases.  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim publisherName As String = publisherInstance  
Dim subscriberName As String = subscriberInstance  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
Dim hostname As String = "adventure-works\garrett1"  
Dim webSyncUrl As String = "https://" + publisherInstance + "/WebSync/replisapi.dll"  
  
'Create connections to the Publisher and Subscriber.  
Dim subscriberConn As ServerConnection = New ServerConnection(subscriberName)  
Dim publisherConn As ServerConnection = New ServerConnection(publisherName)  
  
' Create the objects that we need.  
Dim publication As MergePublication  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    subscriberConn.Connect()  
  
    ' Ensure that the publication exists and that   
    ' it supports pull subscriptions and Web synchronization.  
    publication = New MergePublication()  
    publication.Name = publicationName  
    publication.DatabaseName = publicationDbName  
    publication.ConnectionContext = publisherConn  
  
    If publication.LoadProperties() Then  
        If (publication.Attributes And PublicationAttributes.AllowPull) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowPull  
        End If  
        If (publication.Attributes And PublicationAttributes.AllowWebSynchronization) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowWebSynchronization  
        End If  
  
        ' Define the pull subscription.  
        subscription = New MergePullSubscription()  
        subscription.ConnectionContext = subscriberConn  
        subscription.PublisherName = publisherName  
        subscription.PublicationName = publicationName  
        subscription.PublicationDBName = publicationDbName  
        subscription.DatabaseName = subscriptionDbName  
        subscription.HostName = hostname  
        subscription.CreateSyncAgentByDefault = True  
  
        ' Specify the Windows login credentials for the Merge Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword  
  
        ' Enable Web synchronization.  
        subscription.UseWebSynchronization = True  
        subscription.InternetUrl = webSyncUrl  
  
        ' Specify the same Windows credentials to use when connecting to the  
        ' Web server using HTTPS Basic Authentication.  
        subscription.InternetSecurityMode = AuthenticationMethod.BasicAuthentication  
        subscription.InternetLogin = winLogin  
        subscription.InternetPassword = winPassword  
  
        ' Create the pull subscription at the Subscriber.  
        subscription.Create()  
  
        Dim registered As Boolean = False  
  
        ' Verify that the subscription is not already registered.  
        For Each existing As MergeSubscription In _  
        publication.EnumSubscriptions()  
            If existing.SubscriberName = subscriberName Then  
                registered = True  
            End If  
        Next  
        If Not registered Then  
            ' Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown( _  
             subscriberName, subscriptionDbName, _  
             SubscriptionSyncType.Automatic, _  
             MergeSubscriberType.Local, 0)  
        End If  
    Else  
        ' Do something here if the publication does not exist.  
        Throw New ApplicationException(String.Format( _  
         "The publication '{0}' does not exist on {1}.", _  
         publicationName, publisherName))  
    End If  
Catch ex As Exception  
    ' Implement the appropriate error handling here.  
    Throw New ApplicationException(String.Format( _  
     "The subscription to {0} could not be created.", publicationName), ex)  
Finally  
    subscriberConn.Disconnect()  
    publisherConn.Disconnect()  
End Try  
```  
  
## <a name="see-also"></a>관련 항목:  
 [복제 관리 개체 개념](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [끌어오기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
