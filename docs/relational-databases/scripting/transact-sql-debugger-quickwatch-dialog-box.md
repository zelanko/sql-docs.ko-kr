---
title: "간략한 조사식 대화 상자 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.quickwatch
helpviewer_keywords:
- QuickWatch Dialog [Transact-SQL]
ms.assetid: d6bbb373-1452-41f2-bdc5-86ae689c3dc0
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c1bb8755f37215f0fd42b44f26d1bc260adb391e
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="transact-sql-debugger---quickwatch-dialog-box"></a>Transact-SQL 디버거 - 간략한 조사식 대화 상자
  **간략한 조사식** 대화 상자를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 디버깅할 때 변수나 매개 변수와 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식의 데이터 형식 및 값을 빨리 볼 수 있습니다. **조사식** 창에 식을 추가하여 여러 식을 조사할 수도 있습니다.  
  
## <a name="task-list"></a>작업 목록  
 **간략한 조사식 대화 상자에 액세스하려면**  
  
-   **디버그** 메뉴에서 **간략한 조사식**을 클릭합니다.  
  
 **식에 대한 정보를 보려면**  
  
1.  **식** 목록 상자에서 원하는 식을 입력하거나 선택합니다. 다음의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식이 지원됩니다.  
  
    -   변수  
  
    -   매개 변수.  
  
    -   이름이 @@로 시작하는 시스템 함수  
  
    -   @IntegerCounter + 1 또는 FirstName + LastName과 같이 하나 이상의 변수, 매개 변수 또는 시스템 함수에 연산자를 적용하여 빌드한 식  
  
    -   SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1 등의 단일 값을 반환하는 Transact-SQL 문입니다.  
  
2.  **다시 계산**을 클릭합니다.  
  
 **조사식 창에 간략한 조사식을 추가하려면**  
  
-   **조사식 추가**를 클릭합니다.  
  
 **간략한 조사식 값을 변경하려면**  
  
-   식을 마우스 오른쪽 단추로 클릭하고 **값 편집**을 선택합니다.  
  
## <a name="options"></a>옵션  
 **식 목록**  
 현재 선택한 식을 표시합니다. 드롭다운 목록에는 표시하도록 선택할 수 있는 식 집합이 있습니다. 목록에 있는 식은 현재 **호출 스택** 창에서 선택한 스택 프레임 범위에서 사용할 수 있는 식입니다. 다른 식을 표시하려면 식을 입력하거나 목록에서 선택합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거는 변수, 매개 변수 및 @@ 기호로 시작하는 시스템 함수를 지원합니다.  
  
 **값 표**  
 현재 조사 중인 식의 속성을 표시합니다.  
  
 **이름**  
 조사 중인 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식입니다.  
  
 **값**  
 현재 식에 할당된 값을 표시합니다. 현재 식에 값이 없으면 빈 상태로 표시됩니다.  
  
 식의 길이가 **값** 열의 너비보다 큰 경우 해당 식의 **값** 셀 위로 포인터를 움직이면 도구 설명에 전체 값이 표시됩니다.  
  
 **디버거 시각화 도우미를 사용할 수 있는 경우** 값 [!INCLUDE[tsql](../../includes/tsql-md.md)] 셀에 돋보기 모양의 아이콘이 표시됩니다. 목록에서 **텍스트 시각화 도우미**, **XML 시각화 도우미**또는 **HTML 시각화 도우미**중에서 지정할 수 있습니다. 디버거 시각화 도우미를 시작하려면 돋보기 모양의 아이콘을 클릭합니다. 그러면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거에서 데이터 형식에 적합한 형식으로 데이터를 표시하는 대화 상자가 열립니다.  
  
 **형식**  
 식의 데이터 형식을 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-SQL 디버거](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL 디버거 정보](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [조사식 창](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [지역 창](../../relational-databases/scripting/transact-sql-debugger-locals-window.md)   
 [호출 스택 창](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
