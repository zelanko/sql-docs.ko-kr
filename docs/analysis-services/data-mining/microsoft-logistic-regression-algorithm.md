---
title: "Microsoft 로지스틱 회귀 알고리즘 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logical regression algorithms [Analysis Services]
- algorithms [data mining]
- neural network algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 3dd54d07-1c3b-4b87-b7f0-b962ed8cf844
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c4d3e835e6620ed5e4efb551d3e3ebcde7cf3bf8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="microsoft-logistic-regression-algorithm"></a>Microsoft 로지스틱 회귀 알고리즘
  로지스틱 회귀는 이진 결과 모델링에 사용되는 유명한 통계 기법입니다.  
  
 통계 연구에는 여러 가지 학습 기법을 사용하는 로지스틱 회귀의 다양한 구현이 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 로지스틱 회귀 알고리즘은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 신경망 알고리즘의 변형을 사용하여 구현되었습니다. 이 알고리즘은 신경망의 많은 특성을 공유하지만 학습하기가 더 쉽습니다.  
  
 로지스틱 회귀는 매우 유연하여 모든 종류의 입력을 사용하며 다음과 같은 여러 가지 분석 태스크를 지원한다는 이점이 있습니다.  
  
-   특정 질병의 위험성과 같은 결과를 예측하려면 인구 통계를 사용합니다.  
  
-   결과에 영향을 주는 요소를 조사하여 가중치를 적용합니다. 예를 들어 고객이 상점을 다시 방문하도록 하는 요소를 찾습니다.  
  
-   문서, 전자 메일 또는 여러 특성이 있는 기타 개체를 분류합니다.  
  
## <a name="example"></a>예제  
 인구 통계 정보가 유사하며 Adventure Works사에서 제품을 구입하는 고객 그룹을 가정해 봅니다. 대상 제품 구매 등의 특정 결과와 관계되도록 데이터를 모델링하여 인구 통계 정보에 따라 대상 제품에 대한 고객의 구매 가능성이 어떻게 달라지는지 확인할 수 있습니다.  
  
## <a name="how-the-algorithm-works"></a>알고리즘 작동 방법  
 로지스틱 회귀는 한 쌍의 결과에 대한 여러 요소의 기여도를 측정하는 유명한 통계 기법입니다. Microsoft에서 구현한 방법은 수정된 신경망을 사용하여 입력과 출력 간의 관계를 모델링하는 것입니다. 즉, 각 입력이 출력에 주는 영향을 측정하고 완성된 모델에서 다양한 입력에 가중치를 적용합니다. 로지스틱 회귀라는 이름은 데이터 곡선이 로지스틱 변환을 통해 요약되어 극단적인 값으로 인한 영향을 최소화한다는 사실에서 비롯된 것입니다. 구현에 대한 자세한 내용과 알고리즘을 사용자 지정하는 방법에 대한 자세한 내용은 [Microsoft 로지스틱 회귀 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)를 참조하세요.  
  
## <a name="data-required-for-logistic-regression-models"></a>로지스틱 회귀 모델에 필요한 데이터  
 로지스틱 회귀 모델을 학습하는 데 사용할 데이터를 준비할 때는 필요한 데이터의 양과 사용법을 비롯하여 특정 알고리즘의 요구 사항을 알고 있어야 합니다.  
  
 로지스틱 회귀 모델의 요구 사항은 다음과 같습니다.  
  
 **단일 키 열** 각 모델은 각 레코드를 고유하게 식별하는 숫자 또는 텍스트 열을 하나 포함해야 합니다. 복합 키는 사용할 수 없습니다.  
  
 **입력 열** 각 모델은 분석에서 요소로 사용되는 값을 포함하는 입력 열을 하나 이상 포함해야 합니다. 입력 열은 원하는 만큼 사용할 수 있지만 각 열의 값 수에 따라 추가되는 열로 인해 모델 학습에 걸리는 시간이 길어질 수 있습니다.  
  
 **하나 이상의 예측 가능한 열** 모델은 연속 숫자 데이터를 포함하여 모든 데이터 형식의 예측 가능한 열을 하나 이상 포함해야 합니다. 또한 예측 가능한 열의 값은 모델에 대한 입력으로 처리될 수도 있고, 이를 예측용으로만 사용하도록 지정할 수도 있습니다. 중첩 테이블은 예측 가능한 열에 사용할 수 없지만 입력으로는 사용할 수 있습니다.  
  
 로지스틱 회귀 모델에 대해 지원되는 콘텐츠 형식 및 데이터 형식에 대한 자세한 내용은 [Microsoft 로지스틱 회귀 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)의 요구 사항 섹션을 참조하세요.  
  
## <a name="viewing-a-logistic-regression-model"></a>로지스틱 회귀 모델 보기  
 모델을 탐색하려면 Microsoft 신경망 뷰어 또는 Microsoft 일반 콘텐츠 트리 뷰어를 사용합니다.  
  
 Microsoft 신경망 뷰어를 사용하여 모델을 보는 경우 Analysis Services에서는 특정 결과에 영향을 주는 요소를 중요도에 따라 순위를 지정하여 표시합니다. 비교할 특성 및 값은 사용자가 선택할 수 있습니다. 자세한 내용은 [Microsoft 신경망 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)를 참조하세요.  
  
 보다 자세한 내용을 보려면 Microsoft 일반 콘텐츠 트리 뷰어를 사용하여 모델 세부 정보를 살펴보세요. 로지스틱 회귀 모델의 모델 콘텐츠에는 모델에 사용된 모든 입력과 예측 가능한 특성의 하위 네트워크를 보여 주는 한계 노드가 포함되어 있습니다. 자세한 내용은 [로지스틱 회귀 분석 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)를 참조하세요.  
  
## <a name="creating-predictions"></a>예측 만들기  
 모델을 학습한 후에는 모델 콘텐츠에 대한 쿼리를 만들어 회귀 계수 및 기타 세부 정보를 가져오거나, 모델을 사용하여 예측을 만들 수 있습니다.  
  
-   데이터 마이닝 모델에 대한 쿼리를 만드는 방법에 대한 일반적인 내용은 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)를 참조하세요.  
  
-   로지스틱 회귀 모델에 대한 쿼리 예는 [클러스터링 모델 쿼리 예제](../../analysis-services/data-mining/clustering-model-query-examples.md)를 참조하세요.  
  
## <a name="remarks"></a>주의  
  
-   드릴스루는 지원하지 않습니다. 이는 마이닝 모델의 노드 구조가 기본 데이터와 반드시 일치하지는 않기 때문입니다.  
  
-   데이터 마이닝 차원의 생성은 지원하지 않습니다.  
  
-   OLAP 마이닝 모델의 사용을 지원합니다.  
  
-   PMML(Predictive Model Markup Language)을 사용한 마이닝 모델 생성은 지원하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [로지스틱 회귀 분석 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)   
 [Microsoft 로지스틱 회귀 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)   
 [로지스틱 회귀 모델 쿼리 예제](../../analysis-services/data-mining/logistic-regression-model-query-examples.md)  
  
  

