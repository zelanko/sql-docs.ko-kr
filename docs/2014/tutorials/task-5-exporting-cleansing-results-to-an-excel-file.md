---
title: '태스크 5: 정리 결과 Excel 파일로 내보내기 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f8a716d3b6c0007ceb89f36f23584bb4adb4f706
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080098"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>태스크 5: 정리 결과를 Excel 파일로 내보내기
  이 작업에서는 정리 작업의 결과를 Excel 파일로 내보냅니다. 참조 [내보내기 단계](http://msdn.microsoft.com/library/hh213061.aspx#Export) 자세한 세부 정보에 대 한 항목입니다.  
  
1.  오른쪽 창에서 선택 **Excel** 에 대 한는 **대상 형식**합니다.  
  
2.  클릭 **찾아보기**,으로 출력 파일 이름을 지정 **Cleansed Supplier List.xls**, 클릭 하 고 **열려**합니다.  
  
3.  선택 **데이터만** 에 대 한는 **출력** 정리한 데이터만 내보내려면 형식입니다. 두 번째 옵션 **데이터 및 정리 정보**, 정리 된 데이터와 함께 정리 작업 세부 정보를 내보낼 수 있습니다. **형식 표준화** 옵션을 사용 하면 해당 도메인의 값을 도메인에서 정의 하는 출력 형식을 적용 합니다. 이 자습서에서는 어떠한 도메인에도 출력 형식을 정의하지 않았습니다.  
  
     ![결과 페이지를 내보내기 정리](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "내보내기 정리 결과 페이지")  
  
4.  클릭 **내보내기** 데이터를 내보내려면 합니다. 클릭 하지 마십시오 **마침** 아직 합니다.  
  
5.  클릭 **닫기** 에 **내보내기** 대화 상자.  
  
6.  **마침** 을 클릭하여 작업을 마칩니다. 클릭 하기 전에 결과 내보내려면 잊은 경우 **마침**, 클릭 **데이터 품질 프로젝트 열기** 의 기본 페이지에서 **DQS 클라이언트**선택, **Cleanse Supplier 목록** 프로젝트 및 클릭의 목록에서 **다음** 하려면 화면 맨 아래에 **내보내기** 다시 정리 프로세스의 단계입니다. 으로 전환할 수 있습니다 **결과 관리 및 보기** 탭을 클릭 하 여 **다시** 단추입니다.  
  
7.  열기는 **Cleansed Supplier List.xls** 고 다음을 수행 합니다.  
  
    1.  워크시트에서 adventure-work.com으로 검색해서 adventure-work.com('s' 문자가 없음)으로 끝나는 전자 메일 주소가 없는지 확인합니다.  
  
    2.  이 없는 **USA** 값에 **국가** 열입니다.  
  
    3.  검색할 **로스앤젤레스** 했다는 보고는 **상태** 로 설정 된 **CA**합니다.  
  
    4.  용어가 없는지 확인 **Co.**, **Corp.**, 및 **Inc.** 합니다.  
  
    5.  삭제 된 **Address Validation** 열 스프레드시트에서 선택한 excel 파일을 저장 합니다. 이 추가 열은 Address Validation 복합 도메인에 해당합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 6: Cleanse Supplier List 프로젝트에서 값 가져오기](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  