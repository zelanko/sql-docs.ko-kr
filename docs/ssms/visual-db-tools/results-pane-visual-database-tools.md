---
title: "결과 창(Visual Database Tools) | Microsoft 문서"
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
- View Designer, Results pane
- result sets [SQL Server], queries
- synchronization [SQL Server], query results with definition
- displaying query results in grid
- grid showing query results [SQL Server]
- showing query results in grid
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- viewing query results
- queries [SQL Server], results
- Results pane
ms.assetid: 6309a1bc-a628-4141-8bb5-b35924bd19f9
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0712854db6e1b4b85a58b4d72264ea51e1162b06
ms.lasthandoff: 04/11/2017

---
# <a name="results-pane-visual-database-tools"></a>결과 창(Visual Database Tools)
결과 창은 가장 최근에 실행한 SELECT 쿼리의 결과를 보여 줍니다. 다른 쿼리 형식의 결과는 메시지 상자에 표시됩니다. 결과 창을 열려면 쿼리를 열거나 만듭니다. 테이블의 데이터를 반환해도 결과 창이 나타납니다. 결과 창이 기본적으로 표시되지 않으면 **쿼리 디자이너** 메뉴에서 **창**을 가리킨 다음 **결과**를 클릭합니다.  
  
## <a name="what-you-can-do-in-the-results-pane"></a>결과 창에서 수행할 수 있는 작업  
  
-   가장 최근에 실행한 SELECT 쿼리에 대한 결과 집합을 스프레드시트 모양의 표 형태로 볼 수 있습니다.  
  
-   단일 테이블이나 뷰의 데이터를 표시하는 쿼리 또는 뷰에 대해 결과 집합의 개별 열에 있는 값을 편집하거나, 새 행을 추가하거나, 기존 행을 삭제할 수 있습니다.  
  
## <a name="limitations-in-the-results-pane"></a>결과 창의 제한 사항  
  
-   테이블 반환 함수를 통해 반환되는 결과는 다음과 같은 몇 가지 경우에만 업데이트할 수 있습니다.  
  
-   두 개 이상의 테이블 또는 뷰의 열이 포함된 쿼리나 뷰는 업데이트할 수 없습니다.  
  
-   저장 프로시저를 통해 반환된 결과는 업데이트할 수 없습니다.  
  
-   GROUP BY 또는 DISTINCT 절을 사용하는 쿼리나 뷰는 업데이트할 수 없습니다.  
  
## <a name="navigating-in-the-results-pane"></a>결과 창에서 탐색  
결과 창의 아래쪽에 있는 탐색 모음을 사용하면 레코드를 빠르게 탐색할 수 있습니다.  
  
이 탐색 모음에는 첫 번째 레코드와 마지막 레코드, 다음 레코드와 이전 레코드 또는 특정 레코드로 이동하기 위한 단추가 있습니다.  
  
특정 레코드로 이동하려면 탐색 모음의 입력란에 원하는 행 번호를 입력한 다음 Enter 키를 누릅니다.  
  
쿼리 및 뷰 디자이너에서 바로 가기 키를 사용하는 방법에 대한 자세한 내용은 [쿼리 및 뷰 디자이너에서 탐색&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/navigate-in-the-query-and-view-designer-visual-database-tools.md)을 참조하세요.  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>결과 집합과 쿼리 정의의 동기화 상태 유지  
쿼리나 뷰의 결과에 대한 작업을 수행하는 동안 결과 창의 레코드가 쿼리 정의와 동기화되지 않을 수 있습니다. 예를 들어, 테이블에서 다섯 개의 열 중 네 개의 열에 대한 쿼리를 실행한 다음 다이어그램 창을 사용하여 다섯 번째 열을 쿼리 정의에 추가하는 경우 이 다섯 번째 열의 데이터는 결과 창에 자동으로 추가되지 않습니다. 결과 창에 새 쿼리 정의가 반영되도록 하려면 쿼리를 다시 실행해야 합니다.  
  
쿼리를 변경하면 결과 창의 오른쪽 아래에 경고 아이콘과 "쿼리가 변경되었습니다."라는 텍스트가 표시됩니다. 이 창의 왼쪽 위에도 아이콘이 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 만들기&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[쿼리 실행&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[쿼리 및 뷰 디자인 방법 도움말 항목&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[다이어그램 창&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[조건 창&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[결과 창에서 데이터 작업&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
  

