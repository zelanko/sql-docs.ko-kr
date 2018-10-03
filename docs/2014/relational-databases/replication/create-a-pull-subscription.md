---
title: 끌어오기 구독 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 41d1886d-59c9-41fc-9bd6-a59b40e0af6e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18b53eaf464d0d11949e7dccbc5154debca733f0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48206143"
---
# <a name="create-a-pull-subscription"></a>끌어오기 구독 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 끌어오기 구독을 만드는 방법에 대해 설명합니다.  
  
 P2P 복제에 대한 끌어오기 구독 설정은 스크립트를 통해서는 가능하지만 마법사를 통해서는 사용할 수 없습니다.  
  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 구독 마법사를 사용하여 게시자나 구독자에서 끌어오기 구독을 만듭니다. 마법사의 페이지에 따라 다음을 수행하세요.  
  
-   게시자와 게시를 지정합니다.  
  
-   복제 에이전트가 실행될 위치를 선택합니다. 끌어오기 구독의 경우 게시 유형에 따라 **배포 에이전트 위치** 페이지나 **병합 에이전트 위치** 페이지에서 **각 에이전트를 해당 구독자(끌어오기 구독)에서 실행** 을 선택합니다.  
  
-   구독자와 구독 데이터베이스를 지정합니다.  
  
-   복제 에이전트에서 설정한 연결에 사용할 로그인과 암호를 지정합니다.  
  
    -   스냅숏 및 트랜잭션 게시에 대한 구독의 경우 **배포 에이전트 보안** 페이지에서 자격 증명을 지정합니다.  
  
    -   병합 게시에 대한 구독의 경우 **병합 에이전트 보안** 페이지에서 자격 증명을 지정합니다.  
  
     각 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [복제 에이전트 보안 모델](security/replication-agent-security-model.md)를 참조하세요.  
  
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
  
4.  새 구독 마법사의 **게시** 페이지에 있는 **게시자** 드롭다운 목록에서 **\<SQL Server 게시자 찾기>** 또는 **\<Oracle 게시자 찾기>** 를 선택합니다.  
  
5.  **서버에 연결** 대화 상자에서 게시자에 연결합니다.  
  
6.  **게시** 페이지에서 게시를 선택합니다.  
  
7.  새 구독 마법사의 페이지를 완료합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 끌어오기 구독은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 만들 수 있습니다. 사용되는 저장 프로시저는 구독이 속한 게시 유형에 따라 달라집니다.  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 끌어오기 구독을 만들려면  
  
1.  게시자에서 [sp_helppublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)을 실행하여 게시에서 끌어오기 구독을 지원하는지 확인합니다.  
  
    -   결과 집합의 **allow_pull** 값이 **1**이면 게시에서 끌어오기 구독을 지원합니다.  
  
    -   경우 값 **allow_pull** 됩니다 **0**, 실행 [sp_changepublication &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)을 지정 하 고 **allow_pull**에 대 한 **@property** 하 고 `true` 에 대 한 **@value**합니다.  
  
2.  구독자에서 [sp_addpullsubscription&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql)을 실행합니다. 이때 **@publisher** 및 **@publication**에서 사용 가능합니다. 구독 업데이트에 대한 자세한 내용은 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기](publish/create-an-updatable-subscription-to-a-transactional-publication.md)을 참조하세요.  
  
3.  구독자에서 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)를 실행합니다. 다음을 지정합니다.  
  
    -   구독자에서 배포 에이전트가 실행되는 **@publisher**또는 RMO(복제 관리 개체)를 사용하여 **@publisher_db**및 **@publication** 매개 변수  
  
    -   구독자에서 배포 에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] @job_login **@job_login** 을 지정하고 **@job_password**를 참조하세요.  
  
        > [!NOTE]  
        >  Windows 통합 인증을 사용하여 만든 연결은 항상 **@job_login** 을 지정하고 **@job_password**를 참조하세요. 배포 에이전트는 항상 Windows 통합 인증을 사용하여 구독자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 배포자에 연결합니다.  
  
    -   (선택 사항) 값 **0** 에 대 한 **@distributor_security_mode** 하며 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 정보 **@distributor_login** 고 **@distributor_password**사용 하는 경우, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자에 연결할 때 인증 합니다.  
  
    -   이 구독에 대한 배포 에이전트 작업 일정. 자세한 내용은 [Specify Synchronization Schedules](specify-synchronization-schedules.md)을 참조하세요.  
  
