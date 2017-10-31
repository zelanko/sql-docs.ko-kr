---
title: "SQL Server Reporting Services의 트리 맵 및 선 버스트 차트 | Microsoft Docs"
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 5e15fa8674a09821becd437e78cfb0bb472e3bc8
ms.openlocfilehash: 50224e926c08951887a6423ab1c95eb7ac23a944
ms.contentlocale: ko-kr
ms.lasthandoff: 10/30/2017

---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>Reporting Services의 트리 맵 및 선 버스트 차트
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 트리 맵 및 선 버스트 시각화는 계층적 데이터를 시각적으로 잘 표현할 적합 합니다. 이 문서는 트리 맵 또는 선 버스트 차트를 추가 하는 방법의 개요는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서입니다. 문서에는 AdventureWorks 예제 쿼리를 사용 하 여 시작할 수 있도록를 포함 되어 있습니다.  
  
##  <a name="bkmk_treemap_chart"></a>트리 맵 차트  

트리 맵 차트는 서로 다른 수준과 상대적 크기를 데이터 계층 구조를 나타내는 사각형으로 차트 영역을 분할 합니다. 이 맵은 트렁크로 시작하여 점점 더 작은 분기로 분할하는 트리의 분기와 유사합니다. 각 사각형은 계층의 다음 수준을 나타내는 더 작은 사각형으로 구분 됩니다. 최상위 수준 트리 맵 사각형은 가장 작은 사각형이 오른쪽 아래 모서리에 차트의 왼쪽된 위 모서리에서 가장 큰 사각형이 정렬 됩니다.  사각형 내에서 더 높은 수준의 다음 수준도 사각형이 왼쪽 위에서 오른쪽 아래로 있도록 정렬됩니다.  

예를 들어 샘플 트리 맵의 다음 이미지에서는 남서쪽 지역이 가장 큰 및 독일이 가장 작습니다. 남서쪽 내에서 로드 바이크는 마운틴 바이크보다 더 큽니다.  
 
