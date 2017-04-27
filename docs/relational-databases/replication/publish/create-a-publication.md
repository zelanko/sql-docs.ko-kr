---
title: "게시 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publications [SQL Server replication], creating
- articles [SQL Server replication], defining
- adding articles
- articles [SQL Server replication], adding
ms.assetid: 52ee6de9-1d58-4cb9-8711-372bddbe7154
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a5f9fb102add84a33b08c439cd27cab29c210939
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-publication"></a>게시 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 게시를 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **게시를 만들고 아티클을 정의하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   게시 및 아티클 이름에는 %, \*, [, ], |, :, ", ? 등의 문자를 포함할 수 없습니다. , ' , \ , / , < , >. 이러한 문자를 포함하는 데이터베이스 개체를 복제하려면 마법사의 **아티클** 페이지에서 사용할 수 있는 **아티클 속성 - \<아티클>** 대화 상자에서 개체 이름과 다른 아티클 이름을 지정해야 합니다.  
  
###  <a name="Security"></a> 보안  
 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 [Windows .NET Framework에서 제공하는](http://go.microsoft.com/fwlink/?LinkId=34733) 암호화 서비스 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 를 사용합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사를 사용하여 게시를 만들고 아티클을 정의할 수 있습니다. 게시를 만든 후 **게시 속성 - \<게시>** 대화 상자에서 게시 속성을 보고 수정합니다. Oracle 데이터베이스에서 게시를 만드는 방법에 대한 자세한 내용은 [Oracle 데이터베이스에서 게시 만들기](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)를 참조하세요.  
  
#### <a name="to-create-a-publication-and-define-articles"></a>게시를 만들고 아티클을 정의하려면  
  
1.  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **새 게시**를 클릭합니다.  
  
4.  새 게시 마법사의 페이지에 따라 다음을 수행하세요.  
  
    -   서버에 배포가 구성되어 있지 않은 경우 배포자를 지정합니다. 배포 구성에 대한 자세한 내용은 [게시 및 배포 구성](../../../relational-databases/replication/configure-publishing-and-distribution.md)을 참조하세요.  
  
         **배포자** 페이지에서 게시자 서버가 자신의 고유 배포자(로컬 배포자) 역할을 하는 것으로 지정했지만 서버가 배포자로 구성되어 있지 않은 경우 새 게시 마법사가 서버를 구성합니다. **스냅숏 폴더** 페이지에서 배포자에 대해 기본 스냅숏 폴더를 지정하게 됩니다. 스냅숏 폴더는 공유하도록 지정된 디렉터리일 뿐이며 이 폴더에 읽기/쓰기 작업을 수행하려면 에이전트에게 충분한 액세스 권한이 있어야 합니다. 폴더의 적절한 보안 유지 방법에 대한 자세한 내용은 [스냅숏 폴더 보안 설정](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)을 참조하세요.  
  
         다른 서버가 배포자의 역할을 하도록 지정한 경우 게시자에서 배포자로 연결할 때 사용할 암호를 **관리 암호** 페이지에 입력해야 합니다. 이 암호는 원격 배포자에서 게시자를 설정할 때 지정한 암호와 일치해야 합니다.  
  
         자세한 내용은 [Configure Distribution](../../../relational-databases/replication/configure-distribution.md)를 참조하세요.  
  
    -   게시 데이터베이스를 선택합니다.  
  
    -   보고서 유형을 선택합니다. 자세한 내용은 [복제 유형](../../../relational-databases/replication/types-of-replication.md)을 참조하세요.  
  
    -   게시할 데이터와 데이터베이스 개체를 지정합니다. 필요에 따라 테이블 아티클에서 열을 필터링하고 아티클 속성을 설정합니다.  
  
    -   필요에 따라 테이블 아티클에서 행을 필터링합니다. 자세한 내용은 [게시된 데이터 필터링](../../../relational-databases/replication/publish/filter-published-data.md)을 참조하세요.  
  
    -   스냅숏 에이전트 일정을 설정합니다.  
  
    -   다음 복제 에이전트를 실행 및 연결하는 자격 증명을 지정합니다.  
  
         모든 게시에 대한 \- 스냅숏 에이전트  
  
         모든 트랜잭션 게시에 대한 \- 로그 판독기 에이전트  
  
         \- 구독 업데이트를 허용하는 트랜잭션 게시에 대한 큐 판독기 에이전트  
  
         자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) 및 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)를 참조하세요.  
  
    -   필요에 따라 게시를 스크립팅합니다. 자세한 내용은 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)을 참조하세요.  
  
    -   게시의 이름을 지정합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 게시를 만들 수 있습니다. 사용되는 저장 프로시저는 만들려는 게시의 유형에 따라 달라집니다.  
  
