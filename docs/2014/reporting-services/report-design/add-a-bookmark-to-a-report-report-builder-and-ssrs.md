---
title: 보고서에 책갈피 추가(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f130562e-5673-40e3-8e01-de7227a21d41
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 33252d10da04299c4b4f4e6177745567335a5256
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206916"
---
# <a name="add-a-bookmark-to-a-report-report-builder-and-ssrs"></a>보고서에 책갈피 추가(보고서 작성기 및 SSRS)
  사용자 지정된 목차를 제공하거나 보고서의 사용자 지정된 내부 탐색 링크를 제공하려는 경우 보고서에 책갈피 또는 책갈피 링크를 추가합니다. 일반적으로 각 테이블 또는 차트나 테이블 또는 행렬에 표시된 고유한 그룹 값 등 사용자를 안내하려는 보고서 위치에 책갈피를 추가합니다. 사용자 고유의 문자열을 만들어 책갈피로 사용하거나 그룹의 경우 책갈피를 그룹 식으로 설정할 수 있습니다.  
  
 책갈피를 만든 후에는 사용자가 클릭하면 각 책갈피로 이동되는 보고서 항목을 추가할 수 있습니다. 이러한 항목은 일반적으로 입력란 또는 이미지입니다.  
  
 예를 들어 보고서에 색상별로 그룹화된 테이블이 표시되는 경우 그룹 식을 기반으로 책갈피를 그룹 머리글에 추가합니다. 그런 다음 색 값을 표시한 보고서의 시작 부분에 단일 입력란이 있는 테이블을 추가하고 해당 입력란에 책갈피 링크를 설정합니다. 색을 클릭하면 보고서가 해당 색의 그룹 머리글 행을 표시하는 페이지로 이동합니다.  
  
 모든 보고서 항목에 책갈피를 추가하고 입력란, 이미지 또는 차트의 계산된 계열과 같이 **동작** 속성이 있는 모든 항목에 책갈피 링크를 추가할 수 있습니다. 자세한 내용은 [동작 속성 대화 상자&#40;보고서 작성기 및 SSRS&#41;](../action-properties-dialog-box-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-bookmark"></a>책갈피를 추가하려면  
  
1.  보고서 디자인 뷰에서 책갈피를 추가할 입력란, 이미지, 차트 또는 기타 보고서 항목을 선택합니다. 선택한 항목의 속성이 속성 창에 나타납니다.  
  
2.  **책갈피**옆의 입력란에 이 책갈피의 레이블인 문자열을 입력합니다. 예를 들어 **BikePhoto** 를 보고서의 이미지에 대한 책갈피로 입력할 수 있습니다. 또는 식(**fx**) 단추를 클릭하여 열리는 **식** 대화 상자에서 레이블을 반환하는 식을 지정합니다. 그룹의 경우 입력하는 식이 그룹 식이어야 합니다.  
  
    > [!NOTE]  
    >  책갈피는 모든 문자열일 수 있지만 보고서에서 고유해야 합니다. 책갈피가 고유하지 않으면 해당 책갈피 링크 클릭 시 일치하는 첫 번째 책갈피가 사용됩니다.  
  
### <a name="to-add-a-bookmark-link"></a>책갈피 링크를 추가하려면  
  
1.  디자인 뷰에서 링크를 추가할 입력란, 이미지, 차트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  해당 보고서 항목에 대한 **속성** 대화 상자에서 **동작**을 클릭합니다.  
  
3.  **책갈피로 이동**을 선택합니다. 이 옵션에 대한 추가 섹션이 대화 상자에 나타납니다.  
  
4.  **책갈피 선택** 상자에서 책갈피 또는 책갈피를 반환하는 식을 입력하거나 선택합니다. 앞의 예제를 사용할 경우 **BikePhoto** 를 입력하여 보고서의 이미지에 대한 링크를 만듭니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  (옵션) 텍스트가 자동으로 링크와 비슷하게 서식이 지정되지는 않습니다. 텍스트의 경우 텍스트가 링크임을 나타내기 위해 텍스트 색과 효과를 변경하는 것이 좋습니다. 예를 들어 리본 메뉴의 홈 탭에 있는 **글꼴** 섹션에서 색을 파란색으로 변경하고 효과를 밑줄로 변경합니다.  
  
7.  링크를 테스트하려면 **실행** 을 클릭하여 보고서를 미리 본 다음, 이 링크를 설정한 보고서 항목을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [대화형 정렬, 문서 구조 및 링크&#40;보고서 작성기 및 SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
