---
title: 페이지 번호 또는 기타 보고서 속성 표시(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: c7d95245-4709-4d04-acb4-59bf71e60d97
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0f9e826ff115183180ad42a1c065619f2196cd3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580888"
---
# <a name="display-page-numbers-or-other-report-properties-report-builder-and-ssrs"></a>페이지 번호 또는 기타 보고서 속성 표시(보고서 작성기 및 SSRS)
  보고서의 페이지 머리글이나 바닥글에 페이지 번호, 보고서 제목, 파일 이름 및 기타 보고서 속성을 간단히 추가할 수 있습니다. 다음은 보고서 데이터 창의 기본 제공 필드 폴더에 필드로 저장되는 속성입니다.  
  
-   실행 시간  
  
-   페이지 번호  
  
-   보고서 폴더  
  
-   보고서 이름  
  
-   보고서 서버 URL  
  
-   전체 페이지 수  
  
-   사용자 ID  
  
-   언어  
  
 페이지 번호의 경우 번호 뒤에 "페이지"라는 단어를 추가할 수 있습니다. 총 페이지 수도 표시할 수 있습니다.  
  
> [!NOTE]  
>  바닥글에 총 페이지 수를 추가할 경우 보고서를 실행하거나 미리 볼 때 성능이 저하될 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-page-number-or-other-report-properties"></a>페이지 번호 또는 기타 보고서 속성을 추가하려면  
  
1.  보고서 데이터 창에서 기본 제공 필드 폴더를 확장합니다.  
  
    > [!NOTE]  
    >  보고서 데이터 창이 표시되지 않는 경우 보기 탭에서 **보고서 데이터**를 선택하세요.  
  
2.  **페이지 번호** 필드를 보고서 데이터 창에서 보고서 머리글이나 바닥글로 끌어옵니다.  
  
    > [!NOTE]  
    >  페이지 바닥글은 보고서에 자동으로 추가됩니다. 페이지 머리글을 추가하려면 **삽입** 탭에서 **머리글**을 클릭한 다음 **머리글 추가**를 클릭합니다.  
    >   
    >  간단한 식 [&PageNumber]가 포함된 입력란이 추가됩니다.  
  
### <a name="to-add-the-word-page-before-the-page-number"></a>페이지 번호 뒤에 "페이지"라는 단어를 추가하려면  
  
1.  [&PageNumber]가 들어 있는 입력란을 마우스 오른쪽 단추로 클릭한 다음 **식**을 클릭합니다.  
  
     **다음에 대한 식 설정: 값** 입력란에 식 =Globals!PageNumber가 포함됩니다.  
  
2.  = 기호 뒤에 커서를 두고 **"Page " &** 를 입력합니다.  
  
     식이 ="Page "&Globals!PageNumber로 바뀝니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-total-number-of-pages-after-the-page-number"></a>페이지 번호 뒤에 총 페이지 수를 추가하려면  
  
1.  식이 들어 있는 입력란을 마우스 오른쪽 단추로 클릭한 다음 **식**을 클릭합니다.  
  
2.  식 끝에 **&" of "&** 를 입력합니다.  
  
3.  범주 창에서 **기본 제공 필드** 를 확장한 다음 **TotalPages**를 두 번 클릭합니다.  
  
     식이 ="Page "&Globals!PageNumber &" of "&Globals!TotalPages로 바뀝니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [페이지 머리글 및 바닥글&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [입력란의 텍스트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
  
