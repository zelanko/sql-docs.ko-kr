---
title: 초기 스냅샷 만들기 및 적용 | Microsoft 문서
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], creating
- snapshot replication [SQL Server], initial snapshots
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 11628e5b490c30ef64329f6b9d06aee1b6c10fa9
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908287"
---
# <a name="create-and-apply-the-initial-snapshot"></a>Create and Apply the Initial Snapshot
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 초기 스냅샷을 만들고 적용하는 방법에 대해 설명합니다. 매개 변수가 있는 필터를 사용하는 병합 게시에는 두 부분으로 구성된 스냅샷이 필요합니다. 자세한 내용은 [매개 변수가 있는 필터로 병합 게시에 대한 스냅샷 만들기](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을 참조하세요.  
  스냅샷은 복제가 생성된 후 스냅샷 에이전트에서 생성됩니다. 생성 방법은 다음과 같습니다.  
  
-   즉시. 기본적으로 병합 게시의 스냅샷은 새 게시 마법사에서 게시가 생성된 후 즉시 생성됩니다.    
-   예약된 시간. 새 게시 마법사의 **스냅샷 에이전트** 페이지에서 또는 저장 프로시저나 RMO(복제 관리 개체) 사용 시 일정을 지정합니다.    
-   수동. 명령 프롬프트 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 스냅샷 에이전트를 실행합니다. 에이전트 실행에 대한 자세한 내용은 [복제 에이전트 실행 파일 개념](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) 및 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)를 참조하세요.  
  
병합 복제의 경우 스냅샷 에이전트가 실행될 때마다 스냅샷이 생성됩니다. 트랜잭션 복제의 경우 게시 속성 **immediate_sync**의 설정에 따라 스냅샷 생성이 달라집니다. 이 속성을 TRUE(새 게시 마법사 사용 시 기본 설정)로 설정하면 스냅샷 에이전트가 실행될 때마다 스냅샷이 생성되고 언제든지 스냅샷을 구독자에 적용할 수 있습니다. 이 속성을 FALSE( **sp_addpublication**사용 시 기본 설정)로 설정하면 스냅샷 에이전트가 마지막으로 실행된 후에 새 구독이 추가된 경우에만 스냅샷이 생성됩니다. 구독자는 동기화하기 위해 스냅샷 에이전트가 완료될 때까지 기다려야 합니다.  
  
기본적으로 스냅샷이 생성되면 그 스냅샷은 배포자에 위치한 기본 스냅샷 폴더에 저장됩니다. 이동식 디스크나 CD-ROM과 같은 이동식 미디어 또는 기본 스냅샷 폴더 이외의 위치에 스냅샷 파일을 저장할 수도 있습니다. 또한 저장과 전송이 간단하도록 파일을 압축할 수 있고 스냅샷이 구독자에 적용되기 전 또는 적용된 후 스크립트를 실행할 수 있습니다. 이러한 옵션에 대한 자세한 내용은 [Snapshot Options](../../relational-databases/replication/snapshot-options.md)를 참조하세요.  
  
스냅샷이 매개 변수가 있는 필터를 사용하는 병합 게시용인 경우 2단계 프로세스를 통해 스냅샷이 생성됩니다. 먼저 게시된 개체의 데이터를 제외하고 복제 스크립트와 스키마를 포함하는 스키마 스냅샷이 생성됩니다. 그런 후 스키마 스냅샷에서 복사된 스크립트 및 스키마를 포함하는 스냅샷과 구독의 파티션에 속해 있는 데이터를 사용하여 구독이 초기화됩니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을(를) 참조하세요.  
  
스냅샷이 게시자에 생성된 다음 기본 또는 대체 스냅샷 위치에 저장되면 스냅샷을 구독자로 전송하고 적용할 수 있습니다. 스냅샷이나 트랜잭션 복제에 대한 배포 에이전트 또는 병합 복제에 대한 병합 에이전트에서는 스냅샷을 전송하고 초기 동기화 중에 스키마 및 데이터 파일을 구독자의 구독 데이터베이스에 적용합니다. 새 구독 마법사를 사용할 경우 초기 동기화는 기본적으로 구독이 생성되는 즉시 발생합니다. 이 동작은 마법사의 **구독 초기화** 페이지에 있는 **초기화 시기** 옵션에서 제어할 수 있습니다. 구독을 초기화한 후 스냅샷이 생성되면 구독을 다시 초기화로 표시해야만 구독자에 적용됩니다. 자세한 내용은 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)를 참조하세요.  
  
