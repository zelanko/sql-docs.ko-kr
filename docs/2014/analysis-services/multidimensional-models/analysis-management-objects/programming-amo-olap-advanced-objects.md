---
title: AMO OLAP 고급 개체 프로그래밍 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, OLAP
- OLAP [AMO]
- AMO, OLAP
ms.assetid: b75f35a7-32df-4f22-983d-324aa98e15a9
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6408cfd8dd3a7b8f7d6993ca84c3325bedddee24
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088291"
---
# <a name="programming-amo-olap-advanced-objects"></a>AMO OLAP 고급 개체 프로그래밍
  이 항목에서는 AMO(Analysis Management Objects) OLAP 고급 개체를 프로그래밍하는 방법에 대해 자세히 설명합니다. 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [동작 개체](#Action)  
  
-   [Kpi 개체](#KPI)  
  
-   [Perspective 개체](#Persp)  
  
-   [ProactiveCaching 개체](#PC)  
  
-   [번역 개체](#Transl)  
  
##  <a name="Action"></a> 동작 개체  
 Action 클래스 - 큐브의 특정 영역을 탐색할 때 활성 응답을 만드는 데 사용됩니다. 동작 개체는 AMO를 사용하여 정의될 수 있지만 데이터를 탐색하는 클라이언트 응용 프로그램에서 사용됩니다. 동작에는 여러 유형이 있을 수 있으므로 해당 유형에 따라 동작을 만들어야 합니다. 다음과 같은 유형의 동작이 있을 수 있습니다.  
  
-   동작이 발생하는 큐브에서 선택된 셀에 대한 기본 데이터를 나타내는 행 집합을 반환하는 드릴스루 동작  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 에서 동작이 발생하는 큐브에서 선택된 섹션과 연관된 보고서를 반환하는 보고 동작  
  
-   동작이 발생하는 큐브에서 선택된 섹션과 연관된 동작 요소(URL, HTML, DataSet, RowSet 및 기타 요소)를 반환하는 표준 동작  
  
 동작 개체를 만들려면 다음 단계를 수행해야 합니다.  
  
1.  파생 동작 개체를 만들고 기본 특성을 채웁니다.  
  
     기본 특성에는 동작 유형, 큐브의 대상 유형 또는 섹션, 동작을 사용할 수 있는 큐브의 대상 또는 특정 영역, 캡션 및 MDX 식 캡션의 위치가 있습니다.  
  
2.  동작 유형의 특정 특성을 채웁니다.  
  
     세 동작 유형에는 다양한 특성이 있으며, 다음 코드 예제에서 매개 변수를 참조하십시오.  
  
3.  동작을 큐브 컬렉션에 추가하고 큐브를 업데이트합니다. 동작은 업데이트 가능한 개체가 아닙니다.  
  
 동작을 테스트하려면 다른 응용 프로그램이 필요합니다. [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 동작을 테스트할 수 있습니다. 먼저 설치 해야 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 샘플 참조 [다차원 모델 개체 처리](../processing-a-multidimensional-model-analysis-services.md)합니다.  
  
 다음 코드 예제에서는 Adventure Works Analysis Services Project 예제의 세 가지 동작을 복제합니다. 다음 예제에 사용되는 동작은 "My"로 시작되므로 쉽게 구별할 수 있습니다.  
  
```  
static public void CreateActions(Cube cube)  
{  
    #region Adding a drillthrough action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My Reseller Details"))  
        cube.Actions.Remove("My Drillthrough Action",true);  
  
    //Create a Drillthrough action  
    DrillThroughAction dtaction = new DrillThroughAction("My Reseller Details", "My Drillthrough Action");  
  
    //Define the Action  
    dtaction.Type = ActionType.DrillThrough;  
    dtaction.TargetType = ActionTargetType.Cells;  
    dtaction.Target = "MeasureGroupMeasures(\"Reseller Sales\")";  
    dtaction.Caption = "My Drillthrough...";  
    dtaction.CaptionIsMdx = false;  
  
    #region create drillthrough action specifics  
    //Adding Drillthrough columns  
    //Adding Measure columns to the drillthrough  
    MeasureGroup mg = cube.MeasureGroups.FindByName("Reseller Sales");  
    MeasureBinding mb1 = new MeasureBinding();  
    mb1.MeasureID = mg.Measures.FindByName( "Reseller Sales Amount").ID;  
    dtaction.Columns.Add(mb1);  
  
    MeasureBinding mb2 = new MeasureBinding();  
    mb2.MeasureID = mg.Measures.FindByName("Reseller Order Quantity").ID;  
    dtaction.Columns.Add(mb2);  
  
    MeasureBinding mb3 = new MeasureBinding();  
    mb3.MeasureID = mg.Measures.FindByName("Reseller Unit Price").ID;  
    dtaction.Columns.Add(mb3);  
  
    //Adding Dimension Columns to the drillthrough  
    CubeAttributeBinding cb1 = new CubeAttributeBinding();  
    cb1.CubeID = cube.ID;  
    cb1.CubeDimensionID = cube.Dimensions.FindByName("Reseller").ID;  
    cb1.AttributeID = "Reseller Name";  
    cb1.Type = AttributeBindingType.All;  
    dtaction.Columns.Add(cb1);  
  
    CubeAttributeBinding cb2 = new CubeAttributeBinding();  
    cb2.CubeID = cube.ID;  
    cb2.CubeDimensionID = cube.Dimensions.FindByName("Product").ID;  
    cb2.AttributeID = "Product Name";  
    cb2.Type = AttributeBindingType.All;  
    dtaction.Columns.Add(cb2);  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(dtaction);  
    #endregion  
  
    #region Adding a Standard action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My City Map"))  
        cube.Actions.Remove("My Action", true);  
  
    //Create a Drillthrough action  
    StandardAction stdaction = new StandardAction("My City Map", "My Action");  
  
    //Define the Action  
    stdaction.Type = ActionType.Url;  
    stdaction.TargetType = ActionTargetType.AttributeMembers;  
    stdaction.Target = "[Geography].[City]";  
    stdaction.Caption = "\"My View Map for \" + [Geography].[City].CurrentMember.Member_Caption + \"...\"";  
    stdaction.CaptionIsMdx = true;  
  
    #region create standard action specifics  
    stdaction.Expression = "\"http://maps.msn.com/home.aspx?plce1=\" + " +  
        "[Geography].[City].CurrentMember.Name + \",\" + " +  
        "[Geography].[State-Province].CurrentMember.Name + \",\" + " +  
        "[Geography].[Country].CurrentMember.Name + " +  
        "\"&regn1=\" + " +  
        "Case " +  
            "When [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[Australia] " +  
                "Then \"3\" " +  
            "When [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[Canada] " +  
                "Or [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[United States] " +  
                "Then \"0\" " +  
                "Else \"1\" " +  
        "End ";  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(stdaction);  
  
    #endregion  
  
    #region Adding a Reporting action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My Sales Reason Comparisons"))  
        cube.Actions.Remove("My Report Action", true);  
  
    //Create a Report action  
    ReportAction rsaction = new ReportAction("My Sales Reason Comparisonsp", "My Report Action");  
  
    //Define the Action  
    rsaction.Type = ActionType.Report;  
    rsaction.TargetType = ActionTargetType.AttributeMembers;  
    rsaction.Target = "[Product].[Category]";  
    rsaction.Caption = "\"My Sales Reason Comparisons for \" + [Product].[Category].CurrentMember.Member_Caption + \"...\"";  
    rsaction.CaptionIsMdx = true;  
  
    #region create Report action specifics  
    rsaction.ReportServer = "MyRSSamplesServer";  
    rsaction.Path = "ReportServer?/AdventureWorks Sample Reports/Sales Reason Comparisons";  
    rsaction.ReportParameters.Add("ProductCategory", "UrlEscapeFragment( [Product].[Category].CurrentMember.UniqueName )");  
    rsaction.ReportFormatParameters.Add("rs:Command", "Render");  
    rsaction.ReportFormatParameters.Add("rs:Renderer", "HTML5");  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(rsaction);  
  
    #endregion  
}  
```  
  
##  <a name="KPI"></a> Kpi 개체  
 KPI(핵심 성과 지표)는 큐브의 측정값 그룹과 관련된 계산 모음으로 비즈니스 성취도 평가에 사용됩니다. <xref:Microsoft.AnalysisServices.Kpi> 개체는 AMO를 사용하여 정의될 수 있지만 데이터를 탐색하는 클라이언트 응용 프로그램에서 사용됩니다.  
  
 <xref:Microsoft.AnalysisServices.Kpi> 개체를 만들려면 다음 단계를 수행합니다.  
  
1.  <xref:Microsoft.AnalysisServices.Kpi> 개체를 만들고 기본 특성을 채웁니다.  
  
     기본 특성에는 설명, 표시 폴더, 관련된 측정값 그룹 및 값이 있습니다. 표시 폴더는 최종 사용자가 찾을 수 있도록 클라이언트 응용 프로그램에게 KPI의 위치를 알려 줍니다. 관련된 측정값 그룹은 모든 MDX 계산에서 참조하는 측정값 그룹을 나타냅니다. 값은 성과 지표의 실제 값을 MDX 식으로 보여 줍니다.  
  
2.  KPI 지표인 목표, 상태 및 추세를 정의합니다.  
  
     지표는 -1과 1 사이의 값으로 계산되는 MDX 식입니다. 그러나 지표 값의 범위는 브라우징 응용 프로그램에서 정의됩니다.  
  
3.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 KPI를 찾아보면 -1보다 작은 값은 -1로 처리되고 1보다 큰 값은 1로 처리됩니다.  
  
4.  그래픽 이미지를 정의합니다.  
  
     그래픽 이미지는 표시할 올바른 이미지 집합을 식별하기 위해 클라이언트 응용 프로그램에서 참조로 사용되는 문자열 값입니다. 그래픽 이미지 문자열에는 표시 함수의 동작도 정의됩니다. 일반적으로 범위는 불량에서 양호까지 홀수 개의 상태로 분할되며, 각 상태에는 집합의 이미지가 지정됩니다.  
  
     [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]를 사용하여 KPI를 찾는 경우에는 이름에 따라 지표 범위가 3가지 또는 5가지 상태로 분할됩니다. 범위가 반전되는 이름도 있습니다(예: -1이 '양호'이고 1이 '불량'). [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 범위에 사용되는 3가지 상태는 다음과 같습니다.  
  
    -   불량 = -1 ~ -0.5  
  
    -   보통 = -0.4999 ~ 0.4999  
  
    -   양호 = 0.50 ~ 1  
  
     [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 범위에 사용되는 5가지 상태는 다음과 같습니다.  
  
    -   불량 = -1 ~ -0.75  
  
    -   위험 = -0.7499 ~ -0.25  
  
    -   보통 = -0.2499 ~ 0.2499  
  
    -   향상 = 0.25 ~ 0.7499  
  
    -   양호 = 0.75 ~ 1  
  
 다음 표에서는 이미지의 용도, 이름 및 상태 수에 대해 설명합니다.  
  
|이미지 용도|이미지 이름|상태 수|  
|-----------------|----------------|----------------------|  
|상태|셰이프|3|  
|상태|신호등|3|  
|상태|도로 표지|3|  
|상태|계기|3|  
|상태|역방향 계기|5|  
|상태|온도계|3|  
|상태|실린더|3|  
|상태|면|3|  
|상태|분산 화살표|3|  
|추세|일반 화살표|3|  
|추세|상태 화살표|3|  
|추세|역방향 상태 화살표|5|  
|추세|면|3|  
  
1.  KPI는 업데이트 가능한 개체가 아니므로 KPI를 큐브 컬렉션에 추가한 후 큐브를 업데이트합니다.  
  
 KPI를 테스트하려면 다른 응용 프로그램이 필요합니다. [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 KPI를 테스트할 수 있습니다.  
  
 다음 코드 예제에서는 Adventure Works Analysis Services Project 예제에 포함된 Adventure Works 큐브의 "Financial Perpective/Grow Revenue" 폴더에 KPI를 만듭니다.  
  
```  
static public void CreateKPIs(Cube cube)  
{  
    Kpi kpi = cube.Kpis.Add("My Internet Revenue", "My Internet Revenue");  
    kpi.Description = "(My) Revenue achieved through direct sales via Interner";  
    kpi.DisplayFolder = "\\Financial Perspective\\Grow Revenue";  
    kpi.AssociatedMeasureGroupID = "Internet Sales";  
    kpi.Value = "[Measures].[Internet Sales Amount]";  
    #region Goal  
    kpi.Goal = "Case" +  
               "     When IsEmpty" +  
               "          (" +  
               "            ParallelPeriod" +  
               "            (" +  
               "              [Date].[Fiscal Time].[Fiscal Year]," +  
               "              1," +  
               "              [Date].[Fiscal Time].CurrentMember" +  
               "            )" +  
               "          )" +   
               "     Then [Measures].[Internet Sales Amount]" +  
               "     Else 1.10 *" +  
               "          (" +  
               "            [Measures].[Internet Sales Amount]," +  
               "            ParallelPeriod" +  
               "            (" +  
               "              [Date].[Fiscal Time].[Fiscal Year]," +  
               "              1," +  
               "              [Date].[Fiscal Time].CurrentMember" +  
               "            )" +  
               "          ) " +  
               " End";  
    #endregion  
    #region Status  
    kpi.Status = "Case" +  
                 "   When KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) >= .95 " +  
                 "   Then 1 " +  
                 "   When KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) <  .95 " +  
                 "        And  " +  
                 "        KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) >= .85 " +  
                 "   Then 0 " +  
                 "   Else -1 " +  
                 "End";  
    #endregion  
    #region Trend  
    kpi.Trend = "Case " +  
                "    When VBA!Abs " +  
                "         ( " +  
                "           KpiValue( \"Internet Revenue\" ) -  " +  
                "           ( " +  
                "             KpiValue ( \"Internet Revenue\" ), " +  
                "             ParallelPeriod " +  
                "             (  " +  
                "               [Date].[Fiscal Time].[Fiscal Year], " +  
                "               1, " +  
                "               [Date].[Fiscal Time].CurrentMember " +  
                "             ) " +  
                "           ) / " +  
                "           ( " +  
                "             KpiValue ( \"Internet Revenue\" ), " +  
                "             ParallelPeriod " +  
                "             (  " +  
                "               [Date].[Fiscal Time].[Fiscal Year], " +  
                "               1, " +  
                "               [Date].[Fiscal Time].CurrentMember " +  
                "             ) " +  
                "           )   " +  
                "         ) <=.02  " +  
                "    Then 0 " +  
                "    When KpiValue( \"Internet Revenue\" ) -  " +  
                "         ( " +  
                "           KpiValue ( \"Internet Revenue\" ), " +  
                "           ParallelPeriod " +  
                "           (  " +  
                "             [Date].[Fiscal Time].[Fiscal Year], " +  
                "             1, " +  
                "             [Date].[Fiscal Time].CurrentMember " +  
                "           ) " +  
                "         ) / " +  
                "         ( " +  
                "           KpiValue ( \"Internet Revenue\" ), " +  
                "           ParallelPeriod " +  
                "           (  " +  
                "             [Date].[Fiscal Time].[Fiscal Year], " +  
                "             1, " +  
                "             [Date].[Fiscal Time].CurrentMember " +  
                "           ) " +  
                "         )  >.02 " +  
                "    Then 1 " +  
                "    Else -1 " +  
                "End";  
    #endregion  
    kpi.TrendGraphic = "Standard Arrow";  
    kpi.StatusGraphic = "Cylinder";  
}.  
```  
  
##  <a name="Persp"></a> Perspective 개체  
 <xref:Microsoft.AnalysisServices.Perspective> 개체는 AMO를 사용하여 정의될 수 있지만 데이터를 탐색하는 클라이언트 응용 프로그램에서 사용됩니다.  
  
 <xref:Microsoft.AnalysisServices.Perspective> 개체를 만들려면 다음 단계를 수행합니다.  
  
1.  <xref:Microsoft.AnalysisServices.Perspective> 개체를 만들고 기본 특성을 채웁니다.  
  
     기본 특성에는 이름, 기본 측정값, 설명 및 주석이 있습니다.  
  
2.  최종 사용자에게 표시할 부모 큐브의 모든 개체를 추가합니다.  
  
     큐브 차원(특성 및 계층), 측정값 그룹(측정값 및 측정값 그룹), 동작, KPI 및 계산을 추가합니다.  
  
3.  큐브 뷰는 업데이트 가능한 개체가 아니므로 큐브 뷰를 큐브 컬렉션에 추가한 후 큐브를 업데이트합니다.  
  
 큐브 뷰를 테스트하려면 다른 응용 프로그램이 필요합니다. [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 큐브 뷰를 테스트할 수 있습니다.  
  
 다음 코드 예제에서는 제공된 큐브에 대해 "Direct Sales"라는 큐브 뷰를 만듭니다.  
  
```  
static public void CreatePerspectives(Cube cube)  
{  
    Perspective perspective = cube.Perspectives.Add("Direct Sales", "Direct Sales");  
    CubeDimension dim1 = cube.Dimensions.GetByName("Date");  
    PerspectiveDimension pdim1 = perspective.Dimensions.Add(dim1.DimensionID);  
    pdim1.Attributes.Add("Date");  
    pdim1.Attributes.Add("Calendar Year");  
    pdim1.Attributes.Add("Fiscal Year");  
    pdim1.Attributes.Add("Calendar Quarter");  
    pdim1.Attributes.Add("Fiscal Quarter");  
    pdim1.Attributes.Add("Calendar Month Number");  
    pdim1.Attributes.Add("Fiscal Month Number");  
    pdim1.Hierarchies.Add("Calendar Time");  
    pdim1.Hierarchies.Add("Fiscal Time");  
  
    CubeDimension dim2 = cube.Dimensions.GetByName("Product");  
    PerspectiveDimension pdim2 = perspective.Dimensions.Add(dim2.DimensionID);  
    pdim2.Attributes.Add("Product Name");  
    pdim2.Attributes.Add("Product Line");  
    pdim2.Attributes.Add("Model Name");  
    pdim2.Attributes.Add("List Price");  
    pdim2.Attributes.Add("Size");  
    pdim2.Attributes.Add("Weight");  
    pdim2.Hierarchies.Add("Product Model Categories");  
    pdim2.Hierarchies.Add("Product Categories");  
  
    PerspectiveMeasureGroup pmg = perspective.MeasureGroups.Add("Internet Sales");  
    pmg.Measures.Add("Internet Sales Amount");  
    pmg.Measures.Add("Internet Order Quantity");  
    pmg.Measures.Add("Internet Unit Price");  
  
    pmg = perspective.MeasureGroups.Add("Reseller Sales");  
    pmg.Measures.Add("Reseler Sales Amount");  
    pmg.Measures.Add("Reseller Order Quantity");  
    pmg.Measures.Add("Reseller Unit Price");  
  
    PerspectiveAction pact = perspective.Actions.Add("Drillthrough Action");  
  
    PerspectiveKpi pkpi = perspective.Kpis.Add("Internet Revenue");  
    Cube.Update();  
}  
```  
  
##  <a name="PC"></a> ProactiveCaching 개체  
 <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체는 AMO에서 정의될 수 있습니다.  
  
 <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체를 만들려면 다음 단계를 수행합니다.  
  
1.  <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체를 만듭니다.  
  
     정의할 기본 특성이 없습니다.  
  
2.  캐시 사양을 추가합니다.  
  
|사양|Description|  
|-------------------|-----------------|  
|AggregationStorage|집계에 대한 저장소 유형입니다.<br /><br /> 파티션에만 적용됩니다. 차원에서 `Regular.`여야 합니다.|  
|SilenceInterval|MOLAP 이미징 처리를 시작하기 전에 캐시가 존재하는 최소 시간입니다.|  
|대기 시간|가장 이른 알림과 MOLAP 이미지가 삭제된 시점 사이의 시간입니다.|  
|SilenceOverrideInterval|MOLAP 이미징을 무조건 시작하기 전에 초기 알림을 받은 후 경과해야 하는 시간입니다.|  
|ForceRebuildInterval|새로운 MOLAP 이미지가 삭제된 이후부터 MOLAP 이미징이 무조건 시작되기 전까지의 시간입니다(알림 없음).|  
|OnlineMode|MOLAP 이미지를 사용할 수 있는 때입니다.<br /><br /> `Immediate` 또는 `OnCacheComplete`가 될 수 있습니다.|  
  
1.  <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체를 부모 컬렉션에 추가합니다. <xref:Microsoft.AnalysisServices.ProactiveCaching>은 업데이트 가능한 개체가 아니므로 부모를 업데이트해야 합니다.  
  
 다음 코드 예제에서는 지정된 데이터베이스의 Adventure Works 큐브에 있는 Internet Sales 측정값 그룹의 모든 파티션에서 <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체를 만듭니다.  
  
```  
static public void SetProactiveCachingSettings(Database db)  
{  
    ProactiveCaching pc;  
    if (db.Cubes.ContainsName("Adventure Works") && db.Cubes.FindByName("Adventure Works").MeasureGroups.ContainsName("Internet Sales"))  
    {  
        ProactiveCachingTablesBinding pctb;  
        TableNotification tn;  
  
        MeasureGroup mg = db.Cubes.FindByName("Adventure Works").MeasureGroups.FindByName("Internet Sales");  
        foreach(Partition part in mg.Partitions)  
        {  
            pc = new ProactiveCaching();  
            pc.AggregationStorage = ProactiveCachingAggregationStorage.MolapOnly;  
            pc.SilenceInterval = TimeSpan.FromSeconds(10);  
            pc.Latency = TimeSpan.FromSeconds(-1);  
            pc.SilenceOverrideInterval = TimeSpan.FromMinutes(10);  
            pc.ForceRebuildInterval = TimeSpan.FromSeconds(-1);  
            pc.Enabled = true;  
            pc.OnlineMode = ProactiveCachingOnlineMode.OnCacheComplete;  
            pctb = new ProactiveCachingTablesBinding();  
            pctb.NotificationTechnique = NotificationTechnique.Server;  
            tn = new TableNotification("[FactInternetSales]", "dbo");  
            pctb.TableNotifications.Add( tn);  
            pc.Source = pctb;  
  
            part.ProactiveCaching = pc;  
            part.Update();  
        }  
    }  
}  
```  
  
##  <a name="Transl"></a> 번역 개체  
 번역 개체는 AMO를 사용하여 정의될 수 있지만 데이터를 탐색하는 클라이언트 응용 프로그램에서 사용됩니다. 번역 개체는 코드를 작성할 수 있는 단순 개체입니다. 개체 캡션에 대한 번역은 로캘 ID 및 번역된 캡션 쌍으로 제공됩니다. 캡션에는 여러 번역을 사용할 수 있습니다. 번역은 차원, 특성, 계층, 큐브, 측정값 그룹, 측정값 등의 대부분의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체에 제공될 수 있습니다.  
  
 다음 코드 예제에서는 Product Name 특성의 이름에 대한 스페인어 번역을 제공합니다.  
  
```  
static public void CreateTranslations(Database db)  
{  
    //Spanish Tranlations for Product Category in Product Dimension  
    Dimension dim = db.Dimensions["Product"];  
    DimensionAttribute atr = dim.Attributes["Product Name"];  
    Translation tran = atr.Translations.Add(3082);  
    tran.Caption = "Nombre Producto";  
  
    dim.Update(UpdateOptions.ExpandFull);  
  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices>   
 [AMO 클래스 소개](amo-classes-introduction.md)   
 [AMO OLAP 클래스](amo-olap-classes.md)   
 [논리적 아키텍처 &#40;Analysis Services-다차원 데이터&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [데이터베이스 개체 &#40;Analysis Services-다차원 데이터&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [다차원 모델 개체 처리](../processing-a-multidimensional-model-analysis-services.md)  
  
  