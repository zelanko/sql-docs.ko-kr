---
title: "삭제 쿼리 만들기(Visual Database Tools) | Microsoft 문서"
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
- row removal [SQL Server], Delete query
- Delete query
- queries [SQL Server], types
- removing rows
- removing data
- data deletions [SQL Server]
- deleting rows
- deleting data
ms.assetid: 0db3af43-1ec4-48c8-b769-2bb9c76d3434
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: af72312e54a1ddcce4c1bbd867fbbacc624dcd4a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/18/2017

---
# <a name="create-delete-queries-visual-database-tools"></a>삭제 쿼리 만들기(Visual Database Tools)
삭제 쿼리를 사용하면 테이블에서 모든 행을 삭제할 수 있습니다.  
  
> [!NOTE]  
> 테이블에서 모든 행을 삭제하면 테이블에서 데이터가 지워지지만 테이블 자체가 삭제되지는 않습니다. 데이터베이스에서 테이블을 삭제하려면 개체 탐색기에서 테이블을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.  
  
삭제 쿼리를 만들면 행을 삭제하는 데 사용할 수 있는 옵션이 반영되도록 조건 창이 변경됩니다. 삭제 쿼리에는 데이터를 표시하지 않으므로 출력, 정렬 기준 및 정렬 순서 열이 제거됩니다. 또한, 삭제할 개별 열을 지정할 수 없으므로 테이블이나 테이블 반환 개체를 나타내는 사각형의 열 이름 옆에 있는 확인란이 표시되지 않습니다.  
  
쿼리 및 뷰 디자이너에서 행을 하나라도 삭제할 수 없으면 다른 행도 함께 삭제되지 않으며 데이터베이스에서 삭제할 수 없는 정보가 포함된 행을 알리는 메시지가 나타납니다.  
  
> [!CAUTION]  
> 삭제 쿼리의 실행 동작을 취소할 수는 없습니다. 문제가 발생할 경우에 대비하여 삭제 쿼리를 실행하기 전에 데이터를 백업하는 것이 좋습니다.  
  
### <a name="to-create-a-delete-query"></a>삭제 쿼리를 만들려면  
  
1.  행을 삭제하려는 테이블을 다이어그램 창에 추가합니다.  
  
2.  **쿼리 디자이너** 메뉴에서 **형식 변경**을 가리킨 다음 **삭제**를 클릭합니다. **참고** 삭제 쿼리를 시작할 때 다이어그램 창에 두 개 이상의 테이블이 표시되어 있으면 행을 삭제할 테이블의 이름을 지정하라는 메시지가 쿼리 및 뷰 디자이너의 [테이블 삭제 대화 상자](../../ssms/visual-db-tools/delete-table-dialog-box-visual-database-tools.md) 에 나타납니다.  
  
삭제 쿼리를 실행해도 [결과 창](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)에는 결과가 보고되지 않습니다. 대신, 삭제한 행의 수를 나타내는 메시지가 표시됩니다.  
  
## <a name="see-also"></a>관련 항목:  
[지원되는 쿼리 형식&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  