![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>트리 맵 차트를 삽입 하 고 샘플 AdventureWorks 데이터를 설정 하려면  
   
> [!NOTE]
> 보고서에 차트를 추가 하기 전에 데이터 원본 및 데이터 집합을 만듭니다.  예제 데이터 및 쿼리 예제에 대 한 참조 [샘플 AdventureWorks 데이터](#bkmk_sample_data)합니다.  
  
1.  디자인 화면을 마우스 오른쪽 단추로 클릭 한 다음 선택 **삽입** > **차트**합니다. 선택 된 **Treemap** 아이콘입니다.

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
   
2.  차트의 위치 및 크기를 변경합니다. 샘플 데이터를 사용 하려면 너비가 5 인치인 차트로 좋은 시작 됩니다.  
  
3.  샘플 데이터의 다음 필드를 추가합니다.  
  
    * **값**: LineTotal
    * **범주 그룹** (다음과 같은 순서로):
        1. CategoryName
        2. SubcategoryName
    * **계열 그룹**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  트리 맵의 일반적인 모양에 대 한 페이지 크기를 최적화 하려면 범례 위치를 아래쪽으로 설정 합니다.  
  
5.  하위 범주 및 라인 합계를 표시 하는 도구 설명에 추가 하려면 마우스 오른쪽 단추로 클릭 **LineTotal**를 선택한 후 **계열 속성**합니다.  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     설정의 **도구 설명** 속성을 다음 값:  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    자세한 내용은 참조 [일련 &#40;에 도구 설명 표시 보고서 작성기 및 SSRS &#41; ](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
6.  기본 차트 제목을 변경 **지역별로 분류 한 판매**합니다.  
  
7.  표시되는 레이블 값 수는 글꼴 크기, 전체 차트 영역의 크기 및 특정 사각형 크기에 의해 영향을 받습니다. 더 많은 레이블을 보려면, 변경의 **레이블 글꼴** 속성 **LineTotal** 를 **10pt** 의 기본값과 **8pt**합니다.  
  
  
##  <a name="bkmk_sunburst_chart"></a>선 버스트 차트  
 
선 버스트 차트에서에서 계층은 일련의 원으로 표시 됩니다. 센터에서 계층의 가장 높은 수준입니다 되며 더 낮은 수준의 계층 구조 가운데 외부에 표시 되는 링.  계층의 최하위 수준이 외부 링입니다.  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>선 버스트 차트를 삽입 하 고 샘플 AdventureWorks 데이터를 설정 하려면  
> [!NOTE] 
> 보고서에 차트를 추가 하기 전에 데이터 원본 및 데이터 집합을 만듭니다. 예제 데이터 및 쿼리 예제에 대 한 참조 [샘플 AdventureWorks 데이터](#bkmk_sample_data)합니다.  
  
1.  디자인 화면을 마우스 오른쪽 단추로 클릭 한 다음 선택 **삽입** > **차트**합니다. 선택 된 **선 버스트** 아이콘입니다.
     
     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2.  차트의 위치 및 크기를 변경합니다. 샘플 데이터를 사용 하려면 너비가 5 인치인 차트로 좋은 시작 됩니다.  
  
3.  샘플 데이터의 다음 필드를 추가합니다.  

    * **값**: LineTotal
    * **범주 그룹** (다음과 같은 순서로):
        1. CategoryName
        2. SubcategoryName
        3. S a l
    * **계열 그룹**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  선 버스트 차트의 일반적인 모양에 대 한 페이지 크기를 최적화 하려면 범례 위치를 아래쪽으로 설정 합니다.  
  
5.  기본 차트 제목을 변경 **판매 지역별 판매 이유 포함 분류**합니다.  
  
6. 범주 그룹 값 선 버스트에 레이블로 추가 하려면 레이블 속성을 설정 **Visible = true** 및 **UseValueAsLabel = false**합니다.<br /><br /> 표시되는 레이블 값은 글꼴 크기, 전체 차트 영역의 크기 및 특정 사각형 크기에 의해 영향을 받습니다.  더 많은 레이블을 보려면, 변경의 **레이블 글꼴** 속성 **LineTotal** 를 **10pt** 의 기본값과 **8pt**합니다.

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7.  다른 색 범위를 원하는 경우 차트 **색상표** 속성을 변경합니다.  
    
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a>샘플 AdventureWorks 데이터  
 이 섹션에서는 데이터 원본 및 데이터 집합을 만들기 위한 기본 단계 및 예제 쿼리 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]합니다. 보고서 데이터 원본 및 데이터 집합에 이미 포함 된, 경우에이 섹션을 건너뛸 수 있습니다.  
  
 쿼리는 영업 지역, 제품 범주, 제품 하위 범주 및 판매 이유 데이터와 AdventureWorks 판매 주문 세부 정보 데이터를 반환합니다.  
  
1.  **데이터를 가져올**합니다.  
  
     이 섹션의 쿼리는 GitHub에서 다운로드할 수 있는 AdventureWorks 데이터베이스를 기반: [AdventureWorks 2016 전체 데이터베이스 백업을](https://github.com/Microsoft/sql-server-samples/releases)합니다.  
  
  
2.  **데이터 원본 만들기**합니다.  
  
    1.  아래 **보고서 데이터**를 마우스 오른쪽 단추로 클릭 **데이터 원본**를 선택한 후 **데이터 원본 추가**합니다.  
  
    2.  **내 보고서에 포함된 연결 사용**을 선택합니다.  
  
    3.  연결 유형 선택 **Microsoft SQL Server**합니다.  
  
    4.  서버 및 데이터베이스에 연결 문자열을 입력 합니다. 예를 들어  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5.  연결을 확인 하려면 선택은 **연결 테스트** 단추를 선택한 다음 선택 **확인**합니다.  
  
     데이터 소스를 만드는 방법에 대 한 자세한 내용은 참조 [추가 하 고 데이터 연결 &#40; 확인 보고서 작성기 및 SSRS &#41; ](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
3.  **데이터 집합 만들기**합니다.  
  
    1. 아래 **보고서 데이터**를 마우스 오른쪽 단추로 클릭 **데이터 집합**를 선택한 후 **데이터 집합 추가**합니다.  
  
    2. **내 보고서에 포함된 데이터 집합 사용**을 선택합니다.  
  
    3. 만든 데이터 원본을 선택 합니다.  
  
    4. 선택 된 **텍스트** 쿼리 형식을 복사 하 고 다음 쿼리를 붙여넣습니다는 **쿼리** 텍스트 상자:  
  
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
  
    5. **확인**을 선택합니다.  
  
     데이터 집합을 만드는 방법에 대 한 자세한 내용은 참조 [만들기 공유 데이터 집합 또는 포함 된 데이터 집합 &#40; 보고서 작성기 및 SSRS &#41; ](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
  
## <a name="see-also"></a>참고 항목  
* [공유 데이터 집합 디자인 뷰 &#40; 보고서 작성기 &#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
* [일련 &#40;에 도구 설명 표시 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)
* [자습서: Power BI의 트리 맵](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)
* [트리 맵: Microsoft Research Data Visualization Apps for Office](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
<br>  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]


