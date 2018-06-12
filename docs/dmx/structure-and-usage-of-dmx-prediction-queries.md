---
title: 구조와 DMX 예측 쿼리의 사용법 | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 37ff157cbddb0894880f12097c977b923d92f177
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841866"
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>DMX 예측 쿼리의 구조 및 사용법
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 마이닝 모델의 결과 기반으로 새 데이터 집합에서 알 수 없는 열 값을 예측 하에서 데이터 마이닝 DMX (Extensions) 예측 쿼리를 사용할 수 있습니다.  
  
 사용하는 쿼리 유형은 모델로부터 얻으려는 정보에 따라 다릅니다. 웹 사이트를 방문하는 고객에게서 자전거 구매 가능성이 있는지 파악하는 경우처럼 간단한 예측을 실시간으로 만들려는 경우에는 단일 쿼리를 사용합니다. 데이터 원본에 포함되어 있는 사례 집합에서 예측 일괄 처리를 만들려면 일반 예측 쿼리를 사용합니다.  
  
## <a name="prediction-types"></a>예측 유형  
 DMX를 사용하여 다음과 같은 예측 유형을 만들 수 있습니다.  
  
 예측 조인  
 마이닝 모델에 있는 패턴을 기준으로 입력 데이터에 대한 예측을 만드는 데 사용합니다. 이 쿼리 문 뒤에 야는 **ON** 마이닝 모델 열과 입력된 열 간의 조인 조건을 제공 하는 절.  
  
 자연 예측 조인  
 쿼리를 실행할 테이블의 열 이름과 정확히 일치하는 마이닝 모델의 열 이름을 기준으로 예측을 만드는 데 사용합니다. 이 쿼리 문에 필요 하지 않습니다는 **ON** 마이닝 모델 열과 입력된 열 간의 일치 하는 이름에 따라 조인 조건이 자동으로 생성 되므로 절.  
  
 빈 예측 조인  
 입력 데이터를 제공할 필요 없이 가장 가능성이 높은 예측을 찾는 데 사용합니다. 마이닝 모델의 내용만을 기준으로 예측을 반환합니다.  
  
 단일 쿼리  
 쿼리에 데이터를 제공하여 예측을 만드는 데 사용합니다. 이 문을 사용하면 한 가지 사례를 쿼리하여 신속한 결과를 얻을 수 있으므로 매우 유용합니다. 예를 들어 35세 기혼 여성의 자전거 구매 가능성을 예측하는 쿼리를 사용할 수 있습니다. 이 쿼리에는 외부 데이터 원본이 필요하지 않습니다.  
  
## <a name="query-structure"></a>쿼리 구조  
 DMX에서 예측 쿼리를 만들려면 다음 요소를 결합하여 사용합니다.  
  
-   **[일반] 선택**  
  
-   **TOP**  
  
-   **FROM***\<모델 >***PREDICTION JOIN**  
  
-   **ON**  
  
-   **WHERE**  
  
-   **ORDER BY**  
  
 **선택** 요소는 예측 쿼리의 열을 정의 하 고 결과에 표시 되는 식 집합과 다음 데이터를 포함할 수 있습니다.  
  
-   **예측** 또는 **PredictOnly** 마이닝 모델의 열입니다.  
  
-   예측을 만드는 데 사용하는 입력 데이터의 열  
  
-   데이터 열을 반환하는 함수  
  
 **FROM**  *\<모델 >* **PREDICTION JOIN** 요소는 예측을 만드는 데 사용할 원본 데이터를 정의 합니다. 단일 쿼리의 경우 이 요소는 열에 할당된 일련의 값입니다. 빈 예측 조인의 경우 이 요소는 빈 상태가 됩니다.  
  
 **ON** 요소 외부 데이터 집합의 열에 마이닝 모델에 정의 된 열을 매핑합니다. 빈 예측 조인 쿼리나 자연 예측 조인을 만드는 경우에는 이 요소를 포함하지 않아도 됩니다.  
  
 사용할 수는 **여기서** 예측 쿼리의 결과 필터링 하려면 절. 사용할 수 있습니다는 **TOP** 또는 **ORDER BY** 절 가능성이 가장 높은 예측을 선택할 수 있습니다. 이러한 절을 사용 하는 방법에 대 한 자세한 내용은 참조 [선택 &#40;DMX&#41;](../dmx/select-dmx.md)합니다.  
  
 예측 문의 구문에 대 한 자세한 내용은 참조 [SELECT FROM &#60;모델&#62; PREDICTION JOIN &#40;DMX&#41; ](../dmx/select-from-model-prediction-join-dmx.md) 및 [SELECT FROM &#60;모델&#62; &#40;DMX &#41;](../dmx/select-from-model-dmx.md).  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 참조](../dmx/data-mining-extensions-dmx-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 표기 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
