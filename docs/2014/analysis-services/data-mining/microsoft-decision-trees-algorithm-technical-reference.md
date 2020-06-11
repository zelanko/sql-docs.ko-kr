---
title: Microsoft 의사 결정 트리 알고리즘 기술 참조 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_INPUT_ATTRIBUTES parameter
- SPLIT_METHOD parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- FORCED_REGRESSOR parameter
- decision tree algorithms [Analysis Services]
- decision trees [Analysis Services]
- COMPLEXITY_PENALTY parameter
- SCORE_METHOD parameter
ms.assetid: 1e9f7969-0aa6-465a-b3ea-57b8d1c7a1fd
author: minewiskan
ms.author: owend
ms.openlocfilehash: f6e2322553eef361f0131e3558cd591bc32525ef
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522169"
---
# <a name="microsoft-decision-trees-algorithm-technical-reference"></a>Microsoft 의사 결정 트리 알고리즘 기술 참조
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘은 트리를 만드는 여러 방법을 통합하며 회귀, 분류, 연결 등의 여러 분석 태스크를 지원하는 하이브리드 알고리즘입니다. Microsoft 의사 결정 트리 알고리즘은 불연속 특성과 연속 특성 모두의 모델링을 지원합니다.  
  
 이 항목에서는 알고리즘의 구현을 설명하고, 여러 태스크에 대한 알고리즘 동작을 사용자 지정하는 방법을 설명하며, 의사 결정 트리 모델 쿼리에 대한 추가 정보로 연결되는 링크를 제공합니다.  
  
