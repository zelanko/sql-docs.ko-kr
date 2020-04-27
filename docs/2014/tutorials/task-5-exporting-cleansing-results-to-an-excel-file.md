---
title: '태스크 5: 정리 결과를 Excel 파일로 내보내기 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3c690becefb71b71c154131b6957c1063872b540
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489122"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>태스크 5: 정리 결과를 Excel 파일로 내보내기
  이 작업에서는 정리 작업의 결과를 Excel 파일로 내보냅니다. 자세한 내용은 [내보내기 단계](https://msdn.microsoft.com/library/hh213061.aspx#Export) 항목을 참조 하세요.  
  
1.  오른쪽 창에서 **대상 유형**으로 **Excel** 을 선택 합니다.  
  
2.  **찾아보기**를 클릭 하 고 출력 파일 이름을 **정리 된 공급자 목록 .xls**로 지정한 다음 **열기**를 클릭 합니다.  
  
3.  정리 된 데이터만 내보내려면 **출력** 형식에 대해서 **만 데이터** 를 선택 합니다. 두 번째 옵션인 **데이터 및 정리 정보**를 사용 하 여 정리 된 데이터와 함께 정리 작업 세부 정보를 내보낼 수 있습니다. **표준화 형식** 옵션을 사용 하면 도메인에서 정의한 모든 출력 형식을 해당 도메인의 값에 적용할 수 있습니다. 이 자습서에서는 어떠한 도메인에도 출력 형식을 정의하지 않았습니다.  
  
     ![정리 결과 내보내기 페이지](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "정리 결과 내보내기 페이지")  
  
4.  **내보내기** 를 클릭 하 여 데이터를 내보냅니다. 아직 **마침** 을 클릭 하지 마십시오.  
  
5.  **내보내기** 대화 상자에서 **닫기** 를 클릭 합니다.  
  
6.  **마침** 을 클릭하여 작업을 마칩니다. **마침**을 클릭 하기 전에 결과를 내보내지 않은 경우 **dqs 클라이언트**의 기본 페이지에서 **데이터 품질 프로젝트 열기** 를 클릭 하 고, 프로젝트 목록에서 **공급자 목록 정리** 를 선택 하 고, 화면 아래쪽에서 **다음** 을 클릭 하 여 정리 프로세스의 **내보내기** 단계로 이동 합니다. **뒤로** 단추를 클릭 하 여 **결과 관리 및 보기** 탭으로 전환할 수도 있습니다.  
  
7.  정리 된 **공급자 목록 .xls** 를 열고 다음을 수행 합니다.  
  
    1.  워크시트에서 adventure-work.com를 검색 하 여 adventure-work.com으로 끝나는 전자 메일 주소 (문자 ' 없음 ')가 없는지 확인 합니다.  
  
    2.  **Country** 열에 **USA** 값이 없는지 확인 합니다.  
  
    3.  **Los Angeles**로 검색하고 **State**가 **CA**로 설정되었는지 확인합니다.  
  
    4.  **동료**, **Corp.** 및 **inc.** 용어가 없는지 확인 합니다.  
  
    5.  스프레드시트에서 **주소 유효성 검사** 열을 삭제 하 고 excel 파일을 저장 합니다. 이 추가 열은 Address Validation 복합 도메인에 해당합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 6: Cleanse Supplier List 프로젝트에서 값 가져오기](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  
