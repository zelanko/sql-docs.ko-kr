---
title: Microsoft Naive Bayes 알고리즘 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Bayesian classifiers
- algorithms [data mining]
- predictive modeling [Analysis Services]
- classification algorithms [Analysis Services]
- naive bayes algorithms [Analysis Services]
ms.assetid: 3b53e011-3b1a-4cd1-bdc2-456768ba31b5
caps.latest.revision: 57
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f43178fb87047af76813f1bb1f7e8876bfc63462
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-naive-bayes-algorithm"></a>Microsoft Naive Bayes 알고리즘
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 알고리즘은 Bayes 정리를 기반으로 하는 분류 알고리즘으로, 설명 및 예측 모델링 둘 다에 사용할 수 있습니다. Naïve Bayes라는 이름의 naïve는 이 알고리즘이 Bayes 기술을 사용하지만 있을 수 있는 종속성을 고려하지 않는다는 사실에서 비롯된 것입니다.  
  
 이 알고리즘은 다른 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘보다 계산 과정이 단순하여 입력 열과 예측 가능한 열 간의 관계를 검색하는 마이닝 모델을 신속하게 생성하는 데 유용합니다. 이 알고리즘을 사용하여 초기 데이터 탐색을 수행한 후 나중에 그 결과를 적용하여 보다 복잡하고 정확한 다른 알고리즘으로 추가 마이닝 모델을 만들 수 있습니다.  
  
## <a name="example"></a>예제  
 진행 중인 홍보 행사 전략의 하나로 Adventure Works Cycle사의 마케팅 부서는 우편으로 전단지를 보내 잠재 고객을 공략하기로 결정했습니다. 비용을 줄이기 위해 응답 가능성이 큰 고객에게만 전단지를 보내려고 합니다. 회사는 인구 통계 및 이전 우편물에 대한 응답 정보를 데이터베이스에 저장합니다. 이 데이터를 사용하여 특징이 유사하고 과거에 회사 제품을 구매한 고객과 잠재 고객을 비교하여 연령 및 위치와 같은 인구 통계가 홍보 행사에 대한 응답을 예측하는 데 얼마나 도움이 되는지 확인하려고 합니다. 특히 자전거를 구입한 고객과 구입하지 않은 고객의 차이점을 찾으려고 합니다.  
  
 마케팅 부서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 알고리즘을 사용하여 특정 고객 프로필에 대한 결과를 신속하게 예측할 수 있으므로 전단지에 응답할 가능성이 큰 고객을 결정할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Naive Bayes 뷰어를 사용하면 특히 전단지에 대한 긍정적인 응답에 기여한 입력 열을 시각적으로 조사할 수도 있습니다.  
  
## <a name="how-the-algorithm-works"></a>알고리즘 작동 방법  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 알고리즘은 예측 가능한 열에 가능한 각 상태가 지정되면 각 입력 열의 모든 상태에 대한 확률을 계산합니다.  
  
 다음 그래픽에 표시된 것처럼 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Naive Bayes 뷰어를 사용하여 알고리즘의 상태 분포를 시각적으로 탐색함으로써 이 알고리즘의 작동 방식을 이해할 수 있습니다.  
  
 ![Naive bayes 상태 분포](../../analysis-services/data-mining/media/naive-bayes.gif "Naive bayes 상태 분포")  
  
 여기에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 뷰어는 데이터 집합의 각 입력 열을 나열하고 예측 가능한 열의 각 상태가 지정되면 각 열의 상태 분포를 보여 줍니다.  
  
 모델의 이 뷰를 사용하여 예측 가능한 열의 상태를 차별화하는 데 중요한 입력 열을 식별할 수 있습니다.  
  
 예를 들어 여기에 표시된 Commute Distance에 대한 행에서 입력 값의 분포는 구매자와 비구매자가 다릅니다. 이를 통해 Commute Distance = 0-1마일이라는 입력은 잠재적인 예측 요인이라는 사실을 알 수 있습니다.  
  
 뷰어에서는 분포에 대한 값도 제공하므로 1-2마일 거리를 통근하는 고객의 경우 자전거를 구입할 확률이 0.387인 반면 자전거를 구입하지 않을 확률은 0.287이라는 것도 확인할 수 있습니다. 이 예에서 알고리즘은 통근 거리와 같은 고객 특징에서 파생된 숫자 정보를 사용하여 고객의 자전거 구입 여부를 예측합니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 뷰어를 사용하는 방법에 대한 자세한 내용은 [Microsoft Naive Bayes 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)를 참조하세요.  
  
