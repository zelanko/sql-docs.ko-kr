---
title: "Microsoft 시퀀스 클러스터링 알고리즘 | Microsoft Docs"
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
- clusters [Analysis Services]
- algorithms [data mining]
- sequence clustering algorithms [Analysis Services]
- sequence [Analysis Services]
ms.assetid: ae779a1f-0adb-4857-afbd-a15543dff299
caps.latest.revision: "49"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c64eddbe78782344e4cd3f3f6afdd48884362808
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-sequence-clustering-algorithm"></a>Microsoft 시퀀스 클러스터링 알고리즘
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘은 클러스터링과 함께 시퀀스 분석을 결합하는 고유한 알고리즘입니다. 이 알고리즘을 사용하여 *시퀀스*로 연결할 수 있는 이벤트가 들어 있는 데이터를 탐색할 수 있습니다. 이 알고리즘은 가장 일반적인 시퀀스를 찾고 클러스터링을 수행하여 유사한 시퀀스를 찾습니다. 다음 예제에서는 일반적인 문제나 비즈니스 시나리오에 대한 통찰력을 제공하기 위해 기계 학습에 대한 데이터로 캡처할 수 있는 시퀀스의 종류를 보여 줍니다.  
  
-   사용자가 웹 사이트를 탐색하거나 이동할 때 생성된 클릭스트림 또는 클릭 경로  
  
-   하드 디스크 오류 또는 서버 교착 상태와 같은 사건 앞의 이벤트를 나열하는 로그  
  
-   고객이 온라인 쇼핑 카트에 품목을 추가하는 순서를 설명하는 트랜잭션 레코드  
  
-   서비스 취소나 다른 좋지 않은 결과를 예측하기 위해 일정 기간 동안 고객 또는 환자 상호 작용을 추적하는 레코드  
  
 이 알고리즘은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘과 많은 측면에서 비슷합니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘은 유사한 특성이 포함된 사례 클러스터를 찾는 대신 시퀀스에 유사한 경로가 포함된 사례 클러스터를 찾습니다.  
  
## <a name="example"></a>예제  
 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] web site collects information about what pages site users visit, and about the order in which the pages are visited. 회사에서 온라인 주문 시스템을 제공하므로 고객은 사이트에 로그인해야 합니다. 고객이 사이트에 로그인하면 각 고객 프로필의 클릭 정보가 회사에 제공됩니다. 이 데이터에 대한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘을 사용하면 클릭 패턴 또는 시퀀스가 유사한 고객 그룹 또는 클러스터를 찾을 수 있습니다. 회사는 이러한 클러스터를 사용하여 사용자가 웹 사이트에서 어떻게 이동하는지 분석하고, 특정 제품의 판매와 가장 밀접한 관련이 있는 페이지를 식별하고, 다음에 방문할 가능성이 가장 높은 페이지를 예측할 수 있습니다.  
  
## <a name="how-the-algorithm-works"></a>알고리즘 작동 방법  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘은 클러스터링 기술에 Markov 체인 분석을 결합하여 클러스터와 해당 시퀀스를 식별하는 하이브리드 알고리즘입니다.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘의 특징 중 하나는 시퀀스 데이터를 사용한다는 점입니다. 이 데이터는 일반적으로 특정 사용자에 대한 일련의 제품 구입 또는 웹 클릭과 같은 데이터 집합의 상태 간 일련의 이벤트 또는 전환을 나타냅니다. 알고리즘은 모든 전환 가능성을 점검하고 데이터 집합에서 가능한 모든 시퀀스 간의 차이점 또는 거리를 측정하여 클러스터링에서 입력으로 사용하기에 가장 적합한 시퀀스를 확인합니다. 알고리즘은 후보 시퀀스 목록을 만든 후 EM(Expectation Maximization) 메서드를 사용하는 클러스터링에 대한 입력으로 시퀀스 정보를 사용합니다.  
  
 구현에 대한 자세한 설명은 [Microsoft Sequence Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)를 참조하십시오.  
  
## <a name="data-required-for-sequence-clustering-models"></a>시퀀스 클러스터링 모델에 필요한 데이터  
 시퀀스 클러스터링 모델을 학습하는 데 사용할 데이터를 준비할 때는 필요한 데이터의 양과 사용법을 비롯하여 특정 알고리즘의 요구 사항을 알고 있어야 합니다.  
  
 시퀀스 클러스터링 모델의 요구 사항은 다음과 같습니다.  
  
