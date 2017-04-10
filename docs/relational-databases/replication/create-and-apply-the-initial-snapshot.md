---
title: "초기 스냅숏 만들기 및 적용 | Microsoft Docs"
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
  - "스냅숏 [SQL Server 복제], 만들기"
  - "스냅숏 복제 [SQL Server], 초기 스냅숏"
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 초기 스냅숏 만들기 및 적용
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 초기 스냅숏을 만들고 적용하는 방법에 대해 설명합니다. 매개 변수가 있는 필터를 사용하는 병합 게시에는 두 부분으로 구성된 스냅숏이 필요합니다. 자세한 내용은 [Create a Snapshot for a Merge Publication with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **다음을 사용하여 초기 스냅숏을 만들고 적용하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행 중이면 새 게시 마법사로 게시를 만든 직후 스냅숏 에이전트에서 스냅숏을 생성합니다. 이렇게 생성된 스냅숏은 기본적으로 모든 구독에 대해 배포 에이전트(스냅숏 및 트랜잭션 복제의 경우)나 병합 에이전트(병합 구독의 경우)에 의해 적용됩니다. 스냅숏은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 복제 모니터를 사용하여 생성할 수도 있습니다. 복제 모니터를 시작 하는 방법에 대 한 정보를 참조 하십시오. [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)합니다.  
  
#### Management Studio에서 스냅숏을 만들려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  스냅숏을 만들을 클릭 한 다음 원하는 게시를 마우스 오른쪽 단추로 클릭 **스냅숏 에이전트 상태 보기**합니다.  
  
4.  에 **스냅숏 에이전트 상태 보기-\< 게시>** 대화 상자를 클릭 하 여 **시작**합니다.  
  
 스냅숏 에이전트에서 스냅숏 생성을 마치면 "[100%] 17개 아티클의 스냅숏이 생성되었습니다"라는 메시지가 표시됩니다.  
  
#### 복제 모니터에서 스냅숏을 만들려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장한 다음 게시자를 확장합니다.  
  
2.  스냅숏을 생성 하 고 클릭 한 다음 게시를 마우스 오른쪽 단추로 클릭 **스냅숏 생성**합니다.  
  
3.  스냅숏 에이전트 상태를 보려면 **에이전트** 탭을 클릭합니다. 자세한 내용은 표에서 스냅숏 에이전트를 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **세부 정보 보기**합니다.  
  
#### 스냅숏을 적용하려면  
  
1.  스냅숏이 생성된 후에는 구독을 배포 에이전트나 병합 에이전트와 동기화하여 스냅숏을 적용합니다.  
  
    -   에이전트가 계속 실행되도록 설정된 경우(트랜잭션 복제에 대한 기본값) 스냅숏은 생성된 후 자동으로 적용됩니다.  
  
    -   에이전트가 일정대로 실행되도록 설정된 경우 일정에 따라 다음에 에이전트가 실행될 때 스냅숏이 적용됩니다.  
  
    -   에이전트가 요청 시 실행되도록 설정된 경우 사용자가 다음에 에이전트를 실행할 때 스냅숏이 적용됩니다.  
  
     구독을 동기화 하는 방법에 대 한 자세한 내용은 참조 [밀어넣기 구독을 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md) 및 [끌어오기 구독을 동기화](../../relational-databases/replication/synchronize-a-pull-subscription.md)합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 초기 스냅숏은 스냅숏 에이전트 작업을 만들고 실행하거나 배치 파일에서 스냅숏 에이전트 실행 파일을 실행하여 프로그래밍 방식으로 작성할 수 있습니다. 초기 스냅숏이 생성되면 구독이 처음으로 동기화될 때 구독자로 전송되고 적용됩니다. 명령 프롬프트 또는 배치 파일에서 스냅숏 에이전트를 실행하는 경우 기존 스냅숏이 무효화될 때마다 에이전트를 다시 실행해야 합니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
#### 스냅숏 에이전트 작업을 만들고 실행하여 초기 스냅숏을 생성하려면  
  
1.  스냅숏, 트랜잭션 또는 병합 게시를 만듭니다. 자세한 내용은 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)을 참조하세요.  
  
