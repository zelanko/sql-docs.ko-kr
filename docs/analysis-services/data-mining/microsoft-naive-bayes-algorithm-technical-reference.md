---
title: "Microsoft Naive Bayes 알고리즘 기술 참조 | Microsoft Docs"
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
- MINIMUM_DEPENDENCY_PROBABILITY parameter
- MAXIMUM_INPUT_ATTRIBUTES parameter
- naive bayes model [Analysis Services]
- Bayesian classifiers
- naive bayes algorithms [Analysis Services]
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- MAXIMUM_STATES parameter
ms.assetid: a4cd47fe-2127-4930-b18f-3edd17ee9a65
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 91e15d1d56b8d548651c316d3169fc36b4a7fd04
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="microsoft-naive-bayes-algorithm-technical-reference"></a>Microsoft Naive Bayes 알고리즘 기술 참조
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 알고리즘은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 제공하는 예측 모델링용 분류 알고리즘입니다. 이 알고리즘은 입력 열과 예측 가능한 열 간의 조건부 확률을 계산하며 열이 서로 독립적이라고 가정합니다. 이와 같은 독립성 가정으로 인해 Naive Bayes라는 이름이 붙었습니다.  
  
## <a name="implementation-of-the-microsoft-naive-bayes-algorithm"></a>Microsoft Naive Bayes 알고리즘 구현  
 이 알고리즘은 다른 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘보다 계산 과정이 단순하여 입력 열과 예측 가능한 열 간의 관계를 검색하는 마이닝 모델을 신속하게 생성하는 데 유용합니다. 이 알고리즘은 입력 특성 값과 출력 특성 값의 각 쌍을 고려합니다.  
  
 이 설명서에서는 Bayes 정리의 수학적 속성에 대해 설명하지 않습니다. 이에 대한 자세한 내용은 [Bayesian 네트워크 학습: 지식 및 통계 데이터의 조합](http://go.microsoft.com/fwlink/?LinkId=207029)이라는 제목의 Microsoft Research 자료를 참조하세요.  
  
 모든 모델의 확률이 잠재적인 누락 값을 설명하기 위해 조정되는 방식에 대한 설명은 [누락 값&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)을 참조하세요.  
  
### <a name="feature-selection"></a>기능 선택  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 알고리즘은 자동 기능 선택을 수행하여 모델을 작성할 때 고려되는 값의 수를 제한합니다. 자세한 내용은 [기능 선택&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/feature-selection-data-mining.md)을 참조하세요.  
  
|알고리즘|분석 방법|설명|  
|---------------|------------------------|--------------|  
|Naive Bayes|Shannon Entropy<br /><br /> Bayesian with K2 Prior<br /><br /> Bayesian Dirichlet with uniform prior(기본값)|Naive Bayes는 불연속 또는 분할된 특성만 허용하므로 흥미도 점수를 사용할 수 없습니다.|  
  
 이 알고리즘은 처리 시간을 최소화하고 가장 중요한 특성을 효율적으로 선택할 수 있도록 디자인되었습니다. 그러나 사용자가 다음과 같은 매개 변수를 설정하여 알고리즘에 사용되는 데이터를 제어할 수도 있습니다.  
  
-   입력으로 사용되는 값을 제한하려면 MAXIMUM_INPUT_ATTRIBUTES 값을 줄입니다.  
  
-   모델이 분석하는 특성의 수를 제한하려면 MAXIMUM_OUTPUT_ATTRIBUTES 값을 줄입니다.  
  
-   하나의 특성에 대해 고려할 수 있는 값의 수를 제한하려면 MINIMUM_STATES 값을 줄입니다.  
  
## <a name="customizing-the-naive-bayes-algorithm"></a>Naive Bayes 알고리즘 사용자 지정  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 알고리즘은 결과 마이닝 모델의 동작, 성능 및 정확도에 영향을 주는 여러 매개 변수를 지원합니다. 모델 열에 모델링 플래그를 설정하여 데이터 처리 방식을 제어하거나, 마이닝 구조에 플래그를 설정하여 누락 값 또는 Null이 처리되는 방식을 지정할 수도 있습니다.  
  
### <a name="setting-algorithm-parameters"></a>알고리즘 매개 변수 설정  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 알고리즘은 결과 마이닝 모델의 성능 및 정확도에 영향을 주는 여러 매개 변수를 지원합니다. 다음 표에서는 각 매개 변수에 대해 설명합니다.  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 기능 선택을 호출하기 전에 알고리즘이 처리할 수 있는 최대 입력 특성 수를 지정합니다. 이 값을 0으로 설정하면 입력 특성에 대해 기능 선택을 사용할 수 없습니다.  
  
 기본값은 255입니다.  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 기능 선택을 호출하기 전에 알고리즘이 처리할 수 있는 최대 출력 특성 수를 지정합니다. 이 값을 0으로 설정하면 출력 특성에 대해 기능 선택을 사용할 수 없습니다.  
  
 기본값은 255입니다.  
  
 *MINIMUM_DEPENDENCY_PROBABILITY*  
 입력 특성과 출력 특성 간의 최소 종속성 확률을 지정합니다. 이 값은 알고리즘에서 생성하는 내용의 크기를 제한하는 데 사용됩니다. 이 속성은 0과 1 사이의 값으로 설정할 수 있습니다. 이보다 큰 값을 지정하면 모델 내용의 특성 수가 감소합니다.  
  
 기본값은 0.5입니다.  
  
 *MAXIMUM_STATES*  
 알고리즘이 지원하는 최대 특성 상태 수를 지정합니다. 특성의 상태 수가 최대 상태 수보다 많으면 알고리즘은 가장 많이 사용되는 특성 상태를 사용하고 나머지 상태를 누락된 것으로 처리합니다.  
  
 기본값은 100입니다.  
  
### <a name="modeling-flags"></a>모델링 플래그  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘은 다음과 같은 모델링 플래그를 지원합니다. 마이닝 구조나 마이닝 모델을 만들 경우 분석 중 각 열의 값이 처리되는 방법을 지정하기 위해 모델링 플래그를 정의합니다. 자세한 내용은 [모델링 플래그&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)를 참조하세요.  
  
|모델링 플래그|Description|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|열이 누락 및 있음 상태를 갖는 것으로 간주됩니다. Null은 누락 값입니다.<br /><br /> 마이닝 모델 열에 적용됩니다.|  
|NOT  NULL|열에 null이 포함될 수 없음을 나타냅니다. 따라서 Analysis Services가 모델 학습 중 Null을 발견할 경우 오류가 발생합니다.<br /><br /> 마이닝 구조 열에 적용됩니다.|  
  
## <a name="requirements"></a>요구 사항  
 Naive Bayes 트리 모델은 하나의 키 열, 하나 이상의 예측 가능한 특성 및 하나 이상의 입력 특성을 포함해야 합니다. 특성은 연속일 수 없으므로 데이터에 연속 숫자 데이터가 들어 있는 경우 해당 데이터는 무시되거나 분할됩니다.  
  
### <a name="input-and-predictable-columns"></a>입력 열과 예측 가능한 열  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 알고리즘은 다음 표에 나열된 특정 입력 열과 예측 가능한 열을 지원합니다. 마이닝 모델에 사용되는 경우 콘텐츠 형식의 의미에 대한 자세한 내용은 [콘텐츠 형식&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/content-types-data-mining.md)을 참조하세요.  
  
|열|내용 유형|  
|------------|-------------------|  
|입력 특성|Cyclical, Discrete, Discretized, Key, Table 및 Ordered|  
|예측 가능한 특성|Cyclical, Discrete, Discretized, Table 및 Ordered|  
  
> [!NOTE]  
>  Cyclical  및 Ordered  내용 유형이 지원되기는 하지만 알고리즘은 해당 유형을 불연속 값으로 처리하고 특수한 처리를 수행하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft Naive Bayes 알고리즘](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)   
 [Naive Bayes 모델 쿼리 예제](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)   
 [Naive Bayes 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  

