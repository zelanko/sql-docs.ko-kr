---
title: '작업 4: 결과 관리 및 보기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ecc3ba7e-fecf-478f-8825-6e4764b00e99
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0e045d9722d380af19147746944c842f97ac9843
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186666"
---
# <a name="task-4-manaing-and-viewing-results"></a>태스크 4: 결과 관리 및 보기
  이 작업에서는 컴퓨터 기반 정리 결과를 검토하고 공급자 데이터에서 대화형 정리를 수행할 수도 있습니다. 참조 [대화형 정리 단계](http://msdn.microsoft.com/library/hh213061.aspx#Interactive) 내용을 확인 합니다.  
  
1.  선택 **Contact Email** 도메인 목록에서 도메인입니다.  
  
2.  전환 하는 **잘못 된** 오른쪽 창에서 탭 합니다. 두 개의 전자 메일 주소의 마지막에 's' 문자가 누락된 것을 확인할 수 있습니다. 유효 하지 않은 것으로 끝나는지 모든 전자 메일 주소가 도메인 규칙에 의해 발견 된 이러한 두 전자 메일 **@adventure-works.com** (으로 '). DQS는 정리 중 도메인 규칙을 사용해서 전자 메일이 올바른지 여부를 확인합니다. 이 탭에는 기술 자료에서 잘못된 것으로 표시되었거나 도메인 규칙에 위배되는 도메인 값이 표시됩니다. 여기에서 이 값들은 도메인 규칙(전자 메일 유효성 검사)에 위배됩니다.  
  
3.  에 **수정** 열을 올바른 전자 메일 주소으로 끝나는 입력 **@adventure-works.com** (으로 ').  
  
     ![전자 메일 유효성 검사 규칙에 따라 수정](../../2014/tutorials/media/et-managingandviewingresults-01.jpg "전자 메일 유효성 검사 규칙에 따라 수정")  
  
4.  클릭 **승인** 는 변경 내용을 승인할 레코드에 대 한 합니다. 레코드를 이동를 승인 하면는 **Corrected** 탭 합니다. 각 항목을 개별적으로 승인 하는 대신 사용 하 여 한 번에 모든 변경 내용을 승인할 수 있습니다는 **모든 용어를 승인** 도구 모음 단추입니다.  
  
5.  전환 하는 **새로** 오른쪽 창에서 탭 합니다. 이 탭의 값은 DQS가 기술 자료에서 값이 올바른지 여부를 확인하기에 아직 정보가 충분하지 않은 값입니다. 따라서 도메인 값을 변경하거나 변경을 제안할 수 없습니다.  
  
6.  모든 전자 메일 끝나야 확인 값을 검토 **@adventure-works.com** 클릭 **모든 용어를 승인** 도구 모음입니다. 이 탭에서 승인 된 값으로 이동 된 **올바름** 탭 합니다.  
  
7.  선택 된 **국가** 도메인 목록에서 도메인입니다.  
  
8.  전환 하는 **수정 됨** 오른쪽 창에 탭과 **United State** 값을 자동으로 수정 됩니다는 **미국** 와 ' 끝입니다. 이 규칙은 규칙에 대해 정의 된는 **국가** 도메인 아니지만 DQS는 **83%** 올바른 값이 확신 **미국**합니다. **승인** 단추 모든에 대해 자동으로 선택 됩니다는 **Corrected** 항목입니다. 이 동작을 재정의하고 변경 사항을 거부할 수 있습니다.  
  
9. 다음에 유의 **USA** 로 수정 **미국** 동의어 되기 때문에 및 **미국** 선행 (우선된) 값입니다.  
  
     ![동의어에 따라 수정 내용을](../../2014/tutorials/media/et-managingandviewingresults-02.jpg "동의어에 따라 수정 내용을")  
  
10. 에 **승인** 단추는 이러한 수정 된 값에 대해 이미 선택 됩니다. 이 동작은 수정된 값의 기본 동작입니다. 변경 사항을 거부할 수 있습니다 및 이렇게 하면를 이동 하는 값은 **잘못 된** 탭 합니다.  
  
11. 선택 **Supplier Name** 도메인 목록에서 합니다.  
  
12. 전환 하는 **Corrected** 오른쪽 창에서 탭 합니다.  
  
     ![수정 된 공급자 이름](../../2014/tutorials/media/et-managingandviewingresults-03.jpg "수정 된 공급자 이름")  
  
    1.  다음에 유의 **A. Datum Corp.** 로 수정 **A. Datum Corporation** 및 **이유** 로 설정 된 **용어 기반 관계로 합니다. A. datum Corporation** 기술 자료 검색 프로세스 중에 검색 되었기 때문에 DQS에 알려진된 도메인 값은입니다. 따라서 DQS는 **100% 신뢰도** 이 수정에 대 한 합니다.  
  
    2.  다음에 유의 하 **Lazy Country Storex** 로 수정 **Lazy Country Store**, **신뢰도 수준** 로 설정 된 **100%**, 및는  **이유** 로 설정 된 **도메인 값**합니다. 기술 자료 검색 프로세스 동안 설정 **Lazy Country Storex** 있는 오류로 **Lazy Country Store** 로 **수정**이므로 DQS는 **100% 확신** 이 수정 하는 방법에 대 한 합니다.  
  
    3.  DQS는 목록에서 다른 값에 잘 알고 있지만 사용 하 여 이러한 값에 대 한 수정 찾을 **맞춤법 검사기** 적절 한 수정 사항을 제안 하 고 있습니다. DQS는 **100%** 신뢰 수준은 하지만 이러한 수정 사항에 대 한 신뢰도 수정, DQS에서 수정 사항이 제안 하므로 임계 수준인 80% 이상입니다.  
  
13. 에 **승인** 모든 값에 대해 자동으로 설정 됩니다. 필요에 따라 수정된 값을 재정의하거나 변경 사항을 거부할 수도 있습니다. 기본적으로는 **승인** 단추를 선택 하는 모든 값에 **Corrected** 탭 합니다.  
  
14. 전환 하는 **새로** 탭 합니다.  
  
15. 다음에 유의 **Corp.** 로 수정 **Corporation**, **Co.** 로 수정 **회사**, 및 **Inc.** 로 수정 **Incorporated**합니다. 예를 들어 **Consolidate Inc.** 로 수정 **Consolidate Incorporated** 및 **Consolidated Co.** 로 수정 **Consolidated Company**, 및 **Frabrikam Corp.** 로 수정 **Fabrikam Corporation**합니다.  확인할 수 있습니다 **용어 기반 관계** 이유로 나와 있습니다. 이러한 변경 사항은 도메인 관리 작업 중 정의한 용어 기반 관계를 사용하여 제안됩니다. 변경할 수는 **수정** 여기 수동으로 값입니다.  
  
16. 참조 목록을 스크롤하여 **Hunxgry Coyote Store** 빨간색 구불구불한 선으로 합니다. 마우스 오른쪽 클릭 **Hungy Coyote Store** (없음 ' x')를 합니다. **수정** 열 자동으로 채워져야 할지 **Hungry Coyote Store**합니다. 또한 다음으로 수정 열에 값을 수동으로 입력할 수도 있습니다.  
  
17. 클릭 **모든 용어를 승인** 도구 모음에서 합니다. 된 도메인 값의 **수정** 지정 된 값으로 이동는 **수정 됨** 탭과 새 값과 연결 되지 않은 **수정** 값으로 이동는  **올바른** 탭 합니다.  
  
18. 선택 된 **Address Validation** 도메인 목록에서 복합 도메인입니다.  
  
19. 오른쪽 창에서로 전환 하는 **올바름** 탭 합니다. 표시 되어야 하 여 올바른 것으로 확인 하는 주소는 **Melissa Data – Address Check** DQS 서비스로 **Azure 마켓플레이스**합니다.  
  
20. 전환 하는 **Corrected** 탭 합니다.  
  
21. 다음에 유의 **상태** 있는 레코드에 대 한 **도시** 으로 **로스앤젤레스** 로 설정 된 **CA** 이제 합니다. 에 **이유** 하는 필드는 **규칙 ' City-State Rule'에 의해 수정**합니다.  
  
     ![City-State 규칙 수정](../../2014/tutorials/media/et-managingandviewingresults-04.jpg "City-State 규칙 수정")  
  
22. 에 **승인** 라디오 단추가 목록에이 항목에 대해 이미 선택 되어 있습니다. 이것은 항목에 대 한 기본 동작에는 **Corrected** 탭 합니다.  
  
23. 전환 하는 **제안** 탭 합니다. 에 제안 된 변경 내용을 검토 하 고 **Melissa Data – Address Check** 서비스입니다.  
  
24. **모든 용어 승인 클릭** 를 클릭 한 도구 모음 단추 **확인** 에 **확인** 메시지 상자.  
  
     ![모든 용어 도구 모음 단추 승인](../../2014/tutorials/media/et-managingandviewingresults-05.jpg "승인 모두 용어 도구 모음 단추")  
  
25. **다음** 을 클릭하여 **내보내기** 페이지로 전환합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 5: 정리 결과를 Excel 파일로 내보내기](../../2014/tutorials/task-5-exporting-cleansing-results-to-an-excel-file.md)  
  
  