---
title: 스파크라인 및 데이터 막대(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.sparklines.f1
- "10544"
ms.assetid: b287436b-fa48-4970-a1a7-1dbcb86e7411
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6bde9dbc2bc91c5de90b65c0173d4b691e888086
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sparklines-and-data-bars-report-builder-and-ssrs"></a>스파크라인 및 데이터 막대(보고서 작성기 및 SSRS)
  스파크라인과 데이터 막대는 작은 공간에 많은 정보가 포함되어 있는 작고 간단한 차트로, 보통 텍스트와 인라인으로 표시됩니다.   
    
  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서에서는 스파크라인과 데이터 막대는 보통 테이블이나 행렬에 사용됩니다. 스파크라인과 데이터 막대는 여러 개를 함께 표시할 수 있어 하나씩 보는 대신 서로 빠르게 비교할 수 있기 때문에 유용합니다. 이렇게 하면 이상값(다른 행처럼 작동하지 않는 행)을 쉽게 확인할 수 있습니다. 스파크라인은 크기는 작지만 각각 시간에 따라 여러 데이터 요소를 표시하는 경우가 많습니다. 데이터 막대도 여러 데이터 요소를 표시할 수는 있지만 일반적으로는 하나만 표시합니다. 각 스파크라인은 보통 단일 계열을 제공합니다. 스파크라인은 집계된 데이터를 표시하므로 테이블의 세부 그룹에는 추가할 수 없으며 그룹과 연결된 셀에 배치해야 합니다. 스파크라인 및 데이터 막대에는 동일한 기본 차트 요소(범주, 계열 및 값)가 있지만 범례, 축 선, 레이블 또는 눈금 표시는 없습니다.  
  
 ![rs_SparklineExample](../../reporting-services/report-design/media/rs-sparklineexample.gif "rs_SparklineExample")  
  
 스파크라인을 빠르게 시작하려면 [자습서: 보고서에 스파크라인 추가&#40;보고서 작성기&#41;](../../reporting-services/tutorial-add-a-sparkline-to-your-report-report-builder.md) 와 비디오 [방법: 테이블에서 스파크라인 만들기](http://go.microsoft.com/fwlink/?LinkId=197092) 및 [보고서 작성기의 스파크라인, 막대형 차트 및 표시기](http://technet.microsoft.com/bi/video/ff877165) 를 참조하세요.  
  
> [!NOTE]  
>  스파크라인과 부모 테이블이나 행렬, 목록과 함께 데이터 막대를 보고서와는 별도로 보고서 파트로 게시할 수 있습니다. [보고서 파트](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)에 대해 자세히 알아봅니다.  
  
##  <a name="KindsofSparklines"></a> 스파크라인 유형  
 일반 차트와 같이 다양한 유형의 스파크라인을 만들 수 있습니다. 그러나 보통 3D 스파크라인은 만들지 않습니다. 다음과 같은 전체 차트의 스파크라인 버전을 만들 수 있습니다.  
  
-   [세로 막대형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md): 기본, 누적형 및 100% 기준 누적 세로 막대형 차트  
  
-   [꺾은선형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md): 3D 꺾은선형 차트를 제외한 모든 차트  
  
-   [영역형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/area-charts-report-builder-and-ssrs.md): 3D 영역형 차트를 제외한 모든 차트  
  
-   [원형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md): 도넛형 차트(평면형/3D), 깔때기형과 피라미드형 차트 등의 다른 모양은 아님  
  
-   [범위형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md): 주식형, 원통형, 오차 막대 및 상자 그림 차트  
  
##  <a name="DataBars"></a> 데이터 막대  
 데이터 막대는 보통 단일 데이터 요소를 나타내지만 일반 가로 막대형 차트처럼 여러 데이터 요소를 나타낼 수도 있습니다. 데이터 막대에는 보통 범주가 없는 여러 계열 또는 계열 그룹화가 포함됩니다.  
  
 ![rs_DataBars](../../reporting-services/report-design/media/rs-databars.gif "rs_DataBars")  
  
 누적형 데이터 막대를 사용하는 이 예에서 각 데이터 막대(여기서는 막대가 하나뿐임)에는 여러 데이터 요소가 표시됩니다. 예를 들어 막대의 서로 다른 세 색은 우선 순위 수준이 세 가지인 태스크를 나타낼 수 있습니다. 여기서 막대의 길이는 각 사람에게 할당된 총 태스크 수를 나타냅니다. 이와 같은 100% 누적형 데이터 막대를 대신 만든 경우 각 막대가 셀에 채워지며 각 우선 순위 수준이 전체에서 차지하는 비율이 각 색으로 표시됩니다.  
  
 다음과 같은 전체 차트의 데이터 막대 버전을 만들 수 있습니다.  
  
-   [막대형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md): 기본, 누적형 및 100% 기준 누적 막대형 차트  
  
-   [세로 막대형 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md): 기본, 누적형 및 100% 기준 누적 세로 막대형 차트 세로 막대형 차트는 스파크라인 또는 데이터 막대일 수 있습니다.  
  
##  <a name="AlignDatainTableMatrix"></a> 테이블 또는 행렬에서 스파크라인 데이터 정렬  
 스파크라인을 테이블이나 행렬에 삽입할 때는 각 스파크라인의 데이터 요소를 해당 열의 다른 스파크라인에 있는 데이터 요소에 맞게 정렬하는 것이 중요합니다. 이렇게 하지 않으면 여러 행의 데이터를 비교하기가 어렵습니다. 예를 들어 회사에 소속된 각 영업 사원의 월별 판매 데이터를 비교하는 경우 월을 정렬하게 됩니다. 특정 직원이 4월에 출근하지 않은 경우 이 직원에게는 해당 월의 데이터가 없습니다. 이 경우 해당 월은 건너뛰고 후속 월의 데이터가 다른 직원들의 데이터에 정렬되도록 할 수 있습니다. 이렇게 하려면 가로 축을 정렬하면 됩니다. 자세한 내용은 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)에서 스파크라인에 대한 섹션 및 [테이블 또는 행렬에서 차트의 데이터 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)를 참조하세요.  
  
 마찬가지로 행 전체를 비교하려는 경우에는 데이터를 세로로 정렬해야 합니다. 즉, 단일 데이터 막대나 스파크라인의 줄 또는 막대 높이가 다른 모든 데이터 막대나 스파크라인에 있는 줄 또는 막대 높이를 기준으로 해야 합니다. 이렇게 하지 않으면 행을 서로 비교할 수 없습니다.  
  
 ![rs_SparklineAlignData](../../reporting-services/report-design/media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 이 이미지에서 세로 막대형 차트에는 각 직원의 일일 판매량이 표시됩니다. 직원의 판매량이 없는 일의 경우 차트에서 공백으로 표시되고 이후의 일이 정렬됩니다. 이것이 가로 정렬의 예입니다. 또한 일부 직원의 경우에는 모든 막대가 짧으며 셀 맨 위까지 올라가는 막대가 없습니다. 이것이 세로 정렬의 예입니다. 이렇게 정렬하지 않으면 긴 막대가 없는 행의 경우 짧은 막대가 셀 전체 높이를 채우도록 확장됩니다.  
  
##  <a name="UnderstandScope"></a> 스파크라인 또는 데이터 막대로 제공되는 데이터 이해  
 테이블이나 행렬에 스파크라인 또는 데이터 막대를 추가하는 것을 특정 데이터 영역에 다른 데이터 영역을 *중첩* 한다고 합니다. 중첩이란 스파크라인 또는 데이터 막대에 제공되는 데이터가 테이블이나 행렬의 기준이 되는 데이터 집합과, 테이블이나 행렬에서 스파크라인 또는 데이터 막대를 배치하는 위치에 의해 제어됨을 의미합니다. 자세한 내용은 [중첩된 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)를 참조하세요.  
  
##  <a name="ConvertSparklinetoChart"></a> 스파크라인 또는 데이터 막대를 전체 차트로 변환  
 스파크라인 및 데이터 막대도 일종의 차트이므로, 이들 항목보다는 전체 차트 기능을 사용하려는 경우 차트를 마우스 오른쪽 단추로 클릭하고 **전체 차트로 변환**을 클릭하여 전체 차트로 변환할 수 있습니다. 이렇게 하면 축 선, 레이블, 눈금 표시 및 범례가 자동으로 추가됩니다.  
  
> [!NOTE]  
>  전체 차트를 한 번의 클릭으로 스파크라인이나 데이터 막대로 변환할 수는 없습니다. 그러나 스파크라인 및 데이터 막대에 없는 모든 차트 요소를 삭제하는 것만으로 전체 차트에서 스파크라인 또는 데이터 막대를 만들 수는 있습니다.  
  
##  <a name="HowTo"></a> 방법 도움말 항목  
 [스파크라인 및 데이터 막대 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
 [테이블 또는 행렬에서 차트의 데이터 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
### <a name="other-how-to-topics-for-charts"></a>기타 차트 관련 방법 도움말 항목  
 스파크라인 및 데이터 막대도 일종의 차트이므로, 다음의 차트 관련 방법 도움말 항목에서 유용한 관련 정보를 확인할 수 있습니다.  
  
 [보고서에 차트 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)  
  
 [차트에 빈 요소 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)  
  
 [차트에서 여백 추가 또는 제거&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
 [차트 종류 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/change-a-chart-type-report-builder-and-ssrs.md)  
  
 [색상표를 사용하여 차트에 대한 색 정의&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)  
  
 [계열에 도구 설명 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
 [로그 눈금 간격 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)  
  
 [축 간격 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  
  
 [여러 셰이프 차트에 일관된 색 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>참고 항목  
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [자습서: 보고서에 스파크라인 추가&#40;보고서 작성기&#41;](../../reporting-services/tutorial-add-a-sparkline-to-your-report-report-builder.md)   
  
  
