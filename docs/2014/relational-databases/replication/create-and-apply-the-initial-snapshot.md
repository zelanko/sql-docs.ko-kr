---
title: 초기 스냅숏 만들기 및 적용 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], creating
- snapshot replication [SQL Server], initial snapshots
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
caps.latest.revision: 42
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: acb9bfe0b078dae12d4c4db1263f86dcd7700590
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081558"
---
# <a name="create-and-apply-the-initial-snapshot"></a>초기 스냅숏 만들기 및 적용
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 초기 스냅숏을 만들고 적용하는 방법에 대해 설명합니다. 매개 변수가 있는 필터를 사용하는 병합 게시에는 두 부분으로 구성된 스냅숏이 필요합니다. 자세한 내용은 [매개 변수가 있는 필터로 병합 게시에 대한 스냅숏 만들기](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **다음을 사용하여 초기 스냅숏을 만들고 적용하려면**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행 중이면 새 게시 마법사로 게시를 만든 직후 스냅숏 에이전트에서 스냅숏을 생성합니다. 이렇게 생성된 스냅숏은 기본적으로 모든 구독에 대해 배포 에이전트(스냅숏 및 트랜잭션 복제의 경우)나 병합 에이전트(병합 구독의 경우)에 의해 적용됩니다. 스냅숏은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 복제 모니터를 사용하여 생성할 수도 있습니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](monitor/start-the-replication-monitor.md)을 참조하세요.  
  
#### <a name="to-create-a-snapshot-in-management-studio"></a>Management Studio에서 스냅숏을 만들려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  스냅숏을 생성할 게시를 마우스 오른쪽 단추로 클릭한 다음 **스냅숏 에이전트 상태 보기**를 클릭합니다.  
  
4.  **스냅숏 에이전트 상태 보기 - \<게시>** 대화 상자에서 **시작**을 클릭합니다.  
  
 스냅숏 에이전트에서 스냅숏 생성을 마치면 "[100%] 17개 아티클의 스냅숏이 생성되었습니다"라는 메시지가 표시됩니다.  
  
#### <a name="to-create-a-snapshot-in-replication-monitor"></a>복제 모니터에서 스냅숏을 만들려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장한 다음 게시자를 확장합니다.  
  
2.  스냅숏을 생성할 게시를 마우스 오른쪽 단추로 클릭한 다음 **스냅숏 생성**을 클릭합니다.  
  
3.  스냅숏 에이전트 상태를 보려면 **에이전트** 탭을 클릭합니다. 자세한 내용을 보려면 표에서 스냅숏 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다.  
  
#### <a name="to-apply-a-snapshot"></a>스냅숏을 적용하려면  
  
1.  스냅숏이 생성된 후에는 구독을 배포 에이전트나 병합 에이전트와 동기화하여 스냅숏을 적용합니다.  
  
    -   에이전트가 계속 실행되도록 설정된 경우(트랜잭션 복제에 대한 기본값) 스냅숏은 생성된 후 자동으로 적용됩니다.  
  
    -   에이전트가 일정대로 실행되도록 설정된 경우 일정에 따라 다음에 에이전트가 실행될 때 스냅숏이 적용됩니다.  
  
    -   에이전트가 요청 시 실행되도록 설정된 경우 사용자가 다음에 에이전트를 실행할 때 스냅숏이 적용됩니다.  
  
     구독 동기화 방법은 [Synchronize a Push Subscription](synchronize-a-push-subscription.md) 및 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)대화 상자에서 다시 초기화할 구독을 표시합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 초기 스냅숏은 스냅숏 에이전트 작업을 만들고 실행하거나 배치 파일에서 스냅숏 에이전트 실행 파일을 실행하여 프로그래밍 방식으로 작성할 수 있습니다. 초기 스냅숏이 생성되면 구독이 처음으로 동기화될 때 구독자로 전송되고 적용됩니다. 명령 프롬프트 또는 배치 파일에서 스냅숏 에이전트를 실행하는 경우 기존 스냅숏이 무효화될 때마다 에이전트를 다시 실행해야 합니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
#### <a name="to-create-and-run-a-snapshot-agent-job-to-generate-the-initial-snapshot"></a>스냅숏 에이전트 작업을 만들고 실행하여 초기 스냅숏을 생성하려면  
  
1.  스냅숏, 트랜잭션 또는 병합 게시를 만듭니다. 자세한 내용은 [Create a Publication](publish/create-a-publication.md)를 참조하세요.  
  
