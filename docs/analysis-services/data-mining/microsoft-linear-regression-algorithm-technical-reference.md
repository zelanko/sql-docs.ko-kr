---
title: "Microsoft 선형 회귀 알고리즘 기술 참조 | Microsoft Docs"
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
- AUTO_DETECT_PERIODICITY parameter
- linear regression algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 7807b5ff-8e0d-418d-a05b-b1a9644536d2
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 188666c119f92bc0093877c055ed4097cc2e1471
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-linear-regression-algorithm-technical-reference"></a>Microsoft 선형 회귀 알고리즘 기술 참조
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘은 여러 쌍의 연속 특성을 모델링하는 데 최적화된 특수한 버전의 Microsoft 의사 결정 트리 알고리즘입니다. 이 항목에서는 알고리즘의 구현을 설명하고, 알고리즘 동작을 사용자 지정하는 방법을 설명하며, 모델 쿼리에 대한 추가 정보로 연결되는 링크를 제공합니다.  
  
## <a name="implementation-of-the-linear-regression-algorithm"></a>선형 회귀 알고리즘 구현  
 Microsoft 의사 결정 트리 알고리즘은 선형 회귀, 분류, 연결 분석 등의 많은 태스크에 사용할 수 있습니다. 선형 회귀용으로 이 알고리즘을 구현하기 위해 알고리즘의 매개 변수가 제어되어 트리의 증가를 제한하며 모델의 모든 데이터는 단일 노드에 보관됩니다. 즉, 선형 회귀는 의사 결정 트리를 기반으로 하더라도 트리에는 단일 루트만 포함되고 분기는 포함되지 않습니다. 모든 데이터는 루트 노드에 있습니다.  
  
 이를 위해 알고리즘의 *MINIMUM_LEAF_CASES* 매개 변수는 알고리즘에서 마이닝 모델을 학습하는 데 사용하는 총 사례 수보다 크거나 같게 설정됩니다. 이 매개 변수를 이런 방식으로 설정하면 알고리즘에서 분할을 만들지 않으므로 선형 회귀가 수행됩니다.  
  
 회귀선을 나타내는 수식은 일반적으로 y = ax + b 형식을 사용하며 회귀 수식이라고도 합니다. 변수 Y는 출력 변수를 나타내고 X는 입력 변수를 나타내며 a와 b는 조정 가능한 계수입니다. 완성된 마이닝 모델을 쿼리하여 회귀 수식의 계수, 절편 및 기타 정보를 검색할 수 있습니다. 자세한 내용은 [선형 회귀 모델 쿼리 예제](../../analysis-services/data-mining/linear-regression-model-query-examples.md)를 참조하세요.  
  
### <a name="scoring-methods-and-feature-selection"></a>점수 매기기 방법 및 기능 선택  
 모든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 마이닝 알고리즘에서는 자동으로 기능 선택을 사용하여 분석을 향상시키고 처리 로드를 줄입니다. 선형 회귀 모델에서는 연속 열만 지원하므로 선형 회귀에서 기능 선택에 사용되는 방법은 흥미도 점수입니다. 다음 표에서는 참조를 위해 선형 회귀 알고리즘의 기능 선택과 의사 결정 트리 알고리즘의 기능 선택에 어떤 차이점이 있는지를 보여 줍니다.  
  
|알고리즘|분석 방법|설명|  
|---------------|------------------------|--------------|  
|선형 회귀|흥미도 점수|기본.<br /><br /> 의사 결정 트리 알고리즘에 사용할 수 있는 다른 기능 선택 방법은 불연속 변수에만 적용되므로 선형 회귀 모델에는 적용되지 않습니다.|  
|의사 결정 트리|흥미도 점수<br /><br /> Shannon Entropy<br /><br /> Bayesian with K2 Prior<br /><br /> Bayesian Dirichlet with uniform prior(기본값)|이진이 아닌 연속 값이 열에 포함되어 있는 경우 일관성을 보장하기 위해 모든 열에 흥미도 점수가 사용됩니다. 그렇지 않을 경우 기본 방법이나 지정된 방법이 사용됩니다.|  
  
 의사 결정 트리 모델의 기능 선택을 제어하는 알고리즘 매개 변수는 MAXIMUM_INPUT_ATTRIBUTES와 MAXIMUM_OUTPUT입니다.  
  
## <a name="customizing-the-linear-regression-algorithm"></a>선형 회귀 알고리즘 사용자 지정  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘은 결과 마이닝 모델의 동작, 성능 및 정확도에 영향을 주는 매개 변수를 지원합니다. 마이닝 모델 열이나 마이닝 구조 열에 모델링 플래그를 설정하여 데이터 처리 방식을 제어할 수도 있습니다.  
  
