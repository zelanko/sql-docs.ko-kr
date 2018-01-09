---
title: "데이터 마이닝 알고리즘 (Analysis Services-데이터 마이닝) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
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
- segmentation algorithms [Analysis Services]
- clustering [Data Mining]
- learning algorithms
- data mining [Analysis Services], models
- algorithms [data mining]
- mining models [Analysis Services], algorithms
- inductive learning
- mining models [Analysis Services], creating
- data mining [Analysis Services], algorithms
- machine learning algorithms [Analysis Services]
ms.assetid: ed1fc83b-b98c-437e-bf53-4ff001b92d64
caps.latest.revision: "74"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 43652986e789837299feacf5387cd8b6e6d57a8b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="data-mining-algorithms-analysis-services---data-mining"></a>데이터 마이닝 알고리즘(Analysis Services - 데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]*알고리즘* 데이터 마이닝 (또는 기계 학습)는 데이터 로부터 모델을 만드는 추론 및 계산의 집합입니다. 모델을 만들기 위해 알고리즘은 제공된 데이터를 분석하여 특정 유형의 패턴 또는 추세를 찾습니다. 알고리즘은 많은 반복을 통해 이 분석 결과를 사용하여 마이닝 모델을 만들기 위한 최적의 매개 변수를 찾습니다. 그런 다음 이러한 매개 변수를 전체 데이터 집합에 적용하여 동작 가능한 패턴과 자세한 통계를 추출합니다.  
  
 알고리즘이 데이터로부터 만드는 마이닝 모델은 다음과 같은 다양한 형태가 될 수 있습니다.  
  
-   데이터 집합의 사례 간 관계를 설명하는 일련의 클러스터  
  
-   결과를 예측하고 각 조건이 결과에 미치는 영향을 설명하는 의사 결정 트리  
  
-   판매를 예측하는 수학적 모델  
  
-   트랜잭션에서 제품이 그룹화되는 방법과 제품을 함께 구입할 확률을 설명하는 일련의 규칙  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝에 제공된 알고리즘은 데이터의 패턴을 파생하는, 가장 널리 사용되며 적절한 연구를 거친 메서드입니다. 한 가지 예를 들면 K-means 클러스터링은 가장 오래된 클러스터링 알고리즘 중 하나이며 다양한 구현 및 옵션과 함께 다양한 도구에서 광범위하게 사용할 수 있습니다. 반면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝에 사용되는 K-means 클러스터링의 특정 구현은 Microsoft Research에서 개발되어 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 성능이 최적화되었습니다. 모든 Microsoft 데이터 마이닝 알고리즘은 제공된 API를 사용하여 광범위하게 사용자 지정하고 완전히 프로그래밍할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 데이터 마이닝 구성 요소를 사용하여 모델 만들기, 교육 및 재학습을 자동화할 수도 있습니다.  
  
 OLE DB for Data Mining 사양을 준수하는 타사 알고리즘을 사용하거나 서비스로 등록한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝 프레임워크에서 사용할 수 있는 사용자 지정 알고리즘을 개발할 수도 있습니다.  
  
## <a name="choosing-the-right-algorithm"></a>알고리즘 선택  
 특정 분석 태스크에 적합한 알고리즘을 선택하는 것은 결코 쉽지 않습니다. 동일한 비즈니스 태스크를 수행하기 위해 여러 알고리즘을 사용할 수 있지만 이렇게 하면 각 알고리즘에서 다른 결과를 생성하며 일부 알고리즘에서는 두 개 이상의 결과 유형을 생성할 수 있습니다. 예를 들어 의사 결정 트리가 최종 마이닝 모델에 영향을 미치지 않는 열을 식별할 수 있기 때문에 예측하거나 데이터 집합의 열 수를 줄이는 데 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘을 사용할 수 있습니다.  
  
### <a name="choosing-an-algorithm-by-type"></a>유형별 알고리즘 선택  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝에는 다음과 같은 알고리즘 유형이 포함되어 있습니다.  
  
-   데이터 집합의 다른 특성을 기반으로 하나 이상의 불연속 변수를 예측하는**분류 알고리즘** .  
  
-   데이터 집합의 다른 특성을 기반으로 수익 또는 손실과 같은 하나 이상의 연속 변수를 예측하는**회귀 알고리즘** .  
  
-   데이터를 속성이 유사한 항목의 그룹 또는 클러스터로 나누는**세그먼트화 알고리즘** .  
  
-   데이터 집합에 있는 여러 특성 사이의 상관 관계를 찾는**연결 알고리즘** . 이러한 종류의 알고리즘은 시장 바구니 분석에 사용할 수 있는 연결 규칙을 만드는 데 가장 일반적으로 적용됩니다.  
  
