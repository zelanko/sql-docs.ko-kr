---
title: '작업 5: 정리 결과 Excel 파일로 내보내기 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: aab1eff896ba602f118606b8f80894260e26f7ec
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028924"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>작업 5: 정리 결과를 Excel 파일로 내보내기
  이 작업에서는 정리 작업의 결과를 Excel 파일로 내보냅니다. 참조 [내보내기 단계](https://msdn.microsoft.com/library/hh213061.aspx#Export) 자세한 세부 정보에 대 한 항목입니다.  
  
1.  오른쪽 창에서 선택 **Excel** 에 대 한 합니다 **대상 유형**합니다.  
  
2.  클릭 **찾아보기**, 출력 파일 이름을 **Cleansed Supplier List.xls**를 클릭 하 고 **열기**합니다.  
  
3.  선택 **데이터만** 에 대 한 합니다 **출력** 정리한 데이터만 내보내려면 형식입니다. 두 번째 옵션인 **데이터 및 정리 정보**, 정리 된 데이터와 함께 정리 작업 세부 정보를 내보낼 수 있습니다. 합니다 **형식으로 표준화** 옵션 값을 해당 도메인의 도메인에서 정의한 모든 출력 서식을 적용할 수 있습니다. 이 자습서에서는 어떠한 도메인에도 출력 형식을 정의하지 않았습니다.  
  
     ![결과 페이지를 내보내기 정리](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "내보내기 정리 결과 페이지")  
  
4.  클릭 **내보내기** 데이터 내보냅니다. 클릭 하지 마세요 **완료** 아직 있습니다.  
  
5.  클릭 **닫습니다** 에 **내보내기** 대화 상자.  
  
6.  **마침** 을 클릭하여 작업을 마칩니다. 클릭 하기 전에 결과 내보내려면 않았다면 **완료**, 클릭 **데이터 품질 프로젝트 열기** 의 기본 페이지에서 **DQS 클라이언트**를 선택 **Cleanse Supplier 목록** 프로젝트를 하 고 목록에서 **다음** 이동 하려면 화면 맨 아래에 **내보내기** 정리 프로세스를 다시의 단계입니다. 으로 전환할 수 있습니다 **결과 관리 및 보기** 탭을 클릭 하 여 **다시** 단추입니다.  
  
7.  열기는 **Cleansed Supplier List.xls** 다음을 수행 합니다.  
  
    1.  Adventure-work.com으로 끝나는 전자 메일 주소가 있는지 확인 하십시오 (문자가 없음 ') 워크시트에서 adventure-work.com를 검색 합니다.  
  
    2.  이 없는 **USA** 값을 **국가** 열입니다.  
  
    3.  검색할 **Los Angeles** 되었는지 확인 합니다 **상태** 로 설정 되어 **CA**합니다.  
  
    4.  용어가 없는지 확인 **Co.** 하십시오 **Corp.**, 및 **Inc.** 합니다.  
  
    5.  삭제 된 **Address Validation** 열 스프레드시트에서 excel 파일을 저장 합니다. 이 추가 열은 Address Validation 복합 도메인에 해당합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 6: 값 가져오기는 Cleanse Supplier List 프로젝트](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  