### <a name="setting-algorithm-parameters"></a>알고리즘 매개 변수 설정  
 다음 표에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘에서 제공되는 매개 변수에 대해 설명합니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*MAXIMUM_INPUT_ATTRIBUTES*|기능 선택을 호출하기 전에 알고리즘이 처리할 수 있는 입력 특성 수를 정의합니다. 이 값을 0으로 설정하면 기능 선택이 해제됩니다.<br /><br /> 기본값은 255입니다.|  
|*MAXIMUM_OUTPUT_ATTRIBUTES*|기능 선택을 호출하기 전에 알고리즘이 처리할 수 있는 출력 특성 수를 정의합니다. 이 값을 0으로 설정하면 기능 선택이 해제됩니다.<br /><br /> 기본값은 255입니다.|  
|*FORCE_REGRESSOR*|알고리즘에서 계산한 열의 중요도에 관계없이 알고리즘에서 표시된 열을 회귀 변수로 사용하도록 합니다.|  
  
### <a name="modeling-flags"></a>모델링 플래그  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘은 다음과 같은 모델링 플래그를 지원합니다. 마이닝 구조나 마이닝 모델을 만들 경우 분석 중 각 열의 값이 처리되는 방법을 지정하기 위해 모델링 플래그를 정의합니다. 자세한 내용은 [모델링 플래그&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)를 참조하세요.  
  
|모델링 플래그|Description|  
|-------------------|-----------------|  
|NOT NULL|열에 null이 포함될 수 없음을 나타냅니다. 따라서 Analysis Services가 모델 학습 중 Null을 발견할 경우 오류가 발생합니다.<br /><br /> 마이닝 구조 열에 적용됩니다.|  
|REGRESSOR|분석 중 잠재적 독립 변수로 처리될 연속 숫자 값이 열에 포함되도록 지정합니다. 마이닝 모델 열에 적용됩니다.<br /><br /> 참고: 열에 회귀 변수 플래그를 설정한다고 해서 해당 열이 항상 최종 모델에서 회귀 변수로 사용되는 것은 아닙니다.|  
  
### <a name="regressors-in-linear-regression-models"></a>선형 회귀 모델의 회귀 변수  
 선형 회귀 모델은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘을 기반으로 합니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘을 사용하지 않더라도 의사 결정 트리에 연속 특성에 대한 회귀를 나타내는 트리나 노드가 포함될 수 있습니다.  
  
 연속 열이 회귀 변수를 나타내도록 지정할 필요는 없습니다. 열에 REGRESSOR 플래그를 설정하지 않더라도 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘은 의미 있는 패턴을 포함하는 영역으로 데이터 집합을 분할합니다. 단, 모델링 플래그를 설정할 때 알고리즘이 트리의 노드에 패턴을 맞추기 위해 `a*C1 + b*C2 + ...` 형식의 회귀 수식을 찾으려고 한다는 것이 다릅니다. 잉여에 대한 합계가 계산되며 편차가 너무 클 경우 트리에서 강제로 분할이 수행됩니다.  
  
 예를 들어 income을 특성으로 사용하여 고객의 구매 행동을 예측하며 [Income] 열에 REGRESSOR 모델링 플래그를 설정하는 경우 알고리즘은 먼저 표준 회귀 수식을 사용하여 값을 맞추려고 시도합니다. 편차가 너무 클 경우 회귀 수식이 중단되고 다른 특성에 대해 트리가 분할됩니다. 분할 후 의사 결정 트리 알고리즘은 먼저 각 분기에서 Income에 대한 회귀 변수를 맞추려고 시도합니다.  
  
 FORCED_REGRESSOR 매개 변수를 사용하여 알고리즘이 항상 특정 회귀 변수를 사용하도록 할 수 있습니다. 이 매개 변수는 Microsoft 의사 결정 트리 알고리즘과 Microsoft 선형 회귀 알고리즘에서 사용할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 선형 회귀 모델은 하나의 키 열, 여러 입력 열, 하나 이상의 예측 가능한 열을 포함해야 합니다.  
  
### <a name="input-and-predictable-columns"></a>입력 열과 예측 가능한 열  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘은 다음 표에 나열된 특정 입력 열과 예측 가능한 열을 지원합니다. 마이닝 모델에 사용되는 경우 콘텐츠 형식의 의미에 대한 자세한 내용은 [콘텐츠 형식&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/content-types-data-mining.md)을 참조하세요.  
  
|열|내용 유형|  
|------------|-------------------|  
|입력 특성|Continuous, Cyclical, Key, Table 및 Ordered|  
|예측 가능한 특성|Continuous, Cyclical 및 Ordered|  
  
> [!NOTE]  
>  **Cyclical** 및 **Ordered** 콘텐츠 형식이 지원되기는 하지만 알고리즘은 해당 형식을 불연속 값으로 처리하고 특수한 처리를 수행하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft 선형 회귀 알고리즘](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)   
 [선형 회귀 모델 쿼리 예제](../../analysis-services/data-mining/linear-regression-model-query-examples.md)   
 [선형 회귀 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
