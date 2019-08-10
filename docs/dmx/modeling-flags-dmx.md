---
title: 모델링 플래그 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a610f3aed7f520163dc4e2b30651d8b0397ef644
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893936"
---
# <a name="modeling-flags-dmx"></a>모델링 플래그(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 모델링 플래그를 사용하여 사례 테이블에 정의되어 있는 데이터에 대한 추가 정보를 데이터 마이닝 알고리즘에 제공할 수 있습니다. 데이터 마이닝 알고리즘은 이 정보를 토대로 더욱 정확한 데이터 마이닝 모델을 만들 수 있습니다. 마이닝 구조 열과 마이닝 모델 열에서 모델링 플래그를 정의할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 다음과 같은 모델링 플래그를 지원합니다.  
  
 **NOT NULL**  
 특성 열 값에는 Null 값을 포함할 수 없습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 의 모델 학습 프로세스 중 이 특성 열에 Null 값이 있는 경우에는 오류가 발생합니다. 이 플래그는 마이닝 구조 열에 정의됩니다.  
  
 **회귀 변수**  
 회귀 알고리즘의 회귀 수식에 지정된 열을 사용할 수 있음을 나타냅니다. 이 플래그는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 선형 회귀 알고리즘 및 [!INCLUDE[msCoName](../includes/msconame-md.md)] 의사 결정 트리 알고리즘에서 사용할 수 있으며 마이닝 모델 열에 정의됩니다.  
  
 **MODEL_EXISTENCE_ONLY**  
 특성 열의 값은 특성 자체보다는 중요도가 낮습니다. 이 플래그는 마이닝 모델 열에 정의됩니다.  
  
 타사 알고리즘에서 추가 모델링 플래그를 지원할 수도 있습니다. 알고리즘에서 지 원하는 모델링 플래그를 확인 하려면 **SUPPORTED_MODELING_FLAGS** 스키마 행 집합을 사용 합니다. 서버의 마이닝 서비스를 쿼리하여 특정 알고리즘에 지원되는 모델링 플래그를 확인할 수도 있습니다. 예를 들어 다음 쿼리는 현재 서버에서 Microsoft 선형 회귀 알고리즘에 대해 지원되는 모델링 플래그를 반환합니다.  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 예상 결과:  
  
 NOT NULL,REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>마이닝 모델에 모델링 플래그 지정  
 에서 마이닝 구조 열에 플래그 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 를 지정 하는 데 지원 되는 구문의 예는 [마이닝 구조 &#40;DMX&#41;만들기](../dmx/create-mining-structure-dmx.md)를 참조 하세요.  
  
 마이닝 모델 열에서 모델링 플래그를 지정 하는 구문에 대 한 예는 [ALTER 마이닝 STRUCTURE &#40;&#41;DMX](../dmx/alter-mining-structure-dmx.md)를 참조 하세요.  
  
 마이닝 모델 열을 사용 하는 방법에 대 한 자세한 내용은 [마이닝 모델 열](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)을 참조 하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Data Mining Extensions & #40; DMX & #41; 참조](../dmx/data-mining-extensions-dmx-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 표기 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [DMX 예측 쿼리의 구조 및 사용법](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
