---
title: 밀어넣기 구독 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- push subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], push subscriptions
- subscriptions [SQL Server replication], push
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: adfbbc61-58d1-4330-9ad6-b14ab1142e2b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 6eca1e80614772a1aa65faa60351fb73f83ba433
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70059297"
---
# <a name="create-a-push-subscription"></a>밀어넣기 구독 만들기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 밀어넣기 구독을 만드는 방법에 대해 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대해 밀어넣기 구독을 만드는 방법에 대한 자세한 내용은 [SQL Server 이외 구독자에 대한 구독 만들기](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)를 참조하세요.  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
 
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
새 구독 마법사를 사용하여 게시자 또는 구독자에서 밀어넣기 구독을 만듭니다. 마법사의 페이지에 따라 다음을 수행하세요.  
  
- 게시자와 게시를 지정합니다.  
  
- 복제 에이전트가 실행될 위치를 선택합니다. 밀어넣기 구독의 경우 게시 유형에 따라 **배포 에이전트 위치** 페이지 또는 **병합 에이전트 위치** 페이지에서 **배포자 (밀어넣기 구독)에서 모든 에이전트 실행** 을 선택합니다.  
  
- 구독자와 구독 데이터베이스를 지정합니다.  
  
- 복제 에이전트에서 설정한 연결에 사용할 로그인과 암호를 지정합니다.  
  
  - 스냅샷 및 트랜잭션 게시에 대한 구독의 경우 **배포 에이전트 보안** 페이지에서 자격 증명을 지정합니다.  
  
  - 병합 게시에 대한 구독의 경우 **병합 에이전트 보안** 페이지에서 자격 증명을 지정합니다.  
  
    각 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
- 동기화 일정과 구독자의 초기화 시기를 지정합니다.  
  
- 구독 유형 및 매개 변수가 있는 필터링 값 등의 병합 게시에 대한 추가 옵션을 지정합니다.  
  
- 구독 업데이트를 허용하는 트랜잭션 게시에 대한 추가 옵션을 지정합니다. 한 가지 옵션은 구독자가 게시자에서 변경 사항을 즉시 커밋할 지 큐에 써야 할지 결정하는 것입니다. 또 다른 옵션은 구독자에서 게시자로 연결하는 데 사용되는 자격 증명을 설정하는 것입니다.  
  
- 경우에 따라 구독을 스크립팅합니다.  
  
#### <a name="to-create-a-push-subscription-from-the-publisher"></a>게시자에서 밀어넣기 구독을 만들려면  
  
1. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음, 해당 서버 노드를 확장합니다.  
  
2. **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3. 하나 이상의 구독을 만들 게시를 마우스 오른쪽 단추로 클릭한 다음 **새 구독**을 선택합니다.  
  
4. 새 구독 마법사의 페이지를 완료합니다.  
  
#### <a name="to-create-a-push-subscription-from-the-subscriber"></a>구독자에서 밀어넣기 구독을 만들려면  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2. **복제** 폴더를 확장합니다.  
  
3. **로컬 구독** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 구독**을 선택합니다.  
  
4. 새 구독 마법사의 **게시** 페이지에 있는 **게시자** 드롭다운 목록에서 **\<SQL Server 게시자 찾기>** 또는 **\<Oracle 게시자 찾기>** 를 선택합니다.  
  
5. **서버에 연결** 대화 상자에서 게시자에 연결합니다.  
  
6. **게시** 페이지에서 게시를 선택합니다.  
  
7. 새 구독 마법사의 페이지를 완료합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
복제 조정 프로시저를 사용하여 프로그래밍 방식으로 밀어넣기 구독을 만들 수 있습니다. 사용되는 저장 프로시저는 구독이 속한 게시 유형에 따라 달라집니다.  
  
> [!IMPORTANT]
> 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
#### <a name="to-create-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시에 밀어넣기 구독을 만들려면  
  