2.  실행 [sp_addpublication_snapshot (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)합니다. 이때 **@publication** 및 다음 매개 변수를 지정합니다.  
  
    -   **지정 하는 @job_login** 배포자에서 스냅숏 에이전트가 실행 되는 Windows 인증 자격 증명입니다.  
  
    -   **@job_password**, 제공된 된 Windows 자격 증명에 대 한 암호입니다.  
  
    -   (선택 사항) 값이 **0** 에 대 한 **@publisher_security_mode** 게시자에 연결할 때 에이전트가 SQL Server 인증을 사용 하는 경우. 이 경우 SQL Server 인증 로그인 정보에 대 한도 지정 해야 **@publisher_login** 및 **@publisher_password**합니다.  
  
    -   (옵션) 스냅숏 에이전트 작업에 대한 동기화 일정. 자세한 내용은 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)을 참조하세요.  
  
    > [!IMPORTANT]  
    >  모든 매개 변수에 대해 제공 된 값 원격 배포자로 게시자를 구성할 경우 포함 하 여 *job_login* 및 *job_password*, 를 일반 텍스트로 배포자에 보내집니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 참조 [#40; 및 데이터베이스 엔진에 암호화 된 연결 사용 SQL Server 구성 관리자 및 #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)합니다.  
  
3.  아티클을 게시에 추가합니다. 자세한 내용은 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
4.  게시 데이터베이스의 게시자에서 실행 [sp_startpublication_snapshot (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md), 값을 지정 하 **@publication** 1 단계에서 만든 합니다.  
  
#### 스냅숏 에이전트를 실행하여 초기 스냅숏을 생성하려면  
  
1.  스냅숏, 트랜잭션 또는 병합 게시를 만듭니다. 자세한 내용은 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)을 참조하세요.  
  
2.  아티클을 게시에 추가합니다. 자세한 내용은 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
3.  명령 프롬프트에서 또는 배치 파일에서 시작는 [복제 스냅숏 에이전트](../../relational-databases/replication/agents/replication-snapshot-agent.md) 를 실행 하 여 **snapshot.exe**, 다음 명령줄 인수를 지정 합니다.  
  
    -   **-Publication**  
  
    -   **-Publisher**  
  
    -   **-Distributor**  
  
    -   **-PublisherDB**  
  
    -   **-ReplicationType**  
  
     SQL Server 인증을 사용하는 경우 다음 인수도 지정해야 합니다.  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예제에는 트랜잭션 게시를 만들고 새 게시에 대 한 스냅숏 에이전트 작업을 추가 하는 방법을 보여 줍니다 (사용 하 여 **sqlcmd** 스크립팅 변수). 또한 추가한 작업을 시작합니다.  
  
 [!code-sql[HowTo#sp_trangenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_1.sql)]  
  
 스냅숏 에이전트 작업을 추가 하는이 예제는 병합 게시를 만듭니다 (사용 하 여 **sqlcmd** 변수)는 게시에 대 한 합니다. 또한 추가한 작업을 시작합니다.  
  
 [!code-sql[HowTo#sp_mergegenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_2.sql)]  
  
 다음 명령줄 인수는 스냅숏 에이전트를 시작하여 병합 게시에 대한 스냅숏을 생성합니다.  
  
> [!NOTE]  
>  가독성을 높이기 위해 줄 바꿈이 추가되었지만 배치 파일에서 명령은 단일 행으로 작성해야 합니다.  
  
```  
  
REM -- Declare variables  
SET Publisher=%InstanceName%  
SET PublicationDB=AdventureWorks2012   
SET Publication=AdvWorksSalesOrdersMerge   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1  
  
```  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 스냅숏 에이전트는 게시가 만들어진 후 스냅숏을 생성합니다. RMO(복제 관리 개체)를 사용하여 이러한 스냅숏을 프로그래밍 방식으로 생성하고 복제 에이전트 기능에 액세스하도록 관리 코드에 지시할 수 있습니다. 사용하는 개체는 복제 유형에 따라 달라집니다. 스냅숏 에이전트는 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 개체를 사용하여 동기적으로 시작하거나 에이전트 작업을 사용하여 비동기적으로 시작할 수 있습니다. 생성된 초기 스냅숏은 구독이 처음 동기화될 때 구독자로 전송되어 적용됩니다. 기존 스냅숏에 유효한 최신 데이터가 필요하게 될 때마다 에이전트를 다시 실행해야 합니다. 자세한 내용은 참조 [유지 게시](../../relational-databases/replication/publish/maintain-publications.md)합니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 [Windows .NET Framework에서 제공하는](http://go.microsoft.com/fwlink/?LinkId=34733) 암호화 서비스 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 사용합니다.  
  
#### 스냅숏 에이전트 작업을 시작하여 스냅숏 또는 트랜잭션 게시에 대한 초기 스냅숏을 생성하려면(비동기)  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 게시 및 설정에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1 단계에서 만든 연결 합니다.  
  
3.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 나머지 속성을 로드 합니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  하는 경우의 값 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 는 **false**, 호출 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 이 게시에 대 한 스냅숏 에이전트 작업을 만듭니다.  
  
5.  호출의 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 메서드를이 게시에 대 한 스냅숏을 생성 하는 에이전트 작업을 시작 합니다.  
  
6.  (선택 사항) 때의 값 <xref:Microsoft.SqlServer.Replication.TransPublication.SnapshotAvailable%2A> 는 **true**, 스냅숏이 구독자에 게 제공 합니다.  
  
#### 스냅숏 에이전트를 실행하여 스냅숏 또는 트랜잭션 게시에 대한 초기 스냅숏을 생성하려면(동기)  
  
1.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 클래스의 인스턴스를 만들고 다음 필수 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> -게시자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> -게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> -게시의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> -배포자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> -값 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 값 또는 게시자에 연결할 때 Windows 인증을 사용 하 여 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 및에 대 한 값이 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 연결할 때 인증 합니다. Windows 인증을 사용하는 것이 좋습니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> -값 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 값 또는 배포자에 연결할 때 Windows 인증을 사용 하 여 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 및에 대 한 값이 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자에 연결할 때 인증 합니다. Windows 인증을 사용하는 것이 좋습니다.  
  
2.  값을 설정 <xref:Microsoft.SqlServer.Replication.ReplicationType.Transactional> 또는 <xref:Microsoft.SqlServer.Replication.ReplicationType.Snapshot> 에 대 한 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 메서드를 호출합니다.  
  
#### 스냅숏 에이전트 작업을 시작하여 병합 게시에 대한 초기 스냅숏을 생성하려면(비동기)  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 게시 및 설정에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1 단계에서 만든 연결 합니다.  
  
3.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 나머지 속성을 로드 합니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  하는 경우의 값 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 는 **false**, 호출 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 이 게시에 대 한 스냅숏 에이전트 작업을 만듭니다.  
  
5.  호출의 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 메서드를이 게시에 대 한 스냅숏을 생성 하는 에이전트 작업을 시작 합니다.  
  
6.  (선택 사항) 때의 값 <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 는 **true**, 스냅숏이 구독자에 게 제공 합니다.  
  
#### 스냅숏 에이전트를 실행하여 병합 게시에 대한 초기 스냅숏을 생성하려면(동기)  
  
1.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 클래스의 인스턴스를 만들고 다음 필수 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> -게시자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> -게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> -게시의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> -배포자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> -값 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 값 또는 게시자에 연결할 때 Windows 인증을 사용 하 여 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 및에 대 한 값이 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 연결할 때 인증 합니다. Windows 인증을 사용하는 것이 좋습니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> -값 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 값 또는 배포자에 연결할 때 Windows 인증을 사용 하 여 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 및에 대 한 값이 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자에 연결할 때 인증 합니다. Windows 인증을 사용하는 것이 좋습니다.  
  
2.  값을 설정 <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> 에 대 한 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 메서드를 호출합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 이 예에서는 스냅숏 에이전트를 동기적으로 실행하여 트랜잭션 게시에 대한 초기 스냅숏을 생성합니다.  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot)]  
  
 이 예에서는 에이전트 작업을 비동기적으로 시작하여 트랜잭션 게시에 대한 초기 스냅숏을 생성합니다.  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot_withjob)]  
  
## 참고 항목  
 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)   
 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)   
 [밀어넣기 구독 만들기](../../relational-databases/replication/create-a-push-subscription.md)   
 [동기화 일정 지정](../../relational-databases/replication/specify-synchronization-schedules.md)   
 [스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-snapshot.md)   
 [스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [복제 관리 개체 개념](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [복제 시스템 저장 프로시저 개념](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [스크립팅 변수와 함께 sqlcmd 사용](../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)  
  
  