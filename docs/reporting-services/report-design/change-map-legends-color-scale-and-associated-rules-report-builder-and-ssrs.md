---
title: 보고서 작성기-SSRS의 지도 범례, 색 눈금 및 관련 규칙 변경 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.mapcolorscaleproperties.labels.f1
- sql13.rtp.rptdesigner.mappointlayerproperties.typerules.f1
- sql13.rtp.rptdesigner.shared.maprulesdistribution.f1
- "10512"
- "10539"
- "10533"
- sql13.rtp.rptdesigner.maplegendtitleproperties.general.f1
- "10534"
- "10516"
- sql13.rtp.rptdesigner.mapdistancescaleproperties.general.f1
- sql13.rtp.rptdesigner.mapcolorscaleproperties.general.f1
- sql13.rtp.rptdesigner.mapcolorscaletitleproperties.general.f1
- "10514"
- sql13.rtp.rptdesigner.mappointlayerproperties.sizerules.f1
- "10513"
- sql13.rtp.rptdesigner.shared.mapruleslegend.f1
- sql13.rtp.rptdesigner.shared.embeddedlabels.f1
- "10510"
- "10509"
- sql13.rtp.rptdesigner.maplegendproperties.general.f1
- "10540"
- "10517"
ms.assetid: a1d691b2-c5ae-420f-af60-b7c54a7385a4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c4b71175eb95acf68f1f7a6d0eb2a2e23f609006
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54134284"
---
# <a name="change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs"></a>지도 범례, 색 눈금 및 관련 규칙 변경(보고서 작성기 및 SSRS)
  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서에서 지도에는 지도 범례, 색 눈금 및 거리 눈금이 포함될 수 있습니다. 이러한 지도 부분은 지도에서 데이터 시각화를 해석하는 데 도움이 됩니다.  
  
 범례에는 다음과 같은 지도 부분이 포함됩니다.  
  
-   **지도 범례** 지도 계층에 있는 지도 요소의 표시를 변경하는 분석 데이터를 해석하는 데 도움이 되는 지침을 표시합니다. 하나의 지도에 여러 개의 범례가 있을 수 있으므로 각 지도 계층에서 사용할 범례를 지정해야 합니다. 범례에는 둘 이상의 지도 계층에 대한 지침이 제공될 수 있습니다.  
  
-   **색 눈금** 지도에 표시된 색을 해석하는 데 도움이 되는 지침을 표시합니다. 각 지도에는 하나의 색 눈금이 있습니다. 색 눈금에 대한 데이터는 여러 계층에 제공될 수 있습니다.  
  
-   **거리 눈금** 지도의 눈금을 해석하는 데 도움이 되는 지침을 표시합니다. 각 지도에는 하나의 거리 눈금이 있습니다. 거리 눈금은 현재 지도 뷰포트 확대/축소 값에 따라 결정됩니다.  
  
 ![rs_MapElements](../../reporting-services/report-design/media/rs-mapelements.gif "rs_MapElements")  
  
##  <a name="Viewport"></a> 뷰포트에 상대적인 범례의 위치를 변경하려면  
  
#### <a name="to-change-the-position-of-a-legend-relative-to-the-viewport"></a>뷰포트에 상대적인 범례의 위치를 변경하려면  
  
1.  디자인 뷰에서 범례를 마우스 오른쪽 단추로 클릭하고 _\<보고서 항목>_**속성** 페이지를 엽니다.  
  
2.  **위치**에서 뷰포트에 상대적인 범례를 표시할 곳을 지정하는 위치를 클릭합니다.  
  
3.  뷰포트 외부에 범례를 표시하려면 **뷰포트 외부에 \<보고서 항목 표시**를 선택합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  미리 보기에서 지도 범례와 색 눈금은 해당 범례와 관련된 규칙의 결과가 있는 경우에만 나타납니다. 표시할 항목이 없으면 범례가 렌더링된 보고서에 나타나지 않습니다.  
  
##  <a name="MapLegend"></a> 지도 범례의 레이아웃을 변경하려면  
  
#### <a name="to-change-the-layout-of-a-map-legend"></a>지도 범례의 레이아웃을 변경하려면  
  
1.  디자인 뷰에서 범례를 마우스 오른쪽 단추로 클릭하고 **범례 속성** 페이지를 엽니다.  
  