배포 에이전트 또는 병합 에이전트에서 초기 스냅샷을 적용한 후 에이전트에서는 후속 업데이트 및 다른 데이터의 수정 사항을 전파합니다. 스냅샷을 구독자로 배포 및 적용한 경우 초기 스냅샷 또는 새 스냅샷을 기다리는 구독자만 영향을 받습니다. 해당 게시에 대한 다른 구독자(게시된 데이터에 대한 삽입, 업데이트, 삭제, 기타 수정 사항을 이미 받은 구독자)는 영향을 받지 않습니다.  

기본 스냅샷 폴더 위치를 보거나 수정하려면 다음을 참조하십시오.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [스냅샷 옵션 수정](../../relational-databases/replication/snapshot-options.md)  
  
-   복제 프로그래밍 및 RMO 프로그래밍: [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)  

## <a name="default-snapshot-location"></a>기본 스냅샷 위치

 배포 구성 마법사의 **스냅샷 폴더** 페이지에서 기본 스냅샷 위치를 지정합니다. 이 마법사 사용에 대한 자세한 내용은 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)을 참조하세요. 배포자로 구성되어 있지 않은 서버에서 게시를 만드는 경우 새 게시 마법사의 **스냅샷 폴더** 페이지에서 기본 스냅샷 위치를 지정합니다. 이 마법사를 사용하는 방법에 대한 자세한 내용은 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
 **배포자 속성 - \<Distributor&gt;** 대화 상자의 **게시자** 페이지에서 기본 스냅샷 위치를 수정합니다. 자세한 내용은 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요. **게시 속성 - \<게시&gt;** 대화 상자에서 각 게시에 대한 스냅샷 폴더를 설정합니다. 자세한 내용은 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
### <a name="modify-the-default-snapshot-location"></a>기본 스냅샷 위치 수정  
  
1.  **배포자 속성 - \<Distributor&gt;** 대화 상자의 **게시자** 페이지에서 기본 스냅샷 위치를 변경하려는 게시자의 속성 단추( **...** )를 클릭합니다.  
  
2.  **게시자 속성 - \<Publisher&gt;** 대화 상자에서 **기본 스냅샷 폴더** 속성에 대한 값을 입력합니다.  
  
    > [!NOTE]  
    >  스냅샷 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\computername\snapshot과 같이 UNC(범용 명명 규칙) 경로로 지정해야 합니다. 자세한 내용은 [스냅샷 폴더 보안 설정](../../relational-databases/replication/security/secure-the-snapshot-folder.md)을 참조하세요.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="create-snapshot"></a>스냅샷 만들기
기본적으로 SQL Server 에이전트가 실행 중이면 새 게시 마법사로 게시를 만든 직후 스냅샷 에이전트에서 스냅샷을 생성합니다. 이렇게 생성된 스냅샷은 기본적으로 모든 구독에 대해 배포 에이전트(스냅샷 및 트랜잭션 복제의 경우)나 병합 에이전트(병합 구독의 경우)에 의해 적용됩니다. 스냅샷은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 복제 모니터를 사용하여 생성할 수도 있습니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  

### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio 사용

1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.    
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.    
3.  스냅샷을 생성할 게시를 마우스 오른쪽 단추로 클릭한 다음 **스냅샷 에이전트 상태 보기**를 클릭합니다.    
4.  **스냅샷 에이전트 상태 보기 - \<게시&gt;** 대화 상자에서 **시작**을 클릭합니다.    
 스냅샷 에이전트에서 스냅샷 생성을 마치면 "[100%] 17개 아티클의 스냅샷이 생성되었습니다"라는 메시지가 표시됩니다.  
  