#### <a name="to-create-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시를 만들려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_replicationdboption&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)을 실행하여 스냅숏 또는 트랜잭션 복제를 사용하여 현재 데이터베이스를 게시할 수 있도록 설정합니다.  
  
2.  트랜잭션 게시의 경우 게시 데이터베이스에 대한 로그 판독기 에이전트 작업이 존재하는지 여부를 확인합니다. 스냅숏 게시의 경우에는 이 단계가 필요하지 않습니다.  
  
    -   게시 데이터베이스에 대한 로그 판독기 에이전트 작업이 존재하면 3단계를 실행합니다.  
  
    -   게시된 데이터베이스에 대해 로그 판독기 에이전트 작업이 존재하는지 확실하지 않으면 게시 데이터베이스의 게시자에서 [sp_helplogreader_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)를 실행합니다.  
  
    -   결과 집합이 비어 있으면 로그 판독기 에이전트 작업을 만듭니다. 게시자에서 [sp_addlogreader_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)를 실행합니다. **@job_name** 및 **@password**에 에이전트가 실행되는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 자격 증명을 지정합니다. 게시자에 연결할 때 에이전트가 SQL Server 인증을 사용하면 **@publisher_security_mode** 에 값 **@publisher_security_mode** 을 지정하고 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 **@publisher_login** @password **@publisher_password**에서 트랜잭션 게시에 대해 구독 업데이트를 설정하는 방법에 대해 설명합니다. 3단계로 진행합니다.  
  
3.  게시자에서 [sp_addpublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)을 실행합니다. **@publication**에 게시 이름을 지정하고 **@repl_freq** 매개 변수에 **snapshot** 값(스냅숏 게시의 경우) 또는 **continuous** 값(트랜잭션 게시의 경우)을 지정합니다. 다른 게시 옵션을 지정합니다. 이렇게 하면 게시가 정의됩니다.  
  
    > [!NOTE]  
    >  게시 이름은 다음과 같은 문자를 포함할 수 없습니다:  
    >   
    >  % * [ ] | : " ? \ / < >  
  
4.  게시자에서 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)을 실행합니다. **@publication**에 3단계에서 사용된 게시 이름을, **@snapshot_job_name** 및 **@password**에 스냅숏 에이전트를 실행하는 데 사용되는 Windows 자격 증명을 지정합니다. 게시자에 연결할 때 에이전트가 SQL Server 인증을 사용하면 **@publisher_security_mode** 에 값 **@publisher_security_mode** 을 지정하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 **@publisher_login** @password **@publisher_password**에서 트랜잭션 게시에 대해 구독 업데이트를 설정하는 방법에 대해 설명합니다. 이렇게 하면 게시에 대해 스냅숏 에이전트 작업이 만들어집니다.  
  
    > [!IMPORTANT]  
    >  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
5.  아티클을 게시에 추가합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
6.  스냅숏 에이전트 작업을 시작하여 이 게시에 대한 초기 스냅숏을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
#### <a name="to-create-a-merge-publication"></a>병합 게시를 만들려면  
  
1.  게시자에서 [sp_replicationdboption&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)을 실행하여 병합 복제를 통해 현재 데이터베이스를 게시할 수 있도록 설정합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_addmergepublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)을 실행합니다. **@publication**에 게시 이름을 지정하고 기타 게시 옵션을 지정합니다. 이렇게 하면 게시가 정의됩니다.  
  
    > [!NOTE]  
    >  게시 이름은 다음과 같은 문자를 포함할 수 없습니다:  
    >   
    >  % * [ ] | : " ? \ / < >  
  
