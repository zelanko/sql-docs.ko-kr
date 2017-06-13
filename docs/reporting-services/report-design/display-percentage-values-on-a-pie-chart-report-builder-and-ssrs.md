---
title: "원형 차트 (보고서 작성기 및 SSRS)에서 백분율 값 표시 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6c0fdf9d1b694f2f6d49389e913d1c156ba77838
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>원형 차트에서 백분율 값 표시(보고서 작성기 및 SSRS)
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 페이지가 매겨진된 보고서 범례 기본적으로 범주 표시 합니다. 범례 또는 자체 원형 조각에 백분율 할 수 있습니다.   

![report-builder-pie-chart-preview-percents](../../reporting-services/media/report-builder-pie-chart-preview-percents.png)

 [자습서: 보고서 (보고서 작성기) 원형 차트 추가](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md) 이 샘플 데이터로 먼저 시도 하려는 경우 원형 조각에 백분율을 추가 하는를 안내 합니다.
 
  
## <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>원형 차트에 레이블로 백분율 값을 표시하려면  
  
1.  보고서에 원형 차트를 추가합니다. 자세한 내용은 [보고서에 차트 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)를 참조하세요.  
  
2.  디자인 화면에서 원형을 마우스 오른쪽 단추로 클릭하고 **데이터 레이블 표시**를 선택합니다. 원형 차트의 각 조각 내에 데이터 레이블이 표시됩니다.  
  
3.  디자인 화면에서 레이블을 마우스 오른쪽 단추로 클릭하고 **계열 레이블 속성**을 선택합니다. **계열 레이블 속성** 대화 상자가 표시됩니다.  
  
4.  **레이블 데이터** 옵션에 **#PERCENT** 를 입력합니다.  
  
5.  (선택 사항) 레이블 소수 자릿수를 지정 하려면 입력 "#PERCENT {P*n*}" 여기서  *n*  표시할 소수 자릿수의 수입니다. 예를 들어 소수 자릿수를 표시하지 않으려면 "#PERCENT{P0}"를 입력합니다.  
  
## <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>원형 차트의 범례에 백분율 값을 표시하려면  
  
1.  디자인 화면에서 원형 차트를 마우스 오른쪽 단추로 클릭하고 **계열 속성**을 선택합니다. **계열 속성** 대화 상자가 표시됩니다.  
  
2.  **범례**에서 **사용자 지정 범례 텍스트** 속성에 **#PERCENT** 를 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
* [자습서: 보고서 (보고서 작성기) 원형 차트 추가](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [원형 차트 &#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [차트의 범례 서식 지정 &#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
*  [원형 차트 외부에 데이터 요소 레이블 표시 &#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 
  