### <a name="in-replication-monitor"></a>복제 모니터에서  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장한 다음 게시자를 확장합니다.    
2.  스냅샷을 생성할 게시를 마우스 오른쪽 단추로 클릭한 다음 **스냅샷 생성**을 클릭합니다.    
3.  스냅샷 에이전트 상태를 보려면 **에이전트** 탭을 클릭합니다. 자세한 내용을 보려면 표에서 스냅샷 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다.  

## <a name="using-transact-sql"></a>Transact-SQL 사용
초기 스냅샷은 스냅샷 에이전트 작업을 만들고 실행하거나 배치 파일에서 스냅샷 에이전트 실행 파일을 실행하여 프로그래밍 방식으로 작성할 수 있습니다. 초기 스냅샷이 생성되면 구독이 처음으로 동기화될 때 구독자로 전송되고 적용됩니다. 명령 프롬프트 또는 배치 파일에서 스냅샷 에이전트를 실행하는 경우 기존 스냅샷이 무효화될 때마다 에이전트를 다시 실행해야 합니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  

1.  스냅샷, 트랜잭션 또는 병합 게시를 만듭니다. 자세한 내용은 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
2.  [sp_addpublication_snapshot&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)을 실행합니다. **\@publication** 및 다음 매개 변수를 지정합니다.  
  
    -   **\@job_login** - 배포자에서 스냅샷 에이전트를 실행하는 Windows 인증 자격 증명 지정  
  
    -   **\@job_password** - 제공된 Windows 자격 증명의 암호  
  
    -   (옵션) 게시자에 연결할 때 에이전트가 SQL Server 인증을 사용하면 **\@publisher_security_mode**에 값 **0** . 이 경우 **\@publisher_login** 및 **\@publisher_password**에 SQL Server 인증 로그인 정보도 지정해야 합니다.  
  
    -   (옵션) 스냅샷 에이전트 작업에 대한 동기화 일정. 자세한 내용은 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)을 참조하세요.  
  
    > [!IMPORTANT]  
    >  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
3.  아티클을 게시에 추가합니다. 자세한 내용은 [아티클을 정의](../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
4.  게시 데이터베이스의 게시자에서 1단계의 **\@publication** 값을 지정하여 [sp_startpublication_snapshot&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)을 실행합니다.  
  
## <a name="apply-a-snapshot"></a>스냅샷 적용  

### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio 사용
  
1.  스냅샷이 생성된 후에는 구독을 배포 에이전트나 병합 에이전트와 동기화하여 스냅샷을 적용합니다.   
    -   에이전트가 계속 실행되도록 설정된 경우(트랜잭션 복제에 대한 기본값) 스냅샷은 생성된 후 자동으로 적용됩니다.   
    -   에이전트가 일정대로 실행되도록 설정된 경우 일정에 따라 다음에 에이전트가 실행될 때 스냅샷이 적용됩니다.    
    -   에이전트가 요청 시 실행되도록 설정된 경우 사용자가 다음에 에이전트를 실행할 때 스냅숏이 적용됩니다.  
  
     구독 동기화 방법은 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) 및 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)대화 상자에서 다시 초기화할 구독을 표시합니다.  
  
###   <a name="use-transact-sql"></a>Transact-SQL 사용  
 
