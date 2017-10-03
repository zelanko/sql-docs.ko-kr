---
title: "Reporting Services의 트리 맵 및 선버스트 차트 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/31/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12307c8f-bca7-4d21-8ad5-0c07d819865b
caps.latest.revision: 17
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 7811cfe9238c92746673fac4fce40a4af44d6dcd
ms.openlocfilehash: b9f7ca16589b2383eaed959c6556f0b2b6c4cf74
ms.contentlocale: ko-kr
ms.lasthandoff: 10/02/2017

---
# <a name="tree-map-and-sunburst-charts-in-reporting-services"></a>Reporting Services의 트리 맵 및 선버스트 차트
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 트리 맵 및 선버스트 시각화를 사용하면 계층 데이터를 시각적으로 잘 표현할 수 있습니다.   이 항목에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서에 트리 맵 또는 선버스트 차트를 추가하는 방법에 대한 개요입니다. 또한 이 항목은 시작하는 데 도움이 되는 샘플 Adventureworks 쿼리를 포함하고 있습니다.  
  
##  <a name="bkmk_treemap_chart"></a> 트리 맵 차트  
 ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
  
 트리 맵 차트는 차트 영역을 데이터 계층의 서로 다른 수준과 상대적 크기를 나타내는 사각형으로 분할합니다. 이 맵은 트렁크로 시작하여 점점 더 작은 분기로 분할하는 트리의 분기와 유사합니다. 각 사각형은 계층의 다음 수준을 나타내는 더 작은 사각형으로 구분됩니다. 최상위 수준 트리 맵 사각형은 차트의 왼쪽 위에 가장 큰 사각형이 있고 가장 작은 사각형이 오른쪽 아래에 있도록 정렬됩니다.  사각형 내에서 더 높은 수준의 다음 수준도 사각형이 왼쪽 위에서 오른쪽 아래로 있도록 정렬됩니다.  
  
 예를 들어 샘플 트리 맵의 다음 이미지에서는 남서쪽 지역이 가장 큰 및 독일이 가장 작습니다. 남서쪽 내에서 로드 바이크는 마운틴 바이크보다 더 큽니다.  
  
 ![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-tree-map-chart-and-configure-for-the-sample-adventureworks-data"></a>트리 맵 차트를 삽입하고 샘플 Adventureworks 데이터에 대해 구성하려면  
   
[!NOTE] 보고서에 차트를 추가 하기 전에 데이터 원본 및 데이터 집합을 만듭니다.  샘플 데이터 및 샘플 쿼리는 이 항목의 [샘플 Adventureworks 데이터](#bkmk_sample_data) 섹션을 참조하세요.  
  
1.  디자인 화면을 마우스 오른쪽 단추로 클릭하고 **삽입**, **차트** 를 차례로 클릭합니다.  
  
     트리 맵 ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")을 선택합니다.  
  
     ![ssrs_insert_treemap_sunburst](../../reporting-services/report-design/media/ssrs-insert-treemap-sunburst.png "ssrs_insert_treemap_sunburst")  
  
2.  차트의 위치 및 크기를 변경합니다.   샘플 데이터와 함께 사용하려는 경우 너비가 5인치인 차트로 시작하는 것이 좋습니다.  
  
3.  샘플 데이터의 다음 필드를 추가합니다.  
  
    |||  
    |-|-|  
    |![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")|**값:** LineTotal<br /><br /> **범주 그룹:** 다음 순서로 추가합니다.<br /><br /> 1) CategoryName<br /><br /> 2) SubcategoryName<br /><br /> **계열 그룹:** TerritoryName|  
  
4.  페이지 크기를 트리 맵의 일반적인 모양에 대해 최적화하려면 범례 위치를 아래쪽으로 설정합니다.  
  
5.  하위 범주 및 라인 합계를 표시하는 도구 설명을 추가하려면 **LineTotal** 을 마우스 오른쪽 단추로 클릭한 다음 **계열 속성**을 클릭합니다.  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     **도구 설명** 속성을 다음으로 설정합니다.  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
     자세한 내용은 [계열에 도구 설명 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)를 차례로 클릭합니다.  
  
6.  기본 차트 제목을 "지역별로 분류한 판매"로 변경합니다.  
  
7.  표시되는 레이블 값 수는 글꼴 크기, 전체 차트 영역의 크기 및 특정 사각형 크기에 의해 영향을 받습니다.  더 많은 레이블을 보려면 LineTotal의 레이블 글꼴 속성을 기본값 8pt 대신 10pt로 변경합니다.  
  
  
##  <a name="bkmk_sunburst_chart"></a> 선버스트 차트  
 ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
 선버스트 차트에서 계층은 계층의 최상위 수준이 가운데에 있고 계층의 더 낮은 수준이 이 가운데의 외부에 링으로 표시되는 일련의 원으로 표시됩니다.  계층의 최하위 수준이 외부 링입니다.  
  
 ![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-configure-for-the-sample-adventureworks-data"></a>선버스트 차트를 삽입하고 샘플 Adventureworks 데이터에 대해 구성하려면  
 [!NOTE] 보고서에 차트를 추가 하기 전에 데이터 원본 및 데이터 집합을 만듭니다.  샘플 데이터 및 샘플 쿼리는 이 항목의 [샘플 Adventureworks 데이터](#bkmk_sample_data) 섹션을 참조하세요.  
  
1.  디자인 화면을 마우스 오른쪽 단추로 클릭하고 **삽입**, **차트** 를 차례로 클릭합니다.  
  
     선버스트 ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")을 선택합니다.  
  
     ![ssrs_insert_treemap_sunburst](../../reporting-services/report-design/media/ssrs-insert-treemap-sunburst.png "ssrs_insert_treemap_sunburst")  
  
2.  차트의 위치 및 크기를 변경합니다.   샘플 데이터와 함께 사용하려는 경우 너비가 5인치인 차트로 시작하는 것이 좋습니다.  
  
3.  샘플 데이터의 다음 필드를 추가합니다.  
  
    |||  
    |-|-|  
    |![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")|**값:** LineTotal<br /><br /> **범주 그룹:** 다음 순서로 추가합니다.<br /><br /> 1) CategoryName<br /><br /> 2) SubcategoryName,<br /><br /> 3) SalesReasonName<br /><br /> **계열 그룹:** TerritoryName.|  
  
4.  페이지 크기를 선버스트의 일반적인 모양에 대해 최적화하려면 범례 위치를 아래쪽으로 설정합니다.  
  
5.  기본 차트 제목을 "지역별로 분류한 판매, 판매 이유 포함"으로 변경합니다.  
  
6.
    |||  
    |-|-|  
    |![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")|범주 그룹의 값을 선버스트에 레이블로 추가하려면 레이블 속성 **Visible** =true 및 **UseValueAsLabel**=False를 설정합니다.<br /><br /> 표시되는 레이블 값은 글꼴 크기, 전체 차트 영역의 크기 및 특정 사각형 크기에 의해 영향을 받습니다.  레이블을 더 자세히 보려면 LineTotal의 레이블 글꼴 속성을 기본값 10pt 대신 8pt로 변경합니다.|
  
7.  다른 색 범위를 원하는 경우 차트 **색상표** 속성을 변경합니다.  
  
  
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a> 샘플 Adventureworks 데이터  
 이 섹션은 데이터 원본 및 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]의 데이터 집합을 만들기 위한 샘플 쿼리 및 기본 단계를 포함하고 있습니다. 보고서가 이미 데이터 원본 및 데이터 집합을 포함하고 있는 경우 이 섹션을 건너뛸 수 있습니다.  
  
 쿼리는 Adventureworks 판매 주문 세부 정보 데이터를 판매 지역, 제품 범주, 제품 하위 범주 및 판매 이유 데이터와 함께 반환합니다.  
  
1.  **데이터 가져오기:**  
  
     이 섹션의 쿼리는  [Adventure Works 2014 전체 데이터베이스 백업](https://msftdbprodsamples.codeplex.com/releases/view/125550)에서 다운로드할 수 있는 Adventureworks 데이터베이스를 기반으로 합니다.  
  
     데이터베이스를 설치하는 방법에 대 한 자세한 내용은 [How to install Adventure Works 2014 Sample Databases.pdf](https://msftdbprodsamples.codeplex.com/releases/view/125550)를 참조하세요.  
  
2.  **데이터 원본 만들기:**  
  
    1.  **보고서 데이터** 창에서 **데이터 원본** 을 마우스 오른쪽 단추로 클릭하고 **데이터 원본 추가**를 클릭합니다.  
  
    2.  **내 보고서에 포함된 연결 사용**을 선택합니다.  
  
    3.  연결 형식 **Microsoft SQL Server**를 선택합니다.  
  
    4.  다음 예와 같이 서버 및 데이터베이스에 대한 연결 문자열을 입력합니다.  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2014  
        ```  
  
    5.  **시험 연결** 버튼을 사용하여 확인한 다음 **확인**을 클릭하는 것이 좋습니다.  
  
     데이터 원본을 만드는 방법에 대한 자세한 내용은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)을 참조하세요.  
  
3.  **데이터 집합 만들기:**  
  
    -   **보고서 데이터** 창에서 **데이터 집합** 을 마우스 오른쪽 단추로 클릭하고 **데이터 집합 추가**를 클릭합니다.  
  
    -   **내 보고서에 포함된 데이터 집합 사용**을 선택합니다.  
  
    -   이전 단계에서 만든 데이터 원본을 선택합니다.  
  
    -   **텍스트** 쿼리 유형을 선택하고 다음과 같은 쿼리를 복사하여 **쿼리:** 텍스트 상자에 붙여넣습니다.  
  
        ```  
        SELECT    Sales.SalesOrderHeader.SalesOrderID, Sales.SalesOrderHeader.OrderDate, Sales.SalesOrderDetail.SalesOrderDetailID, Sales.SalesOrderDetail.ProductID, Sales.SalesOrderDetail.LineTotal,   
                                 Sales.SalesOrderDetail.UnitPrice, Sales.SalesOrderDetail.OrderQty, Production.Product.Name, Production.Product.ProductNumber, Sales.SalesTerritory.TerritoryID, lower(Sales.SalesTerritory.Name) AS TerritoryName,   
                                 Production.ProductSubcategory.Name AS SubcategoryName, Production.ProductCategory.Name AS CategoryName, Sales.SalesReason.SalesReasonID, Sales.SalesReason.Name AS SalesReasonName  
        FROM            Sales.SalesOrderDetail INNER JOIN  
                                 Sales.SalesOrderHeader ON Sales.SalesOrderDetail.SalesOrderID = Sales.SalesOrderHeader.SalesOrderID INNER JOIN  
                                 Production.Product ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID INNER JOIN  
                                 Sales.SalesTerritory ON Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND   
                                 Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID INNER JOIN  
                                 Production.ProductSubcategory ON Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID INNER JOIN  
                                 Production.ProductCategory ON Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID INNER JOIN  
                                 Sales.SalesOrderHeaderSalesReason ON Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID INNER JOIN  
                                 Sales.SalesReason ON Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID  
        ```  
  
    -   **확인**을 클릭합니다.  
  
     데이터 집합을 만드는 방법에 대한 자세한 내용은 [공유 데이터 집합 또는 포함된 데이터 집합 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)를 참조하세요.  
  
  
## <a name="see-also"></a>관련 항목:  
 [공유 데이터 집합 디자인 뷰&#40;보고서 작성기&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
 [계열에 도구 설명 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)   
 [자습서: Power BI의 트리 맵](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)   
 [트리 맵: Microsoft Research Data Visualization Apps for Office](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]


