---
title: "쿼리 및 뷰 디자이너에서 탐색(Visual Database Tools) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- View Designer, navigating
- shortcuts [SQL Server]
- Query Designer [SQL Server], navigating
- keyboard shortcuts [Visual Database Tools]
ms.assetid: 1c65acef-6dfa-463a-bf37-5a5335fe3865
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7cc7f7c8972fae08c956db86f95250d830fba39b
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="navigate-in-the-query-and-view-designer-visual-database-tools"></a>쿼리 및 뷰 디자이너에서 탐색(Visual Database Tools)
키보드 또는 마우스를 사용하여 쿼리 및 뷰 디자이너에서 작업할 수 있습니다. 구체적인 방법은 다음 표를 참조하십시오.  
  
## <a name="any-pane"></a>모든 창  
  
|**수행할 작업**|**작업 방법**|**클릭 대상**|  
|----------|-------------|-------------|  
|쿼리 및 뷰 디자이너 창 사이를 이동|F6 , Shift+F6|대상 창 내부의 임의 위치|  
  
> [!TIP]  
> 바로 가기 키 Ctrl+Tab을 사용하여 쿼리 및 뷰 디자이너 창과 다른 창으로 포커스를 이동할 수 있습니다.  
  
## <a name="diagram-pane"></a>다이어그램 창  
  
|**수행할 작업**|**작업 방법**|**클릭 대상**|  
|----------|-------------|-------------|  
|테이블, 기타 테이블 구조 개체 및 조인 선(가능한 경우) 사이를 이동|Tab 키 또는 Shift+Tab|이동할 대상 테이블, 테이블 구조 개체 또는 조인 선|  
|테이블 또는 테이블 구조 개체의 열 사이를 이동|화살표 키|이동할 대상 열|  
|선택된 데이터 열을 출력하기 위해 선택|스페이스바 또는 + 키|열 이름 옆에 있는 확인란|  
|선택된 데이터 열을 쿼리 결과에서 제거|스페이스바 또는 - 키|열 이름 옆에 있는 확인란|  
|선택된 테이블, 테이블 구조 개체 또는 조인 선을 쿼리에서 제거|DELETE|마우스 오른쪽 단추를 클릭한 다음 **제거**선택|  
  
> [!NOTE]  
> 여러 항목을 선택한 경우 이 키를 누르면 선택한 모든 항목에 영향을 줍니다. Ctrl 키를 누른 채 항목을 클릭하면 여러 항목이 선택됩니다.  
  
자세한 내용은 [다이어그램 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)을 참조하세요.  
  
## <a name="criteria-pane"></a>조건 창  
  
|수행할 작업|작업 방법|클릭 대상|  
|------|---------|---------|  
|셀 사이를 이동|화살표 키, Tab 키 또는 Shift+Tab|대상 셀|  
|선택한 열의 마지막 행으로 이동|Ctrl+아래쪽 화살표||  
|선택한 열의 첫째 행으로 이동|Ctrl+위쪽 화살표||  
|표의 표시 부분에서 왼쪽 위 셀로 이동|Ctrl+Home||  
|오른쪽 아래 셀로 이동|Ctrl+End||  
|드롭다운 목록에서 이동|위쪽 화살표 또는 아래쪽 화살표|해당 셀의 단추|  
|표 형태 창의 전체 열 선택|Ctrl+스페이스바|열 머리글|  
|편집 모드와 셀 선택 모드 사이를 전환|F2||  
|셀에서 선택한 텍스트를 클립보드에 복사(편집 모드에서)|CTRL+C||  
|셀에서 선택한 텍스트를 잘라내어 클립보드에 붙여넣기(편집 모드에서)|Ctrl+X||  
|클립보드의 텍스트를 붙여넣기(편집 모드에서)|Ctrl+V||  
|셀 편집 중에 삽입 모드와 겹쳐쓰기 모드 사이를 전환|Ins||  
|출력 열에서 확인란 선택/선택 취소|스페이스바|확인란|  
|셀의 선택 내용 지우기|DELETE||  
|선택된 표 형태 창 열의 모든 값 지우기|DELETE||  
|기존 행 사이에 새 행 삽입|표 형태 창의 행을 선택한 다음 Ins 키||  
|또는... 열 추가|또는... 열을 선택한 다음 Ins 키||  
  
> [!NOTE]  
> 여러 항목을 선택한 경우 이 키를 누르면 선택한 모든 항목에 영향을 줍니다.  
  
자세한 내용은 [조건 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)을 참조하세요.  
  
## <a name="sql-pane"></a>SQL 창  
SQL 창에서 작업하는 경우 Ctrl+화살표 키 같은 표준 Windows 편집 키를 사용하여 단어 사이를 이동할 수 있으며 **편집**메뉴의 **잘라내기**, **복사** 및 **붙여넣기** 명령을 사용할 수 있습니다.  
  
> [!NOTE]  
> 겹쳐쓰기 모드는 없고 텍스트를 삽입할 수만 있습니다.  
  
자세한 내용은 [SQL 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)을 참조하세요.  
  
## <a name="results-pane"></a>결과 창  
  
|**수행할 작업**|**작업 방법**|**클릭 대상**|  
|----------|-------------|-------------|  
|셀 사이를 이동|화살표 키, Tab 키 또는 Shift+Tab|대상 셀|  
|현재 행의 첫째 셀 또는 마지막 셀로 이동|Home 키 또는 End 키||  
|현재 열의 첫째 행으로 이동|Ctrl+위쪽 화살표||  
|왼쪽 위 셀로 이동|Ctrl+Home||  
|첫째 열의 맨 아래 셀로 이동|Ctrl+아래쪽 화살표||  
|셀의 첫째 문자까지 선택|Shift+Home||  
|셀의 마지막 문자까지 선택|Shift+End||  
|편집 모드와 셀 선택 모드 사이를 전환|F2||  
|셀 편집 중에 삽입 모드와 겹쳐쓰기 모드 사이를 전환|Ins||  
|테이블에서 특정 행 삭제|DELETE||  
|현재 셀에 대한 변경 취소|변경된 셀에서 Esc 키||  
|현재 행에 대한 변경 취소|변경되지 않은 셀에서 Esc 키||  
|셀에 null 값 입력|Ctrl+0||  
|선택한 열 또는 행을 클립보드에 복사|CTRL+C||  
|셀에서 선택한 텍스트를 클립보드에 복사(편집 모드에서)|CTRL+C||  
|셀에서 선택한 텍스트를 잘라내어 클립보드에 붙여넣기(편집 모드에서)|Ctrl+X||  
|클립보드의 텍스트를 붙여넣기(편집 모드에서)|Ctrl+V||  
  
> [!NOTE]  
> 여러 항목을 선택한 경우 이 키를 누르면 선택한 모든 항목에 영향을 줍니다.  
  
자세한 내용은 [결과 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자인 방법 도움말 항목&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  

