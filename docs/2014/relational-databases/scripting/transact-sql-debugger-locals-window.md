---
title: 지역 창 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Locals Window [Transact-SQL]
ms.assetid: 59bea640-7823-4b4d-832c-f384d83cca2f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 503a92349f7b7cfecdd4bd72de507da0a5835f7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063376"
---
# <a name="locals-window"></a>지역 창
  **지역** 창에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거의 현재 범위에 있는 지역 식에 대한 정보가 표시됩니다. 범위는 **호출 스택** 창에서 선택한 현재 호출 스택 프레임으로 설정됩니다. 지역 식을 표시하려면 디버그 모드여야 합니다.  
  
## <a name="task-list"></a>작업 목록  
 **지역 창에 액세스하려면**  
  
-   **디버그** 메뉴에서 **창**을 선택한 다음 **지역**을 클릭합니다.  
  
 **식 값을 변경하려면**  
  
-   식을 마우스 오른쪽 단추로 클릭하고 **값 편집**을 선택합니다.  
  
## <a name="columns"></a>열  
 **이름**  
 지역 식의 이름입니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거는 변수, 매개 변수 및 @@ 기호로 시작하는 시스템 함수를 표시합니다.  
  
 **Value**  
 현재 지역 식에 할당된 값을 표시합니다. 식에 할당된 값이 없으면 이 열은 비어 있습니다.  
  
 식의 길이가 **값** 열의 너비보다 큰 경우 해당 식의 **값** 셀 위로 포인터를 움직이면 도구 설명에 전체 값이 표시됩니다.  
  
 **디버거 시각화 도우미를 사용할 수 있는 경우** 값 [!INCLUDE[tsql](../../includes/tsql-md.md)] 셀에 돋보기 모양의 아이콘이 표시됩니다. 목록에서 **텍스트 시각화 도우미**, **XML 시각화 도우미**또는 **HTML 시각화 도우미**중에서 지정할 수 있습니다. 디버거 시각화 도우미를 시작하려면 돋보기 모양의 아이콘을 클릭합니다. 그러면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거에서 데이터 형식에 적합한 형식으로 데이터를 표시하는 대화 상자가 열립니다.  
  
 **형식**  
 식의 데이터 형식을 표시합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Transact-SQL 디버거](transact-sql-debugger.md)   
 [Transact-SQL 디버거 정보](transact-sql-debugger-information.md)   
 [조사식 창](transact-sql-debugger-watch-window.md)   
 [호출 스택 창](transact-sql-debugger-call-stack-window.md)   
 [간략한 조사식 대화 상자](transact-sql-debugger-quickwatch-dialog-box.md)   
 [식&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/expressions-transact-sql)  
