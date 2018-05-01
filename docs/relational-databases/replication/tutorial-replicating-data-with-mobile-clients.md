---
title: '자습서: 서버와 모바일 클라이언트 간의 복제 구성(병합) | Microsoft Docs'
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d9751b7adc3d2cd4169bcd6b3a174de720c05eb9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-configure-replication-between-a-server-and-mobile-clients-merge"></a>자습서: 서버와 모바일 클라이언트 간의 복제 구성(병합)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
병합 복제는 가끔씩만 연결되는 중앙 서버와 모바일 클라이언트 간에 데이터를 이동할 때 발생하는 문제를 해결하는 좋은 방법입니다. 복제 마법사를 사용하면 병합 복제 토폴로지를 쉽게 구성하고 관리할 수 있습니다. 이 자습서에서는 모바일 클라이언트에 대해 복제 토폴로지를 구성하는 방법에 대해 설명합니다.  병합 복제에 대한 자세한 내용은 [병합 복제의 개요](https://docs.microsoft.com/en-us/sql/relational-databases/replication/merge/merge-replication)를 참조하세요.
  
## <a name="what-you-will-learn"></a>학습 내용  
이 자습서에서는 병합 복제를 사용하여 중앙 데이터베이스의 데이터를 여러 모바일 사용자에게 게시하여 각 사용자가 고유하게 필터링된 데이터의 하위 집합을 얻을 수 있도록 안내합니다. 

이 자습서에서는 다음 작업 방법을 배웁니다.
> [!div class="checklist"]
> * 병합 복제를 위한 게시자 구성
> * 병합 게시를 위한 모바일 구독자 추가
> * 병합 게시에 구독 동기화
  
## <a name="prerequisites"></a>사전 요구 사항  
이 자습서는 기본적인 데이터베이스 작업에는 익숙하지만 복제에 대한 경험은 풍부하지 않은 사용자를 위한 것입니다. 이 자습서를 시작하기 전에 [자습서: 복제용 서버 준비](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)를 완료해야 합니다.  
  
이 자습서를 사용하려면 시스템에 SQL Server Management Studio 및 다음 구성 요소가 설치되어 있어야 합니다.  
  
-   게시자 서버(원본)  
  
    -   SQL Server Express 또는 SQL Server Compact를 제외한 모든 SQL Server 버전. 이러한 버전은 복제 게시자가 될 수 없습니다.   
    -   [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스. 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다.  
  
-   구독자 서버(대상)  
  
    -   [!INCLUDE[ssEW](../../includes/ssew-md.md)]를 제외한 모든 SQL Server 버전. [!INCLUDE[ssEW](../../includes/ssew-md.md)] 을 지원하지 않습니다. 

- [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)을 설치합니다.
- [AdventureWorks 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)를 다운로드합니다. SSMS에서 데이터베이스를 복원하는 방법에 대한 지침은 [데이터베이스 복원](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)을 참조하세요.  
 
  
>[!NOTE]
> - 두 버전이 넘게 차이 나는 SQL Server 간에는 복제가 지원되지 않습니다. 자세한 내용은 [복제 토폴로지에서 지원되는 SQL 버전](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/)을 참조하세요.
> - [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 **sysadmin** 고정 서버 역할의 멤버인 로그인을 사용하여 게시자 및 구독자에 연결해야 합니다. sysadmin 역할에 대한 자세한 내용은 [서버 수준 역할](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles)을 참조하세요.  
  
  
**이 자습서를 완료하는 데 소요되는 예상 시간: 60분**  
  
## <a name="configure-a-publisher-for-merge-replication"></a>병합 복제를 위한 게시자 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 섹션에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 병합 게시를 만들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 샘플 데이터베이스에 **Employee**, **SalesOrderHeader** 및 **SalesOrderDetail** 테이블의 하위 집합을 게시합니다. 이러한 테이블은 각 구독에 고유한 데이터 파티션이 포함되도록 매개 변수가 있는 행 필터로 필터링됩니다. 또한 병합 에이전트에 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 PAL(게시 액세스 목록)에 추가합니다.  
  
### <a name="create-merge-publication-and-define-articles"></a>병합 게시 만들기 및 아티클 정의  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2. **개체 탐색기**에서 **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭하고 **시작**을 선택하여 시작합니다. 에이전트가 시작되지 않는 경우 **SQL Server 구성 관리자**에서 수동으로 수행해야 합니다.  
3. **복제** 폴더를 확장하고, **로컬 게시**를 마우스 오른쪽 단추로 클릭한 다음, **새 게시**를 선택합니다.  게시 구성 마법사가 시작됩니다.  

    ![새 게시 마법사 시작](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
3.  게시 데이터베이스 페이지에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 선택한 후, **다음**을 선택합니다. 

      
4.  게시 유형 페이지에서 **병합 게시**를 선택한 후, **다음**을 선택합니다.  
    1. 구독자 유형 페이지에서 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상만 선택되어 있는지 확인한 후, **다음**을 선택합니다. 

    ![병합 복제](media/tutorial-replicating-data-with-mobile-clients/mergerpl.png)
  
   
6.  아티클 페이지에서 **테이블** 노드를 확장하고 세 테이블(**직원**, **SalesOrderHeader** 및 **SalesOrderDetail**)을 선택합니다. **다음**을 선택합니다.  

    ![병합 아티클](media/tutorial-replicating-data-with-mobile-clients/mergearticles.png)

    >[!NOTE]
    > Employee 테이블에는 hierarchyid 데이터 형식을 가진 열(OrganizationNode)이 포함되어 있습니다. 이는 SQL 2017의 복제에만 지원됩니다. SQL 2017보다 낮은 빌드를 사용하는 경우, 양방향 복제에서 이 열을 사용할 때 잠재적인 데이터 손실을 알리는 메시지가 화면 맨 아래에 표시됩니다. 이 자습서의 목적상 이 메시지는 무시할 수 있습니다. 그러나 지원되는 빌드를 사용하지 않는 경우 프로덕션 환경에서 이 데이터 형식을 복제해서는 안 됩니다. hierarchyid 데이터 형식을 복제하는 방법에 대한 자세한 내용은 [복제에서 hierarchyid 열 사용](https://docs.microsoft.com/en-us/sql/t-sql/data-types/hierarchyid-data-type-method-reference#using-hierarchyid-columns-in-replicated-tables)을 참조하세요.
    
  
7.  테이블 행 필터링 페이지에서 **추가**를 선택한 다음, **필터 추가**를 선택합니다.  
  
8.  **필터 추가** 대화 상자의 **필터링할 테이블 선택**에서 **Employee(HumanResources)** 를 선택합니다. **LoginID** 열을 선택하고, 오른쪽 화살표를 선택하여 필터 쿼리의 WHERE 절에 해당 열을 추가한 후, WHERE 절을 다음과 같이 수정합니다.  
  
    ```sql 
    WHERE [LoginID] = HOST_NAME()  
    ```  
  
    1. **이 테이블의 행을 단일 구독으로 이동**을 선택하고 **확인**을 선택합니다.  
 
    ![필터 추가](media/tutorial-replicating-data-with-mobile-clients/mergeaddfilter.png)

    
  
10. **테이블 행 필터링** 페이지에서 **Employee(Human Resources)** 를 선택하고 **추가**를 선택한 다음, **선택한 필터 확장을 위해 조인 추가**를 선택합니다.  
  
    1. **조인 추가** 대화 상자의 **조인된 테이블**에서 **Sales.SalesOrderHeader**를 선택합니다. **수동으로 조인 문 작성**을 선택하고, 다음과 같이 조인 문을 완성합니다.  
  
    ```sql  
    ON [Employee].[BusinessEntityID] =  [SalesOrderHeader].[SalesPersonID] 
    ```  
  
    2. **조인 옵션 지정**에서 **고유 키**를 선택한 다음, **확인**을 선택합니다.

    ![필터에 조인 추가](media/tutorial-replicating-data-with-mobile-clients/mergeaddjoin.png)

  
13. 테이블 행 필터링 페이지에서 **SalesOrderHeader**를 선택하고 **추가**를 선택한 다음, **선택한 필터 확장을 위해 조인 추가**를 선택합니다.  
  
    1. **조인 추가** 대화 상자의 **조인된 테이블** 에서 **Sales.SalesOrderDetail**을 선택합니다.    
    2. **작성기를 사용하여 명령문 만들기**를 선택합니다.  
    c. **미리 보기** 상자에서 조인 문이 다음과 같은지 확인합니다.  
  
    ```sql  
    ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID] 
    ```  
  
    d. **조인 옵션 지정**에서 **고유 키**를 선택한 다음, **확인**을 선택합니다. **다음**을 선택합니다. 

       ![판매 주문 테이블 조인](media/tutorial-replicating-data-with-mobile-clients/joinsalestables.png)
  
21. **즉시 스냅숏 만들기**를 선택하고 **스냅숏 에이전트 실행 시간 예약**을 선택 취소한 후 **다음**을 선택합니다.  

    ![즉시 스냅숏 만들기](media/tutorial-replicating-data-with-mobile-clients/snapshotagent.png)
  
22. 에이전트 보안 페이지에서 **보안 설정**을 선택하고 **프로세스 계정** 상자에 <*Publisher_Machine_Name>***\repl_snapshot**을 입력한 다음, 이 계정에 대한 암호를 입력하고 **확인**을 선택합니다. **다음**을 선택합니다.  

    ![스냅숏 에이전트 보안](media/tutorial-replicating-data-with-mobile-clients/snapshotagentsecurity.png)
  
23. **마법사 완료** 페이지에서 **게시 이름** 상자에 **AdvWorksSalesOrdersMerge**를 입력하고 **마침**을 선택합니다.  

    ![병합 복제 이름 지정](media/tutorial-replicating-data-with-mobile-clients/namemergerepl.png)
  
24. 게시를 만든 후 **닫기**를 선택합니다. **개체 탐색기**의 **복제** 노드에서 **로컬 게시** 및 **새로 고침**을 마우스 오른쪽 단추로 클릭하여 새 병합 복제를 봅니다.  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>스냅숏 생성의 상태를 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  로컬 게시 폴더에서 **AdvWorksSalesOrdersMerge**를 마우스 오른쪽 단추로 클릭한 다음, **스냅숏 에이전트 상태 보기**를 선택합니다.  

    ![스냅숏 에이전트 상태 보기](media/tutorial-replicating-data-with-mobile-clients/viewsnapshotagentstatus.png)
  
3.  게시에 대한 스냅숏 에이전트 작업의 현재 상태가 표시됩니다. 다음 단원을 진행하기 전에 스냅숏 작업이 성공했는지 확인합니다.  
  
### <a name="to-add-the-merge-agent-login-to-the-pal"></a>PAL에 병합 에이전트 로그인을 추가하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  로컬 게시 폴더에서 **AdvWorksSalesOrdersMerge**를 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.  
  
    1. **게시 액세스 목록** 페이지를 선택하고 **추가**를 선택합니다. 
  
    2. 게시 액세스 추가 대화 상자에서 <*Publisher_Machine_Name>***\repl_merge**를 선택하고 **확인**을 선택합니다. **확인**을 선택합니다. 

    ![PAL 병합](media/tutorial-replicating-data-with-mobile-clients/mergepal.png) 

  
**참고 항목**:  
[게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)  
[매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
[아티클 정의](../../relational-databases/replication/publish/define-an-article.md)  
  
  
## <a name="creating-a-subscription-to-the-merge-publication"></a>병합 게시에 대한 구독 만들기
이 섹션에서는 이전에 만든 병합 게시에 구독을 추가합니다. 이 자습서에서는 원격 구독자(NODE2\SQL2016)를 사용합니다. 그런 다음 구독 데이터베이스에 대한 사용 권한을 설정하고 새 구독에 대한 필터링된 데이터 스냅숏을 수동으로 생성합니다.   
  
### <a name="add-a-subscriber-for-merge-publication"></a>병합 게시를 위한 구독자 추가
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결하고 서버 노드를 확장합니다. **복제** 폴더를 확장하고 **로컬 구독** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **새 구독**을 선택합니다. 새 구독 마법사가 시작됩니다.

    ![새 구독](media/tutorial-replicating-data-with-mobile-clients/newsub.png)
  
2.  **게시** 페이지에서 **게시자** 목록에 있는 **SQL Server 게시자 찾기**를 선택합니다.  
  
    1. **서버에 연결** 대화 상자에서 **서버 이름** 상자에 게시자 인스턴스의 이름을 입력하고 **연결**을 선택합니다. 

    ![게시에 게시자 추가](media/tutorial-replicating-data-with-mobile-clients/publication.png)
  
4.  **AdvWorksSalesOrdersMerge**를 선택하고 **다음**을 선택합니다.  
  
5.  병합 에이전트 위치 페이지에서 **각 에이전트를 해당 구독자에서 실행**을 선택한 후, **다음**을 선택합니다.  

    ![끌어오기 구독](media/tutorial-replicating-data-with-mobile-clients/pullsub.png)
  
6.  구독자 페이지에서 구독자 서버의 인스턴스 이름을 선택하고 **구독 데이터베이스**의 목록에서 **새 데이터베이스**를 선택합니다.  
  
    1. **새 데이터베이스** 대화 상자에서 **데이터베이스 이름** 상자에 **SalesOrdersReplica**를 입력하고 **확인**을 선택한 후, **다음**을 선택합니다. 

    ![Sub에 DB 추가](media/tutorial-replicating-data-with-mobile-clients/addsubdb.png)
  
8.  병합 에이전트 보안 페이지에서 줄임표(**…**) 단추를 선택하고 **프로세스 계정** 상자에 <*Subscriber_Machine_Name>***\repl_merge**를 입력한 다음, 해당 계정의 암호를 입력하고 **확인**, **다음**, **다음**을 차례로 선택합니다.  

    ![병합 에이전트 보안](media/tutorial-replicating-data-with-mobile-clients/mergeagentsecurity.png)

9. **동기화 일정**에서 **에이전트 일정**을 **요청 시에만 실행**으로 설정합니다. **다음**을 선택합니다.  

    ![동기화 일정](media/tutorial-replicating-data-with-mobile-clients/mergesyncschedule.png)
  
9. 구독 초기화 페이지의 **초기화 시기** 목록에서 **첫 번째 동기화**를 선택하고 **다음**을 선택한 다음, 다시 **다음**을 선택합니다. 

    ![첫 번째 동기화](media/tutorial-replicating-data-with-mobile-clients/firstsync.png)

10. HOST_NAME 값 페이지에서 **HOST_NAME 값** 상자에 **adventure-works\pamela0** 값을 입력한 다음, **마침**을 선택합니다.  

    ![Hostname](media/tutorial-replicating-data-with-mobile-clients/hostname.png)
  
11. **마침**을 다시 선택하고 구독이 생성되면 **닫기**를 선택합니다.  

### <a name="setting-server-permissions-at-the-subscriber"></a>구독자에서 서버 사용 권한 설정  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결하여 **보안**을 확장하고 **로그인**을 마우스 오른쪽 단추로 클릭한 다음, **새 로그인**을 선택합니다.  
  
    1. **일반** 페이지에서 **검색**을 선택하고 **개체 이름 입력** 필드에서 <*Subscriber_Machine_Name>***\repl_merge**를 입력한 다음, **이름 확인**, **확인**을 차례로 선택합니다. 
    
    ![구독자에 로그인](media/tutorial-replicating-data-with-mobile-clients/sublogin.png)
  
1. **사용자 매핑** 페이지에서 **SalesOrdersReplica** 데이터베이스를 선택하고 **db_owner** 역할을 선택합니다.  **보안 개체** 페이지에서 **추적 변경**에 'Explicit' 권한을 부여합니다. **확인**을 선택합니다.

    ![Sub에 DBO로 로그인 설정](media/tutorial-replicating-data-with-mobile-clients/setdbo.png)
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>구독에 대한 필터링된 데이터 스냅숏을 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  **로컬 게시** 폴더에서 **AdvWorksSalesOrdersMerge** 게시를 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.  
   
    1. **데이터 파티션** 페이지를 선택한 다음, **추가**를 선택합니다.   
    2. **데이터 파티션 추가** 대화 상자의 **HOST_NAME 값** 상자에 **adventure-works\pamela0**를 입력한 다음, **확인**을 선택합니다.  
    c. 새로 추가된 파티션을 선택하고 **선택한 스냅숏 지금 생성**을 선택한 다음, **확인**을 선택합니다. 

    ![파티션 추가](media/tutorial-replicating-data-with-mobile-clients/partition.png)
  
  
**참고 항목**:  
[게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
[끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)  
[Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  

## <a name="synchronize-the-subscription-to-the-merge-publication"></a>병합 게시에 구독 동기화

이 섹션에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 구독을 초기화하기 위해 병합 에이전트를 시작합니다. 또한 이 절차를 사용하여 게시자와 동기화합니다.   
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>동기화를 시작하고 구독을 초기화하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결합니다.  
2. **SQL Server 에이전트**가 실행 중인지 확인합니다. 그렇지 않은 경우, **개체 탐색기**에서 **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭하고 **시작**을 선택합니다. 에이전트를 시작하지 못한 경우 **SQL Server 구성 관리자**를 사용하여 수동으로 시작해야 합니다. 
  
2.  **복제** 노드를 확장합니다. **로컬 구독** 폴더에서 **SalesOrdersReplica** 데이터베이스의 구독을 마우스 오른쪽 단추로 클릭한 다음, **동기화 상태 보기**를 선택합니다.  
  
    1. **시작**을 선택하여 구독을 초기화합니다. 

    ![동기화 상태](media/tutorial-replicating-data-with-mobile-clients/mergesyncstatus.png)
    
  
  
### <a name="next-steps"></a>Next Steps  
병합 복제를 위해 게시자와 구독자를 모두 성공적으로 구성했습니다.  또한 게시자나 구독자에 있는 **SalesOrderHeader** 나 **SalesOrderDetail** 테이블에서 데이터를 삽입, 업데이트 또는 삭제할 수 있고 네트워크가 연결되어 있을 때 이 절차를 반복하여 게시자와 구독자 사이의 데이터를 동기화한 다음 다른 서버에 있는 **SalesOrderHeader** 나 **SalesOrderDetail** 테이블을 쿼리하여 복제된 변경 내용을 볼 수 있습니다.  
  
**참고 항목**:   
[스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[데이터 동기화](../../relational-databases/replication/synchronize-data.md)  
[끌어오기 구독 동기화](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
  
