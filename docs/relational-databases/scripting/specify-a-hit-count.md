---
title: "적중 횟수 지정 | Microsoft 문서"
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
- vs.debug.breakpt.hitcount
helpviewer_keywords:
- Transact-SQL debugger, breakpoint hit count
ms.assetid: 24836939-94ed-4e57-aa85-5d6938d859e4
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 07a60dfe673b6aba231958324b4e9094fc3dcb38
ms.lasthandoff: 04/11/2017

---
# <a name="specify-a-hit-count"></a>적중 횟수 지정
  중단점 적중 횟수는 중단점에 도달할 때마다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거가 증가시키는 카운터입니다. 지정한 적중 횟수에 도달하고 지정한 중단 조건을 만족하면 디버거는 해당 중단점에 대해 지정된 동작을 수행합니다.  
  
## <a name="hit-count-considerations"></a>적중 횟수 고려 사항  
 기본적으로 중단점에 도달할 때마다 실행이 중단됩니다. 다음 옵션 중에서 선택할 수 있습니다.  
  
-   항상 중단(기본값)  
  
-   적중 횟수가 지정한 값과 같으면 중단  
  
-   적중 횟수가 지정한 값의 배이면 중단  
  
-   적중 횟수가 지정한 값보다 크거나 같으면 중단  
  
 중단점 적중 횟수는 디버깅 세션의 범위 내에서 증가합니다. 모든 적중 횟수는 각 디버깅 세션이 시작될 때 0으로 설정됩니다.  
  
 중단점 중단을 실행하지 않고 중단점 적중 횟수를 추적하려면 중단점이 중단되지 않도록 적중 횟수를 매우 높은 값으로 지정합니다.  
  
 중단점의 기본 동작은 적중 횟수와 중단점 조건을 모두 만족하면 실행을 중단하는 것입니다. 다른 동작을 지정하는 방법은 [중단점 동작 지정](../../relational-databases/scripting/specify-a-breakpoint-action.md)을 참조하세요.  
  
#### <a name="to-specify-a-hit-count"></a>적중 횟수를 지정하려면  
  
1.  편집기 창에서 중단점 문자 모양을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **적중 횟수** 를 클릭합니다.  
  
     -또는-  
  
     **중단점** 창에서 중단점 문자 모양을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **적중 횟수** 를 클릭합니다.  
  
2.  **중단점 적중 횟수** 대화 상자의 **중단점이 적중될 때** 상자에서 원하는 동작을 선택합니다.  
  
     **항상 중단**이 아닌 다른 설정을 선택하면 목록 오른쪽에 입력란이 나타납니다. 이 입력란에 정수를 입력하여 원하는 적중 횟수를 지정합니다.  
  
3.  **확인** 을 클릭하여 변경 내용을 구현하거나 **취소** 를 클릭하여 변경 내용을 적용하지 않고 종료합니다.  
  
#### <a name="to-view-or-reset-the-current-hit-count"></a>현재 적중 횟수를 보거나 다시 설정하려면  
  
1.  편집기 창에서 중단점 문자 모양을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **적중 횟수** 를 클릭합니다.  
  
     -또는-  
  
     **중단점** 창에서 중단점 문자 모양을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **적중 횟수** 를 클릭합니다.  
  
2.  **중단점 적중 횟수** 대화 상자의 **다시 설정** 단추 바로 위에 **현재 적중 횟수:** 가 표시됩니다.  
  
3.  현재 적중 횟수를 0으로 설정하려면 **다시 설정** 을 클릭합니다.  
  
4.  **확인** 이나 **취소** 를 클릭하여 대화 상자를 종료합니다.  
  
## <a name="see-also"></a>참고 항목  
 [중단점 조건 지정](../../relational-databases/scripting/specify-a-breakpoint-condition.md)  
  
  
