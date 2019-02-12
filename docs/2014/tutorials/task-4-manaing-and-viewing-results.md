---
title: '작업 4: 결과 관리 및 보기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ecc3ba7e-fecf-478f-8825-6e4764b00e99
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c719b7d4bcd9b792beaa59fdbcf69783d7d3259d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56042784"
---
# <a name="task-4-manaing-and-viewing-results"></a>작업 4: 결과 관리 및 보기
  이 작업에서는 컴퓨터 기반 정리 결과를 검토하고 공급자 데이터에서 대화형 정리를 수행할 수도 있습니다. 참조 [대화형 정리 단계](https://msdn.microsoft.com/library/hh213061.aspx#Interactive) 대 한 자세한 내용은 합니다.  
  
1.  선택 **Contact Email** 도메인 목록에서 도메인입니다.  
  
2.  으로 전환 합니다 **잘못 된** 오른쪽 창에서 탭 합니다. 두 개의 메일 주소를 알림 문자가 누락 된 ' 끝입니다. 모든 전자 메일 주소를 사용 하 여 종료 해야 하는 도메인 규칙에 의해 무효화 되도록 발견 된 이러한 두 전자 메일 **@adventure-works.com** (사용 하 여의 '). DQS는 정리 중 도메인 규칙을 사용해서 전자 메일이 올바른지 여부를 확인합니다. 이 탭에는 기술 자료에서 잘못된 것으로 표시되었거나 도메인 규칙에 위배되는 도메인 값이 표시됩니다. 여기에서 이 값들은 도메인 규칙(전자 메일 유효성 검사)에 위배됩니다.  
  
