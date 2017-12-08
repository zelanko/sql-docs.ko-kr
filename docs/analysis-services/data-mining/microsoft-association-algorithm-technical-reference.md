---
title: "Microsoft 연결 알고리즘 기술 참조 | Microsoft Docs"
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
- MINIMUM_ITEMSET_SIZE parameter
- MAXIMUM_SUPPORT parameter
- association algorithms [Analysis Services]
- MINIMUM_SUPPORT parameter
- OPTIMIZED_PREDICTION_COUNT parameter
- associations [Analysis Services]
- MAXIMUM_ITEMSET_COUNT parameter
- MAXIMUM_ITEMSET_SIZE parameter
- MINIMUM_PROBABILITY parameter
ms.assetid: 50a22202-e936-4995-ae1d-4ff974002e88
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7e639fac7981f92f91b2beef0b57c190ce834f14
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-association-algorithm-technical-reference"></a>Microsoft 연결 알고리즘 기술 참조
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 규칙 알고리즘은 잘 알려진 Apriori 알고리즘을 간단하게 구현한 것입니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘과 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 규칙 알고리즘은 둘 다 연결을 분석하는 데 사용할 수 있지만 각 알고리즘에서 발견되는 규칙은 서로 다를 수 있습니다. 의사 결정 트리 모델에서 특정 규칙을 생성하는 분류는 정보 획득량을 기반으로 하는 반면 연결 모델에서 규칙은 전적으로 신뢰도를 기반으로 합니다. 따라서 연결 모델에서 강력한 규칙 또는 신뢰도가 높은 규칙은 새로운 정보를 제공하지 않기 때문에 반드시 유용한 것은 아닙니다.  
  
## <a name="implementation-of-the-microsoft-association-algorithm"></a>Microsoft 연결 알고리즘 구현  
 Apriori 알고리즘은 패턴을 분석하는 대신 *후보 항목 집합*을 생성한 다음 그 수를 계산합니다. 분석되는 데이터의 형식에 따라 후보 항목은 이벤트, 제품 또는 특성 값을 나타낼 수 있습니다.  
  
 가장 일반적인 연결 모델 유형에서 Yes/No 또는 Missing/Existing 값을 나타내는 부울 변수는 제품 또는 이벤트 이름과 같은 각 특성에 할당됩니다. 시장 바구니 분석은 부울 변수를 사용하여 고객 시장 바구니에서 특정 제품의 존재 또는 부재를 나타내는 연결 규칙 모델의 예입니다.  
  
 각 항목 집합에 대해 알고리즘은 지지도와 신뢰도를 나타내는 점수를 작성합니다. 이러한 점수는 항목 집합에서 유용한 규칙을 이끌어 내고 순위를 지정하는 데 사용할 수 있습니다.  
  
 숫자 특성에 대해서도 연결 모델을 사용할 수 있습니다. 특성이 연속이면 숫자는 버킷에서 *분할* 또는 그룹화될 수 있습니다. 이렇게 불연속화된 값은 부울 또는 특성-값 쌍으로 처리할 수 있습니다.  
  
### <a name="support-probability-and-importance"></a>지지도, 확률 및 중요도  
 *지지도*는 *빈도*라고도 하며 목표 항목 또는 항목 조합을 포함하는 사례 수를 의미합니다. 지정된 지지도보다 높거나 같은 항목만 모델에 포함될 수 있습니다.  
  
 *자주 나타나는 항목 집합* 은 항목 조합의 지지도 역시 MINIMUM_SUPPORT 매개 변수에 의해 정의된 임계값보다 큰 항목 모음을 의미합니다. 예를 들어 항목 집합이 {A,B,C}이고 MINIMUM_SUPPORT 값이 10일 경우 개별 항목 A, B, C는 각각 최소 10개의 사례에서 발견되어야 모델에 포함될 수 있으며 항목 조합 {A,B,C}도 최소 10개의 사례에서 발견되어야 합니다.  
  
 **참고** 항목 집합의 최대 길이(항목 수)를 지정하여 마이닝 모델의 항목 집합 수를 제어할 수도 있습니다.  
  
 기본적으로 특정 항목 또는 항목 집합에 대한 지지도는 해당 항목 또는 항목 집합을 포함하는 사례 수를 나타냅니다. 그러나 이 수를 1보다 작은 10진수 값으로 입력하여 MINIMUM_SUPPORT를 데이터 집합에 있는 총 사례 수에 대한 백분율로 표시할 수도 있습니다. 예를 들어 MINIMUM_SUPPORT 값을 0.03으로 지정할 경우 데이터 집합에 있는 총 사례 수의 3%에 해당하는 사례에 해당 항목 또는 항목 집합이 있어야 모델에 포함될 수 있습니다. 모델에 따라 개수 또는 백분율 중 적절한 방식을 결정해야 합니다.  
  
 반대로 규칙에 대한 임계값은 개수나 백분율이 아닌 확률( *신뢰도*라고도 함)로 표시됩니다. 예를 들어 항목 집합 {A,B,C}가 50개의 사례에 나타나고 항목 집합 {A,B,D}도 50개의 사례에 나타나지만 항목 집합 {A,B}가 다른 50개의 사례에 나타날 경우 {A,B} 다음에 반드시 {C}가 오는 것이 아니라는 점을 명확하게 알 수 있습니다. 따라서 알려진 모든 결과 중 특정 결과에 가중치를 매기기 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 항목 집합 {A,B,C}의 지지도를 모든 관련 항목 집합의 지지도로 나눠 개별 규칙(예: If {A,B} Then {C})의 확률을 계산합니다.  
  
 MINIMUM_PROBABILITY 값을 설정하여 모델이 생성하는 규칙의 수를 제한할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 생성되는 각 규칙마다 *리프트*라고도 하는 *중요도*를 나타내는 점수를 출력합니다. 리프트 중요도는 항목 집합 및 규칙마다 서로 다르게 계산됩니다.  
  
 항목 집합의 중요도는 항목 집합의 확률을 항목 집합에 있는 개별 항목의 복합 확률로 나눠 계산됩니다. 예를 들어 항목 집합에 {A,B}가 있는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 먼저 이 A와 B 조합을 포함하는 모든 사례 수를 계산하고 이 값을 총 사례 수로 나눈 다음 확률을 정규화합니다.  
  
 규칙의 중요도는 규칙 오른쪽에 대한 규칙 왼쪽의 로그 우도로 계산됩니다. 예를 들어 `If {A} Then {B}`규칙에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 B가 있고 A는 없는 사례에 대한 A와 B가 있는 사례의 비율을 계산한 다음 로그 눈금 간격을 사용하여 비율을 정규화합니다.  
  
