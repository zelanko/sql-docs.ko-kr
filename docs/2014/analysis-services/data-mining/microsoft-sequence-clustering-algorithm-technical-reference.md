---
title: Microsoft 시퀀스 클러스터링 알고리즘 기술 참조 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_SEQUENCE_STATES parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_STATES parameter
- sequence clustering algorithms [Analysis Services]
- CLUSTER_COUNT parameter
ms.assetid: 251c369d-6b02-4687-964e-39bf55c9b009
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d0e9e49a61bef168af2703e83d027feec1d9daa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060433"
---
# <a name="microsoft-sequence-clustering-algorithm-technical-reference"></a>Microsoft 시퀀스 클러스터링 알고리즘 기술 참조
  Microsoft 시퀀스 클러스터링 알고리즘은 Markov 체인 분석을 사용하여 정렬된 시퀀스를 식별하고, 이 분석 결과를 클러스터링 기술과 결합하여 모델의 시퀀스 및 기타 특성에 따라 클러스터를 생성하는 하이브리드 알고리즘입니다. 이 항목에서는 알고리즘의 구현, 알고리즘을 사용자 지정하는 방법 및 시퀀스 클러스터링 모델에 대한 특수한 요구 사항을 설명합니다.  
  
 시퀀스 클러스터링 모델을 찾아보고 쿼리하는 방법을 비롯하여 알고리즘에 대한 자세한 내용은 [Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md)을 참조하십시오.  
  
## <a name="implementation-of-the-microsoft-sequence-clustering-algorithm"></a>Microsoft 시퀀스 클러스터링 알고리즘 구현  
 Microsoft 시퀀스 클러스터링 모델에서는 Markov 모델을 사용하여 시퀀스를 식별하고 시퀀스의 확률을 확인합니다. Markov 모델은 여러 상태 간의 전환을 저장하는 방향 그래프입니다. Microsoft 시퀀스 클러스터링 알고리즘에서는 Hidden Markov 모델이 아니라 n차 Markov 체인을 사용합니다.  
  
 Markov 체인의 차수는 현재 상태의 확률을 확인하는 데 사용된 상태 수를 나타냅니다. 예를 들어 1차 Markov 모델에서 현재 상태의 확률은 이전 상태에 따라서만 달라지고, 2차 Markov 체인에서 상태의 확률은 이전의 두 상태에 따라 달라집니다. 각 Markov 체인의 전환 행렬에는 각 상태 조합에 대한 전환이 저장됩니다. Markov 체인의 길이가 늘어나면 행렬의 크기도 기하급수적으로 늘어나며 행렬이 매우 스파스하게 됩니다. 또한 그에 따라 처리 시간도 늘어납니다.  
  
 사이트의 웹 페이지 방문을 분석하는 클릭 동향 분석 예를 사용하여 체인을 시각화하면 매우 유용할 수 있습니다. 각 사용자는 각 세션에 대해 긴 클릭 시퀀스를 생성합니다. 모델을 만들어 웹 사이트에서의 사용자 동작을 분석할 경우 학습에 사용되는 데이터 집합은 URL의 시퀀스로서, 이는 동일한 클릭 경로의 모든 인스턴스 수를 포함하는 그래프로 변환됩니다. 예를 들어 이 그래프에는 사용자가 1페이지에서 2페이지로 이동하는 확률(10%), 1페이지에서 3페이지로 이동하는 확률(20%) 등이 포함됩니다. 가능한 모든 경로와 부분 경로를 함께 포함하면 관찰된 단일 경로보다 길고 복잡한 그래프가 생성됩니다.  
  
 기본적으로 Microsoft 시퀀스 클러스터링 알고리즘에서는 EM(Expectation Maximization) 클러스터링 방법을 사용합니다. 자세한 내용은 [Microsoft 클러스터링 알고리즘 기술 참조](microsoft-clustering-algorithm-technical-reference.md)를 참조하세요.  
  
 순차적 특성과 비순차적 특성이 모두 클러스터링 대상이 됩니다. 각 클러스터는 확률 분포를 사용하여 무작위로 선택됩니다. 각 클러스터에는 전체 경로 집합을 나타내는 Markov 체인과 시퀀스 상태 전환 및 확률이 들어 있는 행렬이 포함됩니다. 초기 분포에 따라 특정 클러스터에 있는 특성의 확률(시퀀스 포함)을 계산하는 데는 Bayes 규칙이 사용됩니다.  
  
 Microsoft 시퀀스 클러스터링 알고리즘에서는 모델에 비순차적 특성을 추가할 수 있습니다. 일반적인 클러스터링 모델에서와 마찬가지로 이러한 추가 특성은 순차적 특성과 결합되어 비슷한 특성이 있는 사례의 클러스터를 생성합니다.  
  
 시퀀스 클러스터링 모델은 일반적인 클러스터링 모델보다 더 많은 클러스터를 만드는 경향이 있습니다. 따라서 Microsoft 시퀀스 클러스터링 알고리즘은 *클러스터 분해*를 수행하여 시퀀스 및 기타 특성에 따라 클러스터를 분리합니다.  
  