4.  게시자에서 [sp_addsubscription&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)을 실행하여 끌어오기 구독을 등록합니다. **@publication**, **@subscriber**및 **@destination_db**를 지정합니다. **@subscription_type**에 **pull** 값을 지정합니다.  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 끌어오기 구독을 만들려면  
  
1.  게시자에서 [sp_helpmergepublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)을 실행하여 게시에서 끌어오기 구독을 지원하는지 확인합니다.  
  
    -   결과 집합의 **allow_pull** 값이 **1**이면 게시에서 끌어오기 구독을 지원합니다.  
  
    -   경우 값 **allow_pull** 됩니다 **0**, 실행 [sp_changemergepublication &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)을 지정 하 고 **allow_pull** 에 대 한 **@property** 하 고 `true` 에 대 한 **@value**합니다.  
  
2.  구독자에서 [sp_addmergepullsubscription&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql)을 실행합니다. **@publisher**, **@publisher_db**, **@publication**과 다음 매개 변수를 지정합니다.  
  
    -   **@subscriber_type** - 클라이언트 구독에 **local** 을 지정하고 서버 구독에 **global** 을 지정합니다.  
  
    -   **@subscription_priority** - 구독의 우선 순위를 지정합니다(**0.00** ~ **99.99**). 이 지정은 서버 구독에만 필요합니다.  
  
         자세한 내용은 [고급 병합 복제 충돌 감지 및 해결](merge/advanced-merge-replication-conflict-detection-and-resolution.md)을 참조하세요.  
  
3.  구독자에서 [sp_addmergepullsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)를 실행합니다. 다음 매개 변수를 지정합니다.  
  
    -   **@publisher**또는 RMO(복제 관리 개체)를 사용하여 **@publisher_db**및 **@publication**를 참조하세요.  
  
    -   **@job_login** 및 **@job_password**에 대해 구독자에서 배포 에이전트가 실행되는 Windows 자격 증명을 지정합니다.  
  
        > [!NOTE]  
        >  Windows 통합 인증을 사용하여 만든 연결은 항상 **@job_login** 및 **@job_password**에서 SQL Server 이외 구독자에 대한 구독을 만드는 방법에 대해 설명합니다. 병합 에이전트는 항상 Windows 통합 인증을 사용하여 구독자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 배포자 및 게시자에 연결합니다.  
  
    -   (옵션) 배포자에 연결할 때 **0** 에 **@distributor_security_mode** 0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] @distributor_login **@distributor_login** 을 지정하고 **@distributor_password**에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 정보 지정  
  
    -   (옵션) 배포자에 연결할 때 **0** 에 **@publisher_security_mode** 0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] @distributor_login **@publisher_login** 을 지정하고 **@publisher_password**에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 정보 지정  
  
    -   이 구독에 대한 병합 에이전트 작업 일정. 자세한 내용은 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기](publish/create-an-updatable-subscription-to-a-transactional-publication.md)을 참조하세요.  
  