2.  [sp_addpublication_snapshot&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)을 실행합니다. 이때 **@publication** 및 다음 매개 변수를 지정합니다.  
  
    -   배포자에서 스냅숏 에이전트를 실행하는 Windows 인증 자격 증명을 지정하는 **@job_login**.  
  
    -   제공된 Windows 자격 증명의 암호인 **@job_password**.  
  
    -   (옵션) 게시자에 연결할 때 에이전트가 SQL Server 인증을 사용하면 **@publisher_security_mode** 에 값 **@publisher_security_mode** . 이 경우 **@publisher_login** 및 **@publisher_password**을 참조하세요.  
  
    -   (옵션) 스냅숏 에이전트 작업에 대한 동기화 일정. 자세한 내용은 [Specify Synchronization Schedules](specify-synchronization-schedules.md)을 참조하세요.  
  
    > [!IMPORTANT]  
    >  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
3.  아티클을 게시에 추가합니다. 자세한 내용은 [아티클을 정의](publish/define-an-article.md)을 참조하세요.  
  
4.  게시 데이터베이스의 게시자에서 1단계의 **@publication** 값을 지정하여 [sp_startpublication_snapshot&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql)을 실행합니다.  
  
#### <a name="to-run-the-snapshot-agent-to-generate-the-initial-snapshot"></a>스냅숏 에이전트를 실행하여 초기 스냅숏을 생성하려면  
  
1.  스냅숏, 트랜잭션 또는 병합 게시를 만듭니다. 자세한 내용은 [Create a Publication](publish/create-a-publication.md)를 참조하세요.  
  
2.  아티클을 게시에 추가합니다. 자세한 내용은 [아티클을 정의](publish/define-an-article.md)을 참조하세요.  
  
