---
title: 마이닝 신경망 모델에 대 한 모델 콘텐츠 (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- output neurons [Analysis Services]
- neural network algorithms [Analysis Services]
- output layer [Data Mining]
- hidden layer
- hidden neurons
- input layer [Data Mining]
- input neurons [Analysis Services]
- mining model content, neural network models
- neural network model [Analysis Services]
ms.assetid: ea21ff9d-857f-475c-bd3d-6d1405bad069
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d5b823481d47f6e986815673aa3ab65d44f07c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733496"
---
# <a name="mining-model-content-for-neural-network-models-analysis-services---data-mining"></a>신경망 모델에 대한 마이닝 모델 콘텐츠(Analysis Services - 데이터 마이닝)
  이 항목에서는 Microsoft 신경망 알고리즘을 사용하는 모델만의 마이닝 모델 콘텐츠에 대해 설명합니다. 모든 모델 유형에서 공유하는 통계 및 구조를 해석하는 방법에 대한 설명은 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-analysis-services-data-mining.md)를 참조하세요.  
  
## <a name="understanding-the-structure-of-a-neural-network-model"></a>신경망 모델의 구조 이해  
 각 신경망 모델에는 모델 및 해당 메타데이터를 나타내는 단일 부모 노드와 입력 특성에 대한 기술 통계를 제공하는 특수한 한계 통계 노드(NODE_TYPE = 24)가 있습니다. 한계 통계 노드는 입력에 대한 정보를 요약하기 때문에 개별 노드에서 데이터를 쿼리하지 않아도 되므로 유용합니다.  
  
 이 두 노드 아래에는 두 개 이상의 노드가 있으며, 이러한 노드는 모델에 포함된 예측 가능한 특성의 수에 따라 매우 많이 있을 수도 있습니다.  
  
-   첫 번째 노드(NODE_TYPE = 18)는 항상 입력 계층의 최상위 노드를 나타냅니다. 이 최상위 노드 아래에는 실제 입력 특성과 해당 값이 들어 있는 입력 노드(NODE_TYPE = 21)가 있습니다.  
  
-   연속된 각 노드에는 각기 다른 *서브네트워크* (NODE_TYPE = 17)가 있습니다. 각 하위 네트워크에는 해당 하위 네트워크에 대한 숨겨진 계층(NODE_TYPE = 19)과 출력 계층(NODE_TYPE = 20)이 항상 포함되어 있습니다.  
  
 ![신경망 모델 콘텐츠의 구조](../media/modelcontentstructure-nn.gif "한 신경망에 대 한 모델 콘텐츠 구조")  
  
 입력 계층의 정보는 간단합니다. 각 입력 계층의 최상위 노드(NODE_TYPE = 18)는 입력 노드(NODE_TYPE = 21) 컬렉션의 구성 도우미 역할을 합니다. 입력 노드의 내용은 다음 표에서 설명합니다.  
  
 각 하위 네트워크(NODE_TYPE = 17)는 입력 계층이 예측 가능한 특정 특성에 주는 영향에 대한 분석을 나타냅니다. 예측 가능한 출력이 여러 개 있으면 하위 네트워크도 여러 개 있습니다. 각 하위 네트워크의 숨겨진 계층에는 여러 개의 숨겨진 노드(NODE_TYPE = 22)가 포함되고 이 숨겨진 노드에는 해당 노드로 끝나는 각 전환의 가중치에 대한 정보가 포함됩니다.  
  
 출력 계층(NODE_TYPE = 20)에는 각각 예측 가능한 특성의 고유 값이 포함된 출력 노드(NODE_TYPE = 23)가 포함됩니다. 예측 가능한 특성이 연속 숫자 데이터 형식일 경우에는 해당 특성에 대한 출력 노드가 하나만 있습니다.  
  
> [!NOTE]  
>  로지스틱 회귀 알고리즘에서는 예측 가능한 결과가 하나만 있고 입력은 여러 개일 수 있는 특수한 신경망을 사용합니다. 로지스틱 회귀에서는 숨겨진 계층을 사용하지 않습니다.  
  
 입력 및 하위 네트워크의 구조를 탐색하는 가장 쉬운 방법은 **Microsoft 일반 콘텐츠 트리 뷰어**를 사용하는 것입니다. 임의의 노드를 클릭하여 확장한 후 자식 노드를 보거나 노드에 포함된 가중치 및 기타 통계를 볼 수 있습니다.  
  
 데이터를 사용하고 모델이 입력과 출력 간의 상관 관계를 찾아내는 방식을 보려면 **Microsoft 신경망 뷰어**를 사용합니다. 이 사용자 지정 뷰어를 사용하면 입력 특성과 해당 값을 필터링하고 이러한 항목이 출력에 주는 영향을 그래픽으로 볼 수 있습니다. 뷰어의 도구 설명에는 각 입력 및 출력 값 쌍과 연결된 확률 및 리프트가 표시됩니다. 자세한 내용은 [Microsoft 신경망 뷰어를 사용하여 모델 찾아보기](browse-a-model-using-the-microsoft-neural-network-viewer.md)를 참조하세요.  
  
