---
title: "날짜 또는 통화로 지정 (보고서 작성기 및 SSRS) 축 레이블의 서식을 지정 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e9a01a74-2f51-4b35-be3a-a6138568f6cf
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7b8f82c7824a44d46a282eca8d617fb12ac9ade5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs"></a>축 레이블의 서식을 날짜 또는 통화로 지정(보고서 작성기 및 SSRS)
올바른 형식의 DateTime 값을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서의 축에 표시하면 차트에 이러한 값이 일로 자동 표시됩니다. X축에 대해 월 또는 시간 간격과 같은 날짜/시간 간격을 지정하려면 축 레이블의 서식을 지정하고 축 간격 유형을 올바른 날짜 또는 시간 간격으로 설정해야 합니다.  
  
> [!NOTE]  
>  세로 막대형 차트와 분산형 차트에서는 가로 축 또는 X축이 범주 축이고 가로 막대형 차트에서는 세로 축 또는 Y축이 범주 축입니다.  
  
 시간 간격의 서식을 올바르게 지정하려면 X축에 표시되는 값이 <xref:System.DateTime> 데이터 형식이어야 합니다. 필드에 <xref:System.String>데이터 형식이 있는 경우 차트에서 간격이 날짜 또는 시간으로 계산되지 않습니다. 자세한 내용은 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)를 참조하세요.  
  
 Y축에 숫자 값을 추가하면 기본적으로 차트에 숫자가 표시되기 전에 해당 숫자에 형식이 지정되지 않습니다. 숫자 필드가 매출 수치인 경우 차트의 가독성을 높이기 위해 숫자의 형식을 통화로 지정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-format-x-axis-labels-as-monthly-intervals"></a>X축 레이블의 서식을 월 간격으로 지정하려면  
  
1.  차트의 가로 축 또는 X축을 마우스 오른쪽 단추로 클릭하고 **HorizontalAxis 속성**을 선택합니다.  
  
2.  **HorizontalAxis 속성** 대화 상자에서 **숫자**를 선택합니다.  
  
3.  **범주** 목록에서 **날짜**를 선택합니다. **유형** 목록에서 x축 레이블에 적용할 날짜 형식을 선택합니다.  
  
4.  **축 옵션**을 선택합니다.  
  
5.  **간격**에 **1**을 입력합니다. **간격 유형** 속성에서 **월**을 선택합니다.  
  
    > [!NOTE]  
    >  간격 유형을 지정하지 않으면 차트에서 간격이 날의 개념으로 계산됩니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-format-y-axis-labels-using-a-currency-format"></a>통화 형식을 사용하여 Y축 레이블의 서식을 지정하려면  
  
1.  차트의 세로 축 또는 Y축을 마우스 오른쪽 단추로 클릭하고 **VerticalAxis 속성**을 선택합니다.  
  
2.  **VerticalAxis 속성** 대화 상자에서 **숫자**를 선택합니다.  
  
3.  **범주** 목록에서 **통화**를 선택합니다. **기호** 목록에서 y축 레이블에 적용할 통화 형식을 선택합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [차트 &#40;의 축 레이블 서식 지정 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [차트 &#40; 서식 지정 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [로그 눈금 간격 &#40;를 지정 합니다. 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [축 간격 &#40;를 지정 합니다. 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  
  
  
