---
title: SQL Server Reporting Services의 트리 맵 및 선버스트 차트 | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: a15a57904b539381bbf65cb259c74d9365840359
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "64568538"
---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>Reporting Services의 트리 맵 및 선버스트 차트 

SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 트리 맵 및 선버스트 시각화를 사용하면 계층 데이터를 시각적으로 잘 표현할 수 있습니다. 이 문서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서에 트리 맵 또는 선버스트 차트를 추가하는 방법에 대한 개요입니다. 문서에는 시작할 수 있도록 AdventureWorks 샘플 쿼리가 포함되어 있습니다.  
  
##  <a name="bkmk_treemap_chart"></a> 트리 맵 차트  

트리 맵 차트는 차트 영역을 데이터 계층의 서로 다른 수준과 상대적 크기를 나타내는 사각형으로 분할합니다. 이 맵은 트렁크로 시작하여 점점 더 작은 분기로 분할하는 트리의 분기와 유사합니다. 각 사각형은 계층의 다음 수준을 나타내는 더 작은 사각형으로 구분됩니다. 최상위 수준 트리 맵 사각형은 차트의 왼쪽 위에 가장 큰 사각형이 있고 가장 작은 사각형이 오른쪽 아래에 있도록 정렬됩니다.  사각형 내에서 더 높은 수준의 다음 수준도 사각형이 왼쪽 위에서 오른쪽 아래로 있도록 정렬됩니다.  

예를 들어 샘플 트리 맵의 다음 이미지에서는 남서쪽 지역이 가장 크고 독일이 가장 작습니다. 남서쪽 내에서 로드 바이크는 마운틴 바이크보다 더 큽니다.  

