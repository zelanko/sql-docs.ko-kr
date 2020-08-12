---
title: 차트의 3D, 3D 가장자리 및 기타 효과(보고서 작성기) | Microsoft Docs
description: 보고서 작성기에서 어떻게 3D 효과를 사용하여 차트에 깊이를 제공하고 시각적 효과를 추가할 수 있는지 알아봅니다.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10156"
ms.assetid: 18ef2119-2931-43ae-9078-f39b460462dd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c9875133b3d3a07d26313f5e4c375e2233d10677
ms.sourcegitcommit: 93e4fd75e8fe0cc85e7949c9adf23b0e1c275465
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84255336"
---
# <a name="chart-effects---3d-bevel-and-other-report-builder"></a>차트 효과 - 3D, 3D 가장자리 및 기타(보고서 작성기)
  3D(3차원) 효과를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지가 매겨진 보고서의 차트에 깊이를 더하고 시각적 효과를 강화할 수 있습니다. 예를 들어 쪼개진 원형 차트에서 특정 조각을 강조하려는 경우 차트를 돌려 원근감을 변경함으로써 해당 조각이 가장 먼저 보이도록 할 수 있습니다. 차트에 3D 효과를 적용할 경우 모든 그라데이션 색과 해칭 스타일이 해제됩니다.  
  
 3차원 효과는 개별 차트에 적용할 수 있으며, 동일 보고서에서 2차원 및 3차원 차트를 모두 표시할 수 있습니다.  
  
 **3D 사용** 을 선택하면 모든 차트 종류에 대해 **차트 영역 속성**대화 상자의 차트 영역에 3차원 효과를 추가할 수 있습니다. 자세한 내용은 [차트에 3D 효과 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-effects-add-3d-effects-report-builder.md)대화 상자의 차트 영역에 3차원 효과를 추가할 수 있습니다.  
  
 가로 막대형 차트, 세로 막대형 차트, 원형 차트 및 도넛형 차트에 빗면 효과, 볼록 효과 및 질감 스타일을 추가하여 차트에 시각적 효과를 줄 수도 있습니다. 자세한 내용은 [차트에 빗면 효과, 볼록 효과 및 질감 스타일 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="coordinate-based-three-dimensional-charts"></a>좌표 기반 3차원 차트  
 좌표 기반 차트 종류(세로 막대형, 가로 막대형, 영역형, 점, 꺾은선형 및 범위형)를 사용할 경우 3차원 효과를 적용하면 "z축"이라는 세 번째 축이 표시됩니다. 이 세 번째 축을 사용하면 차트에 다양한 시각적 효과를 제공할 수 있습니다.  
  
### <a name="changing-the-white-space-in-a-3d-chart"></a>3D 차트에서 공백 변경  
 3차원 모드로 차트 영역을 표시할 때 각 계열은 차트의 z축을 따라 개별 행으로 표시됩니다. 각 계열 간의 간격을 변경하려면 3D 효과 대화 상자의 **요소 간격 깊이** 속성을 변경하여 차트의 요소 간격 깊이를 수정합니다.  
  
### <a name="changing-the-projection-of-a-3d-chart"></a>3D 차트의 투영 변경  
 3D 투영에는 오블리크 투영과 큐브 뷰 투영이라는 두 가지 종류가 있습니다. 차트에 오블리크 투영을 사용하면 2차원 차트에 깊이 차원이 추가됩니다. z축은 가로 축과 세로 축에서 동일한 각도로 그려지며 2차원 차트에서와 같이 상호 수직 상태를 유지합니다.  
  
 큐브 뷰 투영은 해당 시점에서 바라보는 것처럼 뷰 평면을 예측하고 다시 그려 차트를 변형시킵니다. **회전** 값은 뷰를 수평(0도)에서 수직(90도)까지 세로로 옮깁니다. **기울기** 값은 시점 각도를 왼쪽 또는 오른쪽으로 옮깁니다. 0 값은 차트를 2차원으로 볼 때와 동일합니다. **큐브 뷰** 값은 투영을 표시할 때 사용되는 왜곡의 비율을 정의합니다. 이 유형의 투영에서는 차트의 비례는 유지되지만 차트의 모양이 왜곡되므로 낮은 큐브 뷰를 사용하는 것이 가장 효과적입니다.  
  
> [!NOTE]  
>  오블리크 및 큐브 뷰 투영은 서로 별개의 투영 유형이므로 동일 차트에서 함께 사용할 수 없습니다.  
  
### <a name="clustering-data"></a>데이터 클러스터링  
 2D 차트에서는 여러 데이터 계열이 나란히 표시됩니다. 클러스터링은 3D 차트에서 각 계열을 별도의 행으로 표시합니다. 예를 들어 3개의 데이터 요소 계열을 포함하는 차트에서 클러스터링을 사용하면 이 3개의 각 계열이 z축을 따라 별도의 행에 표시됩니다. 기본적으로 3D로 표시되는 모든 차트 종류에는 클러스터링이 적용됩니다.  
  
 가로 막대형 및 세로 막대형 차트에서는 클러스터링을 해제할 수 있습니다. 클러스터링을 해제하면 여러 가로 막대 및 세로 막대 계열이 하나의 행으로 나란히 표시됩니다.  
  
## <a name="shape-based-three-dimensional-charts"></a>셰이프 기반 3차원 차트  
 셰이프 기반 차트 종류(원형, 도넛형, 깔때기형, 피라미드형)의 경우 사용할 수 있는 3차원 효과의 수가 더 적습니다. 셰이프 기반 차트 종류를 사용할 때는 회전 및 기울기 값만 변경할 수 있습니다.  
  
## <a name="rotations"></a>회전  
 차트는 가로 또는 세로로 -90도에서 90도까지 회전할 수 있습니다. 양수 수평 각도는 x축을 따라 시계 반대 방향으로 차트를 회전시키고, 양수 수직 각도는 y축을 따라 시계 방향으로 차트를 회전시킵니다.  
  
## <a name="highlighting-3d-effects"></a>3D 효과 강조  
 **음영** 속성을 통해 3D 차트에 강조 스타일을 추가할 수 있습니다. 이 속성은 차트 영역을 선택할 때 속성 창에 있는 Area3DStyle 아래에 표시됩니다. 단순 조명 스타일은 차트 영역 요소에 동일한 색상을 적용합니다. 현실적인 스타일은 지정된 조명 각도에 따라 차트 영역 요소의 색상을 바꿉니다.  
  
## <a name="see-also"></a>참고 항목  
 [차트의 축 레이블 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [차트에 3D 효과 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-effects-add-3d-effects-report-builder.md)  
  
  