## <a name="model-content-for-a-neural-network-model"></a>신경망 모델에 대한 모델 콘텐츠  
 이 섹션에서는 신경망 모델과 특별히 관련된 마이닝 모델 콘텐츠 열에 대한 세부 정보 및 예만 제공합니다. MODEL_CATALOG와 MODEL_NAME을 비롯하여 여기에 설명되지 않은 스키마 행 집합의 범용 열에 대한 자세한 내용 또는 마이닝 모델 용어에 대한 자세한 내용은 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-analysis-services-data-mining.md)를 참조하세요.  
  
 MODEL_CATALOG  
 모델이 저장되는 데이터베이스의 이름입니다.  
  
 MODEL_NAME  
 모델의 이름입니다.  
  
 ATTRIBUTE_NAME  
 이 노드에 해당하는 특성의 이름입니다.  
  
|노드|콘텐츠|  
|----------|-------------|  
|모델 루트|비어 있음|  
|한계 통계|비어 있음|  
|입력 계층|비어 있음|  
|입력 노드|입력 특성 이름|  
|숨겨진 계층|비어 있음|  
|숨겨진 노드|비어 있음|  
|출력 계층|비어 있음|  
|출력 노드|출력 특성 이름|  
  
 NODE_NAME  
 노드 이름입니다. 이 열에는 NODE_UNIQUE_NAME과 동일한 값이 포함됩니다.  
  
 NODE_UNIQUE_NAME  
 노드의 고유한 이름입니다.  
  
 이름과 ID가 모델에 대한 구조 정보를 반영하는 방식에 대한 자세한 내용은 [노드 이름 및 ID 사용](#bkmk_NodeIDs)섹션을 참조하세요.  
  
 NODE_TYPE  
 신경망 모델이 출력하는 노드 유형은 다음과 같습니다.  
  
|노드 유형 ID|Description|  
|------------------|-----------------|  
|1|모델|  
|17|하위 네트워크의 구성 도우미 노드|  
|18|입력 계층의 구성 도우미 노드|  
|19|숨겨진 계층의 구성 도우미 노드.|  
|20|출력 계층의 구성 도우미 노드|  
|21|입력 특성 노드|  
|22|숨겨진 계층 노드|  
|23|출력 특성 노드|  
|24|한계 통계 노드|  
  
 NODE_CAPTION  
 노드와 연결된 레이블 또는 캡션입니다. 신경망 모델에서는 항상 비어 있습니다.  
  
 CHILDREN_CARDINALITY  
 노드에 있는 예상 자식 수입니다.  
  
|노드|콘텐츠|  
|----------|-------------|  
|모델 루트|한 개 이상의 네트워크, 한 개의 필수 한계 노드 및 한 개의 필수 입력 계층을 포함하는 자식 노드의 수를 나타냅니다. 예를 들어 값이 5인 경우 3개의 하위 네트워크가 있습니다.|  
|한계 통계|항상 0입니다.|  
|입력 계층|모델에 사용된 입력 특성-값 쌍의 수를 나타냅니다.|  
|입력 노드|항상 0입니다.|  
|숨겨진 계층|모델에서 만든 숨겨진 노드의 수를 나타냅니다.|  
|숨겨진 노드|항상 0입니다.|  
|출력 계층|출력 값의 수를 나타냅니다.|  
|출력 노드|항상 0입니다.|  
  
 PARENT_UNIQUE_NAME  
 노드 부모의 고유한 이름입니다. 루트 수준의 모든 노드에 대해서 NULL이 반환됩니다.  
  
 이름과 ID가 모델에 대한 구조 정보를 반영하는 방식에 대한 자세한 내용은 [노드 이름 및 ID 사용](#bkmk_NodeIDs)섹션을 참조하세요.  
  
 NODE_DESCRIPTION  
 노드에 대한 알기 쉬운 설명입니다.  
  
|노드|콘텐츠|  
|----------|-------------|  
|모델 루트|비어 있음|  
|한계 통계|비어 있음|  
|입력 계층|비어 있음|  
|입력 노드|입력 특성 이름|  
|숨겨진 계층|비어 있음|  
|숨겨진 노드|숨겨진 노드 목록에 있는 숨겨진 노드의 시퀀스를 나타내는 정수|  
|출력 계층|비어 있음|  
|출력 노드|출력 특성이 연속 특성인 경우 출력 특성의 이름을 포함합니다.<br /><br /> 출력 특성이 불연속 또는 불연속화된 특성인 경우 특성 이름 및 값을 포함합니다.|  
  
 NODE_RULE  
 노드에 포함된 규칙에 대한 XML 설명입니다.  
  
|노드|콘텐츠|  
|----------|-------------|  
|모델 루트|비어 있음|  
|한계 통계|비어 있음|  
|입력 계층|비어 있음|  
|입력 노드|NODE_DESCRIPTION 열과 같은 정보가 들어 있는 XML 조각|  
|숨겨진 계층|비어 있음|  
|숨겨진 노드|숨겨진 노드 목록에 있는 숨겨진 노드의 시퀀스를 나타내는 정수|  
|출력 계층|비어 있음|  
|출력 노드|NODE_DESCRIPTION 열과 같은 정보가 들어 있는 XML 조각|  
  
 MARGINAL_RULE  
 신경망 모델의 경우 항상 비어 있습니다.  
  
 NODE_PROBABILITY  
 이 노드와 관련된 확률입니다. 신경망 모델의 경우 항상 0입니다.  
  
 MARGINAL_PROBABILITY  
 부모 노드에서 해당 노드에 도달할 확률입니다. 신경망 모델의 경우 항상 0입니다.  
  
 NODE_DISTRIBUTION  
 노드에 대한 통계 정보가 들어 있는 중첩 테이블입니다. 각 노드 유형에 대해 이 테이블에 포함되는 내용에 대한 자세한 내용은 [NODE_DISTRIBUTION 테이블 이해](#bkmk_NodeDistTable)섹션을 참조하세요.  
  
 NODE_SUPPORT  
 신경망 모델의 경우 항상 0입니다.  
  
> [!NOTE]  
>  이 모델 유형의 출력은 확률적이 아니므로 지지도 확률은 항상 0입니다. 이 알고리즘에는 가중치만 의미가 있으므로 이 알고리즘은 확률, 지지도 또는 분산을 컴퓨팅하지 않습니다.  
  
 특정 값에 대한 학습 사례의 지지도에 관한 정보를 보려면 한계 통계 노드를 참조하세요.  
  
 MSOLAP_MODEL_COLUMN  
 |노드|콘텐츠|  
|----------|-------------|  
|모델 루트|비어 있음|  
|한계 통계|비어 있음|  
|입력 계층|비어 있음|  
|입력 노드|입력 특성 이름|  
|숨겨진 계층|비어 있음|  
|숨겨진 노드|비어 있음|  
|출력 계층|비어 있음|  
|출력 노드|입력 특성 이름|  
  
 MSOLAP_NODE_SCORE  
 신경망 모델의 경우 항상 0입니다.  
  
 MSOLAP_NODE_SHORT_CAPTION  
 신경망 모델의 경우 항상 비어 있습니다.  
  
## <a name="remarks"></a>Remarks  
 신경망 모델의 학습 목적은 입력에서 중간점 및 중간점에서 엔드포인트로의 각 전환과 연결된 가중치를 확인하는 것입니다. 따라서 모델의 입력 계층은 주로 모델을 작성하는 데 사용된 실제 값을 저장하기 위해 존재합니다. 숨겨진 계층은 계산된 가중치를 저장하며 입력 특성에 대한 포인터를 제공합니다. 출력 계층은 예측 가능한 값을 저장하며 숨겨진 계층의 중간점에 대한 포인터를 제공합니다.  
  
##  <a name="bkmk_NodeIDs"></a> 노드 이름 및 ID 사용  
 신경망 모델의 노드 이름은 노드 유형에 대한 추가 정보를 제공하므로 이를 통해 숨겨진 계층과 입력 계층의 관계 및 출력 계층과 숨겨진 계층의 관계를 쉽게 이해할 수 있습니다. 다음 표에서는 각 계층의 노드에 할당되는 ID의 규칙을 보여 줍니다.  
  
|노드 유형|노드 ID의 규칙|  
|---------------|----------------------------|  
|모델 루트(1)|00000000000000000.|  
|한계 통계 노드(24)|10000000000000000|  
|입력 계층(18)|30000000000000000|  
|입력 노드(21)|60000000000000000에서 시작|  
|하위 네트워크(17)|20000000000000000|  
|숨겨진 계층(19)|40000000000000000|  
|숨겨진 노드(22)|70000000000000000에서 시작|  
|출력 계층(20)|50000000000000000|  
|출력 노드(23)|80000000000000000에서 시작|  
  
 숨겨진 노드(NODE_TYPE = 22)의 NODE_DISTRIBUTION 테이블을 보면 숨겨진 특정 계층과 관련된 입력 특성을 확인할 수 있습니다. NODE_DISTRIBUTION 테이블의 각 행에는 입력 특성 노드의 ID가 들어 있습니다.  
  
 마찬가지로, 출력 노드(NODE_TYPE = 23)의 NODE_DISTRIBUTION 테이블을 보면 출력 특성과 관련된 숨겨진 계층을 확인할 수 있습니다. NODE_DISTRIBUTION 테이블의 각 행에는 숨겨진 계층 노드의 ID와 관련 계수가 들어 있습니다.  
  
##  <a name="bkmk_NodeDistTable"></a> NODE_DISTRIBUTION 테이블의 정보 해석  
 일부 노드에서는 NODE_DISTRIBUTION 테이블이 비어 있을 수 있습니다. 그러나 입력 노드, 숨겨진 계층 노드 및 출력 노드의 경우 NODE_DISTRIBUTION 테이블에는 모델에 대한 중요하고 주목할 만한 정보가 저장됩니다. 이 정보를 쉽게 해석할 수 있도록 NODE_DISTRIBUTION 테이블에는 각 행에 대해 VALUETYPE 열이 들어 있으므로 이 열을 통해 ATTRIBUTE_VALUE 열의 값이 불연속적(4)인지, 불연속화(5)되었는지, 연속적(3)인지를 알 수 있습니다.  
  
### <a name="input-nodes"></a>입력 노드  
 입력 계층에는 모델에 사용된 각 특성 값에 대한 노드가 포함됩니다.  
  
 **불연속 특성:** 입력된 노드에 ATTRIBUTE_NAME 및 ATTRIBUTE_VALUE 열의 특성 및 해당 값의 이름만 저장합니다. 예를 들어 [Work Shift]가 열인 경우 이 열의 값 중 모델에 사용된 각 값(예: AM 및 PM)에 대해 별도의 노드가 만들어집니다. 각 노드의 NODE_DISTRIBUTION 테이블에는 특성의 현재 값만 나열됩니다.  
  
 **불연속화 된 숫자 특성:** 입력된 노드에 특성 및이 값은 범위 또는 특정 값의 이름을 저장 합니다. 모든 값은 식으로 표현됩니다. 예를 들어 [Time Per Issue]의 값은 '77.4 - 87.4' 또는 ' < 64.0' 등으로 표현됩니다. 각 노드의 NODE_DISTRIBUTION 테이블에는 특성의 현재 값만 나열됩니다.  
  
 **연속 특성:** 입력된 노드에 특성의 평균 값을 저장합니다. 각 노드의 NODE_DISTRIBUTION 테이블에는 특성의 현재 값만 나열됩니다.  
  
### <a name="hidden-layer-nodes"></a>숨겨진 계층 노드  
 숨겨진 계층에는 여러 개의 노드가 포함됩니다. 각 노드의 NODE_DISTRIBUTION 테이블에는 숨겨진 계층에서 입력 계층 노드로의 매핑이 들어 있습니다. ATTRIBUTE_NAME 열에는 입력 계층의 노드에 해당하는 노드 ID가 들어 있습니다. ATTRIBUTE_VALUE 열에는 입력 노드 및 숨겨진 계층 노드의 조합과 연결된 가중치가 들어 있습니다. 테이블의 마지막 행에는 숨겨진 계층에 있는 숨겨진 해당 노드의 가중치를 나타내는 계수가 들어 있습니다.  
  
### <a name="output-nodes"></a>출력 노드  
 출력 계층에는 모델에 사용된 각 출력 값에 대한 출력 노드가 하나씩 포함됩니다. 각 노드의 NODE_DISTRIBUTION 테이블에는 출력 계층에서 숨겨진 계층 노드로의 매핑이 들어 있습니다. ATTRIBUTE_NAME 열에는 숨겨진 계층의 노드에 해당하는 노드 ID가 들어 있습니다. ATTRIBUTE_VALUE 열에는 출력 노드 및 숨겨진 계층 노드의 조합과 연결된 가중치가 들어 있습니다.  
  
 NODE_DISTRIBUTION 테이블에는 특성 유형에 따라 다음과 같은 추가 정보가 포함됩니다.  
  
 **불연속 특성:** NODE_DISTRIBUTION 테이블의 마지막 두 행에는 전체 및 특성의 현재 값에 따라 노드 계수를 포함합니다.  
  
 **불연속화 된 숫자 특성:** 특성의 값이 범위의 값을 제외 하 고 불연속 특성과 동일 합니다.  
  
 **연속 특성:** NODE_DISTRIBUTION 테이블의 마지막 두 행 노드 전체에 대 한 계수 특성의 평균 및 계수의 분산을 포함 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft Neural Network Algorithm](microsoft-neural-network-algorithm.md)   
 [Microsoft 신경망 알고리즘 기술 참조](microsoft-neural-network-algorithm-technical-reference.md)   
 [신경망 모델 쿼리 예제](neural-network-model-query-examples.md)  
  
  
