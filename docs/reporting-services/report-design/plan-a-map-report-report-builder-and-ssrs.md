---
title: 지도 보고서 계획(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: dc0c27a4-7e31-4a15-a0bc-3a02479d5b02
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8918251cccca5c04bd42bcb931c4efa5d1f9fd6d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65576323"
---
# <a name="plan-a-map-report-report-builder-and-ssrs"></a>지도 보고서 계획(보고서 작성기 및 SSRS)
훌륭한 보고서는 조치를 취하거나 상황을 깊이 있게 파악할 수 있는 정보를 제공합니다. 지리적 배경에 대한 인구 통계 또는 판매량 합계와 같은 분석 데이터를 제공하기 위해 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서에 지도를 추가할 수 있습니다. 지도에는 여러 계층이 포함될 수 있으며, 각 계층에는 위치를 나타내는 점, 길을 나타내는 선, 영역을 나타내는 다각형 등의 특정 공간 데이터 유형으로 정의되는 지도 요소가 표시됩니다. 각 계층에서 분석 데이터와 지도 요소를 연결할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="MapPurpose"></a> 지도의 목적 지정  
 훌륭한 보고서 디자인은 사용자가 문제를 해결하기 위해 조치를 취하는 데 도움이 되는 정보를 제공합니다. 유용하고 이해하기 쉬운 지도 표시를 만들려면 지도에서 무엇을 알고 싶어하는지를 결정합니다. 예를 들어 지도에서 시장 기회를 나타내기 위해 다음과 같은 유형의 데이터를 시각화할 수 있습니다.  
  
-   각 상점의 상대적 판매량  
  
-   상점 위치에 상대적인 고객 위치에 따라 고객 인구별로 구분된 판매량  
  
-   판매 지역별 비교 판매량 또는 기타 재무 데이터  
  
-   여러 상점의 할인 전략별 비교 판매량  
  
 지도 표시의 목적을 파악한 후 필요한 데이터를 분석해야 합니다. 분석 데이터는 보고서 데이터 세트에서 제공됩니다. 위치 데이터는 지정해야 하는 공간 데이터 원본에서 제공됩니다.  
  
##  <a name="Data"></a> 공간 및 분석 데이터 지정  
 필요한 공간 및 분석 데이터를 지정해야 합니다.  
  
 분석 데이터는 보고서 데이터 세트, 지도 갤러리의 지도에 포함된 예제 데이터 또는 ESRI 셰이프 파일에서 공간 데이터와 함께 포함된 분석 데이터에서 제공됩니다.  
  
 공간 데이터는 점, 선 및 다각형 형태로 제공됩니다.  
  
-   **점.** 점은 위치를 지정합니다(예: 도시나 상점, 식당 또는 컨벤션 센터의 주소). 지도에 표시할 모든 위치에 대한 공간 데이터를 제공해야 합니다. 지도에 점을 추가한 후 점 위치에 표식을 표시하고 표식 유형, 크기 및 색을 변경할 수 있습니다.  
  
-   **선.** 선은 배달 경로나 비행 경로와 같은 경로를 지정합니다. 지도에 선을 추가한 후 선 색과 선 두께를 변경할 수 있습니다.  
  
-   **다각형.** 다각형은 영역을 지정합니다. 예를 들어, 지역, 영토, 국가, 주, 지방, 군, 도시 또는 여러 도시, 우편 번호, 전화 교환국 또는 인구 조사 구역에서 포괄하는 지역을 지정합니다. 지도에 다각형을 추가한 후 외곽선을 표시하는 것 외에 다각형 영역의 중심점에 표식을 표시할 수 있습니다.  
  
 필요한 공간 데이터를 파악한 후 공간 데이터의 원본을 찾아야 합니다.  
  
### <a name="find-a-source-for-spatial-data"></a>공간 데이터 원본 찾기  
 지도에서 사용할 공간 데이터를 찾으려면 다음 원본을 사용할 수 있습니다.  
  
-   인터넷에서 검색할 수 있으며 공개적으로 사용할 수 있는 셰이프 파일을 비롯한 ESRI 셰이프 파일  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공간 데이터 원본의 공간 데이터  
  
-   지도 갤러리에 있는 보고서의 지도  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공간 데이터 또는 ESRI 셰이프 파일인 공간 데이터를 제공하는 타사 사이트  
  
-   지도 보기의 배경을 제공하는 Bing Maps 타일. 지도에 타일을 표시하려면 보고서 서버가 Bing Maps 웹 서비스를 지원하도록 구성되어 있어야 합니다.  
  
 자세한 내용은 [지도 마법사 및 지도 계층 마법사&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)에서 "ESRI 셰이프 파일을 어떻게 구할 수 있나요?"를 참조하세요.  
  
 공간 데이터는 정치적으로 중요한 정보일 수 있으며 저작권이 있을 수 있습니다. 공간 데이터 원본의 사용 조건과 개인 정보 취급 방침을 확인하여 보고서에서 공간 데이터를 사용하는 방법을 파악해야 합니다.  
  
 원하는 데이터를 찾은 후 보고서 정의에 데이터를 포함하거나 보고서가 처리될 때 데이터를 동적으로 검색할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [보고서 정의 크기와 보고서 처리 시간의 균형 맞추기](#Embedding) 를 참조하십시오.  
  
### <a name="determine-the-spatial-data-and-the-spatial-data-match-fields"></a>공간 데이터 및 공간 데이터 일치 필드 결정  
 지도에 분석 데이터를 표시하고 크기, 색 또는 표식 유형을 변경하려면 공간 데이터와 분석 데이터를 연결하는 필드를 지정해야 합니다.  
  
 공간 데이터에는 다음 필드가 포함되어야 합니다.  
  
-   **Spatial data.** 각 점, 선 또는 다각형을 정의하는 좌표 집합이 있는 공간 데이터 필드입니다.  
  
-   **일치 필드.** 각 공간 데이터 필드를 고유하게 식별하는 하나 이상의 필드입니다. 예를 들어 상점 위치 점의 경우 상점의 이름을 사용할 수 있습니다. 상점 이름이 공간 데이터에서 고유하지 않으면 상점 이름뿐만 아니라 도시 이름도 포함할 수 있습니다.  
  
 일치 필드는 공간 데이터를 분석 데이터와 연결하는 데 사용됩니다.  
  
### <a name="determine-the-analytical-data-and-the-analytical-data-match-fields"></a>분석 데이터 및 분석 데이터 일치 필드 결정  
 공간 데이터를 식별한 후 분석 데이터를 식별해야 합니다. 분석 데이터가 제공되는 원본은 다음과 같습니다.  
  
-   기존 보고서 데이터 세트. 필드는 간단한 필드 식으로 지정됩니다(예: [Sales] 또는 =Fields!Sales.Value).  
  
-   공간 데이터 원본에서 제공하는 데이터 필드. 필드는 #으로 시작하고 공간 데이터 원본에 있는 필드 이름으로 구성된 키워드로 지정됩니다.  
  
 그런 다음 일치 필드의 이름을 결정해야 합니다.  
  
-   일치 필드. 공간 데이터와 분석 데이터 간의 관계를 만들기 위해 공간 데이터 일치 필드와 동일한 정보를 지정하는 하나 이상의 필드입니다. 일치 필드는 형식뿐만 아니라 데이터 형식도 일치시킵니다.  
  
 공간 데이터 원본, 공간 데이터, 분석 데이터 원본, 분석 데이터 및 일치 필드를 식별했으면 보고서에 추가할 지도 유형을 결정할 준비가 된 것입니다.  
  
##  <a name="MapType"></a> 지도 유형 선택  
 지도 마법사를 실행할 때 보고서에 지도와 첫 번째 지도 계층을 추가합니다. 지도 마법사를 사용하여 다음 유형의 지도 중 하나를 보고서에 추가할 수 있습니다.  
  
-   분석 데이터가 연결되지 않은 위치를 표시하는 기본 지도  
  
-   각 상점 위치의 판매량 합계와 같이 각 지도 요소와 연결된 분석 값이 하나인 지도  
  
-   각 상점 위치의 고객 수 및 판매량 합계와 같이 지도 요소와 연결된 분석 값이 두 개 이상인 지도  
  
 다음 표에서는 각 지도 유형에 대해 설명합니다. 모든 지도 유형에서 색상표, 테두리 스타일 및 글꼴을 제어하는 테마를 선택하고 레이블을 표시할 수 있습니다.  
  
|마법사 아이콘|계층 스타일|계층 유형|설명 및 옵션|  
|-----------------|-----------------|----------------|-----------------------------|  
|![rs_MapType_Polygon_Basic](../../reporting-services/report-design/media/rs-maptype-polygon-basic.gif "rs_MapType_Polygon_Basic")|기본 지도|Polygon|영역만 표시하는 지도입니다(예: 판매 지역).<br /><br /> 옵션: 색상표에 따라 색을 변경하거나 한 가지 색을 사용합니다. 색상표는 미리 정의된 색 집합입니다. 색상표의 모든 색이 할당되었으면 색의 음영이 할당됩니다.|  
|![rs_MapType_Polygon_ColorAnalytical](../../reporting-services/report-design/media/rs-maptype-polygon-coloranalytical.gif "rs_MapType_Polygon_ColorAnalytical")|색 분석 지도|Polygon|색을 변경하여 분석 데이터를 표시하는 지도입니다(예: 지역별 판매량 데이터).|  
|![rs_MapType_Polygon_Bubble](../../reporting-services/report-design/media/rs-maptype-polygon-bubble.gif "rs_MapType_Polygon_Bubble")|거품형 지도|Polygon|지역 중심의 거품 크기를 변경하여 분석 데이터를 표시하는 지도입니다(예: 지역별 판매량 데이터).<br /><br /> 옵션: 두 번째 분석 필드에 따라 영역 색을 변경하고 색 규칙을 지정합니다.|  
|![rs_MapType_Line_Basic](../../reporting-services/report-design/media/rs-maptype-line-basic.gif "rs_MapType_Line_Basic")|기본 선 지도|꺾은선형|선만 표시하는 지도입니다(예: 배달 경로).<br /><br /> 옵션: 색상표에 따라 색을 변경하거나 한 가지 색을 사용합니다.|  
|![rs_MapType_Line_Analytical](../../reporting-services/report-design/media/rs-maptype-line-analytical.gif "rs_MapType_Line_Analytical")|분석 선 지도|꺾은선형|선 색 및 두께를 변경하는 지도입니다(예: 경로별 정기 메트릭 및 배달된 물품 수).<br /><br /> 옵션: 한 분석 필드에 따라 선 두께를 변경하고, 두 번째 분석 필드에 따라 선 색을 변경하고, 색 규칙을 지정합니다.|  
|![rs_MapType_Marker_Basic](../../reporting-services/report-design/media/rs-maptype-marker-basic.gif "rs_MapType_Marker_Basic")|기본 표식 지도|Point|도시와 같은 각 위치에 표식을 표시하는 지도입니다.<br /><br /> 옵션: 색상표에 따라 색을 변경하거나 한 가지 색을 사용하고 표식 스타일을 변경합니다.|  
|![rs_MapType_Marker_Bubble](../../reporting-services/report-design/media/rs-maptype-marker-bubble.gif "rs_MapType_Marker_Bubble")|거품형 표식 지도|Point|각 위치에 대한 거품을 표시하고 한 분석 데이터 필드에 따라 거품 크기를 변경하는 지도입니다(예: 도시별 판매량 데이터).<br /><br /> 옵션: 두 번째 분석 필드에 따라 거품 색을 변경하고 색 규칙을 지정합니다.|  
|![rs_MapType_Marker_Analytical](../../reporting-services/report-design/media/rs-maptype-marker-analytical.gif "rs_MapType_Marker_Analytical")|분석 표식 지도|Point|각 위치에 표식을 표시하고 분석 데이터에 따라 표식 색, 크기 및 유형을 변경하는 지도입니다(예: 가장 많이 판매된 제품, 수익 범위 및 할인 전략).<br /><br /> 옵션: 한 분석 필드에 따라 표식 유형을 변경하고, 두 번째 분석 필드에 따라 표식 크기를 변경하고, 세 번째 분석 필드에 따라 표식 색을 변경하고, 색 규칙을 지정합니다.|  
  
 지도 마법사를 사용하여 지도를 추가한 후 계층 마법사를 사용하여 추가 계층을 만들거나 계층에 대한 옵션을 변경할 수 있습니다. 마법사에 대한 자세한 내용은 [지도 마법사 및 지도 계층 마법사&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)를 참조하세요.  
  
 각 계층의 표시 또는 데이터 옵션을 독립적으로 사용자 지정할 수 있습니다. 마법사 실행 후 지도 사용자 지정에 대한 자세한 내용은 [지도 또는 지도 계층의 데이터 및 표시 사용자 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)에서 “ESRI 셰이프 파일을 어떻게 구할 수 있나요?”를 참조하세요.  
  
##  <a name="Legend"></a> 범례 계획  
 사용자가 지도를 해석하는 데 도움이 되도록 여러 지도 범례, 색 눈금 및 거리 눈금을 추가할 수 있습니다. 지도를 디자인할 때 범례를 표시할 위치를 계획해야 합니다. 각 범례에 대한 다음 정보를 지정할 수 있습니다.  
  
-   **범례 위치.** 예를 들어 범례는 뷰포트 내부 또는 외부와 뷰포트와 상대적인 12곳의 별도 위치에 표시될 수 있습니다.  
  
-   **범례 스타일**. 예를 들어 글꼴 스타일, 테두리 스타일, 구분 기호 선 및 채우기 속성을 지정할 수 있습니다.  
  
-   **범례 제목.** 예를 들어 제목 텍스트를 지정할 수 있으며 색 눈금이나 지도 범례의 제목을 표시할지 여부를 독립적으로 제어할 수 있습니다.  
  
-   **지도 범례 레이아웃.** 예를 들어 지도 범례는 긴 표나 넓은 표로 표시될 수 있습니다.  
  
 범례의 내용은 각 계층에 설정하는 규칙 옵션에 따라 보고서를 처리하는 동안 자동으로 만들어집니다.  
  
 기본적으로 모든 계층에서는 첫 번째 지도 범례에 규칙의 결과가 표시됩니다. 여러 범례를 만든 다음 각 규칙에 대해 결과를 표시하기 위해 사용할 범례를 할당할 수 있습니다.  
  
 자세한 내용은 [규칙 및 분석 데이터를 사용하여 다각형, 선 및 점 표시 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md) 및 [지도 범례, 색 눈금 및 관련 규칙 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="Embedding"></a> 보고서 정의 크기와 보고서 처리 시간의 균형 맞추기  
 지도를 사용하는 데 효과적으로 보고서를 디자인하려면 보고서 성능을 제어하는 옵션과 보고서 정의 크기를 제어하는 옵션의 균형을 맞춰야 합니다. 공간 데이터나 Bing Maps 타일 기반의 지도 요소는 정적이고 보고서 정의에 포함되거나 동적이고 보고서가 처리될 때마다 만들어질 수 있습니다. 정적 또는 동적 지도 데이터의 장단점을 평가하고 해당 환경에 적합한 균형점을 찾아야 합니다. 이 결정을 내리려면 다음 정보를 고려하십시오.  
  
-   포함된 지도 요소를 사용하면 보고서 정의의 크기가 매우 증가할 수 있지만 보고서에서 지도를 보는 데 필요한 시간을 줄일 수 있습니다. 보고서 서버에는 작업하는 데 필요한 크기 제한이 있을 수 있습니다.  
  
-   보고서 정의는 처리될 수 있는 공간 데이터 요소 수의 한도와 보고서 정의에 포함될 수 있는 지도 요소 수를 지정하는 별도의 값을 지정합니다.  
  
-   동적 지도 요소를 사용하면 보고서 정의의 크기가 줄어들지만 지도를 처리하고 렌더링하는 데 필요한 시간은 늘어납니다.  
  
-   공간 데이터의 원본이 사용자 컴퓨터에 있으면 지도 요소가 항상 보고서 정의에 포함됩니다. 여기에는 로컬에 설치된 ESRI 셰이프 파일 또는 지도 갤러리의 공간 데이터가 포함됩니다.  
  
 동적 공간 데이터를 사용하려면 공간 데이터 원본이 보고서 서버에 있어야 합니다. 보고서가 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 디자인되는 경우 공간 데이터 원본을 프로젝트에 추가하고 보고서 정의와 함께 보고서 서버에 게시할 수 있습니다. 보고서 작성기를 사용하여 보고서를 디자인하는 경우 먼저 공간 데이터를 보고서 서버에 업로드한 다음 마법사나 계층 속성에서 지도 계층의 공간 데이터 원본을 지정해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [지도 또는 지도 계층의 데이터 및 표시 사용자 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [자습서: 맵 보고서&#40;보고서 작성기&#41;](../../reporting-services/tutorial-map-report-report-builder.md)   
 [지도&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [보고서 문제 해결: 맵 보고서&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
