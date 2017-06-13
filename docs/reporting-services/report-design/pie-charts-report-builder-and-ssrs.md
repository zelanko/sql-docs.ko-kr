---
title: "원형 차트 (보고서 작성기 및 SSRS) | Microsoft Docs"
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
ms.assetid: 536efa9c-c6fb-4cdd-b41f-ff5382910bd7
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dfa24b2135c34e95dae65e0a6fee4bf5da6b3d16
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="pie-charts-report-builder-and-ssrs"></a>원형 차트(보고서 작성기 및 SSRS)
  원형 차트와 도넛형 차트는 데이터를 전체에 대한 비율로 표시합니다. 원형 차트는 그룹 간의 비교에 가장 일반적으로 사용됩니다. 원형 및 도넛형 차트는 피라미드형 및 깔때기형 차트와 마찬가지로 셰이프 차트라고 하는 차트 그룹으로 이루어집니다. 셰이프 차트에는 축이 없습니다. 셰이프 차트에 숫자 필드를 배치하면 차트에서 각각의 값이 전체 합계에 대해 차지하는 비율이 계산됩니다. 셰이프 차트에 대한 자세한 내용은 [셰이프 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)를 참조하세요.  
  
 다음 그림에서는 데이터 레이블을 백분율로 서식 지정한 3차원 원형 차트를 보여 줍니다.  범례는 오른쪽 중간에 배치되어 있습니다.  
  
 ![원형 차트](../../reporting-services/report-design/media/piechart.gif "원형 차트")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>변형  
  
-   **쪼개진 원형**. 모든 조각이 원의 중앙에서 떨어져 있는 원형 차트입니다. 모든 조각이 서로 분리되어 있는 쪼개진 원형 차트뿐 아니라 조각이 한 개만 따로 떨어져 있는 쪼개진 조각 차트를 만들 수도 있습니다.  
  
-   **도넛형**. 중앙에 빈 공간이 있는 원형 차트입니다.  
  
-   **쪼개진 도넛형**. 모든 조각이 도넛의 중앙에서 떨어져 있는 도넛형 차트입니다.  
  
-   **3차원 원형**. 3차원 스타일이 적용된 원형 차트입니다.  
  
-   **3차원 쪼개진 원형**. 3차원 스타일이 적용된 쪼개진 원형 차트입니다.  
  
## <a name="data-considerations-for-display-on-a-pie-chart"></a>원형 차트에 표시할 데이터 고려 사항  
  
-   원형 차트는 시각적 효과가 뛰어나므로 보고서에 자주 사용됩니다. 그러나 원형 차트는 매우 단순한 종류의 차트이므로 데이터를 정확하게 표현하는 데 적합하지 않을 수 있습니다. 데이터를 집계하여 생성된 데이터 요소가 일곱 개 이하인 경우에만 원형 차트를 사용하는 것이 좋습니다.  
  
-   원형 차트에서는 각 데이터 그룹을 차트의 개별 조각으로 표시합니다. 원형 차트에는 적어도 한 개 이상의 데이터 필드와 한 개 이상의 범주 필드를 추가해야 합니다. 원형 차트에 여러 개의 데이터 필드를 추가하면 원형 차트에서 두 데이터 필드가 동일한 차트에 표시됩니다.  
  
-   Null이거나, 비어 있거나, 음수이거나, 0인 값은 비율을 계산하는 데 영향을 주지 않습니다. 따라서 이러한 값은 원형 차트에 표시되지 않습니다. 이러한 유형의 값을 차트에서 시각적으로 표현하려면 원형 차트가 아닌 다른 차트 종류로 변경해야 합니다.  
  
-   사용자 지정 색상표를 사용하여 원형 차트의 색을 직접 정의하는 경우에는 쉽게 구분할 수 있는 고유한 색으로 각 데이터 요소를 표시할 수 있도록 색상표에 다양한 색을 준비해야 합니다. 자세한 내용은 [차트에서 계열 색 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)를 참조하세요.  
  
-   대부분의 다른 차트 종류와 달리 원형 차트에서는 개별 계열이 아니라 개별 데이터 요소를 범례에 표시합니다.  
  
-   원형 차트에서 각 비율을 제대로 비교하려면 적어도 두 개 이상의 값이 있어야 합니다. 원형 차트가 한 가지 색으로만 그려진다면 그룹의 기준으로 삼을 범주 필드를 추가했는지 확인해 보십시오. 원형 차트에 범주가 포함되어 있지 않으면 데이터 필드의 값이 한 개의 값으로 집계 및 표시됩니다.  
  