1. 게시 데이터베이스의 게시자에서 [sp_helppublication](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행하여 게시에서 밀어넣기 구독을 지원하는지 확인합니다.  
  
   - **allow_push** 의 값이 **1**이면 게시에서 밀어넣기 구독을 지원합니다.  
  
   - **allow_push**의 값이 **0**이면 [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)을 실행합니다. **\@속성**에 **allow_push** 및 **\@값**에 **true**를 지정합니다.  
  
2. 게시 데이터베이스의 게시자에서 [sp_addsubscription](../system-stored-procedures/sp-addsubscription-transact-sql.md)을 실행합니다. **\@publication**, **\@subscriber** 및 **\@destination_db**를 지정합니다. **\@subscription_type**의 값을 **push**로 지정합니다. 구독 업데이트 방법은 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기](publish/create-an-updatable-subscription-to-a-transactional-publication.md)를 참조하세요.  
  
3. 게시 데이터베이스의 게시자에서 [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)를 실행합니다. 다음을 지정합니다.  
  
   - **\@subscriber**, **\@subscriber_db** 및 **\@publication** 매개 변수.  
  
   - 배포자의 배포 에이전트가 **\@job_login** 및 **\@job_password**에 대해 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 자격 증명.  
  
     > [!NOTE]
     > Windows 통합 인증을 통해 만든 연결은 항상 **\@job_login** 및 **\@job_password**로 지정한 Windows 자격 증명만 사용합니다. 배포 에이전트는 항상 Windows 통합 인증을 사용하여 배포자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 구독자에 연결합니다.  
  
   - (옵션) **\@subscriber_security_mode**에 대한 **0** 값과 **\@subscriber_login** 및 **\@subscriber_password**에 대한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 정보. 구독자에 연결할 때 SQL Server 인증을 사용해야 하는 경우 이러한 매개 변수를 지정합니다.  
  
   - 이 구독에 대한 배포 에이전트 작업 일정. 자세한 내용은 [동기화 일정 지정](../../relational-databases/replication/specify-synchronization-schedules.md)을 참조하세요.  
  
> [!IMPORTANT]
> 게시자에서 원격 배포자를 사용하여 밀어넣기 구독을 만드는 경우 ‘job_login’ 및 ‘job_password’를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 보내집니다.   이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)를 참조하세요.  
  
#### <a name="to-create-a-push-subscription-to-a-merge-publication"></a>병합 게시에 밀어넣기 구독을 만들려면  
  
1. 게시 데이터베이스의 게시자에서 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)을 실행하여 게시에서 밀어넣기 구독을 지원하는지 확인합니다.  
  
   - **allow_push** 값이 **1**이면 게시에서 밀어넣기 구독을 지원합니다.  
  
   - **allow_push**의 값이 **1**이 아니면 [sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)을 실행합니다. **\@속성**에 **allow_push** 및 **\@값**에 **true**를 지정합니다.  
  
2. 게시 데이터베이스의 게시자에서 [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)을 실행합니다. 다음 매개 변수를 지정합니다.  
  
   - **\@publication**. 게시의 이름입니다.  
  
   - **\@subscriber_type**. 클라이언트 구독의 경우 **로컬**을 지정합니다. 서버 구독의 경우 **글로벌**을 지정합니다.  
  
   - **\@subscription_priority**. 서버 구독에 대해 구독의 우선 순위를 지정합니다(**0.00** ~ **99.99**).  
  
   자세한 내용은 [고급 병합 복제 충돌 감지 및 해결](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)을 참조하세요.  
  
