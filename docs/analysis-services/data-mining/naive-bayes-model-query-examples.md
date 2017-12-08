---
title: "Naive Bayes 모델 쿼리 예제 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- naive bayes model [Analysis Services]
- naive bayes algorithms [Analysis Services]
- content queries [DMX]
ms.assetid: e642bd7d-5afa-4dfb-8cca-4f84aadf61b0
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 622eaa381d4507cb75d66a93916743af40e73932
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="naive-bayes-model-query-examples"></a>Naive Bayes 모델 쿼리 예제
  데이터 마이닝 모델에 대한 쿼리를 작성할 때 분석 중에 발견된 패턴에 대한 세부 정보를 제공하는 내용 쿼리를 작성하거나, 모델의 패턴을 사용하여 새 데이터에 대한 예측을 만드는 예측 쿼리를 작성할 수 있습니다. 데이터 마이닝 스키마 행 집합에 대한 쿼리를 사용하여 모델에 대한 메타데이터를 검색할 수도 있습니다. 이 섹션에서는 Microsoft Naive Bayes 알고리즘을 기반으로 하는 모델에 대해 이러한 쿼리를 만드는 방법을 설명합니다.  
  
 **내용 쿼리**  
  
 [DMX를 사용하여 모델 메타데이터 가져오기](#bkmk_Query1)  
  
 [학습 데이터의 요약 검색](#bkmk_Query2)  
  
 [특성에 대한 추가 정보 찾기](#bkmk_Query3)  
  
 [시스템 저장 프로시저 사용](#bkmk_Query4)  
  
 **예측 쿼리**  
  
 [단일 쿼리를 사용하여 결과 예측](#bkmk_Query5)  
  
 [확률 및 지지도 값과 함께 예측 가져오기](#bkmk_Query6)  
  
 [연결 예측](#bkmk_Query7)  
  
## <a name="finding-information-about-a-naive-bayes-model"></a>Naive Bayes 모델에 대한 정보 찾기  
 Naive Bayes 모델의 모델 콘텐츠는 학습 데이터의 값 분포에 대한 집계 정보를 제공합니다. 데이터 마이닝 스키마 행 집합에 대한 쿼리를 만들어 모델의 메타데이터에 대한 정보를 검색할 수도 있습니다.  
  
###  <a name="bkmk_Query1"></a> 예제 쿼리 1: DMX를 사용하여 모델 메타데이터 가져오기  
 데이터 마이닝 스키마 행 집합을 쿼리하면 모델에 대한 메타데이터를 찾을 수 있습니다. 이러한 메타데이터로는 모델이 만들어진 시기, 모델이 마지막으로 처리된 시기, 모델의 기반이 되는 마이닝 구조의 이름, 예측 가능한 특성으로 사용된 열 이름 등이 포함됩니다. 모델을 만들 때 사용된 매개 변수를 반환할 수도 있습니다.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, DATE_CREATED, LAST_PROCESSED,  
SERVICE_NAME, PREDICTION_ENTITY, FILTER  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_NaiveBayes_Filtered'  
```  
  
 예제 결과:  
  
|||  
|-|-|  
|MODEL_CATALOG|AdventureWorks|  
|MODEL_NAME|TM_NaiveBayes_Filtered|  
|DATE_CREATED|3/1/2008 19:15|  
|LAST_PROCESSED|3/2/2008 20:00|  
|SERVICE_NAME|Microsoft_Naive_Bayes|  
|PREDICTION_ENTITY|Bike Buyer,Yearly Income|  
|FILTER|[Region] = 'Europe' OR [Region] = 'North America'|  
  
 이 예에 사용된 모델은 [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)에서 만드는 Naive Bayes 모델을 기반으로 하되 여기에 두 번째 예측 가능한 특성을 추가하고 학습 데이터에 필터를 적용하여 수정한 것입니다.  
  
###  <a name="bkmk_Query2"></a> 예제 쿼리 2: 학습 데이터의 요약 검색  
 Naive Bayes 모델에서 한계 통계 노드에는 학습 데이터의 값 분포에 대한 집계 정보가 저장됩니다. 따라서 이와 같은 요약 정보를 찾기 위해 학습 데이터에 대한 SQL 쿼리를 만들지 않아도 되므로 편리합니다.  
  
 다음 예에서는 DMX 내용 쿼리를 사용하여 노드(NODE_TYPE = 24)에서 데이터를 검색합니다. 통계는 중첩 테이블에 저장되어 있으므로 결과를 보기 쉽게 만들기 위해 FLATTENED 키워드가 사용됩니다.  
  
```  
SELECT FLATTENED MODEL_NAME,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT], [PROBABILITY], VALUETYPE FROM NODE_DISTRIBUTION) AS t  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
> [!NOTE]  
>  SUPPORT 및 PROBABILITY 열의 이름을 대괄호로 묶어 동일한 이름의 MDX(Multidimensional Expressions) 예약 키워드와 구별해야 합니다.  
  
 일부 결과:  
  
|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|0|1.|  
|TM_NaiveBayes|Bike Buyer|0|8869|0.507263784|4|  
|TM_NaiveBayes|Bike Buyer|1.|8615|0.492736216|4|  
|TM_NaiveBayes|Gender|Missing|0|0|1.|  
|TM_NaiveBayes|Gender|F|8656|0.495081217|4|  
|TM_NaiveBayes|Gender|M|8828|0.504918783|4|  
  
 예를 들어 이러한 결과는 누락 값(VALUETYPE = 1)에 대해 조정된 계산된 확률과 함께 각 불연속 값(VALUETYPE = 4)의 학습 사례 수를 나타냅니다.  
  
 Naive Bayes 모델의 NODE_DISTRIBUTION 테이블에 제공되는 값에 대한 정의는 [Naive Bayes 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)를 참조하세요. 누락 값이 지지도 및 확률 계산에 주는 영향에 대한 자세한 내용은 [누락 값&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)을 참조하세요.  
  
###  <a name="bkmk_Query3"></a> 예제 쿼리 3: 특성에 대한 추가 정보 찾기  
 Naive Bayes 모델에는 서로 다른 특성 간의 관계에 대한 복잡한 정보가 들어 있는 경우도 있으므로 이러한 관계를 가장 쉽게 보는 방법은 [Microsoft Naive Bayes 뷰어](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)를 사용하는 것입니다. 그러나 DMX 쿼리를 만들어 데이터를 반환할 수도 있습니다.  
  
 다음 예에서는 모델에서 특정 특성 `Region`에 대한 정보를 반환하는 방법을 보여 줍니다.  
  
```  
SELECT NODE_TYPE, NODE_CAPTION,   
NODE_PROBABILITY, NODE_SUPPORT, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE ATTRIBUTE_NAME = 'Region'  
```  
  
 이 쿼리는 두 가지 유형의 노드를 반환합니다. 한 노드(NODE_TYPE = 10)는 입력 특성을 나타내고 다른 노드(NODE_TYPE = 11)는 특성의 각 값에 대한 노드입니다. 노드 캡션에는 특성 이름과 특성 값이 모두 표시되므로 노드 이름 대신 노드 캡션이 노드를 식별하는 데 사용됩니다.  
  
|NODE_TYPE|NODE_CAPTION|NODE_PROBABILITY|NODE_SUPPORT|MSOLAP_NODE_SCORE|NODE_TYPE|  
|----------------|-------------------|-----------------------|-------------------|-------------------------|----------------|  
|10|Bike Buyer -> Region|1.|17484|84.51555875|10|  
|11|Bike Buyer -> Region = Missing|0|0|0|11|  
|11|Bike Buyer -> Region = North America|0.508236102|8886|0|11|  
|11|Bike Buyer -> Region = Pacific|0.193891558|3390|0|11|  
|11|Bike Buyer -> Region = Europe|0.29787234|5208|0|11|  
  
 노드에 저장된 노드 확률 점수 및 노드 지지도 값 등의 일부 열은 한계 통계 노드에서 가져올 수 있는 것과 동일합니다. 그러나 MSOLAP_NODE_SCORE는 입력 특성 노드에 대해서만 제공되는 특수 값이며 모델에서 이 특성의 상대적 중요도를 나타냅니다. 뷰어의 종속성 네트워크 창에서도 동일한 정보를 볼 수 있지만 뷰어에는 점수가 표시되지 않습니다.  
  
 다음 쿼리는 모델에 있는 모든 특성의 중요도 점수를 반환합니다.  
  
```  
SELECT NODE_CAPTION, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 10  
ORDER BY MSOLAP_NODE_SCORE DESC  
```  
  
 예제 결과:  
  
|NODE_CAPTION|MSOLAP_NODE_SCORE|  
|-------------------|-------------------------|  
|Bike Buyer -> Total Children|181.3654836|  
|Bike Buyer -> Commute Distance|179.8419482|  
|Bike Buyer -> English Education|156.9841928|  
|Bike Buyer -> Number Children At Home|111.8122599|  
|Bike Buyer -> Region|84.51555875|  
|Bike Buyer -> Marital Status|23.13297354|  
|Bike Buyer -> English Occupation|2.832069191|  
  
 [Microsoft 일반 콘텐츠 트리 뷰어](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)에서 모델 콘텐츠를 찾아보면 주목할 만한 통계를 보다 잘 확인할 수 있습니다. 여기에서는 몇 개의 간단한 예를 보여 주지만 여러 쿼리를 실행하거나 결과를 저장하고 클라이언트에서 처리해야 하는 경우는 보다 많이 있습니다.  
  
###  <a name="bkmk_Query4"></a> 예제 쿼리 4: 시스템 저장 프로시저 사용  
 사용자가 직접 내용 쿼리를 작성할 수 있을 뿐 아니라 몇 가지 Analysis Services 시스템 저장 프로시저를 사용하여 결과를 탐색할 수도 있습니다. 시스템 저장 프로시저를 사용하려면 저장 프로시저 이름 앞에 CALL 키워드를 붙입니다.  
  
```  
CALL GetPredictableAttributes ('TM_NaiveBayes')  
```  
  
 일부 결과:  
  
|ATTRIBUTE_NAME|NODE_UNIQUE_NAME|  
|---------------------|------------------------|  
|Bike Buyer|100000001|  
  
> [!NOTE]  
>  이러한 시스템 저장 프로시저는 Analysis Services 서버와 클라이언트 간의 내부 통신을 위한 것으로서, 마이닝 모델을 개발하고 테스트할 때 편의를 위해서만 사용해야 합니다. 프로덕션 시스템에 대한 쿼리를 만들 때는 항상 DMX를 사용하여 사용자가 직접 쿼리를 작성해야 합니다.  
  
 Analysis Services 시스템 저장 프로시저에 대한 자세한 내용은 [데이터 마이닝 저장 프로시저&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md)를 참조하세요.  
  
## <a name="using-a-naive-bayes-model-to-make-predictions"></a>Naive Bayes 모델을 사용하여 예측 만들기  
 Microsoft Naive Bayes 알고리즘은 일반적으로 예측에 사용되는 경우보다 입력 및 예측 가능한 특성 간의 관계를 탐색하는 데 사용되는 경우가 더 많습니다. 그러나 이 모델에서는 예측 및 연결 모두에 대해 예측 함수를 사용할 수 있습니다.  
  
###  <a name="bkmk_Query5"></a> 예제 쿼리 5: 단일 쿼리를 사용하여 결과 예측  
 다음 쿼리에서는 단일 쿼리를 사용하여 새 값을 제공하고 모델을 기반으로 해당 특성을 갖는 고객이 자전거를 구입할 가능성이 있는지를 예측합니다. 회귀 모델에서 단일 쿼리를 만드는 가장 쉬운 방법은 **단일 쿼리 입력** 대화 상자를 사용하는 것입니다. 예를 들어 `TM_NaiveBayes` 모델을 선택하고 **단일 쿼리**를 선택한 다음 드롭다운 목록에서 `[Commute Distance]` 및 `Gender`의 값을 선택하여 다음과 같은 DMX 쿼리를 작성할 수 있습니다.  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 예제 결과:  
  
|식|  
|----------------|  
|0|  
  
 이 예측 함수는 가장 가능성이 높은 값(이 경우 0)을 반환합니다. 이 값은 이 유형의 고객이 자전거를 구입할 가능성이 없다는 것을 의미합니다.  
  
###  <a name="bkmk_Query6"></a> 예제 쿼리 6: 확률 및 지지도 값과 함께 예측 가져오기  
 결과를 예측하는 것 외에도 예측의 정확도를 알고 싶은 경우가 있습니다. 다음 쿼리에서는 앞의 예와 동일한 단일 쿼리를 사용하되 예측 함수 [PredictHistogram&#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)을 추가하여 해당 예측을 지원하는 통계가 들어 있는 중첩 테이블을 반환합니다.  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer]),  
  PredictHistogram([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 예제 결과:  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|0|10161.5714|0.581192599|0.010530981|0|0|  
|1.|7321.428768|0.418750215|0.008945684|0|0|  
||0.999828444|5.72E-05|5.72E-05|0|0|  
  
 표의 마지막 행에서는 누락 값의 지지도 및 확률에 대한 조정을 보여 줍니다. 분산 및 표준 편차 값은 항상 0이지만 Naive Bayes 모델에서는 연속 값을 모델링할 수 없습니다.  
  
###  <a name="bkmk_Query7"></a> 예제 쿼리 7: 연결 예측  
 마이닝 구조에 예측 가능한 특성을 키로 사용하는 중첩 테이블이 들어 있는 경우 연결 분석에 Microsoft Naive Bayes 알고리즘을 사용할 수 있습니다. 예를 들어 데이터 마이닝 자습서의 [3단원: 시장 바구니 시나리오 구축&#40;중급 데이터 마이닝 자습서&#41;](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a)에서 만든 마이닝 구조를 사용하여 Naive Bayes 모델을 작성할 수 있습니다. 이 예에 사용된 모델을 수정하여 사례 테이블에 수입 및 고객 지역에 대한 정보를 추가했습니다.  
  
 다음 쿼리 예에서는 `'Road Tire Tube'`제품의 구매와 관련된 제품을 예측하는 단일 쿼리를 보여 줍니다. 이 정보를 사용하여 특정 유형의 고객에게 제품을 추천할 수 있습니다.  
  
```  
SELECT   PredictAssociation([Association].[v Assoc Seq Line Items])  
FROM [Association_NB]  
NATURAL PREDICTION JOIN  
(SELECT 'High' AS [Income Group],  
  'Europe' AS [Region],  
  (SELECT 'Road Tire Tube' AS [Model])   
AS [v Assoc Seq Line Items])   
AS t  
```  
  
 일부 결과:  
  
|Model|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
|Touring-2000|  
|Touring-1000|  
  
## <a name="function-list"></a>함수 목록  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘은 공통 함수 집합을 지원합니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 알고리즘은 다음 표에 나열된 추가 함수도 지원합니다.  
  
|||  
|-|-|  
|예측 함수|사용법|  
|[IsDescendant&#40;DMX&#41;](../../dmx/isdescendant-dmx.md)|한 노드가 모델에서 다른 노드의 자식인지 여부를 확인합니다.|  
|[예측&#40;DMX&#41;](../../dmx/predict-dmx.md)|지정한 열에 대한 예측 값을 반환합니다.|  
|[PredictAdjustedProbability&#40;DMX&#41;](../../dmx/predictadjustedprobability-dmx.md)|가중치 확률을 반환합니다.|  
|[PredictAssociation&#40;DMX&#41;](../../dmx/predictassociation-dmx.md)|연관 데이터 집합에서의 멤버 자격을 예측합니다.|  
|[PredictNodeId&#40;DMX&#41;](../../dmx/predictnodeid-dmx.md)|각 사례에 대한 Node_ID를 반환합니다.|  
|[PredictProbability&#40;DMX&#41;](../../dmx/predictprobability-dmx.md)|예측 값의 확률을 반환합니다.|  
|[PredictSupport&#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|지정한 상태에 대한 지원 값을 반환합니다.|  
  
 특정 함수의 구문을 보려면 [DMX&#40;Data Mining Extensions&#41; 함수 참조](../../dmx/data-mining-extensions-dmx-function-reference.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft Naive Bayes 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)   
 [Microsoft Naive Bayes Algorithm](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)   
 [Naive Bayes 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  
