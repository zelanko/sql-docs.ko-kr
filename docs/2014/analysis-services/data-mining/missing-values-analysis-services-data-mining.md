---
title: 누락 값 (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [data mining]
- MISSING_VALUE_SUBSTITUTION
- MissingValueSubstitution property
- MISSING_VALUE_SUBSTITUTION parameter
- null values [Analysis Services]
- coding [Data Mining]
ms.assetid: 2b34abdc-7ed4-4ec1-8780-052a704d6dbe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85968aef6452acb6aac75c5c6d4a093964e8d923
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66083363"
---
# <a name="missing-values-analysis-services---data-mining"></a>누락 값(Analysis Services - 데이터 마이닝)
  
  *누락 값* 을 올바르게 처리하는 것은 효과적인 모델링을 위해 매우 중요합니다. 이 섹션에서는 누락 값의 정의를 알아보고, 데이터 마이닝 구조와 마이닝 모델을 빌드할 때 누락 값을 처리하기 위한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 기능을 설명합니다.  
  
## <a name="definition-of-missing-values-in-data-mining"></a>데이터 마이닝에서 누락 값의 정의  
 누락 값은 다양한 경우를 의미할 수 있습니다. 필드를 적용할 수 없었거나, 이벤트가 발생하지 않았거나, 데이터를 사용할 수 없었던 경우일 수 있습니다. 데이터를 입력한 사람이 올바른 값을 몰랐거나, 필드에 데이터가 채워졌는지 확인하지 않았을 수도 있습니다.  
  
 그러나 데이터 마이닝에서는 누락 값을 통해 중요한 정보를 알 수 있는 경우가 많습니다. 누락 값은 상황에 따라 그 의미가 크게 달라집니다. 예를 들어 송장 목록에서 날짜 값이 누락된 경우는 직원의 고용일을 나타내는 열에서 날짜가 누락된 경우와는 완전히 의미가 다릅니다. 일반적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 누락 값을 정보로 취급하고 누락 값이 계산에 통합되는 확률을 조정합니다. 이렇게 하면 모델의 균형이 잘 이루어지고 모델이 기존 사례에 너무 많은 비중을 두지 않습니다.  
  
 따라서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 누락 값의 관리 및 계산을 위하여 분명히 다른 두 가지 메커니즘을 제공합니다. 첫 번째 방법은 마이닝 구조 수준에서 null 처리를 제어합니다. 두 번째 방법은 알고리즘에 따라 구현 방식이 달라지지만, 일반적으로 null 값을 허용하는 모델에서 누락 값이 처리되고 발생하는 횟수를 계산하는 방법을 정의합니다.  
  
## <a name="specifying-handling-of-nulls"></a>null 처리 방법 지정  
 데이터 원본에서 누락 값은 null, 스프레드시트에서의 빈 셀, N/A 또는 해당 없음과 같은 코드, 9999와 같은 가상의 값 등 여러 가지 방법으로 표현될 수 있습니다. 그러나 데이터 마이닝을 위해서는 null만 누락 값으로 간주됩니다. 데이터에 null이 아닌 다른 자리 표시자 값이 포함되면 모델링 결과에 영향을 줄 수 있으므로 이를 null로 교체하거나 가능하면 올바른 값으로 대체하여 수정해야 합니다. 적절한 값을 유추하고 입력하는 데는 SQL Server Integration Services의 조회 변환 또는 데이터 프로파일러 태스크, Excel용 데이터 마이닝 추가 기능에서 제공되는 예제로 채우기 도구 등 다양한 도구를 사용할 수 있습니다.  
  
 모델링하는 태스크에서 어떠한 경우에도 누락 값이 있어서는 안 되는 열이 있을 경우, 마이닝 구조를 정의할 때 해당 열에 `NOT_NULL` 모델링 플래그를 적용해야 합니다. 이 플래그는 사례에 적절한 값이 없는 경우 처리가 실패함을 나타냅니다. 모델을 처리할 때 이 오류가 발생하는 경우 오류를 기록한 다음 모델에 제공된 데이터를 수정하는 단계를 수행할 수 있습니다.  
  
## <a name="calculation-of-the-missing-state"></a>누락 상태 계산  
 데이터 마이닝 알고리즘에서는 누락 값이 정보입니다. 사례 테이블에서 `Missing`은 다른 상태와 마찬가지로 유효한 상태입니다. 또한 데이터 마이닝 모델에서는 다른 값을 사용하여 값의 누락 여부를 예측할 수 있습니다. 즉, 값이 누락된 사실이 오류로 간주되지 않습니다.  
  
 마이닝 모델을 만들 때 모든 불연속 열에 대해 `Missing` 상태가 자동으로 모델에 추가됩니다. 예를 들어 [Gender] 입력 열에 Male과 Female의 두 가지 값을 입력할 수 있는 경우, `Missing` 값을 나타내는 세 번째 값이 자동으로 추가되며 이 열에 대한 모든 값의 분포를 보여 주는 히스토그램에 `Missing` 값이 있는 사례의 수가 항상 포함됩니다. Gender 열에 누락된 값이 없는 경우 히스토그램은 0개의 사례에서 누락 상태가 발견되었음을 보여 줍니다.  
  
 데이터에 가능한 값의 예가 모두 포함되지 않을 수도 있다고 생각하고, 데이터에 예가 없다는 이유만으로 모델에서 가능성을 배제하려고 하지 않는 경우에는 기본적으로 `Missing` 상태를 포함하는 것이 좋습니다. 예를 들어 어떤 매장의 판매 데이터에서 특정 제품을 구입한 고객 전체가 여성임을 나타낸다고 해서 여성만 해당 제품을 구입할 수 있다고 예측하는 모델을 만들려고 하지는 않을 것입니다. 대신, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가능한 다른 상태를 수용 하는 방법으로 이라는 `Missing`추가 알 수 없는 값에 대 한 자리 표시자를 추가 합니다.  
  
 예를 들어 다음 표에서는 Bike Buyer 자습서에서 사용하기 위해 만든 의사 결정 트리 모델에 있는 (All) 노드에 대한 값의 분포를 보여 줍니다. 예제 시나리오에서 [Bike Buyer] 열은 예측 가능한 특성이며, 여기서 1은 "예"를 나타내고 0은 "아니요"를 나타냅니다.  
  
|값|사례|  
|-----------|-----------|  
|0|9296|  
|1|9098|  
|Missing|0|  
  
 이 분포는 고객의 절반 정도는 자전거를 구입했고 나머지 절반은 구입하지 않았음을 보여 줍니다. 이 특정 데이터 집합은 아주 간결하여 모든 사례의 [Bike Buyer] 열에 값이 있고 `Missing` 값의 수가 0입니다. 그러나 [자전거 구매자] 필드에 null이 있는 경우에는 해당 행이 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] `Missing` 값을 갖는 사례로 계산 됩니다.  
  
 입력이 연속 열인 경우 모델은 특성에 대한 `Existing` 및 `Missing`의 두 가지 가능한 상태를 표 형식으로 만듭니다. 즉, 열에 숫자 데이터 형식 값이 포함되거나 값이 포함되지 않습니다. 값이 있는 사례의 경우 모델은 평균, 표준 편차 및 기타 의미 있는 통계를 계산합니다. 값이 없는 사례의 경우에는 모델에서 `Missing` 값의 수를 제공하고 그에 따라 예측을 조정합니다. 예측을 조정하는 방법은 알고리즘에 따라 다르며 다음 섹션에 설명되어 있습니다.  
  