-   **단일 키 열** 시퀀스 클러스터링 모델에는 레코드를 식별하는 키가 필요합니다.  
  
-   **시퀀스 열** 시퀀스 데이터의 경우 모델에는 시퀀스 ID 열을 포함하는 중첩 테이블이 있어야 합니다. 시퀀스 ID는 정렬 가능한 모든 데이터 형식이 될 수 있습니다. 예를 들어 열이 시퀀스의 이벤트를 식별한다면 웹 페이지 식별자, 정수 또는 텍스트 문자열을 사용할 수 있습니다. 각 시퀀스마다 시퀀스 식별자가 하나만 허용되고, 각 모델마다 시퀀스 유형이 하나만 허용됩니다.  
  
-   **비시퀀스 특성(선택 사항)** 알고리즘은 시퀀스와 관계가 없는 다른 특성의 추가를 지원합니다. 이러한 특성은 중첩 열을 포함할 수 있습니다.  
  
 예를 들어 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 웹 사이트의 앞서 언급한 예에서 시퀀스 클러스터링 모델은 주문 정보를 사례 테이블로, 각 주문의 특정 고객에 대한 인구 통계를 비시퀀스 특성으로, 그리고 고객이 사이트를 탐색하거나 장바구니에 품목을 넣은 시퀀스가 포함된 중첩 테이블을 시퀀스 정보로 포함할 수 있습니다.  
  
 시퀀스 클러스터링 모델에 대해 지원되는 콘텐츠 형식 및 데이터 형식에 대한 자세한 내용은 [Microsoft 시퀀스 클러스터링 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)의 요구 사항 섹션을 참조하세요.  
  
## <a name="viewing-a-sequence-clustering-model"></a>시퀀스 클러스터링 모델 보기  
 이 알고리즘이 만든 마이닝 모델에는 데이터에서 가장 일반적인 시퀀스에 대한 설명이 들어 있습니다. **Microsoft 시퀀스 클러스터 뷰어**를 사용하여 모델을 탐색할 수 있습니다. 시퀀스 클러스터링 모델을 볼 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 여러 전환을 포함하는 클러스터가 표시됩니다. 또한 관련 통계도 볼 수 있습니다. 자세한 내용은 [Microsoft 시퀀스 클러스터 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)를 참조하세요.  
  
 보다 자세한 내용을 보려면 [Microsoft 일반 콘텐츠 트리 뷰어](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)에서 모델을 살펴보십시오. 모델에 대해 저장되는 콘텐츠에는 각 노드의 모든 값 분포, 각 클러스터에 대한 확률 및 전환의 세부 정보 등이 포함됩니다. 자세한 내용은 [시퀀스 클러스터링 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)를 참조하세요.  
  
## <a name="creating-predictions"></a>예측 만들기  
 모델을 학습한 후에는 그 결과가 일련의 패턴으로 저장됩니다. 데이터의 가장 일반적인 시퀀스에 대한 설명을 사용하여 새 시퀀스의 다음 단계를 예측할 수 있습니다. 그러나 알고리즘에는 다른 열이 포함되므로 결과 모델을 사용하여 시퀀스에 포함되는 데이터와 순차적이지 않은 입력 간의 관계를 식별할 수 있습니다. 예를 들어 모델에 인구 통계 데이터를 추가하는 경우 특정 고객 그룹에 대한 예측을 만들 수 있습니다. 예측 쿼리는 여러 개의 예측을 반환하거나 기술 통계를 반환하도록 사용자 지정할 수 있습니다.  
  
 데이터 마이닝 모델에 대한 쿼리를 만드는 방법에 대한 자세한 내용은 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)를 참조하세요. 시퀀스 클러스터링 모델에서 쿼리를 사용하는 방법에 대한 예제는 [시퀀스 클러스터링 모델 쿼리 예제](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)를 참조하세요.  
  
## <a name="remarks"></a>주의  
  
-   PMML(Predictive Model Markup Language)을 사용한 마이닝 모델 생성은 지원하지 않습니다.  
  
-   드릴스루를 지원합니다.  
  
-   OLAP 마이닝 모델의 사용과 마이닝 모델 차원의 생성을 지원합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft 시퀀스 클러스터링 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [시퀀스 클러스터링 모델 쿼리 예제](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Microsoft 시퀀스 클러스터 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  