4.  게시자에서 [sp_addmergesubscription&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql)을 실행합니다. 이때 **@publication**, **@subscriber**, **@subscriber_db**, **@subscription_type**에 값 **pull**을 지정합니다. 끌어오기 구독이 등록됩니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음은 트랜잭션 게시에 끌어오기 구독을 만드는 예입니다. 구독자에서 첫 번째 일괄 처리가 실행되고 두 번째 일괄 처리는 게시자에서 실행됩니다. 로그인 및 암호 값은 sqlcmd 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpullsub.sql#sp_addtranpullsubscriptionagent)]  
  
 [!code-sql[HowTo#sp_addtranpullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpullsub.sql#sp_addtranpullsubscription)]  
  
 다음은 병합 게시에 끌어오기 구독을 만드는 예입니다. 구독자에서 첫 번째 일괄 처리가 실행되고 두 번째 일괄 처리는 게시자에서 실행됩니다. 로그인 및 암호 값은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsub.sql#sp_addmergepullsubscriptionagent)]  
  
 [!code-sql[HowTo#sp_addmergepullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsub.sql#sp_addmergepullsubscription)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 끌어오기 구독을 만드는 데 사용되는 RMO 클래스는 구독이 속한 게시 유형에 따라 달라집니다.  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 끌어오기 구독을 만들려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 및 게시자 모두에 대한 연결을 만듭니다.  
  
2.  1단계에서 만든 게시자 연결을 사용하여 <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 및 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>를 지정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. 이 메서드가 반환 하는 경우 `false`, 2 단계에서 지정한 속성이 올바르지 않습니다. 또는 게시 서버에 존재 하지 않습니다.  
  
4.  비트 논리 AND를 수행 합니다. (`&` Visual C# 및 `And` Visual Basic의) 간에 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 속성 및 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>합니다. 결과가 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>이면 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>와 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 사이의 비트 논리 OR(Visual C#의 `|` 및 Visual Basic의 `Or`)의 결과에 대해 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>를 설정합니다. 그런 다음 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 를 호출하여 끌어오기 구독을 설정합니다.  
  
5.  구독 데이터베이스가 없는 경우 <xref:Microsoft.SqlServer.Management.Smo.Database> 클래스를 사용하여 만듭니다. 자세한 내용은 [데이터베이스 생성, 변경 및 제거](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)를 참조하세요.  
  
6.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 클래스의 인스턴스를 만듭니다.  
  
7.  다음 구독 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 대해 1단계에서 만든 구독자에 대한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>에 대한 구독 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>에 대한 게시자 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>에 대한 게시 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>에 대한 게시 이름  
  
    -   합니다 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 및 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 또는 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> 의 필드 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> 에 대 한 자격 증명을 제공 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 배포 에이전트가 구독자에서 실행 되는 Windows 계정입니다. 이 계정은 Windows 인증을 사용하여 구독자에 대한 로컬 연결 및 원격 연결을 만드는 데 사용됩니다.  
  
        > [!NOTE]  
        >  `sysadmin` 고정 서버 역할의 멤버가 구독을 만들 때 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>를 설정할 필요는 없지만 설정해 두는 것이 좋습니다. 이 경우 에이전트는 SQL Server 에이전트 계정을 가장합니다. 자세한 내용은 [복제 에이전트 보안 모델](security/replication-agent-security-model.md)을 참조하세요.  
  
    -   (옵션) 구독을 동기화하는 데 사용되는 에이전트 작업을 만드는 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A>에 `true` 값. `false`(기본값)를 지정한 경우 구독을 프로그래밍 방식으로만 동기화할 수 있으므로 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> 속성에서 이 개체에 액세스할 때 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A>의 추가 속성을 지정해야 합니다. 자세한 내용은 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)을 참조하세요.  
  
        > [!NOTE]  
        >  일부 버전의 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조하세요. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다. 값을 지정 하는 경우 `true` Express 구독자에 대 한 에이전트 작업은 만들어지지 않습니다. 그러나 중요한 구독 관련 메타데이터는 구독자에 저장됩니다.  
  
    -   (옵션) SQL Server 인증을 사용하여 배포자에 연결할 때 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 의 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드와 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 또는 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 필드  
  
8.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 메서드를 호출합니다.  
  
9. 2단계에서 만들어진 <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 사용하여 <xref:Microsoft.SqlServer.Replication.TransPublication.MakePullSubscriptionWellKnown%2A> 메서드를 호출한 다음 끌어오기 구독을 게시자로 등록합니다. 이 등록이 이미 존재하는 경우 예외가 발생합니다.  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 끌어오기 구독을 만들려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 및 게시자 모두에 대한 연결을 만듭니다.  
  
2.  1단계에서 만든 게시자 연결을 사용하여 <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>및 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>를 지정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. 이 메서드가 반환 하는 경우 `false`, 2 단계에서 지정한 속성이 올바르지 않습니다. 또는 게시 서버에 존재 하지 않습니다.  
  
4.  비트 논리 AND를 수행 합니다. (`&` Visual C# 및 `And` Visual Basic의) 간에 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 속성 및 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>합니다. 결과가 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>이면 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>와 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 사이의 비트 논리 OR(Visual C#의 `|` 및 Visual Basic의 `Or`)의 결과에 대해 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>를 설정합니다. 그런 다음 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 를 호출하여 끌어오기 구독을 설정합니다.  
  
5.  구독 데이터베이스가 없는 경우 <xref:Microsoft.SqlServer.Management.Smo.Database> 클래스를 사용하여 만듭니다. 자세한 내용은 [데이터베이스 생성, 변경 및 제거](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)를 참조하세요.  
  
6.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 클래스의 인스턴스를 만듭니다.  
  
7.  다음 구독 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 대해 1단계에서 만든 구독자에 대한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>에 대한 구독 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>에 대한 게시자 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>에 대한 게시 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>에 대한 게시 이름  
  
    -   구독자에서 병합 에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정에 대한 자격 증명을 제공하는 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A>의 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 필드와 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> 또는 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> 필드. 이 계정은 Windows 인증을 사용하여 구독자에 대한 로컬 연결 및 원격 연결을 만드는 데 사용됩니다.  
  
        > [!NOTE]  
        >  `sysadmin` 고정 서버 역할의 멤버가 구독을 만들 때 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>를 설정할 필요는 없지만 설정해 두는 것이 좋습니다. 이 경우 에이전트는 SQL Server 에이전트 계정을 가장합니다. 자세한 내용은 [복제 에이전트 보안 모델](security/replication-agent-security-model.md)을 참조하세요.  
  
    -   (옵션) 구독을 동기화하는 데 사용되는 에이전트 작업을 만드는 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A>에 `true` 값. `false`(기본값)를 지정한 경우 구독을 프로그래밍 방식으로만 동기화할 수 있으므로 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> 속성에서 이 개체에 액세스할 때 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A>의 추가 속성을 지정해야 합니다. 자세한 내용은 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)을 참조하세요.  
  
    -   (옵션) SQL Server 인증을 사용하여 배포자에 연결할 때 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 의 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드와 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 또는 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 필드  
  
    -   (옵션) SQL Server 인증을 사용하여 게시자에 연결할 때 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 의 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드와 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 또는 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 필드  
  
8.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 메서드를 호출합니다.  
  
9. 2단계에서 만들어진 <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 사용하여 <xref:Microsoft.SqlServer.Replication.MergePublication.MakePullSubscriptionWellKnown%2A> 메서드를 호출한 다음 끌어오기 구독을 게시자로 등록합니다. 이 등록이 이미 존재하는 경우 예외가 발생합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 다음은 트랜잭션 게시에 끌어오기 구독을 만드는 예입니다. 배포 에이전트 작업을 만드는 데 사용되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정 자격 증명은 런타임에 전달됩니다.  
  
 [!code-csharp[HowTo#rmo_CreateTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpullsub)]  
  
 다음은 병합 게시에 끌어오기 구독을 만드는 예입니다. 병합 에이전트 작업을 만드는 데 사용되는 Windows 계정 자격 증명은 런타임에 전달됩니다.  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub)]  
  
 다음은 [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql)에서 관련된 에이전트 작업 및 구독 메타데이터를 만들지 않고 병합 게시에 끌어오기 구독을 만드는 예입니다. 병합 에이전트 작업을 만드는 데 사용되는 Windows 계정 자격 증명은 런타임에 전달됩니다.  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub_NoJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub_nojob)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub_NoJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub_nojob)]  
  
 다음은 웹 동기화를 사용하여 인터넷을 통해 동기화할 수 있는 병합 게시에 끌어오기 구독을 만드는 예입니다. 병합 에이전트 작업을 만드는 데 사용되는 Windows 계정 자격 증명은 런타임에 전달됩니다. 자세한 내용은 [Configure Web Synchronization](configure-web-synchronization.md)을 참조하세요.  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub_WebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub_websync)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub_WebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub_websync)]  
  
## <a name="see-also"></a>참고 항목  
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [끌어오기 구독 속성 보기 및 수정](view-and-modify-pull-subscription-properties.md)   
 [Configure Web Synchronization](configure-web-synchronization.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [복제 보안을 위한 최선의 구현 방법](security/replication-security-best-practices.md)  
  
  