3.  명령 프롬프트 또는 배치 파일에서 [snapshot.exe](agents/replication-snapshot-agent.md) 를 실행하여 **복제 병합 에이전트**를 시작하고 다음 명령줄 인수를 지정합니다.  
  
    -   **-Publication**  
  
    -   **-Publisher**  
  
    -   **-Distributor**  
  
    -   **-PublisherDB**  
  
    -   **-ReplicationType**  
  
     SQL Server 인증을 사용하는 경우 다음 인수도 지정해야 합니다.  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **@publisher_security_mode**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **@publisher_security_mode**  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예제에서는 트랜잭션 게시를 만들고 **sqlcmd** 스크립팅 변수를 사용하여 새 게시에 대한 스냅숏 에이전트 작업을 추가하는 방법을 보여 줍니다. 또한 추가한 작업을 시작합니다.  
  
 [!code-sql[HowTo#sp_trangenerate_snapshot](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpubinitialsnapshot.sql#sp_trangenerate_snapshot)]  
  
 이 예제에서는 병합 게시를 만들고 **sqlcmd** 변수를 사용하여 게시에 대한 스냅숏 에이전트 작업을 추가합니다. 또한 추가한 작업을 시작합니다.  
  
 [!code-sql[HowTo#sp_mergegenerate_snapshot](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubinitialsnapshot.sql#sp_mergegenerate_snapshot)]  
  
 다음 명령줄 인수는 스냅숏 에이전트를 시작하여 병합 게시에 대한 스냅숏을 생성합니다.  
  
> [!NOTE]  
>  가독성을 높이기 위해 줄 바꿈이 추가되었지만 배치 파일에서 명령은 단일 행으로 작성해야 합니다.  
  
 [!code-sql[HowTo#startmergesnapshot_10](../../snippets/tsql/SQL15/replication/howto/tsql/createmergesnapshot_10.bat)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 스냅숏 에이전트는 게시가 만들어진 후 스냅숏을 생성합니다. RMO(복제 관리 개체)를 사용하여 이러한 스냅숏을 프로그래밍 방식으로 생성하고 복제 에이전트 기능에 액세스하도록 관리 코드에 지시할 수 있습니다. 사용하는 개체는 복제 유형에 따라 달라집니다. 스냅숏 에이전트는 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 개체를 사용하여 동기적으로 시작하거나 에이전트 작업을 사용하여 비동기적으로 시작할 수 있습니다. 생성된 초기 스냅숏은 구독이 처음 동기화될 때 구독자로 전송되어 적용됩니다. 기존 스냅숏에 유효한 최신 데이터가 필요하게 될 때마다 에이전트를 다시 실행해야 합니다. 자세한 내용은 [게시 유지 관리](publish/maintain-publications.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 [Windows .NET Framework에서 제공하는](http://go.microsoft.com/fwlink/?LinkId=34733) 암호화 서비스 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 사용합니다.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>스냅숏 에이전트 작업을 시작하여 스냅숏 또는 트랜잭션 게시에 대한 초기 스냅숏을 생성하려면(비동기)  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체의 나머지 속성을 로드합니다. 이 메서드가 반환 하는 경우 `false`, 2 단계에서 게시 속성이 올바르게 정의 된 또는 게시가 없습니다.  
  
4.  하는 경우의 값 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 은 `false`, 호출 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 이 게시에 대 한 스냅숏 에이전트 작업을 만듭니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 메서드를 호출하여 이 게시에 대한 스냅숏을 생성하는 에이전트 작업을 시작합니다.  
  
6.  (선택 사항) 때의 값 <xref:Microsoft.SqlServer.Replication.TransPublication.SnapshotAvailable%2A> 은 `true`, 스냅숏이 구독자에 사용할 수 있습니다.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-running-the-snapshot-agent-synchronous"></a>스냅숏 에이전트를 실행하여 스냅숏 또는 트랜잭션 게시에 대한 초기 스냅숏을 생성하려면(동기)  
  
1.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 클래스의 인스턴스를 만들고 다음 필수 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - 게시자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - 게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - 게시의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - 배포자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - 게시자에 연결할 때 Windows 인증을 사용하려면 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 값, 게시자에 연결할 때 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 인증을 사용하려면 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> , <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값. Windows 인증을 사용하는 것이 좋습니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - 배포자에 연결할 때 Windows 인증을 사용하려면 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 값, 배포자에 연결할 때 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 인증을 사용하려면 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> , <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값. Windows 인증을 사용하는 것이 좋습니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationType.Transactional> 에 <xref:Microsoft.SqlServer.Replication.ReplicationType.Snapshot> 또는 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>값을 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 메서드를 호출합니다.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>스냅숏 에이전트 작업을 시작하여 병합 게시에 대한 초기 스냅숏을 생성하려면(비동기)  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체의 나머지 속성을 로드합니다. 이 메서드가 반환 하는 경우 `false`, 2 단계에서 게시 속성이 올바르게 정의 된 또는 게시가 없습니다.  
  
4.  하는 경우의 값 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 은 `false`, 호출 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 이 게시에 대 한 스냅숏 에이전트 작업을 만듭니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 메서드를 호출하여 이 게시에 대한 스냅숏을 생성하는 에이전트 작업을 시작합니다.  
  
6.  (선택 사항) 때의 값 <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 은 `true`, 스냅숏이 구독자에 사용할 수 있습니다.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-running-the-snapshot-agent-synchronous"></a>스냅숏 에이전트를 실행하여 병합 게시에 대한 초기 스냅숏을 생성하려면(동기)  
  
1.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 클래스의 인스턴스를 만들고 다음 필수 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - 게시자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - 게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - 게시의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - 배포자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - 게시자에 연결할 때 Windows 인증을 사용하려면 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 값, 게시자에 연결할 때 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 인증을 사용하려면 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> , <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값. Windows 인증을 사용하는 것이 좋습니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - 배포자에 연결할 때 Windows 인증을 사용하려면 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 값, 배포자에 연결할 때 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 인증을 사용하려면 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> , <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값. Windows 인증을 사용하는 것이 좋습니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> 에 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>값을 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 메서드를 호출합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 이 예에서는 스냅숏 에이전트를 동기적으로 실행하여 트랜잭션 게시에 대한 초기 스냅숏을 생성합니다.  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_generatesnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_generatesnapshot)]  
  
 이 예에서는 에이전트 작업을 비동기적으로 시작하여 트랜잭션 게시에 대한 초기 스냅숏을 생성합니다.  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_generatesnapshot_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_generatesnapshot_withjob)]  
  
## <a name="see-also"></a>관련 항목  
 [Create a Publication](publish/create-a-publication.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [ssSDSFull](create-a-push-subscription.md)   
 [Specify Synchronization Schedules](specify-synchronization-schedules.md)   
 [스냅숏 만들기 및 적용](create-and-apply-the-snapshot.md)   
 [스냅숏으로 구독 초기화](initialize-a-subscription-with-a-snapshot.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Replication System Stored Procedures Concepts](concepts/replication-system-stored-procedures-concepts.md)   
 [스크립팅 변수와 함께 sqlcmd 사용](../scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