> [!NOTE]  
>  중첩 테이블에 있는 특성의 경우에는 누락 값이 정보를 제공하지 못합니다. 예를 들어 고객이 제품을 구입하지 않은 경우 중첩 **Products** 테이블에는 해당 제품에 해당하는 행이 없으며 마이닝 모델에서 누락 제품에 대한 특성을 만들지 않습니다. 그러나 특정 제품을 구입하지 않은 고객에게 관심이 있는 경우 모델 필터에 NOT EXISTS 문을 사용하여 중첩 테이블에 존재하지 않는 제품을 기준으로 필터링된 모델을 만들 수 있습니다. 자세한 내용은 [마이닝 모델에 필터 적용](apply-a-filter-to-a-mining-model.md)을 참조하세요.  
  
## <a name="adjusting-probability-for-missing-states"></a>누락 상태에 대한 확률 조정  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 값의 개수를 계산할 뿐 아니라 데이터 집합 값의 확률도 계산합니다. 
  `Missing` 값의 경우에도 마찬가지입니다. 예를 들어 다음 표에서는 위의 예에 있는 사례에 대한 확률을 보여 줍니다.  
  
|값|사례|확률|  
|-----------|-----------|-----------------|  
|0|9296|50.55%|  
|1|9098|49.42%|  
|Missing|0|0.03%|  
  
 사례 수가 0인 경우 `Missing` 값의 확률이 0.03%로 계산된다는 사실이 이상해 보일 수 있습니다. 사실 이 동작은 의도적으로 설계된 동작이며 모델에서 알 수 없는 값을 정상적으로 처리할 수 있도록 하는 조정을 나타냅니다.  
  
 일반적으로 확률은 긍적적인 사례 수를 모든 가능한 사례 수로 나누어 계산됩니다. 이 예에서 알고리즘은 특정 조건([Bike Buyer] = 1 또는 [Bike Buyer] = 0)을 만족하는 사례 수의 합계를 계산한 다음 해당 숫자를 총 행 수로 나눕니다. 그러나 `Missing` 사례를 고려하기 위해 모든 가능한 사례 수에 1이 추가됩니다. 따라서 알 수 없는 사례에 대한 확률이 더 이상 0은 아니지만 아주 작은 숫자입니다. 이는 거의 희박하지만 발생할 가능성이 있는 상태임을 나타냅니다.  
  
 작은 `Missing` 값을 더한다고 해서 예측 결과가 변경되지는 않지만 기록 데이터에 가능한 결과가 모두 포함되지는 않는 시나리오에서 모델링이 더 향상될 수 있습니다.  
  
