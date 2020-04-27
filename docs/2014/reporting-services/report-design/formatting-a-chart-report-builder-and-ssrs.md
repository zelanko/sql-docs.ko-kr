---
title: 차트 서식 지정(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10214"
- sql12.rtp.rptdesigner.calculatedseriesproperties.fill.f1
- sql12.rtp.rptdesigner.serieslabelproperties.fill.f1
- sql12.rtp.rptdesigner.legendproperties.fill.f1
- "10149"
- sql12.rtp.rptdesigner.seriesproperties.shadow.f1
- sql12.rtp.rptdesigner.seriesproperties.markers.f1
- "10255"
- sql12.rtp.rptdesigner.charttitleproperties.fill.f1
- "10154"
- "10170"
- "10173"
- sql12.rtp.rptdesigner.seriesproperties.fill.f1
- "10169"
- "10158"
- sql12.rtp.rptdesigner.chartareaproperties.fill.f1
- sql12.rtp.rptdesigner.charttitleproperties.shadow.f1
- "10246"
- "10150"
- sql12.rtp.rptdesigner.calculatedseriesproperties.borders.f1
- sql12.rtp.rptdesigner.chartproperties.fill.f1
- "10159"
- sql12.rtp.rptdesigner.majorgridlineproperties.gridlineoptions.f1
- "10160"
- sql12.rtp.rptdesigner.serieslabelproperties.font.f1
- "10182"
- "10163"
- "10164"
- "10253"
- "10216"
- "10171"
- "10257"
- sql12.rtp.rptdesigner.chartareaproperties.border.f1
- sql12.rtp.rptdesigner.calculatedseriesproperties.shadow.f1
- sql12.rtp.rptdesigner.chartproperties.border.f1
- sql12.rtp.rptdesigner.minorgridlineproperties.gridlineoptions.f1
- sql12.rtp.rptdesigner.chartareaproperties.shadow.f1
- sql12.rtp.rptdesigner.charttitleproperties.borders.f1
- sql12.rtp.rptdesigner.charttitleproperties.font.f1
- "10247"
ms.assetid: d3984300-c766-42f8-b7c4-863123d67c99
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: af164d4db9b6439f0634d113652b95939827b0f5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105854"
---
# <a name="formatting-a-chart-report-builder-and-ssrs"></a>차트 서식 지정(보고서 작성기 및 SSRS)
  차트용 데이터를 정의한 후 차트가 원하는 대로 표시되면 서식을 추가하여 전반적인 차트 모양을 향상시키고 중요한 데이터 요소를 강조 표시할 수 있습니다. 가장 일반적인 서식 지정 옵션은 차트 요소를 마우스 오른쪽 단추로 클릭하여 표시되는 바로 가기 메뉴에서 제공되는 속성 대화 상자에서 수정할 수 있습니다. 각 차트 요소에는 자체 대화 상자가 있습니다. 차트 요소에 대한 자세한 내용은 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)를 참조하세요.  
  
 차트와 관련된 모든 속성은 속성 창에 있지만 이들 중 많은 속성은 대화 상자에서도 설정할 수 있습니다. 계열에 서식을 지정하는 경우 속성 창의 **CustomAttributes** 속성 범주에만 있는 사용자 지정 특성을 사용하여 계열 관련 속성을 지정할 수 있습니다.  
  
 최소한의 단계를 사용하여 효과적으로 차트에 서식을 지정하려면 기본 테두리 스타일, 색상표 및 그리기 스타일을 변경하십시오. 이 세 가지 기능은 차트에서 시각적으로 가장 큰 변화를 생성합니다. 그리기 스타일은 원형, 도넛형, 가로 막대형 및 세로 막대형 차트에서만 사용할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="in-this-section"></a>섹션 내용  
 [차트에서 계열 색 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)  
 색상표를 사용하여 색을 정의하고 고유한 색상표를 정의하고 식을 기반으로 색을 정의하는 방법을 설명합니다.  
  
 [차트의 축 레이블 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)  
 눈금선, 눈금 표시, 제목을 표시하는 방법과 축 눈금의 숫자와 날짜에 서식을 지정하는 방법을 설명합니다.  
  
 [차트의 범례 서식 지정&#40;보고서 작성기 및 SSRS&#41;](chart-legend-formatting-report-builder.md)  
 차트 범례에서 항목 순서를 바꾸고 서식을 지정하는 방법을 설명합니다.  
  
 [차트의 데이터 요소에 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
 데이터 요소 레이블의 위치를 지정하고 차트의 모든 계열에 대한 데이터 요소 표식에 서식을 지정하는 방법을 설명합니다.  
  
 [차트의 3D, 빗면 및 기타 효과&#40;보고서 작성기 및 SSRS&#41;](chart-effects-3d-bevel-and-other-report-builder.md)  
 차트에 적용할 수 있는 다양한 3D 효과를 설명합니다.  
  
 [차트에 테두리 프레임 추가&#40;보고서 작성기 및 SSRS&#41;](add-a-border-frame-to-a-chart-report-builder-and-ssrs.md)  
 차트에 테두리 프레임을 추가하는 방법을 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [차트에 테두리 프레임 추가&#40;보고서 작성기 및 SSRS&#41;](add-a-border-frame-to-a-chart-report-builder-and-ssrs.md)   
 [색상표를 사용하여 차트에 대한 색 정의&#40;보고서 작성기 및 SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [차트에 3D 가장자리, 볼록 및 질감 스타일 추가&#40;보고서 작성기 및 SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)  
  
  