-   다른 모든 차트 종류와 마찬가지로 원형 차트에서는 기본 색상표에 들어 있는 색 값을 기준으로 색을 생성합니다. 따라서 보고서에 여러 개의 원형 차트를 사용하는 경우 원형 차트마다 데이터 요소를 표시하는 데 서로 다른 색이 적용될 수 있습니다. 보고서에 포함된 원형 차트가 여러 개이면 각 차트마다 동일한 색 구성을 유지하도록 각 범주 그룹에 대한 색을 수동으로 설정할 수 있습니다. 차트에서 색을 정의하는 방법에 대한 자세한 내용은 [차트에서 계열 색 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="applying-drawing-styles-to-a-pie-chart"></a>원형 차트에 그리기 스타일 적용  
 원형 차트에 특별한 그리기 스타일을 추가하여 시각적 효과를 더욱 높일 수 있습니다. 그리기 스타일에는 빗면 및 오목 효과가 있습니다. 이러한 효과는 2차원 원형 차트에서만 사용할 수 있습니다. 다음 그림에서는 원형 차트에 빗면 및 오목 그리기 스타일을 적용한 예를 보여 줍니다.  
  
 ![원형 그리기 스타일](../../reporting-services/report-design/media/rs-piedrawingeffects-concave2.gif "원형 그리기 스타일")  
  
 자세한 내용은 [차트에 빗면 효과, 볼록 효과 및 질감 스타일 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)를 참조하세요.  
  
## <a name="displaying-percentage-values-on-a-pie-chart"></a>원형 차트에 백분율 값 표시  
 다른 셰이프 차트와 마찬가지로 원형 차트는 전체 합계에 대해 각 부분이 차지하는 비율을 표시합니다. 따라서 원형 차트 레이블은 백분율로 서식 지정하는 것이 일반적입니다. 그러나 다른 차트 종류와의 일관성을 유지하기 위해 이 차트에서는 기본적으로 백분율 레이블을 표시하지 않습니다. 차트에서 값을 백분율로 표시하는 방법에 대한 자세한 내용은 [원형 차트에서 백분율 값 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)를 참조하세요. 보고서에서 숫자를 백분율로 서식 지정하는 방법에 대한 자세한 내용은 [숫자 및 날짜 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)을 참조하세요.  
  
 ![원형 차트 데이터 요소 레이블을 백분율로](../../reporting-services/report-design/media/rs-piechartpercentages.gif "원형 차트 데이터 요소 레이블을 백분율로")  
  
## <a name="preventing-overlapped-labels-on-a-pie-chart"></a>원형 차트에서 레이블 겹침 방지  
 원형 차트에 포함된 데이터 요소가 많으면 데이터 레이블이 겹칠 수 있습니다. 레이블이 겹치지 않도록 하는 데는 여러 가지 방법이 있습니다.  
  
-   데이터 요소 레이블의 글꼴 크기를 줄입니다.  
  
-   레이블에 더 많은 공간을 할애할 수 있도록 차트의 너비와 높이를 늘립니다.  
  
-   원형 차트 레이블을 차트 영역 바깥쪽에 표시합니다. 자세한 내용은 [원형 차트 외부에 데이터 요소 레이블 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)를 참조하세요.  
  
-   작은 원형 조각을 한 개의 조각으로 합칩니다.  
  
## <a name="consolidating-small-slices-on-a-pie-chart"></a>원형 차트에서 작은 조각 통합  
 원형 차트에 요소가 너무 많을 경우 데이터가 가려지거나 가독성이 떨어집니다. 데이터에 작은 데이터 요소가 많은 경우 여러 원형 조각을 수집하는 방법에는 두 가지가 있습니다.  
  
-   작은 데이터 조각을 원형 차트의 한 조각으로 수집합니다. 이 방법은 원형 차트에 나머지 데이터를 단순히 수집하는 "기타" 데이터 요소를 추가하는 경우 등에 유용합니다. 자세한 내용은 [원형 차트에서 작은 조각 수집&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)를 참조하세요.  
  
-   작은 조각을 보조 원형 차트로 수집합니다. 두 번째 원형 차트는 디자이너에 표시되지 않습니다. 대신 보고서 처리 중에 차트가 두 번째 원형 차트를 표시해야 할지 여부를 데이터 요소의 값을 기준으로 계산합니다. 표시해야 하는 경우 값이 다른 원형 차트에 추가됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [원형 차트 외부에 데이터 요소 레이블 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [원형 차트에서 작은 조각 수집&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)   
 [원형 차트에서 백분율 값 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)   
 [자습서: 보고서에 원형 차트 추가&#40;보고서 작성기&#41;](../../reporting-services/tutorial-add-a-pie-chart-to-your-report-report-builder.md)   
 [차트의 범례 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
 [차트의 빈 데이터 요소 및 Null 데이터 요소&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [차트에서 계열 색 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)  
  
  
