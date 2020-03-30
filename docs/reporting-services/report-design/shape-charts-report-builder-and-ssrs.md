---
title: 셰이프 차트(보고서 작성기) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4b8404c1-aa89-4350-8bd6-203bc0446ee4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4e1d8d10837708b7cde4f83056a23a0e143662ab
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77080991"
---
# <a name="shape-charts-report-builder-and-ssrs"></a>셰이프 차트(보고서 작성기 및 SSRS)
  세이프 차트에서는 값 데이터를 전체의 백분율로 표시합니다. 셰이프 차트는 집합의 서로 다른 값이 차지하는 비율을 비교하여 표시하는 데 주로 사용됩니다. 범주는 셰이프의 개별 세그먼트로 표현됩니다. 세그먼트의 크기는 값에 따라 결정됩니다. 셰이프 차트는 원형 차트와 비슷하지만 범주를 가장 큰 것부터 가장 작은 것 순으로 정렬한다는 점에서 차이가 있습니다.  
  
 깔대기형 차트에서는 값을 점점 감소하는 비율로 표시합니다. 영역의 크기는 모든 값의 합계에 대한 계열 값의 비율로 결정됩니다. 예를 들어 웹 사이트 방문자 추세를 표시하는 데 깔대기형 차트를 사용할 수 있습니다. 이 경우 홈 페이지 방문자 수가 가장 많았던 시점을 나타내는 제일 넓은 영역이 깔대기형 차트의 맨 위에 표시되고 다른 영역은 크기에 비례하여 그 아래 표시됩니다. 깔때기형 차트에 데이터를 추가하는 방법에 대한 자세한 내용은 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)를 참조하세요.  
  
 다음 그림에서는 깔대기형 차트의 예를 보여 줍니다.  
  
 ![깔때기형 차트](../../reporting-services/report-design/media/rs-funnelchart.gif "깔때기형 차트")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>변형  
  
-   **피라미드형**. 피라미드형 차트에서는 차트가 피라미드 모양이 되도록 비례 데이터를 표시합니다.  
  
## <a name="data-considerations-for-shape-charts"></a>셰이프 차트의 데이터 고려 사항  
  
-   셰이프 차트는 시각적 효과가 뛰어나므로 보고서에 자주 사용됩니다. 그러나 셰이프 차트는 매우 단순한 종류의 차트이므로 데이터를 정확하게 표현하는 데 적합하지 않을 수 있습니다. 데이터를 집계하여 생성된 데이터 요소가 일곱 개 이하인 경우에만 셰이프 차트를 사용하는 것이 좋습니다. 일반적으로 셰이프 차트는 데이터 영역별로 범주를 하나만 표시하려는 경우에 사용합니다.  
  
-   셰이프 차트에서는 각 데이터 그룹을 차트의 개별 세그먼트로 표시합니다. 적어도 한 개 이상의 데이터 필드와 한 개 이상의 범주 필드를 추가해야 합니다. 셰이프 차트에 여러 개의 데이터 필드를 추가하면 셰이프 차트에서 두 데이터 필드가 동일한 차트에 표시됩니다.  
  
-   셰이프 차트는 백분율을 비례에 따라 정렬된 순서로 표시하는 데 가장 효과적입니다. 그러나 일관성을 유지하기 위해 이 차트에서는 기본적으로 데이터 세트의 값을 정렬하지 않습니다. 데이터를 깔때기형 또는 피라미드형으로 가장 정확하게 나타내려면 값을 내림차순으로 정렬하는 것이 좋습니다. 자세한 내용은 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)를 참조하세요.  
  
-   Null이거나, 비어 있거나, 음수이거나, 0인 값은 비율을 계산하는 데 영향을 주지 않습니다. 따라서 이러한 값은 셰이프 차트에 표시되지 않습니다. 이러한 유형의 값을 차트에서 시각적으로 표현하려면 셰이프 차트가 아닌 다른 차트 종류로 변경해야 합니다. 셰이프 이외의 차트에 빈 요소를 추가하는 방법에 대한 자세한 내용은 [차트에 빈 요소 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)를 참조하세요.  
  
-   사용자 지정 색상표를 사용하여 셰이프 차트의 색을 직접 정의하는 경우에는 쉽게 구분할 수 있는 고유한 색으로 각 데이터 요소를 강조 표시할 수 있도록 색상표에 다양한 색을 준비해야 합니다. 자세한 내용은 [차트에서 계열 색 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)을 클릭합니다.  
  
-   다른 모든 차트 종류와 달리 셰이프 차트에서는 개별 계열이 아니라 개별 데이터 요소를 범례에 표시합니다.  
  
-   깔대기형 차트에서는 값 및 범주 축 대한 설정이 무시됩니다. 여러 범주나 계열 그룹이 있으면 차트 범례에 그룹 레이블이 표시됩니다.  
  
-   셰이프 차트 종류는 동일한 차트 영역의 다른 어떠한 차트 종류와도 결합할 수 없습니다. 셰이프 차트에 표시된 데이터를 서로 비교하여 표시하려는 경우 데이터가 다른 종류의 차트에 표시되어 있으면 둘째 차트 영역을 추가해야 합니다.  
  
-   원형 및 도넛형 차트에 그리기 스타일을 추가로 적용하여 시각적 효과를 높일 수 있습니다. 자세한 내용은 [차트에서 계열 색 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [차트의 빈 데이터 요소 및 Null 데이터 요소&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [원형 차트 &#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
