---
title: 중단점 필터 지정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.breakpt.contraints
helpviewer_keywords:
- Transact-SQL debugger, breakpoint filter
ms.assetid: 7bf1dddd-7b0b-4c47-8a7b-28a5569b4fa5
caps.latest.revision: 6
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8a55eb14c606348a63072d669db98fe3cae6b3f2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186274"
---
# <a name="specify-a-breakpoint-filter"></a>중단점 필터 지정
  중단점 필터는 중단점이 지정된 컴퓨터, 운영 체제 프로세스 및 스레드에서만 작동하도록 제한합니다. 중단점 필터는 일반적으로 병렬 응용 프로그램을 디버깅할 때 사용됩니다.  
  
##  <a name="BKMK_ActionConsiderations"></a> 필터 고려 사항  
 중단점 필터는 일반적으로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거에서는 사용되지 않는데 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 및 저장 프로시저는 병렬 응용 프로그램이 아니기 때문입니다.  
  
#### <a name="to-specify-a-breakpoint-filter"></a>중단점 필터를 지정하려면  
  
1.  편집기 창에서 중단점 문자 모양을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **필터** 를 클릭합니다.  
  
     -또는-  
  
     **중단점** 창에서 중단점 문자 모양을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **필터** 를 클릭합니다.  
  
2.  **중단점 필터** 대화 상자의 **필터** 상자에 컴퓨터 이름을 지정하거나 운영 체제 프로세스 및 스레드를 이름이나 ID 번호로 지정합니다.  
  
    -   `MachineName`은 데이터베이스 엔진 인스턴스를 실행 중인 컴퓨터입니다.  
  
    -   `ProcessID`및 `ProcessName` 은 데이터베이스 엔진의 인스턴스를 실행 중인 운영 체제 프로세스입니다.  
  
    -   `ThreadID` 및 `ThreadName` 는 실행 중인 운영 체제 스레드는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리, 프로시저 또는 함수는 데이터베이스 엔진의 인스턴스에 있습니다.  
  
3.  **확인** 을 클릭하여 변경 내용을 구현하거나 **취소** 를 클릭하여 변경 내용을 적용하지 않고 종료합니다.  
  
## <a name="see-also"></a>관련 항목  
 [중단점 조건 지정](specify-a-breakpoint-condition.md)   
 [적중 횟수 지정](specify-a-hit-count.md)   
 [중단점 동작 지정](specify-a-breakpoint-action.md)  
  
  