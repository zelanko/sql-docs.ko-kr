---
title: '자습서: 두 개의 완전히 연결된 서버 간 복제 구성(트랜잭션) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de374f4372f62741ff3c49a9433cf339cecf3d26
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-configure-replication-between-two-fully-connected-servers-transactional"></a>자습서: 두 개의 완전히 연결된 서버 간 복제 구성(트랜잭션)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
트랜잭션 복제는 계속 연결되는 서버 간에 데이터를 이동할 때 발생하는 문제를 해결하는 좋은 방법입니다. 복제 마법사를 사용하면 복제 토폴로지를 쉽게 구성하고 관리할 수 있습니다. 이 자습서에서는 계속 연결되는 서버에 대해 트랜잭션 복제 토폴로지를 구성하는 방법을 보여줍니다. 트랜잭션 복제가 작동하는 방법에 대한 자세한 내용은 [트랜잭션 복제 개요](https://docs.microsoft.com/en-us/sql/relational-databases/replication/transactional/transactional-replication)를 참조하세요. 
  
## <a name="what-you-will-learn"></a>학습 내용  
이 자습서에서는 트랜잭션 복제를 사용하여 한 데이터베이스의 데이터를 다른 데이터베이스에 게시하는 방법을 보여 줍니다. 

이 자습서에서는 다음 작업 방법을 배웁니다.
> [!div class="checklist"]
> * 트랜잭션 복제를 통해 게시자 만들기
> * 트랜잭션 게시자에 대한 구독자 만들기
> * 구독 유효성 검사 및 대기 시간 측정
> * 오류 해결 방법
  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 자습서는 기본적인 데이터베이스 작업에는 익숙하지만 복제에 대한 경험은 풍부하지 않은 사용자를 위한 것입니다. 이 자습서를 사용하려면 이전 자습서인 [복제용 서버 준비](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)를 완료해야 합니다.  
  
이 자습서를 사용하려면 시스템에 SQL Server Management Studio (SSMS) 및 다음 구성 요소가 있어야 합니다.  
  
-   게시자 서버(원본)  
  
    -   SQL Server Express 또는 SQL Compact를 제외한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전. 이들 버전은 복제 게시자가 될 수 없습니다.   
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 예제 데이터베이스. 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다.  
  
-   구독자 서버(대상)  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제외한 [!INCLUDE[ssEW](../../includes/ssew-md.md)]의 모든 버전. [!INCLUDE[ssEW](../../includes/ssew-md.md)] 는 트랜잭션 복제에서 구독자가 될 수 없습니다.  
  
- [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)을 설치합니다.
- [AdventureWorks 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)를 다운로드합니다. SSMS에서 데이터베이스를 복원하는 방법에 대한 지침은 [데이터베이스 복원](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)을 참조하세요. 
 
>[!NOTE]
> - 두 버전이 넘게 차이 나는 SQL Server 간에는 복제가 지원되지 않습니다. 자세한 내용은 [복제 토폴로지에서 지원되는 SQL 버전](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/)을 참조하세요.
> - [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 **sysadmin** 고정 서버 역할의 멤버인 로그인을 사용하여 게시자 및 구독자에 연결해야 합니다. sysadmin 역할에 대한 자세한 내용은 [서버 수준 역할](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles)을 참조하세요.  
  
  
**이 자습서를 완료하는 데 소요되는 예상 시간: 60분**  
  
## <a name="configure-the-publisher-for-transactional-replication"></a>트랜잭션 복제를 위한 게시자 구성
이 섹션에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 트랜잭션 게시를 만들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 샘플 데이터베이스에 **Product** 테이블의 필터링된 하위 집합을 게시합니다. 또한 배포 에이전트에 사용된 SQL Server 로그인을 PAL(게시 액세스 목록)에 추가합니다. 이 자습서를 시작하려면 이전 자습서인 [복제용 서버 준비](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)를 완료해야 합니다.


### <a name="create-a-publication-and-define-articles"></a>게시 만들기 및 아티클 정의
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2. **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭하고 **시작**을 선택합니다. SQL Server 에이전트는 게시를 만들기 전에 실행되어야 합니다. 에이전트가 시작되지 않으면 **SQL Server 구성 관리자**에서 수동으로 시작해야 합니다. 
3. **복제** 폴더를 확장하고 **로컬 게시** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **새 게시**를 선택합니다.  그러면 게시 구성 마법사가 시작됩니다.  

    ![새 게시](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
  
3. 게시 데이터베이스 페이지에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 선택한 후, **다음**을 선택합니다.  
  
4. 게시 유형 페이지에서 **트랜잭션 게시**를 선택한 후, **다음**을 선택합니다.  

    ![트랜잭션 복제](media/tutorial-replicating-data-between-continuously-connected-servers/tranrepl.png)
  
5. 아티클 페이지에서 **테이블** 노드를 확장하고 **제품** 확인란을 선택합니다. 그런 다음, **제품**을 확장하고 **ListPrice** 및 **StandardCost** 옆에 있는 확인란의 선택을 취소합니다. **다음**을 선택합니다.  

    ![게시할 아티클](media/tutorial-replicating-data-between-continuously-connected-servers/replarticles.png)
  
6. 테이블 행 필터링 페이지에서 **추가**를 선택합니다.   
  
7. **필터 추가** 대화 상자에서 **SafetyStockLevel** 열을 선택하고 오른쪽 화살표를 선택하여 필터 쿼리의 필터 문 WHERE 절에 해당 열을 추가합니다. 그런 다음, WHERE 절 한정자에 수동으로 다음과 같이 입력합니다.  
  
    ```sql  
    WHERE [SafetyStockLevel] < 500  
    ```
  
    ![필터 문](media/tutorial-replicating-data-between-continuously-connected-servers/filter.png)
  
8. **확인**선택하고 **다음**을 선택합니다.  
  
9. **즉시 스냅숏을 만들고 구독 초기화에 사용할 수 있도록 유지** 확인란을 선택하고 **다음**을 선택합니다.  

    ![스냅숏 에이전트](media/tutorial-replicating-data-between-continuously-connected-servers/snapshot.png)
  
10. 에이전트 보안 페이지에서 **스냅숏 에이전트의 보안 설정 사용** 확인란을 선택 취소합니다.   
  
    1. 스냅숏 에이전트에 대한 **보안 설정**을 선택하고 **프로세스 계정** 상자에 <*Publisher_Machine_Name>***\repl_snapshot**을 입력하고, 이 계정에 대한 암호를 입력한 다음, **확인**을 선택합니다.  

    ![스냅숏 에이전트 보안](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagentsecurity.png)
  
12. 이전 단계를 반복하여 <*Publisher_Machine_Name*>**\repl_logreader**를 로그 판독기 에이전트에 대한 프로세스 계정으로 설정한 다음, **확인**을 선택합니다.  

    ![로그 판독기 에이전트 보안](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentsecurity.png)   

  
13. 마법사 완료 페이지에서 **게시 이름** 상자에 **AdvWorksProductTrans**를 입력하고 **마침**을 선택합니다.  

    ![게시 이름 지정](media/tutorial-replicating-data-between-continuously-connected-servers/advworksproducttrans.png)
  
14. 게시를 만든 후 **닫기** 를 선택하여 마법사를 완료합니다. 

    게시를 만들려고 할 때 SQL Server 에이전트가 실행되고 있지 않은 경우 다음과 같은 오류가 발생할 수 있습니다. 이것은 게시가 성공적으로 만들어졌지만 스냅숏 에이전트를 시작하지 못했음을 나타냅니다. 이러한 경우 SQL Server 에이전트를 시작한 다음, 스냅숏 에이전트를 수동으로 시작해야 합니다. 이에 대한 지침은 다음 섹션에서 다룹니다. 

    ![스냅숏 에이전트 시작 실패](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenterror.png)
    
  
### <a name="to-view-the-status-of-snapshot-generation"></a>스냅숏 생성의 상태를 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  **로컬 게시** 폴더에서 **AdvWorksProductTrans**를 마우스 오른쪽 단추로 클릭한 다음, **스냅숏 에이전트 상태 보기**를 선택합니다.  

    ![스냅숏 에이전트 상태](media/tutorial-replicating-data-between-continuously-connected-servers/viewsnapshot.png)
  
3.  게시에 대한 스냅숏 에이전트 작업의 현재 상태가 표시됩니다. 다음 섹션을 진행하기 전에 스냅숏 작업이 성공했는지 확인합니다.
          
    게시를 처음 만들 때 SQL Server 에이전트가 실행되고 있지 않은 경우, 게시의 **스냅숏 에이전트 상태**를 확인하면 스냅숏 에이전트가 '실행되지 않음'으로 표시됩니다. 이 경우 **시작**을 선택하여 스냅숏 에이전트를 시작합니다. 

       ![스냅숏 에이전트 시작](media/tutorial-replicating-data-between-continuously-connected-servers/startsnapshotagent.png)
     
       여기서 오류가 표시되면 [스냅숏 에이전트를 사용하여 오류 해결](#troubleshoot-erros-with-snapshot-agent)을 참조하세요. 

  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>PAL에 배포 에이전트 로그인을 추가하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  **로컬 게시** 폴더에서 **AdvWorksProductTrans**를 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.  **게시 속성** 대화 상자가 표시됩니다.    
  
    1. **게시 액세스 목록** 페이지를 선택하고 **추가**를 선택합니다.  
    2. **게시 액세스 추가** 대화 상자에서 <*Publisher_Machine_Name>***\repl_distribution**을 선택한 다음, **확인**을 선택합니다. **확인**을 선택합니다.

   
   ![PAL 목록에 로그인 추가](media/tutorial-replicating-data-between-continuously-connected-servers/tranreplproperties.png)

**참고 항목**:  
[복제 프로그래밍 개념](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  

## <a name="create-a-subscription-to-the-transactional-publication"></a>트랜잭션 게시에 구독 만들기
이 섹션에서는 이전에 만든 게시에 구독자를 추가합니다. 이 자습서에서는 원격 구독자(NODE2\SQL2016)를 사용하지만 구독을 게시자에게 로컬로 추가할 수도 있습니다. 

### <a name="to-create-the-subscription"></a>구독을 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  **로컬 게시** 폴더에서 **AdvWorksProductTrans** 게시를 마우스 오른쪽 단추로 클릭한 다음, **새 구독**을 선택합니다.  새 구독 마법사가 시작됩니다. 
 
    ![새 구독](media/tutorial-replicating-data-between-continuously-connected-servers/newsub.png)     
  
3.  게시 페이지에서 **AdvWorksProductTrans**를 선택한 후, **다음**을 선택합니다.  

    ![Tran 게시자 선택](media/tutorial-replicating-data-between-continuously-connected-servers/selectpub.png)
  
4.  배포 에이전트 위치 페이지에서 **배포자에서 모든 에이전트 실행**을 선택한 후, **다음**을 선택합니다.  끌어오기 및 밀어넣기 구독에 대한 자세한 내용은 [게시 구독](https://docs.microsoft.com/en-us/sql/relational-databases/replication/subscribe-to-publications)을 참조하세요.

    ![배포자에서 에이전트 실행](media/tutorial-replicating-data-between-continuously-connected-servers/runagentsatdist.png)
  
5.  구독자 페이지에서 구독자 인스턴스 이름이 표시되지 않는 경우 **구독자 추가**를 선택한 다음, 드롭다운 목록에서 **SQL Server 구독자 추가**를 선택합니다. 그러면 **서버에 연결** 대화 상자가 시작됩니다. 구독자 인스턴스 이름을 입력한 다음, **연결**을 선택합니다.  
    
    1. 구독자가 추가되면 구독자의 인스턴스 이름 옆에 있는 상자를 선택합니다. 그런 다음, **구독 데이터베이스**에서 **새 데이터베이스**를 선택합니다.   

  ![구독자 서버 추가](media/tutorial-replicating-data-between-continuously-connected-servers/addsub.png)

7. 그러면 **새 데이터베이스** 대화 상자가 시작됩니다. **데이터베이스 이름** 상자에 **ProductReplica**를 입력하고 **확인**을 선택한 후, **다음**을 선택합니다. 
  
    ![제품 복제본 DB](media/tutorial-replicating-data-between-continuously-connected-servers/productreplica.png)
  
8.  **배포 에이전트 보안** 대화 상자에서 줄임표(**...**) 단추를 선택합니다. **프로세스 계정** 상자에 <*Publisher_Machine_Name>***\repl_distribution**을 입력하고 이 계정의 암호를 입력한 다음, **확인**, **다음**을 차례로 선택합니다.

    ![배포 계정 추가](media/tutorial-replicating-data-between-continuously-connected-servers/adddistaccount.png)
  
9. **마침**을 선택하여 나머지 페이지에 기본값을 적용하고 마법사를 완료합니다.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>구독자에서 데이터베이스 권한 설정  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결하여 **보안**을 확장하고 **로그인**을 마우스 오른쪽 단추로 클릭한 다음, **새 로그인**을 선택합니다.     
  
    1. **일반** 페이지의 **로그인 이름**에서 **검색**을 선택하고 <*Subscriber_Machine_Name>***\repl_distribution**에 대한 로그인을 추가합니다.
    2. **사용자 매핑** 페이지에서 **ProductReplica** 데이터베이스에 대한 로그인을 **db_owner**에 부여합니다. 

    ![구독자에 로그인](media/tutorial-replicating-data-between-continuously-connected-servers/loginforsub.png)

2. **확인**을 선택하여 **새 로그인** 대화 상자를 닫습니다. 

  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>구독의 동기화 상태를 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  **로컬 게시** 폴더에서 **AdvWorksProductTrans** 게시를 확장하고 **ProductReplica** 데이터베이스의 구독을 마우스 오른쪽 단추로 클릭한 다음, **동기화 상태 보기**를 선택합니다. 구독의 현재 동기화 상태가 표시됩니다.  
    ![동기화 상태 보기](media/tutorial-replicating-data-between-continuously-connected-servers/viewsyncstatus.png)
3.  **AdvWorksProductTrans**에 해당 구독이 표시되지 않으면 F5 키를 눌러 목록을 새로 고칩니다.  
  
**참고 항목**:  
[스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[밀어넣기 구독 만들기](../../relational-databases/replication/create-a-push-subscription.md)  
[게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  

## <a name="measuring-replication-latency"></a>복제 대기 시간 측정
이 섹션에서는 추적 프로그램 토큰을 사용하여 변경 내용이 구독자에 복제되었는지 여부 및 대기 시간을 확인합니다. 대기 시간은 게시자에서 변경한 내용이 구독자에게 표시되는 데 걸리는 시간입니다.
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하여 서버 노드를 확장하고 **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **복제 모니터 시작**을 선택합니다.

    ![복제 모니터 시작](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)

2. 왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자 인스턴스를 확장한 다음, **AdvWorksProductTrans** 게시를 선택합니다.  
  
    1. **추적 프로그램 토큰** 탭을 선택합니다.  
    2. **추적 프로그램 삽입**을 선택합니다.    
    c. **게시자에서 배포자로 연결 시 대기 시간**, **배포자에서 구독자로 연결 시 대기 시간**, **총 대기 시간**열에서 추적 프로그램 토큰에 대한 경과 시간을 확인합니다. **보류 중**이라는 값은 토큰이 지정된 지점에 아직 도달하지 않았음을 나타냅니다.


   ![추적 프로그램 토큰](media/tutorial-replicating-data-between-continuously-connected-servers/tracertoken.png)


**참고 항목**   
[트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

## <a name="error-troubleshooting-methodology"></a>오류 해결 방법
이 섹션에서는 기본 복제 동기화 실패 문제를 해결하는 방법을 설명합니다. 이 섹션에서는 문제 해결을 목적으로 복제 구성 요소를 탐색하는 방법을 소개합니다. 그러나 실제 발생한 오류는 여기에서 설명된 내용과 다를 수 있으므로 다른 해결 방법이 필요할 수 있습니다. 그럴 경우, 추가 문제 해결이 필요하며 이는 본 자습서의 범위를 벗어납니다. 


### <a name="troubleshoot-errors-with-snapshot-agent"></a>스냅숏 에이전트를 사용하여 오류 해결
**스냅숏 에이전트**는 스냅숏을 생성하고 지정된 스냅숏 폴더에 기록되는 에이전트입니다. 

1. 스냅숏 에이전트의 상태를 확인하려면 복제 중인 **로컬 게시** 노드를 확장하고 **AdvWorksProductTrans** 게시 > **스냅숏 에이전트 상태 보기**를 선택합니다. 
2. **스냅숏 에이전트 상태**에 오류가 보고되면 **스냅숏 에이전트** 작업 기록에서 자세한 내용을 확인할 수 있습니다. 여기에 액세스하려면 **개체 탐색기**에서 **SQL Server 에이전트**를 확장하고 **작업 활동 모니터**를 엽니다. 

    1. **범주**로 정렬하고 'REPL-스냅숏' 범주로 **스냅숏 에이전트**를 식별합니다. 

    2. **스냅숏 에이전트** 및 **기록 보기**를 오른쪽 단추로 클릭합니다. 

   ![스냅숏 에이전트 기록](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenthistory.png)
    
1. **스냅숏 에이전트 기록**에서 관련 로그 항목을 선택합니다. 이는 일반적으로 오류를 보고하는 항목 *앞*에 한두 줄로 되어 있습니다(오류는 빨간색 X로 표시됨).  로그 아래의 텍스트 상자에서 메시지 텍스트를 검토합니다. 

    ![스냅숏 에이전트 액세스 거부됨](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotaccessdenied.png)

        The replication agent had encountered an exception.
        Exception Message: Access to path '\\node1\repldata.....' is denied.


  스냅숏 폴더에 Windows 권한이 올바르게 구성되지 않은 경우 **스냅숏 에이전트**의 '액세스가 거부됨' 오류가 표시됩니다. repldata 폴더에서 <*Publisher_Machine_Name>***\repl_snapshot** 계정의 사용 권한을 확인해야 합니다. 자세한 내용은 [스냅숏 폴더에 대한 공유 만들기 및 사용 권한 할당](tutorial-preparing-the-server-for-replication.md#create-a-share-for-the-snapshot-folder-and-assign-permissions)을 참조하세요.

### <a name="troubleshoot-errors-with-log-reader-agent"></a>로그 판독기 에이전트를 사용하여 오류 해결
**로그 판독기 에이전트**는 게시자 데이터베이스에 연결하고 트랜잭션 로그에서 '복제용'으로 표시된 트랜잭션을 검색합니다. 그런 다음, 해당 트랜잭션을 **배포** 데이터베이스에 추가합니다. 

1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하여 서버 노드를 확장하고 **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **복제 모니터 시작**을 선택합니다.  

    ![복제 모니터 시작](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)
  
    복제 모니터 시작: ![복제 모니터](media/tutorial-replicating-data-between-continuously-connected-servers/replmonitor.png) 
   
2. 빨간색 X는 게시가 동기화되지 않음을 나타냅니다. 왼쪽에서 **내 게시자**를 확장한 다음, 관련 게시자 서버를 확장합니다.  
  
3.  왼쪽에 있는 **AdvWorksProductTrans** 게시를 선택한 다음, 탭 중 하나에서 빨간색 X를 찾아 문제가 어디에 있는지 확인합니다. 이 경우 빨간색 X가 **에이전트 탭**에 있으며 에이전트 중 하나에 오류가 발생했음을 나타냅니다. 

    ![에이전트 오류](media/tutorial-replicating-data-between-continuously-connected-servers/agenterror.png)

4. **에이전트 탭**을 선택하여 오류가 발생한 에이전트를 확인합니다. 

    ![로그 판독기 실패](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentfailure.png)


5. 이 보기에서는 **스냅숏 에이전트**와 **로그 판독기 에이전트**라는 두 에이전트를 보여줍니다. 오류가 발생한 에이전트에는 빨간색 X가 표시됩니다. 이 경우에는 **로그 판독기 에이전트**에 빨간색 X가 표시되어 있으며, 이는 문제가 있다는 의미입니다. 오류를 보고하는 줄을 두 번 클릭합니다(이 경우 **로그 판독기 에이전트**). 이렇게 하면 선택한 에이전트에 대한 **에이전트 기록**이 시작됩니다(이 경우 **로그 판독기 에이전트** 기록). 이는 오류에 대한 자세한 정보를 제공합니다. 
    
    ![로그 판독기 오류](media/tutorial-replicating-data-between-continuously-connected-servers/logreadererror.png)

       Status: 0, code: 20011, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.
       The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.
       Status: 0, code: 15517, text: 'Cannot execute as the database principal because the principal "dbo" does not exist, this type of principal cannot be impersonated, or you do not have permission.'.
       Status: 0, code: 22037, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.        

6. 앞서 언급한 오류는 일반적으로 게시자 데이터베이스의 소유자가 올바르게 설정되어 있지 않은 경우에 발생합니다. 이 문제는 일반적으로 데이터베이스가 복원되었을 때 발생합니다. 이를 확인하려면 **개체 탐색기**에서 **데이터베이스**를 확장하고 **AdventureWorks2012** > **속성**을 마우스 오른쪽 단추로 클릭합니다. **파일** 페이지 아래에 소유자가 있는지 확인합니다. 이 필드가 비어 있는 경우 문제의 가능한 원인은 다음과 같습니다. 

    ![DB 속성](media/tutorial-replicating-data-between-continuously-connected-servers/dbproperties.png)

7. **파일** 페이지에서 소유자가 비어 있는 경우 **AdventureWorks2012** 데이터베이스의 컨텍스트 내에서 **새 쿼리 창**을 엽니다. 다음 T-SQL 코드 조각을 실행합니다.

    ```sql
    -- set the owner of the database to 'sa' or a specific user account, without the brackets. 
    EXEC sp_changedbowner '<useraccount>'
    -- example for sa: exec sp_changedbowner 'sa'
    -- example for user account: exec sp_changedbowner 'sqlrepro\administrator' 
    ```

8. **로그 판독기 에이전트**를 다시 시작해야 합니다. 이렇게 하려면 **개체 탐색기**에서 **SQL Server 에이전트** 노드를 확장하고 **작업 활동 모니터**를 엽니다. **범주**로 정렬하고 **'REPL-LogReader'** 범주를 사용하여 **로그 판독기 에이전트**를 확인합니다. **로그 판독기 에이전트** 작업과 **작업 시작 단계**를 마우스 오른쪽 단추로 클릭합니다. 

    ![로그 판독기 에이전트 다시 시작](media/tutorial-replicating-data-between-continuously-connected-servers/startjobatstep.png)

9. **복제 모니터**를 다시 열어 게시가 동기화되고 있는지 확인합니다. 아직 열려 있지 않은 경우 **개체 탐색기**에서 **복제**를 마우스 오른쪽 단추로 클릭하여 찾을 수 있습니다. 
10. **AdvWorksProductTrans** 게시, **에이전트** 탭을 차례로 선택하고 **로그 판독기 에이전트**를 두 번 선택하여 에이전트 기록을 엽니다. 이제 **로그 판독기 에이전트**가 실행 중이며 명령을 복제하고 있다는 메시지 또는 "복제된 트랜잭션 없음"이라는 메시지가 나타납니다.

    ![로그 판독기 실행](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderrunning.png)

### <a name="troubleshoot-errors-with-distribution-agent"></a>배포 에이전트를 사용하여 오류 해결
**배포 에이전트**는 **배포** 데이터베이스에서 찾은 데이터를 가져와서 구독자에 적용합니다. 

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하여 서버 노드를 확장하고 **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **복제 모니터 시작**을 선택합니다.  
2. **복제 모니터**에서 **AdvWorksProductTrans** 게시를 선택하고, **모든 구독** 탭을 선택합니다. 해당 구독과 **자세히 보기**를 오른쪽 단추로 클릭합니다.

    ![배포 세부 정보 보기](media/tutorial-replicating-data-between-continuously-connected-servers/viewdetails.png)

2. **배포자에서 구독자로 연결** 기록 대화 상자가 열리고, 에이전트에 발생한 오류에 대한 설명이 표시됩니다. 

     ![배포 에이전트 기록 오류](media/tutorial-replicating-data-between-continuously-connected-servers/disthistoryerror.png)
    
        Error messages:
        Agent 'NODE1\SQL2016-AdventureWorks2012-AdvWorksProductTrans-NODE2\SQL2016-7' is retrying after an error. 89 retries attempted. See agent job history in the Jobs folder for more details.

3. 이 오류는 **배포 에이전트**가 다시 시도 중이라는 것을 나타냅니다. 자세한 정보를 확인하려면 **개체 탐색기** > **작업 활동 모니터**에서 **SQL Server 에이전트**를 확장합니다. **범주**별로 작업을 정렬합니다. 

    1. **'REPL-Distribution'** 범주를 사용하여 **배포 에이전트**를 확인합니다. 에이전트와 **기록 보기**를 마우스 오른쪽 단추로 클릭합니다.

    ![배포 에이전트 기록 보기](media/tutorial-replicating-data-between-continuously-connected-servers/viewdistagenthistory.png)

5. 오류 항목 중 하나를 선택하고 창 아래쪽에서 오류 텍스트를 확인합니다.  

    ![배포 에이전트에 대한 잘못된 암호](media/tutorial-replicating-data-between-continuously-connected-servers/distpwwrong.png)
    
        Message:
        Unable to start execution of step 2 (reason: Error authenticating proxy NODE1\repl_distribution, system error: The user name or password is incorrect.)

6. 이 오류는 **배포 에이전트**에서 사용하는 암호가 잘못되었음을 나타냅니다. 이 문제를 해결하려면 **개체 탐색기**에서 **복제** 노드를 확장하고, 구독>**속성**을 마우스 오른쪽 단추로 클릭합니다. **에이전트 프로세스 계정** 옆에 있는 줄임표(...)를 선택하고 암호를 수정합니다.

    ![배포 에이전트의 암호 수정](media/tutorial-replicating-data-between-continuously-connected-servers/distagentpwchange.png)

7. **복제 모니터**를 다시 확인합니다. **개체 탐색기**에서 **복제**를 마우스 오른쪽 단추로 클릭하면 찾을 수 있습니다. **모든 구독**에 있는 빨간색 X는 **배포 에이전트**에 여전히 오류가 있음을 나타냅니다. **복제 모니터** > **세부 정보 보기**에서 구독을 마우스 오른쪽 단추로 클릭하여 **구독자에게 배포** 기록을 엽니다. 이제 여기에는 오류가 다르게 표시됩니다. 

    ![배포 에이전트가 연결할 수 없음](media/tutorial-replicating-data-between-continuously-connected-servers/distagentcantconnect.png)
           
        Connecting to Subscriber 'NODE2\SQL2016'        
        Agent message code 20084. The process could not connect to Subscriber 'NODE2\SQL2016'.
        Number:  18456
        Message: Login failed for user 'NODE2\repl_distribution'.

8. 이 오류는 사용자 **NODE2\repl_distribution**의 로그인이 실패했으므로 **배포 에이전트**가 구독자에게 연결할 수 없음을 나타냅니다.  더 자세히 조사하려면 구독자에 연결하고 **개체 탐색기**의 **관리** 노드에 있는 *현재***SQL 오류 로그**를 엽니다. 

    ![구독자 로그인 실패](media/tutorial-replicating-data-between-continuously-connected-servers/loginfailed.png) 이 오류가 표시되는 경우, 구독자에 로그인이 누락된 것입니다. 이 문제를 해결하려면 [구독자에서 데이터베이스 권한 설정](#setting-database-permissions-at-the-subscriber)을 참조하세요.

9. 로그인 오류가 해결되었으면 **복제 모니터**를 다시 확인합니다. 모든 문제가 해결되었으면 **모든 구독**에서 **게시 이름** 옆에 녹색 화살표가 표시되고 **실행 중** 상태가 표시됩니다. **구독**을 마우스 오른쪽 단추로 클릭하여 **배포자에서 구독자로 연결** 기록을 한 번 더 실행함으로써 성공을 확인합니다. 배포 에이전트를 처음 실행하는 경우, 아래 그림과 같이 스냅숏이 구독자에게 대량 복사되었음을 알 수 있습니다. 

     ![배포 에이전트 성공](media/tutorial-replicating-data-between-continuously-connected-servers/distagentsuccess.png)   

  ## <a name="next-steps"></a>다음 단계
트랜잭션 복제를 위해 게시자와 구독자를 모두 성공적으로 구성했습니다.  이제 게시자의 **제품** 테이블에서 데이터를 삽입, 업데이트 또는 삭제할 수 있습니다. 그런 다음, 구독자에서 **제품** 테이블을 쿼리하여 복제된 변경 내용을 볼 수 있습니다. 다음 아티클에서는 병합 복제를 구성하는 방법을 설명합니다.  

자세히 알아보려면 다음 문서로 진행합니다.
> [!div class="nextstepaction"]
> [다음 단계](tutorial-replicating-data-with-mobile-clients.md)

  
