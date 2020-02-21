---
title: '자습서: 맵 보고서(보고서 작성기) | Microsoft Docs'
ms.date: 08/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 8d831356-7efa-40cc-ae95-383b3eecf833
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4db47bde02745ddc554f17e1f951c836c1542cc8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63041668"
---
# <a name="tutorial-map-report-report-builder"></a>자습서: 지도 보고서(보고서 작성기)
이 [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] 자습서에서는 페이지가 매겨진 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 보고서에 지리적 배경 데이터를 표시하는 데 사용할 수 있는 지도 기능에 대해 알아봅니다. 
  
지도는 일반적으로 점, 선 및 다각형으로 구성된 공간 데이터를 기반으로 합니다. 예를 들어 다각형으로는 군의 경계를 나타내고, 선으로는 도로를 나타내며, 점으로는 도시의 위치를 나타낼 수 있습니다. 각 공간 데이터 형식은 별도의 지도 계층에 지도 요소 집합으로 표시됩니다.  
  
지도 요소의 모양을 변경하려면 지도 요소를 데이터 세트의 분석 데이터와 일치시키는 값이 있는 필드를 지정합니다. 또한 데이터의 범위에 따라 색, 크기 또는 기타 속성을 변경하는 규칙을 정의할 수도 있습니다.  

![report-builder-map-final-map-only](../reporting-services/media/report-builder-map-final-map-only.png)
  
이 자습서에서는 뉴욕 주의 군에 있는 상점 위치를 표시하는 지도 보고서를 작성합니다.  
   