![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>트리 맵 차트를 삽입하고 샘플 AdventureWorks 데이터를 설정하려면  

> [!NOTE]
> 보고서에 차트를 추가하기 전에 데이터 원본 및 데이터 세트를 만듭니다.  샘플 데이터 및 샘플 쿼리는 [샘플 AdventureWorks 데이터](#bkmk_sample_data)를 참조하세요.  
  
1. 디자인 화면을 마우스 오른쪽 단추로 클릭한 다음 **삽입** > **차트**를 선택합니다. **트리 맵** 아이콘을 선택합니다.

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  

2. 차트의 위치 및 크기를 변경합니다. 샘플 데이터와 함께 사용하려면 너비가 5인치인 차트로 시작하는 것이 좋습니다.  
  
3. 샘플 데이터의 다음 필드를 추가합니다.  
  
    * **값:** LineTotal
    * **범주 그룹**(다음 순서로):
        1. CategoryName
        2. SubcategoryName
    * **계열 그룹:** TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4. 페이지 크기를 트리 맵의 일반적인 모양에 대해 최적화하려면 범례 위치를 아래쪽으로 설정합니다.  
  
5. 하위 범주 및 라인 합계를 표시하는 도구 설명을 추가하려면 **LineTotal** 을 마우스 오른쪽 단추로 클릭한 다음 **계열 속성**을 선택합니다.  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     **도구 설명** 속성을 다음 값으로 설정합니다.  
  
    ```
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    자세한 내용은 [계열에 도구 설명 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)를 참조하세요.  
  
6. 기본 차트 제목을 **지역별로 분류한 판매**로 변경합니다.  
  
7. 표시되는 레이블 값 수는 글꼴 크기, 전체 차트 영역의 크기 및 특정 사각형 크기에 의해 영향을 받습니다. 더 많은 레이블을 보려면 **LineTotal**의 **Label Font** 속성을 기본값 **8pt**가 아닌 **10pt**로 변경합니다.  

##  <a name="bkmk_sunburst_chart"></a> 선버스트 차트  

선버스트 차트에서 계층은 일련의 원으로 표시됩니다. 가장 높은 수준의 계층은 가운데에 위치하며 낮은 수준의 계층은 그 외부에 표시된 링입니다.  계층의 최하위 수준이 외부 링입니다.  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>선버스트 차트를 삽입하고 샘플 AdventureWorks 데이터를 설정하려면

> [!NOTE]
> 보고서에 차트를 추가하기 전에 데이터 원본 및 데이터 세트를 만듭니다. 샘플 데이터 및 샘플 쿼리는 [샘플 AdventureWorks 데이터](#bkmk_sample_data)를 참조하세요.  
  
1. 디자인 화면을 마우스 오른쪽 단추로 클릭한 다음 **삽입** > **차트**를 선택합니다. **선버스트** 아이콘을 선택합니다.

     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2. 차트의 위치 및 크기를 변경합니다. 샘플 데이터와 함께 사용하려면 너비가 5인치인 차트로 시작하는 것이 좋습니다.  
  
3. 샘플 데이터의 다음 필드를 추가합니다.  

    * **값:** LineTotal
    * **범주 그룹**(다음 순서로):
        1. CategoryName
        2. SubcategoryName
        3. SalesReasonName
    * **계열 그룹:** TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4. 페이지 크기를 선버스트 차트의 일반적인 모양에 대해 최적화하려면 범례 위치를 아래쪽으로 설정합니다.  
  
5. 기본 차트 제목을 **지역별로 분류한 판매, 판매 이유 포함**으로 변경합니다.  
  
6. 범주 그룹의 값을 선버스트에 레이블로 추가하려면 레이블 속성 **Visible=true** 및 **UseValueAsLabel=false**를 설정합니다.<br /><br /> 표시되는 레이블 값은 글꼴 크기, 전체 차트 영역의 크기 및 특정 사각형 크기에 의해 영향을 받습니다.  더 많은 레이블을 보려면 **LineTotal**의 **Label Font** 속성을 기본값 **8pt**가 아닌 **10pt**로 변경합니다.

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7. 다른 색 범위를 원하는 경우 차트 **색상표** 속성을 변경합니다.  

     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  

##  <a name="bkmk_sample_data"></a> 샘플 AdventureWorks 데이터

이 섹션은 데이터 원본 및 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]의 데이터 세트를 만들기 위한 샘플 쿼리 및 기본 단계를 포함하고 있습니다. 보고서가 이미 데이터 원본 및 데이터 세트를 포함하고 있는 경우 이 섹션을 건너뛸 수 있습니다.  
  
쿼리는 AdventureWorks 판매 주문 세부 정보 데이터를 판매 지역, 제품 범주, 제품 하위 범주 및 판매 이유 데이터와 함께 반환합니다.  
  
1. **데이터 가져오기**  
  
     이 섹션의 쿼리는 GitHub [AdventureWorks 2016 전체 데이터베이스 백업](https://github.com/Microsoft/sql-server-samples/releases)에서 다운로드할 수 있는 AdventureWorks 데이터베이스를 기반으로 합니다.  

2. **데이터 원본 만들기**  
  
    1. **보고서 데이터**에서 **데이터 원본**을 마우스 오른쪽 단추로 클릭하고 **데이터 원본 추가**를 선택합니다.  
  
    2. **내 보고서에 포함된 연결 사용**을 선택합니다.  
  
    3. 연결 형식으로 **Microsoft SQL Server**를 선택합니다.  
  
    4. 서버 및 데이터베이스에 연결 문자열을 입력합니다. 예를 들어  
  
        ```
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5. 데이터베이스에 대한 연결을 확인하려면 **연결 테스트** 단추를 선택한 다음 **확인**을 선택합니다.  
  
     데이터 원본을 만드는 방법에 대한 자세한 내용은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)를 참조하세요.  
  
3. **데이터 세트를 만듭니다**.  
  
    1. **보고서 데이터**에서 **데이터 세트**를 마우스 오른쪽 단추로 클릭한 다음, **데이터 세트 추가**를 선택합니다.  
  
    2. **내 보고서에 포함된 데이터 세트 사용**을 선택합니다.  
  
    3. 만든 데이터 원본을 선택합니다.  
  
    4. **텍스트** 쿼리 형식을 선택하고 다음과 같은 쿼리를 복사하여 **쿼리** 텍스트 상자에 붙여넣습니다.  
  
        ```sql
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
  
    5. **확인**을 선택합니다.  
  
     데이터 세트를 만드는 방법에 대한 자세한 내용은 [공유 데이터 세트 또는 포함된 데이터 세트 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:

* [공유 데이터 세트 디자인 뷰&#40;보고서 작성기&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)

* [계열에 도구 설명 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)

* [자습서: Power BI의 트리 맵](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)

* [트리 맵: Microsoft Research Data Visualization Apps for Office](https://research.microsoft.com/projects/msrdatavis/treemap.aspx)