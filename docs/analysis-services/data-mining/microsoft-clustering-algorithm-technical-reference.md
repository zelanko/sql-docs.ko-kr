---
title: "Microsoft 클러스터링 알고리즘 기술 참조 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clustering [Data Mining]
- MAXIMUM_INPUT_ATTRIBUTES parameter
- CLUSTER_SEED parameter
- MODELLING_CARDINALITY parameter
- MINIMUM_SUPPORT parameter
- STOPPING_TOLERANCE parameter
- MAXIMUM_STATES parameter
- SAMPLE_SIZE parameter
- CLUSTERING_METHOD parameter
- soft clustering [Data Mining]
- clustering algorithms [Analysis Services]
- CLUSTER_COUNT parameter
ms.assetid: ec40868a-6dc7-4dfa-aadc-dedf69e555eb
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 187eea9af56b4da074f374923c29d7ebcea0aca2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="microsoft-clustering-algorithm-technical-reference"></a>Microsoft 클러스터링 알고리즘 기술 참조
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]이 섹션의 구현에 설명 된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘, 클러스터링 모델의 동작을 제어 하는 데 사용할 수 있는 매개 변수를 포함 합니다. 또한 클러스터링 모델을 만들고 처리할 때 성능을 향상시킬 수 있는 방법도 제공합니다.  
  
 클러스터링 모델 사용 방법은 다음 항목을 참조하십시오.  
  
