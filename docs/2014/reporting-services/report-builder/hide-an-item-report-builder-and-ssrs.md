---
title: 항목 숨기기(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.shared.visibility.f1
- "10503"
ms.assetid: 9d78f8de-959b-456f-8947-687fa6e2ba91
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a67d093576076e9822427773afb710c57f801827
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025494"
---
# <a name="hide-an-item-report-builder-and-ssrs"></a>항목 숨기기(보고서 작성기 및 SSRS)
  지정하는 보고서 매개 변수 또는 기타 식에 따라 항목을 숨기려면 보고서 항목의 표시 유형을 설정합니다.  
  
 드릴다운 보고서와 같은 경우 보고서에서 입력란을 클릭할 때 보고서 항목의 표시 유형이 설정/해제되도록 보고서를 디자인할 수도 있습니다. 자세한 내용은 [항목에 확장 또는 축소 동작 추가&#40;보고서 작성기 및 SSRS&#41;](../report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)를 참조하세요.  
  
 다음 절차에서는 상수 또는 식을 기반으로 보고서 항목을 렌더링된 보고서에서 표시하거나 숨기는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-hide-a-report-item"></a>보고서 항목을 숨기려면  
  
1.  보고서 디자인 뷰에서 보고서 항목을 마우스 오른쪽 단추로 클릭하고 해당 **속성** 페이지를 엽니다.  
  
    > [!NOTE]  
    >  전체 테이블 또는 행렬 데이터 영역을 선택하려면 데이터 영역을 클릭하여 선택하고 행, 열 또는 모퉁이 핸들을 마우스 오른쪽 단추로 클릭한 다음 **테이블릭스 속성**을 클릭합니다.  
  
2.   **표시 유형**을 클릭합니다.  
  
3.  **보고서를 처음 실행할 때**에서 보고서를 처음으로 볼 때 항목을 숨길지 여부를 지정합니다.  
  
    -   항목을 표시하려면 **표시**를 클릭합니다.  
  
    -   항목을 숨기려면 **숨기기**를 클릭합니다.  
  
    -   런타임에 평가되는 식을 지정하려면 **식에 따라 표시 또는 숨기기**를 클릭합니다. **식**대화 상자에서 식을 입력하거나 식( **fx** ) 단추를 클릭하여 식을 만듭니다.  
  
        > [!NOTE]  
        >  표시 유형에 대한 식을 지정할 때는 다음 이미지와 같이 보고서 항목의 Hidden 속성을 설정하게 됩니다. 평가 식은 값이 False일 때 보고서 항목을 표시하고 값이 True일 때 보고서 항목을 숨깁니다.   
        > ![Properties_Visibility 대화 상자 및 Hidden 속성](../media/hiddenproperty-propertiesvisibility.png "Properties_Visibility 대화 상자 및 Hidden 속성")  
  
4.  **확인** 을 두 번 클릭합니다.  
  
### <a name="to-hide-static-rows-in-a-table-matrix-or-list"></a>테이블, 행렬 또는 목록에서 정적 행을 숨기려면  
  
1.  보고서 디자인 뷰에서 테이블, 행렬 또는 목록을 클릭하여 행 및 열 핸들을 표시합니다.  
  
2.  행 핸들을 마우스 오른쪽 단추로 클릭한 다음 **행 표시 유형**을 클릭합니다. **행 표시 유형** 대화 상자가 열립니다.  
  
3.  표시 유형을 설정하려면 첫 번째 절차의 3-4단계를 따릅니다.  
  
### <a name="to-hide-static-columns-in-a-table-matrix-or-list"></a>테이블, 행렬 또는 목록에서 정적 열을 숨기려면  
  
1.  디자인 뷰에서 테이블, 행렬 또는 목록을 선택하여 행 및 열 핸들을 표시합니다.  
  
2.  열 핸들을 마우스 오른쪽 단추로 클릭한 다음 **열 표시 유형**을 클릭합니다.  
  
3.  **열 표시 유형** 대화 상자에서 첫 번째 절차의 3-4단계를 따릅니다.  
  
## <a name="see-also"></a>관련 항목  
 [드릴다운 동작&#40;보고서 작성기 및 SSRS&#41;](../report-design/drilldown-action-report-builder-and-ssrs.md)   
 [항목에 확장 또는 축소 동작 추가&#40;보고서 작성기 및 SSRS&#41;](../report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
