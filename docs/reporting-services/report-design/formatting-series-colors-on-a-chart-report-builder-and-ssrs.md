---
title: "차트에서 계열 색 서식 지정(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10245"
- "10252"
- sql13.rtp.rptdesigner.serieslabelproperties.borders.f1
- sql13.rtp.rptdesigner.seriesproperties.borders.f1
ms.assetid: fe541501-cac5-47b1-b95f-c410db789190
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 691f319ecd8b3b9bf6788ff4ac8ea9df469f433f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="formatting-series-colors-on-a-chart-report-builder-and-ssrs"></a>차트에서 계열 색 서식 지정(보고서 작성기 및 SSRS)
  Reporting Services는 차트에 여러 개의 기본 제공 색상표를 제공하며, 사용자가 사용자 지정 색상표를 정의할 수도 있습니다. 기본적으로 차트는 기본 제공 **Pacific** 색상표를 사용하여 각 계열을 채웁니다. 이 색은 범례에도 나타납니다. 차트에 여러 개의 계열이 추가될 때는 색상표에서 색을 정의한 순서대로 차트가 계열에 색을 할당합니다.  
  
 색상표에 있는 색보다 계열 수가 더 많을 경우 차트는 색을 다시 사용하므로 두 계열의 색이 같을 수 있습니다. 각 데이터 요소에 색상표의 색이 할당되는 셰이프 차트를 사용하는 경우에 이러한 상황이 자주 발생합니다. 혼동을 피하려면 적어도 차트에 있는 계열 수만큼의 색이 있는 사용자 지정 색상표를 정의하십시오.  
  
 속성 창에서 새 색상표를 선택하거나 사용자 지정 색상표를 정의할 수 있습니다. 자세한 내용은 [색상표를 사용하여 차트에 대한 색 정의&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-built-in-palettes"></a>기본 제공 색상표 사용  
 Reporting Services에는 차트의 계열에 대한 색 집합을 정의하는 데 사용할 수 있는 미리 정의된 기본 제공 색상표 목록이 있습니다. 모든 기본 제공 색상표에는 10 - 16개의 색 값이 포함되어 있습니다. 더 많은 색을 포함하도록 기본 제공 색상표를 확장할 수는 없습니다. 따라서 16개가 넘는 색이 필요한 경우에는 사용자 지정 색상표를 정의해야 합니다.  
  
 보고서를 인쇄하는 경우 **회색조** 색상표를 사용하는 것을 고려해 보십시오. 이 색상표는 흑백 음영을 사용하여 차트에서 각 계열을 나타냅니다.  
  
 이전 버전의 Reporting Services에서는 기본값으로 지정된 색상표가 기본 차트 색상표로 사용되었습니다. 이 색상표는 일관성을 위해 같은 이름으로 계속 사용되고 있습니다. 기본 색상표를 사용해도 차트를 원활하게 업그레이드할 수 있지만, 업그레이드한 후에 변경이 필요할 수도 있습니다.  
  
## <a name="using-custom-palettes"></a>사용자 지정 색상표 사용  
 차트에 자신만의 색을 적용하려면 사용자 지정 색상표를 사용합니다. 사용자 지정 색상표를 사용하면 자신만의 색을 차트에 표시할 순서대로 추가할 수 있습니다. 사용자 지정 색상표는 디자인할 때 차트에 있는 계열의 수를 알 수 없는 경우에 특히 유용합니다. 자세한 내용은 [색상표를 사용하여 차트에 대한 색 정의&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="using-a-color-fill-on-each-series"></a>각 계열에 색 채우기 사용  
 차트에 있는 각 계열에 대한 색을 지정하여 자신만의 색을 차트에 정의할 수도 있습니다. 이렇게 하려면 **계열 속성** 대화 상자를 열고 **채우기** 의 **색**속성을 설정합니다. 이 방법은 모든 정의된 색상표를 재정의합니다. 일반적으로 보고서 처리 전까지는 데이터 집합에 있는 계열 수를 알지 못할 수도 있기 때문에 사용자 지정 색상표를 사용하여 자신만의 색을 정의하는 것이 좋습니다.  
  
 이 방법은 식을 기준으로 계열의 색을 조건부로 설정할 때 가장 적합합니다.  자세한 내용은 [차트의 데이터 요소에 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)을 클릭합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [여러 셰이프 차트에 일관된 색 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
 [색상표를 사용하여 차트에 대한 색 정의&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md))  
  
 [줄무늬 선을 추가하여 차트 데이터 강조 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>관련 항목:  
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [차트에 3D 가장자리, 볼록 및 질감 스타일 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [차트의 범례 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)  
  
  
