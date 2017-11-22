---
title: "Microsoft 클러스터링 알고리즘 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
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
- segmentation algorithms [Analysis Services]
- nearest neighbor [Data Mining]
- clustering [Data Mining]
- clusters [Analysis Services]
- relationships [Analysis Services], clusters
- algorithms [data mining]
- classification algorithms [Analysis Services]
- datasets [Analysis Services]
- clustering algorithms [Analysis Services]
ms.assetid: 92a1e67e-f46e-4960-99b2-4d20f6192fbd
caps.latest.revision: "62"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 2d569cea784548d1e6869868f3f2e0030927b96e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-clustering-algorithm"></a>Microsoft 클러스터링 알고리즘
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘은 비슷한 특성을 포함하는 클러스터로 그룹화하는 데이터 집합의 사례를 반복하는 *세그먼트화* 또는 *클러스터링* 알고리즘입니다. 이러한 그룹화는 데이터 탐색, 데이터 내 잘못된 부분 식별, 예측 만들기 등에 유용합니다.  
  
 클러스터링 모델은 관찰만 가지고는 논리적으로 이끌어 낼 수 없을 수 있는 데이터 집합 내 관계를 식별합니다. 예를 들어 자전거로 통근하는 사람은 일반적으로 회사에서 먼 곳에 살지 않는다는 사실을 쉽게 추측할 수 있습니다. 그러나 알고리즘은 자전거 통근자에 대해 확연하게 드러나지 않는 다른 특징을 찾아낼 수 있습니다. 다음 다이어그램에서 클러스터 A는 자가용으로 통근하는 사람에 대한 데이터를 나타내고 클러스터 B는 자전거로 통근하는 사람에 대한 데이터를 나타냅니다.  
  
 ![출퇴근 자 경향에 대 한 클러스터 패턴](../../analysis-services/data-mining/media/clustering-example.gif "출퇴근 자 경향에 대 한 클러스터 패턴")  
  
 클러스터링 알고리즘은 클러스터링 모델을 작성하기 위해 예측 가능한 열을 지정하지 않아도 된다는 점에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘 등의 기타 데이터 마이닝 알고리즘과 다릅니다. 클러스터링 알고리즘은 데이터에 존재하는 관계와 알고리즘이 식별하는 클러스터를 통해서만 모델의 성향을 습득합니다.  
  
## <a name="example"></a>예제  
 인구 통계 정보가 유사하며 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 사에서 유사한 제품을 구입하는 고객 그룹을 가정해 봅니다. 이 고객 그룹은 데이터 클러스터를 나타냅니다. 데이터베이스에는 이러한 클러스터가 여러 개 존재할 수 있습니다. 클러스터를 구성하는 열을 관찰하면 데이터 집합의 레코드 간 관계를 보다 확실히 파악할 수 있습니다.  
  
## <a name="how-the-algorithm-works"></a>알고리즘 작동 방법  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘은 먼저 데이터 집합 내 관계를 식별하고 이러한 관계를 기반으로 일련의 클러스터를 생성합니다. 다음 다이어그램에서 볼 수 있는 것과 같이 알고리즘이 데이터를 그룹화하는 방법을 시각적으로 나타내는 데에는 산점도가 유용합니다. 산점도는 데이터 집합 내 모든 사례를 나타내며 각 사례는 그래프에서 하나의 점으로 표시됩니다. 클러스터는 그래프에 나타난 요소를 그룹화하고 이를 통해 알고리즘이 식별하는 관계를 보여 줍니다.  
  
 ![산 점도 데이터 집합 내에서 사례의](../../analysis-services/data-mining/media/clustering-plot.gif "데이터 집합 내에서 사례의 산 점도")  
  
 클러스터를 정의한 다음 알고리즘은 클러스터가 요소의 그룹화를 얼마나 잘 나타내는지를 계산하고 그룹화를 다시 정의하여 데이터를 보다 잘 나타내는 클러스터를 만듭니다. 알고리즘은 클러스터를 다시 정의하여 결과를 더 이상 향상시킬 수 없을 때까지 이 과정을 반복합니다.  
  
 클러스터링 기술을 지정하거나 최대 클러스터 수를 제한하거나 클러스터를 만드는 데 필요한 지지도를 변경하여 알고리즘 작동 방법을 사용자 지정할 수 있습니다. 자세한 내용은 [Microsoft 클러스터링 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)를 참조하세요. 이 알고리즘에는 널리 사용되는 두 가지 클러스터링 메서드인 K-means 클러스터링 및 Expectation Maximization 메서드가 있습니다.  
  
