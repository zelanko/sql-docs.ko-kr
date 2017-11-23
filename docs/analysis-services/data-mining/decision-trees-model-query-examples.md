---
title: "의사 결정 트리 모델 쿼리 예제 | Microsoft Docs"
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
- decision tree algorithms [Analysis Services]
- content queries [DMX]
- decision trees [Analysis Services]
ms.assetid: ceaf1370-9dd1-4d1a-a143-7f89a723ef80
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b1b441eb4718e5f362fb1ef6f6a3a889cf5dc812
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="decision-trees-model-query-examples"></a>의사 결정 트리 모델 쿼리 예제
  데이터 마이닝 모델에 대한 쿼리를 만들 때 분석 중에 발견된 패턴에 대한 세부 정보를 제공하는 내용 쿼리를 만들거나, 모델의 패턴을 사용하여 새 데이터에 대한 예측을 수행하는 예측 쿼리를 만들 수 있습니다. 예를 들어 의사 결정 트리 모델에 대한 내용 쿼리는 각 트리 수준의 사례 수에 대한 통계를 제공하거나 사례를 구분하는 규칙을 제공할 수 있습니다. 또한 예측 쿼리는 권장 사항, 분류 등을 생성하기 위해 모델을 새 데이터에 매핑합니다. 쿼리를 사용하여 모델에 대한 메타데이터를 검색할 수도 있습니다.  
  
 이 섹션에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘을 기반으로 하는 모델에 대한 쿼리를 만드는 방법에 대해 설명합니다.  
  
 **내용 쿼리**  
  
 [데이터 마이닝 스키마 행 집합에서 모델 매개 변수 검색](#bkmk_Query1)  
  
 [DMX를 사용하여 모델의 트리에 대한 정보 가져오기](#bkmk_Query2)  
  
 [모델에서 하위 트리 검색](#bkmk_Query3)  
  
 **예측 쿼리**  
  
 [예측 및 확률 반환](#bkmk_Query4)  
  
 [의사 결정 트리 모델에서 연결 예측](#bkmk_Query5)  
  
 [의사 결정 트리 모델에서 회귀 수식 검색](#bkmk_Query6)  
  
##  <a name="bkmk_top2"></a> 의사 결정 트리 모델에 대한 정보 찾기  
 의사 결정 트리 모델의 내용에 대한 의미 있는 쿼리를 만들려면 모델 내용의 구조와 노드 유형에 따라 저장되는 정보의 종류를 이해해야 합니다. 자세한 내용은 [의사 결정 트리 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)를 참조하세요.  
  
###  <a name="bkmk_Query1"></a> 예제 쿼리 1: 데이터 마이닝 스키마 행 집합에서 모델 매개 변수 검색  
 데이터 마이닝 스키마 행 집합을 쿼리하면 모델이 만들어진 날짜, 모델이 마지막으로 처리된 날짜, 모델의 기반이 되는 마이닝 구조의 이름, 예측 가능한 특성으로 사용된 열 이름 등 모델에 대한 메타데이터를 찾을 수 있습니다. 모델을 처음으로 만들 때 사용한 매개 변수를 반환할 수도 있습니다.  
  
```  
select MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Decision Tree'  
```  
  
 예제 결과:  
  
 MINING_PARAMETERS  
  
 COMPLEXITY_PENALTY=0.5, MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_OUTPUT_ATTRIBUTES=255,MINIMUM_SUPPORT=10,SCORE_METHOD=4,SPLIT_METHOD=3,FORCE_REGRESSOR=  
  
###  <a name="bkmk_Query2"></a> 예제 쿼리 2: DMX를 사용하여 모델 내용에 대한 정보 반환  
 다음 쿼리는 [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)에서 모델을 작성할 때 만들어진 의사 결정 트리에 대한 몇 가지 기본 정보를 반환합니다. 각 트리 구조는 자체 노드에 저장됩니다. 이 모델에는 예측 가능한 특성이 하나이므로 트리 노드가 한 개뿐입니다. 그러나 의사 결정 트리 알고리즘을 사용하여 연결 모델을 만드는 경우 각 제품에 대해 하나씩 수백 개의 트리가 있을 수 있습니다.  
  
 이 쿼리는 예측 가능한 특정 특성을 나타내는 최상위 트리 노드인 유형 2 노드를 모두 반환합니다.  
  
> [!NOTE]  
>  열 CHILDREN_CARDINALITY는 대괄호로 묶어 동일한 이름의 MDX 예약 키워드와 구분해야 합니다.  
  
```  
SELECT MODEL_NAME, NODE_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY]  
FROM TM_DecisionTrees.CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 예제 결과:  
  
|MODEL_NAME|NODE_NAME|NODE_CAPTION|NODE_SUPPORT|CHILDREN_CARDINALITY|  
|-----------------|----------------|-------------------|-------------------|---------------------------|  
|TM_DecisionTree|000000001|모두|12939|5|  
  
 이러한 결과의 의미는 무엇입니까? 의사 결정 트리 모델에서 특정 노드의 카디널리티를 보면 해당 노드의 직접 자식 수를 알 수 있습니다. 이 노드의 카디널리티는 5이므로 모델에서 잠재적 자전거 구매자의 대상 모집단이 5개의 하위 그룹으로 나뉘었음을 알 수 있습니다.  
  
 다음 관련 쿼리는 이러한 5개 하위 그룹의 자식을 자식 노드의 특성 및 값 분포와 함께 반환합니다. 지지도, 확률 및 분산과 같은 통계는 중첩 테이블 NODE_DISTRIBUTION에 저장되므로 이 예에서는 `FLATTENED` 키워드를 사용하여 중첩 테이블 열을 출력합니다.  
  
> [!NOTE]  
>  중첩 테이블 열 SUPPORT는 대괄호로 묶어 동일한 이름의 예약 키워드와 구분해야 합니다.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT]  
FROM NODE_DISTRIBUTION) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE [PARENT_UNIQUE_NAME] = '000000001'  
```  
  
 예제 결과:  
  
|NODE_NAME|NODE_CAPTION|T.ATTRIBUTE_NAME|T.ATTRIBUTE_VALUE|SUPPORT|  
|----------------|-------------------|-----------------------|------------------------|-------------|  
|00000000100|Number Cars Owned = 0|Bike Buyer|Missing|0|  
|00000000100|Number Cars Owned = 0|Bike Buyer|0|1067|  
|00000000100|Number Cars Owned = 0|Bike Buyer|1|1875|  
|00000000101|Number Cars Owned = 3|Bike Buyer|Missing|0|  
|00000000101|Number Cars Owned = 3|Bike Buyer|0|678|  
|00000000101|Number Cars Owned = 3|Bike Buyer|1|473|  
  
 이러한 결과를 통해 자전거를 구입한 고객([Bike Buyer] = 1) 중 1067명이 차량을 소유하지 않았으며 473명은 3대의 차량을 소유했다는 것을 알 수 있습니다.  
  
###  <a name="bkmk_Query3"></a> 예제 쿼리 3: 모델에서 하위 트리 검색  
 자전거를 구입한 고객에 대한 추가 정보를 검색한다고 가정합니다. 다음 예와 같이 쿼리에 [IsDescendant&#40;DMX&#41;](../../dmx/isdescendant-dmx.md) 함수를 사용하여 하위 트리에 대한 추가 세부 정보를 볼 수 있습니다. 이 쿼리는 트리에서 42세 이상인 고객을 포함하는 리프 노드(NODE_TYPE = 4)를 검색하여 자전거 구매자 수를 반환합니다. 이 쿼리는 중첩 테이블의 행을 Bike Buyer = 1인 행으로 제한합니다.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,NODE_TYPE,  
(  
SELECT [SUPPORT] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Bike Buyer' AND ATTRIBUTE_VALUE = '1'  
) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE ISDESCENDANT('0000000010001')  
AND NODE_TYPE = 4  
```  
  
 예제 결과:  
  
|NODE_NAME|NODE_CAPTION|t.SUPPORT|  
|----------------|-------------------|---------------|  
|000000001000100|Yearly Income >= 26000 and < 42000|266|  
|00000000100010100|Total Children = 3|75|  
|0000000010001010100|Number Children At Home = 1|75|  
  
## <a name="making-predictions-using-a-decision-trees-model"></a>의사 결정 트리 모델을 사용하여 예측 수행  
 의사 결정 트리는 분류, 회귀, 연결 등과 같은 다양한 태스크에 사용할 수 있으므로 의사 결정 트리 모델에 대한 예측 쿼리를 작성할 때 많은 옵션을 사용할 수 있습니다. 예측 결과를 이해하려면 모델을 만든 용도를 알아야 합니다. 다음 쿼리 예제에서는 3가지 다른 시나리오를 보여 줍니다.  
  
-   분류 모델에 대한 예측을 예측이 정확할 확률과 함께 반환한 다음 확률별로 결과 필터링  
  
-   단일 쿼리를 만들어 연결 예측  
  
-   의사 결정 트리에서 입력과 출력 간의 관계가 선형인 부분에 대한 회귀 수식 검색  
  
###  <a name="bkmk_Query4"></a> 예제 쿼리 4: 예측 및 확률 반환  
 다음 예제 쿼리에서는 [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)에서 만든 의사 결정 트리 모델을 사용하고 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW의 dbo.ProspectiveBuyers 테이블에서 예제 데이터의 새 집합을 전달하여 새 데이터 집합의 고객 중 자전거를 구입할 가능성이 있는 고객을 예측합니다.  
  
 이 쿼리에서는 모델에서 발견한 확률에 대한 유용한 정보를 포함하는 중첩 테이블을 반환하는 예측 함수 [PredictHistogram&#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)을 사용합니다. 쿼리의 최종 WHERE 절은 결과를 필터링하여 자전거를 구매할 가능성이 있는 것으로 예측된 고객, 즉 확률이 0%를 초과하는 고객만 반환합니다.  
  
```  
SELECT  
  [TM_DecisionTree].[Bike Buyer],  
  PredictHistogram([Bike Buyer]) as Results  
From  
  [TM_DecisionTree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [FirstName],  
      [LastName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM_DecisionTree].[First Name] = t.[FirstName] AND  
  [TM_DecisionTree].[Last Name] = t.[LastName] AND  
  [TM_DecisionTree].[Marital Status] = t.[MaritalStatus] AND  
  [TM_DecisionTree].[Gender] = t.[Gender] AND  
  [TM_DecisionTree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM_DecisionTree].[Total Children] = t.[TotalChildren] AND  
  [TM_DecisionTree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM_DecisionTree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM_DecisionTree].[Number Cars Owned] = t.[NumberCarsOwned]  
WHERE [Bike Buyer] = 1  
AND PredictProbability([Bike Buyer]) >'.05'  
```  
  
 기본적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 열 레이블 **Expression**을 사용하여 중첩 테이블을 반환합니다. 반환되는 열에 별칭을 지정하여 이 레이블을 변경할 수 있습니다. 이렇게 하면 별칭(이 경우 **Results**)이 열 제목과 중첩 테이블의 값 모두로 사용됩니다. 결과를 보려면 중첩 테이블을 확장해야 합니다.  
  
 예제 결과 **Bike Buyer** = 1:  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|1|2540|0.634849242045644|0.013562168281562|0|0|  
|0|1460|0.364984174579377|0.00661336932550915|0|0|  
||0|0.000166583374979177|0.000166583374979177|0|0|  
  
 공급자가 여기에 표시된 것과 같은 계층적 행 집합을 지원하지 않는 경우 쿼리에 FLATTENED 키워드를 사용하여 반복되는 열 값 대신 Null을 포함하는 테이블로 결과를 반환할 수 있습니다. 자세한 내용은 [중첩 테이블&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md) 또는 [DMX Select 문 이해](../../dmx/understanding-the-dmx-select-statement.md)를 참조하세요.  
  
###  <a name="bkmk_Query5"></a> 예제 쿼리 5: 의사 결정 트리 모델에서 연결 예측  
 다음 예제 쿼리는 Association 마이닝 구조를 기반으로 합니다. 이 예제의 단계별 작업을 따라가려면 이 마이닝 구조에 새 모델을 추가하고 Microsoft 의사 결정 트리를 알고리즘으로 선택합니다. 연결 마이닝 구조를 만드는 방법은 [3단원: 시장 바구니 시나리오 구축&#40;중급 데이터 마이닝 자습서&#41;](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a)을 참조하세요.  
  
 다음 예제 쿼리는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 필드를 선택한 다음 드롭다운 목록에서 이러한 필드의 값을 선택하여 간단하게 만들 수 있는 단일 쿼리입니다.  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
FROM  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Patch kit' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 예상 결과:  
  
|Model|  
|-----------|  
|Mountain-200|  
|Mountain Tire Tube|  
|Touring Tire Tube|  
  
 결과를 통해 Patch Kit 제품을 구매한 고객에게 권장하기에 가장 좋은 3가지 제품을 알 수 있습니다. 값을 입력하거나 **단일 쿼리 입력** 대화 상자에서 값을 추가 또는 제거하여 권장 사항을 결정할 때 여러 제품을 입력으로 제공할 수도 있습니다. 다음 예제 쿼리에서는 여러 값을 제공하여 이에 대해 예측을 수행하는 방법을 보여 줍니다. 값은 입력 값을 정의하는 SELECT 문에서 UNION 절로 연결됩니다.  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
From  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Racing Socks' AS [Model]  
  UNION SELECT 'Women''s Mountain Shorts' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 예상 결과:  
  
|Model|  
|-----------|  
|Long-Sleeve Logo Jersey|  
|Mountain-400-W|  
|Classic Vest|  
  
###  <a name="bkmk_Query6"></a> 예제 쿼리 6: 의사 결정 트리 모델에서 회귀 수식 검색  
 연속 특성에 대한 회귀를 포함하는 의사 결정 트리 모델을 만드는 경우 회귀 수식을 사용하여 예측을 수행하거나 회귀 수식에 대한 정보를 추출할 수 있습니다. 회귀 모델 쿼리에 대한 자세한 내용은 [선형 회귀 모델 쿼리 예제](../../analysis-services/data-mining/linear-regression-model-query-examples.md)를 참조하세요.  
  
 의사 결정 트리 모델에 회귀 노드와 불연속 특성 또는 범위에 따라 분할되는 노드가 혼합되어 있는 경우 회귀 노드만 반환하는 쿼리를 만들 수 있습니다. NODE_DISTRIBUTION 테이블에는 회귀 수식에 대한 세부 정보가 포함됩니다. 이 예에서는 쉽게 볼 수 있도록 열이 일반화되고 NODE_DISTRIBUTION 테이블에 별칭이 지정됩니다. 그러나 이 모델에는 Income을 다른 연속 특성과 연결하는 회귀 변수가 없습니다. 이 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 특성의 평균 값과 해당 특성에 대한 모델의 총 분산을 반환합니다.  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM DT_Predict. CONTENT  
WHERE NODE_TYPE = 25  
```  
  
 예제 결과:  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Yearly Income|Missing|0|0.000457142857142857|0|1.|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
||57220.8876687257|0|0|1041216662.54387|11|  
  
 회귀 모델에 사용되는 값 형식 및 통계에 대한 자세한 내용은 [선형 회귀 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)를 참조하세요.  
  
## <a name="list-of-prediction-functions"></a>예측 함수 목록  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘은 공통 함수 집합을 지원합니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘은 다음 표에 나열된 함수를 추가로 지원합니다.  
  
|||  
|-|-|  
|예측 함수|사용법|  
|[IsDescendant&#40;DMX&#41;](../../dmx/isdescendant-dmx.md)|한 노드가 모델에서 다른 노드의 자식인지 여부를 확인합니다.|  
|[IsInNode&#40;DMX&#41;](../../dmx/isinnode-dmx.md)|지정한 노드에 현재 사례가 포함되었는지 여부를 나타냅니다.|  
|[PredictAdjustedProbability&#40;DMX&#41;](../../dmx/predictadjustedprobability-dmx.md)|가중치 확률을 반환합니다.|  
|[PredictAssociation&#40;DMX&#41;](../../dmx/predictassociation-dmx.md)|연관 데이터 집합에서의 멤버 자격을 예측합니다.|  
|[PredictHistogram&#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|현재 예측된 값과 관련 된 값의 테이블을 반환 합니다.|  
|[PredictNodeId&#40;DMX&#41;](../../dmx/predictnodeid-dmx.md)|각 사례에 대한 Node_ID를 반환합니다.|  
|[PredictProbability&#40;DMX&#41;](../../dmx/predictprobability-dmx.md)|예측 값의 확률을 반환합니다.|  
|[PredictStdev&#40;DMX&#41;](../../dmx/predictstdev-dmx.md)|지정된 열의 예측 표준 편차를 반환합니다.|  
|[PredictSupport&#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|지정한 상태에 대한 지원 값을 반환합니다.|  
|[PredictVariance&#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|지정한 열의 분산을 반환합니다.|  
  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘에 공통된 함수 목록은 [일반 예측 함수&#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md)를 참조하세요. 특정 함수의 구문은 [DMX&#40;Data Mining Extensions&#41; 함수 참조](../../dmx/data-mining-extensions-dmx-function-reference.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft 의사 결정 트리 알고리즘](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)   
 [Microsoft 의사 결정 트리 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)   
 [의사 결정 트리 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
