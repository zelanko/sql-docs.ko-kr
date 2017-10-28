---
title: "스크립트를 프로젝트 또는 솔루션으로 저장 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 72dfd37f-dbe7-4d1d-bda6-7eb54c7922d3
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: 3772efa6ab55acd4087cd47f897040f782476636
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="lesson-3-3---save-scripts-as-projects-or-solutions"></a>3-3단원 - 스크립트를 프로젝트 또는 솔루션으로 저장
[!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio에 익숙한 개발자라면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 솔루션 탐색기를 쉽게 활용할 수 있을 것입니다. 업무 지원 스크립트를 스크립트 프로젝트로 그룹화하고 스크립트 프로젝트를 하나의 솔루션으로 함께 관리할 수 있습니다. 스크립트 프로젝트와 솔루션에 배치된 스크립트는 하나의 그룹으로 함께 열거나 Visual SourceSafe와 같은 원본 제어 제품에 함께 저장할 수 있습니다. 스크립트 프로젝트에는 스크립트를 제대로 실행하기 위한 연결 정보가 포함되며 지원 텍스트 파일 같이 스크립트가 아닌 파일이 포함될 수 있습니다.  
  
다음 연습에서는 스크립트 프로젝트와 솔루션에 배치되어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 쿼리하는 간단한 스크립트를 만듭니다.  
  
## <a name="using-script-projects-and-solutions"></a>스크립트 프로젝트 및 솔루션 사용  
  
#### <a name="to-create-a-script-project-and-solution"></a>스크립트 프로젝트와 솔루션을 만들려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 열고 개체 탐색기로 서버에 연결합니다.  
  
2.  **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다. **새 프로젝트** 대화 상자가 열립니다.  
  
3.  **이름** 입력란에 **StatusCheck**를 입력하고 **템플릿** 에서 **SQL Server 스크립트**를 클릭한 다음 **확인** 을 클릭하여 새 솔루션과 스크립트 프로젝트를 엽니다.  
  
4.  솔루션 탐색기에서 **연결**을 마우스 오른쪽 단추로 클릭한 다음 **새 연결**을 클릭합니다. **서버에 연결** 대화 상자가 열립니다.  
  
5.  **서버 이름** 목록 상자에 서버 이름을 입력합니다.  
  
6.  **옵션**을 클릭한 다음 **연결 속성** 탭을 클릭합니다.  
  
7.  **연결할 데이터베이스** 상자에서 서버를 찾아보고 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 선택한 다음 **연결**을 클릭합니다. 데이터베이스를 포함한 연결 정보가 프로젝트에 추가됩니다.  
  
8.  속성 창이 표시되지 않으면 솔루션 탐색기에서 새 연결을 클릭한 다음 F4 키를 누릅니다. 연결 속성이 나타나고 **로** 초기 데이터베이스 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 포함하는 연결 정보가 표시됩니다.  
  
9. 솔루션 탐색기에서 연결을 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다. 서버의 **데이터베이스에 연결된** SQLQuery1.sql [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 이라는 새 쿼리가 생성되어 스크립트 프로젝트에 추가됩니다.  
  
10. 쿼리 편집기에 다음 쿼리를 입력하여 작업 주문 시작 날짜 전 기한이 있는 작업 주문 수를 확인합니다. 자습서 창에서 코드를 복사하여 붙여 넣을 수 있습니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT COUNT(WorkOrderID)  
    FROM Production.WorkOrder  
    WHERE DueDate < StartDate;  
  
    ```  
  
    > [!NOTE]  
    > 쿼리를 입력할 공간이 더 필요하면 Shift+Alt+Enter를 눌러 전체 화면 모드로 전환합니다.  
  
11. 솔루션 탐색기에서 **SQLQuery1**을 마우스 오른쪽 단추로 클릭한 다음 **이름 바꾸기**를 클릭합니다. 쿼리의 새 이름으로 **Check Workorders****.sql** 을 입력하고 Enter 키를 누릅니다.  
  
12. 솔루션과 스크립트 프로젝트를 저장하려면 **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[요약: 솔루션 및 스크립트 프로젝트](../../tools/sql-server-management-studio/lesson-3-4-summary-solutions-and-script-projects.md)  
  
  
  

