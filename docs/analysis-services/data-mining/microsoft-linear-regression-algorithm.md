---
title: Microsoft 선형 회귀 알고리즘 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 081db3d1c66426ddfc925e81591f3b891ecc0ea2
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="microsoft-linear-regression-algorithm"></a>Microsoft 선형 회귀 알고리즘
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘은 종속 변수와 독립 변수 간의 선형 관계를 계산하고 이 관계를 예측에 사용하는 데 도움이 되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘의 변형입니다.  
  
 이 관계는 데이터 계열을 가장 잘 나타내는 선에 대한 수식 형식을 사용합니다. 예를 들어 다음 다이어그램의 선은 데이터를 가장 잘 나타내는 선형 표시입니다.  
  
 ![데이터 집합을 모델링 하는 선](../../analysis-services/data-mining/media/linear-regression.gif "데이터 집합을 모델링 하는 선")  
  
 다이어그램의 각 데이터 요소에는 회귀선으로부터의 거리와 관련된 오류가 있습니다. 회귀 수식에서 계수 a와 b는 회귀선의 각도와 위치를 조정합니다. 모든 요소와 관련된 오류 수의 합계가 최소가 될 때까지 a와 b를 조정하여 회귀 수식을 얻을 수 있습니다.  
  
 여러 변수를 사용하는 다른 유형의 회귀도 있으며 비선형 회귀 방법도 있습니다. 그러나 선형 회귀는 일부 기본 요소의 변경에 대한 응답을 모델링하는 데 있어 유용하고 잘 알려진 방법입니다.  
  
## <a name="example"></a>예제  
 선형 회귀를 사용하여 두 연속 열 간의 관계를 확인할 수 있습니다. 예를 들어 선형 회귀를 사용하여 제조 또는 판매 데이터로부터 추세 선을 계산할 수 있습니다. 또한 선형 회귀를 보다 복합적인 데이터 마이닝 모델 개발을 위한 전신으로 사용하여 데이터 열 간의 관계를 평가할 수도 있습니다.  
  
 데이터 마이닝 도구가 필요 없는 선형 회귀 계산 방법도 많이 있지만 이 태스크에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘을 사용함으로써 얻을 수 있는 장점은 변수 간의 가능한 모든 관계가 자동으로 계산 및 테스트된다는 것입니다. 최소 제곱 구하기와 같은 계산 방법을 선택할 필요가 없습니다. 그러나 선형 회귀는 여러 가지 요소가 결과에 영향을 미치는 시나리오에서 관계를 지나치게 단순화할 수 있습니다.  
  
## <a name="how-the-algorithm-works"></a>알고리즘 작동 방법  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘의 변형입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘을 선택하면 알고리즘의 동작을 강제하고 특정 입력 데이터 형식을 요구하는 매개 변수와 함께 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘의 특수한 사례가 호출됩니다. 또한 표준 의사 결정 트리 모델이 데이터를 작은 하위 집합 또는 트리로 반복해서 분할하는 데 반해 선형 회귀 모델에서는 초기 패스의 관계 계산에 전체 데이터 집합이 사용됩니다.  
  
## <a name="data-required-for-linear-regression-models"></a>선형 회귀 모델에 필요한 데이터  
 선형 회귀 모델에 사용할 데이터를 준비할 때는 특정 알고리즘에 대한 요구 사항을 알고 있어야 합니다. 여기에는 데이터의 필요 정도와 사용 방식이 포함됩니다. 이 모델 유형의 요구 사항은 다음과 같습니다.  
  
-   **단일 키 열** 각 모델은 각 레코드를 고유하게 식별하는 숫자 또는 텍스트 열을 하나 포함해야 합니다. 복합 키는 사용할 수 없습니다.  
  
-   **예측 가능한 열** 하나 이상의 예측 가능한 열이 필요합니다. 여러 예측 가능한 특성을 모델에 포함할 수 있지만 예측 가능한 특성은 연속 숫자 데이터 형식이어야 합니다. 데이터에 대한 기본 저장소가 숫자인 경우라도 datetime 데이터 형식은 예측 가능한 특성으로 사용할 수 없습니다.  
  
-   **입력 열** 입력 열에는 연속 숫자 데이터가 포함되어야 하며 적절한 데이터 형식이 할당되어야 합니다.  
  
 자세한 내용은 [Microsoft 선형 회귀 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)의 요구 사항 섹션을 참조하세요.  
  
## <a name="viewing-a-linear-regression-model"></a>선형 회귀 모델 보기  
 **Microsoft 트리 뷰어**를 사용하여 모델을 탐색할 수 있습니다. 선형 회귀 모델에 대한 트리 구조는 매우 간단하며 회귀 수식에 대한 모든 정보는 단일 노드에 포함됩니다. 자세한 내용은 [Microsoft 트리 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)를 참조하세요.  
  
 수식에 대한 세부 정보를 보려면 [Microsoft 일반 콘텐츠 트리 뷰어](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)를 사용하여 계수 및 기타 세부 정보를 확인하십시오.  
  
 선형 회귀 모델의 경우 모델 콘텐츠에는 메타데이터, 회귀 수식 및 입력 값의 분산에 대한 통계가 포함됩니다. 자세한 내용은 [선형 회귀 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)의 요구 사항 섹션을 참조하세요.  
  
## <a name="creating-predictions"></a>예측 만들기  
 모델을 처리한 후에는 결과가 선형 회귀 수식과 함께 일련의 통계로 저장되며 이를 사용하여 향후 추세를 계산할 수 있습니다. 선형 회귀 모델을 사용하는 쿼리의 예는 [선형 회귀 모델 쿼리 예제](../../analysis-services/data-mining/linear-regression-model-query-examples.md)를 참조하세요.  
  
 마이닝 모델에 대한 쿼리를 만드는 방법에 대한 일반적인 내용은 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)를 참조하세요.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘을 선택하여 선형 회귀 모델을 만드는 것 외에, 예측 가능한 특성이 연속 숫자 데이터 형식인 경우 회귀를 포함하는 의사 결정 트리 모델도 만들 수 있습니다. 이 경우 알고리즘은 적절한 분할 지점을 찾으면 데이터를 분할하지만 일부 데이터 영역에 대해서는 분할하는 대신 회귀 수식을 만듭니다. 의사 결정 트리 모델 내의 회귀 트리에 대한 자세한 내용은 [의사 결정 트리 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)를 참조하세요.  
  
## <a name="remarks"></a>주의  
  
-   PMML(Predictive Model Markup Language)을 사용한 마이닝 모델 생성은 지원하지 않습니다.  
  
-   데이터 마이닝 차원의 생성은 지원하지 않습니다.  
  
-   드릴스루를 지원합니다.  
  
-   OLAP 마이닝 모델의 사용을 지원합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft 선형 회귀 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)   
 [선형 회귀 모델 쿼리 예제](../../analysis-services/data-mining/linear-regression-model-query-examples.md)   
 [선형 회귀 모델 & #40;에 대 한 마이닝 모델 콘텐츠 Analysis Services-데이터 마이닝 & #41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
