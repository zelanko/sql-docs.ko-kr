---
title: '자습서: 두 개의 완전히 연결된 서버 간 복제 구성(트랜잭션) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
ms.openlocfilehash: 9d8c3441f219017125b755b498a534317a1fca01
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34550484"
---
# <a name="tutorial-configure-replication-between-two-fully-connected-servers-transactional"></a>자습서: 두 개의 완전히 연결된 서버 간 복제 구성(트랜잭션)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
트랜잭션 복제는 계속 연결되는 서버 간에 데이터를 이동할 때 발생하는 문제를 해결하는 좋은 방법입니다. 복제 마법사를 사용하면 복제 토폴로지를 쉽게 구성하고 관리할 수 있습니다. 

이 자습서에서는 계속 연결되는 서버에 대해 트랜잭션 복제 토폴로지를 구성하는 방법을 보여줍니다. 트랜잭션 복제가 작동하는 방법에 대한 자세한 내용은 [트랜잭션 복제 개요](https://docs.microsoft.com/en-us/sql/relational-databases/replication/transactional/transactional-replication)를 참조하세요. 
  
## <a name="what-you-will-learn"></a>학습 내용  
이 자습서에서는 트랜잭션 복제를 사용하여 한 데이터베이스의 데이터를 다른 데이터베이스에 게시하는 방법을 보여 줍니다. 

이 자습서에서는 다음 작업 방법을 배웁니다.
> [!div class="checklist"]
> * 트랜잭션 복제를 통해 게시자를 만듭니다.
> * 트랜잭션 게시자에 대한 구독자를 만듭니다.
> * 구독 유효성을 검사하고 및 대기 시간을 측정합니다.
  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 자습서는 기본적인 데이터베이스 작업에는 익숙하지만 복제에 대한 경험은 풍부하지 않은 사용자를 위한 것입니다. 이 자습서를 시작하기 전에 [자습서: 복제용 SQL 서버 준비](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)를 완료해야 합니다.  
  
이 자습서를 완료하려면 SQL Server, SSMS(SQL Server Management Studio) 및 AdventureWorks 데이터베이스가 필요합니다.  
  
- 게시자 서버(원본)에서 설치합니다.  
  
   - SQL Server Express 또는 SQL Server Compact를 제외한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전. 이들 버전은 복제 게시자가 될 수 없습니다.   
   - [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 예제 데이터베이스. 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다.  
  
- 구독자 서버(대상)에서 [!INCLUDE[ssEW](../../includes/ssew-md.md)]을 제외한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 모든 버전을 설치합니다. [!INCLUDE[ssEW](../../includes/ssew-md.md)]는 트랜잭션 복제에서 구독자가 될 수 없습니다.  
  
- [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)을 설치합니다.
- [AdventureWorks 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)를 다운로드합니다. SSMS에서 데이터베이스를 복원하는 방법에 대한 지침은 [데이터베이스 복원](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)을 참조하세요. 
 
>[!NOTE]
> - 두 버전이 넘게 차이 나는 SQL Server 인스턴스에서는 복제가 지원되지 않습니다. 자세한 내용은 [복제 토폴로지에서 지원되는 SQL Server 버전](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/)을 참조하세요.
> - [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 **sysadmin** 고정 서버 역할의 멤버인 로그인을 사용하여 게시자 및 구독자에 연결해야 합니다. 이 역할에 대한 자세한 내용은 [서버 수준 역할](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles)을 참조하세요.  
  
  
**이 자습서를 완료하는 데 소요되는 예상 시간: 60분**  
  
## <a name="configure-the-publisher-for-transactional-replication"></a>트랜잭션 복제를 위한 게시자 구성
이 섹션에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 트랜잭션 게시를 만들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 샘플 데이터베이스에 **Product** 테이블의 필터링된 하위 집합을 게시합니다. 또한 배포 에이전트에 사용된 SQL Server 로그인을 PAL(게시 액세스 목록)에 추가합니다.


### <a name="create-a-publication-and-define-articles"></a>게시 만들기 및 아티클 정의
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음, 해당 서버 노드를 확장합니다.  
  
2. **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭한 다음, **시작**을 선택합니다. SQL Server 에이전트는 게시를 만들기 전에 실행되어야 합니다. 이 단계에서 에이전트를 시작하지 않으면 SQL Server 구성 관리자에서 수동으로 시작해야 합니다. 
3. **복제** 폴더를 확장하고 **로컬 게시** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **새 게시**를 선택합니다. 이 단계에서 새 게시 마법사가 시작합니다.  

   ![새 게시 마법사를 시작하기 위한 선택 항목](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
  
3. **게시 데이터베이스** 페이지에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 선택한 후, **다음**을 선택합니다.  
  
4. **게시 유형** 페이지에서 **트랜잭션 게시**를 선택한 후, **다음**을 선택합니다.  

   ![선택된 게시 유형이 있는 "게시 유형" 페이지](media/tutorial-replicating-data-between-continuously-connected-servers/tranrepl.png)
  
5. **문서** 페이지에서 **테이블** 노드를 확장하고 **제품** 확인란을 선택합니다. 그런 다음, **제품**을 확장하고 **ListPrice** 및 **StandardCost** 옆에 있는 확인란의 선택을 취소합니다. **다음**을 선택합니다.  

   ![선택된 게시할 문서가 있는 "문서" 페이지](media/tutorial-replicating-data-between-continuously-connected-servers/replarticles.png)
  
6. **테이블 행 필터링** 페이지에서 **추가**를 선택합니다.   
  
7. **필터 추가** 대화 상자에서 **SafetyStockLevel** 열을 선택합니다. 오른쪽 화살표를 선택하여 필터 쿼리의 필터 문 WHERE 절에 해당 열을 추가합니다. 그런 다음, WHERE 절 한정자에 수동으로 다음과 같이 입력합니다.  
  
   ```sql  
   WHERE [SafetyStockLevel] < 500  
   ```
  
   !["테이블 흐름 필터링" 페이지 및 "필터 추가" 대화 상자](media/tutorial-replicating-data-between-continuously-connected-servers/filter.png)
  
8. **확인**선택하고 **다음**을 선택합니다.  
  
9. **즉시 스냅숏을 만들고 구독 초기화에 사용할 수 있도록 유지** 확인란을 선택하고 **다음**을 선택합니다.  

   ![확인란이 선택된 "스냅숏 에이전트" 페이지](media/tutorial-replicating-data-between-continuously-connected-servers/snapshot.png)
  
10. **에이전트 보안** 페이지에서 **스냅숏 에이전트의 보안 설정 사용** 확인란을 선택 취소합니다.   
  
    스냅숏 에이전트에 대한 **보안 설정**을 선택합니다. **프로세스 계정** 상자에 <*Publisher_Machine_Name*>**\repl_snapshot**을 입력하고, 이 계정에 대한 암호를 입력한 다음, **확인**을 선택합니다.  

    !["에이전트 보안" 페이지 및 "스냅숏 에이전트 보안" 대화 상자](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagentsecurity.png)
  
12. 이전 단계를 반복하여 <*Publisher_Machine_Name*>**\repl_logreader**를 로그 판독기 에이전트에 대한 프로세스 계정으로 설정합니다. 그런 다음, **확인**을 선택합니다.  

    ![“로그 판독기 에이전트 보안” 대화 상자 및 “에이전트 보안” 페이지](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentsecurity.png)   

  
13. **마법사 완료** 페이지에서 **게시 이름** 상자에 **AdvWorksProductTrans**를 입력하고 **마침**을 선택합니다.  

    ![게시 이름이 있는 "마법사 완료" 페이지](media/tutorial-replicating-data-between-continuously-connected-servers/advworksproducttrans.png)
  
14. 게시를 만든 후 **닫기** 를 선택하여 마법사를 완료합니다. 

게시를 만들려고 할 때 SQL Server 에이전트가 실행되고 있지 않은 경우 다음과 같은 오류가 발생할 수 있습니다. 이 오류는 게시가 성공적으로 만들어졌지만 스냅숏 에이전트를 시작하지 못했음을 나타냅니다. 이러한 경우 SQL Server 에이전트를 시작한 다음, 스냅숏 에이전트를 수동으로 시작해야 합니다. 다음 섹션에서 지침을 제공합니다. 

![스냅숏 에이전트가 시작하지 못했음을 나타내는 경고](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenterror.png)
    
  
### <a name="view-the-status-of-snapshot-generation"></a>스냅숏 생성의 상태 보기  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음, **복제** 폴더를 확장합니다.  
  
2. **로컬 게시** 폴더에서 **AdvWorksProductTrans**를 마우스 오른쪽 단추로 클릭한 다음, **스냅숏 에이전트 상태 보기**를 선택합니다.  
   ![스냅숏 에이전트 상태 보기를 위한 바로 가기 메뉴의 명령](media/tutorial-replicating-data-between-continuously-connected-servers/viewsnapshot.png)
  
3. 게시에 대한 스냅숏 에이전트 작업의 현재 상태가 표시됩니다. 다음 섹션을 진행하기 전에 스냅숏 작업이 성공했는지 확인합니다.
          
게시를 만들 때 SQL Server 에이전트가 실행되고 있지 않은 경우, 게시의 스냅숏 에이전트 상태를 확인하면 스냅숏 에이전트가 '실행되지 않음'으로 표시됩니다. 이 경우 **시작**을 선택하여 스냅숏 에이전트를 시작합니다. 

!["시작" 단추 및 스냅숏 에이전트가 실행되지 못했음을 표시하는 상태 메시지의 변경](media/tutorial-replicating-data-between-continuously-connected-servers/startsnapshotagent.png)
     
여기서 오류가 표시되면 [스냅숏 에이전트 오류 해결](../../troubleshooters/replication/troubleshoot-tran-repl-errors.md#find-errors-with-the-snapshot-agent)을 참조하세요. 

  
### <a name="add-the-distribution-agent-login-to-the-pal"></a>PAL에 배포 에이전트 로그인 추가  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음, **복제** 폴더를 확장합니다.  
  
2. **로컬 게시** 폴더에서 **AdvWorksProductTrans**를 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.  **게시 속성** 대화 상자가 표시됩니다.    
  
   1. **게시 액세스 목록** 페이지를 선택하고 **추가**를 선택합니다.  
   2. **게시 액세스 추가** 대화 상자에서 <*Publisher_Machine_Name*>**\repl_distribution**을 선택한 다음, **확인**을 선택합니다.
   
   ![로그인을 게시 액세스 목록에 추가하기 위한 선택 항목](media/tutorial-replicating-data-between-continuously-connected-servers/tranreplproperties.png)

자세한 내용은 [복제 프로그래밍 개념](../../relational-databases/replication/concepts/replication-programming-concepts.md)을 참조하십시오.  
  

## <a name="create-a-subscription-to-the-transactional-publication"></a>트랜잭션 게시에 구독 만들기
이 섹션에서는 이전에 만든 게시에 구독자를 추가합니다. 이 자습서에서는 원격 구독자(NODE2\SQL2016)를 사용하지만 구독을 게시자에게 로컬로 추가할 수도 있습니다. 

### <a name="create-the-subscription"></a>구독 만들기  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음, **복제** 폴더를 확장합니다.  
  
2. **로컬 게시** 폴더에서 **AdvWorksProductTrans** 게시를 마우스 오른쪽 단추로 클릭한 다음, **새 구독**을 선택합니다. 새 구독 마법사가 시작됩니다. 
 
   ![새 구독 마법사를 시작하기 위한 선택 항목](media/tutorial-replicating-data-between-continuously-connected-servers/newsub.png)     
  
3. **게시** 페이지에서 **AdvWorksProductTrans**를 선택한 후, **다음**을 선택합니다.  

   ![선택된 게시가 있는 "게시" 페이지](media/tutorial-replicating-data-between-continuously-connected-servers/selectpub.png)
  
4. **배포 에이전트 위치** 페이지에서 **배포자에서 모든 에이전트 실행**을 선택한 후, **다음**을 선택합니다.  구독 끌어오기 및 밀어넣기에 대한 자세한 내용은 [게시 구독](https://docs.microsoft.com/en-us/sql/relational-databases/replication/subscribe-to-publications)을 참조하세요.

   ![배포자에서 모든 에이전트를 실행하기 위해 선택된 옵션이 있는“배포 에이전트 위치” 페이지](media/tutorial-replicating-data-between-continuously-connected-servers/runagentsatdist.png)
  
5. **구독자 페이지**에서 구독자 인스턴스 이름이 표시되지 않는 경우 **구독자 추가**를 선택한 다음, 드롭다운 목록에서 **SQL Server 구독자** 추가를 선택합니다. 이 단계는 **서버에 연결** 대화 상자를 엽니다. 구독자 인스턴스 이름을 입력한 다음, **연결**을 선택합니다.  
    
   구독자가 추가된 후 구독자의 인스턴스 이름 옆에 있는 확인 상자를 선택합니다. 그런 다음, **구독 데이터베이스**에서 **새 데이터베이스**를 선택합니다.   

   ![구독자 서버를 추가 하기 위한 선택 항목이 있는 "구독자" 페이지](media/tutorial-replicating-data-between-continuously-connected-servers/addsub.png)

7. **새 데이터베이스** 대화 상자가 나타납니다. **데이터베이스 이름** 상자에 **ProductReplica**를 입력하고 **확인**을 선택한 후, **다음**을 선택합니다. 
  
   ![구독 데이터베이스에 대한 이름 입력하기](media/tutorial-replicating-data-between-continuously-connected-servers/productreplica.png)
  
8. **배포 에이전트 보안** 페이지에서 줄임표(**...**) 단추를 선택합니다. **프로세스 계정** 상자에 <*Publisher_Machine_Name*>**\repl_distribution**을 입력하고 이 계정의 암호를 입력한 다음, **확인**, **다음**을 차례로 선택합니다.

   ![“배포 에이전트 보안” 대화 상자의 배포 계정 정보](media/tutorial-replicating-data-between-continuously-connected-servers/adddistaccount.png)
  
9. **마침**을 선택하여 나머지 페이지에 기본값을 적용하고 마법사를 완료합니다.  
  
### <a name="set-database-permissions-at-the-subscriber"></a>구독자에서 데이터베이스 권한 설정  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결합니다. **보안**을 확장하고, **로그인**을 마우스 오른쪽 단추로 클릭한 다음, **새 로그인**을 선택합니다.     
  
   1. **일반** 페이지의 **로그인 이름**에서 **검색**을 선택하고 <*Subscriber_Machine_Name*>**\repl_distribution**에 대한 로그인을 추가합니다.

   2. **사용자 매핑** 페이지에서 **ProductReplica** 데이터베이스에 대한 로그인 **db_owner** 멤버 자격을 부여합니다. 

   ![구독자에서 로그인을 구성하기 위한 선택 항목](media/tutorial-replicating-data-between-continuously-connected-servers/loginforsub.png)

2. **확인**을 선택하여 **새 로그인** 대화 상자를 닫습니다. 

  
### <a name="view-the-synchronization-status-of-the-subscription"></a>구독의 동기화 상태 보기  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결합니다. 서버 노드를 확장한 다음, **복제** 폴더를 확장합니다.  
  
2. **로컬 게시** 폴더에서 **AdvWorksProductTrans** 게시를 확장하고 **ProductReplica** 데이터베이스의 구독을 마우스 오른쪽 단추로 클릭한 다음, **동기화 상태 보기**를 선택합니다. 구독의 현재 동기화 상태가 표시됩니다.

   ![“동기화 상태 보기” 대화 상자를 열기 위한 선택 항목](media/tutorial-replicating-data-between-continuously-connected-servers/viewsyncstatus.png)
3. **AdvWorksProductTrans**에 해당 구독이 표시되지 않으면 F5 키를 선택하여 목록을 새로 고칩니다.  
  
참조 항목:  
- [스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
- [밀어넣기 구독 만들기](../../relational-databases/replication/create-a-push-subscription.md)  
- [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  

## <a name="measure-replication-latency"></a>복제 대기 시간 측정
이 섹션에서는 추적 프로그램 토큰을 사용하여 변경 내용이 구독자에 복제되었는지 여부 및 대기 시간을 확인합니다. 대기 시간은 게시자에서 변경한 내용이 구독자에게 표시되는 데 걸리는 시간입니다.
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결합니다. 서버 노드를 확장하고 **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **복제 모니터 시작**을 선택합니다.

   ![바로 가기 메뉴에서 "복제 모니터 시작" 명령](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)

2. 왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자 인스턴스를 확장한 다음, **AdvWorksProductTrans** 게시를 선택합니다.  
  
   1. **추적 프로그램 토큰** 탭을 선택합니다.  
   2. **추적 프로그램 삽입**을 선택합니다.    
   c. **게시자에서 배포자로 연결 시 대기 시간**, **배포자에서 구독자로 연결 시 대기 시간**, **총 대기 시간**열에서 추적 프로그램 토큰에 대한 경과 시간을 확인합니다. **보류 중**이라는 값은 토큰이 지정된 지점에 아직 도달하지 않았음을 나타냅니다.

   ![추적 프로그램 토큰에 대한 정보](media/tutorial-replicating-data-between-continuously-connected-servers/tracertoken.png)


참조 항목: 
- [트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)
- [트랜잭션 복제 동기화 오류 해결](../../troubleshooters/replication/troubleshoot-tran-repl-errors.md)


## <a name="next-steps"></a>다음 단계
트랜잭션 복제를 위해 게시자와 구독자를 모두 성공적으로 구성했습니다. 이제 게시자의 **제품** 테이블에서 데이터를 삽입, 업데이트 또는 삭제할 수 있습니다. 그런 다음, 구독자에서 **제품** 테이블을 쿼리하여 복제된 변경 내용을 볼 수 있습니다. 

다음 문서에서는 병합 복제를 구성하는 방법을 설명합니다.  

> [!div class="nextstepaction"]
> [자습서: 서버와 모바일 클라이언트 간의 복제 구성(병합)](tutorial-replicating-data-with-mobile-clients.md)

  