## <a name="data-required-for-naive-bayes-models"></a>Naive Bayes 모델에 필요한 데이터  
 Naive Bayes 모델을 학습하는 데 사용할 데이터를 준비할 때는 필요한 데이터의 양과 사용법을 비롯하여 해당 알고리즘의 요구 사항을 알고 있어야 합니다.  
  
 Naive Bayes 모델의 요구 사항은 다음과 같습니다.  
  
-   **단일 키 열** 각 모델은 각 레코드를 고유하게 식별하는 숫자 또는 텍스트 열을 하나 포함해야 합니다. 복합 키는 사용할 수 없습니다.  
  
-   **입력 열** Naive Bayes 모델에서는 모든 열이 불연속이거나 값이 범주화된 상태여야 합니다. 열을 불연속화(범주화)하는 방법에 대한 자세한 내용은 [분할 메서드&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/discretization-methods-data-mining.md)를 참조하세요.  
  
-   **변수는 독립적이어야 합니다.** Naive Bayes 모델의 경우 입력 특성이 서로 독립적인지도 확인해야 합니다. 이는 예측을 위해 이 모델을 사용하는 경우에 특히 중요합니다. 이미 밀접하게 관련된 두 열의 데이터를 사용하는 경우 두 열의 영향이 확대되므로 결과에 영향을 미치는 다른 요인이 불명확해질 수 있습니다.  
  
     반대로 이 알고리즘에서 변수 간의 상관 관계를 식별하는 기능은 입력 간의 관계를 식별하기 위해 모델이나 데이터 집합을 탐색하는 경우에 유용합니다.  
  
-   **하나 이상의 예측 가능한 열** 예측 가능한 특성에는 불연속 값 또는 불연속화된 값이 포함되어야 합니다.  
  
     예측 가능한 열의 값은 입력으로 처리할 수 있습니다. 이 방법은 열 간의 관계를 찾기 위해 새 데이터 집합을 탐색하는 경우에 유용할 수 있습니다.  
  
## <a name="viewing-the-model"></a>모델 보기  
 **Microsoft Naive Bayes 뷰어**를 사용하여 모델을 탐색할 수 있습니다. 이 뷰어에서는 입력 특성과 예측 가능한 특성의 관계를 보여 줍니다. 또한 뷰어에서는 각 클러스터에 대한 자세한 프로필, 각 클러스터를 다른 클러스터와 구별하게 해 주는 특성 목록 및 전체 학습 데이터 집합의 특성도 제공합니다. 자세한 내용은 [Microsoft Naive Bayes 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)를 참조하세요.  
  
 자세한 내용을 보려면 [Microsoft 일반 콘텐츠 트리 뷰어&#40;데이터 마이닝&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)에서 모델을 살펴보세요. 모델에 저장된 정보 유형에 대한 자세한 내용은 [Naive Bayes 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)을 참조하세요.  
  
## <a name="making-predictions"></a>예측  
 모델을 학습한 후에는 그 결과가 일련의 패턴으로 저장되며 이러한 패턴을 탐색하거나 사용하여 예측을 만들 수 있습니다.  
  
 새 데이터와 예측 가능한 특성의 관계에 대한 예측을 반환하는 쿼리를 만들거나 모델에서 발견된 상관 관계를 설명하는 통계를 검색할 수 있습니다.  
  
 데이터 마이닝 모델에 대한 쿼리를 만드는 방법에 대한 자세한 내용은 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)를 참조하세요. Naive Bayes 모델에서 쿼리를 사용하는 방법의 예는 [Naive Bayes 모델 쿼리 예제](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)를 참조하세요.  
  
## <a name="remarks"></a>주의  
  
-   PMML(Predictive Model Markup Language)을 사용하여 마이닝 모델을 만들 수 있습니다.  
  
-   드릴스루를 지원합니다.  
  
-   데이터 마이닝 차원의 생성은 지원하지 않습니다.  
  
-   OLAP 마이닝 모델의 사용을 지원합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [기능 선택 & #40; 데이터 마이닝 & #41;](../../analysis-services/data-mining/feature-selection-data-mining.md)   
 [Naive Bayes 모델 쿼리 예제](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)   
 [Naive Bayes 모델 & #40;에 대 한 마이닝 모델 콘텐츠 Analysis Services-데이터 마이닝 & #41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)   
 [Microsoft Naive Bayes 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)  
  
  