### <a name="feature-selection-in-a-sequence-clustering-model"></a>시퀀스 클러스터링 모델의 기능 선택  
 시퀀스를 작성할 때는 기능 선택이 호출되지 않지만 클러스터링 단계에서 기능 선택이 적용됩니다.  
  
|모델 유형|기능 선택 방법|주석|  
|----------------|------------------------------|--------------|  
|시퀀스 클러스터링|사용되지 않음|기능 선택이 호출되지 않습니다. 그러나 MINIMUM_SUPPORT 및 MINIMUM_PROBABILIITY 매개 변수의 값을 설정하여 알고리즘의 동작을 제어할 수 있습니다.|  
|Clustering|흥미도 점수|클러스터링 알고리즘은 불연속 또는 불연속화된 알고리즘을 사용할 수 있지만 각 특성의 점수는 거리로 계산되며 연속적입니다. 따라서 흥미도 점수가 사용됩니다.|  
  
 자세한 내용은 [Feature Selection](../../sql-server/install/feature-selection.md)을 참조하세요.  
  
### <a name="optimizing-performance"></a>성능 최적화  
 Microsoft 시퀀스 클러스터링 알고리즘에서는 다양한 방법으로 처리를 최적화할 수 있습니다.  
  
-   CLUSTER_COUNT 매개 변수의 값을 설정하여 생성되는 클러스터 수를 제어합니다.  
  
-   MINIMUM_SUPPORT 매개 변수의 값을 늘려 특성으로 포함되는 시퀀스 수를 줄입니다. 그 결과 빈도가 낮은 시퀀스는 제거됩니다.  
  
-   모델을 처리하기 전에 관련 특성을 그룹화하여 복잡성을 줄입니다.  
  
 일반적으로 다음과 같은 몇 가지 방법으로 n차 Markov 체인 모드의 성능을 최적화할 수 있습니다.  
  
-   가능한 시퀀스의 길이를 제어합니다.  
  
-   프로그래밍 방식으로 n 값을 줄입니다.  
  
-   지정된 임계값을 초과하는 확률만 저장합니다.  
  
 이러한 방법에 대한 자세한 설명은 이 항목에서는 다루지 않습니다.  
  
## <a name="customizing-the-sequence-clustering-algorithm"></a>시퀀스 클러스터링 알고리즘 사용자 지정  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘은 결과 마이닝 모델의 동작, 성능 및 정확도에 영향을 주는 매개 변수를 지원합니다. 알고리즘의 학습 데이터 처리 방식을 제어하는 모델링 플래그를 설정하여 완성된 모델의 동작을 수정할 수도 있습니다.  
  
### <a name="setting-algorithm-parameters"></a>알고리즘 매개 변수 설정  
 다음 표에서는 Microsoft 시퀀스 클러스터링 알고리즘에서 사용할 수 있는 매개 변수에 대해 설명합니다.  
  
 CLUSTER_COUNT  
 알고리즘에서 작성할 클러스터의 대략적인 개수를 지정합니다. 데이터에서 대략적인 개수의 클러스터를 작성할 수 없는 경우 알고리즘은 가능한 한 많은 클러스터를 작성합니다. CLUSTER_COUNT 매개 변수를 0으로 설정하면 알고리즘은 경험적 접근을 사용하여 작성할 최적의 클러스터 수를 결정합니다.  
  
 기본값은 10입니다.  
  
