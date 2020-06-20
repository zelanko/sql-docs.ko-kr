---
title: '작업 8: 복합 도메인 규칙 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: cff3b662-7876-4445-9bdd-96be35b3ca0c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4766a1206eb09e98bb20d3712a63762126b682b7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006244"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>태스크 8: 복합 도메인 규칙 만들기
  이 작업에서는 **주소 유효성 검사** 복합 도메인에 대 한 규칙을 만듭니다. 도메인 간 규칙을 정의 합니다. **city** **가 로스앤젤레스 인 경우**시/ **도는** **CA** 여야 합니다. 여기서 **city** 및 **state** 는 두 개의 도메인입니다.  
  
1.  오른쪽 창에서 **CD 규칙** 탭으로 전환 합니다.  
  
2.  도구 모음에서 **새 도메인 규칙 추가를** 클릭 합니다.  
  
3.  **이름** 에 **City 상태 규칙** 을 입력 하 고 **enter**키를 누릅니다.  
  
4.  **규칙 작성** 창의 도메인 목록에서 **City** 를 선택 하 고 조건 **값이 다음 인** 경우 값에 대해 **로스앤젤레스** 를 입력 합니다.  
  
5.  Then 창의 도메인 목록에서 **상태** 를 선택 하 고 **값이 다음을**선택 하 고 값으로 **CA** 를 입력 한 **다음** **tab**키를 누릅니다.  
  
     ![복합 도메인 규칙](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "복합 도메인 규칙")  
  
6.  페이지 맨 아래에 있는 **닫기** 단추를 클릭 하 여 DQS 클라이언트의 기본 페이지로 전환 합니다. 이 기술 자료는 다음 단원에서 게시합니다. 이 기술 자료는 잠긴 상태(자물쇠 아이콘)입니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 9: 참조 데이터 서비스 구성](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  