### <a name="feature-selection"></a>기능 선택  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 규칙 알고리즘은 어떤 종류의 자동 기능 선택도 수행하지 않습니다. 대신 알고리즘에서 사용하는 데이터를 제어하는 매개 변수를 제공합니다. 이러한 매개 변수에는 각 항목 집합의 크기 제한, 항목 집합을 모델에 추가하는 데 필요한 최대/최소 지지도 설정이 포함될 수 있습니다.  
  
-   너무 흔해서 유용하지 않은 항목과 이벤트를 필터를 사용하여 제외시키려면 MAXIMUM_SUPPORT 값을 낮춰 모델에서 자주 나타나는 항목 집합을 제거합니다.  
  
-   드물게 나타나는 항목과 항목 집합을 필터를 사용하여 제외시키려면 MINIMUM_SUPPORT 값을 높입니다.  
  
-   규칙을 필터를 사용하여 제외시키려면 MINIMUM_PROBABILITY 값을 높입니다.  
  
## <a name="customizing-the-microsoft-association-rules-algorithm"></a>Microsoft 연결 규칙 알고리즘 사용자 지정  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 규칙 알고리즘은 결과 마이닝 모델의 동작, 성능 및 정확도에 영향을 주는 여러 매개 변수를 지원합니다.  
  
### <a name="setting-algorithm-parameters"></a>알고리즘 매개 변수 설정  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 데이터 마이닝 디자이너를 사용하여 언제든지 마이닝 모델의 매개 변수를 변경할 수 있습니다. 사용 하 여 매개 변수를 프로그래밍 방식으로 변경할 수도 있습니다는 <xref:Microsoft.AnalysisServices.MiningModel.AlgorithmParameters%2A> 또는 AMO를 사용 하 여 컬렉션의 [MiningModels 요소 &#40; ASSL &#41; ](../../analysis-services/scripting/collections/miningmodels-element-assl.md) XMLA의 합니다. 다음 표에서는 각 매개 변수에 대해 설명합니다.  
  
> [!NOTE]  
>  DMX 문을 사용하여 기존 모델의 매개 변수를 변경할 수 없습니다. 따라서 모델을 만들 때 DMX CREATE MODEL 또는 ALTER STRUCTURE… ADD MODEL에 매개 변수를 지정해야 합니다.  
  
 *MAXIMUM_ITEMSET_COUNT*  
 생성할 최대 항목 집합 수를 지정합니다. 값을 지정하지 않으면 기본값이 사용됩니다.  
  
 기본값은 200000입니다.  
  
> [!NOTE]  
>  항목 집합은 지지도 순으로 순위가 지정됩니다. 지지도가 동일한 항목 집합 간의 순서는 임의로 지정됩니다.  
  
 *MAXIMUM_ITEMSET_SIZE*  
 항목 집합에 사용할 수 있는 최대 항목 수를 지정합니다. 이 값을 0으로 설정하면 항목 집합 크기가 무제한으로 지정됩니다.  
  
 기본값은 3입니다.  
  
