---
title: 연결 모델 쿼리 예제 | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cb268ffeb4b7f997876b7fc28dfb773b971aaf1e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34020020"
---
# <a name="association-model-query-examples"></a>연결 모델 쿼리 예제
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  데이터 마이닝 모델에 대한 쿼리를 만들 때 분석 중에 발견된 규칙과 항목 집합에 대한 세부 정보를 제공하는 내용 쿼리를 만들거나, 데이터에서 발견된 연결을 사용하여 예측을 수행하는 예측 쿼리를 만들 수 있습니다. 연결 모델에서 예측은 일반적으로 규칙을 기반으로 하여 권장 구성을 생성하는 데 사용되고, 내용에 대한 쿼리는 일반적으로 항목 집합 간의 관계를 탐색합니다. 모델에 대한 메타데이터를 검색할 수도 있습니다.  
  
 이 섹션에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 규칙 알고리즘을 기반으로 하는 모델에 대해 이러한 종류의 쿼리를 만드는 방법에 대해 설명합니다.  
  
 **내용 쿼리**  
  
 [DMX를 사용하여 모델 메타데이터 데이터 가져오기](#bkmk_Query1)  
  
 [스키마 행 집합에서 메타데이터 가져오기](#bkmk_Query2)  
  
 [모델의 원래 매개 변수 검색](#bkmk_Query3)  
  
 [항목 집합 및 제품 목록 검색](#bkmk_Query4)  
  
 [상위 10개 항목 집합 반환](#bkmk_Query5)  
  
 **예측 쿼리**  
  
 [연관된 항목 예측](#bkmk_Query6)  
  
 [관련 항목 집합에 대한 신뢰도 결정](#bkmk_Query7)  
  
##  <a name="bkmk_top2"></a> 모델 정보 찾기  
 모든 마이닝 모델은 마이닝 모델 스키마 행 집합이라고 하는 표준화된 스키마에 따라, 알고리즘을 통해 학습한 내용을 표시합니다. 마이닝 모델 스키마 행 집합에 대한 쿼리는 DMX(Data Mining Extensions) 문을 사용하거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 저장 프로시저를 사용하여 만들 수 있습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 SQL과 유사한 구문을 사용하여 스키마 행 집합을 직접 시스템 테이블로 쿼리할 수도 있습니다.  
  
###  <a name="bkmk_Query1"></a> 예제 쿼리 1: DMX를 사용하여 모델 메타데이터 가져오기  
 다음 쿼리는 연결 모델 `Association`에 대한 기본 메타데이터(예: 모델 이름, 모델이 저장된 데이터베이스, 모델의 자식 노드 수)를 반환합니다. 이 쿼리는 DMX 내용 쿼리를 사용하여 모델의 부모 노드에서 메타데이터를 검색합니다.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  CHILDREN_CARDINALITY 열의 이름을 대괄호로 묶어 동일한 이름의 MDX 예약 키워드와 구분해야 합니다.  
  
 예제 결과:  
  
|||  
|-|-|  
|MODEL_CATALOG|Association Test|  
|MODEL_NAME|연결|  
|NODE_CAPTION|Association Rules Model|  
|NODE_SUPPORT|14879|  
|CHILDREN_CARDINALITY|942|  
|NODE_DESCRIPTION|Association Rules Model; ITEMSET_COUNT=679; RULE_COUNT=263; MIN_SUPPORT=14; MAX_SUPPORT=4334; MIN_ITEMSET_SIZE=0; MAX_ITEMSET_SIZE=3; MIN_PROBABILITY=0.400390625; MAX_PROBABILITY=1; MIN_LIFT=0.14309369632511; MAX_LIFT=1.95758227647523|  
  
 연결 모델에서 이러한 열의 의미에 대한 정의는 [연결 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)를 참조하세요.  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a> 예제 쿼리 2: 스키마 행 집합에서 추가 메타데이터 가져오기  
 데이터 마이닝 스키마 행 집합을 쿼리하면 DMX 내용 쿼리에 반환되는 것과 동일한 정보를 찾을 수 있는데, 스키마 행 집합은 모델이 마지막으로 처리된 날짜, 마이닝 구조, 예측 가능한 특성으로 사용된 열 이름 등 몇 개의 추가 열을 제공합니다.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, SERVICE_NAME, PREDICTION_ENTITY,   
MINING_STRUCTURE, LAST_PROCESSED  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 예제 결과:  
  
|||  
|-|-|  
|MODEL_CATALOG|Adventure Works DW Multidimensional 2012|  
|MODEL_NAME|연결|  
|SERVICE_NAME|Association Rules Model|  
|PREDICTION_ENTITY|v Assoc Seq Line Items|  
|MINING_STRUCTURE|연결|  
|LAST_PROCESSED|9/29/2007 10:21:24 PM|  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query3"></a> 예제 쿼리 3: 모델의 원래 매개 변수 검색  
 다음 쿼리는 모델을 만들 때 사용했던 매개 변수 설정에 대한 세부 정보가 포함된 단일 열을 반환합니다.  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 예제 결과:  
  
 MAXIMUM_ITEMSET_COUNT=200000,MAXIMUM_ITEMSET_SIZE=3,MAXIMUM_SUPPORT=1,MINIMUM_SUPPORT=9.40923449156529E-04,MINIMUM_IMPORTANCE=-999999999,MINIMUM_ITEMSET_SIZE=0,MINIMUM_PROBABILITY=0.4  
  
 [맨 위로 이동](#bkmk_top2)  
  
## <a name="finding-information-about-rules-and-itemsets"></a>규칙 및 항목 집합에 대한 정보 찾기  
 연결 모델의 일반적인 용도는 자주 사용하는 항목 집합에 대한 정보를 검색하는 것과 특정 규칙과 항목 집합에 대한 세부 정보를 추출하는 것입니다. 예를 들어 특별히 관심 있는 항목으로 점수가 매겨진 규칙 목록을 추출하거나 가장 일반적인 항목 집합의 목록을 만들 수 있습니다. 이러한 정보는 DMX 내용 쿼리를 사용하여 검색할 수 있습니다. **Microsoft 연결 뷰어**에서도 이러한 정보를 찾아볼 수 있습니다.  
  
###  <a name="bkmk_Query4"></a> 예제 쿼리 4: 항목 집합 및 제품 목록 검색  
 다음 쿼리는 모든 항목 집합과 각 항목 집합에 포함된 제품을 나열하는 중첩 테이블을 검색합니다. NODE_NAME 열에는 모델 내에 있는 항목 집합의 고유 ID가 들어 있고, NODE_CAPTION에는 항목에 대한 텍스트 설명이 제공됩니다. 이 예에서는 두 제품을 포함하는 항목 집합이 결과에 두 개의 행을 생성하도록 중첩 테이블이 평면화됩니다. 클라이언트에서 계층적 데이터를 지원하는 경우 FLATTENED 키워드를 생략해도 됩니다.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
NODE_PROBABILITY, NODE_SUPPORT,  
(SELECT ATTRIBUTE_NAME FROM NODE_DISTRIBUTION) as PurchasedProducts  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 예제 결과:  
  
|||  
|-|-|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
|NODE_PROBABILITY|0.291283016331743|  
|NODE_SUPPORT|4334|  
|PURCHASEDPRODUCTS.ATTRIBUTE_NAME|v Assoc Seq Line Items(Sport-100)|  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a> 예제 쿼리 5: 상위 10개 항목 집합 반환  
 이 예는 DMX에서 기본적으로 제공하는 몇 가지 그룹화 및 순서 지정 함수를 사용하는 방법을 보여 줍니다. 각 노드에 대한 지지도 순으로 정렬된 경우 이 쿼리는 상위 10개의 항목 집합을 반환합니다. Transact-SQL을 사용하고 있으므로 결과를 명시적으로 그룹화할 필요는 없지만 각 쿼리에는 한 개의 집계 함수만 사용할 수 있습니다.  
  
```  
SELECT TOP 10 (NODE_SUPPORT),NODE_NAME, NODE_CAPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 예제 결과:  
  
|||  
|-|-|  
|NODE_SUPPORT|4334|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
  
 [맨 위로 이동](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>모델을 사용하여 예측 수행  
 연결 규칙 모델은 항목 집합에서 발견된 상관 관계를 기반으로 하는 권장 구성을 생성하는 데 주로 사용됩니다. 따라서 연결 규칙 모델을 기반으로 예측 쿼리를 만들 때 일반적으로 모델의 규칙을 사용하여 새로운 데이터를 토대로 예측을 수행합니다.  [PredictAssociation&#40;DMX&#41;](../../dmx/predictassociation-dmx.md) 은 권장 구성을 반환하는 함수로, 쿼리 결과를 사용자 지정하는 데 사용할 수 있는 몇 개의 인수를 포함합니다.  
  
 서로 다른 교차 판매 전략의 효율성을 비교할 수 있도록 다양한 규칙과 항목 집합에 대한 신뢰도를 반환하려는 경우 연결 모델에 대한 쿼리가 유용할 수 있습니다. 다음 예에서는 이러한 쿼리를 만드는 방법을 보여 줍니다.  
  
###  <a name="bkmk_Query6"></a> 예제 쿼리 6: 관련 항목 예측  
 다음 예제에서는 [중간 데이터 마이닝 자습서&#40;Analysis Services - 데이터 마이닝&#41;](http://msdn.microsoft.com/library/404b31d5-27f4-4875-bd60-7b2b8613eb1b)에서 만든 연결 모델을 사용하며, 특정 제품을 구매한 고객에게 어떤 제품을 권장할 것인지를 알려 주는 예측 쿼리를 만드는 방법을 보여 줍니다. 사용자가 **SELECT…UNION** 문에서 모델에 값을 제공하는 쿼리를 단일 쿼리라고 합니다. 새로운 값에 해당하는 예측 가능한 모델 열이 중첩 테이블이므로 **SELECT** 절을 하나 사용하여 새 값을 중첩 테이블 열 `[Model]`에 매핑하고, 또 다른 **SELECT** 절을 사용하여 중첩 테이블 열을 사례 수준 열 `[v Assoc Seq Line Items]`에 매핑해야 합니다. INCLUDE-STATISTICS 키워드를 쿼리에 추가하면 권장 구성에 대한 확률과 지지도를 확인할 수 있습니다.  
  
```  
SELECT PredictAssociation([Association].[vAssocSeqLineItems],INCLUDE_STATISTICS, 3)  
FROM [Association]  
NATURAL PREDICTION JOIN   
(SELECT  
(SELECT 'Classic Vest' as [Model])  
AS [v Assoc Seq Line Items])  
AS t  
```  
  
 예제 결과:  
  
|Model|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283|0.252696|  
|Water Bottle|2866|0.19262|0.175205|  
|Patch kit|2113|0.142012|0.132389|  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a> 예제 쿼리 7: 관련 항목 집합에 대한 신뢰도 확인  
 규칙은 권장 구성을 생성하는 데 유용한 반면 항목 집합은 데이터 집합의 패턴을 보다 상세하게 분석하는 데 더 유용합니다. 예를 들어 이전 예제 쿼리에 의해 반환된 권장 구성이 만족스럽지 않을 경우 제품 A가 포함된 다른 항목 집합을 검사하여 제품 A가 고객이 다른 종류의 제품과 함께 구매하고자 하는 액세서리인지 여부 또는 제품 A가 특정 제품의 구매와 강한 상관 관계가 있는지 여부를 확인할 수 있습니다. 이러한 관계를 확인하는 가장 쉬운 방법은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 뷰어에서 항목 집합을 필터링하는 것이지만 쿼리를 통해 동일한 정보를 검색할 수 있습니다.  
  
 다음 예제 쿼리는 단일 항목인 Water Bottle을 포함하여 Water Bottle 항목을 포함하는 모든 항목 집합을 반환합니다.  
  
```  
SELECT TOP 100 FROM   
(  
SELECT FLATTENED NODE_CAPTION, NODE_SUPPORT,   
(SELECT ATTRIBUTE_NAME from NODE_DISTRIBUTION  
WHERE ATTRIBUTE_NAME = 'v Assoc Seq Line Items(Water Bottle)') as D  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
) AS Items  
WHERE [D.ATTRIBUTE_NAME] <> NULL  
ORDER BY NODE_SUPPORT DESC  
```  
  
 예제 결과:  
  
|NODE_CAPTION|NODE_SUPPORT|D.ATTRIBUTE_NAME|  
|-------------------|-------------------|-----------------------|  
|Water Bottle = Existing|2866|v Assoc Seq Line Items(Water Bottle)|  
|Mountain Bottle Cage = Existing, Water Bottle = Existing|1136|v Assoc Seq Line Items(Water Bottle)|  
|Road Bottle Cage = Existing, Water Bottle = Existing|1068|v Assoc Seq Line Items(Water Bottle)|  
|Water Bottle = Existing, Sport-100 = Existing|734|v Assoc Seq Line Items(Water Bottle)|  
  
 이 쿼리는 조건과 일치하는 중첩 테이블의 행뿐만 아니라 외부 또는 사례 테이블의 모든 행을 반환합니다. 따라서 대상 특성 이름에 Null 값이 있는 사례 테이블 행을 제거하는 조건을 추가해야 합니다.  
  
 [맨 위로 이동](#bkmk_top2)  
  
## <a name="function-list"></a>함수 목록  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘은 공통 함수 집합을 지원합니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 알고리즘은 다음 표에 나열된 함수를 추가로 지원합니다.  
  
|||  
|-|-|  
|예측 함수|사용법|  
|[IsDescendant & #40; DMX & #41;](../../dmx/isdescendant-dmx.md)|한 노드가 신경망 그래프에서 다른 노드의 자식인지 여부를 확인합니다.|  
|[IsInNode & #40; DMX & #41;](../../dmx/isinnode-dmx.md)|지정한 노드에 현재 사례가 포함되었는지 여부를 나타냅니다.|  
|[PredictAdjustedProbability & #40; DMX & #41;](../../dmx/predictadjustedprobability-dmx.md)|가중치 확률을 반환합니다.|  
|[PredictAssociation & #40; DMX & #41;](../../dmx/predictassociation-dmx.md)|연관 데이터 집합에서의 멤버 자격을 예측합니다.|  
|[PredictHistogram & #40; DMX & #41;](../../dmx/predicthistogram-dmx.md)|현재 예측된 값과 관련 된 값의 테이블을 반환 합니다.|  
|[PredictNodeId & #40; DMX & #41;](../../dmx/predictnodeid-dmx.md)|각 사례에 대한 Node_ID를 반환합니다.|  
|[PredictProbability & #40; DMX & #41;](../../dmx/predictprobability-dmx.md)|예측 값의 확률을 반환합니다.|  
|[PredictSupport & #40; DMX & #41;](../../dmx/predictsupport-dmx.md)|지정한 상태에 대한 지원 값을 반환합니다.|  
|[PredictVariance & #40; DMX & #41;](../../dmx/predictvariance-dmx.md)|예측 값의 분산을 반환합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft 연결 알고리즘](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Microsoft 연결 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)   
 [연결 모델 & #40;에 대 한 마이닝 모델 콘텐츠 Analysis Services-데이터 마이닝 & #41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