## <a name="implementation-of-the-decision-trees-algorithm"></a>의사 결정 트리 알고리즘의 구현  
 Microsoft 의사 결정 트리 알고리즘은 모델에 대한 근사 사후 분포를 가져옴으로써 Bayesian 방법을 학습 인과 상호 작용 모델에 적용합니다. 이 방법에 대한 자세한 내용은 Microsoft Research 사이트의 자료, [구조와 매개 변수 학습](https://go.microsoft.com/fwlink/?LinkId=237640&clcid=0x409)을 참조하십시오.  
  
 학습에 필요한 *사전 지식* 의 정보 값을 평가하는 방법은 *가능성 등가*의 가정을 기반으로 합니다. 이 가정은 조건부 독립성의 동일한 단정을 다른 방법으로 나타내는 네트워크 구조를 판별하는 데 데이터가 유용하지 않다는 가정입니다. 각 사례는 하나의 Bayesian 사전 지식 네트워크와 해당 네트워크의 신뢰성에 대한 하나의 측정값을 포함하는 것으로 가정됩니다.  
  
 알고리즘은 이러한 사전 지식 네트워크를 사용하여 현재 학습 데이터에 대해 네트워크 구조의 상대적 *사후 확률* 을 계산하고 사후 확률이 가장 높은 네트워크 구조를 식별합니다.  
  
 Microsoft 의사 결정 트리 알고리즘에서는 다양한 방법을 사용하여 최상의 트리를 컴퓨팅합니다. 사용되는 방법은 태스크에 따라 선형 회귀, 분류 또는 연결 분석일 수 있습니다. 하나의 모델이 예측 가능한 여러 특성에 대한 여러 개의 트리를 포함할 수 있습니다. 또한 각 트리는 데이터에 있는 특성 및 값의 수에 따라 여러 분기를 포함할 수 있습니다. 특정 모델에 작성되는 트리의 형태와 깊이는 점수 매기기 방법과 사용된 기타 매개 변수에 따라 달라집니다. 매개 변수의 변경 내용은 노드 분할 위치에도 영향을 줍니다.  
  
### <a name="building-the-tree"></a>트리 작성  
 Microsoft 의사 결정 트리 알고리즘은 가능한 입력 값 집합을 만들 때 *feature selection* 을 수행하여 가장 많은 정보를 제공하는 특성 및 값을 식별하고 매우 드물게 나타나는 값은 고려하지 않습니다. 또한 이 알고리즘은 값을 *Bin*에 그룹화하여 성능을 최적화하기 위해 한 단위로 처리할 수 있는 값 그룹을 만듭니다.  
  
 트리는 입력과 목표 결과 간의 상관 관계를 확인하여 작성됩니다. 모든 특성의 상관 관계가 확인된 후 알고리즘은 결과를 가장 명확하게 구분하는 단일 특성을 식별합니다. 최상의 구분 지점은 얻은 정보를 계산하는 수식을 사용하여 측정됩니다. 얻은 정보에 대한 최상의 점수가 있는 특성은 사례를 하위 집합으로 나누는 데 사용되고 하위 집합은 트리를 더 이상 분할할 수 없을 때까지 동일한 프로세스에서 재귀적으로 분석됩니다.  
  
 얻은 정보를 계산하는 데 사용되는 정확한 수식은 알고리즘을 만들 때 설정한 매개 변수, 예측 가능한 열의 데이터 형식 및 입력의 데이터 형식에 따라 달라집니다.  
  
### <a name="discrete-and-continuous-inputs"></a>불연속 및 연속 입력  
 예측 가능한 특성과 입력이 모두 불연속적일 경우 입력당 결과 수를 계산하려면 행렬을 만들고 해당 행렬에 있는 각 셀에 대한 점수를 생성해야 합니다.  
  
 그러나 예측 가능한 특성이 불연속적이고 입력이 연속적일 경우에는 연속 열의 입력이 자동으로 분할됩니다. 기본값을 그대로 사용하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 최적의 Bin 수를 찾도록 설정할 수도 있고, <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 및 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 속성을 설정하여 연속 입력이 불연속화되는 방식을 제어할 수도 있습니다. 자세한 내용은 [마이닝 모델에서 열의 불연속화 변경](change-the-discretization-of-a-column-in-a-mining-model.md)을 참조하세요.  
  
 연속 특성의 경우 알고리즘은 선형 회귀를 사용하여 의사 결정 트리의 분할 위치를 결정합니다.  
  
 예측 가능한 특성이 연속 숫자 데이터 형식일 경우 기능 선택은 출력에도 적용되어 가능한 결과 수를 줄이므로 모델을 보다 빠르게 작성할 수 있습니다. 기능 선택의 임계값을 변경하고 그에 따라 MAXIMUM_OUTPUT_ATTRIBUTES 매개 변수를 설정하여 가능한 값의 수를 늘리거나 줄일 수 있습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘에서 예측 가능한 불연속 열을 사용하는 방법은 [Bayesian 네트워크 학습: 지식 및 통계 데이터의 조합(Learning Bayesian Networks: The Combination of Knowledge and Statistical Data)](https://go.microsoft.com/fwlink/?LinkId=45963)을 참조하세요. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘에서 예측 가능한 연속 열을 사용하는 방법에 대한 자세한 내용은 [시계열 분석을 위한 자동 회귀 트리 모델](https://go.microsoft.com/fwlink/?LinkId=45966)의 부록을 참조하세요.  
  
### <a name="scoring-methods-and-feature-selection"></a>점수 매기기 방법 및 기능 선택  
 Microsoft 의사 결정 트리 알고리즘에서는 얻은 정보를 평가하기 위한 Shannon's entropy, Bayesian network with K2 prior 및 Bayesian network with a uniform Dirichlet distribution of priors라는 세 개의 수식을 제공합니다. 세 방법 모두 데이터 마이닝 분야에서 잘 수립된 방법입니다., 여러 가지 매개 변수와 점수 매기기 방법을 사용해 보고 어느 것이 최상의 결과를 제공하는지 확인하는 것이 좋습니다. 이러한 점수 매기기 방법에 대한 자세한 내용은 [Feature Selection](../../sql-server/install/feature-selection.md)을 참조하십시오.  
  
 모든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 마이닝 알고리즘에서는 자동으로 기능 선택을 사용하여 분석을 향상시키고 처리 로드를 줄입니다. 기능 선택에 사용되는 방법은 모델을 작성하는 데 사용된 알고리즘에 따라 달라집니다. 의사 결정 트리 모델의 기능 선택을 제어하는 알고리즘 매개 변수는 MAXIMUM_INPUT_ATTRIBUTES와 MAXIMUM_OUTPUT입니다.  
  
|알고리즘|분석 방법|의견|  
|---------------|------------------------|--------------|  
|의사 결정 트리|흥미도 점수<br /><br /> Shannon Entropy<br /><br /> Bayesian with K2 Prior<br /><br /> Bayesian Dirichlet with uniform prior(기본값)|이진이 아닌 연속 값이 열에 포함되어 있는 경우 일관성을 보장하기 위해 모든 열에 흥미도 점수가 사용됩니다. 그렇지 않을 경우 기본 방법이나 지정된 방법이 사용됩니다.|  
|선형 회귀|흥미도 점수|선형 회귀는 연속 열만 지원하므로 흥미도 점수만 사용합니다.|  
  
### <a name="scalability-and-performance"></a>확장성 및 성능  
 분류는 중요한 데이터 마이닝 전략입니다. 일반적으로 사례를 분류하는 데 필요한 정보의 양은 입력 레코드의 수에 직접적으로 비례하여 증가합니다. 이로 인해 분류할 수 있는 데이터의 크기가 제한됩니다. Microsoft 의사 결정 트리 알고리즘에서는 다음 방법을 사용하여 이러한 문제를 해결하고 성능을 향상시키고 메모리 제한을 제거합니다.  
  
-   기능 선택을 사용하여 특성 선택을 최적화합니다.  
  
-   Bayesian 점수 매기기를 사용하여 트리 증가를 제어합니다.  
  
-   연속 특성에 대한 Bin 생성을 최적화합니다.  
  
-   입력 값을 동적으로 그룹화하여 가장 중요한 값을 확인합니다.  
  
 Microsoft 의사 결정 트리 알고리즘은 빠르고 확장 가능할 뿐 아니라, 쉽게 병렬 처리할 수 있도록 디자인되었으므로 모든 프로세서가 함께 작동하여 하나의 일관된 모델을 작성합니다. 이러한 모든 특성으로 인해 의사 결정 트리 분류자는 데이터 마이닝에 이상적인 도구입니다.  
  
 성능 제한이 심각한 경우 의사 결정 트리 모델의 학습 도중 다음 방법을 사용하여 처리 시간을 개선할 수 있습니다. 그러나 이 경우 특성을 제거하여 처리 성능을 향상시키면 모델 결과가 변경되고 해당 모델이 전체 모집단을 대표하는 정도가 낮아질 수 있다는 것을 알고 있어야 합니다.  
  
-   COMPLEXITY_PENALTY 매개 변수의 값을 늘려 트리 증가를 제한합니다.  
  
-   연결 모델의 항목 수를 제한하여 작성되는 트리 수를 제한합니다.  
  
-   MINIMUM_SUPPORT 매개 변수의 값을 늘려 과잉 맞춤을 방지합니다.  
  
-   모든 특성의 불연속 값 수를 10개 이하로 제한합니다. 다른 모델에서 다른 방법으로 값을 그룹화해 볼 수도 있습니다.  
  
    > [!NOTE]  
    >  데이터 마이닝을 시작하기 전에  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 에서 제공되는 데이터 탐색 도구를 사용하여 데이터의 값 분포를 시각화하고 적절하게 값을 그룹화할 수 있습니다. 자세한 내용은 [데이터 프로파일링 태스크 및 뷰어](../../integration-services/control-flow/data-profiling-task-and-viewer.md)를 참조하세요. [Excel 2007용 데이터 마이닝 추가 기능](https://www.microsoft.com/download/details.aspx?id=8569)을 사용하여 Microsoft Excel에서 데이터를 탐색하고 그룹화하고 레이블을 재지정할 수도 있습니다.  
  
## <a name="customizing-the-decision-trees-algorithm"></a>의사 결정 트리 알고리즘 사용자 지정  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘은 결과 마이닝 모델의 성능 및 정확도에 영향을 주는 매개 변수를 지원합니다. 마이닝 모델 열이나 마이닝 구조 열에 모델링 플래그를 설정하여 데이터 처리 방식을 제어할 수도 있습니다.  
  
> [!NOTE]  
>  Microsoft 의사 결정 트리 알고리즘은 모든 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 있지만 Microsoft 의사 결정 트리 알고리즘의 동작을 사용자 지정하는 고급 매개 변수는 특정 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서만 사용할 수 있습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server 2012 버전에서 지 원하는 기능](https://go.microsoft.com/fwlink/?linkid=232473) 을 참조 하세요 https://go.microsoft.com/fwlink/?linkid=232473) .  
  
### <a name="setting-algorithm-parameters"></a>알고리즘 매개 변수 설정  
 다음 표에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘에서 사용할 수 있는 매개 변수에 대해 설명합니다.  
  
 *COMPLEXITY_PENALTY*  
 의사 결정 트리의 증가를 제어합니다. 낮은 값을 지정하면 분할 수가 증가되고 높은 값을 지정하면 분할 수가 감소됩니다. 기본값은 다음 목록에 설명된 것과 같이 특정 모델의 특성 수에 따라 달라집니다.  
  
-   특성 수가 1에서 9 사이인 경우 기본값은 0.5입니다.  
  
-   특성 수가 10에서 99 사이인 경우 기본값은 0.9입니다.  
  
-   특성 수가 100 이상인 경우 기본값은 0.99입니다.  
  
 *FORCE_REGRESSOR*  
 알고리즘에서 계산한 열의 중요도에 관계없이 알고리즘에서 지정된 열을 회귀 변수로 사용하도록 합니다. 이 매개 변수는 연속 특성을 예측하는 의사 결정 트리에만 사용됩니다.  
  
> [!NOTE]  
>  이 매개 변수를 설정하면 알고리즘에서는 해당 특성을 회귀 변수로 사용하려고 합니다. 그러나 해당 특성이 최종 모델에서 실제로 회귀 변수로 사용되는지 여부는 분석 결과에 따라 달라집니다. 모델 콘텐츠를 쿼리하면 회귀 변수로 사용된 열을 확인할 수 있습니다.  
  
 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 일부 버전에서만 사용 가능]  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 기능 선택을 호출하기 전에 알고리즘이 처리할 수 있는 입력 특성 수를 정의합니다.  
  
 기본값은 255입니다.  
  
 이 값을 0으로 설정하면 기능 선택이 해제됩니다.  
  
 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 일부 버전에서만 사용 가능]  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 기능 선택을 호출하기 전에 알고리즘이 처리할 수 있는 출력 특성 수를 정의합니다.  
  
 기본값은 255입니다.  
  
 이 값을 0으로 설정하면 기능 선택이 해제됩니다.  
  
 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 일부 버전에서만 사용 가능]  
  
 *MINIMUM_SUPPORT*  
 의사 결정 트리에서 분할을 생성하는 데 필요한 최소 리프 사례 수를 결정합니다.  
  
 기본값은 10입니다.  
  
 데이터 세트가 매우 큰 경우 과잉 맞춤을 방지하기 위해 이 값을 늘려야 할 수 있습니다.  
  
 *SCORE_METHOD*  
 분할 점수를 계산하는 데 사용되는 메서드를 결정합니다. 다음 옵션을 사용할 수 있습니다.  
  