-   **시퀀스 분석 알고리즘** 은 웹 사이트에서 일련의 클릭 또는 컴퓨터 유지 관리 앞의 일련의 로그 이벤트와 같이 데이터에서 빈번한 시퀀스 또는 에피소드를 요약합니다.  
  
 솔루션에서 알고리즘을 하나로 제한해야 할 이유는 없습니다. 경험이 많은 분석가는 경우에 따라 하나의 알고리즘을 사용하여 가장 효율적인 입력(즉, 변수)을 결정하고, 다른 알고리즘을 적용하여 해당 데이터를 기반으로 특정 결과를 예측하기도 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝을 사용하여 단일의 마이닝 구조에서 여러 모델을 작성할 수 있으므로, 단일 데이터 마이닝 솔루션에서 클러스터링 알고리즘, 의사 결정 트리 모델 및 Naïve Bayes 모델을 사용하여 데이터를 다양하게 표시할 수 있습니다. 또한 단일 솔루션 내에서 여러 알고리즘을 사용하여 별도 태스크를 수행할 수도 있습니다. 예를 들어 회귀를 사용하여 재무 예측을 가져오고, 신경망 알고리즘을 사용하여 예측에 영향을 주는 요소를 분석할 수 있습니다.  
  
### <a name="choosing-an-algorithm-by-task"></a>태스크별 알고리즘 선택  
 특정 태스크에서 사용할 알고리즘을 선택하는 데 도움이 되도록 다음 표에서는 각 알고리즘이 일반적으로 사용되는 태스크 유형을 제안합니다.  
  
|태스크 예|사용할 Microsoft 알고리즘|  
|-----------------------|---------------------------------|  
|**불연속 특성 예측:**<br /><br /> 잠재 구매자 목록에서 잠재 고객을 좋음 또는 나쁨 플래그로 지정합니다.<br /><br /> 다음 6개월 이내에 서버가 실패할 확률을 계산합니다.<br /><br /> 환자 결과를 분류하고 관련 요인을 탐색합니다.|[Microsoft 의사 결정 트리 알고리즘](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft Naive Bayes 알고리즘](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)<br /><br /> [Microsoft 클러스터링 알고리즘](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft 신경망 알고리즘](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)|  
|**연속 특성 예측:**<br /><br /> 내년 매출을 예측합니다.<br /><br /> 과거 기록 및 계절별 추세를 고려하여 사이트 방문자를 예측합니다.<br /><br /> 인구 통계를 고려하여 위험 점수를 생성합니다.|[Microsoft 의사 결정 트리 알고리즘](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft 시계열 알고리즘](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)<br /><br /> [Microsoft 선형 회귀 알고리즘](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)|  
|**시퀀스 예측:**<br /><br /> 회사 웹 사이트의 클릭 동향 분석을 수행합니다.<br /><br /> 서버 장애를 일으키는 요인을 분석합니다.<br /><br /> 외래 환자가 내원 중에 수행하는 일련의 활동을 캡처한 후 분석하여 일반 활동에 대한 모범 사례를 공식화합니다.|[Microsoft 시퀀스 클러스터링 알고리즘](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)|  
|**트랜잭션에서 공통 항목 그룹 찾기:**<br /><br /> 시장 바구니 분석을 사용하여 제품 배치를 결정할 수 있습니다.<br /><br /> 구매 고객에게 추가 제품을 제안합니다.<br /><br /> 이벤트에 대한 방문자의 설문 조사 데이터를 분석하여 상호 관련된 활동 또는 부스를 찾고 미래 활동을 계획합니다.|[Microsoft 연결 알고리즘](../../analysis-services/data-mining/microsoft-association-algorithm.md)<br /><br /> [Microsoft 의사 결정 트리 알고리즘](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)|  
|**유사 항목 그룹 찾기:**<br /><br /> 인구 통계, 동작 등과 같은 특성을 기반으로 환자 위험 프로필 그룹을 만듭니다.<br /><br /> 검색 및 구매 패턴별로 사용자를 분석합니다.<br /><br /> 사용 특징이 유사한 서버를 식별합니다.|[Microsoft 클러스터링 알고리즘](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft 시퀀스 클러스터링 알고리즘](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)|  
  
## <a name="related-content"></a>관련 내용  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝에 제공되는 각 데이터 마이닝 알고리즘에 대한 학습 리소스를 연결하는 링크를 제공합니다.  
  
