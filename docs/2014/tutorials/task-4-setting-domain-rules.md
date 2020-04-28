---
title: '작업 4: 도메인 규칙 설정 | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: dd59bf315e90bd52ba1388d27c533ab4a3136d3c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72381737"
---
# <a name="task-4-setting-domain-rules"></a>태스크 4: 도메인 규칙 설정
  이 작업에서는 **연락처 전자 메일** 도메인에 대 한 규칙을 만들어 전자 메일 주소가 ** \@adventure-works.com**으로 끝나는지 확인 합니다. 이 페이지에 대한 자세한 내용은 [도메인 규칙 만들기](https://msdn.microsoft.com/library/hh510397.aspx) 항목을 참조하십시오.  
  
1.  **도메인 목록** 에서 **Contact Email**을 클릭합니다.  
  
2.  오른쪽 창에서 **도메인 규칙** 으로 전환합니다.  
  
     ![새 도메인 규칙 추가 도구 모음 단추](../../2014/tutorials/media/et-settingdomainrules-01.jpg "새 도메인 규칙 추가 도구 모음 단추")  
  
3.  오른쪽 창의 도구 모음에서 **새 도메인 규칙 추가** 단추를 클릭하여 규칙을 추가합니다.  
  
4.  **규칙 이름** 에 **Email Validation** 을 입력하고 **Enter**키를 누릅니다. **활성** 확인란은 기본적으로 선택되어 있어야 합니다. 이 컨트롤을 사용하면 규칙을 일시적으로 비활성화할 수 있습니다.  
  
5.  **규칙 작성** 창에서 **아래쪽 화살표**를 클릭하고 **값이 다음으로 종료**를 선택합니다.  
  
6.  텍스트 상자에 ** \@adventure-works.com** 를 입력 하 고 **tab**키를 누릅니다. **규칙 작성** 창에서 **선택한 절에 새 조건 추가** 도구 모음 단추를 클릭하여 조건을 추가할 수 있습니다.  
  
     ![전자 메일 유효성 검사 규칙](../../2014/tutorials/media/et-settingdomainrules-02.jpg "전자 메일 유효성 검사 규칙")  
  
7.  오른쪽 창의 도구 모음에서 **테스트 데이터에서 선택한 도메인 규칙 실행** 단추를 클릭하여 예제 데이터로 규칙을 테스트합니다.  
  
     ![테스트 데이터에 대한 도메인 규칙 실행 도구 모음 단추](../../2014/tutorials/media/et-settingdomainrules-03.jpg "테스트 데이터에 대한 도메인 규칙 실행 도구 모음 단추")  
  
8.  **도메인 규칙 테스트** 대화 상자의 도구 모음에서 **도메인 규칙에서 새 테스트 용어를 추가합니다.** 단추를 클릭합니다.  
  
     ![도메인 규칙 테스트 대화 상자](../../2014/tutorials/media/et-settingdomainrules-04.jpg "도메인 규칙 테스트 대화 상자")  
  
9. **Contact Email** 열에 **frank7\@adventure-works.com** (올바른 값)를 입력 합니다.  
  
10. 이전 두 단계를 반복 하 **여\@joe2 adventure-work.com** (가 없는 잘못 된 값)을 추가 합니다.  
  
11. 도구 모음에서 마지막 단추(**모든 용어에 대한 도메인 규칙을 테스트합니다.**)를 클릭하여 규칙에 대해 입력 데이터를 테스트합니다.  
  
     ![모든 용어에 대해 도메인 규칙 테스트 도구 모음 단추](../../2014/tutorials/media/et-settingdomainrules-05.jpg "모든 용어에 대해 도메인 규칙 테스트 도구 모음 단추")  
  
12. 첫 번째 항목은 유효한 항목으로 표시되고 두 번째 항목은 잘못된 항목으로 표시됨을 알 수 있습니다.  
  
     ![도메인 규칙 테스트 결과](../../2014/tutorials/media/et-settingdomainrules-06.jpg "도메인 규칙 테스트 결과")  
  
13. **닫기** 를 클릭하여 **도메인 규칙 테스트** 대화 상자를 닫습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 5: 용어 기반 관계 설정](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  
