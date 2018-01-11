---
title: "계열에 대한 차트 영역 지정(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10157"
- sql13.rtp.rptdesigner.chartareaproperties.alignment.f1
ms.assetid: dc3c365b-c263-402a-bf6f-c2a7081db073
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1674e3981f598b47f0691e36de96f9add9700ece
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="specify-a-chart-area-for-a-series-report-builder-and-ssrs"></a>계열에 대한 차트 영역 지정(보고서 작성기 및 SSRS)
  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서에서 *차트* 는 외부 테두리, 차트 제목 및 범례를 포함하는 최상위 컨테이너입니다. 기본적으로 차트에는 한 개의 기본 *차트 영역*이 포함됩니다. 차트 영역은 차트 화면에는 표시되지 않지만 하나 이상의 계열에 대한 축 레이블, 축 제목 및 그리기 영역만을 포함하는 컨테이너로 생각할 수 있습니다. 다음 그림에서는 단일 차트 내 차트 영역의 개념을 보여 줍니다.  
  
 ![차트 영역의 다이어그램 표시](../../reporting-services/report-design/media/chartareasdiagram.gif "차트 영역의 다이어그램 표시")  
  
 기본적으로 모든 계열이 기본 차트 영역에 추가됩니다. 영역형, 세로 막대형, 꺾은선형 또는 분산형 차트를 사용할 때는 이러한 계열을 조합하여 같은 차트 영역에 표시할 수 있습니다. 같은 차트 영역에 여러 계열이 있는 경우 차트의 가독성이 떨어집니다. 이 경우 차트 종류를 여러 차트 영역으로 분리할 수 있습니다. 여러 차트 영역을 사용하면 가독성이 높아져 손쉽게 비교할 수 있습니다. 예를 들어 가격/거래량 주식형 차트는 보통 서로 다른 값의 범위를 포함하지만 같은 기간 동안의 가격 및 거래량을 비교할 수 있습니다.  
  
 가로 막대형, 극좌표형 또는 셰이프 계열만 동일한 차트 영역에 있는 같은 차트 종류의 계열과 결합할 수 있습니다. 극좌표형 또는 셰이프 차트를 사용하는 경우 표시할 필드마다 별도의 차트 데이터 영역을 사용하는 방법을 고려해야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-associate-a-series-with-a-new-chart-area"></a>계열과 새 차트 영역을 연결하려면  
  
1.  차트의 아무 곳이나 마우스 오른쪽 단추로 클릭하고 **새 차트 영역 추가**를 선택합니다. 새로운 빈 차트가 나타납니다.  
  
2.  차트에서 계열을 마우스 오른쪽 단추로 클릭하거나 차트 데이터 창의 해당하는 영역에서 계열 또는 데이터 필드를 마우스 오른쪽 단추로 클릭하고 **계열 속성**을 클릭합니다.  
  
3.  **축 및 차트 영역**에서 계열을 표시할 차트 영역을 선택합니다.  
  
4.  (옵션) 차트 영역을 세로로 맞춥니다. 이렇게 하려면 차트를 마우스 오른쪽 단추로 클릭하고 **차트 영역 속성**을 선택합니다. **맞춤**에서, 선택한 차트 영역과 맞출 다른 차트 영역을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [차트의 여러 계열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md)   
 [차트의 데이터 요소에 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [색상표를 사용하여 차트에 대한 색 정의&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [극좌표형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/polar-charts-report-builder-and-ssrs.md)   
 [셰이프 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)   
 [원형 차트 &#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
