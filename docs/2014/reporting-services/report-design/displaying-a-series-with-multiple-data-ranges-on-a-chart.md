---
title: 차트 (보고서 작성기 및 SSRS)에 데이터 범위가 여러 개 있는 계열 표시 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 45da3d39-278e-4760-a4b3-9932c9547cf2
caps.latest.revision: 11
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: deba57aaef05f5859f7a241fee0a3ca17c8362c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090604"
---
# <a name="displaying-a-series-with-multiple-data-ranges-on-a-chart-report-builder-and-ssrs"></a>차트에 데이터 범위가 여러 개 있는 계열 표시(보고서 작성기 및 SSRS)
  차트는 최소 계열 값과 최대 계열 값을 사용하여 축 배율을 계산합니다. 차트 계열에 두 개 이상의 데이터 범위가 포함되어 있으면 데이터 요소가 가려지고 몇 개의 데이터 요소만 차트에서 쉽게 볼 수 있습니다. 예를 들어 보고서에서 한 달 간의 하루 총 판매량을 표시한다고 가정합니다.  
  
 ![데이터 범위가 여러 개 있는 차트](../media/rs-multipledatarangeschart.gif "데이터 범위가 여러 개 있는 차트")  
  
 한 달 동안 하루 총 판매량은 대부분 10에서 40 사이에 분포했지만 4월 초의 판매량은 한 주 동안의 진행된 판촉 행사로 급등했습니다. 이러한 판매 데이터 변경으로 인해 데이터 요소가 균일하지 않게 배포되어 차트에 대한 전체 가독성이 떨어집니다.  
  
 가독성을 개선하기 위해 다음과 같이 여러 방식을 사용할 수 있습니다.  
  
-   **배율 구분선 사용**. 데이터가 두 개 이상의 데이터 범위 집합을 형성하는 경우 배율 구분선을 사용하여 범위 간격을 제거합니다. 배율 구분선은 계열에서 높은 값과 낮은 값 사이가 구분되도록 그리기 영역에 표시하는 줄무늬입니다.  
  
-   **불필요한 값 필터링**. 차트에 표시할 중요한 데이터 범위를 가리는 데이터 요소가 있는 경우 보고서 필터를 사용하여 원하지 않는 데이터 요소를 제거합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 차트에 필터를 추가하는 방법에 대한 자세한 내용은 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)를 참조하세요.  
  
-   **여러 계열 비교를 위해 각 데이터 범위를 개별 계열로 그리기**. 데이터 범위가 두 개 이상인 경우 데이터 범위를 개별 계열로 구분하십시오. 자세한 내용은 [차트의 여러 계열&#40;보고서 작성기 및 SSRS&#41;](multiple-series-on-a-chart-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="displaying-multiple-data-ranges-using-scale-breaks"></a>배율 구분선을 사용하여 여러 데이터 범위 표시  
 배율 구분선을 사용하면 차트 위에서 선을 그릴 위치가 계산됩니다. 배율 구분선을 그리기 위해 범위 사이를 충분히 구분해야 합니다. 기본적으로 차트의 25% 이상의 데이터 범위 사이가 구분되는 경우에만 배율 구분선을 추가할 수 있습니다.  
  
 ![배율 구분선을 포함하는 차트](../media/rs-multipledatarangeschart-scalebreak.gif "배율 구분선을 포함하는 차트")  
  
> [!NOTE]  
>  차트에서 배율 구분선의 배치 위치는 지정할 수 없습니다. 그러나 이 항목의 뒷부분에 설명되어 있는 대로 배율 구분선을 계산하는 방식은 수정할 수 있습니다.  
  
 데이터 범위 사이에 충분한 간격이 있어도 사용되는 배율 구분선이 표시되지 않는 경우 CollapsibleSpaceThreshold 속성을 25 미만의 값으로 설정할 수 있습니다. CollapsibleSpaceThreshold는 데이터 범위 사이에 필요한 축소 가능한 공간의 백분율을 지정합니다. 자세한 내용은 [차트에 배율 구분선 추가&#40;보고서 작성기 및 SSRS&#41;](add-scale-breaks-to-a-chart-report-builder-and-ssrs.md)를 참조하세요.  
  
 차트에서는 차트당 최대 5개의 배율 구분선을 지원하지만 두 개 이상의 배율 구분선을 표시하면 차트를 읽을 수 없게 될 수 있습니다. 데이터 범위가 두 개 이상인 경우 이 데이터를 표시하는 다른 방법을 사용하십시오. 자세한 내용은 [차트의 여러 계열&#40;보고서 작성기 및 SSRS&#41;](multiple-series-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="unsupported-scale-break-scenarios"></a>지원되지 않는 배율 구분선 시나리오  
 다음과 같은 차트 시나리오에서는 배율 구분선이 지원되지 않습니다.  
  
-   3차원 차트가 사용됩니다.  
  
-   로그 값 축이 지정되었습니다.  
  
-   값 축 최소 또는 최대가 명시적으로 설정되었습니다.  
  
-   이 차트 종류가 극좌표형, 방사형, 원형, 도넛형, 깔때기형, 피라미드형 또는 모든 누적 차트입니다.  
  
 배율 구분선이 있는 차트의 예는 예제 보고서로 제공됩니다. 이 샘플 보고서 및 기타 보고서를 다운로드하는 방법은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][보고서 작성기 및 보고서 디자이너 샘플 보고서](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
## <a name="see-also"></a>관련 항목  
 [차트에 여러 계열을 &#40;보고서 작성기 및 SSRS&#41;](multiple-series-on-a-chart-report-builder-and-ssrs.md)   
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [3D, 빗면 및 기타 효과 차트에 &#40;보고서 작성기 및 SSRS&#41;](chart-effects-3d-bevel-and-other-report-builder.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [축 속성 대화 상자, 축 옵션&#40;보고서 작성기 및 SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [원형 차트에서 작은 조각 수집 &#40;보고서 작성기 및 SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  