> [!NOTE]  
> 이 자습서에서 마법사의 단계는 두 개의 절차로 통합됩니다. 하나는 데이터 세트를 만드는 절차이고 다른 하나는 테이블을 만드는 절차입니다. 보고서 서버를 찾고, 데이터 원본을 선택하고, 데이터 세트를 만들고, 마법사를 실행하는 방법에 대한 단계별 지침은 이 시리즈의 첫 번째 자습서를 참조하세요. [자습서: 기본 테이블 보고서 만들기&#40;보고서 작성기&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
이 자습서에 소요되는 예상 시간: 30분.  
  
## <a name="requirements"></a>요구 사항  
이 자습서에서는 Bing 지도를 배경으로 지원하도록 보고서 서버를 구성해야 합니다. 자세한 내용은 [지도 보고서 지원 계획](https://msdn.microsoft.com/5ddc97a7-7ee5-475d-bc49-3b814dce7e19)을 참조하세요. 

기타 요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)을 참조하세요.  
  
## <a name="Map"></a>1. 지도 마법사에서 다각형 계층을 사용하여 지도 만들기  
이 섹션에서는 지도 갤러리에서 보고서에 지도를 추가합니다. 뉴욕 주의 군을 표시하는 계층이 하나 있는 지도를 추가합니다. 각 군의 모양은 지도 갤러리의 지도에 포함된 공간 데이터를 기반으로 하는 다각형으로 되어 있습니다.  
  
### <a name="to-add-a-map-with-the-map-wizard-in-a-new-report"></a>새 보고서에서 지도 마법사를 사용하여 지도를 추가하려면  
  
1.  컴퓨터,[웹 포털 또는 SharePoint 통합 모드에서](../reporting-services/report-builder/start-report-builder.md) 보고서 작성기를 시작 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 합니다.  
  
    **새 보고서 또는 데이터 세트** 대화 상자가 열립니다.  
  
    **새 보고서 또는 데이터 세트** 대화 상자가 표시되지 않는 경우 **파일** 메뉴 &gt; **새로 만들기**를 클릭합니다.  
  
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **지도 마법사**를 클릭합니다.  
  
4.  **공간 데이터의 원본 선택** 페이지에서 **지도 갤러리** 가 선택되어 있는지 확인합니다.  
  
6.  지도 갤러리 상자의 **USA** 에서 **States by County**를 확장하고 **New York**을 클릭합니다.  
  
    지도 미리 보기 창에 뉴욕 주 지도가 표시됩니다.  
    
    ![report-builder-map-ny-counties](../reporting-services/media/report-builder-map-ny-counties.png)
  
7.  **다음**을 클릭합니다.  
  
8.  **공간 데이터 및 지도 보기 옵션 선택** 페이지에서 기본값을 적용하고 **다음**을 클릭합니다. 
 
    기본적으로 지도 갤러리의 지도 요소는 보고서 정의에 자동으로 포함됩니다.  
  
9. **지도 시각화 선택** 페이지에서 **기본 지도** 가 선택되어 있는지 확인하고 **다음**을 클릭합니다.  
  
11. **색 테마 및 데이터 시각화 선택** 페이지에서 **레이블 표시** 옵션을 선택합니다.  
  
12. **단색 지도** 옵션이 선택되어 있으면 선택을 취소합니다.  
  
13. **데이터 필드** 드롭다운 목록에서 **#COUNTYNAME**을 클릭합니다. 마법사의 지도 미리 보기 창에 다음 항목이 표시됩니다.  
  
    -   **지도 제목**텍스트가 포함된 제목  
  
    -   뉴욕의 군을 표시하는 지도. 각 군이 다른 색이고 군 이름이 군 지역 위의 적절한 곳에 나타납니다.  
  
    -   제목과 항목 1 ~ 5의 목록이 포함된 범례  
  
    -   값 1 ~ 160이 포함되고 색이 없는 색 눈금  
  
    -   킬로미터(km) 및 마일(mi)이 표시되는 거리 눈금  
    
    ![report-builder-map-choose-color-theme](../reporting-services/media/report-builder-map-choose-color-theme.png)
  
14. **Finish**를 클릭합니다.  
  
    디자인 화면에 지도가 추가됩니다.  
  
13. "지도 제목" 텍스트를 선택하고 **Sales by Store**를 입력한 후 Enter 키를 누릅니다.  

15. 지도를 두 번 클릭하여 **지도 계층**창을 표시합니다. **지도 계층** 창에는 **포함**계층 유형의 다각형 계층인 PolygonLayer1이 표시됩니다. 각 군은 이 계층의 포함된 지도 요소입니다.  
  
    > [!NOTE]  
    > **지도 계층** 창이 보이지 않는 경우 현재 보기의 외부에 표시되어 있을 수 있습니다. 디자인 뷰 창의 아래쪽에 있는 스크롤 막대를 사용하여 뷰를 변경합니다. 또는 **보기** 탭에서 **보고서 데이터** 옵션의 선택을 취소하여 디자인 화면 영역을 더 제공합니다.   

15. PolygonLayer1 옆의 화살표 > **다각형 속성**을 선택합니다.

16. **글꼴** 탭에서 색을 **어두운 회색**으로 변경합니다.

17. **홈** 탭 > **실행**을 선택하여 보고서를 미리 봅니다.  
  
    ![report-builder-map-first-preview](../reporting-services/media/report-builder-map-first-preview.png)
  
렌더링된 보고서에 지도 제목, 지도 및 거리 눈금이 표시됩니다. 군은 지도 다각형 계층에 있습니다. 각 군은 색상표의 색으로 구분되지만 해당 색은 데이터와 연결되어 있지 않은 다각형으로 되어 있습니다. 거리 눈금에는 킬로미터와 마일 단위로 거리가 표시됩니다.  
  
각 군과 연결된 분석 데이터가 없기 때문에 지도 범례와 색 눈금은 아직 표시되지 않습니다. 이 자습서의 뒷부분에서 분석 데이터를 추가합니다.  
  
## <a name="PointLayer"></a>2. 지도 점 계층을 추가하여 상점 위치 표시  
이 섹션에서는 지도 계층 마법사를 사용하여 상점의 위치를 표시하는 점 계층을 추가합니다.  
  
> [!NOTE]  
> 이 자습서의 쿼리에는 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
### <a name="to-add-a-point-layer-based-on-a-sql-server-spatial-query"></a>SQL Server 공간 쿼리에 따라 점 계층을 추가하려면  
  
1.  **실행** 탭 > **디자인**을 선택하여 디자인 뷰로 다시 전환합니다.  
  
2.  지도를 두 번 클릭하여 **지도 계층** 창을 표시합니다. 도구 모음에서 **새 계층 마법사** 단추 ![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")를 클릭합니다. 

    ![report-builder-map-new-layer-wizard-icon](../reporting-services/media/report-builder-map-new-layer-wizard-icon.png) 
  
3.  **공간 데이터의 원본 선택** 페이지에서 **SQL Server 공간 쿼리**를 선택하고 **다음**을 클릭합니다.  
  
4.  **SQL Server 공간 데이터가 있는 데이터 세트 선택** 페이지에서 **SQL Server 공간 데이터가 있는 새 데이터 세트 추가** > **다음**을 클릭합니다.  
  
5.  **SQL Server 공간 데이터 원본에 대한 연결을 선택하십시오.** 페이지에서 기존 데이터 원본을 선택하거나 보고서 서버로 이동한 후 데이터 원본을 선택합니다.  

    > [!NOTE]  
    > 적절한 권한만 가지고 있으면 선택하는 데이터 원본은 중요하지 않습니다. 데이터를 데이터 원본에서 가져오는 것은 아니기 때문입니다. 자세한 내용은 [데이터에 연결하는 다른 방법&#40;보고서 작성기&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)를 참조하세요.  
  
6.  **다음**을 클릭합니다.  
  
7.  **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다.  
  
8.  다음 텍스트를 복사하여 쿼리 창에 붙여넣습니다.  
  
    ```  
    Select 114 as StoreKey, 'Contoso Albany Store' as StoreName, 1125 as SellingArea, 'Albany' as City, 'Albany' as County,   
     CAST(1000000 as money) as Sales, CAST('POINT(-73.7472924218681 42.6564617079878)' as geography) AS SpatialLocation  
    UNION ALL SELECT 115 AS StoreKey, 'Contoso New York No.1 Store' AS  StoreName, 500 as SellingArea, 'New York' AS City, 'New York City' as County,  
     CAST('2000000' as money) as Sales, CAST('POINT(-73.9922069374483 40.7549638237402)' as geography) AS SpatialLocation  
    UNION ALL Select 116 as StoreKey, 'Contoso Rochester No.1 Store' as StoreName, 462 as SellingArea, 'Rochester' as City,  'Monroe' as County,    
     CAST(3000000 as money) as Sales, CAST('POINT(-77.624041566786 43.1547066024338)' as geography)  AS SpatialLocation  
    UNION ALL Select 117 as StoreKey, 'Contoso New York No.2 Store' as StoreName, 700 as SellingArea, 'New York' as City,'New York City' as County,    
      CAST(4000000 as money) as Sales, CAST('POINT(-73.9712488 40.7830603)' as geography) AS SpatialLocation  
    UNION ALL Select 118 as StoreKey, 'Contoso Syracuse Store' as StoreName, 680 as SellingArea, 'Syracuse' as City, 'Onondaga' as County,  
     CAST(5000000 as money) as Sales, CAST('POINT(-76.1349120532546 43.0610223535974)' as geography) AS SpatialLocation  
    UNION ALL Select 120 as StoreKey, 'Contoso Plattsburgh Store' as StoreName, 560 as SellingArea, 'Plattsburgh' as City,  'Clinton' as County,  
     CAST(6000000 as money) as Sales, CAST('POINT(-73.4728622833178 44.7028831413324)' as geography) AS SpatialLocation  
    UNION ALL Select 121 as StoreKey, 'Contoso Brooklyn Store' as StoreName, 1125 as SellingArea, 'Brooklyn' as City, 'New York City' as County,  
     CAST(7000000 as money) as Sales, CAST('POINT (-73.9638533447143 40.6785123489351)' as geography) AS SpatialLocation  
    UNION ALL Select 122 as StoreKey, 'Contoso Oswego Store' as StoreName, 500 as SellingArea, 'Oswego' as City, 'Oswego' as County,    
     CAST(8000000 as money) as Sales, CAST('POINT(-76.4602850815536 43.4353224527794)' as geography) AS SpatialLocation  
    UNION ALL Select 123 as StoreKey, 'Contoso Ithaca Store' as StoreName, 460 as SellingArea, 'Ithaca' as City, 'Tompkins' as County,  
     CAST(9000000 as money) as Sales, CAST('POINT(-76.5001866085881 42.4310489934743)' as geography) AS SpatialLocation  
    UNION ALL Select 124 as StoreKey, 'Contoso Buffalo Store' as StoreName, 700 as SellingArea, 'Buffalo' as City, 'Erie' as County,    
     CAST(100000 as money) as Sales, CAST('POINT(-78.8784 42.8864)' as geography) AS SpatialLocation  
    UNION ALL Select 125 as StoreKey, 'Contoso Queens Store' as StoreName, 700 as SellingArea,'Queens' as City, 'New York City' as County,  
     CAST(500000 as money) as Sales, CAST('POINT(-73.7930979029883 40.7152781765927)' as geography) AS SpatialLocation  
    UNION ALL Select 126 as StoreKey, 'Contoso Elmira Store' as StoreName, 680 as SellingArea, 'Elmira' as City, 'Chemung' as County,  
     CAST(800000 as money) as Sales, CAST('POINT(-76.7397414783301 42.0736492742663)' as geography) AS SpatialLocation  
    UNION ALL Select 127 as StoreKey, 'Contoso Poestenkill Store' as StoreName, 455 as SellingArea, 'Poestenkill' as City, 'Rensselaer' as County,    
    CAST(1500000 as money) as Sales, CAST('POINT(-73.5626737425063 42.6940551238618)' as geography) AS SpatialLocation  
    ```  
  
9. 쿼리 디자이너 도구 모음에서 **실행** ( **!** )을 클릭합니다.  
  
    결과 집합에는 소비재를 판매하는 뉴욕 주의 상점 집합을 나타내는 7개의 열이 포함됩니다. 명확하지 않은 열에 대한 설명을 포함하는 목록은 다음과 같습니다. 
    *   **StoreKey**: 상점 식별자입니다.  
    *   **StoreName**.
    *   **SellingArea**: 455평방피트에서 1125평방피트 사이의 제품 전시 영역입니다.
    *   **City**.
    *   **County**.
    *   **판매**: 총 판매량입니다. 
    *   **SpatialLocation**: 경도 및 위도 위치입니다. 

    ![report-builder-map-design-query](../reporting-services/media/report-builder-map-design-query.png) 
  
10. **다음**을 클릭합니다.  
  
    DataSet1이라는 보고서 데이터 세트가 만들어집니다. 마법사를 완료하면 보고서 데이터 창에서 해당 필드 컬렉션을 볼 수 있습니다.  
  
11. **공간 데이터 및 지도 보기 옵션 선택** 페이지에서 **공간 필드** 가 **SpatialLocation** 이고 **계층 유형** 이 **점**인지 확인합니다. 이 페이지의 다른 기본값을 적용합니다.  
  
    지도 보기에 각 상점의 위치를 표시하는 원이 표시됩니다.  
  
12. **다음**을 클릭합니다.  
  
13. 지도 시각화 선택 페이지에서 데이터에 따라 크기가 달라지는 표식을 표시하는 **거품형 지도** 를 지도 유형으로 클릭합니다. **다음**을 클릭합니다.  
  
14. **분석 데이터 세트 선택** 페이지에서 DataSet1을 클릭하고 **다음**을 클릭합니다. 이 데이터 세트에는 새 점 계층에 표시될 분석 데이터와 공간 데이터가 모두 들어 있습니다.   
  
16. **색 테마 및 데이터 시각화 선택** 페이지에서 **거품 크기를 사용하여 데이터 시각화**를 선택합니다.  
  
17. **데이터 필드**에서 `[Sum(SellingArea)]` 을 선택하고 제품을 전시하기 위해 따로 설정한 영역의 크기에 맞춰 거품 크기를 변경합니다.  
  
18. **레이블 표시**를 선택한 다음 **데이터 필드**서 `[City]`를 선택합니다.

18. **Finish**를 클릭합니다.  
  
    보고서에 지도 계층이 추가됩니다. 범례에 SellingArea 값에 따른 거품 크기가 표시됩니다.  
  
 19. 지도를 두 번 클릭하여 **지도 계층** 창을 표시합니다. **지도 계층** 창에 공간 데이터 원본 유형이 **DataRegion**인 새 계층 PointLayer1이 표시됩니다.  
  
19. 범례 제목을 추가합니다. 범례에서 **제목**텍스트를 선택하고 **표시 영역(평방피트)** 을 입력한 다음 Enter 키를 누릅니다.  
  
21. **지도 계층 창**에서 PointLayer1 옆의 화살표를 클릭한 다음 **점 속성**을 클릭합니다.  

    ![report-builder-map-point-properties](../reporting-services/media/report-builder-map-point-properties.png)
  
22. **글꼴** 탭에서 스타일을 **굵게** , 크기를 **10pt**로 지정합니다.

    ![report-builder-map-point-properties-font](../reporting-services/media/report-builder-map-point-properties-font.png)
  
23. **일반** 탭에서 **배치** 로 **아래쪽**을 선택합니다.

24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
24. **실행** 을 클릭하여 보고서를 미리 봅니다.  

    ![report-builder-map-city-names](../reporting-services/media/report-builder-map-city-names.png)
  
    지도에 뉴욕 주에 있는 상점의 위치가 표시됩니다. 각 상점의 표식 크기는 전시 영역에 따라 다릅니다. 이 자습서에는 다섯 개의 전시 구역 범위가 자동으로 계산되어 있습니다.


  
## <a name="LineLayer"></a>3. 지도 선 계층을 추가하여 경로 표시  
지도 계층 마법사를 사용하여 두 상점 간의 경로를 표시하는 지도 계층을 추가할 수 있습니다. 이 자습서에서는 세 개의 상점 위치를 연결하는 경로를 만듭니다. 비즈니스 애플리케이션에서 이 경로는 상점 간 최적 경로일 수 있습니다.  
  
### <a name="to-add-a-line-layer-to-map"></a>선 계층을 지도에 추가하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  지도를 두 번 클릭하여 **지도 계층** 창을 표시합니다. 도구 모음에서 **새 계층 마법사** 단추 ![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")를 클릭합니다.  
  
3.  **공간 데이터의 원본 선택** 페이지에서 **SQL Server 공간 쿼리** 를 선택하고 **다음**을 클릭합니다.  
  
4.  **SQL Server 공간 데이터가 있는 데이터 세트 선택** 페이지에서 **SQL Server 공간 데이터가 있는 새 데이터 세트 추가**를 클릭하고 **다음**을 클릭합니다.  
  
5.  **SQL Server 공간 데이터 원본에 대한 연결을 선택하십시오.** 에서 첫 번째 절차에서 사용한 데이터 원본을 선택합니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다. 쿼리 디자이너가 텍스트 기반 모드로 전환됩니다.  
  
8.  쿼리 창에서 다음 텍스트를 붙여 넣습니다.  
  
    ```  
    SELECT N'Path' AS Name, CAST('LINESTRING(  
       -76.5001866085881 42.4310489934743,  
       -76.4602850815536 43.4353224527794,  
       -73.4728622833178 44.7028831413324)' AS geography) as Route  
    ```  
  
9. **다음**을 클릭합니다.  
  
    지도에 세 개의 상점을 연결하는 경로가 표시됩니다.  
  
10. **공간 데이터 및 지도 보기 옵션 선택** 페이지에서 **공간 필드** 가 **Route** 이고 **계층 유형** 이 **선**인지 확인합니다. 다른 기본값을 적용합니다.  
  
    지도 보기에 뉴욕 주 북부에 있는 한 상점에서 뉴욕 주 남부에 있는 한 상점까지의 경로가 표시됩니다.  
  
11. **다음**을 클릭합니다.  
  
12. **지도 시각화 선택** 페이지에서 **기본 선 지도**를 클릭하고 **다음**을 클릭합니다.  
  
13. **색 테마 및 데이터 시각화 선택**에서 **단색 지도**옵션을 선택합니다. 경로가 선택한 테마에 따라 단색으로 표시됩니다.  
  
14. **Finish**를 클릭합니다.  

    ![report-builder-map-line](../reporting-services/media/report-builder-map-line.png)
  
     지도에 공간 데이터 원본 유형이 **DataRegion**인 새 선 계층이 표시됩니다. 이 예제에서 공간 데이터는 데이터 세트에서 제공되지만 분석 데이터가 선과 연결되어 있지 않습니다.  

## <a name="adjust-the-zoom"></a>확대/축소 조정
1. 뉴욕 주 전체를 볼 수 없는 경우 확대/축소를 조정할 수 있습니다. 맵을 선택한 상태로 속성 창에서 **MapViewport** 속성을 확인합니다. 

15. **보기** 섹션을 확장한 다음 **확대/축소** 속성을 볼 수 있도록 **보기** 를 확장합니다. **125**로 설정합니다. 

    ![report-builder-map-zoom](../reporting-services/media/report-builder-map-zoom.png)

      확대/축소 비율입니다. 125%에서는 전체 주가 표시됩니다.
  
## <a name="TileLayer"></a>4. Bing Maps 타일 배경 추가  
이 섹션에서는 Bing 지도 타일 배경을 표시하는 지도 계층을 추가합니다.  
  
1.  디자인 뷰로 전환합니다.  
  
2.  지도를 두 번 클릭하여 **지도 계층** 창을 표시합니다. 도구 모음에서 **계층 추가**![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer")를 클릭합니다.  
  
3.  드롭다운 목록에서 **타일 계층**을 클릭합니다.  
  
    **지도 계층** 창의 마지막 계층은 TileLayer1입니다. 기본적으로 타일 계층에는 도로 지도 스타일이 표시됩니다.  
  
    > [!NOTE]  
    > 마법사의 **공간 데이터 및 지도 보기 옵션 선택** 페이지에서 타일 계층을 추가할 수도 있습니다. 이렇게 하려면 **이 지도 보기에 대해 Bing 지도 배경 추가**를 선택합니다. 렌더링된 보고서의 타일 배경에 현재 지도 뷰포트 중심과 확대/축소 수준에 해당하는 Bing Maps 타일이 표시됩니다.  
  
4.  TileLayer1 옆의 화살표 > **타일 속성**을 클릭합니다.  
  
5.  **일반** 탭의 **유형**에서 **위성**을 선택합니다. 항공 보기에는 텍스트가 포함되지 않습니다.  

    ![report-builder-map-bing-aerial](../reporting-services/media/report-builder-map-bing-aerial.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Transparent"></a>5. 계층을 투명하게 만들기  
이 섹션에서는 한 계층의 항목이 다른 계층을 통과하여 표시되도록 원하는 효과를 얻을 때까지 계층의 순서와 투명도를 조정합니다. 만든 첫 번째 계층인 PolygonLayer1부터 시작합니다. 
  
1.  지도를 두 번 클릭하여 **지도 계층** 창을 표시합니다.  
  
3.  PolygonLayer1 옆의 화살표 > **계층 데이터**를 클릭합니다. **지도 다각형 계층 속성** 대화 상자가 열립니다.  
  
4.  **가시성** 탭의 **투명도(백분율)** 에서 **30**을 입력합니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     디자인 화면에 군이 반투명으로 표시됩니다.  

    ![report-builder-map-transparency](../reporting-services/media/report-builder-map-transparency.png)
  
## <a name="Vary"></a>6. 판매량을 기준으로 군 색 변경  
보고서 처리기가 지도 마법사의 마지막 페이지에서 선택한 테마에 따라 색상표에서 색 값을 자동으로 할당하기 때문에 다각형 계층에 있는 각 군의 색은 서로 다릅니다.  
  
다음 섹션에서는 특정 색을 각 군의 상점별 판매량 범위와 연결하는 색 규칙을 지정합니다. 빨강-노랑-녹색은 상대적인 높은-중간-낮은 판매량을 나타냅니다. 통화를 표시하도록 색 눈금의 형식을 지정합니다. 새 범례에서 연간 판매량 범위를 표시합니다. 상점이 없는 군의 경우 연결된 데이터가 없음을 표시하기 위해 색을 사용하지 않습니다.  
  
### <a name="Relationship"></a>6a. 공간 데이터와 분석 데이터 간의 관계 만들기  
분석 데이터에 따른 색으로 군 모양을 변경하려면 먼저 분석 데이터를 공간 데이터와 연결해야 합니다. 이 자습서에서는 일치시킬 군 이름을 사용합니다. 
  
1.  디자인 뷰로 전환합니다.  
  
2.  지도를 두 번 클릭하여 **지도 계층** 창을 표시합니다.  
  
3.  PolygonLayer1 옆의 화살표를 클릭하고 **계층 데이터**를 클릭합니다. **지도 다각형 계층 속성** 대화 상자가 열립니다.  
  
4.  **분석 데이터** 탭의 **분석 데이터 세트**에서 DataSet1을 선택합니다. 이 데이터 세트는 군에 대한 공간 데이터 쿼리를 만들 때 마법사에서 만들어진 것입니다.  
  
6.  **일치시킬 필드**에서 **추가**를 클릭합니다. 새 행이 추가됩니다.  
  
7.  **공간 데이터 세트 필드**에서 COUNTYNAME을 클릭합니다.  
  
8.  **분석 데이터 세트 필드**에서 [County]를 클릭합니다.  

    ![report-builder-map-county-colors](../reporting-services/media/report-builder-map-county-colors.png)
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. 보고서를 미리 봅니다.  

    ![report-builder-map-county-highlight](../reporting-services/media/report-builder-map-county-highlight.png)
  
공간 데이터 원본과 분석 데이터 세트에서 일치 필드를 지정하면 보고서 처리기가 지도 요소에 따라 분석 데이터를 그룹화할 수 있습니다. 데이터 바인딩된 지도 요소에는 지정한 값에 대한 성공적인 일치 항목이 있습니다.  
  
상점이 있는 각 군은 마법사에서 선택한 스타일의 색상표를 기반으로 하는 색으로 표시됩니다. 다른 군은 회색으로 표시됩니다.  
  
### <a name="ColorRules"></a>6b. 다각형에 대한 색 규칙 지정  
상점 판매량을 기반으로 각 군의 색을 변경하는 규칙을 만들려면 범위 값, 표시할 범위 내의 하위 범위 수 및 사용할 색을 지정해야 합니다.  
  
#### <a name="to-specify-color-rules-for-all-polygons-that-have-associated-data"></a>연결된 데이터가 있는 모든 다각형에 대한 색 규칙을 지정하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  PolygonLayer1 옆의 화살표를 클릭하고 **다각형 색 규칙**을 클릭합니다. **지도 색 규칙 속성** 대화 상자가 열립니다. 색 규칙 옵션 **색상표를 사용하여 데이터 시각화** 가 선택되어 있습니다. 이 옵션은 마법사에서 설정된 것입니다.  
  
3.  **색 범위를 사용하여 데이터 시각화**를 선택합니다. 색상표 옵션이 시작 색, 중간 색 및 마지막 색 옵션으로 바뀝니다.  
  
4.  군별 판매량에 대한 범위 값을 정의합니다. **데이터 필드**의 드롭다운 목록에서 `[Sum(Sales)]`을 선택합니다.  
  
5.  통화가 천 단위로 표시되도록 형식을 변경하려면 식을 다음과 같이 변경합니다. `=Sum(Fields!Sales.Value)/1000`  
  
6.  **시작 색** 을 **빨강**으로 변경합니다.  
  
7.  **마지막 색** 을 **녹색**으로 변경합니다.  
  
    **빨강** 은 낮은 판매량 값을 나타내고, **노랑** 은 중간 판매량 값을 나타내며, **녹색** 은 높은 판매량 값을 나타냅니다. 보고서 처리기는 이러한 값과 **분포** 페이지에서 선택한 옵션에 따라 색의 범위를 계산합니다.  
    
    ![report-builder-map-county-color-rules](../reporting-services/media/report-builder-map-county-color-rules.png)
  
8.  **분포**를 클릭합니다.  
  
9. 분포 유형이 **최적**인지 확인합니다. 5단계에 있는 식의 경우 최적 분포는 각 범위에 있는 항목 수와 각 범위 간격의 균형을 맞추는 하위 범위로 값을 나눕니다.  
  
10. 이 페이지에 있는 다른 옵션에 기본값을 적용합니다. 최적 배포 유형을 선택하는 경우 보고서가 실행될 때 하위 범위의 수가 계산됩니다.  
  
11. **범례**를 클릭합니다.  
  
12. **색 눈금 옵션**에서 **색 눈금에 표시** 가 선택되어 있는지 확인합니다.  
  
13. **이 범례에 표시**의 드롭다운 목록에서 빈 줄을 선택합니다. 이제부터 색 눈금에서만 색 범위가 표시됩니다.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

15. 보고서를 미리 봅니다.

    ![report-builder-map-county-color-rule-preview](../reporting-services/media/report-builder-map-county-color-rule-preview.png)
  
    색 눈금에 빨강, 주황, 노랑 및 녹색의 네 가지 색이 표시됩니다. 각 색은 군별 판매량에 따라 자동으로 계산되는 판매량 범위를 나타냅니다.  
  
### <a name="ColorScale"></a>6c. 색 눈금의 데이터 형식을 통화로 지정  
기본적으로 데이터는 일반 형식을 사용하지만 이 섹션에서는 사용자 지정 형식을 적용합니다.  
  
1. 디자인 뷰로 전환합니다.  

2. 색 눈금을 선택합니다. **홈** 탭 > **숫자** 섹션에서 **통화**를 클릭합니다.  
  
4.  **숫자** 섹션에서 **소수 자릿수 줄이기** 단추를 두 번 클릭합니다.  
  
    색 눈금에 각 범위에 대한 통화 형식으로 연간 판매량이 표시됩니다.  
  
### <a name="NewLegend"></a>6d. 범례 제목 추가   
  
1.  색 눈금을 선택한 상태로 속성 창에서 **MapColorScale**속성을 확인합니다. 
  
2. 제목 섹션을 확장하고 Caption 속성에 **Sales (Thousands)** 를 입력합니다.

3. TextColor 속성을 **흰색**으로 변경합니다.  

    ![report-builder-map-color-scale-title](../reporting-services/media/report-builder-map-color-scale-title.png)
  
8.  보고서를 미리 봅니다.  
  
연결된 상점과 판매량이 있는 군은 색 규칙에 따라 표시되고 판매량이 없는 군은 무색으로 표시됩니다.  
  
### <a name="NoData"></a>6f. 데이터가 없는 군의 색 변경  
계층에 있는 모든 지도 요소의 기본 표시 옵션을 설정할 수 있습니다. 색 규칙은 이러한 표시 옵션보다 우선합니다.  
  
#### <a name="to-set-the-display-properties-for-all-elements-on-a-layer"></a>계층의 모든 요소에 대한 표시 속성을 설정하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  지도를 두 번 클릭하여 **지도 계층** 창을 표시합니다.  
  
3.  PolygonLayer1에서 아래쪽 화살표를 클릭한 다음 **다각형 속성**을 클릭합니다. 

     ![report-builder-map-polygon-layer-properties](../reporting-services/media/report-builder-map-polygon-layer-properties.png)

     **지도 다각형 속성** 대화 상자가 열립니다. 규칙 기반 표시 옵션이 적용되기 전에 이 대화 상자의 표시 옵션 집합이 계층에 있는 모든 다각형에 적용됩니다.  
  
4.  **채우기** 탭에서 채우기 스타일이 **단색**인지 확인합니다. 인지 확인합니다. 그라데이션과 패턴이 모든 색에 적용됩니다.  
  
6.  **색**에서 **연한 강철색**을 선택합니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  보고서를 미리 봅니다.  
  
연결된 데이터가 없는 군은 회색-파란색으로 표시됩니다. 연결된 분석 데이터가 있는 군만 지정한 색 규칙에 따라 **빨강** ~ **녹색** 으로 표시됩니다.  
  
## <a name="CustomPoint"></a>7. 사용자 지정 점 추가  
아직 건설되지 않은 새 상점을 나타내기 위해 이 섹션에서는 **별 모양** 표식 유형으로 점을 지정합니다.  
  
1.  디자인 뷰로 전환합니다.  
  
2.  지도를 두 번 클릭하여 **지도 계층** 창을 표시합니다. 도구 모음에서 **계층 추가** ![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer")를 클릭한 다음, **점 계층**을 클릭합니다.  
  
    새 점 계층이 지도에 추가됩니다. 기본적으로 점 계층의 공간 데이터 형식은 **포함**입니다.  
  
3.  PointLayer2의 화살표 > **점 추가**를 클릭합니다.  
  
4.  지도 뷰포트로 포인터를 이동합니다. 커서는 십자 기호로 변경됩니다.  
  
5.  점을 추가할 지도의 위치를 클릭합니다. 이 자습서에서는 Oneida 군의 위치를 클릭합니다. 원으로 표시된 점이 계층의 클릭한 지점에 추가됩니다. 기본적으로 점이 선택됩니다.  

    ![report-builder-map-custom-point](../reporting-services/media/report-builder-map-custom-point.png)
  
6.  추가한 점을 마우스 오른쪽 단추로 클릭하고 **포함 점 속성**을 클릭합니다.  
  
7.  **이 계층의 점 옵션 무시**를 선택합니다. 추가 페이지가 대화 상자에 나타납니다. 여기서 설정한 값은 계층 또는 색 규칙에 대한 표시 옵션보다 우선합니다.  

    ![report-builder-map-custom-point-general](../reporting-services/media/report-builder-map-custom-point-general.png)
  
8.  **표식** 탭에서 **표식 유형**으로 **별 모양**을 선택합니다.  

10. **표식 크기** 를 **18pt**로 변경합니다.
  
3.  **레이블** 탭의 **레이블 텍스트**에 **New Store**를 입력합니다.  
  
5.  **배치**에서 **위쪽**을 클릭합니다.  

13. **글꼴** 탭에서 글꼴 크기를 **10pt** , 스타일을 **굵게**로 지정합니다.

    ![report-builder-map-custom-point-font](../reporting-services/media/report-builder-map-custom-point-font.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  보고서를 미리 봅니다.  
  
레이블이 상점 위치 위에 나타납니다.  

![report-builder-map-custom-point-new-store](../reporting-services/media/report-builder-map-custom-point-new-store.png)
  
## <a name="CenterView"></a>8. 지도 중심 및 크기 조정   
이 섹션에서는 지도 중심을 변경하고 방법과 확대/축소 수준을 변경하는 또 다른 방법을 알아봅니다.  
 
1.  디자인 뷰로 전환합니다.  

1.  지도를 선택하고 마우스 오른쪽 단추를 클릭한 다음 **뷰포트 속성**을 클릭합니다.  
  
2.  **중심 및 확대/축소** 탭에서 **보기 중심 및 확대/축소 수준 설정** 선택되어 있는지 확인합니다.  

4. **확대/축소 수준(백분율)** 을 **125**로 설정합니다.
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  지도를 클릭한 다음 끌어 중심을 원하는 위치로 변경합니다.  
  
6.  마우스 휠을 사용하여 확대/축소 수준을 변경할 수도 있습니다.  
  
7.  보고서를 미리 봅니다.  
  
디자인 뷰의 화면과 보기에 지도가 예제 데이터를 기반으로 표시됩니다. 렌더링된 보고서에서는 지도 보기가 지정한 보기의 가운데에 표시됩니다.  
  
## <a name="Title"></a>9. 보고서 제목 추가  
  
1.  디자인 뷰로 전환합니다.
  
1.  디자인 화면에서 **제목을 추가하려면 클릭하십시오.** 를 클릭합니다.  
  
2.  **Sales in New York Stores** 를 입력한 다음 입력란 바깥쪽을 클릭합니다.  
  
이 제목은 보고서 맨 위에 나타납니다. 페이지 머리글이 정의되지 않았을 때 보고서 본문의 맨 위에 있는 항목은 보고서 머리글에 해당합니다.  
  
## <a name="Save"></a>10. 보고서 저장  
  
1.  디자인 뷰 또는 미리 보기에서 **파일** 메뉴 > **다른 이름으로 저장**을 선택합니다.
 
3.  **이름**에 **Store Sales in New York**을 입력합니다.  

3. 로컬 컴퓨터 또는 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 서버에 저장합니다.
  
4. **저장**을 클릭합니다. 

보고서 서버에 저장하는 경우 서버에서 볼 수 있습니다.

![report-builder-map-in-portal](../reporting-services/media/report-builder-map-in-portal.png) 
  
## <a name="next-steps"></a>다음 단계  
보고서에 지도를 추가하는 방법에 대한 연습을 완료했습니다.  
  
자세한 내용은 [지도&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/maps-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[보고서 작성기 자습서](../reporting-services/report-builder-tutorials.md)  
[SQL Server의 보고서 작성기](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
[지도 마법사 및 지도 계층 마법사&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
[규칙 및 분석 데이터를 사용하여 다각형, 선 및 점 표시 변경&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  

