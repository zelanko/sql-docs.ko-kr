---
title: 모델링 플래그 (데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [data mining]
- data types [data mining]
- REGRESSOR flag
- MODEL_EXISTENCE_ONLY flag
- REGRESSOR column
- columns [data mining], modeling flags
- NOT NULL modeling flag
- modeling flags [data mining]
- null values [Analysis Services]
- MODEL_EXISTENCE_ONLY column
- coding [Data Mining]
ms.assetid: 8826d5ce-9ba8-4490-981b-39690ace40a4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0f1c802f6503b84ff4f6879c18d3bffebb46d7ad
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84521081"
---
# <a name="modeling-flags-data-mining"></a>모델링 플래그(데이터 마이닝)
  에서 모델링 플래그를 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 하 여 사례 테이블에 정의 된 데이터에 대 한 추가 정보를 데이터 마이닝 알고리즘에 제공할 수 있습니다. 데이터 마이닝 알고리즘은 이 정보를 토대로 더욱 정확한 데이터 마이닝 모델을 만들 수 있습니다.  
  
 마이닝 구조 수준에서 정의되는 모델링 플래그도 있고 마이닝 모델 열 수준에서 정의되는 모델링 플래그도 있습니다. 예를 들어 `NOT NULL` 모델링 플래그는 마이닝 구조 열에 사용됩니다. 모델을 만드는 데 사용하는 알고리즘에 따라 마이닝 모델 열에 추가 모델링 플래그를 정의할 수 있습니다.  
  
> [!NOTE]  
>  타사 플러그 인의 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 미리 정의한 모델링 플래그 외에 다른 모델링 플래그를 사용할 수 있습니다.  
  
## <a name="list-of-modeling-flags"></a>모델링 플래그 목록  
 다음 목록에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 지원하는 모델링 플래그에 대해 설명합니다. 특정 알고리즘에서 지원하는 모델링 플래그에 대한 자세한 내용은 모델을 만드는 데 사용된 알고리즘의 기술 참조 항목을 참조하십시오.  
  
 `NOT NULL`  
 특성 열 값이 Null 값을 포함할 수 없음을 나타냅니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 모델 학습 프로세스 중 이 특성 열에 Null 값이 있는 경우에는 오류가 발생합니다.  
  
 **MODEL_EXISTENCE_ONLY**  
 열이 `Missing` 및 `Existing` 상태로 처리됨을 나타냅니다. 값이 `NULL`인 경우 Missing으로 간주됩니다 MODEL_EXISTENCE_ONLY 플래그는 예측 가능한 특성에 적용되며 대부분의 알고리즘에서 지원됩니다.  
  
 실제로 MODEL_EXISTENCE_ONLY 플래그를 `True`로 설정하면 `Missing` 및 `Existing`과 같은 두 개의 문이 있는 경우 값을 다르게 표시합니다. 누락되지 않은 상태는 모두 단일 `Existing` 값으로 통합됩니다.  
  
 이 모델링 플래그는 일반적으로 `NULL` 상태가 암시적인 의미를 갖는 특성을 나타내는 데 사용됩니다. 따라서 `NOT NULL` 상태의 명시적 값은 열이 값을 갖는다는 사실만큼이나 중요하지 않습니다. 예를 들어 서명되지 않은 계약의 경우 [DateContractSigned] 열이 `NULL`이고 서명된 계약의 경우 `NOT NULL`일 수 있습니다. 따라서 모델의 목적이 계약에 서명할 것인지 여부를 예측하는 것이라면 MODEL_EXISTENCE_ONLY 플래그를 사용하여 `NOT NULL` 사례의 정확한 날짜 값은 무시하고 계약이 `Missing` 또는 `Existing`인 사례만 구별할 수 있습니다.  
  
> [!NOTE]  
>  Missing은 알고리즘에서 사용하는 특수한 상태로 열의 텍스트 값인 "Missing"과는 다릅니다. 자세한 내용은 [누락 값&#40;Analysis Services - 데이터 마이닝&#41;](missing-values-analysis-services-data-mining.md)에서 미리 정의한 모델링 플래그 외에 다른 모델링 플래그를 사용할 수 있습니다.  
  
 `REGRESSOR`  
 열이 처리 중에 회귀 변수로 사용할 후보임을 나타냅니다. 이 플래그는 마이닝 모델 열에서 정의되며 연속 숫자 데이터 형식이 있는 열에만 적용할 수 있습니다. 이 플래그를 사용 하는 방법에 대 한 자세한 내용은이 항목의 [회귀 변수 모델링 플래그 사용](#bkmk_UseRegressors)섹션을 참조 하세요.  
  
## <a name="viewing-and-changing-modeling-flags"></a>모델링 플래그 확인 및 변경  
 데이터 마이닝 디자이너에서 구조 또는 모델의 속성을 확인하여 마이닝 구조 열 또는 모델 열과 관련된 모델링 플래그를 볼 수 있습니다.  
  
 현재 마이닝 구조에 적용된 모델링 플래그를 확인하려면 다음과 같은 쿼리를 사용하여 데이터 마이닝 스키마 행 집합에 대해 구조 열의 모델링 플래그를 반환하는 쿼리를 만들면 됩니다.  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_STRUCTURE_COLUMNS  
WHERE STRUCTURE_NAME = '<structure name>'  
```  
  
 데이터 마이닝 디자이너를 사용하거나 연관된 열의 속성을 편집하여 모델에 사용된 모델링 플래그를 추가하거나 변경할 수 있습니다. 이러한 변경 사항을 적용하려면 구조 또는 모델을 다시 처리해야 합니다.  
  
 DMX를 사용하거나 AMO 또는 XMLA 스크립트를 사용하여 새 마이닝 구조 또는 마이닝 모델에서 모델링 플래그를 지정할 수 있습니다. 그러나 기존 마이닝 모델과 구조에 사용된 모델링 플래그는 DMX를 사용하여 변경할 수 없습니다. `ALTER MINING STRUCTURE....ADD MINING MODEL`구문을 사용하여 새 마이닝 모델을 만들어야 합니다.  
  
##  <a name="uses-of-the-regressor-modeling-flag"></a><a name="bkmk_UseRegressors"></a>회귀 변수 모델링 플래그 사용  
 열에 REGRESSOR 모델링 플래그를 설정하면 해당 열에 잠재적인 회귀 변수가 포함되어 있다는 사실이 알고리즘에 전달됩니다. 모델에 사용되는 실제 회귀 변수는 알고리즘에 따라 결정됩니다. 잠재적인 회귀 변수가 예측 가능한 특성을 모델링하지 않는 경우 이를 무시할 수 있습니다.  
  
 데이터 마이닝 마법사를 사용하여 모델을 작성하는 경우 연속 입력 열은 모두 가능한 회귀 변수로 플래그가 지정됩니다. 따라서 열에 REGRESSOR 플래그를 명시적으로 설정하지 않은 경우라도 모델에서 열을 회귀 변수로 사용할 수 있습니다.  
  
 처리된 모델에 실제로 사용된 회귀 변수를 확인하려면 다음 예에 표시된 것과 같이 마이닝 모델의 스키마 행 집합에 대해 쿼리를 실행하십시오.  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_COLUMNS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 **참고** 마이닝 모델을 수정한 다음 열의 내용 유형을 Continuous에서 Discrete로 변경할 경우 마이닝 열의 플래그를 수동으로 변경한 다음 모델을 다시 처리해야 합니다.  
  
### <a name="regressors-in-linear-regression-models"></a>선형 회귀 모델의 회귀 변수  
 선형 회귀 모델은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘을 기반으로 합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘을 사용하지 않는 경우라도 연속 특성에 대한 회귀를 나타내는 트리나 노드가 의사 결정 트리에 포함될 수 있습니다.  
  
 따라서 이러한 모델에서는 연속 열이 회귀 변수를 나타내도록 지정할 필요가 없습니다. 열에 REGRESSOR 플래그를 설정하지 않더라도 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘은 의미 있는 패턴을 포함하는 영역으로 데이터 세트를 분할합니다. 단, 모델링 플래그를 설정할 때 알고리즘이 트리의 노드에 패턴을 맞추기 위해 다음 형식의 회귀 수식을 찾으려고 한다는 것이 다릅니다.  
  
 a*C1 + b\*C2 + ...  
  
 그런 다음 잉여에 대한 합계가 계산되며 편차가 너무 클 경우 트리에서 강제로 분할이 수행됩니다.  
  
 예를 들어 **Income** 을 특성으로 사용하여 고객의 구매 행동을 예측하며 열에 REGRESSOR 모델링 플래그를 설정하는 경우 알고리즘은 먼저 표준 회귀 수식을 사용하여 **Income** 값을 맞추려고 시도합니다. 편차가 너무 클 경우 회귀 수식이 중단되고 다른 특성에 대해 트리가 분할됩니다. 분할 후 의사 결정 트리 알고리즘은 먼저 각 분기에서 Income에 대한 회귀 변수를 맞추려고 시도합니다.  
  
 FORCE_REGRESSOR 매개 변수를 사용하여 알고리즘이 항상 특정 회귀 변수를 사용하도록 할 수 있습니다. 이 매개 변수는 의사 결정 트리 알고리즘과 선형 회귀 알고리즘에서 사용할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 모델링 플래그 사용에 대해 자세히 알아보려면 다음 링크를 사용하십시오.  
  
|Task|항목|  
|----------|-----------|  
|데이터 마이닝 디자이너를 사용하여 모델링 플래그 편집|[모델링 플래그 확인 또는 변경&#40;데이터 마이닝&#41;](modeling-flags-data-mining.md)|  
|가능성이 높은 회귀 변수를 권장하기 위해 알고리즘에 대한 힌트 지정|[모델에서 회귀 변수로 사용할 열 지정](specify-a-column-to-use-as-regressor-in-a-model.md)|  
|특정 알고리즘에서 지원하는 모델링 플래그 확인(각 알고리즘 참조 항목의 모델링 플래그 섹션 참조)|[데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining-algorithms-analysis-services-data-mining.md)|  
|마이닝 구조 열과 각 열에 설정할 수 있는 속성에 대한 자세한 정보|[마이닝 구조 열](mining-structure-columns.md)|  
|마이닝 모델 열과 모델 수준에서 적용할 수 있는 모델링 플래그에 대한 자세한 정보|[마이닝 모델 열](mining-model-columns.md)|  
|DMX 문에서 모델링 플래그 작업에 사용되는 구문 확인|[모델링 플래그&#40;DMX&#41;](/sql/dmx/modeling-flags-dmx)|  
|누락된 값 및 이러한 값의 작업 방법 이해|[누락 값&#40;Analysis Services - 데이터 마이닝&#41;](missing-values-analysis-services-data-mining.md)|  
|모델 및 구조 관리와 사용법 속성 설정에 대한 자세한 정보|[데이터 마이닝 개체 이동](moving-data-mining-objects.md)|  
  
  