3.  게시자에서 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)을 실행합니다. **@publication**에 2단계에서 사용된 게시 이름을, **@snapshot_job_name** 및 **@password**에 스냅숏 에이전트를 실행하는 데 사용되는 Windows 자격 증명을 지정합니다. 게시자에 연결할 때 에이전트가 SQL Server 인증을 사용하면 **@publisher_security_mode** 에 값 **@publisher_security_mode** 을 지정하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 **@publisher_login** @password **@publisher_password**에서 트랜잭션 게시에 대해 구독 업데이트를 설정하는 방법에 대해 설명합니다. 이렇게 하면 게시에 대해 스냅숏 에이전트 작업이 만들어집니다.  
  
    > [!IMPORTANT]  
    >  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
4.  아티클을 게시에 추가합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
5.  스냅숏 에이전트 작업을 시작하여 이 게시에 대한 초기 스냅숏을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 트랜잭션 게시를 만듭니다. 스크립팅 변수는 스냅숏 에이전트 및 로그 판독기 에이전트에 대한 작업을 만드는 데 필요한 Windows 자격 증명을 전달하는 데 사용됩니다.  
  
 [!code-sql[HowTo#sp_AddTranPub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_1.sql)]  
  
 다음 예에서는 병합 게시를 만듭니다. 스크립팅 변수는 스냅숏 에이전트에 대한 작업을 만드는 데 필요한 Windows 자격 증명을 전달하는 데 사용됩니다.  
  
 [!code-sql[HowTo#sp_AddMergePub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 게시를 만들 수 있습니다. 게시를 만드는 데 사용하는 RMO 클래스는 만드는 게시 유형에 따라 달라집니다.  
  
#### <a name="to-create-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시를 만들려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  게시 데이터베이스에 대한 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 클래스의 인스턴스를 만들고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 인스턴스로 설정한 다음 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>에서 **false**가 반환되면 데이터베이스가 있는지 확인합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> 속성이 **false**이면 **true**로 설정합니다.  
  
4.  트랜잭션 게시에 대한 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentExists%2A> 속성의 값을 확인합니다. 이 속성이 **true**이면 이 데이터베이스에 대한 로그 판독기 에이전트 작업이 이미 존재하는 것입니다. 이 속성이 **false**이면 다음을 수행합니다.  
  
    -   로그 판독기 에이전트를 실행하는 데 사용되는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 계정에 대한 자격 증명을 제공하기 위한 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A>의 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 및 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 필드를 설정합니다.  
  
        > [!NOTE]  
        >  **sysadmin** 고정 서버 역할의 멤버가 게시를 만들 때는 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A>를 설정하지 않아도 됩니다. 이 경우 에이전트는 SQL Server 에이전트 계정을 가장합니다. 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
    -   (선택 사항) SQL Server 인증을 사용하여 게시자에 연결할 경우 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentPublisherSecurity%2A>의 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 또는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 필드와 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 필드를 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.CreateLogReaderAgent%2A> 메서드를 호출하여 데이터베이스에 대한 로그 판독기 에이전트 작업을 만듭니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 만들고 이 개체에 대해 다음 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>에 대한 1단계의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>에 대한 게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>에 대한 게시의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationType.Transactional> 또는 <xref:Microsoft.SqlServer.Replication.PublicationType.Snapshot>의 <xref:Microsoft.SqlServer.Replication.PublicationType>  
  
    -   스냅숏 에이전트를 실행하는 데 사용되는 Windows 계정에 대한 자격 증명을 제공하기 위한 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>의 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 및 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 필드 이 계정은 스냅숏 에이전트에서 로컬 배포자에 연결할 때 사용되며, Windows 인증이 사용되는 경우에는 모든 원격 연결에도 사용됩니다.  
  
        > [!NOTE]  
        >  **sysadmin** 고정 서버 역할의 멤버가 게시를 만들 때는 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>를 설정하지 않아도 됩니다. 이 경우 에이전트는 SQL Server 에이전트 계정을 가장합니다. 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
    -   (선택 사항) SQL Server 인증을 사용하여 게시자에 연결할 경우 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentPublisherSecurity%2A>의 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 또는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 필드와 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 필드  
  
    -   (선택 사항) 포함 논리 OR 연산자(Visual C#에서는 **|**, Visual Basic에서는 **Or**) 및 배타적 논리 OR 연산자(Visual C#에서는 **^**, Visual Basic에서는 **Xor**)를 사용하여 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 속성에 대한 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 값을 설정합니다.  
  
    -   (선택 사항) SQL Server 이외 게시자인 경우 <xref:Microsoft.SqlServer.Replication.TransPublication.PublisherName%2A>에 대한 게시자의 이름  
  
6.  <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 메서드를 호출하여 게시를 만듭니다.  
  
    > [!IMPORTANT]  
    >  원격 배포자로 게시자를 구성할 경우 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>를 포함하여 모든 속성에 제공된 값이 일반 텍스트로 배포자에게 보내집니다. 이 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 메서드를 호출하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
7.  <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 메서드를 호출하여 게시에 대한 스냅숏 에이전트 작업을 만듭니다.  
  
#### <a name="to-create-a-merge-publication"></a>병합 게시를 만들려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  게시 데이터베이스에 대한 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 클래스의 인스턴스를 만들고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 인스턴스로 설정한 다음 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>에서 **false**가 반환되면 데이터베이스가 있는지 확인합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 속성이 **false**이면 **true**로 설정한 후 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>를 호출합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만들고 이 개체에 대해 다음 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>에 대한 1단계의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>에 대한 게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>에 대한 게시의 이름  
  
    -   스냅숏 에이전트를 실행하는 데 사용되는 Windows 계정에 대한 자격 증명을 제공하기 위한 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>의 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 및 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 필드 이 계정은 스냅숏 에이전트에서 로컬 배포자에 연결할 때 사용되며, Windows 인증이 사용되는 경우에는 모든 원격 연결에도 사용됩니다.  
  
        > [!NOTE]  
        >  **sysadmin** 고정 서버 역할의 멤버가 게시를 만들 때는 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>를 설정하지 않아도 됩니다. 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
    -   (선택 사항) 포함 논리 OR 연산자(Visual C#에서는 **|**, Visual Basic에서는 **Or**) 및 배타적 논리 OR 연산자(Visual C#에서는 **^**, Visual Basic에서는 **Xor**)를 사용하여 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 속성에 대한 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 값을 설정합니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 메서드를 호출하여 게시를 만듭니다.  
  
    > [!IMPORTANT]  
    >  원격 배포자로 게시자를 구성할 경우 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>를 포함하여 모든 속성에 제공된 값이 일반 텍스트로 배포자에게 보내집니다. 이 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 메서드를 호출하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
6.  <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 메서드를 호출하여 게시에 대한 스냅숏 에이전트 작업을 만듭니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 이 예에서는 AdventureWorks 데이터베이스에서 트랜잭션 게시를 사용할 수 있도록 설정하고 로그 판독기 에이전트 작업을 정의하며 AdvWorksProductTran 게시를 만듭니다. 이 게시에 대한 아티클을 정의해야 합니다. 로그 판독기 에이전트 작업 및 스냅숏 에이전트 작업을 만드는 데 필요한 Windows 계정 자격 증명은 런타임에 전달됩니다. RMO를 사용하여 스냅숏 및 트랜잭션 아티클을 정의하는 방법은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)를 참조하세요.  
  
 [!code-cs[HowTo#rmo_CreateTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpub)]  
  
 이 예에서는 AdventureWorks 데이터베이스에서 병합 게시를 사용할 수 있도록 설정하고 AdvWorksSalesOrdersMerge 게시를 만듭니다. 이 게시에 대한 아티클을 정의해야 합니다. 스냅숏 에이전트 작업을 만드는 데 필요한 Windows 계정 자격 증명은 런타임에 전달됩니다. RMO를 사용하여 병합 아티클을 정의하는 방법은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)를 참조하세요.  
  
 [!code-cs[HowTo#rmo_CreateMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 변수와 함께 sqlcmd 사용](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)   
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replication Management Objects Concepts](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [배포 구성](../../../relational-databases/replication/configure-distribution.md)   
 [배포자 보안 설정](../../../relational-databases/replication/security/secure-the-distributor.md)   
 [게시자 보안 설정](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  