2.  **범례 레이아웃**에서 범례에 사용할 테이블 레이아웃을 클릭합니다. 다른 옵션을 클릭하면 디자인 화면의 레이아웃이 변경됩니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="MapLegendTitle"></a> 지도 범례 제목을 표시하거나 숨기려면  
  
#### <a name="to-show-or-hide-a-map-legend-title"></a>지도 범례 제목을 표시하거나 숨기려면  
  
-   디자인 화면에서 지도 범례를 마우스 오른쪽 단추로 클릭한 다음 **범례 제목 표시**를 클릭합니다.  
  
##  <a name="ColorScaleTitle"></a> 색 눈금 제목을 표시하거나 숨기려면  
  
#### <a name="to-show-or-hide-a-color-scale-title"></a>색 눈금 제목을 표시하거나 숨기려면  
  
-   디자인 화면에서 색 눈금을 마우스 오른쪽 단추로 클릭한 다음 **색 눈금 제목 표시**를 클릭합니다.  
  
##  <a name="MoveItems"></a> 첫 번째 범례에서 항목을 제외하려면  
 필요한 만큼 범례를 추가로 만들고 규칙 결과를 표시할 범례를 지정하는 각 지도 계층에 대한 규칙을 업데이트합니다.  
  
#### <a name="to-create-a-new-legend"></a>새 범례를 만들려면  
  
-   디자인 뷰에서 지도 뷰포트 외부의 지도를 마우스 오른쪽 단추로 클릭한 다음 **범례 추가**를 클릭합니다.  
  
     지도에 새 범례가 나타납니다.  
  
#### <a name="to-display-rule-results-in-a-legend"></a>범례에 규칙 집합을 표시하려면  
  
1.  디자인 뷰에서 지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  원하는 데이터가 있는 계층을 마우스 오른쪽 단추로 클릭한 다음 _\<맵 요소 유형>_**색 규칙**을 클릭합니다.  
  
3.  **범례**를 클릭합니다.  
  
4.  **이 범례에 표시** 드롭다운 목록에서 규칙 결과를 표시할 범례의 이름을 클릭합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TemplateStyle"></a> 템플릿 스타일에 따라 지도 요소 색을 변경하려면  
  
#### <a name="to-vary-map-element-colors-based-on-a-template-style"></a>템플릿 스타일에 따라 지도 요소 색을 변경하려면  
  
1.  디자인 뷰에서 지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  원하는 데이터가 있는 계층을 마우스 오른쪽 단추로 클릭한 다음 _\<맵 요소 유형>_**색 규칙**을 클릭합니다.  
  
3.  **템플릿 스타일 적용**을 클릭합니다.  
  
     템플릿 스타일은 글꼴, 테두리 스타일 및 색상표를 지정합니다. 각 지도 요소에는 지도 마법사나 지도 계층 마법사에서 지정된 테마에 대한 색상표의 색이 할당됩니다. 이것이 분석 데이터가 연결되지 않은 계층에 적용되는 유일한 옵션입니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ColorPalette"></a> 색상표에 따라 지도 요소 색을 변경하려면  
  
#### <a name="to-vary-map-element-colors-based-on-color-palette"></a>색상표에 따라 지도 요소 색을 변경하려면  
  
1.  디자인 뷰에서 지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  원하는 데이터가 있는 계층을 마우스 오른쪽 단추로 클릭한 다음 _\<맵 요소 유형>_**색 규칙**을 클릭합니다.  
  
3.  **색상표를 사용하여 데이터 시각화**를 클릭합니다.  
  
     이 옵션은 기본 제공 색상표나 지정한 사용자 지정 색상표를 사용합니다. 관련된 분석 데이터에 따라 각 지도 요소에는 색상표의 색 음영이나 다른 색이 할당됩니다.  
  
4.  **데이터 필드**에 색으로 시각화할 분석 데이터가 포함된 필드의 이름을 입력합니다.  
  
5.  **색상표**의 드롭다운 목록에서 사용할 색상표의 이름을 선택합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ColorRanges"></a> 색 범위에 따라 지도 요소 색을 변경하려면  
  
#### <a name="to-vary-map-element-colors-based-on-color-ranges"></a>색 범위에 따라 지도 요소 색을 변경하려면  
  
