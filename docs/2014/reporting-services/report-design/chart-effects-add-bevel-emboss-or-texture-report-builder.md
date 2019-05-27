---
title: 차트에 빗면 효과, 볼록 효과 및 질감 스타일 추가(보고서 작성기 및 SSRS)| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 737cfc80-b39e-497c-817b-b46693deb58f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b25d12646a2662cb5c6ab8f2a9b510aa02d7c49b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106277"
---
# <a name="add-bevel-emboss-and-texture-styles-to-a-chart-report-builder-and-ssrs"></a>차트에 빗면 효과, 볼록 효과 및 질감 스타일 추가(보고서 작성기 및 SSRS)
  특정 차트 종류를 사용할 때 그리기 효과를 지정하여 차트의 시각적 효과를 높일 수 있습니다. 이러한 그리기 효과는 차트의 계열에만 적용됩니다. 다른 차트 요소에는 그리기 효과가 아무런 영향을 주지 않습니다.  
  
 원형 또는 도넛형 차트의 변형을 사용하는 경우 이미지에 적용할 수 있는 빗면 효과나 볼록 효과와 비슷한 부드러운 가장자리 또는 오목 그리기 스타일을 지정할 수 있습니다.  
  
 가로 막대형 또는 세로 막대형 차트의 변형을 사용하는 경우 각각의 가로 또는 세로 막대에 원통형, 쐐기형 및 그라데이션 같은 질감 스타일을 적용할 수 있습니다.  
  
 이러한 그리기 스타일 이외에도 여러 가지 차트 요소에 테두리와 그림자를 추가하여 깊이감을 더할 수 있습니다. 차트의 서식을 지정하는 다른 방법에 대한 자세한 내용은 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-bevel-or-emboss-styles-to-a-pie-or-doughnut-chart"></a>원형 또는 도넛형 차트에 빗면 또는 볼록 스타일을 추가하려면  
  
1.  **보기** 탭에서 **속성** 을 선택하여 속성 창을 엽니다.  
  
2.  그리기 효과를 적용할 원형 또는 도넛형 차트를 선택합니다. 전체 차트가 아니라 차트의 데이터 필드를 선택합니다.  
  
3.  속성 창에서 **CustomAttributes** 노드를 확장합니다.  
  
4.  드롭다운 목록에서 PieDrawingStyle에 대한 스타일을 선택합니다.  
  
> [!NOTE]  
>  3D와 빗면 또는 볼록 스타일을 동일한 차트에서 사용할 수 없습니다. 차트에 3D를 사용하도록 설정한 경우 PieDrawingStyle 속성이 표시되지 않습니다.  
  
 ![오목 그리기 스타일을 포함하는 원형 차트](../media/rs-piedrawingeffects-concave.gif "오목 그리기 스타일을 포함하는 원형 차트")  
  
### <a name="to-add-texture-styles-to-a-bar-or-column-chart"></a>가로 막대형 또는 세로 막대형 차트에 질감 스타일을 추가하려면  
  
1.  질감 스타일을 적용할 가로 막대형 또는 세로 막대형 차트를 선택합니다. 전체 차트가 아니라 차트의 데이터 필드를 선택합니다.  
  
2.  속성 창을 엽니다.  
  
3.  **CustomAttributes** 노드를 확장합니다.  
  
4.  드롭다운 목록에서 DrawingStyle에 대한 스타일을 선택합니다.  
  
> [!NOTE]  
>  3D와 빗면 또는 볼록 스타일을 동일한 차트에서 사용할 수 없습니다. 차트에 3D를 사용하도록 설정한 경우 PieDrawingStyle 속성이 표시되지 않습니다.  
  
 ![LightToDark 그리기 효과를 포함하는 가로 막대형 차트](../media/rs-bardrawingeffects-lighttodark.gif "LightToDark 그리기 효과를 포함하는 가로 막대형 차트")  
  
## <a name="see-also"></a>관련 항목  
 [가로 막대형 차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [세로 막대형 차트&#40;보고서 작성기 및 SSRS&#41;](column-charts-report-builder-and-ssrs.md)   
 [원형 차트&#40;보고서 작성기 및 SSRS&#41;](pie-charts-report-builder-and-ssrs.md)   
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)  
  
  
