---
title: 차트의 축 레이블 서식 지정(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10148"
- sql12.rtp.rptdesigner.calculatedseriesproperties.axeschartareas.f1
- "10142"
- sql12.rtp.rptdesigner.axisproperties.minortickmarks.f1
- "10143"
- sql12.rtp.rptdesigner.axisproperties.labels.f1
- "10145"
- sql12.rtp.rptdesigner.axistitleproperties.font.f1
- "10139"
- sql12.rtp.rptdesigner.axisproperties.labelfont.f1
- "10140"
- sql12.rtp.rptdesigner.axisproperties.majortickmarks.f1
- sql12.rtp.rptdesigner.axisproperties.line.f1
- "10141"
helpviewer_keywords:
- "10140"
ms.assetid: ddf50dd5-5314-42ff-97f4-c3a4a17cfcdd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a98a3496e237de1d4eeb530dfe5e22b70149890
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105851"
---
# <a name="formatting-axis-labels-on-a-chart-report-builder-and-ssrs"></a>차트의 축 레이블 서식 지정(보고서 작성기 및 SSRS)
  좌표 기반 차트 종류(세로 막대형, 가로 막대형, 영역형, 점, 꺾은선형 및 범위형)에는 데이터 관계를 범주화하고 표시하는 데 사용되는 두 개의 축이 있습니다. 각 축에는 다양한 유형의 서식이 지정됩니다.  
  
 **축 속성** 대화 상자를 사용하거나 속성 창을 사용하여 축 서식을 지정할 수 있습니다. 서식을 지정하려는 축을 마우스 오른쪽 단추로 클릭하고 **축 속성** 을 클릭하여 축 텍스트, 숫자와 날짜 형식, 주 눈금 표시와 보조 눈금 표시, 레이블 자동 맞춤, 그리고 축 선의 굵기, 색 및 스타일에 대한 값을 변경합니다. 축 제목의 값을 변경하려면 축 제목을 마우스 오른쪽 단추로 클릭하고 **축 제목 속성**을 클릭합니다.  
  
 축 레이블은 차트의 주 간격을 식별합니다. 기본적으로 차트는 텍스트 겹침을 방지할 수 있는 최적의 축 레이블 배치 방법을 결정하기 위한 알고리즘을 사용합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="types-of-axes"></a>축 유형  
 차트에는 값 축과 범주 축이라는 두 가지 기본 축이 있습니다.  
  
 ![차트의 범주 및 값 축](../media/rsaxes-categorical-vs-value.gif "차트의 범주 및 값 축")  
  
 데이터 세트에서 차트 화면으로 필드를 끌어서 놓으면 차트는 이 필드가 범주 축에 속하는지 값 축에 속하는지 확인합니다.  
  
 값 축은 일반적으로 차트의 세로 축, 또는 y축입니다. 이 축은 차트에 포함되는 숫자 데이터 값을 표시하는 데 사용됩니다. 데이터 필드 영역으로 끌어서 놓은 필드는 값 축에 표시됩니다. 범주 축은 일반적으로 차트에서 가로 축, 또는 x축입니다. 가로 막대형 차트에서는 축이 반대가 됩니다. 즉, 가로 막대형 차트 종류에서는 범주 축이 세로 축이고 값 축이 가로 축입니다. 자세한 내용은 [가로 막대형 차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="how-the-chart-calculates-axis-label-intervals"></a>차트에서 축 레이블 간격을 계산하는 방법  
 축 레이블의 서식을 지정하기 전에 차트에서 축 레이블 간격을 계산하는 방법을 이해해야 합니다. 이 방법을 이해하면 원하는 축 레이블 동작을 구현하는 데 필요한 속성을 설정할 수 있습니다.  
  
 축 눈금은 축을 따라 표시될 데이터 범위를 정의하는 최소값과 최대값으로 바인딩됩니다. 차트는 결과 집합의 값을 바탕으로 각 축에서 최소값과 최대값을 계산합니다. 값 축에서 눈금은 항상 값 필드의 가장 작은 수와 가장 큰 수에 의해 결정됩니다. 범주 축에서 최소값과 최대값 형식은 범주 필드의 형식에 따라 결정됩니다. 데이터 세트의 모든 필드는 세 가지 범주 필드 유형 중 하나로 분류할 수 있습니다. 다음 표에서는 이러한 세 가지 유형의 범주 필드에 대해 설명합니다.  
  
|범주 필드 유형|Description|예제|  
|-------------------------|-----------------|-------------|  
|숫자|범주는 x축을 따라 숫자순으로 표시됩니다.|x축을 따라 직원 ID 번호를 표시하는 직원 ID 번호별 판매 보고서|  
|날짜/시간|범주는 시간순으로 x축을 따라 표시됩니다.|x축을 따라 서식이 지정된 날짜를 표시하는 월별 판매 보고서|  
|문자열|범주는 데이터 원본에 처음 나타나는 순서대로 x축을 따라 표시됩니다.|x축을 따라 지역 이름을 표시하는 지역별 판매 보고서|  
  
 두 개의 축이 있는 모든 차트 종류는 깔끔한 차트 이미지를 만들고 레이블이 겹치지 않도록 하기 위해 범주가 너무 많을 경우 일부 축 레이블을 표시하지 않도록 설계되었습니다.  
  
 애플리케이션에서는 다음 단계에 따라 축에 레이블을 배치하는 위치를 계산합니다.  
  
1.  결과 집합의 값을 기반으로 최소값과 최대값을 식별합니다.  
  
2.  이러한 최소값 및 최대값을 기반으로 축 간격의 등거리 수(일반적으로 4~6)가 계산됩니다.  
  
3.  축 레이블 속성을 기반으로 이러한 간격에 따라 레이블이 표시됩니다. 레이블 위치에 영향을 주는 속성에는 글꼴 크기, 레이블이 표시되는 각도, 텍스트 줄 바꿈 속성이 있습니다. 이러한 축 레이블 자동 맞춤 옵션은 변경할 수 있습니다.  
  
### <a name="example-of-how-the-chart-calculates-axis-labels"></a>차트가 축 레이블을 계산하는 방법의 예  
 다음 표에는 세로 막대형 차트에 표시될 샘플 판매 데이터가 있습니다. 이름 필드는 범주 그룹 영역에 추가되고 수량 필드는 값 역에 추가됩니다.  
  
|이름|수량|  
|----------|--------------|  
|Michael Blythe|229|  
|Jae Pak|112|  
|Ranjit Varkey Chudukatil|494|  
|Jillian Carson|247|  
|Linda Mitchell|339|  
|Rachel Valdez|194|  
  
 수량 필드는 값 축을 따라 표시됩니다. 최저값은 112, 최고값은 494입니다. 이 경우 차트는 눈금이 0에서 시작하고 500에서 끝나도록 계산을 합니다. 또한 균일한 간격(100)으로 5개의 수를 계산하여 0, 100, 200, 300, 400 및 500에 레이블을 만듭니다.  
  
 이름 필드는 범주 축을 따라 표시됩니다. 차트는 4~6개의 레이블을 계산하며 레이블이 충돌하지 않으면서 범주 축에 레이블을 맞추도록 자동 맞춤 설정을 계산합니다. 이러한 계산의 결과 일부 범주 레이블이 생략될 수 있습니다. 각 축에 대한 자동 맞춤 옵션을 개별적으로 재정의할 수 있습니다.  
  
## <a name="displaying-all-labels-on-the-category-axis"></a>범주 축에 모든 레이블 표시  
 값 축에서 축 간격은 차트의 데이터 요소를 일정하게 측정할 수 있도록 합니다. 그러나 범주 축에서는 이 기능 때문에 범주가 축 레이블 없이 표시될 수 있습니다. 대개 사용자는 모든 범주에 레이블을 표시하려고 합니다. 간격의 수를 1로 설정하여 모든 범주를 표시할 수 있습니다.  자세한 내용은 [축 간격 지정&#40;보고서 작성기 및 SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)을 클릭합니다.  
  
> [!NOTE]  
>  축의 자동 레이블 기능을 수동 간격으로 대체하면 차트는 이에 맞게 모든 다른 요소의 크기를 조정해야 합니다. 결과적으로 레이블의 크기나 위치 또는 차트의 다른 요소 크기에 예상하지 못한 결과가 발생할 수 있습니다.  
  
## <a name="variable-axis-intervals"></a>가변 축 간격  
 차트는 차트의 크기에 관계없이 5개 내외의 축 레이블 간격을 계산합니다. 넓거나 높은 차트에서는 한 축에 5개의 레이블만 표시하는 경우 각 레이블 사이에 넓은 공백이 나타날 수 있습니다. 이렇게 되면 축에서 각 데이터 요소의 값을 식별하기가 더 어려워집니다. 넓거나 높은 차트에서는 가변 축 간격을 설정하여 이러한 현상을 방지할 수 있습니다. 차트의 너비나 높이를 바탕으로 차트에서 해당 축에 따라 표시할 수 있는 최적의 레이블 수를 계산합니다. 자세한 내용은 [축 간격 지정&#40;보고서 작성기 및 SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)을 클릭합니다.  
  
## <a name="sorting-axis-values"></a>축 값 정렬  
 범주는 결과 집합에 나타나는 순서대로 x축을 따라 표시됩니다. 쿼리에 SORT 명령을 추가하거나 식을 사용하여 데이터 세트를 정렬하는 방법으로 그룹 순서를 변경할 수 있습니다. 차트 데이터 영역은 다른 모든 데이터 영역과 같은 방식으로 정렬됩니다. 데이터 정렬 방법은 [데이터 영역의 데이터 정렬&#40;보고서 작성기 및 SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="specifying-scalar-values-on-the-category-axis"></a>범주 축에 스칼라 값 지정  
 기본적으로 차트는 데이터 세트에서 유효한 값을 포함하는 데이터 요소에 대한 축 레이블만 표시합니다. 예를 들어 범주 축에 1, 2, 6 값이 있는 경우 차트에는 범주 1, 2, 6만 표시됩니다. 범주 값의 눈금을 유지하려면 스칼라 축을 사용하도록 차트를 지정하면 됩니다. 이 시나리오의 경우 데이터 세트에는 3~5 값이 없지만 차트의 x축에는 1~6에 대한 레이블이 표시됩니다.  
  
 스칼라 축은 다음 두 가지 방법으로 설정할 수 있습니다.  
  
-   **축 속성** 대화 상자에서 **스칼라 축** 옵션을 선택합니다. 이렇게 하면 데이터 그룹화 값이 없는 축 위치에 숫자 또는 날짜/시간 값이 추가됩니다. 자세한 내용은 [축 속성 대화 상자, 축 옵션&#40;보고서 작성기 및 SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)를 참조하세요.  
  
-   **계열 속성** 대화 상자의 **범주 필드** 옵션에 대한 필드를 선택하거나 식을 입력합니다. 차트는 지정한 범주 필드의 모든 값에 대해 축 간격을 추가합니다.  
  
## <a name="adding-or-removing-side-margins-from-the-category-axis"></a>범주 축에서 양쪽 여백 추가 또는 제거  
 가로 막대형, 새로 막대형 및 분산형 차트 종류의 경우 x축의 끝에 자동으로 양쪽 여백이 추가됩니다. 여백의 크기는 변경할 수 없습니다. 다른 모든 차트 종류에서는 양쪽 여백이 추가되지 않습니다. 자세한 내용은 [차트에서 여백 추가 또는 제거&#40;보고서 작성기 및 SSRS&#41;](add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)을 클릭합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [축 레이블의 서식을 날짜 또는 통화로 지정&#40;보고서 작성기 및 SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)  
  
 [차트의 레이블 위치 지정&#40;보고서 작성기 및 SSRS&#41;](position-labels-in-a-chart-report-builder-and-ssrs.md)  
  
 [축 간격 지정&#40;보고서 작성기 및 SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)  
  
 [차트에서 여백 추가 또는 제거&#40;보고서 작성기 및 SSRS&#41;](add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
 [로그 눈금 간격 지정&#40;보고서 작성기 및 SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>관련 항목  
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [차트의 데이터 요소에 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
  
  