> [!NOTE]  
>  제한에 도달하면 모델 처리가 중지되므로 이 값을 줄이면 모델을 만드는 데 필요한 시간이 줄어들 수 있습니다.  
  
 *MAXIMUM_SUPPORT*  
 지지도에 대한 항목 집합의 최대 사례 수를 지정합니다. 이 매개 변수는 자주 나타나 잠재적으로 별 의미가 없는 항목을 제거하는 데 사용될 수 있습니다.  
  
 이 값이 1보다 작으면 총 사례의 백분율을 나타내고 1보다 크면 항목 집합을 포함하는 사례의 절대 수를 나타냅니다.  
  
 기본값은 1입니다.  
  
 *MINIMUM_ITEMSET_SIZE*  
 항목 집합에 사용할 수 있는 최소 항목 수를 지정합니다. 이 값을 늘리면 모델에 더 적은 수의 항목 집합이 포함될 수 있습니다. 단일 항목으로 구성된 항목 집합을 무시하려는 경우 이 매개 변수가 유용할 수 있습니다.  
  
 기본값은 1입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 처리의 일부로 단일 항목의 확률을 계산해야 하기 때문에 최소값을 늘려 모델 처리 시간을 줄일 수는 없습니다. 그러나 이 값을 높게 설정하여 작은 항목 집합을 필터를 사용하여 제외시킬 수는 있습니다.  
  
 *MINIMUM_PROBABILITY*  
 규칙이 참이 되는 최소 확률을 지정합니다.  
  
 예를 들어 이 값을 0.5로 설정하면 확률이 50% 미만인 규칙은 생성되지 않습니다.  
  
 기본값은 0.4입니다.  
  
 *MINIMUM_SUPPORT*  
 알고리즘이 규칙을 생성하기 전에 항목 집합이 있어야 하는 최소 사례 수를 지정합니다.  
  
 이 값을 1보다 작게 설정하면 최소 사례 수가 총 사례에 대한 백분율로 계산됩니다.  
  
 이 값을 1보다 큰 정수로 설정하면 최소 사례 수가 항목 집합을 포함해야 하는 사례 수로 계산됩니다. 메모리가 제한된 경우 알고리즘은 이 매개 변수의 값을 자동으로 늘릴 수 있습니다.  
  
 기본값은 0.03입니다. 이는 항목 집합이 최소한 총 사례 중 3% 이상에서 발견되어야 모델에 포함될 수 있음을 의미합니다.  
  
 *OPTIMIZED_PREDICTION_COUNT*  
 예측 최적화를 위해 캐시할 항목 수를 정의합니다.  
  
 기본값은 0입니다. 기본값을 사용할 경우 알고리즘은 쿼리에서 요청한 만큼 많은 예측을 생성합니다.  
  
 *OPTIMIZED_PREDICTION_COUNT* 에 대해 0이 아닌 값을 지정하면 추가 예측을 요청한 경우에도 예측 쿼리는 지정된 수 이하의 항목만 반환할 수 있습니다. 그러나 값을 설정하면 예측 성능을 향상시킬 수 있습니다.  
  
 예를 들어 이 값을 3으로 설정할 경우 알고리즘은 예측을 위해 3개의 항목만 캐시합니다. 3개의 항목이 반환된다고 균등하게 예상되는 추가 예측을 볼 수 없습니다.  
  
### <a name="modeling-flags"></a>모델링 플래그  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 규칙 알고리즘과 함께 사용할 수 있는 모델링 플래그는 다음과 같습니다.  
  
 NOT  NULL  
 열에 null이 포함될 수 없음을 나타냅니다. 따라서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 모델 학습 중 null 값을 발견할 경우 오류가 발생합니다.  
  
 마이닝 구조 열에 적용됩니다.  
  
 MODEL_EXISTENCE_ONLY  
 열이 **Missing** 및 **Existing**상태를 갖는 것으로 간주됩니다. Null은 누락 값입니다.  
  
 마이닝 모델 열에 적용됩니다.  
  
## <a name="requirements"></a>요구 사항  
 연결 모델에는 하나의 키 열, 여러 개의 입력 열 및 하나의 예측 가능한 열이 있어야 합니다.  
  
### <a name="input-and-predictable-columns"></a>입력 열과 예측 가능한 열  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 규칙 알고리즘은 다음 표에 나열된 특정 입력 열과 예측 가능한 열을 지원합니다. 마이닝 모델의 콘텐츠 형식에 대한 자세한 내용은 [콘텐츠 형식&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/content-types-data-mining.md)을 참조하세요.  
  
|열|내용 유형|  
|------------|-------------------|  
|입력 특성|Cyclical, Discrete, Discretized, Key, Table, Ordered|  
|예측 가능한 특성|Cyclical, Discrete, Discretized, Key, Table, Ordered|  
  
> [!NOTE]  
>  Cyclical  및 Ordered  내용 유형이 지원되기는 하지만 알고리즘은 해당 유형을 불연속 값으로 처리하고 특수한 처리를 수행하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft 연결 알고리즘](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [연결 모델 쿼리 예제](../../analysis-services/data-mining/association-model-query-examples.md)   
 [연결 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
