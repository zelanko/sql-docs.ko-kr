---
title: '1단원: 병합 복제를 사용하여 데이터 게시 | Microsoft 문서'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: c3c6e0b6-54cd-4b7d-8efb-2cefe14fcd7f
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: a1f2e84ca089699eb0ad980cdce93ca26e9df499
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251805"
---
# <a name="lesson-1-publishing-data-using-merge-replication"></a>1단원: 병합 복제를 사용하여 데이터 게시
  이 단원에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 병합 게시를 만들어 **샘플 데이터베이스에**Employee **,** SalesOrderHeader **및** SalesOrderDetail [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 테이블의 하위 집합을 게시합니다. 이러한 테이블은 각 구독에 고유한 데이터 파티션이 포함되도록 매개 변수가 있는 행 필터로 필터링됩니다. 또한 병합 에이전트에 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 PAL(게시 액세스 목록)에 추가합니다. 이 자습서를 사용하려면 이전 자습서인 [복제용 서버 준비](tutorial-preparing-the-server-for-replication.md)를 완료해야 합니다.  
  
### <a name="to-create-a-publication-and-define-articles"></a>게시를 만들고 아티클을 정의하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장하고 **로컬 게시**를 마우스 오른쪽 단추로 클릭한 다음 **새 게시**를 클릭합니다.  
  
     게시 구성 마법사가 시작됩니다.  
  
3.  게시 데이터베이스 페이지에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 선택하고 **다음**을 클릭합니다.  
  
4.  게시 유형 페이지에서 **병합 게시**를 선택하고 **다음**을 클릭합니다.  
  
5.  구독자 유형 페이지에서 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전만 선택되어 있는지 확인한 후 **다음**을 클릭합니다.  
  
6.  아티클 페이지에서 **테이블** 노드를 확장하고 **SalesOrderHeader** 와 **SalesOrderDetail**을 선택한 다음 **Employee**를 확장하고 **EmployeeID** 또는 **LoginID**를 선택한 후 **다음**을 클릭합니다.  
  
    > [!TIP]  
    >  필요한 추가 열은 자동으로 선택됩니다. 자동으로 선택된 열 중 하나를 선택하고 **게시할 개체** 목록 아래의 정보에서 열이 필요한 이유에 대한 설명을 봅니다.  
  
7.  테이블 행 필터 페이지에서 **추가** 를 클릭한 다음 **필터 추가**를 클릭합니다.  
  
8.  **필터 추가** 대화 상자의 **필터링할 테이블을 선택하십시오.** 에서 **Employee(HumanResources)** 를 선택하고 **LoginID** 열을 클릭한 다음 오른쪽 화살표를 클릭하여 해당 열을 필터 쿼리의 WHERE 절에 추가하고 WHERE 절을 다음과 같이 수정합니다.  
  
    ```  
    WHERE [LoginID] = HOST_NAME()  
    ```  
  
9. **이 테이블의 행을 단일 구독으로 이동**을 클릭하고 **확인**을 클릭합니다.  
  
10. **테이블 행 필터** 페이지에서 **Employee(Human Resources)** 를 클릭하고 **추가** 를 클릭한 다음 **선택한 필터 확장을 위해 조인 추가**를 클릭합니다.  
  
11. **조인 추가** 대화 상자의 **조인된 테이블** 에서 **Sales.SalesOrderHeader**를 선택하고 **조인 문 직접 작성**을 클릭한 후 다음과 같이 조인 문을 완성합니다.  
  
    ```  
    ON Employee.EmployeeID = SalesOrderHeader.SalesPersonID  
    ```  
  
12. **조인 옵션을 지정하십시오.** 에서 **고유 키**를 선택한 다음 **확인**을 클릭합니다.  
  
13. 테이블 행 필터 페이지에서 **SalesOrderHeader**를 클릭하고 **추가**를 클릭한 다음 **선택한 필터 확장을 위해 조인 추가**를 클릭합니다.  
  
14. **조인 추가** 대화 상자의 **조인된 테이블** 에서 **Sales.SalesOrderDetail**을 선택합니다.  
  
15. **조인 문 직접 작성**을 클릭합니다.  
  
16. **필터링된 테이블 열**에서 **BusinessEntityID**를 선택한 다음 화살표 단추를 클릭하여 열 이름을 조인 문에 추가합니다.  
  
17. **조인 문** 상자에서 다음과 같이 조인 문을 작성합니다.  
  
    ```  
    ON Employee.BusinessEntityID = SalesOrderHeader.SalesPersonID  
    ```  
  
18. **조인 옵션을 지정하십시오.** 에서 **고유 키**를 선택한 다음 **확인**을 클릭합니다.  
  
19. **테이블 행 필터** 페이지에서 **SalesOrderHeader(Sales)** 를 클릭하고 **추가**를 클릭한 다음 **선택한 필터 확장을 위해 조인 추가**를 클릭합니다.  
  
20. **조인 추가** 대화 상자의 **조인된 테이블** 에서 **Sales.SalesOrderDetail**을 선택한 다음 **확인**, **다음**을 차례로 클릭합니다.  
  
21. **즉시 스냅숏 만들기**를 선택하고 **스냅숏 에이전트 실행 시간 예약**을 선택 취소한 후 **다음**을 클릭합니다.  
  
22. 에이전트 보안 페이지에서 **보안 설정**을 클릭하고 **프로세스 계정** 상자에 \<*Machine_Name>***\repl_snapshot**을 입력한 다음 이 계정에 대한 암호를 입력하고 **확인**을 클릭합니다. **마침**을 클릭합니다.  
  
23. 마법사 완료 페이지에서 **게시 이름** 상자에 **AdvWorksSalesOrdersMerge** 를 입력하고 **마침**을 클릭합니다.  
  
24. 게시를 만든 후 **닫기**를 클릭합니다.  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>스냅숏 생성의 상태를 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  로컬 게시 폴더에서 **AdvWorksSalesOrdersMerge**를 마우스 오른쪽 단추로 클릭한 다음 **스냅숏 에이전트 상태 보기**를 클릭합니다.  
  
3.  게시에 대한 스냅숏 에이전트 작업의 현재 상태가 표시됩니다. 다음 단원을 진행하기 전에 스냅숏 작업이 성공했는지 확인합니다.  
  
### <a name="to-add-the-merge-agent-login-to-the-pal"></a>PAL에 병합 에이전트 로그인을 추가하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  로컬 게시 폴더에서 **AdvWorksSalesOrdersMerge**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
     **게시 속성** 대화 상자가 표시됩니다.  
  
3.  **게시 액세스 목록** 페이지를 선택하고 **추가**를 클릭합니다.  
  
4.  게시 액세스 추가 대화 상자에서 *<Machine_Name>***\repl_merge**를 선택한 다음 **확인**을 클릭합니다. **확인**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
 병합 게시를 성공적으로 만들었습니다. 다음 단원에서는 이 게시를 구독합니다. [2단원: 병합 게시에 대한 구독 만들기](lesson-2-creating-a-subscription-to-the-merge-publication.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [게시된 데이터 필터링](publish/filter-published-data.md)   
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [아티클 정의](publish/define-an-article.md)  
  
  