3. 게시 데이터베이스의 게시자에서 [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)를 실행합니다. 다음을 지정합니다.  
  
   - **\@subscriber**, **\@subscriber_db** 및 **\@publication** 매개 변수.  
  
   - **\@job_login** 및 **\@job_password**에 대해 배포자에서 병합 에이전트가 실행되는 Windows 자격 증명.  
  
     > [!NOTE]
     > Windows 통합 인증을 통해 만든 연결은 항상 **\@job_login** 및 **\@job_password**로 지정한 Windows 자격 증명만 사용합니다. 병합 에이전트는 항상 Windows 통합 인증을 사용하여 배포자에 로컬로 연결합니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 구독자에 연결합니다.  
  
   - (옵션) **\@subscriber_security_mode**에 대한 **0** 값과 **\@subscriber_login** 및 **\@subscriber_password**에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로그인 정보. 구독자에 연결할 때 SQL Server 인증을 사용해야 하는 경우 이러한 매개 변수를 지정합니다.  
  
   - (옵션) **\@publisher_security_mode**에 대한 **0** 값과 **\@publisher_login** 및 **\@publisher_password**에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로그인 정보. 구독자에 연결할 때 SQL Server 인증을 사용해야 하는 경우 이러한 값을 지정합니다.  
  
   - 이 구독에 대한 병합 에이전트 작업 일정. 자세한 내용은 [동기화 일정 지정](../../relational-databases/replication/specify-synchronization-schedules.md)을 참조하세요.  
  
> [!IMPORTANT]
> 게시자에서 원격 배포자를 사용하여 밀어넣기 구독을 만드는 경우 ‘job_login’ 및 ‘job_password’를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 보내집니다.   이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)를 참조하세요.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음은 트랜잭션 게시에 밀어넣기 구독을 만드는 예입니다. 로그인 및 암호 값은 **sqlcmd** 스크립팅 변수를 통해 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/create-a-push-subscription_1.sql)]  
  
 다음은 병합 게시에 밀어넣기 구독을 만드는 예입니다. 로그인 및 암호 값은 **sqlcmd** 스크립팅 변수를 통해 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/create-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> 복제 관리 개체 사용  
 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 밀어넣기 구독을 만들 수 있습니다. 밀어넣기 구독을 만들 때 사용하는 RMO 클래스는 구독을 만드는 게시 유형에 따라 달라집니다.  
  
