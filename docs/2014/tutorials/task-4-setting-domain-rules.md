---
title: '작업 4: 도메인 규칙 설정 | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6c3b51408258b93f6585b46171793eb885a6d0d3
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53349577"
---
# <a name="task-4-setting-domain-rules"></a>작업 4: 도메인 규칙 설정
  이 작업에 대 한 규칙을 만듭니다는 **Contact Email** 도메인으로 끝나는 경우 전자 메일 주소를 확인 하려면 **@adventure-works.com**합니다. 이 페이지에 대한 자세한 내용은 [도메인 규칙 만들기](https://msdn.microsoft.com/library/hh510397.aspx) 항목을 참조하십시오.  
  
1.  **도메인 목록** 에서 **Contact Email**을 클릭합니다.  
  
2.  오른쪽 창에서 **도메인 규칙** 으로 전환합니다.  
  
     ![새 도메인 규칙 도구 모음 단추 추가](../../2014/tutorials/media/et-settingdomainrules-01.jpg "새 도메인 규칙 도구 모음 단추 추가")  
  
3.  오른쪽 창의 도구 모음에서 **새 도메인 규칙 추가** 단추를 클릭하여 규칙을 추가합니다.  
  
4.  **규칙 이름** 에 **Email Validation** 을 입력하고 **Enter**키를 누릅니다. **활성** 확인란은 기본적으로 선택되어 있어야 합니다. 이 컨트롤을 사용하면 규칙을 일시적으로 비활성화할 수 있습니다.  
  
5.  **규칙 작성** 창에서 **아래쪽 화살표**를 클릭하고 **값이 다음으로 종료**를 선택합니다.  
  
6.  형식 **@adventure-works.com** 텍스트 상자에 키를 눌러 **탭**합니다. **규칙 작성** 창에서 **선택한 절에 새 조건 추가** 도구 모음 단추를 클릭하여 조건을 추가할 수 있습니다.  
  
     ![유효성 검사 규칙을 전자 메일](../../2014/tutorials/media/et-settingdomainrules-02.jpg "메일 유효성 검사 규칙")  
  
7.  오른쪽 창의 도구 모음에서 **테스트 데이터에서 선택한 도메인 규칙 실행** 단추를 클릭하여 예제 데이터로 규칙을 테스트합니다.  
  
     ![테스트 데이터 도구 모음 단추에서 도메인 규칙 실행](../../2014/tutorials/media/et-settingdomainrules-03.jpg "테스트 데이터 도구 모음 단추에서 도메인 규칙 실행")  
  
8.  **도메인 규칙 테스트** 대화 상자의 도구 모음에서 **도메인 규칙에서 새 테스트 용어를 추가합니다.** 단추를 클릭합니다.  
  
     ![도메인 규칙 대화 상자를 테스트할](../../2014/tutorials/media/et-settingdomainrules-04.jpg "도메인 규칙 대화 상자 테스트")  
  
9. 형식 **frank7@adventure-works.com** (유효 값)에 **Contact Email** 열입니다.  
  
10. 이전 두 단계를 반복 추가 **joe2@adventure-work.com** (no 사용 하 여 잘못 된 값의 ').  
  
11. 도구 모음에서 마지막 단추(**모든 용어에 대한 도메인 규칙을 테스트합니다.**)를 클릭하여 규칙에 대해 입력 데이터를 테스트합니다.  
  
     ![모든 조건 도구 모음 단추에서 도메인 규칙 테스트](../../2014/tutorials/media/et-settingdomainrules-05.jpg "모든 조건 도구 모음 단추에서 도메인 규칙 테스트")  
  
12. 첫 번째 항목은 유효한 항목으로 표시되고 두 번째 항목은 잘못된 항목으로 표시됨을 알 수 있습니다.  
  
     ![도메인 규칙 테스트 결과](../../2014/tutorials/media/et-settingdomainrules-06.jpg "도메인 규칙 테스트 결과")  
  
13. **닫기** 를 클릭하여 **도메인 규칙 테스트** 대화 상자를 닫습니다.  
  
## <a name="next-step"></a>다음 단계  
 [작업 5: 용어 기반 관계 설정](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  