1.  스냅샷, 트랜잭션 또는 병합 게시를 만듭니다. 자세한 내용은 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
2.  아티클을 게시에 추가합니다. 자세한 내용은 [아티클을 정의](../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
3.  명령 프롬프트 또는 배치 파일에서 [snapshot.exe](../../relational-databases/replication/agents/replication-snapshot-agent.md) 를 실행하여 **Replication Snapshot Agent**를 시작하고 다음 명령줄 인수를 지정합니다.  
  
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
    -   **-PublisherSecurityMode** =  **\@publisher_security_mode**  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예제에서는 트랜잭션 게시를 만들고 **sqlcmd** 스크립팅 변수를 사용하여 새 게시에 대한 스냅샷 에이전트 작업을 추가하는 방법을 보여 줍니다. 또한 추가한 작업을 시작합니다.  
  
 [!code-sql[HowTo#sp_trangenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_1.sql)]  
  
 이 예제에서는 병합 게시를 만들고 **sqlcmd** 변수를 사용하여 게시에 대한 스냅샷 에이전트 작업을 추가합니다. 또한 추가한 작업을 시작합니다.  
  
 [!code-sql[HowTo#sp_mergegenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_2.sql)]  
  
 다음 명령줄 인수는 스냅샷 에이전트를 시작하여 병합 게시에 대한 스냅샷을 생성합니다.  
  
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
 스냅샷 에이전트는 게시가 만들어진 후 스냅샷을 생성합니다. RMO(복제 관리 개체)를 사용하여 이러한 스냅샷을 프로그래밍 방식으로 생성하고 복제 에이전트 기능에 액세스하도록 관리 코드에 지시할 수 있습니다. 사용하는 개체는 복제 유형에 따라 달라집니다. 스냅샷 에이전트는 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 개체를 사용하여 동기적으로 시작하거나 에이전트 작업을 사용하여 비동기적으로 시작할 수 있습니다. 생성된 초기 스냅샷은 구독이 처음 동기화될 때 구독자로 전송되어 적용됩니다. 기존 스냅샷에 유효한 최신 데이터가 필요하게 될 때마다 에이전트를 다시 실행해야 합니다. 자세한 내용은 [게시 유지 관리](../../relational-databases/replication/publish/maintain-publications.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 [Windows .NET Framework에서 제공하는](https://go.microsoft.com/fwlink/?LinkId=34733) 암호화 서비스 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 사용합니다.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>스냅샷 에이전트 작업을 시작하여 스냅샷 또는 트랜잭션 게시에 대한 초기 스냅샷을 생성하려면(비동기)  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체의 나머지 속성을 로드합니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A>의 값이 **false**이면 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A>를 호출하여 이 게시에 대한 스냅샷 에이전트 작업을 만듭니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 메서드를 호출하여 이 게시에 대한 스냅샷을 생성하는 에이전트 작업을 시작합니다.  
  
6.  (옵션) <xref:Microsoft.SqlServer.Replication.TransPublication.SnapshotAvailable%2A> 의 값이 **true**이면 구독자에서 스냅샷을 사용할 수 있습니다.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-running-the-snapshot-agent-synchronous"></a>스냅샷 에이전트를 실행하여 스냅샷 또는 트랜잭션 게시에 대한 초기 스냅샷을 생성하려면(동기)  
  
1.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 클래스의 인스턴스를 만들고 다음 필수 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - 게시자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - 게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - 게시의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - 배포자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - 게시자에 연결할 때 Windows 인증을 사용하려면 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 값, 게시자에 연결할 때 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 인증을 사용하려면 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> , <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값. Windows 인증을 사용하는 것이 좋습니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - 배포자에 연결할 때 Windows 인증을 사용하려면 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 값, 배포자에 연결할 때 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 인증을 사용하려면 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> , <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값. Windows 인증을 사용하는 것이 좋습니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationType.Transactional> 에 <xref:Microsoft.SqlServer.Replication.ReplicationType.Snapshot> 또는 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>값을 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 메서드를 호출합니다.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>스냅샷 에이전트 작업을 시작하여 병합 게시에 대한 초기 스냅샷을 생성하려면(비동기)  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체의 나머지 속성을 로드합니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A>의 값이 **false**이면 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A>를 호출하여 이 게시에 대한 스냅샷 에이전트 작업을 만듭니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 메서드를 호출하여 이 게시에 대한 스냅샷을 생성하는 에이전트 작업을 시작합니다.  
  
6.  (옵션) <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 의 값이 **true**이면 구독자에서 스냅샷을 사용할 수 있습니다.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-running-the-snapshot-agent-synchronous"></a>스냅샷 에이전트를 실행하여 병합 게시에 대한 초기 스냅샷을 생성하려면(동기)  
  
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
 이 예에서는 스냅샷 에이전트를 동기적으로 실행하여 트랜잭션 게시에 대한 초기 스냅샷을 생성합니다.  
  
 [!code-cs[HowTo#rmo_GenerateSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot)]  
  
 이 예에서는 에이전트 작업을 비동기적으로 시작하여 트랜잭션 게시에 대한 초기 스냅샷을 생성합니다.  
  
 [!code-cs[HowTo#rmo_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot_withjob)]  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)   
 [스냅샷으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [스크립팅 변수와 함께 sqlcmd 사용](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
