---
title: '1단원: 트랜잭션 복제를 사용 하 여 데이터 게시 | Microsoft Docs'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 9c55aa3c-4664-41fc-943f-e817c31aad5e
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 8267f70049d0ef37c0ce80bc594dff25d53f15fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721087"
---
# <a name="lesson-1-publishing-data-using-transactional-replication"></a>1단원: 트랜잭션 복제를 사용 하 여 데이터 게시
  이 단원에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 트랜잭션 게시를 만들어 **샘플 데이터베이스에** Product [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 테이블의 필터링된 하위 집합을 게시합니다. 또한 배포 에이전트에 사용된 SQL Server 로그인을 PAL(게시 액세스 목록)에 추가합니다. 이 자습서를 시작하려면 이전 자습서인 [복제용 서버 준비](tutorial-preparing-the-server-for-replication.md)를 완료해야 합니다.  
  
### <a name="to-create-a-publication-and-define-articles"></a>게시를 만들고 아티클을 정의하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장하고 **로컬 게시** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 게시**를 클릭합니다.  
  
     게시 구성 마법사가 시작됩니다.  
  
3.  게시 데이터베이스 페이지에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 선택하고 **다음**을 클릭합니다.  
  
4.  게시 유형 페이지에서 **트랜잭션 게시**를 선택하고 **다음**을 클릭합니다.  
  
5.  아티클 페이지에서 **테이블** 노드를 확장하고 **Product** 확인란을 선택한 다음 **Product** 를 확장하고 **ListPrice** 및 **StandardCost** 확인란의 선택을 취소합니다. **다음**을 클릭합니다.  
  
6.  테이블 행 필터 페이지에서 **추가**를 클릭합니다.  
  
7.  **필터 추가** 대화 상자에서 **SafetyStockLevel** 열을 클릭하고 오른쪽 화살표를 클릭하여 필터 쿼리의 필터 문 WHERE 절에 해당 열을 추가한 후 WHERE 절을 다음과 같이 수정합니다.  
  
    ```  
    WHERE [SafetyStockLevel] < 500  
    ```  
  
8.  **확인**, **다음**을 차례로 클릭합니다.  
  
9. **즉시 스냅숏을 만들고 구독 초기화에 사용할 수 있도록 유지합니다.** 확인란을 선택하고 **다음**을 클릭합니다.  
  
10. 에이전트 보안 페이지에서 **스냅숏 에이전트의 보안 설정 사용** 확인란을 선택 취소합니다.  
  
11. 스냅숏 에이전트에 대해 **보안 설정**을 클릭하고 **프로세스 계정** 상자에 \<_Machine_Name>_**\repl_snapshot**을 입력한 다음 이 계정에 대한 암호를 입력하고 **확인**을 클릭합니다.  
  
12. 이전 단계를 반복하여 repl_logreader를 로그 판독기 에이전트에 대한 프로세스 계정으로 설정한 다음 **마침**을 클릭합니다.  
  
13. 마법사 완료 페이지에서 **게시 이름** 상자에 **AdvWorksProductTrans** 를 입력하고 **마침**을 클릭합니다.  
  
14. 게시를 만든 후 **닫기** 를 클릭하여 마법사를 완료합니다.  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>스냅숏 생성의 상태를 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  **로컬 게시** 폴더에서 **AdvWorksProductTrans**를 마우스 오른쪽 단추로 클릭한 다음 **스냅숏 에이전트 상태 보기**를 클릭합니다.  
  
3.  게시에 대한 스냅숏 에이전트 작업의 현재 상태가 표시됩니다. 다음 단원을 진행하기 전에 스냅숏 작업이 성공했는지 확인합니다.  
  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>PAL에 배포 에이전트 로그인을 추가하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  **로컬 게시** 폴더에서 **AdvWorksProductTrans**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
     **게시 속성** 대화 상자가 표시됩니다.  
  
3.  **게시 액세스 목록** 페이지를 선택하고 **추가**를 클릭합니다.  
  
4.  **게시 액세스 추가** 대화 상자에서 _<Machine_Name>_**\repl_distribution**을 선택한 다음 **확인**을 클릭합니다. **확인**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
 트랜잭션 게시를 성공적으로 만들었습니다. 다음 단원에서는 이 게시를 구독합니다. [2단원: 트랜잭션 게시에 구독을 만드는](lesson-2-creating-a-subscription-to-the-transactional-publication.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [게시된 데이터 필터링](publish/filter-published-data.md)   
 [Define an Article](publish/define-an-article.md)   
 [스냅숏 만들기 및 적용](create-and-apply-the-snapshot.md)  
  
  
