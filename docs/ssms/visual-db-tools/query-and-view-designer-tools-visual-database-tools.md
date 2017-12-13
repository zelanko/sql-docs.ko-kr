---
title: "쿼리 및 뷰 디자이너 도구(Visual Database Tools) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.querydesigner
- vdt.pane.diagram
- vdt.pane.grid
- vdt.dlgbox.querybuilder
- vdt.pane.sql
- vdt.pane.results
helpviewer_keywords:
- Query Designer [SQL Server], panes
- View Designer, panes
- Query Designer [SQL Server], components
- View Designer, components
ms.assetid: 12e4b5a5-b793-4b6c-a0e5-c450c49bf26f
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e5e890d0a453291ba71ab06b0489fb3d0c8c216a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="query-and-view-designer-tools-visual-database-tools"></a>쿼리 및 뷰 디자이너 도구(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 쿼리, 뷰, 인라인 함수 또는 단일 문 저장 프로시저를 디자인할 때 사용하는 디자이너는 다이어그램 창, 조건 창, SQL 창 및 결과 창으로 구성됩니다.  
  
![쿼리 디자이너](../../ssms/visual-db-tools/media/vs_queryviewdsgpanes.gif "쿼리 디자이너")  
  
-   다이어그램 창은 쿼리하는 테이블과 기타 테이블 반환 개체를 표시합니다. 각 사각형은 테이블이나 테이블 반환 개체를 나타내며 사용 가능한 데이터 열을 표시합니다. 조인은 사각형 사이에 선으로 표시됩니다. 자세한 내용은 [다이어그램 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)을 참조하세요.  
  
-   조건 창에는 표시할 데이터 열, 선택할 행, 행을 그룹화하는 방법 등의 옵션을 지정하는 스프레드시트 모양의 표가 들어 있습니다. 자세한 내용은 [조건 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)을 참조하세요.  
  
-   SQL 창은 쿼리 또는 뷰에 대한 SQL 문을 표시합니다. 디자이너에서 만든 SQL 문을 편집하거나 사용자만의 SQL 문을 직접 입력할 수 있습니다. SQL 창은 통합 쿼리와 같이 다이어그램 창이나 조건 창을 통해 만들 수 없는 SQL 문을 입력하는 데 특히 유용합니다. 자세한 내용은 [SQL 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)을 참조하세요.  
  
-   결과 창은 쿼리 또는 뷰에서 검색한 데이터가 있는 표를 표시합니다. 쿼리 및 뷰 디자이너의 결과 창에서는 가장 최근에 실행한 SELECT 쿼리의 결과를 보여 줍니다. 표의 셀에 들어 있는 값을 편집하여 데이터베이스를 수정할 수 있으며 행을 추가하거나 삭제할 수도 있습니다. 자세한 내용은 [결과 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)을 참조하세요.  
  
다이어그램 창에서 열을 선택하여 표시하거나 조건 창에 해당 열을 입력하거나 SQL 창에서 SQL 문의 일부로 열을 만들어 지정하는 등 어느 창에서나 쿼리 또는 뷰를 만들 수 있습니다.  
  
## <a name="displaying-and-hiding-panes"></a>창 표시 및 숨기기  
창을 숨기거나 보이지 않는 창을 표시하려면 디자인 화면을 마우스 오른쪽 단추로 클릭하고 **창**을 가리킨 다음 창 이름을 클릭합니다. 쿼리 및 뷰 디자이너가 쿼리 디자이너 모드로 열리면 **결과** 창을 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[쿼리 및 뷰 디자이너 열기&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-the-query-and-view-designer-visual-database-tools.md)  
[SQL 편집기&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-editor-visual-database-tools.md)  
  