1.  디자인 뷰에서 지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  원하는 데이터가 있는 계층을 마우스 오른쪽 단추로 클릭한 다음 _\<맵 요소 유형>_**색 규칙**을 클릭합니다.  
  
3.  **색 범위를 사용하여 데이터 시각화**를 클릭합니다.  
  
     이 옵션은 이 페이지에서 지정하는 시작, 중간 및 마지막 색과 **분포** 페이지에서 지정하는 옵션과 결합되어 관련 분석 데이터를 범위로 나눕니다. 보고서 처리기는 연결된 데이터와 속한 범위에 따라 각 지도 요소에 적절한 색을 할당합니다.  
  
4.  **데이터 필드**에 색으로 시각화할 분석 데이터가 포함된 필드의 이름을 입력합니다.  
  
5.  **시작 색**에서 가장 작은 범위에 사용할 색을 지정합니다.  
  
6.  **중간 색**에서 중간 범위에 사용할 색을 지정합니다.  
  
7.  **마지막 색**에서 가장 큰 범위에 사용할 색을 지정합니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="CustomColors"></a> 사용자 지정 색에 따라 지도 요소 색을 변경하려면  
  
#### <a name="to-vary-map-element-colors-based-on-custom-colors"></a>사용자 지정 색에 따라 지도 요소 색을 변경하려면  
  
1.  디자인 뷰에서 지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  원하는 데이터가 있는 계층을 마우스 오른쪽 단추로 클릭한 다음 _\<맵 요소 유형>_**색 규칙**을 클릭합니다.  
  
3.  **사용자 지정 색을 사용하여 데이터 시각화**를 클릭합니다.  
  
     이 옵션은 지정한 색 목록을 사용합니다. 관련된 분석 데이터에 따라 각 지도 요소에는 목록의 색이 할당됩니다. 색보다 많은 지도 요소가 있으면 색이 할당되지 않습니다.  
  
4.  **데이터 필드**에 색으로 시각화할 분석 데이터가 포함된 필드의 이름을 입력합니다.  
  
5.  **사용자 지정 색**에서 **추가** 를 클릭하여 각 사용자 지정 색을 지정합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="DistributionOptions"></a> 범례의 분포 옵션을 설정하려면  
  
#### <a name="to-set-distribution-options-for-a-legend"></a>범례의 분포 옵션을 설정하려면  
  
1.  디자인 뷰에서 지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  원하는 데이터가 있는 계층을 마우스 오른쪽 단추로 클릭한 다음 _\<맵 요소 유형>_**색 규칙**을 클릭합니다.  
  
3.  \<규칙 유형> 옵션을 **사용하여 데이터 시각화 옵션**을 선택합니다. 배포 옵션을 사용하려면 계층과 연결된 분석 데이터에 따라 **분포** 페이지에서 범위를 만들어야 합니다.  
  
4.  **분포**를 클릭합니다.  
  
5.  다음 분포 유형 중 하나를 선택합니다.  
  
    -   **동일 간격**. 데이터를 동일한 범위 간격으로 나누는 범위를 지정합니다.  
  
    -   **동일 분포**. 각 범위에 동일한 수의 항목이 있도록 해당 데이터를 나누는 범위를 지정합니다.  
  
    -   **최적**. 균형 있는 하위 범위를 만들기 위해 분포를 자동으로 조정하는 범위를 지정합니다.  
  
    -   **사용자 지정**. 값의 분포를 제어하기 위해 범위 수를 지정합니다.  
  
     배포 옵션에 대한 자세한 내용은 [규칙 및 분석 데이터를 사용하여 다각형, 선 및 점 표시 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)를 참조하세요.  
  
6.  **하위 범위 수**에 사용할 하위 범위 수를 입력합니다. 분포 유형이 **최적**이면 하위 범위의 수가 자동으로 계산됩니다.  
  
7.  **범위 시작**에 최소 범위 값을 입력합니다. 이 값보다 작은 모든 값은 범위 최소값으로 동일합니다.  
  
8.  **범위 끝**에 최대 범위 값을 입력합니다. 이 값보다 큰 모든 값은 범위 최대값으로 동일합니다.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="RuleLegend"></a> 규칙 범례의 내용을 변경하려면  
  
#### <a name="to-change-the-contents-of-a-color-size-width-or-marker-type-legend"></a>색, 크기, 두께 또는 표식 유형 범례의 내용을 변경하려면  
  
