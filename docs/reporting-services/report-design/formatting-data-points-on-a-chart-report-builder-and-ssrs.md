---
title: 차트의 데이터 요소에 서식 지정(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10248"
- sql13.rtp.rptdesigner.serieslabelproperties.general.f1
ms.assetid: 08ec3818-f63a-4e89-b52c-750e47f48b85
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0481f39c0c047f401914e2c710a1f52c393bc335
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65580332"
---
# <a name="formatting-data-points-on-a-chart-report-builder-and-ssrs"></a>차트의 데이터 요소에 서식 지정(보고서 작성기 및 SSRS)
페이지가 매겨진 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서의 데이터 요소는 차트에서 가장 작은 개별 엔터티입니다. 셰이프 차트가 아닌 차트에서 데이터 요소는 차트 종류에 따라 다르게 표시됩니다. 예를 들어 선 계열은 하나 이상의 연결된 데이터 요소로 구성됩니다. 셰이프 차트에서 데이터 요소는 전체 차트를 구성하는 개별 조각 또는 세그먼트로 표현됩니다. 예를 들어 원형 차트에서는 각 조각이 데이터 요소입니다. 자세한 내용은 [차트 종류&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)를 참조하세요.  
  
 계열은 하나 이상의 데이터 요소로 구성됩니다. 기본적으로 모든 서식 옵션은 계열의 모든 데이터 요소에 적용됩니다. 개별 데이터 요소에 대한 속성을 지정하려면 런타임에 데이터 세트를 기반으로 개별 데이터 요소의 서식을 지정하는 계열의 필드나 식을 지정합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-tooltips-and-drillthrough-actions-to-data-points"></a>데이터 요소에 도구 설명 및 드릴스루 동작 추가  
 계열에서 **도구 설명** 속성의 값을 설정하여 각 데이터 요소에 도구 설명을 추가할 수 있습니다. 도구 설명을 표시하여 사용자에게 그룹 이름, 데이터 요소 값 및 계열 합계에 대한 데이터 요소의 백분율과 같은 데이터 요소에 대한 정보를 볼 수 있는 기능을 제공할 수 있습니다. 자세한 내용은 [계열에 도구 설명 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)를 참조하세요.  
  
 또한 계열의 데이터 요소에 대한 드릴스루 동작을 지정하여 다른 보고서나 URL을 표시할 수도 있습니다. 매개 변수를 전달하여 클릭한 데이터 요소에 대한 정보를 표시할 수 있습니다. 자세한 내용은 [보고서에 드릴스루 동작 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="highlighting-individual-data-points-in-a-series"></a>계열의 개별 데이터 요소 강조 표시  
 셰이프 차트가 아닌 차트에서 Color 속성에 대한 식을 지정하여 개별 데이터 요소를 강조 표시할 수 있습니다. 예를 들어 이름이 `MyField` 인 계열에서 가장 높은 데이터 요소 값을 다른 데이터 요소와는 다른 색으로 강조 표시하기 위한 식은 다음과 유사합니다.  
  
 `=Iif(Fields!MyField.Value >= Max(Fields!MyField.Value, "MyDataSet"), "Red", "Green")`  
  
 이 예에서 `MyField` 에 대해 가장 높은 값은 빨강으로 표시되고 나머지 데이터 요소는 녹색으로 표시됩니다. 계열의 **채우기** 속성을 사용하여 계열에 대한 색을 지정하면 차트에서 색상표에서 지정된 색을 덮어씁니다. 자세한 내용은 [차트에서 계열 색 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)을 클릭합니다.  
  
## <a name="positioning-data-point-labels-on-a-chart"></a>차트에서 데이터 요소 레이블 위치 지정  
 모든 차트 종류에서 차트를 마우스 오른쪽 단추로 클릭하고 **데이터 레이블 표시**를 선택하면 데이터 요소 레이블을 표시할 수 있습니다. 데이터 요소 레이블의 위치는 다음과 같이 차트 종류에 따라 다른 방법으로 지정됩니다.  
  
-   가로 막대형 차트의 경우 **BarLabelStyle** 사용자 지정 특성을 사용하여 데이터 요소 레이블의 위치를 변경할 수 있습니다. 4가지 가능한 위치는 바깥쪽, 왼쪽, 가운데 및 오른쪽입니다. 막대 레이블 스타일을 Outside로 설정하면 레이블이 차트 영역 내에서 막대의 바깥쪽으로 배치됩니다. 레이블의 위치를 막대의 바깥쪽 및 차트 영역의 안쪽으로 지정할 수 없으면 레이블이 막대 안쪽으로 배치됩니다.  
  
-   원형 차트의 경우 **PieLabelStyle** 사용자 지정 특성을 사용하여 데이터 요소 레이블의 위치를 변경할 수 있습니다. 데이터 요소 레이블의 위치를 지정할 때는 원형 차트의 크기, 원형 차트와 해당 범례 사이의 가용 공간 및 레이블의 크기 등 다양한 요소를 고려해야 합니다. 자세한 내용은 [원형 차트 외부에 데이터 요소 레이블 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)를 참조하세요.  
  
-   피라미드형 또는 깔때기형 차트에서는 **FunnelLabelStyle** 및 **PyramidLabelStyle** 사용자 지정 특성을 사용하여 데이터 요소 레이블의 위치를 지정할 수 있습니다. 피라미드형 또는 깔때기형 차트 종류를 선택한 경우 **속성** 창에서 이러한 특성을 설정할 수 있습니다.  
  
-   누적 차트에서 데이터 요소 레이블은 항상 계열 안쪽에 배치되며 계열의 **위치** 속성은 무시됩니다.  
  
-   다른 모든 차트 종류의 경우 계열 레이블의 **위치** 속성을 사용하여 데이터 요소 레이블의 위치를 변경할 수 있습니다. 기본적으로 차트는 레이블 겹침을 피하기 위해 데이터 요소 레이블의 위치를 자동으로 계산합니다. **위치**값을 설정하면 모든 데이터 요소 레이블의 위치가 같은 방법으로 지정되어 레이블 겹침이 발생할 수 있습니다. 적은 수의 데이터 요소가 있는 경우에만 이 방법을 사용하는 것이 좋습니다.  
  
 자세한 내용은 [차트의 레이블 위치 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/position-labels-in-a-chart-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="adding-keywords-for-data-point-labels-tooltips-and-legend-text"></a>데이터 요소 레이블, 도구 설명 및 범례 텍스트의 키워드 추가  
 대/소문자를 구분하는 차트 관련 키워드를 사용하여 차트에 있는 항목을 표현할 수 있습니다. 이러한 키워드는 도구 설명, 사용자 지정 범례 텍스트 및 데이터 요소 레이블 속성에만 적용할 수 있습니다. 대부분의 경우 차트 키워드에도 동일한 단순 식이 있지만 키워드를 입력하는 것이 더 빠르고 간편합니다. 다음은 차트 키워드 목록입니다.  
  
|차트 키워드|Description|적용 가능한 차트 종류|동일한 단순 식의 예|  
|-------------------|-----------------|------------------------------|------------------------------------------------|  
|#VALY|데이터 요소의 Y 값|모두|`=Fields!MyDataField.Value`|  
|#VALY2|데이터 요소의 Y 값 #2|범위, 거품형|None|  
|#VALY3|데이터 요소의 Y 값 #3|주식형, 원통형|None|  
|#VALY4|데이터 요소 #4의 Y 값|주식형, 원통형|None|  
|#SERIESNAME|계열 이름|모두|None|  
|#LABEL|데이터 요소 레이블|모두|None|  
|#AXISLABEL|축 데이터 요소 레이블|셰이프|`=Fields!MyDataField.Value`|  
|#INDEX|데이터 요소 인덱스|모두|None|  
|#PERCENT|데이터 요소 Y 값의 백분율|모두|`=FormatPercent(Fields!MyDataField.Value/Sum(Fields!MyDataField.Value, "MyDataSet"),2)`|  
|#TOTAL|계열의 모든 Y 값에 대한 합계|모두|`=Sum(Fields!MyDataField.Value)`|  
|#LEGENDTEXT|범례 항목의 텍스트에 해당하는 텍스트|모두|None|  
|#AVG|계열의 모든 Y 값에 대한 평균|모두|`=Avg(Fields!MyDataField.Value)`|  
|#MIN|계열의 모든 Y 값에 대한 최소값|모두|`=Min(Fields!MyDataField.Value)`|  
|#MAX|계열의 모든 Y 값에 대한 최대값|모두|`=Max(Fields!MyDataField.Value)`|  
|#FIRST|계열의 모든 Y 값에 대한 첫 번째 값|모두|`=First(Fields!MyDataField.Value)`|  
  
 키워드 형식을 지정하려면 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 형식 문자열을 괄호로 묶습니다. 예를 들어 도구 설명에서 데이터 요소의 값을 두 소수 자릿수를 포함하는 숫자로 지정하려면 계열의 **도구 설명** 속성에 대해 "#VALY{N2}"와 같이 형식 문자열 "N2"를 중괄호로 묶습니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 형식 문자열에 대한 자세한 내용은 MSDN의 [형식 지정(Formatting Types)](https://go.microsoft.com/fwlink/?LinkId=112024) 을 참조하십시오. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 숫자 형식을 지정하는 방법에 대한 자세한 내용은 [숫자 및 날짜 형식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)를 참조하세요.  
  
 차트에 키워드를 추가하는 방법에 대한 자세한 내용은 [계열에 도구 설명 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md), [범례 항목의 텍스트 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)를 참조하세요.  
  
## <a name="increasing-readability-in-a-chart-with-multiple-data-points"></a>여러 데이터 요소를 사용하여 차트의 가독성 향상  
 차트에 여러 계열이 있는 경우 차트 데이터 요소의 가독성이 떨어질 수 있습니다. 차트에 여러 계열을 추가할 때는 차트에서 각 계열을 읽고 이해하기 쉽게 구분해 주는 방법을 고려하는 것이 좋습니다. 자세한 내용은 [차트의 여러 계열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md)을 참조하세요.  
  
 간단히 하기 위해 셰이프 차트를 사용할 때 하나의 데이터 필드와 하나의 범주 필드만 추가하십시오. 자세한 내용은 [셰이프 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)를 참조하세요. 차트에 데이터 필드와 범주 필드가 두 개 이상 필요한 경우 차트 종류를 변경하는 것이 좋습니다. 계열을 마우스 오른쪽 단추로 클릭하고 **차트 종류 변경**을 선택할 수 있습니다.  
  
## <a name="inserting-data-point-markers"></a>데이터 요소 표식 삽입  
 데이터 요소 표식은 계열의 각 데이터 요소를 강조하기 위한 시각적 표시기입니다. 분산형 차트에서는 개별 데이터 요소의 모양과 크기를 결정하는 데 표식을 사용합니다. 표식의 크기는 차트 종류를 기준으로 지정됩니다. 표식의 크기, 색 또는 스타일을 변경할 수 있습니다. 범위/셰이프 차트 또는 누적 세로 막대형 하위 차트에서는 표식을 사용할 수 없습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [계열에 도구 설명 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
 [원형 차트 외부에 데이터 요소 레이블 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)  
  
 [원형 차트에서 백분율 값 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>참고 항목  
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [차트의 축 레이블 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [축 레이블의 서식을 날짜 또는 통화로 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [자습서: 보고서에 원형 차트 추가&#40;보고서 작성기&#41;](../../reporting-services/tutorial-add-a-pie-chart-to-your-report-report-builder.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