|ID|속성|  
|--------|----------|  
|1|Entropy|  
|3|Bayesian with K2 Prior|  
|4|Bayesian Dirichlet Equivalent (BDE) with uniform prior<br /><br /> (기본값)|  
  
 기본값은 4 또는 BDE입니다.  
  
 이러한 점수 매기기 방법에 대한 자세한 내용은 [Feature Selection](../../sql-server/install/feature-selection.md)을 참조하십시오.  
  
 *SPLIT_METHOD*  
 노드를 분할하는 데 사용되는 메서드를 결정합니다. 다음 옵션을 사용할 수 있습니다.  
  
|ID|속성|  
|--------|----------|  
|1|**Binary:** 특성의 실제 값 수에 관계없이 트리가 두 개의 분리로 분할됨을 나타냅니다.|  
|2|**Complete:** 트리에서 특성 값 수만큼의 분할을 만들 수 있음을 나타냅니다.|  
|3|**Both:** 최상의 결과를 생성하기 위해 이진(Both) 분할을 사용할지 완전(Complete) 분할을 사용할지를 Analysis Services에서 결정할 수 있도록 지정합니다.|  
  
 기본값은 3입니다.  
  
### <a name="modeling-flags"></a>모델링 플래그  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘은 다음과 같은 모델링 플래그를 지원합니다. 마이닝 구조나 마이닝 모델을 만들 경우 분석 중 각 열의 값이 처리되는 방법을 지정하기 위해 모델링 플래그를 정의합니다. 자세한 내용은 [모델링 플래그&#40;데이터 마이닝&#41;](modeling-flags-data-mining.md)를 참조하세요.  
  
