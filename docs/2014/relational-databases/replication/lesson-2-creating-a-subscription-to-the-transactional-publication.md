---
title: '2단원: 트랜잭션 게시에 구독 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d3e8b5f0be58d9153fbe4d0ffd0287ea753fcc5e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721079"
---
# <a name="lesson-2-creating-a-subscription-to-the-transactional-publication"></a>2단원: 트랜잭션 게시에 구독 만들기
  이 단원에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 구독을 만듭니다. 이 단원에서는 이전 단원을 완료 해야 [1 단원: 트랜잭션 복제를 사용 하 여 데이터 게시](lesson-1-publishing-data-using-transactional-replication.md)합니다.  
  
### <a name="to-create-the-subscription"></a>구독을 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  **로컬 게시** 폴더에서 **AdvWorksProductTrans** 게시를 마우스 오른쪽 단추로 클릭한 다음 **새 구독**을 클릭합니다.  
  
     새 구독 마법사가 시작됩니다.  
  
3.  게시 페이지에서 **AdvWorksProductTrans**를 선택한 후 **다음**을 클릭합니다.  
  
4.  배포 에이전트 위치 페이지에서 **배포자에서 모든 에이전트 실행**을 선택한 후 **다음**을 클릭합니다.  
  
5.  구독자 페이지에서 구독자 인스턴스 이름이 표시되지 않는 경우 **구독자 추가**, **SQL Server 구독자 추가**를 차례로 클릭하고 **서버에 연결** 대화 상자에 구독자 인스턴스 이름을 입력한 다음 **연결**을 클릭합니다.  
  
6.  구독자 페이지에서 구독자 서버의 인스턴스 이름을 선택 하 고 선택  **\<새 데이터베이스 >** 아래 **구독 데이터베이스**합니다.  
  
7.  **새 데이터베이스** 대화 상자에서 **데이터베이스 이름** 상자에 **ProductReplica** 를 입력하고 **확인**을 클릭한 후 **다음**을 클릭합니다.  
  
8.  에 **배포 에이전트 보안** 대화 상자에서 줄임표 (**...** ) 단추를 입력 합니다 \< _Machine_Name >_**\repl_distribution** 에 **프로세스 계정** 상자에서이 대 한 암호를 입력 합니다. 계정, 클릭 **확인**를 클릭 하 고 **다음**합니다.  
  
9. **마침** 을 클릭하여 나머지 페이지의 기본값을 적용하고 마법사를 완료합니다.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>구독자에서 데이터베이스 권한 설정  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결하고 **데이터베이스**, **ProductReplica**및 **보안**을 확장하고 **사용자**를 마우스 오른쪽 단추로 클릭한 다음 **새 사용자**를 선택합니다.  
  
2.  **일반** 페이지에 있는 **사용자 유형** 목록에서 **Windows 사용자**를 선택합니다.  
  
3.  선택 합니다 **사용자 이름** 상자 하 고 줄임표 (...) 단추를 클릭 합니다 **선택할 개체 이름을 입력** < Machine_Name > 상자**\repl_distribution**, 를클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  
  
4.  **멤버 자격** 페이지의 **데이터베이스 역할 멤버 자격** 영역에서 **db_owner**를 선택한 다음 **확인** 을 클릭하여 사용자를 만듭니다.  
  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>구독의 동기화 상태를 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  **로컬 게시** 폴더에서 **AdvWorksProductTrans** 게시를 확장하고 **ProductReplica** 데이터베이스의 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 상태 보기**를 클릭합니다.  
  
     구독의 현재 동기화 상태가 표시됩니다.  
  
3.  **AdvWorksProductTrans**에 해당 구독이 표시되지 않으면 F5 키를 눌러 목록을 새로 고칩니다.  
  
## <a name="next-steps"></a>다음 단계  
 트랜잭션 게시에 구독을 성공적으로 만들었습니다. 이 구독에 대한 배포 에이전트가 계속 실행되므로 구독은 생성될 때 초기화됩니다. 다음 단원에서는 추적 프로그램 토큰을 사용하여 변경 내용이 구독자에 복제되었는지 여부 및 대기 시간을 확인합니다. [3단원: 구독 유효성 검사 및 대기 시간 측정](lesson-3-validating-the-subscription-and-measuring-latency.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [스냅숏으로 구독 초기화](initialize-a-subscription-with-a-snapshot.md)   
 [ssSDSFull](create-a-push-subscription.md)   
 [게시 구독](subscribe-to-publications.md)  
  
  