> [!IMPORTANT]
> 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework에서 제공하는 [암호화 서비스](https://go.microsoft.com/fwlink/?LinkId=34733)를 사용합니다.  
  
#### <a name="to-create-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시에 밀어넣기 구독을 만들려면  
  
1. <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2. 1단계에서 만든 게시자 연결을 사용하여 <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>및 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>를 지정합니다.  
  
3. <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 지정한 속성이 올바르지 않거나 서버에 게시가 없는 것입니다.  
  
4. <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 속성과 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> 사이에서 비트 논리 AND(Visual C#의 **&** 및 Visual Basic의 **And**)를 수행합니다. 결과가 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>이면 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 와 **|** 속성과 **Or** 및 Visual Basic의 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 를 지정하고 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>를 참조하세요. 그런 다음 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 를 호출하여 밀어넣기 구독을 설정합니다.  
  
5. 구독 데이터베이스가 없는 경우 <xref:Microsoft.SqlServer.Management.Smo.Database> 클래스를 사용하여 만듭니다. 자세한 내용은 [데이터베이스 생성, 변경 및 제거](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)를 참조하세요.  
  
6. <xref:Microsoft.SqlServer.Replication.TransSubscription> 클래스의 인스턴스를 만듭니다.  
  
7. 다음 구독 속성을 설정합니다.  
  
   - <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 대해 1단계에서 만든 게시자에 대한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>  
  
   - <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>에 대한 구독 데이터베이스 이름  
  
   - <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>에 대한 구독자 이름 
  
   - <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>에 대한 게시 데이터베이스 이름  
  
   - <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>에 대한 게시 이름
  
   - 배포자의 배포 에이전트가 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 를 지정하고 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 필드와 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 필드. 이 계정은 Windows 인증을 사용하여 배포자에 대한 로컬 연결 및 원격 연결을 만드는 데 사용됩니다.  
  
     > [!NOTE]
     > **sysadmin** 고정 서버 역할의 멤버가 구독을 만들 때 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>를 설정할 필요는 없지만 설정해 두는 것이 좋습니다. 이 경우 에이전트는 SQL Server 에이전트 계정을 가장합니다. 자세한 내용은 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
   - (옵션) **@value** 에 <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> 값(기본값). **false**를 지정한 경우 구독은 프로그래밍 방식으로만 동기화할 수 있습니다.  
  
   - (옵션) SQL Server 인증을 사용하여 구독자에 연결할 때 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 의 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드와 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 또는 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 필드  
  
8. <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 메서드를 호출합니다.  
  
> [!IMPORTANT]
> 원격 배포자가 있는 게시자에서 밀어넣기 구독을 만드는 경우 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>를 비롯한 모든 속성에 제공된 값이 일반 텍스트로 배포자에게 보내집니다. <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 메서드를 호출하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)를 참조하세요.  
  
#### <a name="to-create-a-push-subscription-to-a-merge-publication"></a>병합 게시에 밀어넣기 구독을 만들려면  
  
1. <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2. 1단계에서 만든 게시자 연결을 사용하여 <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>및 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>를 지정합니다.  
  
3. <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 지정한 속성이 올바르지 않거나 서버에 게시가 없는 것입니다.  
  
4. <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 속성과 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> 사이에서 비트 논리 AND(Visual C#의 **&** 및 Visual Basic의 **And**)를 수행합니다. 결과가 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>이면 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 와 **|** 속성과 **Or** 및 Visual Basic의 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 를 지정하고 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>를 참조하세요. 그런 다음 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 를 호출하여 밀어넣기 구독을 설정합니다.  
  
5. 구독 데이터베이스가 없는 경우 <xref:Microsoft.SqlServer.Management.Smo.Database> 클래스를 사용하여 만듭니다. 자세한 내용은 [데이터베이스 생성, 변경 및 제거](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)를 참조하세요.  
  
6. <xref:Microsoft.SqlServer.Replication.MergeSubscription> 클래스의 인스턴스를 만듭니다.  
  
7. 다음 구독 속성을 설정합니다.  
  
   - <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 대해 1단계에서 만든 게시자에 대한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>  
  
   - <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>에 대한 구독 데이터베이스 이름  
  
   - <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>에 대한 구독자 이름    
   - <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>에 대한 게시 데이터베이스 이름  
  
   - <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>에 대한 게시 이름    
   - 배포자의 배포 에이전트가 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 를 지정하고 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 필드와 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 필드. 이 계정은 Windows 인증을 통해 배포자에 대한 로컬 연결 및 원격 연결을 만드는 데 사용됩니다.  
  
     > [!NOTE]
     > **sysadmin** 고정 서버 역할의 멤버가 구독을 만들 때 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>를 설정할 필요는 없지만 설정해 두는 것이 좋습니다. 이 경우 에이전트는 SQL Server 에이전트 계정을 가장합니다. 자세한 내용은 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
   - (옵션) **@value** 에 <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> 값(기본값). **false**를 지정한 경우 구독은 프로그래밍 방식으로만 동기화할 수 있습니다.  
  
   - (옵션) SQL Server 인증을 사용하여 구독자에 연결할 때 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 의 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드와 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 또는 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 필드  
  
   - (옵션) SQL Server 인증을 사용하여 게시자에 연결할 때 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 의 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드와 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 또는 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 필드  
  
8. <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 메서드를 호출합니다.  
  
> [!IMPORTANT]  
> 원격 배포자가 있는 게시자에서 밀어넣기 구독을 만드는 경우 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>를 비롯한 모든 속성에 제공된 값이 일반 텍스트로 배포자에게 보내집니다. <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 메서드를 호출하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)를 참조하세요.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 다음은 트랜잭션 게시에 _새 밀어넣기 구독을 만드는 예입니다. 배포 에이전트 작업을 실행하는 데 사용되는 Windows 계정 자격 증명은 런타임에 전달됩니다.  
  
 [!code-cs[HowTo#rmo_CreateTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpushsub)]  
  
 다음은 병합 게시에 새 밀어넣기 구독을 만드는 예입니다. 병합 에이전트 작업을 실행하는 데 사용되는 Windows 계정 자격 증명은 런타임에 전달됩니다.  
  
 [!code-cs[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## <a name="see-also"></a>참고 항목  
 [밀어넣기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)   
 [복제 관리 개체 개념](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [밀어넣기 구독 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)   
 [스크립팅 변수와 함께 sqlcmd 사용](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
