---
title: 지도 또는 지도 계층 추가, 변경 또는 삭제(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10526"
- sql12.rtp.rptdesigner.maptilelayerproperties.general.f1
- "10529"
- "10525"
- "10535"
- sql12.rtp.rptdesigner.mappolygonlayerproperties.general.f1
- sql12.rtp.rptdesigner.shared.layervisibility.f1
- sql12.rtp.rptdesigner.mappointlayerproperties.general.f1
- sql12.rtp.rptdesigner.shared.layerfilters.f1
- "10524"
- sql12.rtp.rptdesigner.maplayerproperties.general.f1
- sql12.rtp.rptdesigner.maplinelayerproperties.general.f1
- "10532"
- "10528"
- "10527"
- sql12.rtp.rptdesigner.maplayerproperties.analyticaldata.f1
ms.assetid: 6e89815e-187e-45bf-bf63-3d5c4a246360
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 13a67a94f6478c085995142085a93fa85bb27d89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106713"
---
# <a name="add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs"></a>지도 또는 지도 계층 추가, 변경 또는 삭제(보고서 작성기 및 SSRS)
  지도는 계층의 모음입니다. 보고서에 지도를 추가할 때 첫 번째 계층을 정의합니다. 지도 계층 마법사를 사용하여 추가 계층을 만들 수 있습니다.  
  
 계층의 옵션을 추가, 제거 또는 변경하는 가장 쉬운 방법은 지도 계층 마법사를 사용하는 것입니다. 지도 창에서 옵션을 수동으로 변경할 수도 있습니다. **지도** 창을 표시하려면 보고서 디자인 화면에서 지도를 클릭합니다. 다음 그림에서는 창의 일부를 보여 줍니다.  
  
 ![rsMapLayerZone](../media/rsmaplayerzone.gif "rsMapLayerZone")  
  
 지도 계층은 지도 창에 나타나는 순서대로 아래쪽에서 위쪽으로 그려집니다. 위의 그림에서 타일 계층이 가장 먼저 그려지고 다각형 계층이 마지막으로 그려집니다. 이후에 그려지는 계층은 이전에 그려진 계층의 지도 요소를 숨길 수 있습니다. 지도 창 도구 모음에서 화살표 키를 사용하여 계층의 순서를 변경할 수 있습니다. 계층을 표시하거나 숨기려면 표시 유형 아이콘을 설정하거나 해제합니다. 계층의 투명도 변경할 수 있습니다 합니다 `Visibility` 페이지의 **계층 데이터** 속성 대화 상자.  
  
 다음 표에서는 **지도** 창의 도구 모음 아이콘을 보여 줍니다.  
  
|기호|Description|사용 시기|  
|------------|-----------------|-----------------|  
|![rs_IconMapLayerWizard](../../tutorials/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")|지도 계층 마법사|마법사를 사용하여 계층을 추가하려면 **새 계층 마법사**를 클릭합니다.|  
|![rs_IconMapAddLayer](../../tutorials/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer")|계층 추가|계층을 수동으로 추가하려면 **계층 추가**를 클릭한 다음 추가할 지도 계층의 유형을 클릭합니다.|  
|![rs_IconMapPolygonLayer](../media/rs-iconmappolygonlayer.gif "rs_IconMapPolygonLayer")|다각형 계층|다각형 좌표의 집합을 기반으로 영역이나 모양을 표시하는 지도 계층을 추가합니다.|  
|![rs_IconMapLineLayer](../media/rs-iconmaplinelayer.gif "rs_IconMapLineLayer")|선 계층|선 좌표의 집합을 기반으로 경로를 표시하는 지도 계층을 추가합니다.|  
|![rs_IconMapPointLayer](../media/rs-iconmappointlayer.gif "rs_IconMapPointLayer")|점 계층|점 좌표의 집합을 기반으로 위치를 표시하는 지도 계층을 추가합니다.|  
|![rs_IconMapTileLayer](../media/rs-iconmaptilelayer.gif "rs_IconMapTileLayer")|타일 계층|뷰포트가 정의하는 현재 지도 보기 영역에 해당하는 Bing Maps 타일을 표시하는 지도 계층을 추가합니다.|  
  
 지도 창의 아래쪽에는 지도 보기 영역이 있습니다. 지도의 중심 및 확대/축소 옵션을 변경하려면 화살표 키를 사용하여 보기 중심을 조정하고 슬라이더를 사용하여 확대/축소 수준을 조정합니다.  
  
 계층에 대한 자세한 내용은 [지도&#40;보고서 작성기 및 SSRS&#41;](maps-report-builder-and-ssrs.md)를 클릭합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="AddLayer"></a> 지도 계층 마법사에서 계층을 추가하려면  
  
-   리본의 **삽입** 메뉴에서 **지도**를 클릭한 다음 **지도 Wizard.** 를 클릭합니다. 이 마법사를 사용하여 기존 지도에 계층을 추가할 수 있습니다. 지도 마법사와 지도 계층 마법사의 마법사 페이지는 대부분 동일합니다.  
  
     자세한 내용은 [지도 마법사 및 지도 계층 마법사&#40;보고서 작성기 및 SSRS&#41;](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)를 참조하세요.  

##  <a name="ChangeLayer"></a> 지도 계층 마법사를 사용하여 계층의 옵션을 변경하려면  
  
-   지도 계층 마법사를 실행합니다. 이 마법사를 통해 지도 계층 마법사를 사용하여 만든 계층의 옵션을 변경할 수 있습니다. 지도 창에서 계층을 마우스 오른쪽 단추로 클릭한 다음 도구 모음에서 계층 마법사 단추(![rs_IconMapLayerWizard](../../tutorials/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard"))를 클릭합니다.  
  
     자세한 내용은 [지도 마법사 및 지도 계층 마법사&#40;보고서 작성기 및 SSRS&#41;](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)를 참조하세요.  

##  <a name="AddVectorLayer"></a> 지도 창 도구 모음에서 점, 선 또는 다각형 계층을 추가하려면  
  
1.  지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  도구 모음에서 **계층 추가** 단추를 클릭하고 드롭다운 목록의 **점**, **선** 또는 **다각형** 중에서 추가할 계층의 유형을 클릭합니다.  
  
    > [!NOTE]  
    >  지도 계층을 추가하고 수동으로 구성할 수 있지만 지도 계층 마법사를 사용하여 새 계층을 추가하는 것이 좋습니다. 지도 창 도구 모음에서에서 마법사를 시작하려면 계층 마법사 단추(![rs_IconMapLayerWizard](../../tutorials/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard"))를 클릭합니다.  
  
3.  계층을 마우스 오른쪽 단추로 클릭한 다음 **계층 데이터**를 클릭합니다.  
  
4.  **다음의 공간 데이터 사용**에서 공간 데이터의 원본을 선택합니다. 옵션은 선택한 원본에 따라 달라집니다.  
  
     이 계층의 보고서에서 분석을 시각화하려면 다음을 수행합니다.  
  
    1.  **분석 데이터**를 클릭합니다.  
  
    2.  **분석 데이터 집합**에서 분석 데이터와 공간 데이터 간의 관계를 만드는 일치 필드와 분석 데이터가 포함된 데이터 집합의 이름을 클릭합니다.  
  
    3.  **추가**를 클릭합니다.  
  
    4.  공간 데이터 세트에 있는 일치 필드의 이름을 입력합니다.  
  
    5.  분석 데이터 세트에 있는 일치 필드의 이름을 입력합니다.  
  
     공간 및 분석 데이터를 연결하는 방법에 대한 자세한 내용은 [지도 또는 지도 계층의 데이터 및 표시 사용자 지정&#40;보고서 작성기 및 SSRS&#41;](customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)을 참조하세요.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="FilterAnalyticalData"></a> 계층에 대한 분석 데이터를 필터링하려면  
  
1.  지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  지도 창에서 계층을 마우스 오른쪽 단추로 클릭하고  **계층 데이터**를 클릭합니다.  
  
3.  **필터**를 클릭합니다.  
  
4.  지도 표시에 사용되는 분석 데이터를 제한할 필터 수식을 정의합니다. 자세한 내용은 [필터 수식 예&#40;보고서 작성기 및 SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)를 참조하세요.  

##  <a name="PointProperties"></a> 점 계층 또는 다각형 중심점에 대한 점 속성을 제어하려면  
  
1.  **지도 점 속성** 대화 상자에서 **일반** 을 선택하여 다음 지도 요소의 레이블, 도구 설명 및 표식 유형 옵션을 변경할 수 있습니다.  
  
    -   점 계층의 모든 동적 또는 포함된 점. 점의 색 규칙, 크기 규칙 및 표식 유형 규칙은 이러한 옵션을 무시합니다. 특정 포함된 점에 대한 옵션을 무시하려면 [Map Embedded Point Properties Dialog Box, Marker](../map-embedded-point-properties-dialog-box-marker.md) 페이지를 사용합니다.  
  
    -   다각형 계층의 모든 동적 또는 포함된 다각형에 대한 중심점. 중심점의 색 규칙, 크기 규칙 및 표식 유형 규칙은 이러한 옵션을 무시합니다. 특정 중심점에 대한 옵션을 무시하려면 [지도 포함 점 속성 대화 상자, 표식](../map-embedded-point-properties-dialog-box-marker.md) 페이지를 사용합니다.  

##  <a name="Embedded"></a> 포함된 데이터를 공간 데이터의 원본으로 지정하려면  
  
1.  지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  계층을 마우스 오른쪽 단추로 클릭한 다음 **계층 데이터**를 클릭합니다.  
  
3.  **다음의 공간 데이터 사용**에서 **보고서에 포함된 데이터**를 선택합니다.  
  
4.  기존 보고서에서 지도 요소를 로드하거나 ESRI 파일에 따라 지도 요소를 만들려면 **찾아보기**를 클릭하고 파일을 가리킨 다음 **열기**를 클릭합니다. 지도 요소는 이 보고서 정의에 포함됩니다. 가리키는 공간 데이터는 계층 유형과 일치해야 합니다. 예를 들어 점 계층의 경우 점 좌표의 집합을 지정하는 공간 데이터를 가리켜야 합니다.  
  
5.  **공간 필드**에서 공간 데이터가 포함된 필드의 이름을 지정합니다. 공간 데이터의 원본에서 이 이름을 확인해야 할 수 있습니다.  
  
    > [!NOTE]  
    >  필드의 이름을 모르고 ESRI 셰이프 파일로 이동한 경우 이 옵션 대신 **ESRI 셰이프 파일에 연결** 옵션을 사용합니다.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="ESRI"></a> ESRI 셰이프 파일을 공간 데이터의 원본으로 지정하려면  
  
1.  지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  계층을 마우스 오른쪽 단추로 클릭한 다음 **계층 데이터**를 클릭합니다.  
  
3.  **다음의 공간 데이터 사용**에서 **ESRI 셰이프 파일에 연결**을 선택합니다.  
  
4.  **파일 이름**에 ESRI 셰이프 파일의 위치를 입력하거나 **찾아보기** 를 클릭하여 ESRI 셰이프 파일을 선택합니다.  
  
    > [!NOTE]  
    >  셰이프 파일이 로컬 컴퓨터에 있는 경우 공간 데이터가 보고서 정의에 포함됩니다. 보고서가 처리될 때 데이터를 동적으로 검색하려면 ESRI .shp 파일 및 해당 .dbf 지원 파일을 보고서 서버로 업로드해야 합니다. 자세한 내용은 "방법: 파일 또는 보고서 업로드 (보고서 관리자) "에 [Reporting Services 설명서](https://go.microsoft.com/fwlink/?linkid=121312) SQL Server 온라인 설명서의 합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="DatasetField"></a> 보고서 데이터 집합 필드를 공간 데이터의 원본으로 지정하려면  
  
1.  지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  계층을 마우스 오른쪽 단추로 클릭한 다음 **계층 데이터**를 클릭합니다.  
  
3.  **다음의 공간 데이터 사용**에서 **데이터 집합의 공간 필드**를 선택합니다.  
  
4.  **데이터 집합 이름**에서 원하는 공간 데이터가 포함된 보고서의 데이터 집합 이름을 클릭합니다.  
  
5.  **공간 필드 이름**에서 공간 데이터가 포함된 데이터 세트의 필드 이름을 클릭합니다.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="TileLayer"></a> 타일 계층을 추가하려면  
  
1.  지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  도구 모음에서 **계층 추가** 단추를 클릭하고 드롭다운 목록에서 **타일 계층**을 클릭합니다.  
  
    > [!NOTE]  
    >  보고서에서 Bing 지도 타일을 사용하는 방법은 [추가 사용 조건(Additional Terms of Use)](https://go.microsoft.com/fwlink/?LinkId=151371) 및 [개인 정보 취급 방침](https://go.microsoft.com/fwlink/?LinkId=151372)을 참조하십시오.  
  
3.  지도 창에서 타일 계층을 마우스 오른쪽 단추로 클릭한 다음 **타일 속성**을 클릭합니다.  
  
4.  **타일 옵션**에서 타일 스타일을 선택합니다. Bing Maps 타일을 사용할 수 있으면 디자인 화면의 계층이 선택한 스타일로 업데이트됩니다.  
  
    > [!NOTE]  
    >  지도 또는 지도 계층 마법사에서 다각형, 선 또는 점 계층을 추가할 때 타일 계층도 추가할 수 있습니다. **공간 데이터 및 지도 보기 옵션 선택** 페이지에서 **이 지도 보기에 대해 Bing Maps 배경 추가**옵션을 선택합니다.  

##  <a name="DrawingOrder"></a> 계층의 그리기 순서를 변경하려면  
  
1.  지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  지도 창에서 계층을 클릭하여 선택합니다.  
  
3.  지도 창 도구 모음에서 위로 또는 아래로 화살표를 클릭하여 각 계층의 그리기 순서를 변경합니다.  

##  <a name="Transparency"></a> 다각형, 선 또는 점 계층의 투명도를 변경하려면  
  
1.  지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  계층을 마우스 오른쪽 단추로 클릭한 다음 **계층 데이터**를 클릭합니다.  
  
3.  `Visibility`을 클릭합니다.  
  
4.  **투명도 옵션**에서 투명도를 나타내는 값(%)을 입력합니다(예: **40**). 0% 투명도는 계층이 불투명함을 의미합니다. 100% 투명도는 보고서에서 계층을 볼 수 없음을 의미합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="TileTransparency"></a> 타일 계층의 투명도를 변경하려면  
  
1.  지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  계층을 마우스 오른쪽 단추로 클릭한 다음 **타일 속성**을 클릭합니다.  
  
3.  `Visibility`을 클릭합니다.  
  
4.  **투명도 옵션**에서 투명도를 나타내는 값(%)을 입력합니다(예: **40**).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="Secure"></a> 타일 계층에 대한 보안 연결을 지정하려면  
  
1.  지도 창이 나타날 때까지 지도를 클릭합니다.  
  
2.  지도 창에서 타일 계층을 클릭하여 선택합니다. 속성 창에 타일 계층 속성이 표시됩니다.  
  
3.  속성 창에서 UseSecureConnection을 **True**로 설정합니다.  
  
 Bing Maps 웹 서비스의 연결에서는 HTTP SSL(Secure Sockets Layer) 서비스를 사용하여 해당 계층에 대한 Bing Maps 타일을 검색합니다.  

##  <a name="Language"></a> 타일 레이블의 언어를 지정하려면  
  
1.  기본적으로 레이블을 표시하는 타일 스타일의 경우 언어는 보고서 작성기에 대한 기본 로캘에서 결정됩니다. 다음과 같은 방법으로 타일 레이블에 대한 언어 설정을 사용자 지정할 수 있습니다.  
  
    -   뷰포트 외부의 지도를 클릭하여 선택합니다. 속성 창의 드롭다운 목록에서 TileLanguage 속성에 대한 문화권 값을 선택합니다.  
  
    -   보고서 배경을 클릭하여 보고서를 선택합니다. 속성 창의 드롭다운 목록에서 Language 속성에 대한 문화권 값을 선택합니다.  
  
     타일 레이블 언어 설정의 우선 순위는 보고서 속성 Language, 보고서 작성기에 대한 기본 로캘 및 지도 속성 TileLanguage입니다.  

##  <a name="ConditionalHide"></a> 뷰포트 확대/축소 수준을 기반으로 계층을 조건에 따라 숨기려면  
  
1.  설정 `Visibility` 지도 계층에 대 한 표시를 제어 하는 옵션입니다.  
  
    -   지도 계층 창에서 계층을 마우스 오른쪽 단추로 클릭하여 선택하고 지도 계층 도구 모음에서 속성을 클릭하여 **지도 계층 속성**을 클릭합니다.  
  
    -   `Visibility`을 클릭합니다.  
  
    -   계층 표시 유형에서 **확대/축소 값에 따라 표시 또는 숨기기**를 선택합니다.  
  
    -   계층을 표시할 때 사용할 최소 및 최대 확대/축소 값을 입력합니다.  
  
    -   (선택 사항) 투명도 값을 입력합니다.  
  
     조건에 따라 계층을 숨길 수도 있습니다. 자세한 내용은 [항목 숨기기&#40;보고서 작성기 및 SSRS&#41;](../report-builder/hide-an-item-report-builder-and-ssrs.md)를 참조하세요.  

## <a name="see-also"></a>관련 항목  
 [지도&#40;보고서 작성기 및 SSRS&#41;](maps-report-builder-and-ssrs.md)   
 [보고서 문제 해결: 맵 보고서&#40;보고서 작성기 및 SSRS&#41;](troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