|||  
|-|-|  
|**알고리즘 기본 사항 설명**|알고리즘에서 수행하는 작업과 작업 방법을 설명하고 알고리즘이 유용할 수 있는 비즈니스 시나리오를 간략하게 설명합니다.|  
||[Microsoft 연결 알고리즘](../../analysis-services/data-mining/microsoft-association-algorithm.md)<br /><br /> [Microsoft 클러스터링 알고리즘](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft 의사 결정 트리 알고리즘](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft 선형 회귀 알고리즘](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)<br /><br /> [Microsoft 로지스틱 회귀 알고리즘](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)<br /><br /> [Microsoft Naive Bayes 알고리즘](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)<br /><br /> [Microsoft 신경망 알고리즘](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)<br /><br /> [Microsoft 시퀀스 클러스터링 알고리즘](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)<br /><br /> [Microsoft 시계열 알고리즘](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)|  
|**기술 참조**|알고리즘 구현에 대한 기술 정보를 제공하고 필요한 경우 학술 참조를 제공합니다. 알고리즘의 동작을 제어하고 모델 결과를 사용자 지정하기 위해 설정할 수 있는 매개 변수를 나열합니다. 데이터 요구 사항에 설명하고 가능한 경우 성능 팁을 제공합니다.|  
||[Microsoft 연결 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)<br /><br /> [Microsoft 클러스터링 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)<br /><br /> [Microsoft 의사 결정 트리 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)<br /><br /> [Microsoft 선형 회귀 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)<br /><br /> [Microsoft 로지스틱 회귀 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)<br /><br /> [Microsoft Naive Bayes 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)<br /><br /> [Microsoft 신경망 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)<br /><br /> [Microsoft 시퀀스 클러스터링 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)<br /><br /> [Microsoft 시계열 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)|  
|**모델 콘텐츠**|각 데이터 마이닝 모델 유형에서 정보가 구성되는 방법과 각 노드에 저장된 정보를 해석하는 방법을 설명합니다.|  
||[연결 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)<br /><br /> [클러스터링 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)<br /><br /> [의사 결정 트리 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)<br /><br /> [선형 회귀 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)<br /><br /> [로지스틱 회귀 분석 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)<br /><br /> [Naive Bayes 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)<br /><br /> [신경망 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)<br /><br /> [시퀀스 클러스터링 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)<br /><br /> [시계열 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)|  
|**데이터 마이닝 쿼리**|각 모델 유형과 함께 사용할 수 있는 여러 쿼리를 제공합니다. 모델의 패턴에 대해 알아 볼 수 있는 내용 쿼리 및 패턴을 기반으로 예측을 작성하는 데 도움이 되는 예측 쿼리 등을 예로 들 수 있습니다.|  
||[연결 모델 쿼리 예제](../../analysis-services/data-mining/association-model-query-examples.md)<br /><br /> [클러스터링 모델 쿼리 예제](../../analysis-services/data-mining/clustering-model-query-examples.md)<br /><br /> [의사 결정 트리 모델 쿼리 예제](../../analysis-services/data-mining/decision-trees-model-query-examples.md)<br /><br /> [선형 회귀 모델 쿼리 예제](../../analysis-services/data-mining/linear-regression-model-query-examples.md)<br /><br /> [로지스틱 회귀 모델 쿼리 예제](../../analysis-services/data-mining/logistic-regression-model-query-examples.md)<br /><br /> [Naive Bayes 모델 쿼리 예제](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)<br /><br /> [신경망 모델 쿼리 예제](../../analysis-services/data-mining/neural-network-model-query-examples.md)<br /><br /> [시퀀스 클러스터링 모델 쿼리 예제](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)<br /><br /> [시계열 모델 쿼리 예제](../../analysis-services/data-mining/time-series-model-query-examples.md)|  
  
## <a name="related-tasks"></a>관련 작업  
  
|**항목**|**설명**|  
|---------------|---------------------|  
|데이터 마이닝 모델에 사용되는 알고리즘 결정|[마이닝 모델을 만드는 데 사용한 매개 변수 쿼리](../../analysis-services/data-mining/query-the-parameters-used-to-create-a-mining-model.md)|  
|사용자 지정 플러그 인 알고리즘 만들기|[플러그 인 알고리즘](../../analysis-services/data-mining/plugin-algorithms.md)|  
|알고리즘별 뷰어를 사용하여 모델 탐색|[데이터 마이닝 모델 뷰어](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|일반 테이블 형식을 사용하여 모델 내용 보기|[Microsoft 일반 콘텐츠 트리 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)|  
|데이터를 설정하고 알고리즘을 사용하여 모델을 만드는 방법에 대해 알아봅니다|[마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)<br /><br /> [마이닝 모델&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 도구](../../analysis-services/data-mining/data-mining-tools.md)  
  
  