1.  디자인 뷰에서 지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  원하는 데이터가 있는 계층을 마우스 오른쪽 단추로 클릭한 다음 _\<맵 요소 유형>_**규칙**을 클릭합니다.  
  
3.  \<*규칙 유형*>**을 사용하여 데이터 시각화**가 선택되어 있는지 확인합니다.  
  
4.  **데이터 필드**에서 계층에서 시각화할 분석 데이터가 선택되어 있는지 확인합니다.  
  
    > [!NOTE]  
    >  드롭다운 목록에 필드가 나타나지 않으면 계층을 마우스 오른쪽 단추로 클릭한 다음 **계층 데이터** 를 클릭하여 지도 계층 데이터 속성 대화 상자, 분석 데이터 페이지를 열고 이 계층의 분석 데이터를 지정했는지 확인합니다.  
  
5.  **범례**를 클릭합니다.  
  
6.  **이 범례에 표시**에서 규칙 결과를 표시하는 데 사용할 지도 범례를 선택합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ColorScale"></a> 색 눈금의 내용을 변경하려면  
  
#### <a name="to-change-the-contents-of-the-color-scale-or-a-color-legend"></a>색 눈금 또는 색 범례의 내용을 변경하려면  
  
1.  디자인 뷰에서 지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  원하는 데이터가 있는 계층을 마우스 오른쪽 단추로 클릭한 다음 _\<맵 요소 유형>_**색 규칙**을 클릭합니다.  
  
3.  사용할 색 규칙 옵션을 선택합니다. 지도 범례나 색 눈금에 항목을 표시하려면 \<규칙 유형> 옵션을 **사용하여 데이터 시각화** 옵션 중 하나를 선택해야 합니다.  
  
4.  **데이터 필드**에서 계층에서 시각화할 분석 데이터가 선택되어 있는지 확인합니다.  
  
    > [!NOTE]  
    >  드롭다운 목록에 필드가 나타나지 않으면 계층을 마우스 오른쪽 단추로 클릭한 다음 **계층 데이터** 를 클릭하여 지도 계층 데이터 속성 대화 상자, 분석 데이터 페이지를 열고 이 계층의 분석 데이터를 지정했는지 확인합니다.  
  
5.  **범례**를 클릭합니다.  
  
6.  **색 눈금 옵션**에서 **색 눈금에 표시** 를 선택하여 색 눈금에 규칙 결과를 표시합니다. 둘 이상의 색 규칙에 대해 이 옵션을 지정할 수 있습니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="HideItems"></a> 범례에서 모든 항목을 제거하려면  
  
#### <a name="to-hide-items-based-on-a-rule"></a>규칙에 따라 항목을 숨기려면  
  
1.  디자인 뷰에서 지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  원하는 데이터가 있는 계층을 마우스 오른쪽 단추로 클릭한 다음 _\<맵 요소 유형>_**규칙**을 클릭합니다.  
  
3.  **범례**를 클릭합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ChangeFormatItems"></a> 범례의 내용 형식을 변경하려면  
 지도 범례와 연결된 규칙의 범례 옵션을 설정합니다.  
  
#### <a name="to-change-the-format-of-content-in-a-legend"></a>범례의 내용 형식을 변경하려면  
  
1.  디자인 뷰에서 지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  원하는 데이터가 있는 계층을 마우스 오른쪽 단추로 클릭한 다음 _\<맵 요소 유형>_**규칙**을 클릭합니다.  
  
3.  **범례**를 클릭합니다.  
  
4.  **범례 텍스트** 에 범례에 표시할 데이터를 지정하는 키워드가 표시됩니다. 범례 키워드와 사용자 지정 형식을 사용하여 범례 텍스트의 형식을 제어할 수 있습니다. 예를 들어 #FROMVALUE {C2}는 소수 자릿수가 두 자리인 통화를 지정합니다. 자세한 내용은 [규칙 및 분석 데이터를 사용하여 다각형, 선 및 점 표시 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)를 참조하세요.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [지도&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [지도 또는 지도 계층 추가, 변경 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [지도 또는 지도 계층의 데이터 및 표시 사용자 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [보고서 문제 해결: 맵 보고서&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)   
 [지도 마법사 및 지도 계층 마법사&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  
