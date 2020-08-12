---
title: 차트 종류(보고서 작성기) | Microsoft Docs
description: 보고서 작성기에서 데이터 세트를 시각화하고 적절한 차트 종류를 선택할 수 있도록 고유한 차트 특성 중에서 선택합니다.
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10423"
ms.assetid: 57b00017-69ae-4e71-8d78-44744e208ac7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8f19176d540a547ec4617244835f87b9994d368e
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681412"
---
# <a name="chart-types-report-builder-and-ssrs"></a>차트 종류(보고서 작성기 및 SSRS)

표현하려는 데이터의 형식에 적합한 차트 종류를 선택하는 것이 중요합니다. 어떤 차트 종류를 선택하는가에 따라 데이터를 차트 폼에 삽입했을 때 그 데이터를 얼마나 잘 해석할 수 있는지가 결정됩니다. 예를 들어 차트의 크기에 비해 많은 양의 데이터 요소가 데이터 세트에 포함되어 있으면 영역형, 꺾은선형 또는 분산형 차트를 사용하여 데이터를 표현하는 것이 더 나을 수 있습니다. 선택한 차트 종류에 따라 데이터를 준비하는 방법에 대한 자세한 내용은 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="choosing-a-chart-type"></a>차트 종류 선택  
 각 차트 종류마다 데이터 세트를 시각화하는 데 도움이 되는 고유한 특징이 있습니다. 임의의 차트 종류를 사용하여 데이터를 표시할 수는 있지만 보고서에 표시하려는 내용이 무엇인지에 따라 데이터에 적합한 차트 종류를 사용하면 데이터를 더 쉽게 읽을 수 있습니다. 다음 표에는 특정 데이터 세트에 어떤 차트 종류가 적합한지 판단하는 데 도움이 되는 차트의 특징이 요약 정리되어 있습니다.  
  
 차트를 만든 후 차트 종류를 변경할 수 있습니다. 자세한 내용은 [차트 종류 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/change-a-chart-type-report-builder-and-ssrs.md)을 참조하세요.  
  
 이 중 대부분의 차트 종류에 대한 예는 예제 보고서로 제공됩니다. 샘플 보고서를 다운로드하는 방법은 [보고서 작성기 및 보고서 디자이너 샘플 보고서](https://go.microsoft.com/fwlink/?LinkId=198283)를 참조하세요.  
  
|차트 종류|비율 데이터 표시|주식 데이터 표시|선형 데이터 표시|다중 값 데이터 표시|  
|----------------|------------------------|------------------------|-------------------------|-------------------------------|  
|[영역형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/area-charts-report-builder-and-ssrs.md)|||![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")||  
|[가로 막대형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)|||![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")||  
|[데이터 막대](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)|||![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")||  
|[세로 막대형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)|||![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")||  
|[꺾은선형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md)|||![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")||  
|[원형 차트 &#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)|![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")||||  
|[극좌표형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/polar-charts-report-builder-and-ssrs.md)|![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")||||  
|[범위형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md)|||![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")|![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")|  
|[분산형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/scatter-charts-report-builder-and-ssrs.md)|![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")||![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")||  
|[셰이프 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)|![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")||||  
|[스파크라인](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)|![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")|![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")|![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")|![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")|  
|[주식형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/stock-charts-report-builder-and-ssrs.md)||![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")||![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")|  

## <a name="next-steps"></a>다음 단계

[차트](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[차트의 빈 데이터 요소 및 Null 데이터 요소](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
[보고서에 차트 추가](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
