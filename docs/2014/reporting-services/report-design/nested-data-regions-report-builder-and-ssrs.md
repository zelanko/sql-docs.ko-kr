---
title: 중첩된 데이터 영역(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 15c2bc9b-428a-47ac-9630-8dde925d0595
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7511a4b6a441d00ca51eb29daed29cef616e6473
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56297411"
---
# <a name="nested-data-regions-report-builder-and-ssrs"></a>중첩된 데이터 영역(보고서 작성기 및 SSRS)
  일반적으로 데이터 요약을 간결하게 표시하거나 데이터를 테이블이나 행렬 이외에 시각적인 방식으로도 표시하려는 경우 차트와 같은 한 데이터 영역을 행렬과 같은 다른 데이터 영역에 중첩할 수 있습니다.  
  
 예를 들어 행에서 대리점별로 그룹화되고 열에서 분기별로 그룹화된 판매 주문이 포함된 행렬( *테이블릭스*라고도 함)의 경우 모퉁이 셀에 테이블이나 차트를 추가하여 모든 상점의 판매 데이터를 요약하거나 행렬 열 머리글에 차트를 추가하여 열 데이터의 판매 기여도를 전체 판매에 대한 백분율로 표시할 수 있습니다.  
  
 ![rs_NestedDataRegion](../media/rs-nesteddataregion.gif "rs_NestedDataRegion")  
  
 이 그림에서 모퉁이 셀의 원형 차트와 행의 스파크라인 차트는 중첩된 데이터 영역입니다.  
  
 정의에 따르면 중첩된 데이터 영역은 동일한 보고서 데이터 세트를 기반으로 합니다. 서로 다른 데이터 세트를 기반으로 하는 데이터 영역은 중첩할 수 없습니다. 서로 다른 데이터 세트의 데이터를 표시하려면 드릴스루 보고서 또는 하위 보고서를 사용하세요. 자세한 내용은 [드릴스루, 드릴다운, 하위 보고서 및 중첩 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](drillthrough-drilldown-subreports-and-nested-data-regions.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-scope-for-a-nested-data-region"></a>중첩된 데이터 영역의 범위 이해  
 중첩된 데이터 영역의 데이터에 대한 범위는 부모 데이터 영역에 배치할 때 자동으로 정의됩니다. 예를 들어 테이블릭스 모퉁이 셀에 중첩된 차트의 데이터에 대한 범위는 데이터 세트, 테이블릭스 데이터 영역 및 차트 데이터 영역에 대해 필터가 적용된 후 테이블릭스 데이터 영역에 바인딩되는 데이터 세트의 데이터로 지정됩니다. 테이블릭스 셀에 중첩된 테이블릭스의 범위는 모퉁이 셀의 범위와 동일하지만 중첩된 셀의 행 및 열 그룹 멤버까지 범위가 확장됩니다(해당 그룹 필터 적용). 범위에 대한 자세한 내용은 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
 아래에서는 다음 테이블릭스 영역의 셀에 대한 범위를 설명합니다.  
  
-   **테이블릭스 모퉁이** 해당 범위는 데이터 집합 및 외부 테이블릭스에 필터와 정렬 식이 적용된 후 테이블릭스 데이터 영역에 연결된 데이터 영역의 데이터입니다.  
  
-   **테이블릭스 열 그룹** 데이터 집합, 외부 테이블릭스 및 열 그룹에 필터 및 정렬 식이 적용된 후 가장 안쪽 열 그룹의 데이터입니다.  
  
-   **테이블릭스 행 그룹** 데이터 집합, 외부 테이블릭스 및 행 그룹에 필터 및 정렬 식이 적용된 후 가장 안쪽 행 그룹의 데이터입니다.  
  
-   **테이블릭스 본문** 데이터 집합, 외부 테이블릭스 및 행과 열 그룹에 필터 및 정렬 식이 적용된 후 행 그룹과 열 그룹의 교차로 표현되는 가장 안쪽 그룹의 데이터입니다.  
  
 자세한 내용은 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](tablix-data-region-areas-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="nesting-a-chart-sparkline-or-data-bar-in-a-tablix"></a>테이블릭스에 차트, 스파크라인 또는 데이터 막대 중첩  
 테이블릭스 열 그룹 머리글 또는 그룹 바닥글 행이나 테이블릭스 본문 셀에 차트(스파크라인 또는 데이터 막대 포함)를 추가한 경우 차트에 전달되는 데이터의 범위는 해당 셀 데이터의 하위 집합입니다. 기본적으로 테이블릭스 셀에 차트를 추가하면 차트 차원이 확장되어 셀을 채웁니다.  
  
> [!NOTE]  
>  테이블릭스 셀에서 차트의 크기를 더 세밀하게 제어하려면 먼저 사각형에 차트를 추가한 다음 사각형을 테이블릭스 셀에 추가합니다.  
  
 기본적으로 차트 범례 색은 차트 계열의 데이터 요소 색에 따라 결정됩니다. 중첩된 차트 데이터 영역 모두에서 동일한 데이터 범주에 동일한 색을 사용하려면 사용자 지정 색을 사용하고 데이터에 대해 정렬 식을 설정해야 합니다. 자세한 내용은 [여러 셰이프 차트에 일관된 색 지정&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md) 및 [데이터 영역의 데이터 정렬&#40;보고서 작성기 및 SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="nesting-a-gauge-or-an-indicator-in-a-tablix"></a>테이블릭스에 계기 또는 표시기 중첩  
 테이블, 행렬 또는 목록 안쪽에 계기 또는 표시기를 중첩하여 KPI(핵심 성과 지표)를 표시할 수 있습니다. 테이블 안에 계기 또는 표시기를 배치하면 테이블릭스의 각 행에 대해 계기 또는 표시기가 렌더링됩니다. 테이블릭스에 표시기를 추가하는 방법에 대한 자세한 내용은 [표시기&#40;보고서 작성기 및 SSRS&#41;](indicators-report-builder-and-ssrs.md)를 참조하세요.  
  
### <a name="adding-a-gauge-to-a-tablix"></a>테이블릭스에 계기 추가  
 다음 두 가지 방법으로 테이블릭스 데이터 영역에 계기를 추가할 수 있습니다.  
  
-   테이블릭스 셀 안쪽을 클릭하고 계기를 삽입합니다. **계기 유형 선택** 대화 상자가 나타납니다. 계기 유형을 선택하면 선택한 테이블릭스 셀 안쪽에 계기 데이터 영역이 놓입니다. 계기에 서식을 지정하려면 테이블릭스의 크기를 조정해야 합니다.  
  
-   테이블 바깥쪽을 클릭하고 계기를 삽입합니다. **계기 유형 선택** 대화 상자가 나타납니다. 계기 유형을 선택하면 보고서의 왼쪽 위 모퉁이에 계기 데이터 영역이 놓입니다. 데이터를 추가하고 계기의 서식을 지정한 다음 테이블릭스 셀 안으로 끌어 놓습니다.  
  
 차트와 마찬가지로 계기로 전달된 데이터 세트는 해당 셀에 대한 데이터의 하위 세트를 범위로 사용합니다. 계기를 테이블릭스 셀 안쪽에 배치하면 계기는 항상 데이터 행 하나만 집계합니다.  
  
 테이블릭스의 데이터가 그룹화된 경우 테이블릭스 안에 중첩된 계기 데이터 영역은 자동으로 이 그룹을 상속하지 않습니다. 테이블릭스에 표시되는 정보와 같은 정보를 표시하려면 계기에 일치하는 그룹 식을 추가해야 합니다. 예를 들어 테이블릭스의 데이터가 Product로 그룹화되어 있는 경우 동일한 데이터를 표시하려면 Product 그룹 식을 계기에 추가해야 합니다. 자세한 내용은 [계기&#40;보고서 작성기 및 SSRS&#41;](gauges-report-builder-and-ssrs.md) 및 [데이터 영역에서 그룹 추가 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)를 참조하세요.  
  
 계기 눈금에 표시되는 최소값과 최대값을 설정해야 합니다. 계기의 최대값을 지정하려면 `=Max!MyField.Value`와 같은 식을 사용할 수 있습니다. 하지만 이 식은 셀의 데이터 범위 내에서만 계산되기 때문에 각 계기의 최대값은 테이블릭스의 모든 행에 대해 동일하지 않습니다. 이 때문에 테이블릭스의 계기 간 비교를 이해하기 어려울 수 있습니다. 최대값에 정적 값을 지정할 수도 있습니다. 그러면 테이블릭스 안의 모든 행에 이 최대값이 적용된 계기가 표시됩니다. 자세한 내용은 [계기의 최소값 또는 최대값 설정&#40;보고서 작성기 및 SSRS&#41;](set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)를 참조하세요.  
  
 계기에서 데이터가 너무 커질 경우에는 눈금 승수를 사용하여 표시되는 자릿수를 줄일 수 있습니다. 승수를 지정하려면 눈금을 마우스 오른쪽 단추로 클릭하고 **눈금 속성**을 선택합니다. **눈금 속성** 대화 상자가 열리면 **승수**의 값을 지정합니다.  
  
## <a name="nesting-a-table-or-matrix-and-a-chart-in-a-list"></a>목록에서 테이블 또는 행렬 및 차트 중첩  
 목록에 여러 데이터 영역을 중첩하려면 먼저 사각형을 추가한 다음 해당 사각형에 데이터 영역을 다시 추가합니다.  
  
 목록 데이터 영역에 대한 그룹을 정의한 다음 테이블릭스와 차트를 추가하여 동일한 데이터를 여러 가지 방식으로 표시할 수 있습니다. 이를 위해서는 포함된 테이블릭스와 차트에 동일한 그룹 및 정렬 식을 정의해야 합니다. 정의에 따르면 테이블릭스와 차트는 부모 목록 데이터 영역의 데이터 세트에 있는 데이터를 사용합니다.  
  
> [!NOTE]  
>  기본적으로 디자인 화면에 목록 데이터 영역을 추가하면 목록에 정보 행이 포함됩니다. 그룹 행을 추가하고 정보 행을 제거하는 방법으로 이 기본값을 변경할 수 있습니다. 자세한 내용은 [테이블릭스 데이터 영역의 유연성 살펴보기&#40;보고서 작성기 및 SSRS&#41;](exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)를 참조하세요.  
  
 자세한 내용은 [그룹 이해&#40;보고서 작성기 및 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md) 및 [테이블, 행렬 또는 목록 추가, 이동 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [계기&#40;보고서 작성기 및 SSRS&#41;](gauges-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [보고서 항목 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md)   
 [자습서: 보고서에 KPI 추가 &#40;보고서 작성기&#41;](../tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [계기의 눈금 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)  
  
  
