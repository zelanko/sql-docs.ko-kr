---
title: 차트 종류(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10423"
ms.assetid: 57b00017-69ae-4e71-8d78-44744e208ac7
caps.latest.revision: 10
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: f69c4a6dd5f2593650067be51eae3b63e49dcd96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080138"
---
# <a name="chart-types-report-builder-and-ssrs"></a>차트 종류(보고서 작성기 및 SSRS)
  표현하려는 데이터의 형식에 적합한 차트 종류를 선택하는 것이 중요합니다. 어떤 차트 종류를 선택하는가에 따라 데이터를 차트 폼에 삽입했을 때 그 데이터를 얼마나 잘 해석할 수 있는지가 결정됩니다. 예를 들어 차트의 크기에 비해 많은 양의 데이터 요소가 데이터 집합에 포함되어 있으면 영역형, 꺾은선형 또는 분산형 차트를 사용하여 데이터를 표현하는 것이 더 나을 수 있습니다. 선택한 차트 종류에 따라 데이터를 준비 하는 방법에 대 한 논의 알려면 [차트 &#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="choosing-a-chart-type"></a>차트 종류 선택  
 각 차트 종류마다 데이터 집합을 시각화하는 데 도움이 되는 고유한 특징이 있습니다. 임의의 차트 종류를 사용하여 데이터를 표시할 수는 있지만 보고서에 표시하려는 내용이 무엇인지에 따라 데이터에 적합한 차트 종류를 사용하면 데이터를 더 쉽게 읽을 수 있습니다. 다음 표에는 특정 데이터 집합에 어떤 차트 종류가 적합한지 판단하는 데 도움이 되는 차트의 특징이 요약 정리되어 있습니다.  
  
 차트를 만든 후 차트 종류를 변경할 수 있습니다. 자세한 내용은 [차트 종류 변경&#40;보고서 작성기 및 SSRS&#41;](change-a-chart-type-report-builder-and-ssrs.md)을 참조하세요.  
  
 이 중 대부분의 차트 종류에 대한 예는 예제 보고서로 제공됩니다. 샘플 보고서를 다운로드하는 방법은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][보고서 작성기 및 보고서 디자이너 샘플 보고서](http://go.microsoft.com/fwlink/?LinkId=198283)를 참조하세요.  
  
|차트 종류|비율 데이터 표시|주식 데이터 표시|선형 데이터 표시|다중 값 데이터 표시|  
|----------------|------------------------|------------------------|-------------------------|-------------------------------|  
|[영역형 차트 &#40;보고서 작성기 및 SSRS&#41;](area-charts-report-builder-and-ssrs.md)|||![사용 가능](../media/greencheck.gif "사용 가능")||  
|[가로 막대형 차트 &#40;보고서 작성기 및 SSRS&#41;](bar-charts-report-builder-and-ssrs.md)|||![사용 가능](../media/greencheck.gif "사용 가능")||  
|[데이터 막대](sparklines-and-data-bars-report-builder-and-ssrs.md)|||![사용 가능](../media/greencheck.gif "사용 가능")||  
|[세로 막대형 차트 &#40;보고서 작성기 및 SSRS&#41;](column-charts-report-builder-and-ssrs.md)|||![사용 가능](../media/greencheck.gif "사용 가능")||  
|[꺾은선형 차트 &#40;보고서 작성기 및 SSRS&#41;](line-charts-report-builder-and-ssrs.md)|||![사용 가능](../media/greencheck.gif "사용 가능")||  
|[원형 차트 &#40;보고서 작성기 및 SSRS&#41;](pie-charts-report-builder-and-ssrs.md)|![사용 가능](../media/greencheck.gif "사용 가능")||||  
|[극좌표 형 차트 &#40;보고서 작성기 및 SSRS&#41;](polar-charts-report-builder-and-ssrs.md)|![사용 가능](../media/greencheck.gif "사용 가능")||||  
|[범위 차트 &#40;보고서 작성기 및 SSRS&#41;](range-charts-report-builder-and-ssrs.md)|||![사용 가능](../media/greencheck.gif "사용 가능")|![사용 가능](../media/greencheck.gif "사용 가능")|  
|[분산형 차트 &#40;보고서 작성기 및 SSRS&#41;](scatter-charts-report-builder-and-ssrs.md)|![사용 가능](../media/greencheck.gif "사용 가능")||![사용 가능](../media/greencheck.gif "사용 가능")||  
|[셰이프 차트는 &#40;보고서 작성기 및 SSRS&#41;](shape-charts-report-builder-and-ssrs.md)|![사용 가능](../media/greencheck.gif "사용 가능")||||  
|[스파크 라인](sparklines-and-data-bars-report-builder-and-ssrs.md)|![사용 가능](../media/greencheck.gif "사용 가능")|![사용 가능](../media/greencheck.gif "사용 가능")|![사용 가능](../media/greencheck.gif "사용 가능")|![사용 가능](../media/greencheck.gif "사용 가능")|  
|[차트를 판매 &#40;보고서 작성기 및 SSRS&#41;](stock-charts-report-builder-and-ssrs.md)||![사용 가능](../media/greencheck.gif "사용 가능")||![사용 가능](../media/greencheck.gif "사용 가능")|  
  
## <a name="see-also"></a>관련 항목  
 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [차트의 빈 데이터 요소 및 Null 데이터 요소&#40;보고서 작성기 및 SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [보고서에 차트를 추가 &#40;보고서 작성기 및 SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md)  
  
  