> [!NOTE]  
>  0이 아닌 숫자를 지정하면 알고리즘에서는 지정된 개수를 찾고자 시도하지만 최종적으로 찾는 개수는 그보다 많을 수도 있고 적을 수도 있습니다.  
  
 MINIMUM_SUPPORT  
 특성을 지원하며 클러스터를 만드는 데 필요한 최소 사례 수를 지정합니다.  
  
 기본값은 10입니다.  
  
 MAXIMUM_SEQUENCE_STATES  
 시퀀스에 포함할 수 있는 최대 상태 수를 지정합니다.  
  
 이 값을 100보다 큰 숫자로 설정하면 알고리즘은 의미 없는 정보를 제공하는 모델을 작성합니다.  
  
 기본값은 64입니다.  
  
 MAXIMUM_STATES  
 알고리즘이 지원하는 비시퀀스 특성에 대한 최대 상태 수를 지정합니다. 알고리즘은 특성의 가장 일반적인 상태 하 고 나머지 상태를 취급 비시퀀스 특성의 상태 수가 최대 상태 수보다 크면 `Missing`합니다.  
  
 기본값은 100입니다.  
  
### <a name="modeling-flags"></a>모델링 플래그  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘에서 지원되는 모델링 플래그는 다음과 같습니다.  
  
 NOT NULL  
 열에 null이 포함될 수 없음을 나타냅니다. 따라서 Analysis Services가 모델 학습 중 Null을 발견할 경우 오류가 발생합니다.  
  
 마이닝 구조 열에 적용됩니다.  
  
 MODEL_EXISTENCE_ONLY  
 열 수 있는 방법을 두 가지 가능한 상태를 가진 것으로 처리 합니다. `Missing` 및 `Existing`합니다. Null로 처리 되는 `Missing` 값입니다.  
  
 마이닝 모델 열에 적용됩니다.  
  
 마이닝 모델에서의 누락 값 사용과 누락 값이 확률 점수에 주는 영향에 대한 자세한 내용은 [누락 값&#40;Analysis Services - 데이터 마이닝&#41;](missing-values-analysis-services-data-mining.md)을 참조하세요.  
  
## <a name="requirements"></a>요구 사항  
 사례 테이블에는 사례 ID 열이 있어야 합니다. 필요에 따라 사례에 대한 특성을 저장하는 다른 열도 사례 테이블에 포함될 수 있습니다.  
  
 Microsoft 시퀀스 클러스터링 알고리즘을 사용하려면 중첩 테이블로 저장된 시퀀스 정보가 필요합니다. 중첩 테이블에는 단일 Key Sequence 열이 있어야 합니다. `Key Sequence` 열 모든 종류의 정렬할 수 있는, 문자열 데이터 형식을 비롯 한 데이터를 포함할 수 있지만 열의 각 사례에 대해 고유한 값을 포함 해야 합니다. 또한 모델을 처리하기 전에 사례 테이블과 중첩 테이블이 모두 해당 테이블과 관련된 키를 기준으로 오름차순으로 정렬되도록 해야 합니다.  
  
> [!NOTE]  
>  Microsoft 시퀀스 알고리즘을 사용하는 모델을 만들면서 시퀀스 열은 사용하지 않을 경우 결과 모델은 시퀀스를 포함하지 않고 단지 모델에 포함된 다른 특성에 따라 사례를 클러스터링하기만 합니다.  
  
### <a name="input-and-predictable-columns"></a>입력 열과 예측 가능한 열  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘은 다음 표에 나열된 특정 입력 열과 예측 가능한 열을 지원합니다. 마이닝 모델에 사용되는 경우 콘텐츠 형식의 의미에 대한 자세한 내용은 [콘텐츠 형식&#40;데이터 마이닝&#41;](content-types-data-mining.md)을 참조하세요.  
  
|Column|내용 유형|  
|------------|-------------------|  
|입력 특성|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Table 및 Ordered|  
|예측 가능한 특성|Continuous, Cyclical, Discrete, Discretized, Table 및 Ordered|  
  
## <a name="remarks"></a>Remarks  
  
-   시퀀스 예측에 대한 [PredictSequence&#40;DMX&#41;](/sql/dmx/predictsequence-dmx) 함수를 사용합니다. 버전에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시퀀스 예측을 지원 하는 참조 하십시오 [SQL Server 2012 버전에서 지 원하는 기능](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473)합니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘에서는 PMML(Predictive Model Markup Language)을 사용하여 마이닝 모델을 만들 수 없습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘에서는 드릴스루, OLAP 마이닝 모델 사용 및 데이터 마이닝 차원 사용을 지원합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 시퀀스 클러스터링 알고리즘](microsoft-sequence-clustering-algorithm.md)   
 [시퀀스 클러스터링 모델 쿼리 예제](clustering-model-query-examples.md)   
 [마이닝 모델 콘텐츠 시퀀스 클러스터링 모델에 대 한 &#40;Analysis Services-데이터 마이닝&#41;](mining-model-content-for-sequence-clustering-models.md)  
  
  
