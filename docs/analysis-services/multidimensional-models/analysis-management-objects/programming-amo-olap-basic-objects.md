---
title: "AMO OLAP 기본 개체 프로그래밍 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, OLAP
- OLAP [AMO]
- AMO, OLAP
ms.assetid: ad1c970e-c0cb-4687-9563-56ab62c2db5f
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e92a5a964dc95906cc6d74e983723868e7b48c61
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="programming-amo-olap-basic-objects"></a>AMO OLAP 기본 개체 프로그래밍
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]복잡 한 만드는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체는 매우 간단 하지만 세부 사항에 주의 기울여야 합니다. 이 항목에서는 OLAP 기본 개체를 프로그래밍하는 방법에 대해 자세히 설명합니다. 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [차원 개체](#Dim)  
  
-   [큐브 개체](#Cub)  
  
-   [MeasureGroup 개체](#MG)  
  
-   [파티션 개체](#Part)  
  
-   [Aggregation 개체](#AD)  
  
##  <a name="Dim"></a>차원 개체  
 차원을 관리하거나 처리하려면 <xref:Microsoft.AnalysisServices.Dimension> 개체를 프로그래밍하십시오.  
  
### <a name="creating-dropping-and-finding-a-dimension"></a>차원 만들기, 삭제 및 찾기  
 <xref:Microsoft.AnalysisServices.Dimension> 개체를 만들려면 다음 네 단계를 수행하십시오.  
  
1.  차원 개체를 만들고 기본 특성을 채웁니다.  
  
     기본 특성에는 이름, 차원 유형, 저장소 모드, 데이터 원본 바인딩, 특성 All 멤버 이름 및 기타 차원 특성이 있습니다.  
  
     차원을 만들기 전에 해당 차원이 아직 없다는 것을 확인해야 합니다. 차원이 있을 경우 기존 차원이 삭제된 후 다시 만들어집니다.  
  
2.  차원을 정의하는 특성을 만듭니다.  
  
     각 특성은 사용하기 전에 먼저 개별적으로 스키마에 추가되어야 합니다(예제 코드의 끝에 있는 CreateDataItem 메서드 참조). 그래야 차원의 특성 컬렉션에 추가할 수 있습니다.  
  
     모든 특성의 키 및 이름 열을 정의해야 합니다.  
  
     차원의 기본 키 특성은 차원에 대한 키 액세스여야 하므로 AttributeUsage.Key로 정의해야 합니다.  
  
3.  사용자가 차원 탐색을 위해 액세스할 계층을 만듭니다.  
  
     계층을 만들면 수준이 만들어진 순서에 따라 위쪽에서 아래쪽으로 수준 순서가 정의됩니다. 계층의 수준 컬렉션의 맨 처음에 추가된 수준이 가장 높은 수준입니다.  
  
4.  현재 차원의 Update 메서드를 사용하여 서버를 업데이트합니다.  
  
 다음 샘플 코드는 예제 데이터베이스의 Adventure Works products 테이블에서 Product 차원을 만듭니다.  
  
```  
static void CreateProductDimension(Database db, string datasourceName)  
{  
    // Create the Product dimension  
    Dimension dim = db.Dimensions.FindByName("Product");  
    if ( dim != null)  
       dim.Drop();  
    dim = db.Dimensions.Add("Product");  
    dim.Type = DimensionType.Products;  
    dim.UnknownMember = UnknownMemberBehavior.Hidden;  
    dim.AttributeAllMemberName = "All Products";  
    dim.Source = new DataSourceViewBinding(datasourceName);  
    dim.StorageMode = DimensionStorageMode.Molap;  
  
    #region Create attributes  
  
    DimensionAttribute attr;  
  
    attr = dim.Attributes.Add("Product Name");  
    attr.Usage = AttributeUsage.Key;  
    attr.Type = AttributeType.Product;  
    attr.OrderBy = OrderBy.Name;  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductKey"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProduct", "EnglishProductName");  
  
    attr = dim.Attributes.Add("Product Line");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductLine"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductLineName");  
  
    attr = dim.Attributes.Add("Model Name");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ModelName"));  
    attr.AttributeRelationships.Add(new AttributeRelationship("Product Line"));  
    attr.AttributeRelationships.Add(new AttributeRelationship("Subcategory"));  
  
    attr = dim.Attributes.Add("Subcategory");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProductSubcategory", "ProductSubcategoryKey"));  
    attr.KeyColumns[0].NullProcessing = NullProcessing.UnknownMember;  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProductSubcategory", "EnglishProductSubcategoryName");  
    attr.AttributeRelationships.Add(new AttributeRelationship("Category"));  
  
    attr = dim.Attributes.Add("Category");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProductCategory", "ProductCategoryKey"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProductCategory", "EnglishProductCategoryName");  
  
    attr = dim.Attributes.Add("List Price");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ListPrice"));  
    attr.AttributeHierarchyEnabled = false;  
  
    attr = dim.Attributes.Add("Size");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "Size"));  
    attr.AttributeHierarchyEnabled = false;  
  
    attr = dim.Attributes.Add("Weight");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "Weight"));  
    attr.AttributeHierarchyEnabled = false;  
  
    #endregion  
  
    #region Create hierarchies  
  
    Hierarchy hier;  
  
    hier = dim.Hierarchies.Add("Product Model Categories");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Category").SourceAttributeID = "Category";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Subcategory";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Model Name";  
  
    hier = dim.Hierarchies.Add("Product Categories");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Category").SourceAttributeID = "Category";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Subcategory";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Product Name";  
  
    hier = dim.Hierarchies.Add("Product Model Lines");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Product Line";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Model Name";  
  
    #endregion  
  
    dim.Update();  
}  
  
static DataItem CreateDataItem(DataSourceView dsv, string tableName, string columnName)  
{  
    DataTable dataTable = ((DataSourceView)dsv).Schema.Tables[tableName];  
    DataColumn dataColumn = dataTable.Columns[columnName];  
    return new DataItem(tableName, columnName,  
        OleDbTypeConverter.GetRestrictedOleDbType(dataColumn.DataType));  
}  
  
```  
  
### <a name="processing-a-dimension"></a>차원 처리  
 차원을 처리하는 과정은 <xref:Microsoft.AnalysisServices.Dimension> 개체의 Process 메서드를 사용하는 것과 마찬가지로 간단합니다.  
  
 차원 처리 작업은 해당 차원을 사용하는 모든 큐브에 영향을 줄 수 있습니다. 처리 옵션에 대 한 자세한 내용은 참조 하세요. [다차원 모델 &#40; 처리 Analysis Services &#41; ](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 다음 코드에서는 제공된 데이터베이스의 모든 차원에서 증분 업데이트를 수행합니다.  
  
```  
static void UpdateAllDimensions(Database db)  
{  
    foreach (Dimension dim in db.Dimensions)  
        dim.Process(ProcessType.ProcessUpdate);  
}  
```  
  
##  <a name="Cub"></a>큐브 개체  
 큐브를 관리하거나 처리하려면 <xref:Microsoft.AnalysisServices.Cube> 개체를 프로그래밍하십시오.  
  
### <a name="creating-dropping-and-finding-a-cube"></a>큐브 만들기, 삭제 및 찾기  
 큐브 관리는 차원 관리와 비슷합니다. <xref:Microsoft.AnalysisServices.Cube> 개체를 만들려면 다음 네 단계를 수행하십시오.  
  
1.  큐브 개체를 만들고 기본 특성을 채웁니다.  
  
     기본 특성에는 이름, 저장소 모드, 데이터 원본 바인딩, 기본 측정값 및 기타 큐브 특성이 있습니다.  
  
     큐브를 만들기 전에 해당 큐브가 없다는 것을 확인해야 합니다. 예제에서는 큐브가 있을 경우 기존 차원이 삭제된 후 다시 만들어집니다.  
  
2.  큐브의 차원을 추가합니다.  
  
     차원은 데이터베이스의 현재 큐브 차원 컬렉션에 추가되므로, 큐브 차원은 데이터베이스 차원 컬렉션에 대한 참조입니다. 각 차원은 개별적으로 큐브에 매핑되어야 합니다. 예제에서 차원은 데이터베이스 차원 내부 식별자, 큐브 차원의 이름 및 큐브의 명명된 차원에 대한 ID를 제공하며 매핑됩니다.  
  
     예제 코드에서는 "Date" 차원이 세 번 추가됩니다. 자세히 말해서 Date, Ship Date, Delivery Date 등의 다른 큐브 차원 이름을 사용하여 해당 차원을 추가할 때마다 추가됩니다. 이러한 차원을 “롤플레잉 차원"이라고 합니다. 기본 차원은 Date 차원으로 같지만 팩트 테이블에서는 다른 "역할"(Order Date, Ship Date, Delivery Date)에 사용됩니다. "롤플레잉" 차원이 정의되는 방법을 이해하려면 이 문서의 뒷부분에 나오는 "MeasureGroup 만들기, 삭제 및 찾기"를 참조하십시오.  
  
3.  큐브 데이터 검색을 위해 사용자가 액세스할 측정값 그룹을 만듭니다.  
  
     측정값 그룹을 만드는 방법은 이 문서의 뒷부분에 나오는 "MeasureGroup 만들기, 삭제 및 찾기"에 설명되어 있습니다. 예제에서는 각 측정값 그룹별로 다른 메서드로 측정값 그룹 생성을 래핑합니다.  
  
4.  현재 큐브의 Update 메서드를 사용하여 서버를 업데이트합니다.  
  
     서버의 모든 개체를 완전히 업데이트하기 위해 update 메서드는 Update 옵션 ExpandFull과 함께 사용됩니다.  
  
 다음 코드 예제에서는 Adventure Works 큐브의 일부를 만듭니다. Adventure Works Analysis Services Project 예제에 포함된 모든 차원 또는 측정값 그룹을 만들지는 않습니다.  
  
```  
static void CreateAdventureWorksCube(Database db, string datasourceName)  
{  
    // Create the Adventure Works cube  
    Cube cube = db.Cubes.FindByName("Adventure Works");  
    if ( cube != null)  
       cube.Drop();  
    db.Cubes.Add("Adventure Works");  
    cube.DefaultMeasure = "[Reseller Sales Amount]";  
    cube.Source = new DataSourceViewBinding(datasourceName);  
    cube.StorageMode = StorageMode.Molap;  
  
    #region Create cube dimensions  
  
    Dimension dim;  
  
    dim = db.Dimensions.GetByName("Date");  
    cube.Dimensions.Add(dim.ID, "Date", "Order Date Key - Dim Time");  
    cube.Dimensions.Add(dim.ID, "Ship Date",  
        "Ship Date Key - Dim Time");  
    cube.Dimensions.Add(dim.ID, "Delivery Date",  
        "Delivery Date Key - Dim Time");  
  
    dim = db.Dimensions.GetByName("Customer");  
    cube.Dimensions.Add(dim.ID);  
  
    dim = db.Dimensions.GetByName("Reseller");  
    cube.Dimensions.Add(dim.ID);  
    #endregion  
  
    #region Create measure groups  
  
    CreateSalesReasonsMeasureGroup(cube);  
    CreateInternetSalesMeasureGroup(cube);  
    CreateResellerSalesMeasureGroup(cube);  
    CreateCustomersMeasureGroup(cube);  
    CreateCurrencyRatesMeasureGroup(cube);  
  
    #endregion  
  
    cube.Update(UpdateOptions.ExpandFull);  
}  
```  
  
### <a name="processing-a-cube"></a>큐브 처리  
 큐브를 처리하는 과정은 <xref:Microsoft.AnalysisServices.Cube> 개체의 Process 메서드를 사용하는 것과 마찬가지로 간단합니다. 큐브를 처리하면 큐브의 모든 측정값 그룹과 측정값 그룹의 모든 파티션도 처리됩니다. 큐브에서는 파티션이 유일하게 처리할 수 있는 개체이며, 처리 목적으로 제공되는 측정값 그룹은 유일한 파티션 컨테이너입니다. 큐브에 대해 지정된 처리 유형은 파티션에 전파됩니다. 큐브 및 측정값 그룹의 처리는 내부적으로 차원 및 파티션의 처리로 확인됩니다.  
  
 처리 옵션에 대 한 자세한 내용은 참조 하세요. [처리 개체 &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md), 및 [다차원 모델 &#40; 처리 Analysis Services &#41; ](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 다음 코드에서는 지정된 데이터베이스의 모든 큐브에서 전체 처리를 수행합니다.  
  
```  
foreach (Cube cube in db.Cubes)  
             cube.Process(ProcessType.ProcessFull);  
     }  
```  
  
##  <a name="MG"></a>MeasureGroup 개체  
 측정값 그룹을 관리하거나 처리하려면 <xref:Microsoft.AnalysisServices.MeasureGroup> 개체를 프로그래밍하십시오.  
  
### <a name="creating-dropping-and-finding-a-measuregroup"></a>MeasureGroup 만들기, 삭제 및 찾기  
 측정값 그룹 관리는 차원 및 큐브 관리와 비슷합니다. <xref:Microsoft.AnalysisServices.MeasureGroup> 개체를 만들려면 다음 단계를 수행하십시오.  
  
1.  측정값 그룹 개체를 만들고 기본 특성을 채웁니다.  
  
     기본 특성에는 이름, 저장소 모드, 처리 모드, 기본 측정값 및 기타 측정값 그룹 특성이 있습니다.  
  
     측정값 그룹을 만들기 전에 해당 측정값 그룹이 없다는 것을 확인합니다. 다음 예제 코드에서는 측정값 그룹이 있을 경우 기존 측정값 그룹이 삭제된 후 다시 만들어집니다.  
  
2.  측정값 그룹의 측정값을 만듭니다. 만들어진 각 측정값에는 이름, 집계 함수, 원본 열, 형식 문자열에 대한 특성이 지정됩니다. 다른 특성도 지정할 수 있습니다. 다음 예제 코드에서는 CreateDataItem 메서드가 스키마에 열을 추가합니다.  
  
3.  측정값 그룹의 차원을 추가합니다.  
  
4.  차원이 부모 큐브 차원 컬렉션의 현재 측정값 그룹 차원 컬렉션에 추가됩니다. 차원이 측정값 그룹 차원 컬렉션에 포함된 후에는 차원을 통해 측정값 그룹을 검색할 수 있도록 팩트 테이블의 키 열을 차원에 매핑할 수 있습니다.  
  
     다음 예제 코드에서 "Mapping dimension and key column from fact table" 아래의 행을 참조하십시오. 롤플레잉 차원은 서로 다른 서로게이트 키를 서로 다른 이름의 같은 차원에 연결하여 구현됩니다. 각 롤플레잉 차원(Date, Ship Date, Delivery Date)에 대해 각기 다른 서로게이트 키(OrderDateKey, ShipDateKey, DueDateKey)가 연결됩니다. 모든 키는 팩트 테이블 FactInternetSales에 있습니다.  
  
5.  측정값 그룹의 디자인된 파티션을 추가합니다.  
  
     다음 예제 코드에서는 파티션 생성이 한 메서드로 래핑됩니다.  
  
6.  현재 측정값 그룹의 Update 메서드를 사용하여 서버를 업데이트합니다.  
  
     다음 예제 코드에서는 큐브가 업데이트될 때 모든 측정값 그룹이 업데이트됩니다.  
  
 다음 코드 예제에서는 Adventure Works Analysis Services Project 예제의 InternetSales 측정값 그룹을 만듭니다.  
  
```  
static void CreateInternetSalesMeasureGroup(Cube cube)  
{  
    // Create the Internet Sales measure group  
    Database db = cube.Parent;  
    MeasureGroup mg = cube.MeasureGroups.FindByName("Internet Sales");  
    if ( mg != null)  
       mg.Drop();  
    mg = cube.MeasureGroups.Add("Internet Sales");  
    mg.StorageMode = StorageMode.Molap;  
    mg.ProcessingMode = ProcessingMode.LazyAggregations;  
    mg.Type = MeasureGroupType.Sales;  
  
    #region Create measures  
  
    Measure meas;  
  
    meas = mg.Measures.Add("Internet Sales Amount");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "Currency";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesAmount");  
  
    meas = mg.Measures.Add("Internet Order Quantity");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "#,#";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "OrderQuantity");  
  
    meas = mg.Measures.Add("Internet Unit Price");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "Currency";  
    meas.Visible = false;  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "UnitPrice");  
  
    meas = mg.Measures.Add("Internet Total Product Cost");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    //meas.MeasureExpression = "[Internet Total Product Cost] * [Average Rate]";  
    meas.FormatString = "Currency";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "TotalProductCost");  
  
    meas = mg.Measures.Add("Internet Order Count");  
    meas.AggregateFunction = AggregationFunction.Count;  
    meas.FormatString = "#,#";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ProductKey");  
  
    #endregion  
  
    #region Create measure group dimensions  
  
    CubeDimension cubeDim;  
    RegularMeasureGroupDimension regMgDim;  
    ManyToManyMeasureGroupDimension mmMgDim;  
    MeasureGroupAttribute mgAttr;  
  
    //   Mapping dimension and key column from fact table  
    //      > select dimension and add it to the measure group  
    cubeDim = cube.Dimensions.GetByName("Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
  
    //      > add key column from dimension and map it with   
    //        the surrogate key in the fact table  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);   // this is dimension key column  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "OrderDateKey"));   // this surrogate key in fact table  
  
    cubeDim = cube.Dimensions.GetByName("Ship Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ShipDateKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Delivery Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "DueDateKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Customer");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Full Name").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "CustomerKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Product");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Product Name").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ProductKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Source Currency");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Currency").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "CurrencyKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Sales Reason");  
    mmMgDim = new ManyToManyMeasureGroupDimension();  
    mmMgDim.CubeDimensionID = cubeDim.ID;  
    mmMgDim.MeasureGroupID = cube.MeasureGroups.GetByName("Sales Reasons").ID;  
    mg.Dimensions.Add(mmMgDim);  
  
    cubeDim = cube.Dimensions.GetByName("Internet Sales Order Details");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Sales Order Key").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesOrderNumber"));  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesOrderLineNumber"));  
  
    #endregion  
  
    #region Create partitions  
  
    CreateInternetSalesMeasureGroupPartitions( mg)  
  
    #endregion  
}  
```  
  
### <a name="processing-a-measure-group"></a>측정값 그룹 처리  
 측정값 그룹을 처리하는 과정은 <xref:Microsoft.AnalysisServices.MeasureGroup> 개체의 Process 메서드를 사용하는 것과 마찬가지로 간단합니다. 측정값 그룹을 처리하면 측정값 그룹에 속한 모든 파티션도 처리됩니다. 측정값 그룹의 처리는 내부적으로 차원 및 파티션의 처리로 확인됩니다. 이 문서의 [파티션 처리](#ProcPart) 를 참조하십시오.  
  
 처리 옵션에 대 한 자세한 내용은 참조 하세요. [처리 개체 &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md), 및 [다차원 모델 &#40; 처리 Analysis Services &#41; ](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 다음 코드에서는 제공된 큐브의 모든 측정값 그룹에서 전체 처리를 수행합니다.  
  
```  
static void FullProcessAllMeasureGroups(Cube cube)  
{  
    foreach (MeasureGroup mg in cube.MeasureGroups)  
        mg.Process(ProcessType.ProcessFull);  
}  
```  
  
##  <a name="Part"></a>파티션 개체  
 파티션을 관리하거나 처리하려면 <xref:Microsoft.AnalysisServices.Partition> 개체를 프로그래밍하십시오.  
  
### <a name="creating-dropping-and-finding-a-partition"></a>파티션 만들기, 삭제 및 찾기  
 파티션은 두 단계를 수행하여 만들 수 있는 간단한 개체입니다.  
  
1.  파티션 개체를 만들고 기본 특성을 채웁니다.  
  
     기본 특성에는 이름, 저장소 모드, 파티션 원본, 사이트 및 기타 측정값 그룹 특성이 있습니다. 파티션 원본은 현재 파티션에 대한 SQL select 문을 정의합니다. 조각은 현재 파티션에 포함된 부모 측정값 그룹의 차원 중 일부를 구분하는 튜플이나 집합을 지정하는 MDX 식입니다. MOLAP 파티션의 경우 파티션을 처리할 때마다 조각화가 자동으로 결정됩니다.  
  
     파티션을 만들기 전에 해당 파티션이 없다는 것을 확인해야 합니다. 다음 예제 코드에서는 파티션이 있을 경우 기존 파티션이 삭제된 후 다시 만들어집니다.  
  
2.  현재 파티션의 Update 메서드를 사용하여 서버를 업데이트합니다.  
  
     다음 예제 코드에서는 큐브가 업데이트될 때 모든 파티션이 업데이트됩니다.  
  
 다음 코드 예제에서는 'InternetSales' 측정값 그룹의 파티션을 만듭니다.  
  
```  
static void CreateInternetSalesMeasureGroupPartitions(MeasureGroup mg)  
{  
    Partition part;  
    part = mg.Partitions.FindByName("Internet_Sales_184");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_184");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey <= '184'");  
    part.Slice = "[Date].[Calendar Year].&[2001]";  
    part.Annotations.Add("LastOrderDateKey", "184");  
  
    part = mg.Partitions.FindByName("Internet_Sales_549");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_549");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey > '184' AND OrderDateKey <= '549'");  
    part.Slice = "[Date].[Calendar Year].&[2002]";  
    part.Annotations.Add("LastOrderDateKey", "549");  
  
    part = mg.Partitions.FindByName("Internet_Sales_914");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_914");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey > '549' AND OrderDateKey <= '914'");  
    part.Slice = "[Date].[Calendar Year].&[2003]";  
    part.Annotations.Add("LastOrderDateKey", "914");  
}  
```  
  
###  <a name="ProcPart"></a>파티션 처리  
 파티션을 처리하는 과정은 <xref:Microsoft.AnalysisServices.Partition> 개체의 Process 메서드를 사용하는 것과 마찬가지로 간단합니다.  
  
 처리 옵션에 대 한 자세한 내용은 참조 하세요. [처리 개체 &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md) 및 [다차원 모델 &#40; 처리 Analysis Services &#41; ](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 다음 코드 예제에서는 지정된 측정값 그룹의 모든 파티션에서 전체 처리를 수행합니다.  
  
```  
static void FullProcessAllPartitions(MeasureGroup mg)  
{  
    foreach (Partition part in mg.Partitions)  
        part.Process(ProcessType.ProcessFull);  
}  
```  
  
### <a name="merging-partitions"></a>파티션 병합  
 파티션 병합이란 두 개 이상의 파티션을 하나의 파티션으로 만드는 작업입니다.  
  
 파티션 병합은 <xref:Microsoft.AnalysisServices.Partition> 개체의 메서드입니다. 이 명령은 하나 이상의 원본 파티션의 데이터를 대상 파티션에 병합한 다음 원본 파티션을 삭제합니다.  
  
 다음 조건이 모두 충족되는 경우에만 파티션을 병합할 수 있습니다.  
  
-   파티션이 같은 측정값 그룹에 있어야 합니다.  
  
-   파티션이 같은 모드(MOLAP, HOLAP 및 ROLAP)로 저장되어 있어야 합니다.  
  
-   파티션이 같은 서버에 있어야 하며, 같은 서버에 있는 경우 원격 파티션을 병합할 수 있습니다.  
  
 이전 버전과 달리에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 모든 원본 파티션의 집계 디자인이 같지 않아도있지 않습니다.  
  
 대상 파티션에 대한 집계 결과 집합이 병합 명령을 실행하기 이전 상태의 집계 집합과 같아야 합니다.  
  
 다음 코드 예제에서는 지정된 측정값 그룹의 모든 파티션을 병합합니다. 파티션은 측정값 그룹의 첫 번째 파티션에 병합됩니다.  
  
```  
static void MergeAllPartitions(MeasureGroup mg)  
{  
    if (mg.Partitions.Count > 1)  
    {  
        Partition[] partArray = new Partition[mg.Partitions.Count - 1];  
        for (int i = 1; i < mg.Partitions.Count; i++)  
            partArray[i - 1] = mg.Partitions[i];  
        mg.Partitions[0].Merge(partArray);  
        //To have last changes in the server reflected in AMO  
        mg.Refresh();  
    }  
```  
  
##  <a name="AD"></a>Aggregation 개체  
 집계를 디자인하여 하나 이상의 파티션에 적용하려면 <xref:Microsoft.AnalysisServices.Aggregation> 개체를 프로그래밍하십시오.  
  
### <a name="creating-and-dropping-aggregations"></a>집계 만들기 및 삭제  
 집계는 <xref:Microsoft.AnalysisServices.AggregationDesign> 개체의 DesignAggregations 메서드를 사용하여 쉽게 만들어서 측정값 그룹에 지정할 수 있습니다. <xref:Microsoft.AnalysisServices.AggregationDesign> 개체는 별개에서의 개체로 <xref:Microsoft.AnalysisServices.AggregationDesign> 에 포함 된 개체는 <xref:Microsoft.AnalysisServices.MeasureGroup> 개체입니다. 집계는 지정된 최적화 수준(0 - 100) 또는 지정된 저장소 수준(바이트)까지 디자인할 수 있습니다. 여러 파티션에서 동일한 집계 디자인을 사용할 수 있습니다.  
  
 다음 코드 예제에서는 제공된 측정값 그룹의 모든 파티션에 대한 집계를 만듭니다. 파티션의 기존 집계는 모두 삭제됩니다.  
  
```  
static public String DesignAggregationsOnPartitions(MeasureGroup mg, double optimizationWanted, double maxStorageBytes)  
{  
    double optimization = 0;  
    double storage = 0;  
    long aggCount = 0;  
    bool finished = false;  
    AggregationDesign ad = null;  
    String aggDesignName;  
    String AggregationsDesigned = "";  
    aggDesignName = mg.AggregationPrefix + "_" + mg.Name;  
    ad = mg.AggregationDesigns.Add();  
    ad.Name = aggDesignName;  
    ad.InitializeDesign();  
    while ((!finished) && (optimization < optimizationWanted) && (storage < maxStorageBytes))  
    {  
        ad.DesignAggregations(out optimization, out storage, out aggCount, out finished);  
    }  
    ad.FinalizeDesign();  
    foreach (Partition part in mg.Partitions)  
    {  
        part.AggregationDesignID = ad.ID;  
        AggregationsDesigned += aggDesignName + " = " + aggCount.ToString() + " aggregations designed\r\n\tOptimization: " + optimization.ToString() + "/" + optimizationWanted.ToString() + "\n\r\tStorage: " + storage.ToString() + "/" + maxStorageBytes.ToString() + " ]\n\r";  
     }  
     return AggregationsDesigned;  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices>   
 [AMO 클래스 소개](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO OLAP 클래스](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)   
 [논리적 아키텍처 &#40; Analysis Services-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [데이터베이스 개체 &#40; Analysis Services-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [다차원 모델 &#40; 처리 Analysis Services &#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Analysis Services 다차원 모델링 자습서에 대 한 예제 데이터 및 프로젝트 설치](../../../analysis-services/install-sample-data-and-projects.md)  
  
  