3.  에 **수정** 열, 형식 올바른 전자 메일 주소 끝나는 **@adventure-works.com** (사용 하 여의 ').  
  
     ![전자 메일 유효성 검사 규칙의 수정 사항이](../../2014/tutorials/media/et-managingandviewingresults-01.jpg "전자 메일 유효성 검사 규칙에 따라 수정")  
  
4.  클릭 **승인** 두 레코드 모두 변경 내용을 승인 합니다. 를 승인 하면 레코드를 이동 합니다 **수정 됨** 탭 합니다. 각 항목을 개별적으로 승인 하는 대신 사용 하 여 한 번에 모든 변경 내용을 승인할 수 있습니다 합니다 **모든 용어를 승인** 도구 모음 단추입니다.  
  
5.  으로 전환 합니다 **새로 만들기** 오른쪽 창에서 탭 합니다. 이 탭의 값은 DQS가 기술 자료에서 값이 올바른지 여부를 확인하기에 아직 정보가 충분하지 않은 값입니다. 따라서 도메인 값을 변경하거나 변경을 제안할 수 없습니다.  
  
6.  모든 전자 메일 끝나야 확인 값을 검토 **@adventure-works.com** 누릅니다 **모든 용어를 승인** 도구 모음에서 합니다. 이 탭에서 승인 된 값으로 이동 합니다 **올바름** 탭 합니다.  
  
7.  선택 된 **국가** 도메인 목록에서 도메인입니다.  
  
8.  전환할 합니다 **수정 됨** 오른쪽 창에서 탭 하 고 있음을 **United State** 값을 자동으로 수정 됩니다는 **미국** 사용 하 여의 ' 끝입니다. 이 규칙은 규칙에 대 한 정의 **국가** 도메인 하지만 DQS **83%** 올바른 값이 인지 확신할 **미국**합니다. 합니다 **승인** 단추 모두에 대 한 자동으로 선택 됩니다 합니다 **수정** 항목입니다. 이 동작을 재정의하고 변경 사항을 거부할 수 있습니다.  
  
9. 있음을 **USA** 로 수정 됩니다 **미국** 동의어 되므로 및 **미국** 선행 (우선된) 값입니다.  
  
     ![동의어를 기반으로 수정](../../2014/tutorials/media/et-managingandviewingresults-02.jpg "동의어를 기반으로 수정")  
  
10. 다음에 유의 합니다 **승인** 단추는 이러한 수정 된 값에 대해 이미 선택 합니다. 이 동작은 수정된 값의 기본 동작입니다. 변경 사항을 거부할 수 있습니다 하 고 이렇게 하면 값으로 이동 합니다 **잘못 된** 탭 합니다.  
  
11. 선택 **Supplier Name** 도메인 목록에서.  
  
12. 으로 전환 합니다 **수정 됨** 오른쪽 창에서 탭 합니다.  
  
     ![수정 된 공급자 이름](../../2014/tutorials/media/et-managingandviewingresults-03.jpg "수정 된 공급자 이름")  
  
    1.  있음을 **A. Datum Corp.** 로 수정 됩니다 **A. Datum Corporation** 하며 **이유** 로 설정 된 **용어 기반 관계입니다. A. datum Corporation** 은 지식 검색 프로세스 중에 검색 되었기 때문에 DQS에 알려진된 도메인 값입니다. DQS는 따라서 **100% 확신** 이 수정에 대 한 합니다.  
  
    2.  있음을 **Lazy Country Storex** 로 수정 됩니다 **Lazy Country Store**를 **신뢰도** 로 설정 되어 **100%**, 및를 **원인** 로 설정 되어 **도메인 값**합니다. 설정한 지식 검색 프로세스 중 **Lazy Country Storex** 를 사용 하 여 오류로 **Lazy Country Store** 으로 **수정**이므로 DQS는 **100% 확신할** 이 수정 하는 방법에 대 한 합니다.  
  
    3.  DQS는 목록의 다른 값을 사용 하 여 친숙 한 이지만 사용 하 여 이러한 값에 대 한 수정 합니다 **맞춤법 검사기** 하 고 적절 한 수정 사항을 제안 합니다. Dqs **100%** 신뢰도 수준 이지만 이러한 수정에 대 한 확신은 신뢰도 DQS 제안 된 수정에 대 한 임계값 수준인 80%를 초과 합니다.  
  
13. 다음에 유의 합니다 **승인** 모든 값에 대 한 자동으로 활성화 됩니다. 필요에 따라 수정된 값을 재정의하거나 변경 사항을 거부할 수도 있습니다. 기본적으로는 **승인** 에서 모든 값에 대 한 단추를 선택 합니다 **수정** 탭 합니다.  
  
14. 으로 전환 합니다 **새로 만들기** 탭 합니다.  
  
15. 있음을 **Corp.** 로 수정 됩니다 **Corporation**합니다 **Co.** 로 수정 됩니다 **회사**, 및 **Inc.** 로 수정 됩니다 **Incorporated**합니다. 예를 들어 **Consolidate Inc.** 로 수정 됩니다 **Consolidate Incorporated** 하 고 **Consolidated Co.** 으로 수정 되 **Consolidated Company**, 및 **Frabrikam Corp.** 로 수정 됩니다 **Fabrikam Corporation**합니다.  알 수 있습니다 **용어 기반 관계** 이유를 설명 합니다. 이러한 변경 사항은 도메인 관리 작업 중 정의한 용어 기반 관계를 사용하여 제안됩니다. 변경할 수 있습니다 합니다 **수정** 수동으로 여기 값입니다.  
  
16. 참조 목록을 스크롤하여 **Hunxgry Coyote Store** 빨간색 구불구불한 선으로 합니다. 마우스 오른쪽 단추로 클릭 하 고 클릭 **Hungy Coyote Store** ('x') 포함 합니다. 합니다 **수정** 열을 사용 하 여 자동으로 채워질 수 해야 **Hungry Coyote Store**합니다. 또한 다음으로 수정 열에 값을 수동으로 입력할 수도 있습니다.  
  
17. 클릭 **모든 용어를 승인** 도구 모음에서 합니다. 도메인 값을 합니다 **수정** 지정 된 값으로 이동 합니다 **수정 됨** 탭과 연결 되지 않은 사용 하 여 새 값 **수정** 값 이동는  **올바른** 탭 합니다.  
  
18. 선택 된 **Address Validation** 도메인 목록에서 복합 도메인입니다.  
  
19. 오른쪽 창에서 전환 하는 **올바름** 탭 합니다. 올바른 것으로 발견 되는 주소를 표시 합니다 **Melissa Data-Address Check** DQS 서비스로 합니다 **Azure Marketplace**합니다.  
  
20. 으로 전환 합니다 **수정 됨** 탭 합니다.  
  
21. 있음을 **상태** 이 있는 레코드에 대 한 **City** 으로 **Los Angeles** 로 설정 되어 **CA** 이제 합니다. 에 **이유** 필드에는 **규칙 ' City-State Rule'에 의해 수정**합니다.  
  
     ![City-State 규칙 수정](../../2014/tutorials/media/et-managingandviewingresults-04.jpg "City-State 규칙 수정")  
  
22. 다음에 유의 합니다 **승인** 라디오 단추는 목록에서이 항목에 대해 이미 선택 합니다. 이 항목에 대 한 기본 동작을 **수정 됨** 탭 합니다.  
  
23. 으로 전환 합니다 **제안** 탭 합니다. 제안한 변경 내용을 검토 합니다 **Melissa Data-Address Check** 서비스입니다.  
  
24. **모든 용어 승인 클릭** 도구 모음 단추를 클릭 **확인** 에 **확인** 메시지 상자입니다.  
  
     ![모든 조건 도구 모음 단추를 승인할](../../2014/tutorials/media/et-managingandviewingresults-05.jpg "모든 조건 도구 모음 단추를 승인 합니다.")  
  
25. **다음** 을 클릭하여 **내보내기** 페이지로 전환합니다.  
  
## <a name="next-step"></a>다음 단계  
 [작업 5: 정리 결과 Excel 파일로 내보내기](../../2014/tutorials/task-5-exporting-cleansing-results-to-an-excel-file.md)  
  
  
