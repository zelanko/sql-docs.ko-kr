---
title: 원형 차트에서 백분율 값 표시(보고서 작성기) | Microsoft Docs
description: Reporting Services 페이지를 매긴 보고서에서는 기본적으로 범례에 범주가 표시됩니다. 범례 또는 원형 조각 자체에서 백분율할 수 있습니다.
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ffa11ae9d6c0d539accb4bbf6d796019cbc3371e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75254604"
---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>원형 차트에서 백분율 값 표시(보고서 작성기 및 SSRS)
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 페이지가 매겨진 보고서에서 기본적으로 범례는 범주를 표시합니다. 범례 또는 원형 조각 자체에서 백분율할 수 있습니다.   

![report-builder-pie-chart-preview-percents](../../reporting-services/media/report-builder-pie-chart-preview-percents.png)

 [자습서: 보고서에 원형 차트 추가(보고서 작성기)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)는 이 샘플 데이터로 먼저 시도하려는 경우 원형 조각에 백분율을 추가하는 것을 안내합니다.
 
  
## <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>원형 차트에 레이블로 백분율 값을 표시하려면  
  
1.  보고서에 원형 차트를 추가합니다. 자세한 내용은 [보고서에 차트 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)를 참조하세요.  
  
2.  디자인 화면에서 원형을 마우스 오른쪽 단추로 클릭하고 **데이터 레이블 표시**를 선택합니다. 원형 차트의 각 조각 내에 데이터 레이블이 표시됩니다.  
  
3.  디자인 화면에서 레이블을 마우스 오른쪽 단추로 클릭하고 **계열 레이블 속성**을 선택합니다. **계열 레이블 속성** 대화 상자가 표시됩니다.  
  
4.  **레이블 데이터** 옵션에 **#PERCENT** 를 입력합니다.  
  
5.  (옵션) 레이블을 표시할 때 사용할 소수 자릿수를 지정하려면 "#PERCENT{P*n*}"를 입력합니다. 여기서 *n* 은 표시할 소수 자릿수입니다. 예를 들어 소수 자릿수를 표시하지 않으려면 "#PERCENT{P0}"를 입력합니다.  
  
## <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>원형 차트의 범례에 백분율 값을 표시하려면  
  
1.  디자인 화면에서 원형 차트를 마우스 오른쪽 단추로 클릭하고 **계열 속성**을 선택합니다. **계열 속성** 대화 상자가 표시됩니다.  
  
2.  **범례**에서 **사용자 지정 범례 텍스트** 속성에 **#PERCENT** 를 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
* [자습서: 보고서에 원형 차트 추가(보고서 작성기)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [원형 차트 &#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [차트의 범례 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
*  [원형 차트 외부에 데이터 요소 레이블 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 
  