## <a name="data-required-for-clustering-models"></a>클러스터링 모델에 필요한 데이터  
 클러스터링 모델을 학습하는 데 사용할 데이터를 준비할 때는 필요한 데이터의 양과 사용법을 비롯한 특정 알고리즘의 요구 사항을 알고 있어야 합니다.  
  
 클러스터링 모델의 요구 사항은 다음과 같습니다.  
  
-   **단일 키 열** 각 모델은 각 레코드를 고유하게 식별하는 숫자 또는 텍스트 열을 하나 포함해야 합니다. 복합 키는 사용할 수 없습니다.  
  
-   **입력 열** 각 모델은 클러스터 작성에 사용되는 값을 포함하는 입력 열을 하나 이상 포함해야 합니다. 입력 열은 원하는 만큼 사용할 수 있지만 각 열의 값 수에 따라 추가되는 열로 인해 모델 학습에 걸리는 시간이 길어질 수 있습니다.  
  
-   **선택적 예측 가능한 열** 이 알고리즘의 경우 모델을 작성하는 데 예측 가능한 열이 필요하지는 않지만 거의 모든 데이터 형식의 예측 가능한 열을 추가할 수는 있습니다. 예측 가능한 열의 값은 클러스터링 모델에 대한 입력으로 처리되거나 예측용으로만 사용되도록 지정할 수 있습니다. 예를 들어 지역 및 연령과 같은 인구 통계를 클러스터링하여 고객의 소득을 예측하려는 경우 소득을 **PredictOnly** 로 지정한 다음 지역 또는 연령과 같은 다른 모든 열을 입력으로 추가할 수 있습니다.  
  
 클러스터링 모델에 대해 지원되는 콘텐츠 형식 및 데이터 형식에 대한 자세한 내용은 [Microsoft 클러스터링 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)의 요구 사항 섹션을 참조하세요.  
  
## <a name="viewing-a-clustering-model"></a>클러스터링 모델 보기  
 **Microsoft 클러스터 뷰어**를 사용하여 모델을 탐색할 수 있습니다. 클러스터링 모델을 탐색할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 클러스터 간의 관계를 보여 주는 다이어그램으로 클러스터를 표시하며 각 클러스터에 대한 자세한 프로필, 각 클러스터를 다른 클러스터와 구별하게 해주는 특성 목록 및 전체 학습 데이터 집합의 특징도 제공합니다. 자세한 내용은 [Microsoft 클러스터 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)를 참조하세요.  
  
 보다 자세한 내용을 보려면 [Microsoft 일반 콘텐츠 트리 뷰어](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)에서 모델을 살펴보십시오. 모델에 대해 각 노드의 모든 값 분포, 각 클러스터에 대한 확률, 기타 정보 등의 콘텐츠가 저장됩니다. 자세한 내용은 [클러스터링 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)를 참조하세요.  
  
## <a name="creating-predictions"></a>예측 만들기  
 모델을 학습한 후에는 그 결과가 일련의 패턴으로 저장되며 이러한 패턴을 탐색하거나 사용하여 예측을 만들 수 있습니다.  
  
 새 데이터가 발견된 클러스터에 맞는지 여부에 대한 예측을 반환하거나 클러스터에 대한 기술 통계를 구하는 쿼리를 만들 수 있습니다.  
  
 데이터 마이닝 모델에 대한 쿼리를 만드는 방법에 대한 자세한 내용은 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)를 참조하세요. 클러스터링 모델에서 쿼리를 사용하는 방법에 대한 예제는 [클러스터링 모델 쿼리 예제](../../analysis-services/data-mining/clustering-model-query-examples.md)를 참조하세요.  
  
## <a name="remarks"></a>주의  
  
-   PMML(Predictive Model Markup Language)을 사용하여 마이닝 모델을 만들 수 있습니다.  
  
-   드릴스루를 지원합니다.  
  
-   OLAP 마이닝 모델의 사용과 마이닝 모델 차원의 생성을 지원합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft 클러스터링 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)   
 [클러스터링 모델 &#40;에 대 한 마이닝 모델 콘텐츠 Analysis Services-데이터 마이닝 &#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)   
 [클러스터링 모델 쿼리 예제](../../analysis-services/data-mining/clustering-model-query-examples.md)  
  
  