-   [클러스터링 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
-   [클러스터링 모델 쿼리 예제](../../analysis-services/data-mining/clustering-model-query-examples.md)  
  
## <a name="implementation-of-the-microsoft-clustering-algorithm"></a>Microsoft  클러스터링 알고리즘 구현  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘은 두 가지 메서드를 통해 클러스터를 만들고 데이터 요소를 해당 클러스터에 할당합니다. 첫 번째는 하드 클러스터링 메서드인 *K-means* 알고리즘으로, 한 개의 데이터 요소는 한 개의 클러스터에만 속할 수 있으며 해당 클러스터에 있는 각 데이터 요소의 멤버 자격에 대해 단일 확률이 계산됩니다. 두 번째는 *소프트 클러스터링* 메서드인 EM( *Expectation Maximization* ) 메서드로, 한 개의 데이터 요소는 항상 여러 개의 클러스터에 속해 있으며 데이터 요소와 클러스터의 각 조합에 대해 확률이 계산됩니다.  
  
 *CLUSTERING_METHOD* 매개 변수를 설정하여 사용할 알고리즘을 선택할 수 있습니다. 기본 클러스터링 메서드는 Scalable  EM입니다.  
  
### <a name="em-clustering"></a>EM  클러스터링  
 EM  클러스터링에서 알고리즘은 초기 클러스터 모델을 반복적으로 구체화하여 데이터에 적합하게 맞추며 데이터 요소가 클러스터에 존재할 확률을 결정합니다. 알고리즘은 확률 모델이 데이터에 적합할 경우 프로세스를 끝냅니다. 모델이 제공될 경우 적합도를 결정하는 데 사용되는 함수는 데이터의 로그 유사도입니다.  
  
 프로세스 중 빈 클러스터가 생성되거나 하나 이상의 클러스터의 멤버 자격이 지정된 임계값 미만일 경우 모집단이 적은 클러스터는 새 데이터 요소에서 다시 시드되고 EM  알고리즘이 다시 실행됩니다.  
  
 EM  클러스터링 메서드의 결과는 확률적입니다. 즉,  각 데이터 요소는 모든 클러스터에 속해 있지만 데이터 요소를 클러스터에 할당할 때마다 확률은 다릅니다. 이 메서드는 클러스터 중복을 허용하므로 모든 클러스터에 있는 항목의 합계가 학습 집합에 있는 총 항목 수를 초과할 수 있습니다. 마이닝 모델 결과에서 지지도를 나타내는 점수는 이를 설명하기 위해 조정됩니다.  
  
 EM  알고리즘은 Microsoft  클러스터링 모델에 사용되는 기본 알고리즘으로, K-Means  클러스터링에 비해 다음과 같은 여러 이점을 제공하기 때문에 기본 알고리즘으로 사용됩니다.  
  
-   데이터베이스 검색은 최대 한 번만 필요합니다.  
  
-   메모리(RAM)가 한정된 경우에도 작동합니다.  
  
-   정방향 전용 커서를 사용할 수 있습니다.  
  
-   샘플링 방법보다 뛰어납니다.  
  
 Microsoft 구현은 Scalable EM과 Non-scalable EM을 제공합니다. 기본적으로 Scalable  EM에서는 처음 50,000개의 레코드를 사용하여 초기 검색을 시드합니다. 이 작업이 성공할 경우 모델은 이 데이터만 사용합니다. 50,000개의 레코드를 사용해도 모델이 적합하지 않을 경우 50,000개의 레코드를 추가로 읽습니다. Non-scalable  EM에서는 크기에 관계없이 전체 데이터 집합을 읽습니다. 이 메서드를 사용하면 보다 정확한 클러스터를 만들 수는 있지만 메모리 요구 사항이 상당히 증가될 수 있습니다. Scalable  EM은 로컬 버퍼에서 작동하기 때문에 Non-scalable  EM에 비해 데이터를 보다 빨리 반복 처리할 수 있으며 알고리즘은 CPU  메모리 캐시를 보다 효율적으로 사용할 수 있습니다. 또한 모든 데이터가 주 메모리에 저장될 수 있어도 Scalable  EM은 Non-scalable  EM보다 3배 이상 빠릅니다. 대부분의 경우 성능이 향상되었다고 해서 전체 모델의 품질이 저하되는 것은 아닙니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘의 EM 구현에 대해 설명하는 기술 보고서는 [Scaling EM (Expectation Maximization) Clustering to Large Databases](http://go.microsoft.com/fwlink/?LinkId=45964)(EM(Expectation Maximization) 클러스터링을 큰 데이터베이스로 크기 조정)를 참조하세요.  
  
### <a name="k-means-clustering"></a>K-Means  클러스터링  
 K-Means  클러스터링은 클러스터에 포함된 항목 간의 차이는 최소화하면서 클러스터 간의 거리는 최대화하여 클러스터 멤버 자격을 할당하는 잘 알려진 메서드입니다. K-Means의 "means"는 클러스터의 *중심* 을 의미하는데, 이 중심은 임의로 선택된 다음 클러스터에 포함된 모든 데이터 요소의 정확한 평균을 나타낼 때까지 반복적으로 구체화되는 데이터 요소입니다. "K"는 클러스터링 프로세스를 시드하는 데 사용되는 임의의 데이터 요소 수를 의미합니다. K-Means  알고리즘은 클러스터에 포함된 데이터 레코드와 클러스터 평균을 나타내는 벡터 간의 유클리드 제곱 거리를 계산하여 해당 합계가 최소값에 도달할 경우 최종 K  클러스터 집합에 수렴합니다.  
  
 K-Means  알고리즘은 각 데이터 요소를 정확히 한 개의 클러스터에 할당하며 멤버 자격의 불확실성을 허용하지 않습니다. 클러스터의 멤버 자격은 중심에서의 거리로 표시됩니다.  
  
 일반적으로 K-Means  알고리즘은 연속 특성의 클러스터를 만드는 데 사용되는데 이때 평균에 대한 거리는 간단히 계산할 수 있습니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 구현은 확률을 사용하여 불연속 특성을 클러스터링하도록 K-Means  메서드를 조정합니다.  불연속 특성의 경우 특정 클러스터에서 데이터 요소의 거리는 다음과 같이 계산됩니다.  
  
 1 - P(data point, cluster)  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘은 K-Means  계산에 사용된 거리 함수를 표시하지 않으므로 완성된 모델에서는 거리 측정값을 사용할 수 없습니다. 그러나 예측 함수를 사용하여 거리에 해당하는 값을 반환할 수 있습니다.  이때 거리는 클러스터에 속하는 데이터 요소의 확률로 계산됩니다. 자세한 내용은 [ClusterProbability&#40;DMX&#41;](../../dmx/clusterprobability-dmx.md)를 참조하세요.  
  
 K-Means 알고리즘은 데이터 집합을 샘플링하는 두 가지 메서드를 제공합니다. Non-scalable K-Means는 전체 데이터 집합을 로드한 다음 하나의 클러스터링 패스를 만들며, Scalable K-Means 알고리즘은 처음 50,000개의 사례를 사용하며 데이터에 적합한 모델을 얻기 위해 더 많은 데이터가 필요한 경우에만 사례를 추가로 읽습니다.  
  
### <a name="updates-to-the-microsoft-clustering-algorithm-in-sql-server-2008"></a>SQL  Server  2008의 Microsoft  클러스터링 알고리즘 업데이트  
 SQL Server 2008에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘의 기본 구성은 내부 매개 변수 NORMALIZATION = 1을 사용하도록 변경되었습니다. 정규화는 z 점수 통계를 사용하여 수행되며 정규 분포를 가정합니다. 기본 동작에 대한 이 변경은 크기가 크고 이상값이 많을 수 있는 특성의 효과를 최소화하는 것입니다. 그러나 z 점수 정규화는 균일 분포와 같은 정규가 아닌 분포에서 클러스터링 결과를 변경할 수 있습니다. 정규화를 방지하고 SQL Server 2005의 K-means 클러스터링 알고리즘과 동일한 동작을 얻기 위해 **매개 변수 설정** 대화 상자를 사용하여 사용자 지정 매개 변수 NORMALIZATION을 추가하고 해당 값을 0으로 설정할 수 있습니다.  
  
> [!NOTE]  
>  NORMALIZATION  매개 변수는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘의 내부 속성이며 지원되지 않습니다. 일반적으로 모델 결과를 향상시키기 위해 클러스터링 모델에서 정규화를 사용하는 것이 좋습니다.  
  
## <a name="customizing-the-microsoft-clustering-algorithm"></a>Microsoft  클러스터링 알고리즘 사용자 지정  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘은 결과 마이닝 모델의 동작,  성능 및 정확도에 영향을 주는 여러 매개 변수를 지원합니다.  
  
### <a name="setting-algorithm-parameters"></a>알고리즘 매개 변수 설정  
 다음 표에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘에서 사용할 수 있는 매개 변수에 대해 설명합니다. 이러한 매개 변수는 결과 마이닝 모델의 성능과 정확도에 영향을 줍니다.  
  
 CLUSTERING_METHOD  
 알고리즘에서 사용할 클러스터링 메서드를 지정합니다. 사용할 수 있는 클러스터링 메서드에는  
  
|ID|메서드|  
|--------|------------|  
|1|Scalable  EM|  
|2|Non-scalable  EM|  
|3|Scalable  K-Means|  
|4|Non-scalable  K-Means|  
  
 기본값은 1(scalable  EM)입니다.  
  
 CLUSTER_COUNT  
 알고리즘에서 작성할 클러스터의 대략적인 개수를 지정합니다. 데이터에서 대략적인 개수의 클러스터를 작성할 수 없는 경우 알고리즘은 가능한 한 많은 클러스터를 작성합니다. CLUSTER_COUNT를 0으로 설정하면 알고리즘은 추론을 사용하여 작성할 클러스터의 수를 정확하게 결정합니다.  
  
 기본값은 10입니다.  
  
 CLUSTER_SEED  
 모델 작성 초기 단계에서 임의로 클러스터를 생성하는 데 사용되는 초기값을 지정합니다.  
  
 이 값을 변경하여 초기 클러스터가 생성되는 방식을 변경한 다음 다른 초기값을 사용하여 생성된 모델을 비교할 수 있습니다. 초기값이 변경되었지만 발견된 클러스터가 많이 변경되지 않은 경우 이 모델은 상대적으로 안정적인 모델로 간주될 수 있습니다.  
  
 기본값은 0입니다.  
  
 MINIMUM_SUPPORT  
 클러스터를 생성하는 데 필요한 최소 사례 수를 지정합니다. 클러스터의 사례 수가 이 값보다 적을 경우 해당 클러스터는 빈 클러스터로 간주되어 무시됩니다.  
  
 이 값을 너무 높게 설정하면 유효한 클러스터를 놓칠 수 있습니다.  
  
> [!NOTE]  
>  기본 클러스터링 메서드인 EM을 사용하는 경우 일부 클러스터의 지지도 값이 지정된 값보다 낮을 수 있습니다. 이는 가능한 모든 클러스터의 멤버 자격에 대해 각 사례가 평가되는데 일부 클러스터의 경우 최소 지지도만 있을 수 있기 때문입니다.  
  
 기본값은 1입니다.  
  
 MODELLING_CARDINALITY  
 클러스터링 프로세스 중 생성되는 샘플 모델 수를 지정합니다.  
  
 후보 모델 수를 줄이면 성능은 향상되지만 뛰어난 일부 후보 모델을 놓칠 수 있는 위험이 있습니다.  
  
 기본값은 10입니다.  
  
 STOPPING_TOLERANCE  
 일치 상태에 도달하고 알고리즘이 모델 작성을 마치는 시기를 결정하는 데 사용되는 값을 지정합니다. 클러스터 확률의 전체 변경 비율이 STOPPING_TOLERANCE  매개 변수를 모델 크기로 나눈 비율보다 작으면 일치 상태에 도달합니다.  
  
 기본값은 10입니다.  
  
 SAMPLE_SIZE  
 CLUSTERING_METHOD  매개 변수가 확장 가능한 클러스터링 메서드 중 하나로 설정될 경우 각 패스에서 알고리즘이 사용하는 사례 수를 지정합니다. SAMPLE_SIZE  매개 변수를 0으로 설정하면 전체 데이터 집합이 단일 패스로 클러스터링되어 단일 패스로 전체 데이터 집합을 로드하면 메모리 및 성능 문제가 발생할 수 있습니다.  
  
 기본값은 50000입니다.  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 기능 선택을 호출하기 전에 알고리즘이 처리할 수 있는 최대 입력 특성 수를 지정합니다. 이 값을 0으로 설정하면 최대 특성 수가 없는 것으로 지정됩니다.  
  
 특성 수를 늘리면 성능이 상당히 저하될 수 있습니다.  
  
 기본값은 255입니다.  
  
 MAXIMUM_STATES  
 알고리즘이 지원하는 최대 특성 상태 수를 지정합니다. 특성 상태 수가 최대값보다 많으면 알고리즘은 가장 일반적인 상태를 사용하고 나머지 상태는 무시합니다.  
  
 상태 수를 늘리면 성능이 상당히 저하될 수 있습니다.  
  
 기본값은 100입니다.  
  
### <a name="modeling-flags"></a>모델링 플래그  
 알고리즘은 다음과 같은 모델링 플래그를 지원합니다. 모델링 플래그는 마이닝 구조나 마이닝 모델을 만들 때 정의할 수 있으며, 분석 중 각 열의 값이 처리되는 방식을 지정합니다.  
  
|모델링 플래그|Description|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|열이 Missing 및 Existing 상태를 갖는 것으로 간주됩니다. Null은 누락 값입니다.<br /><br /> 마이닝 모델 열에 적용됩니다.|  
|NOT NULL|이 열에는 Null이 포함될 수 없습니다. 따라서 Analysis Services가 모델 학습 중 Null을 발견할 경우 오류가 발생합니다.<br /><br /> 마이닝 구조 열에 적용됩니다.|  
  
## <a name="requirements"></a>요구 사항  
 클러스터링 모델은 키 열 및 입력 열을 포함해야 합니다. 입력 열을 예측 가능한 열로 정의할 수도 있습니다. **Predict Only** 로 설정된 열은 클러스터를 작성하는 데 사용되지 않습니다. 클러스터의 이러한 값 분포는 클러스터가 작성된 다음에 계산됩니다.  
  
### <a name="input-and-predictable-columns"></a>입력 열과 예측 가능한 열  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘은 다음 표에 나열된 특정 입력 열과 예측 가능한 열을 지원합니다. 마이닝 모델에 사용되는 경우 콘텐츠 형식의 의미에 대한 자세한 내용은 [콘텐츠 형식&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/content-types-data-mining.md)을 참조하세요.  
  
|Column|내용 유형|  
|------------|-------------------|  
|입력 특성|Continuous,  Cyclical,  Discrete,  Discretized,  Key,  Table,  Ordered|  
|예측 가능한 특성|Continuous,  Cyclical,  Discrete,  Discretized,  Table,  Ordered|  
  
> [!NOTE]  
>  Cyclical  및 Ordered  내용 유형이 지원되기는 하지만 알고리즘은 해당 유형을 불연속 값으로 처리하고 특수한 처리를 수행하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft 클러스터링 알고리즘](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)   
 [클러스터링 모델 쿼리 예제](../../analysis-services/data-mining/clustering-model-query-examples.md)   
 [클러스터링 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
  