|모델링 플래그|설명|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|열이 `Missing` 및 `Existing` 상태를 갖는 것으로 간주됩니다. Null은 누락 값입니다.<br /><br /> 마이닝 모델 열에 적용됩니다.|  
|NOT NULL|열에 null이 포함될 수 없음을 나타냅니다. 따라서 Analysis Services가 모델 학습 중 Null을 발견할 경우 오류가 발생합니다.<br /><br /> 마이닝 구조 열에 적용됩니다.|  
  
### <a name="regressors-in-decision-tree-models"></a>의사 결정 트리 모델의 회귀 변수  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘을 사용하지 않는 경우라도 연속 숫자 입력 및 출력을 포함하는 의사 결정 트리 모델에는 연속 특성에 대한 회귀를 나타내는 노드가 포함될 수 있습니다.  
  
 연속 숫자 데이터 열이 회귀 변수를 나타내도록 지정할 필요는 없습니다. 열에 REGRESSOR 플래그를 설정하지 않았더라도 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘은 자동으로 열을 잠재적 회귀 변수로 사용하고 데이터 세트를 의미 있는 패턴이 있는 영역으로 분할합니다.  
  
 그러나 FORCE_REGRESSOR 매개 변수를 사용하면 알고리즘이 항상 특정 회귀 변수를 사용하도록 할 수 있습니다. 이 매개 변수는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘과 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘에서만 사용할 수 있습니다. 모델링 플래그를 설정 하면 알고리즘은 a * C1 + b \* C2 + ... 형식의 회귀 수식을 찾으려고 합니다. 트리의 노드에 패턴을 맞추려면입니다. 잉여에 대한 합계가 계산되며 편차가 너무 클 경우 트리에서 강제로 분할이 수행됩니다.  
  
 예를 들어 **Income** 을 특성으로 사용하여 고객의 구매 행동을 예측하며 열에 REGRESSOR 모델링 플래그를 설정하는 경우 알고리즘은 먼저 표준 회귀 수식을 사용하여 **Income** 값을 맞추려고 시도합니다. 편차가 너무 클 경우 회귀 수식이 중단되고 다른 특성에 따라 트리가 분할됩니다. 분할 후 의사 결정 트리 알고리즘은 먼저 각 분기에서 Income에 대한 회귀 변수를 맞추려고 시도합니다.  
  
