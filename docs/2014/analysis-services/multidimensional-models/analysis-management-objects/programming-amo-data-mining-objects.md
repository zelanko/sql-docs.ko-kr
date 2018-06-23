---
title: AMO 데이터 마이닝 개체 프로그래밍 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
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
- data mining [AMO]
- AMO, data mining
- Analysis Management Objects, data mining
ms.assetid: d27f58b9-91be-449c-8403-439aa6dd1ff9
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 62ef444d7fa112267a4a272553834e24fe5b0df9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181452"
---
# <a name="programming-amo-data-mining-objects"></a>AMO 데이터 마이닝 개체 프로그래밍
  AMO를 사용하여 데이터 마이닝 개체를 프로그래밍하는 과정은 매우 간단합니다. 첫 번째 단계는 마이닝 프로젝트를 지원하는 데이터 구조 모델을 만드는 것입니다. 그런 다음 데이터 내부의 보이지 않는 관계를 예측하거나 찾는 데 사용할 마이닝 알고리즘을 지원하는 데이터 마이닝 모델을 만듭니다. 구조 및 알고리즘을 포함하여 만든 마이닝 프로젝트를 통해 마이닝 모델을 처리하여 나중에 클라이언트 응용 프로그램에서 쿼리 또는 예측하는 데 사용하는 학습된 모델을 얻을 수 있습니다.  
  
 한 가지 기억할 것은 AMO의 목적은 쿼리가 아니라 마이닝 구조 및 모델 관리라는 점입니다. 사용 데이터를 쿼리하려면 [ADOMD.NET을 사용 하 여 개발](../adomd-net/developing-with-adomd-net.md)합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [MiningStructure 개체](#MiningStructure)  
  
-   [MiningModel 개체](#MiningModel)  
  
##  <a name="MiningStructure"></a> MiningStructure 개체  
 마이닝 구조는 모든 마이닝 모델을 만드는 데 사용되는 데이터 구조의 정의입니다. 마이닝 구조에는 데이터베이스에 정의된 데이터 원본 뷰에 대한 바인딩이 포함되며 마이닝 모델에 참여하는 모든 열에 대한 정의가 포함됩니다. 하나의 마이닝 구조에서 둘 이상의 마이닝 모델을 가질 수 있습니다.  
  
 <xref:Microsoft.AnalysisServices.MiningStructure> 개체를 만들려면 다음 단계를 수행합니다.  
  
1.  <xref:Microsoft.AnalysisServices.MiningStructure> 개체를 만들고 기본 특성을 채웁니다. 기본 특성에는 개체 이름, 개체 ID(내부 식별) 및 데이터 원본 바인딩이 있습니다.  
  
2.  모델에 대한 열을 만듭니다. 열은 스칼라 또는 테이블 정의가 될 수 있습니다.  
  
     각 열에는 이름 및 내부 ID, 형식, 내용 정의 및 바인딩이 필요합니다.  
  
3.  개체의 Update 메서드를 사용하여 <xref:Microsoft.AnalysisServices.MiningStructure> 개체를 서버로 업데이트합니다.  
  
     마이닝 구조는 처리될 수 있으며 마이닝 구조가 처리될 때 자식 마이닝 모델이 처리되거나 유지됩니다.  
  
 다음 코드 예제에서는 시계열로 판매량을 예측하는 마이닝 구조를 만듭니다. 샘플 코드를 실행 하기 전에 있는지 확인 하는 데이터베이스 *db*에 대 한 매개 변수로 전달 된, `CreateSalesForecastingMiningStructure`에 포함 된 `db.DataSourceViews[0]` 보기에 대 한 참조 *dbo.vTimeSeries* 는 에서[!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)]예제 데이터베이스.  
  
```  
public static MiningStructure CreateSalesForecastingMiningStructure(Database db)  
{  
    MiningStructure ms = db.MiningStructures.FindByName("Forecasting Sales Structure");  
    if (ms != null)  
        ms.Drop();  
    ms = db.MiningStructures.Add("Forecasting Sales Structure", "Forecasting Sales Structure");  
    ms.Source = new DataSourceViewBinding(db.DataSourceViews[0].ID);  
  
    ScalarMiningStructureColumn amount = ms.Columns.Add("Amount", "Amount");  
    amount.Type = MiningStructureColumnTypes.Double;  
    amount.Content = MiningStructureColumnContents.Continuous;  
    amount.KeyColumns.Add("vTimeSeries", "Amount", OleDbType.Currency);  
  
    ScalarMiningStructureColumn modelRegion = ms.Columns.Add("Model Region", "Model Region");  
    modelRegion.IsKey = true;  
    modelRegion.Type = MiningStructureColumnTypes.Text;  
    modelRegion.Content = MiningStructureColumnContents.Key;  
    modelRegion.KeyColumns.Add("vTimeSeries", "ModelRegion", OleDbType.WChar, 56);  
  
    ScalarMiningStructureColumn qty = ms.Columns.Add("Quantity", "Quantity");  
    qty.Type = MiningStructureColumnTypes.Long;  
    qty.Content = MiningStructureColumnContents.Continuous;  
    qty.KeyColumns.Add("vTimeSeries", "Quantity", OleDbType.Integer);  
  
    ScalarMiningStructureColumn timeIndex = ms.Columns.Add("TimeIndex", "TimeIndex");  
    timeIndex.IsKey = true;  
    timeIndex.Type = MiningStructureColumnTypes.Long;  
    timeIndex.Content = MiningStructureColumnContents.KeyTime;  
    timeIndex.KeyColumns.Add("vTimeSeries", "TimeIndex", OleDbType.Integer);  
  
    ms.Update();  
    return ms;  
}  
```  
  
##  <a name="MiningModel"></a> MiningModel 개체  
 마이닝 모델은 마이닝 알고리즘에 사용되는 모든 열과 열 정의에 대한 저장소입니다.  
  
 <xref:Microsoft.AnalysisServices.MiningModel> 개체를 만들려면 다음 단계를 수행합니다.  
  
1.  <xref:Microsoft.AnalysisServices.MiningModel> 개체를 만들고 기본 특성을 채웁니다.  
  
     기본 특성에는 개체 이름, 개체 ID(내부 식별) 및 마이닝 알고리즘 사양이 있습니다.  
  
2.  마이닝 모델의 열을 추가합니다. 열 중 하나는 사례 키로 정의되어야 합니다.  
  
3.  개체의 Update 메서드를 사용하여 <xref:Microsoft.AnalysisServices.MiningModel> 개체를 서버로 업데이트합니다.  
  
     <xref:Microsoft.AnalysisServices.MiningModel> 개체는 부모 <xref:Microsoft.AnalysisServices.MiningStructure>의 다른 모델과 별개로 처리할 수 있습니다.  
  
 다음 코드 예제에서는 "Forecasting Sales Structure" 마이닝 구조를 기반으로 Microsoft 시계열 예측 모델을 만듭니다.  
  
```  
public static MiningModel CreateSalesForecastingMiningModel(MiningStructure ms)  
{  
    if (ms.MiningModels.ContainsName("Sales Forecasting Model"))  
    {  
        ms.MiningModels["Sales Forecasting Model"].Drop();  
    }  
    MiningModel mm = ms.CreateMiningModel(true, "Sales Forecasting Model");  
    mm.Algorithm = MiningModelAlgorithms.MicrosoftTimeSeries;  
    mm.AlgorithmParameters.Add("PERIODICITY_HINT", "{12}");  
  
    MiningModelColumn amount = new MiningModelColumn();  
    amount.SourceColumnID = "Amount";  
    amount.Usage = MiningModelColumnUsages.Predict;  
  
    MiningModelColumn modelRegion = new MiningModelColumn();  
    modelRegion.SourceColumnID = "Model Region";  
    modelRegion.Usage = MiningModelColumnUsages.Key;  
  
    MiningModelColumn qty = new MiningModelColumn();  
    qty.SourceColumnID = "Quantity";  
    qty.Usage = MiningModelColumnUsages.Predict;  
  
    MiningModelColumn ti = new MiningModelColumn();  
    ti.SourceColumnID = "TimeIndex";  
    ti.Usage = MiningModelColumnUsages.Key;  
  
    mm.Update();  
    mm.Process(ProcessType.ProcessFull);  
    return mm;  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices>   
 [AMO 기본 클래스](amo-fundamental-classes.md)   
 [AMO 클래스 소개](amo-classes-introduction.md)   
 [AMO 데이터 마이닝 클래스](amo-data-mining-classes.md)   
 [논리적 아키텍처 &#40;Analysis Services-다차원 데이터&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [데이터베이스 개체 &#40;Analysis Services-다차원 데이터&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  