> [!NOTE]  
>  데이터 마이닝 공급자마다 누락 값을 처리하는 방법이 서로 다릅니다. 예를 들어 일부 공급자의 경우 중첩 열의 누락 데이터는 스파스 표현이라고 간주하지만 비중첩 열의 해당 누락 데이터는 임의로 누락되었다고 간주합니다.  
  
 데이터에 모든 결과가 지정된 것이 확실한 경우 확률을 조정할 수 없도록 하려면 마이닝 구조의 열에 NOT_NULL 모델링 플래그를 설정해야 합니다.  
  
> [!NOTE]  
>  타사 플러그 인에서 가져올 수 있는 사용자 지정 알고리즘을 비롯한 각 알고리즘이 누락 값을 다르게 처리할 수 있습니다.  
  
### <a name="special-handling-of-missing-values-in-decision-tree-models"></a>의사 결정 트리 모델에서 누락 값의 특수 처리  
 Microsoft 의사 결정 트리 알고리즘에서 누락 값에 대한 확률을 계산하는 방식은 다른 알고리즘과 다릅니다. 이 의사 결정 트리 알고리즘은 총 사례 수에 단순히 1을 더하는 대신 약간 다른 수식을 사용하여 `Missing` 상태를 조정합니다.  
  
 의사 결정 트리 모델에서 `Missing` 상태의 확률은 다음과 같이 계산됩니다.  
  
 StateProbability = (NodePriorProbability)* (StateSupport + 1) / (NodeSupport + TotalStates)  
  
 또한 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]에서 의사 결정 트리 알고리즘은 모델에 필터가 있을 때 알고리즘으로 보정할 수 있는 추가 조정 기능을 제공하므로 학습 중에 많은 상태가 제외될 수도 있습니다.  
  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 학습 중에는 있는 상태가 특정 노드에서 지지도가 0인 경우 표준 조정이 이루어집니다. 그러나 학습 중에 상태가 발생하지 않으면 알고리즘은 확률을 정확히 0으로 설정합니다. 이러한 조정은 `Missing` 상태뿐만 아니라 학습 데이터에는 있지만 모델 필터링 결과 지지도가 0인 다른 상태에도 적용됩니다.  
  
 이 추가 조정을 통해 다음과 같은 수식이 발생합니다.  
  
 학습 집합에서 지지도가 0인 경우 StateProbability = 0.0  
  
 ELSE StateProbability = (NodePriorProbability)* (StateSupport + 1) / (NodeSupport + TotalStatesWithNonZeroSupport)  
  
 이 조정을 통해 트리의 안정성이 유지됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
 다음 항목에서는 누락 값을 처리하는 방법에 대해 자세히 설명합니다.  
  
|작업|링크|  
|-----------|-----------|  
|개별 모델 열에 누락 값의 처리를 제어하는 플래그를 추가|[데이터 마이닝&#41;&#40;모델링 플래그 보기 또는 변경](modeling-flags-data-mining.md)|  
|마이닝 모델에 누락 값의 처리를 제어하는 속성을 설정|[마이닝 모델의 속성 변경](change-the-properties-of-a-mining-model.md)|  
|DMX에서 모델링 플래그를 지정하는 방법|[DMX&#41;&#40;모델링 플래그](/sql/dmx/modeling-flags-dmx)|  
|마이닝 구조에서 누락 값을 처리하는 방법 변경|[마이닝 구조 속성 변경](change-the-properties-of-a-mining-structure.md)|  
  
## <a name="see-also"></a>참고 항목  
 [마이닝 모델 콘텐츠 &#40;Analysis Services 데이터 마이닝&#41;](mining-model-content-analysis-services-data-mining.md)   
 [데이터 마이닝&#41;&#40;모델링 플래그](modeling-flags-data-mining.md)  
  
  
