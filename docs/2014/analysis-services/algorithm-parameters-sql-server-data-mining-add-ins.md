---
title: 알고리즘 매개 변수 (SQL Server 데이터 마이닝 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_STATES
- FORCED_REGRESSOR
- PERIODICITY_HINT
- HOLDOUT_SEED
- MAXIMUM_ITEMSET_SIZE
- HIDDEN_NODE_RATIO
- CLUSTERING_METHOD
- FORECAST_METHOD
- STOPPING_TOLERANCE
- MISSING_VALUE_SUBSTITUTION
- MINIMUM_IMPORTANCE
- HISTORIC_MODEL_COUNT
- SPLIT_METHOD
- MAXIMUM_OUTPUT_ATTRIBUTES
- HOLDOUT_PERCENTAGE
- MINIMUM_PROBABILITY
- SAMPLE_SIZE
- HISTORICAL_MODEL_GAP
- CLUSTER_SEED
- SCORE_METHOD
- INSTABILITY_SENSITIVITY
- AUTO_DETECT_PERIODICITY
- MAXIMUM_SEQUENCE_STATES
- MINIMUM_DEPENDENCY_PROBABILITY
- MINIMUM_SUPPORT
- MAXIMUM_SUPPORT
- MINIMUM_ITEMSET_SIZE
- PREDICTION_SMOOTHING
- algorithm parameters
- MAXIMUM_SERIES_VALUE
- MODELLING_CARDINALITY
- MAXIMUM_INPUT_ATTRIBUTES
- MINIMUM_SERIES_VALUE
- MAXIMUM_ITEMSET_COUNT
- CLUSTER_COUNT
- COMPLEXITY_PENALTY
ms.assetid: fcdc3f85-813d-4279-90b0-16e26edd008d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e902272c58f1e841a3108199e53d51ac12f8ae4a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062594"
---
# <a name="algorithm-parameters-sql-server-data-mining-add-ins"></a>알고리즘 매개 변수(SQL Server 데이터 마이닝 추가 기능)
  Excel용 테이블 분석 도구를 사용하여 데이터 마이닝을 수행하는 경우 데이터 마이닝 알고리즘이나 매개 변수를 구성할 필요가 없습니다. 각 도구에서 데이터를 분석하여 최적의 매개 변수를 자동으로 선택합니다. 그러나 모델을 수정하거나 마이닝 모델을 새로 만들려는 경우 Excel용 데이터 마이닝 클라이언트는 사용자가 지정할 수 있는 몇 가지 옵션을 제공합니다.  
  
-   **고급** 을 클릭 한 다음 **구조에 모델 추가**를 클릭 하 여 데이터 마이닝 모델을 수동으로 만듭니다.  
  
-   데이터 마이닝 클라이언트의 모델링 마법사 중 하나를 사용 하 고 **매개 변수** 를 클릭 하 여 [!INCLUDE[msCoName](../includes/msconame-md.md)] 데이터 마이닝 알고리즘의 동작을 제어 합니다.  
  
-   **쿼리** 를 클릭 하 여 모델 쿼리 마법사를 연 다음 **고급** 을 클릭 하 여 **데이터 마이닝 고급 쿼리 편집기**를 엽니다. 이 편집기에서는 DMX 템플릿을 사용하여 모델을 작성할 수 있습니다.  
  
 마이닝 모델 뷰어에서 매개 변수를 설정하여 이미 만든 마이닝 모델의 동작을 수정하거나 결과를 필터링할 수도 있습니다.  
  
## <a name="list-of-algorithm-parameters"></a>알고리즘 매개 변수 목록  
 매개 변수를 설정하면 모든 [!INCLUDE[msCoName](../includes/msconame-md.md)] 알고리즘을 사용자 지정할 수 있습니다. 최상의 매개 변수 설정은 데이터 컴퍼지션에 따라 달라지기 때문에 이 항목에서는 매개 변수 변경에 따른 영향에 대해 자세히 설명하지 않습니다.  
  
 다음 표에서는 매개 변수를 나열하고 매개 변수의 기능에 대해 설명하며 자세한 기술 정보에 대한 링크를 제공합니다.  
  
|매개 변수 이름|사용 위치|Description|  
|--------------------|-------------|-----------------|  
|AUTO_DETECT_PERIODICITY|Microsoft Time Series 알고리즘|주기성을 찾는 데 사용되는 0과 1 사이의 숫자 값을 지정합니다. 이 값을 1에 가깝게 설정하면 거의 주기적인 패턴을 다양하게 검색하고 주기 힌트를 자동으로 생성할 수 있습니다. 많은 주기 힌트를 처리할수록 모델 학습 시간은 현저하게 길어지지만 보다 정확한 모델을 만들 수 있습니다. 이 값을 0에 가깝게 설정하면 주기성이 강한 데이터에 대해서만 주기성을 검색합니다.<br /><br /> 기본값은 0.6입니다.|  
|CLUSTER_COUNT|Microsoft Clustering Algorithm<br /><br /> Microsoft 시퀀스 클러스터링 알고리즘|알고리즘에서 작성할 클러스터의 대략적인 개수를 지정합니다. 데이터에서 대략적인 개수의 클러스터를 작성할 수 없는 경우 알고리즘은 가능한 한 많은 클러스터를 작성합니다. CLUSTER_COUNT를 0으로 설정하면 알고리즘은 추론을 사용하여 작성할 클러스터의 수를 정확하게 결정합니다.<br /><br /> 기본값은 10입니다.|  
|CLUSTER_SEED|Microsoft Clustering Algorithm|모델 작성 초기 단계에서 임의로 클러스터를 생성하는 데 사용되는 초기값을 지정합니다.<br /><br /> 기본값은 0입니다.|  
|CLUSTERING_METHOD|Microsoft Clustering Algorithm|알고리즘에서 사용할 클러스터링 메서드를 지정합니다. 다음 클러스터링 메서드를 사용할 수 있습니다. 확장 가능한 EM (1), 확장 불가능 EM (2), 확장 가능한 K-의미 (3) 및 확장 가능 하지 않은 K-(4).<br /><br /> 기본값은 1입니다.|  
|COMPLEXITY_PENALTY|Microsoft 의사 결정 트리 알고리즘<br /><br /> Microsoft Time Series 알고리즘|의사 결정 트리의 증가를 제어합니다. 낮은 값을 지정하면 분할 수가 증가되고 높은 값을 지정하면 분할 수가 감소됩니다. 기본값은 다음 목록에 설명된 것과 같이 특정 모델의 특성 수에 따라 달라집니다.<br /><br /> 특성 수가 1에서 9 사이인 경우 기본값은 0.5입니다.<br /><br /> 특성 수가 10에서 99 사이인 경우 기본값은 0.9입니다.<br /><br /> 특성 수가 100 이상인 경우 기본값은 0.99입니다.<br /><br /> 참고: 시계열 모델에서이 매개 변수는 ARTxp 알고리즘 또는 혼합 모델을 사용 하 여 작성 된 모델에만 적용 됩니다.|  
|FORCED_REGRESSOR|Microsoft 의사 결정 트리 알고리즘<br /><br /> Microsoft 선형 회귀 알고리즘|알고리즘에서 계산한 열의 중요도에 관계없이 알고리즘에서 표시된 열을 회귀 변수로 사용하도록 합니다.<br /><br /> 참고:이 매개 변수는 연속 특성을 예측 하는 의사 결정 트리에만 사용 됩니다. 정의에 따르면 선형 회귀 모델은 연속 특성을 예측하는 특수한 사례의 의사 결정 트리입니다. 그러나 의사 결정 트리 모델은 선형 회귀 수식을 나타내는 노드를 포함할 수 있습니다.|  
|FORECAST_METHOD|Microsoft Time Series 알고리즘|ARTxp 알고리즘, ARIMA 알고리즘 또는 두 알고리즘의 조합을 사용하여 예측을 수행할지 여부를 나타냅니다.<br /><br /> 기본값은 MIXED입니다.|  
|HIDDEN_NODE_RATIO|Microsoft Neural Network Algorithm|입력 및 출력 뉴런에 대한 숨겨진 뉴런의 비율을 지정합니다. 다음 수식에서는 숨겨진 계층의 초기 뉴런 수를 결정합니다.<br /><br /> HIDDEN_NODE_RATIO * SQRT(총 입력 뉴런 \* 총 출력 뉴런)<br /><br /> 기본값은 4.0입니다.|  
|HISTORIC_MODEL_COUNT|Microsoft Time Series 알고리즘|작성할 기록 모델 수를 지정합니다.<br /><br /> 기본값은 1입니다.|  
|HISTORICAL_MODEL_GAP|Microsoft Time Series 알고리즘|두 연속 기록 모델 간의 지연 시간을 지정합니다. 예를 들어 이 값을 g로 설정하면 g, 2*g, 3\*g 등의 시간 간격으로 데이터를 잘라 기록 모델을 작성합니다.<br /><br /> 기본값은 10입니다.|  
|HOLDOUT_PERCENTAGE|Microsoft 로지스틱 회귀 알고리즘<br /><br /> Microsoft Neural Network Algorithm|홀드아웃 오류를 계산하는 데 사용되는 학습 데이터 내의 사례 비율을 지정합니다. 이 비율은 마이닝 모델 학습 중 중지 조건의 일부로 사용됩니다.<br /><br /> 기본값은 30입니다.<br /><br /> 참고: 이 매개 변수는 마이닝 구조에 적용되는 홀드아웃 백분율 값과는 다릅니다.|  
|HOLDOUT_SEED|Microsoft 로지스틱 회귀 알고리즘<br /><br /> Microsoft Neural Network Algorithm|알고리즘이 홀드아웃 데이터를 임의로 결정할 때 난수 생성기의 초기값으로 사용할 숫자를 지정합니다. 이 매개 변수를 0으로 설정하면 알고리즘은 마이닝 모델의 이름을 기반으로 초기값을 생성하여 다시 처리하는 동안 모델 콘텐츠가 동일하게 유지되도록 합니다.<br /><br /> 기본값은 0입니다.<br /><br /> 참고: 이 매개 변수는 마이닝 구조에 적용되는 홀드아웃 초기값과는 다릅니다.|  
|INSTABILITY_SENSITIVITY|Microsoft Time Series 알고리즘|예측 분산이 특정 임계값을 초과하여 ARTxp 알고리즘이 예측을 표시하지 않는 지점을 제어합니다. 기본값은 1입니다.<br /><br /> 참고:이 매개 변수는 혼합 모델 또는 ARTxp 알고리즘을 사용 하는 모델에만 적용 됩니다.|  
|MAXIMUM_INPUT_ATTRIBUTES|Microsoft Clustering Algorithm<br /><br /> Microsoft 의사 결정 트리 알고리즘<br /><br /> Microsoft 선형 회귀 알고리즘<br /><br /> Microsoft Naive Bayes 알고리즘<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Microsoft 로지스틱 회귀 알고리즘|기능 선택을 호출하기 전에 알고리즘이 처리할 수 있는 입력 특성 수를 정의합니다. 이 값을 0으로 설정하면 기능 선택이 해제됩니다.<br /><br /> 기본값은 255입니다.|  
|MAXIMUM_ITEMSET_COUNT|Microsoft 연결 알고리즘|생성할 최대 항목 집합 수를 지정합니다. 이 값을 지정하지 않으면 알고리즘이 가능한 모든 항목 집합을 생성합니다.<br /><br /> 기본값은 200000입니다.|  
|MAXIMUM_ITEMSET_SIZE|Microsoft 연결 알고리즘|항목 집합에 사용할 수 있는 최대 항목 수를 지정합니다. 이 값을 0으로 설정하면 항목 집합 크기가 무제한으로 지정됩니다.<br /><br /> 기본값은 3입니다.|  
|MAXIMUM_OUTPUT_ATTRIBUTES|Microsoft 의사 결정 트리 알고리즘<br /><br /> Microsoft 선형 회귀 알고리즘<br /><br /> Microsoft 로지스틱 회귀 알고리즘<br /><br /> Microsoft Naive Bayes 알고리즘<br /><br /> Microsoft Neural Network Algorithm|기능 선택을 호출하기 전에 알고리즘이 처리할 수 있는 출력 특성 수를 정의합니다. 이 값을 0으로 설정하면 기능 선택이 해제됩니다.<br /><br /> 기본값은 255입니다.|  
|MAXIMUM_SEQUENCE_STATES|Microsoft 시퀀스 클러스터링 알고리즘|시퀀스에 포함할 수 있는 최대 상태 수를 지정합니다. 이 값을 100보다 큰 숫자로 설정하면 알고리즘은 의미 없는 정보를 제공하는 모델을 작성합니다.<br /><br /> 기본값은 64입니다.|  
|MAXIMUM_SERIES_VALUE|Microsoft Time Series 알고리즘|예측에 사용할 최대값을 지정합니다. 이 매개 변수는 MINIMUM_SERIES_VALUE와 함께 예측을 예상 범위로 제한하는 데 사용됩니다. 예를 들어 특정 일의 예상 판매 수량이 재고 제품 수를 초과하지 않도록 지정할 수 있습니다.|  
|MAXIMUM_STATES|Microsoft Clustering Algorithm<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Microsoft 시퀀스 클러스터링 알고리즘|알고리즘이 지원하는 최대 특성 상태 수를 지정합니다. 특성의 상태 수가 최대 상태 수보다 많으면 알고리즘은 특성의 가장 인기 있는 상태를 사용 하 고 나머지 상태를 무시 합니다.<br /><br /> 기본값은 100입니다.|  
|MAXIMUM_SUPPORT|Microsoft 연결 알고리즘|항목 집합을 지원할 수 있는 최대 사례 수를 지정합니다. 이 값이 1보다 작으면 총 사례의 백분율을 나타내고 이 값이 1보다 크면 항목 집합을 포함할 수 있는 사례의 절대 수를 나타냅니다.<br /><br /> 기본값은 1입니다.|  
|MINIMUM_IMPORTANCE|Microsoft 연결 알고리즘|연결 규칙의 중요도 임계값을 지정합니다. 중요도가 이 값보다 작은 규칙은 필터링되어 제외됩니다.|  
|MINIMUM_ITEMSET_SIZE|Microsoft 연결 알고리즘|항목 집합에 사용할 수 있는 최소 항목 수를 지정합니다.<br /><br /> 기본값은 1입니다.|  
|MINIMUM_DEPENDENCY_PROBABILITY|Microsoft Naive Bayes 알고리즘|입력 특성과 출력 특성 간의 최소 종속성 확률을 지정합니다. 이 값은 알고리즘에서 생성하는 내용의 크기를 제한하는 데 사용됩니다. 이 속성은 0과 1 사이의 값으로 설정할 수 있습니다. 이보다 큰 값을 지정하면 모델 내용의 특성 수가 감소합니다.<br /><br /> 기본값은 0.5입니다.|  
|MINIMUM_PROBABILITY|Microsoft 연결 알고리즘|규칙이 참이 되는 최소 확률을 지정합니다. 예를 들어 이 값을 0.5로 설정하면 확률이 50% 미만인 규칙은 생성되지 않습니다.<br /><br /> 기본값은 0.4입니다.|  
|MINIMUM_SERIES_VALUE|Microsoft Time Series 알고리즘|시계열 예측에 대한 하한 제한 조건을 지정합니다. 예측 값이 이 제약 조건보다 작을 수 없습니다.|  
|MINIMUM_SUPPORT|Microsoft 연결 알고리즘|알고리즘이 규칙을 생성하기 전에 항목 집합이 있어야 하는 최소 사례 수를 지정합니다. 이 값을 1보다 작게 설정하면 최소 사례 수가 총 사례에 대한 백분율로 지정되고 1보다 큰 정수로 설정하면 최소 사례 수가 항목 집합이 있어야 하는 사례의 절대 수로 지정됩니다. 메모리가 제한된 경우 알고리즘이 이 매개 변수의 값을 늘릴 수 있습니다.<br /><br /> 기본값은 0.03입니다.|  
|MINIMUM_SUPPORT|Microsoft Clustering Algorithm|각 클러스터의 최소 사례 수를 지정합니다.<br /><br /> 기본값은 1입니다.|  
|MINIMUM_SUPPORT|Microsoft 의사 결정 트리 알고리즘|의사 결정 트리에서 분할을 생성하는 데 필요한 최소 리프 사례 수를 결정합니다.<br /><br /> 기본값은 10입니다.|  
|MINIMUM_SUPPORT|Microsoft 시퀀스 클러스터링 알고리즘|각 클러스터의 최소 사례 수를 지정합니다.<br /><br /> 기본값은 10입니다.|  
|MINIMUM_SUPPORT|Microsoft Time Series 알고리즘|각 시계열 트리에서 분할을 생성하는 데 필요한 최소 시간 조각 수를 지정합니다.<br /><br /> 기본값은 10입니다.|  
|MISSING_VALUE_SUBSTITUTION|Microsoft Time Series 알고리즘|기록 데이터의 간격을 채우는 데 사용되는 메서드를 지정합니다. 기본적으로 데이터의 간격이나 가장자리 값은 불규칙하면 안 됩니다. 다음 메서드를 사용 하 여 불규칙 한 간격이 나 가장자리를 채울 수 있습니다. 이전 값을 사용 하거나 평균 값을 사용 하거나 특정 숫자 상수를 사용 합니다.|  
|MODELLING_CARDINALITY|Microsoft Clustering Algorithm|클러스터링 프로세스 중 생성되는 샘플 모델 수를 지정합니다.<br /><br /> 기본값은 10입니다.|  
|PERIODICITY_HINT|Microsoft Time Series 알고리즘|데이터의 주기성과 관련된 알고리즘에 대한 힌트를 제공합니다. 예를 들어 판매량이 매년 다르고 계열의 측정 단위가 월인 경우 주기성은 12입니다. 이 매개 변수는 {n [, n]} 형식이며, 여기서 n은 임의의 양수입니다. 대괄호([]) 안의 n은 선택 사항이며 필요한 만큼 반복할 수 있습니다.<br /><br /> 기본값은 {1}입니다.|  
|PREDICTION_SMOOTHING|Microsoft Time Series 알고리즘|ARTXP 및 ARIMA 시계열 알고리즘의 혼합을 제어합니다. FORECAST_METHOD 매개 변수가 MIXED로 설정된 경우에만 지정된 값이 유효합니다. 값은 0에서 1 사이여야 합니다. 값이 0이면 모델에서 ARTXP만 사용합니다. 값이 1이면 모델에서 ARIMA만 사용합니다. 값이 0에 가까울수록 ARTXP에 더 가중되고 값이 1에 가까울수록 ARIMA에 더 가중됩니다.|  
|SAMPLE_SIZE|Microsoft Clustering Algorithm|CLUSTERING_METHOD  매개 변수가 확장 가능한 클러스터링 메서드 중 하나로 설정될 경우 각 패스에서 알고리즘이 사용하는 사례 수를 지정합니다. SAMPLE_SIZE 매개 변수를 0으로 설정하면 전체 데이터 세트가 단일 패스로 클러스터됩니다. 메모리 및 성능 문제가 발생할 수 있습니다.<br /><br /> 기본값은 50000입니다.|  
|SAMPLE_SIZE|Microsoft 로지스틱 회귀 알고리즘<br /><br /> Microsoft Neural Network Algorithm|모델의 학습에 사용되는 사례 수를 지정합니다. 알고리즘 공급자는 지정한 수와 HOLDOUT_PERCENTAGE 매개 변수로 지정된 홀드아웃 비율에 포함되지 않은 총 사례 수의 비율 중 더 작은 값을 사용합니다.<br /><br /> 즉, HOLDOUT_PERCENTAGE를 30으로 설정하면 알고리즘은 이 매개 변수 값이나 총 사례 수의 70%에 해당하는 값 중 더 작은 값을 사용합니다.<br /><br /> 기본값은 10000입니다.|  
|SCORE_METHOD|Microsoft 의사 결정 트리 알고리즘|분할 점수를 계산하는 데 사용되는 메서드를 결정합니다. 다음 옵션을 사용할 수 있습니다. (1) 엔트로피, (2) Bayesian K2 이전 또는 (3) Bayesian Dirichlet 동급 (MANAGE-BDE) 이전.<br /><br /> 기본값은 3입니다.|  
|SPLIT_METHOD|Microsoft 의사 결정 트리 알고리즘|노드를 분할하는 데 사용되는 메서드를 결정합니다. 다음 옵션을 사용할 수 있습니다. Binary (1), Complete (2) 또는 Both (3).<br /><br /> 기본값은 3입니다.|  
|STOPPING_TOLERANCE|Microsoft 클러스터링 알고리즘 기술 참조|일치 상태에 도달하고 알고리즘이 모델 작성을 마치는 시기를 결정하는 데 사용되는 값을 지정합니다. 클러스터 확률의 전체 변경 비율이 STOPPING_TOLERANCE  매개 변수를 모델 크기로 나눈 비율보다 작으면 일치 상태에 도달합니다.<br /><br /> 기본값은 10입니다.|  
  
### <a name="comments"></a>주석  
 알고리즘에 대한 자세한 내용은 SQL Server 온라인 설명서를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 알고리즘은 데이터 마이닝 추가 기능 SQL Server &#40;&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md)  
  
  
