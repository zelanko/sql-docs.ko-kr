---
title: 꺾은선형 차트(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 194e6679-890d-4a3e-a756-130d32ef7e29
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 68e6ea1c31cea554944824e38926318682b163ce
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63209187"
---
# <a name="line-charts-report-builder-and-ssrs"></a>꺾은선형 차트(보고서 작성기 및 SSRS)
  꺾은선형 차트에서 계열은 단일 선으로 연결된 일련의 점으로 표시됩니다. 꺾은선형 차트는 연속적인 일정 기간 동안 발생하는 많은 양의 데이터를 표시하는 데 사용됩니다. 꺾은선형 차트에 데이터를 추가하는 방법에 대한 자세한 내용은 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)를 참조하세요.  
  
 다음 그림에서는 계열이 세 개 포함된 꺾은선형 차트를 보여 줍니다.  
  
 ![꺾은선형 차트](../media/rs-linechart.gif "꺾은선형 차트")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>변형  
  
-   **곡선형**. 일반적인 선 대신 곡선을 사용하는 꺾은선형 차트입니다.  
  
-   **단계별 선형**. 일반적인 선 대신 단계별 선을 사용하는 꺾은선형 차트입니다. 단계별 선형 차트에서는 사다리나 계단의 층과 같은 모양으로 선을 사용하여 점을 연결합니다.  
  
-   **스파크라인 차트**. 테이블 또는 테이블릭스 셀에 선 계열만 표시하는 꺾은선형 차트의 변형입니다. 자세한 내용은 [스파크라인 및 데이터 막대 추가&#40;보고서 작성기 및 SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="data-considerations-for-line-charts"></a>꺾은선형 차트의 데이터 고려 사항  
  
-   기본 꺾은선형 차트의 시각적 효과를 높이기 위해 계열 테두리의 두께를 3으로 변경하고 그림자 오프셋 값으로 1을 추가하는 것도 좋은 방법입니다. 이렇게 하면 훨씬 더 강조된 꺾은선형 차트를 만들 수 있습니다. 단, 차트 종류를 꺾은선형에서 다른 종류로 변경하려면 이러한 속성을 원래 값으로 되돌려야 합니다.  
  
-   데이터 세트에 빈 값이 들어 있는 경우 꺾은선형 차트에서는 차트의 연속성을 유지하기 위해 자리 표시자 선의 형태로 빈 점을 추가합니다. 이러한 선을 표시하지 않으려면 가로 막대형 차트나 세로 막대형 차트 같이 데이터를 연속적으로 표시하지 않는 차트 종류를 사용하여 데이터 세트를 표시하는 것이 좋습니다.  
  
-   꺾은선형 차트에는 선을 그리기 위한 점이 적어도 두 개 이상 필요합니다.  데이터 세트에 포함된 데이터 요소가 한 개뿐이면 꺾은선형 차트가 단일 데이터 요소 표식으로 표시됩니다.  
  
-   선으로 그려진 계열은 차트 영역 내에서 공간을 많이 차지하지 않습니다.  따라서 꺾은선형 차트는 세로 막대형 차트 같은 다른 차트 종류와 자주 결합하여 사용됩니다. 그러나 가로 막대형, 극좌표형, 원형 또는 셰이프 차트 종류와는 꺾은선형 차트를 결합할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [가로 막대형 차트&#40;보고서 작성기 및 SSRS&#41;](bar-charts-report-builder-and-ssrs.md)   
 [세로 막대형 차트&#40;보고서 작성기 및 SSRS&#41;](column-charts-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [차트 종류&#40;보고서 작성기 및 SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [영역형 차트&#40;보고서 작성기 및 SSRS&#41;](area-charts-report-builder-and-ssrs.md)   
 [차트의 빈 데이터 요소 및 Null 데이터 요소&#40;보고서 작성기 및 SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
