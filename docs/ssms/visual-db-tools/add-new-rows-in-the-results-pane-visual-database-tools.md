---
title: 결과 창에서 새 행 추가(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- inserting rows
- Query Designer [SQL Server], Results pane
- Results pane
- adding rows
- row additions [SQL Server], Results pane
ms.assetid: 59891c84-3f54-4ab9-8b86-72c59627b480
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 444d6d79a1c381a9a65df17c3949ddba5020a51e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832511"
---
# <a name="add-new-rows-in-the-results-pane-visual-database-tools"></a>결과 창에서 새 행 추가(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
데이터를 직접 입력하거나 메모장 또는 Excel 같은 다른 프로그램에서 복사하여 붙여넣는 방식으로 새 데이터를 추가할 수 있습니다. 붙여넣을 행은 행이 들어갈 테이블과 열 수 및 형식이 똑같아야 합니다. 결과 창에 여러 행을 한 번에 붙여넣을 수 있습니다.  
  
데이터를 입력하는 방법에 대한 자세한 내용은 [결과 업데이트 규칙&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-updating-results-visual-database-tools.md)을 참조하세요.  
  
### <a name="to-add-a-new-data-row"></a>새 데이터 행을 추가하려면  
  
1.  결과 창의 아래쪽에 새 데이터 행을 추가할 수 있는 빈 행으로 이동합니다.  
  
    모든 열의 초기 값은 *NULL*입니다.  
  
    > [!TIP]  
    > 결과 창의 아래쪽에 있는 탐색 모음을 사용하면 비어 있는 첫째 행으로 직접 이동할 수 있습니다.  
  
2.  클립보드에서 행을 붙여넣는 경우 왼쪽에 있는 단추를 클릭하여 새 행을 선택합니다.  
  
    > [!NOTE]  
    > 붙여넣을 행이 데이터베이스에 하나 이상 커밋되지 않으면 커밋할 수 없는 행에 대한 정보가 메시지로 표시됩니다.  
  
3.  새 행에 데이터를 입력합니다. 붙여 넣으려면 **편집** 메뉴에서 **붙여넣기** 를 선택합니다.  
  
4.  해당 행에서 포커스를 옮기면 행이 데이터베이스에 커밋됩니다.  
  
행을 저장할 때 오류가 발생하면 쿼리 및 뷰 디자이너에 오류 메시지가 나타나고 편집 중이던 행으로 되돌아갑니다. 그런 다음 아래의 작업을 수행할 수 있습니다.  
  
-   해당 행을 다시 편집하여 오류를 해결합니다.  
  
-   Esc 키를 눌러 편집을 취소합니다. 변경한 셀에서 Esc 키를 누르면 해당 셀에 대한 변경이 취소됩니다. 변경하지 않은 셀에서 Esc 키를 누르면 행 전체에 대한 변경이 취소됩니다.  
  
## <a name="see-also"></a>참고 항목  
[결과 창에서 데이터 작업&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
[쿼리 관련 기본 작업 수행&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
