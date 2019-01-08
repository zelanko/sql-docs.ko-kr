---
title: 마이닝 모델 콘텐츠 (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- standard deviation
- confidence scores [data mining]
- mining models [Analysis Services]
- variance
- machine learning algorithms [Analysis Services]
- model content
- support [data mining]
- node distribution
ms.assetid: e7c039f6-3266-4d84-bfbd-f99b6858acf4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a0cb21136253767f009cb19604c8a0ea7e4c71a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52503397"
---
# <a name="mining-model-content-analysis-services---data-mining"></a>마이닝 모델 콘텐츠(Analysis Services - 데이터 마이닝)
  기본 마이닝 구조의 데이터를 사용하여 마이닝 모델을 디자인하고 처리하고 나면 마이닝 모델이 완성되고 마이닝 모델에 *마이닝 모델 콘텐츠*가 포함됩니다. 이 콘텐츠를 사용하여 예측을 만들거나 데이터를 분석할 수 있습니다.  
  
 마이닝 모델 콘텐츠에는 모델에 대한 메타데이터, 데이터에 대한 통계 및 마이닝 알고리즘을 통해 발견한 패턴이 포함됩니다. 사용된 알고리즘에 따라 모델 콘텐츠에는 회귀 수식, 규칙 및 항목 집합의 정의, 가중치 또는 기타 통계가 포함될 수 있습니다.  
  
 사용된 알고리즘에 관계없이 마이닝 모델 콘텐츠는 표준 구조로 표시됩니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 제공하는 Microsoft 일반 콘텐츠 트리 뷰어에서 구조를 탐색한 다음 사용자 지정 뷰어 중 하나로 전환하여 모델 유형에 따라 정보가 해석되고 그래픽으로 표시되는 방법을 확인할 수 있습니다. 또한 MINING_MODEL_CONTENT 스키마 행 집합을 지원하는 클라이언트를 사용하여 마이닝 모델 콘텐츠에 대한 쿼리를 만들 수도 있습니다. 자세한 내용은 [데이터 마이닝 쿼리 태스크 및 방법](data-mining-query-tasks-and-how-tos.md)을 참조하세요.  
  
 이 섹션에서는 모든 종류의 마이닝 모델에 제공되는 콘텐츠의 기본 구조에 대해 설명합니다. 또한 이 섹션에서는 모든 마이닝 모델에 공통된 노드 유형에 대해 설명하고 정보를 해석하는 방법에 대한 지침을 제공합니다.  
  
 [마이닝 모델 콘텐츠의 구조](#bkmk_Structure)  
  
 [모델 콘텐츠의 노드](#bkmk_Nodes)  
  
 [알고리즘 유형별 마이닝 모델 콘텐츠](#bkmk_AlgoType)  
  
 [마이닝 모델 콘텐츠를 보기 위한 도구](#bkmk_Viewing)  
  
 [마이닝 모델 콘텐츠를 쿼리하기 위한 도구](#bkmk_Querying)  
  
##  <a name="bkmk_Structure"></a> 마이닝 모델 콘텐츠의 구조  
 각 모델의 콘텐츠는 일련의 *노드*로 표시됩니다. 노드는 모델의 특정 부분에 대한 메타데이터 및 정보를 포함하는 마이닝 모델 개체이며 계층 구조로 정렬됩니다. 계층 구조에 노드를 정확히 배열하는 방법과 계층 구조의 의미는 사용된 알고리즘에 따라 다릅니다. 예를 들어 의사 결정 트리 모델을 만들면 모두 모델 루트에 연결된 여러 트리가 모델에 포함될 수 있고 신경망 모델을 만들면 하나 이상의 네트워크와 하나의 정적 노드가 모델에 포함될 수 있습니다.  
  
 각 모델의 첫 번째 노드는 *루트 노드*또는 *모델 부모* 노드라고 합니다. 모든 모델에는 루트 노드(NODE_TYPE = 1)가 있습니다. 일반적으로 루트 노드에는 모델에 대한 몇 가지 메타데이터와 자식 노드 개수가 포함되지만 모델에서 발견되는 패턴에 대한 추가 정보는 거의 포함되지 않습니다.  
  
 루트 노드의 자식 노드 개수는 모델을 만드는 데 사용된 알고리즘에 따라 달라집니다. 자식 노드의 의미와 내용은 이러한 알고리즘뿐 아니라 데이터의 깊이와 복잡도에 의해 결정됩니다.  
  
##  <a name="bkmk_Nodes"></a> 마이닝 모델 콘텐츠의 노드  
 마이닝 모델에서 노드는 모델의 전부 또는 일부에 대한 정보를 저장하는 범용 컨테이너입니다. 각 노드의 구조는 항상 동일하며 데이터 마이닝 스키마 행 집합으로 정의된 열을 포함합니다. 자세한 내용은 [DMSCHEMA_MINING_MODEL_CONTENT 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)을 참조하세요.  
  
 각 노드에는 각 모델 내에서 고유한 식별자를 포함하는 노드에 대한 메타데이터, 보모 노드의 ID 및 노드에 있는 자식 노드 개수가 포함됩니다. 메타데이터는 노드가 속한 모델과 특정 모델이 저장되는 데이터베이스 카탈로그를 식별합니다. 노드에 제공되는 추가 내용은 모델을 만드는 데 사용된 알고리즘의 유형에 따라 다르며, 여기에는 다음이 포함될 수 있습니다.  
  
-   특정 예측 값을 지원하는 학습 데이터의 사례 수  
  
-   평균, 표준 편차 또는 분산과 같은 통계  
  
-   계수 및 수식  
  
-   규칙 및 측면 포인터에 대한 정의  
  
-   모델의 특정 부분을 나타내는 XML 조각  
  
### <a name="list-of-mining-content-node-types"></a>마이닝 콘텐츠 노드 유형 목록  
 다음 표에서는 데이터 마이닝 모델에 출력되는 다양한 유형의 노드를 보여 줍니다. 알고리즘마다 정보를 처리하는 방법이 다르기 때문에 각 모델은 몇 개의 특정 종류의 노드만 생성합니다. 알고리즘을 변경하면 노드 유형이 변경될 수 있습니다. 또한 모델을 다시 처리하면 각 노드의 내용이 변경될 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]에서 제공하는 것과 다른 데이터 마이닝 서비스를 사용하거나 사용자 고유의 플러그 인 알고리즘을 만드는 경우 추가 사용자 지정 노드 유형을 사용할 수 있습니다.  
  
|NODE_TYPE ID|노드 레이블|노드 내용|  
|-------------------|----------------|-------------------|  
|1|Model|메타데이터 및 루트 내용 노드입니다. 모든 모델 유형에 적용됩니다.|  
|2|trEE|분류 트리의 루트 노드입니다. 의사 결정 트리 모델에 적용됩니다.|  
|3|내부|트리의 내부 분할 노드입니다. 의사 결정 트리 모델에 적용됩니다.|  
|4|배포|트리의 터미널 노드입니다. 의사 결정 트리 모델에 적용됩니다.|  
|5|클러스터|알고리즘을 통해 검색되는 클러스터입니다. 클러스터링 모델 및 시퀀스 클러스터링 모델에 적용됩니다.|  
|6|알 수 없음|알 수 없는 노드 유형입니다.|  
|7|항목 집합|알고리즘을 통해 검색되는 항목 집합입니다. 연결 모델 및 시퀀스 클러스터링 모델에 적용됩니다.|  
|8|AssociationRule|알고리즘을 통해 검색되는 연결 규칙입니다. 연결 모델 및 시퀀스 클러스터링 모델에 적용됩니다.|  
|9|PredictableAttribute|예측 가능한 특성입니다. 모든 모델 유형에 적용됩니다.|  
|10|InputAttribute|입력 특성입니다. 의사 결정 트리 및 Naïve Bayes 모델에 적용됩니다.|  
|11|InputAttributeState|입력 특성의 상태에 대한 통계입니다. 의사 결정 트리 및 Naïve Bayes 모델에 적용됩니다.|  
|13|시퀀스|시퀀스 클러스터의 Markov 모델 구성 요소에 대한 최상위 노드입니다. 시퀀스 클러스터링 모델에 적용됩니다.|  
|14|전환|Markov 전환 행렬입니다. 시퀀스 클러스터링 모델에 적용됩니다.|  
|15|TimeSeries|시계열 트리의 루트가 아닌 노드입니다. 시계열 모델에만 적용됩니다.|  
|16|TsTree|예측 가능한 시계열에 해당하는 시계열 트리의 루트 노드입니다. MIXED 매개 변수를 사용하여 모델을 만든 경우에만 시계열 모델에 적용됩니다.|  
|17|NNetSubnetwork|하나의 하위 네트워크입니다. 신경망 모델에 적용됩니다.|  
|18|NNetInputLayer|입력 계층의 노드가 포함된 그룹입니다. 신경망 모델에 적용됩니다.|  
|19|NNetHiddenLayer|숨겨진 계층을 나타내는 노드가 포함된 그룹입니다. 신경망 모델에 적용됩니다.|  
|21|NNetOutputLayer|출력 계층의 노드가 포함된 그룹입니다. 신경망 모델에 적용됩니다.|  
|21|NNetInputNode|입력 특성과 해당 상태를 일치시키는 입력 계층의 노드입니다. 신경망 모델에 적용됩니다.|  
|22|NNetHiddenNode|숨겨진 계층의 노드입니다. 신경망 모델에 적용됩니다.|  
|23|NNetOutputNode|출력 계층의 노드입니다. 일반적으로 이 노드는 출력 특성과 해당 상태를 일치시킵니다. 신경망 모델에 적용됩니다.|  
|24|NNetMarginalNode|학습 집합에 대한 한계 통계입니다. 신경망 모델에 적용됩니다.|  
|25|RegressionTreeRoot|회귀 트리의 루트입니다. 연속 입력 특성이 포함된 의사 결정 트리 모델 및 선형 회귀 모델에 적용됩니다.|  
|26|NaiveBayesMarginalStatNode|학습 집합에 대한 한계 통계입니다. Naïve Bayes 모델에 적용됩니다.|  
|27|ArimaRoot|ARIMA 모델의 루트 노드입니다. ARIMA 알고리즘을 사용하는 시계열 모델에만 적용됩니다.|  
|28|ArimaPeriodicStructure|ARIMA 모델의 주기 구조입니다. ARIMA 알고리즘을 사용하는 시계열 모델에만 적용됩니다.|  
|29|ArimaAutoRegressive|ARIMA 모델의 단일 용어에 대한 자동 회귀 계수입니다.<br /><br /> ARIMA 알고리즘을 사용하는 시계열 모델에만 적용됩니다.|  
|30|ArimaMovingAverage|ARIMA 모델의 단일 용어에 대한 이동 평균 계수입니다. ARIMA 알고리즘을 사용하는 시계열 모델에만 적용됩니다.|  
|1000|CustomBase|사용자 지정 노드 유형의 시작 지점입니다. 사용자 지정 노드 유형의 값은 이 상수보다 큰 정수여야 합니다. 사용자 지정 플러그 인 알고리즘을 사용하여 만든 모델에 적용됩니다.|  
  
### <a name="node-id-name-caption-and-description"></a>노드 ID, 이름, 캡션 및 설명  
 모든 모델의 루트 노드는 항상 고유 ID(**NODE_UNIQUE_NAME**)로 0을 갖습니다. 모든 노드 ID는 Analysis Services에 의해 자동으로 할당되며 수정할 수 없습니다.  
  
 각 모델의 루트 노드에는 모델에 대한 몇 가지 기본 메타데이터도 포함됩니다. 이러한 메타데이터로는 모델이 저장되는 Analysis Services 데이터베이스(**MODEL_CATALOG**), 스키마(**MODEL_SCHEMA)** 및 모델 이름(**MODEL_NAME)** 이 있습니다. 그리나 이 정보는 모델의 모든 노드에서 반복되므로 이 메타데이터를 가져오기 위해 루트 노드를 쿼리할 필요는 없습니다.  
  
 고유 식별자로 사용되는 이름 외에도 각 노드에는 별도의 *이름* (**NODE_NAME**)이 있습니다. 이 이름은 표시 목적으로 알고리즘을 통해 자동으로 생성되며 수정할 수 없습니다.  
  
> [!NOTE]  
>  Microsoft 클러스터링 알고리즘을 사용하면 각 클러스터에 이름을 할당할 수 있습니다. 그러나 이러한 이름은 서버에서 유지되지 않으며, 모델을 다시 처리하면 알고리즘을 통해 새 클러스터 이름이 생성됩니다.  
  
 각 노드의 *캡션* 및 *설명* 은 알고리즘을 통해 자동으로 생성되며 노드 내용을 이해하는 데 도움이 되는 레이블 역할을 합니다. 각 필드에 대해 생성되는 텍스트는 모델 유형에 따라 다릅니다. 경우에 따라 이름, 캡션 및 설명에 똑같은 문자열이 포함될 수도 있고 설명에 추가 정보가 포함될 수도 있습니다. 구현 세부 사항은 개별 모델 유형에 대한 항목을 참조하세요.  
  
> [!NOTE]  
>  Analysis Services 서버에서는 이름 바꾸기를 구현하는 사용자 지정 플러그 인 알고리즘을 사용하여 모델을 작성한 경우에만 모델의 이름 바꾸기를 지원합니다. 이름 바꾸기를 사용하려면 플러그 인 알고리즘을 만들 때 메서드를 재정의해야 합니다.  
  
### <a name="node-parents-node-children-and-node-cardinality"></a>부모 노드, 자식 노드 및 노드 카디널리티  
 트리 구조에서 부모 노드와 자식 노드 간의 관계는 PARENT_UNIQUE_NAME 열의 값에 의해 결정됩니다. 이 값은 자식 노드에 저장되며 부모 노드의 ID를 보여 줍니다. 다음은 이 정보의 사용 방법을 보여 주는 몇 가지 예입니다.  
  
-   PARENT_UNIQUE_NAME의 값이 NULL이면 노드가 모델의 최상위 노드임을 나타냅니다.  
  
-   PARENT_UNIQUE_NAME의 값이 0이면 노드가 모델에서 최상위 노드의 직계 하위 항목이어야 합니다. 이는 루트 노드의 ID는 항상 0이기 때문입니다.  
  
-   DMX(Data Mining Extensions) 쿼리 내의 함수를 사용하여 특정 노드의 하위 항목이나 부모를 찾을 수 있습니다. 쿼리에서 함수를 사용하는 방법은 [데이터 마이닝 쿼리](data-mining-queries.md)를 참조하세요.  
  
 *카디널리티* 는 집합에 있는 항목의 개수를 나타냅니다. 처리된 마이닝 모델의 컨텍스트에서 카디널리티는 특정 노드에 있는 자식의 개수를 보여 줍니다. 예를 들어 의사 결정 트리 모델에 [연간 소득] 노드가 있고 이 노드에 각각 [연간 소득] = 높음 및 [연간 소득] = 낮음 조건을 나타내기 위한 두 개의 자식 노드가 있으면 [연간 소득] 노드에 대한 CHILDREN_CARDINALITY 값은 2일 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 노드의 카디널리티를 카운트할 때 직계 자식 노드만 카운트합니다. 그러나 사용자 지정 플러그 인 알고리즘을 만들면 CHILDREN_CARDINALITY를 오버로드하여 카디널리티를 다르게 카운트할 수 있습니다. 이렇게 하면 예를 들어 직계 자식뿐 아니라 모든 하위 항목의 개수를 카운트하려는 경우에 유용할 수 있습니다.  
  
 모든 모델에서 카디널리티가 카운트되는 방법은 동일하지만 카디널리티 값을 해석하거나 사용하는 방법은 모델 유형에 따라 다릅니다. 예를 들어 클러스터링 모델에서는 최상위 노드의 카디널리티가 발견된 총 클러스터 수를 보여 주지만 다른 유형의 모델에서는 카디널리티가 항상 노드 유형에 따라 설정된 값을 가질 수 있습니다. 카디널리티를 해석하는 방법은 개별 모델 유형에 대한 항목을 참조하세요.  
  
> [!NOTE]  
>  Microsoft 신경망 알고리즘을 통해 만든 모델과 같은 일부 모델에는 전체 모델의 학습 모델에 대한 기술 통계를 제공하는 특수한 노드 유형이 추가로 포함될 수 있습니다. 정의에 따르면 이러한 노드에는 자식 노드가 없습니다.  
  
### <a name="node-distribution"></a>노드 분포  
 NODE_DISTRIBUTION 열에는 많은 노드에서 알고리즘을 통해 발견된 패턴에 대한 중요한 세부 정보를 제공하는 중첩 테이블이 포함됩니다. 이 테이블에 제공되는 정확한 통계는 모델 유형, 트리에 있는 노드의 위치 및 예측 가능한 특성이 연속 숫자 값인지 또는 불연속 값인지 여부에 따라 달라집니다. 그러나 이러한 통계에는 특성의 최소값 및 최대값, 값에 할당된 가중치, 노드에 있는 사례 수, 회귀 수식에 사용되는 계수, 표준 편차 및 분산과 같은 통계 측정값 등이 포함될 수 있습니다. 노드 분포를 해석하는 방법은 작업 중인 모델 유형에 대한 항목을 참조하세요.  
  
> [!NOTE]  
>  NODE_DISTRIBUTION 테이블은 노드 유형에 따라 비어 있을 수 있습니다. 예를 들어 일부 노드는 자세한 통계가 포함된 자식 노드의 컬렉션을 구성하기 위해서만 사용됩니다.  
  
 NODE_DISTRIBUTION 중첩 테이블에는 항상 다음과 같은 열이 포함되어 있습니다. 각 열의 내용은 모델 유형에 따라 달라집니다. 특정 모델 유형에 대한 자세한 내용은 [알고리즘 유형별 마이닝 모델 콘텐츠](#bkmk_AlgoType)를 참조하세요.  
  
 ATTRIBUTE_NAME  
 이 열에 포함되는 내용은 알고리즘에 따라 달라집니다. 이러한 내용은 예측 가능한 특성과 같은 열 이름, 규칙, 항목 집합, 수식의 일부와 같은 알고리즘 내부 정보 등일 수 있습니다.  
  
 이 열에는 특성-값 쌍도 포함될 수 있습니다.  
  
 ATTRIBUTE_VALUE  
 ATTRIBUTE_NAME에 지정된 특성의 값입니다.  
  
 특성 이름이 열이면 대부분의 간단한 사례에서는 ATTRIBUTE_VALUE에 해당 열의 불연속 값 중 하나가 포함됩니다.  
  
 ATTRIBUTE_VALUE에는 알고리즘이 값을 처리하는 방법에 따라 특성 값이 있는지 여부(`Existing`) 또는 값이 null인지 여부(`Missing`)를 나타내는 플래그도 포함될 수 있습니다.  
  
 예를 들어 특정 항목을 한 번 이상 구매한 고객을 찾도록 모델을 설정한 경우 ATTRIBUTE_NAME 열에는 `Model = 'Water bottle'`과 같은 관심 있는 항목을 정의하는 특성-값 쌍이 포함될 수 있고 ATTRIBUTE_VALUE 열에는 `Existing` 또는 `Missing` 키워드만 포함될 수 있습니다.  
  
 별칭  
 이 특성-값 쌍이 있거나 이 항목 집합 또는 규칙이 포함된 사례 수입니다.  
  
 일반적으로 각 노드의 지지도 값은 현재 노드에 포함된 학습 집합의 사례 수를 나타냅니다. 대부분의 모델 유형에서 지지도는 사례의 정확한 개수를 나타냅니다. 지지도 값은 학습 데이터를 쿼리하지 않고도 학습 사례 내의 데이터 분포를 볼 수 있기 때문에 유용합니다. 또한 Analysis Services 서버에서는 유추가 강력한 유추인지 아니면 약한 유추인지 여부를 확인하기 위해 이러한 저장된 값을 사용하여 저장된 확률과 이전 확률을 계산합니다.  
  
 예를 들어 분류 트리에서 지지도 값은 위에 설명된 특성 조합이 있는 사례 수를 나타냅니다.  
  
 의사 결정 트리에서는 각 트리 수준의 지지도 합계는 부모 노드의 지지도에 대한 합계입니다. 예를 들어 1200 개의 사례가 있는 모델을 성별로 균등 하 게 나눈 이며 다음 수입-낮음, 보통 및 높음의 자식 노드인 노드 (2)의 노드 (4), (5)에 대 한 세 가지 값 균등 하 게 세분화 및 (6), 항상 노드 (2)와 동일한 사례 수입니다.  
  
|노드 ID 및 노드 특성|지지도 개수|  
|---------------------------------|-------------------|  
|(1) Model root|1200|  
|(2) Gender = Male<br /><br /> (3) Gender = Female|600<br /><br /> 600|  
|(4) Gender = Male and Income = High<br /><br /> (5) Gender = Male and Income = Medium<br /><br /> (6) Gender = Male and Income = Low|200<br /><br /> 200<br /><br /> 200|  
|(7) Gender = Female and Income = High<br /><br /> (8) Gender = Female and Income = Medium<br /><br /> (9) Gender = Female and Income = Low|200<br /><br /> 200<br /><br /> 200|  
  
 클러스터링 모델의 경우 여러 클러스터에 속할 확률을 포함하도록 지지도 개수에 가중치가 적용될 수 있습니다. 여러 클러스터 멤버 자격은 기본 클러스터링 메서드입니다. 이 경우 각 사례가 반드시 하나의 클러스터에만 속하는 것이 아니기 때문에 이러한 모델의 지지도는 모든 클러스터에서 더해져 100%가 될 수 없습니다.  
  
 PROBABILITY  
 전체 모델 내의 특정 노드에 대한 확률을 나타냅니다.  
  
 일반적으로 확률은 노드 내의 총 사례 수로 나눈 이 특정 값에 대한 지지도(NODE_SUPPORT)를 나타냅니다.  
  
 그러나 확률은 데이터에서 값이 누락되어 발생하는 바이어스를 제거하기 위해 약간 조정됩니다.  
  
 예를 들어 [총 자녀 수]의 현재 값이 '1' 및 '2'이면 자녀 수가 0 또는 3일 수 없음을 예측하는 모델을 만들지 않을 수 있습니다. 누락 값이 희박하지만 발생할 수 있도록 하기 위해 특성의 실제 값 개수에는 항상 1이 더해집니다.  
  
 예:  
  
 [총 자녀 수 = 1]의 확률 = [총 자녀 수가 1인 사례 수] + 1/[모든 사례 수] + 3  
  
 [총 자녀 수 = 2]의 확률= [총 자녀 수가 2인 사례 수] +1/[모든 사례 수] +3  
  
> [!NOTE]  
>  조정값 3은 기존 값의 총 개수인 n에 1을 더하여 계산됩니다.  
  
 조정 후 모든 값의 확률은 여전히 더해져 1이 됩니다. 데이터가 없는 값의 확률(이 예제의 경우, [총 자녀 수 = '0', '3' 또는 기타 다른 값])은 0이 아닌 매우 낮은 수준에서 시작해서 사례가 추가됨에 따라 천천히 증가합니다.  
  
 분산  
 노드 내의 값 분산을 나타냅니다. 정의에 따르면 불연속 값의 분산은 항상 0입니다. 모델에서 연속 값을 지원하는 경우 분모 n 또는 노드에 있는 사례 수를 사용하여 분산이 σ(시그마)로 계산됩니다.  
  
 일반적으로 표준 편차(`StDev`)를 나타날 때는 두 가지 방법이 사용됩니다. 하나는 바이어스를 사용하여 표준 편차를 계산하는 방법이고 다른 하나는 바이어스를 사용하지 않고 표준 편차를 계산하는 방법입니다. 일반적으로 Microsoft 데이터 마이닝 알고리즘은 표준 편차를 계산할 때 바이어스를 사용하지 않습니다.  
  
 NODE_DISTRIBUTION 테이블에는 모든 불연속 및 분할된 특성의 실제 값과 연속 값의 평균이 표시됩니다.  
  
 VALUE_TYPE  
 값 또는 특성의 데이터 형식과 값의 사용법을 나타냅니다. 일부 값 형식은 다음과 같은 특정 모델 유형에만 적용됩니다.  
  
|VALUE_TYPE ID|값 레이블|값 형식 이름|  
|--------------------|-----------------|---------------------|  
|1|Missing|사례 데이터에 해당 특성에 대한 값이 포함되지 않았음을 나타냅니다. `Missing` 상태는 값이 있는 특성과 별도로 계산됩니다.|  
|2|Existing|사례 데이터에 해당 특성에 대한 값이 포함되어 있음을 나타냅니다.|  
|3|연속|특성 값이 연속 숫자 값이며 분산 및 표준 편차와 함께 평균으로 표시할 수 있음을 나타냅니다.|  
|4|불연속|불연속 값으로 처리되는 숫자 또는 텍스트 값을 나타냅니다.<br /><br /> **참고** 불연속 값도 누락될 수 있지만 누락된 불연속 값은 계산을 수행할 때 다르게 처리됩니다. 자세한 내용은 [누락 값&#40;Analysis Services - 데이터 마이닝&#41;](missing-values-analysis-services-data-mining.md)을 참조하세요.|  
|5|불연속화됨|특성에 불연속화 숫자 값이 포함되어 있음을 나타냅니다. 이러한 값은 불연속화 버킷을 나타내는 서식 있는 문자열이 됩니다.|  
|6|Existing|특성에 연속 숫자 값이 포함되어 있고 이러한 값이 누락 또는 유추된 데이터 및 값에 제공되었음을 나타냅니다.|  
|7|계수|계수를 나타내는 숫자 값을 가리킵니다.<br /><br /> 계수는 종속 변수의 값을 계산할 때 적용되는 값입니다. 예를 들어 모델에서 나이를 기반으로 소득을 예측하는 회귀 수식을 만들면 나이와 소득을 연결하는 수식에 계수가 사용됩니다.|  
|8|득점|특성의 득점을 나타내는 숫자 값을 가리킵니다.|  
|9|통계|회귀 변수의 통계를 나타내는 숫자 값을 가리킵니다.|  
|10|노드 고유 이름|값이 숫자나 문자열로 처리되지 않고 모델에 있는 다른 내용 노드의 고유 식별자로 처리되어야 함을 나타냅니다.<br /><br /> 예를 들어 신경망 모델에서 ID는 출력 계층의 노드에서 숨겨진 계층의 노드를 가리키는 포인터와 숨겨진 계층의 노드에서 입력 계층의 노드를 가리키는 포인터를 제공합니다.|  
|11|가로채기|회기 수식의 가로채기를 나타내는 숫자 값을 가리킵니다.|  
|12|주기성|값이 모델의 주기 구조를 나타냄을 가리킵니다.<br /><br /> ARIMA 모델이 포함된 시계열 모델에만 적용됩니다.<br /><br /> 참고: Microsoft 시계열 알고리즘은 자동으로 학습 데이터를 기반으로 주기 구조를 검색합니다. 따라서 최종 모델의 예측에는 모델을 만들 때 매개 변수로 제공하지 않은 주기성 값이 포함될 수 있습니다.|  
|13|자동 회귀 순서|값이 자동 회귀 계열의 개수를 나타냄을 가리킵니다.<br /><br /> ARIMA 알고리즘을 사용하는 시계열 모델에 적용됩니다.|  
|14|이동 평균 순서|계열의 이동 평균 수를 나타내는 값을 가리킵니다.<br /><br /> ARIMA 알고리즘을 사용하는 시계열 모델에 적용됩니다.|  
|15|차이 순서|값이 계열이 차별화되는 횟수를 가리키는 값임을 나타냅니다.<br /><br /> ARIMA 알고리즘을 사용하는 시계열 모델에 적용됩니다.|  
|16|Boolean|부울 유형을 나타냅니다.|  
|17|기타|알고리즘을 통해 정의된 사용자 지정 값을 나타냅니다.|  
|18|미리 렌더링된 문자열|알고리즘을 통해 문자열로 렌더링되는 사용자 지정 값을 나타냅니다. 개체 모델에 의해 서식이 적용되지 않았습니다.|  
  
 값 형식은 ADMOMD.NET 열거형에서 파생됩니다. 자세한 내용은 <xref:Microsoft.AnalysisServices.AdomdServer.MiningValueType>가 포함됩니다.  
  
### <a name="node-score"></a>노드 점수  
 노드 점수 관리는 모델 유형에 따라 다르며 노드 유형의 영향을 받을 수도 있습니다. 각 모델 및 노드 유형에 따라 NODE_SCORE가 계산되는 방법은 [알고리즘 유형별 마이닝 모델 콘텐츠](#bkmk_AlgoType)를 참조하세요.  
  
### <a name="node-probability-and-marginal-probability"></a>노드 확률 및 한계 확률  
 마이닝 모델 스키마 행 집합에는 모든 모델 유형에 대해 NODE_PROBABILITY 및 MARGINAL_PROBABILITY 열이 포함됩니다. 이러한 열에는 확률 값이 중요한 노드의 값만 포함됩니다. 예를 들어 모델의 루트 노드에는 확률 점수가 포함되지 않습니다.  
  
 확률 점수를 제공하는 노드에서는 노드 확률과 한계 확률이 서로 다른 계산을 나타냅니다.  
  
-   **한계 확률** 은 부모 노드에서 해당 노드에 도달할 확률입니다.  
  
-   **노드 확률** 은 루트에서 해당 노드에 도달할 확률입니다.  
  
-   **노드 확률** 은 항상 **한계 확률**보다 작거나 같습니다.  
  
 예를 들어 의사 결정 트리에 있는 모든 고객의 모집단을 누락된 값 없이 성별로 균등하게 나누면 자식 노드의 확률은 .5가 되어야 합니다. 그러나는 각 성별 노드가 동일 하 게 나뉩니다 소득 수준에서 가정-높음, 중간 및 낮음. 각 자식 노드의 MARGINAL_PROBABILITY 점수는 항상 .33이어야 하지만 NODE_PROBABILTY 값이 해당 노드를 가리키는 모든 확률의 곱한 값이 되어 항상 MARGINAL_PROBABILITY 값보다 작습니다.  
  
|노드 수준/특성 및 값|한계 확률|노드 확률|  
|----------------------------------------|--------------------------|----------------------|  
|모델 루트<br /><br /> 모든 대상 고객|1|1|  
|성별로 나눈 대상 고객|.5|.5|  
|성별로 나누고 다시 소득에 따라 세 가지로 나눈 대상 고객|.33|.5 * .33 = .165|  
  
### <a name="node-rule-and-marginal-rule"></a>노드 규칙 및 한계 규칙  
 마이닝 모델 스키마 행 집합에는 모든 모델 유형에 대해 NODE_RULE 및 MARGINAL_RULE 열도 포함됩니다. 이러한 열에는 모델을 직렬화하고 모델 구조의 특정 부분을 나타내는 데 사용할 수 있는 XML 조각이 포함됩니다. 이러한 열은 값이 의미가 없을 경우 일부 노드에 대해 비워 둘 수 있습니다.  
  
 위 두 가지 종류의 확률 값과 유사한 두 가지 종류의 XML 규칙이 제공됩니다. MARGINAL_RULE의 XML 조각은 현재 노드의 특성과 값을 정의하는 반면 NODE_RULE의 XML 조각은 모델 루트에서 현재 노드까지의 경로를 나타냅니다.  
  
##  <a name="bkmk_AlgoType"></a> 알고리즘 유형별 마이닝 모델 콘텐츠  
 각 알고리즘은 콘텐츠 스키마의 일부로 서로 다른 유형의 정보를 저장합니다. 예를 들어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘은 각각 가능한 클러스터를 나타내는 많은 자식 노드를 생성합니다. 각 클러스터 노드에는 클러스터의 항목에서 공유하는 특성을 나타내는 규칙이 포함됩니다. 반면에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘은 자식 노드를 포함하지 않고 대신 모델의 부모 노드에 분석을 통해 발견된 선형 관계를 나타내는 수식이 포함됩니다.  
  
 다음 표에서는 각 알고리즘 유형에 대해 설명하는 항목에 대한 링크를 제공합니다.  
  
-   **모델 콘텐츠 항목:** 알고리즘 유형별로 각 노드의 의미를 설명하고 모델 유형에 따라 가장 적합한 노드에 대한 지침을 제공합니다.  
  
-   **쿼리 항목:** 특정 모델 유형에 대한 쿼리 예와 쿼리 결과를 해석하는 방법에 대한 지침을 제공합니다.  
  
|알고리즘 또는 모델 유형|모델 콘텐츠|마이닝 모델 쿼리|  
|-----------------------------|-------------------|----------------------------|  
|연결 규칙 모델|[연결 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md)|[연결 모델 쿼리 예제](association-model-query-examples.md)|  
|클러스터링 모델|[의사 결정 트리 모델 & #40;에 대 한 마이닝 모델 콘텐츠 Analysis Services-데이터 마이닝 & #41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[클러스터링 모델 쿼리 예제](clustering-model-query-examples.md)|  
|의사 결정 트리 모델|[의사 결정 트리 모델 & #40;에 대 한 마이닝 모델 콘텐츠 Analysis Services-데이터 마이닝 & #41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[의사 결정 트리 모델 쿼리 예제](decision-trees-model-query-examples.md)|  
|선형 회귀 모델|[선형 회귀 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)|[선형 회귀 모델 쿼리 예제](linear-regression-model-query-examples.md)|  
|로지스틱 회귀 모델|[로지스틱 회귀 분석 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-for-logistic-regression-models.md)|[선형 회귀 모델 쿼리 예제](linear-regression-model-query-examples.md)|  
|Naïve Bayes 모델|[Naive Bayes 모델 & #40;에 대 한 마이닝 모델 콘텐츠 Analysis Services-데이터 마이닝 & #41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)|[Naive Bayes 모델 쿼리 예제](naive-bayes-model-query-examples.md)|  
|신경망 모델|[신경망 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)|[신경망 모델 쿼리 예제](neural-network-model-query-examples.md)|  
|시퀀스 클러스터링|[시퀀스 클러스터링 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-for-sequence-clustering-models.md)|[시퀀스 클러스터링 모델 쿼리 예제](sequence-clustering-model-query-examples.md)|  
|시계열 모델|[시계열 모델 & #40;에 대 한 마이닝 모델 콘텐츠 Analysis Services-데이터 마이닝 & #41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)|[시계열 모델 쿼리 예제](time-series-model-query-examples.md)|  
  
##  <a name="bkmk_Viewing"></a> 마이닝 모델 콘텐츠를 보기 위한 도구  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 모델을 찾아볼 경우 **및**에서 사용할 수 있는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Microsoft 일반 콘텐츠 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]트리 뷰어에서 정보를 볼 수 있습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 일반 콘텐츠 뷰어에는 마이닝 모델 콘텐츠 스키마 행 집합에서 사용할 수 있는 것과 동일한 정보를 사용하여 마이닝 모델 콘텐츠 스키마 행 집합의 열, 규칙, 속성, 특성, 노드 및 기타 콘텐츠가 표시됩니다. 콘텐츠 스키마 행 집합은 데이터 마이닝 모델의 콘텐츠에 대한 세부 정보를 나타내는 일반 프레임워크입니다. 모델 콘텐츠는 계층적 행 집합을 지원하는 모든 클라이언트에서 볼 수 있습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 뷰어에서는 작성한 모델의 구조를 보다 쉽게 이해할 수 있도록 모든 정보를 일관된 형식으로 나타내는 HTML 테이블 뷰어에 이 정보를 표시합니다. 자세한 내용은 [Microsoft 일반 콘텐츠 트리 뷰어를 사용하여 모델 찾아보기](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)를 참조하세요.  
  
##  <a name="bkmk_Querying"></a> 마이닝 모델 콘텐츠를 쿼리하기 위한 도구  
 마이닝 모델 콘텐츠를 검색하려면 데이터 마이닝 모델에 대한 쿼리를 만들어야 합니다.  
  
 내용 쿼리를 만드는 가장 쉬운 방법은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 다음 DMX 문을 실행하는 것입니다.  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 자세한 내용은 [데이터 마이닝 쿼리](data-mining-queries.md)를 참조하세요.  
  
 또한 데이터 마이닝 스키마 행 집합을 사용하여 마이닝 모델 콘텐츠를 쿼리할 수도 있습니다. 스키마 행 집합은 클라이언트에서 마이닝 구조 및 모델에 대한 정보를 검색하고 쿼리하기 위해 사용하는 표준 구조입니다. 스키마 행 집합은 XMLA, Transact-SQL 또는 DMX 문을 사용하여 쿼리할 수 있습니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 연결을 열고 시스템 테이블을 쿼리하여 데이터 마이닝 스키마 행 집합의 정보에 액세스할 수도 있습니다. 자세한 내용은 [데이터 마이닝 스키마 행 집합 쿼리 &#40;Analysis Services-데이터 마이닝&#41;](data-mining-schema-rowsets-ssas.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 일반 콘텐츠 트리 뷰어&#40;데이터 마이닝&#41;](../microsoft-generic-content-tree-viewer-data-mining.md)   
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
  
