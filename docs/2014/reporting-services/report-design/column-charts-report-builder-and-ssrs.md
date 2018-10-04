---
title: 세로 막대형 차트(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ae8c138b-e356-4ad8-862c-a4a8d0c04149
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 5980f2f1213b0f74422cdac773e4dfa9c806fd5e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056443"
---
# <a name="column-charts-report-builder-and-ssrs"></a>세로 막대형 차트(보고서 작성기 및 SSRS)
  세로 막대형 차트에서 계열은 범주별로 그룹화된 일련의 세로 막대로 표시됩니다. 세로 막대형 차트는 기간에 따라 변경되는 데이터를 표시하거나 항목 간 차이를 설명하는 데 유용하게 사용할 수 있습니다. 일반 세로 막대형 차트는 가로 막대 집합으로 계열을 표시하는 가로 막대형 차트 및 시작점과 끝점이 다양한 세로 막대 집합으로 계열을 표시하는 범위형 세로 막대 차트와 밀접하게 연관되어 있습니다. 자세한 내용은 [가로 막대형 차트 &#40;보고서 작성기 및 SSRS&#41; ](charts-report-builder-and-ssrs.md) 하 고 [범위 형 차트 &#40;보고서 작성기 및 SSRS&#41;](range-charts-report-builder-and-ssrs.md).  
  
 세 계열이 모두 공통 기간을 공유하여 각 계열을 서로 비교하는 것이 가능하므로 이 데이터에는 세로 막대형 차트가 적합합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations-of-a-column-chart"></a>세로 막대형 차트의 변형  
  
-   **누적 가로 막대형**. 여러 계열을 세로로 누적하여 표시하는 세로 막대형 차트입니다. 차트에 계열이 하나만 있으면 누적 세로 막대형 차트는 세로 막대형 차트와 동일한 모양으로 표시됩니다.  
  
-   **100% 기준 누적 가로 막대형**. 차트 영역 전체에 꼭 맞도록 여러 계열을 세로로 누적하여 표시하는 세로 막대형 차트입니다. 차트에 계열이 하나만 있으면 모든 세로 막대가 차트 영역 전체에 맞게 표시됩니다.  
  
-   **3D 묶은 가로 막대형**. 3D 차트에서 각 계열을 별도의 행에 표시하는 세로 막대형 차트입니다.  
  
-   **3D 원통형**. 3D 차트에서 막대를 실린더 모양으로 표시하는 세로 막대형 차트입니다.  
  
-   `Histogram` 을 참조하세요. 막대가 정규 분포로 정렬되도록 차트를 계산하는 세로 막대형 차트입니다.  
  
-   `Pareto` 을 참조하세요. 가장 긴 막대에서 가장 짧은 막대 순서로 막대를 정렬하는 세로 막대형 차트입니다.  
  
## <a name="data-considerations-for-a-column-chart"></a>세로 막대형 차트의 데이터 고려 사항  
  
-   가로 막대형 및 세로 막대형 차트는 그룹 간의 비교에 매우 일반적으로 사용됩니다. 네 개 이상의 계열을 차트에 표시해야 하는 경우에는 누적 가로 막대형 또는 세로 막대형 차트를 사용하는 것이 좋습니다. 차트에 표시할 계열이 여러 개인 경우 누적 가로 막대형 또는 세로 막대형 차트를 여러 개의 그룹으로 묶을 수도 있습니다. 자세한 내용은 [가로 막대형 차트 &#40;보고서 작성기 및 SSRS&#41; ](charts-report-builder-and-ssrs.md) 하 고 *세로 막대형 차트*.  
  
-   세로 막대형 차트에서는 범주 축 레이블을 가로로 표시할 수 있는 공간이 충분하지 않습니다. 범주 레이블이 긴 경우 가로 막대형 차트를 사용하거나 레이블의 회전 각도를 변경하는 것이 좋을 수 있습니다.  
  
-   세로 막대형 차트의 개별 막대에 특별한 그리기 스타일을 추가하여 시각적 효과를 더욱 높일 수 있습니다. 그리기 스타일에는 쐐기형, 볼록, 원통형 및 그라데이션 효과 등이 있습니다. 이러한 효과는 2D 차트의 모양을 향상시킬 목적으로 디자인되었습니다. 3D 차트를 사용할 때도 그리기 스타일을 적용할 수는 있지만 그 효과는 다를 수 있습니다. 가로 막대형 차트에 그리기 스타일을 추가 하는 방법에 대 한 자세한 내용은 참조 하세요. [추가 3d 가장자리, 볼록 효과 및 질감 스타일 차트에 &#40;보고서 작성기 및 SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)합니다.  
  
-   세로 막대형 차트에서만 차트를 히스토그램 또는 파레토 차트로 표시할 수 있습니다. 이렇게 하려면 ShowColumnAs 속성을 설정 `Histogram` 나 `Pareto` 속성 창에서 `true`합니다.  
  
## <a name="see-also"></a>관련 항목  
 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [차트 종류&#40;보고서 작성기 및 SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [가로 막대형 차트 &#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [범위 형 차트 &#40;보고서 작성기 및 SSRS&#41;](range-charts-report-builder-and-ssrs.md)   
 [자습서: 보고서에 막대형 차트 추가&#40;보고서 작성기&#41;](../tutorial-add-a-bar-chart-to-your-report-report-builder.md)   
 [빈 데이터 요소 및 Null 데이터 요소 차트에서 &#40;보고서 작성기 및 SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