## <a name="requirements"></a>요구 사항  
 의사 결정 트리 모델은 하나의 키 열, 여러 개의 입력 열 및 하나 이상의 예측 가능한 열을 포함해야 합니다.  
  
### <a name="input-and-predictable-columns"></a>입력 열과 예측 가능한 열  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘은 다음 표에 나열된 특정 입력 열과 예측 가능한 열을 지원합니다. 마이닝 모델에 사용되는 경우 콘텐츠 형식의 의미에 대한 자세한 내용은 [콘텐츠 형식&#40;데이터 마이닝&#41;](content-types-data-mining.md)을 참조하세요.  
  
|열|내용 유형|  
|------------|-------------------|  
|입력 특성|Continuous, Cyclical, Discrete, Discretized, Key, Ordered, Table|  
|예측 가능한 특성|Continuous, Cyclical, Discrete, Discretized, Ordered, Table|  
  
> [!NOTE]  
>  Cyclical  및 Ordered  내용 유형이 지원되기는 하지만 알고리즘은 해당 유형을 불연속 값으로 처리하고 특수한 처리를 수행하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft 의사 결정 트리 알고리즘](microsoft-decision-trees-algorithm.md)   
 [의사 결정 트리 모델 쿼리 예제](decision-trees-model-query-examples.md)   
 [의사 결정 트리 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
