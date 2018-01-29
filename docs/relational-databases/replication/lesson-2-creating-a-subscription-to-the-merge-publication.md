---
title: "2단원: 병합 게시에 대한 구독 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 06722baa-9065-443e-b1d5-99036cf89074
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1fb890bc73be0a4d27c5ea9cafe1e2fbed930679
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="lesson-2-creating-a-subscription-to-the-merge-publication"></a>2단원: 병합 게시에 대한 구독 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 단원에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 구독을 만듭니다. 그런 다음 구독 데이터베이스에 대한 사용 권한을 설정하고 새 구독에 대한 필터링된 데이터 스냅숏을 수동으로 생성합니다. 이 단원을 수행하려면 이전 단원인 [1단원: 병합 복제를 사용하여 데이터 게시](../../relational-databases/replication/lesson-1-publishing-data-using-merge-replication.md)를 완료해야 합니다.  
  
### <a name="to-create-the-subscription"></a>구독을 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결하여 해당 서버 노드와 **복제** 폴더를 확장하고 **로컬 구독** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 구독**을 클릭합니다.  
  
    새 구독 마법사가 시작됩니다.  
  
2.  **게시** 페이지에서 **게시자** 목록에 있는 **SQL Server 게시자 찾기** 를 클릭합니다.  
  
3.  **서버에 연결** 대화 상자에서 **서버 이름** 상자에 게시자 인스턴스의 이름을 입력하고 **연결**을 클릭합니다.  
  
4.  **AdvWorksSalesOrdersMerge**를 클릭하고 **다음**을 클릭합니다.  
  
5.  병합 에이전트 위치 페이지에서 **각 에이전트를 해당 구독자에서 실행**을 클릭한 후 **다음**을 클릭합니다.  
  
6.  구독자 페이지에서 구독자 서버의 인스턴스 이름을 선택하고 **구독 데이터베이스**의 목록에서 **<New Database>** 를 선택합니다.  
  
7.  **새 데이터베이스** 대화 상자에서 **데이터베이스 이름** 상자에 **SalesOrdersReplica** 를 입력하고 **확인**을 클릭한 후 **다음**을 클릭합니다.  
  
8.  병합 에이전트 보안 페이지에서 줄임표 단추(**…**)를 클릭하고 **프로세스 계정** 상자에 \<*Machine_Name>***\repl_merge**를 입력한 다음 해당 계정의 암호를 입력하고 **확인**, **다음**, **다음**을 차례로 클릭합니다.  
  
9. 구독 초기화 페이지의 **초기화 시기** 목록에서 **첫 번째 동기화 시** 를 선택하고 **다음**을 클릭한 후 다시 **다음** 을 클릭합니다.  
  
10. HOST_NAME 값 페이지에서 **HOST_NAME 값** 상자에 값 **adventure-works\pamela0** 을 입력한 다음 **마침**을 클릭합니다.  
  
11. **마침** 을 다시 클릭하고 구독이 생성되면 **닫기**를 클릭합니다.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>구독자에서 데이터베이스 권한 설정  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결하고 **데이터베이스**, **SalesOrdersReplica**및 **보안**을 확장하고 **사용자**를 마우스 오른쪽 단추로 클릭한 다음 **새 사용자**를 선택합니다.  
  
2.  **일반** 페이지에서 **사용자 이름** 상자에 \<*Machine_Name>***\repl_merge**를 입력하고 줄임표 단추(**…**)와 **찾아보기**를 차례로 클릭한 다음 \<*Machine_Name>***\repl_merge**를 선택하고 **확인**, **이름 확인**, **확인**을 차례로 클릭합니다.  
  
3.  **데이터베이스 역할 멤버 자격**에서 **db_owner**를 선택한 다음 **확인** 을 클릭하여 사용자를 만듭니다.  
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>구독에 대한 필터링된 데이터 스냅숏을 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  **로컬 게시** 폴더에서 **AdvWorksSalesOrdersMerge** 게시를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
    **게시 속성** 대화 상자가 표시됩니다.  
  
3.  **데이터 파티션** 페이지를 선택한 다음 **추가**를 클릭합니다.  
  
4.  **데이터 파티션 추가** 대화 상자의 **HOST_NAME 값** 상자에 **adventure-works\pamela0** 을 입력한 다음 **확인**을 클릭합니다.  
  
5.  새로 추가된 파티션을 선택하고 **선택한 스냅숏 지금 생성**을 클릭한 다음 **확인**을 클릭합니다.  
  
## <a name="next-steps"></a>Next Steps  
구독이 초기화되면 사용할 수 있도록 병합 게시에 대한 구독을 만들고 새 구독의 데이터 파티션에 대한 필터링된 스냅숏을 생성했습니다. 다음 단원에서는 병합 에이전트에 구독 데이터베이스에 대한 권한을 부여하고 병합 에이전트를 실행하여 동기화를 시작하고 구독을 초기화합니다. [3단원: 병합 게시에 구독 동기화](../../relational-databases/replication/lesson-3-synchronizing-the-subscription-to-the-merge-publication.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
[끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)  
[매개 변수가 있는 필터를 사용하는 병합 게시의 스냅숏](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
