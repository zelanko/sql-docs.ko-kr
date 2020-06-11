---
title: DMX 예측 쿼리의 구조 및 사용 | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 167bf7e17b172b9d3e6c58df1f52510f93a668aa
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669994"
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>DMX 예측 쿼리의 구조 및 사용법
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  에서 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터 마이닝 확장 (DMX)의 예측 쿼리를 사용 하 여 마이닝 모델의 결과를 기반으로 새 데이터 집합에서 알 수 없는 열 값을 예측할 수 있습니다.  
  
 사용하는 쿼리 유형은 모델로부터 얻으려는 정보에 따라 다릅니다. 웹 사이트를 방문하는 고객에게서 자전거 구매 가능성이 있는지 파악하는 경우처럼 간단한 예측을 실시간으로 만들려는 경우에는 단일 쿼리를 사용합니다. 데이터 원본에 포함되어 있는 사례 집합에서 예측 일괄 처리를 만들려면 일반 예측 쿼리를 사용합니다.  
  
## <a name="prediction-types"></a>예측 유형  
 DMX를 사용하여 다음과 같은 예측 유형을 만들 수 있습니다.  
  
 예측 조인  
 마이닝 모델에 있는 패턴을 기준으로 입력 데이터에 대한 예측을 만드는 데 사용합니다. 이 쿼리 문에는 마이닝 모델 열과 입력 열 간의 조인 조건을 제공 하는 **ON** 절이와 야 합니다.  
  
 자연 예측 조인  
 쿼리를 실행할 테이블의 열 이름과 정확히 일치하는 마이닝 모델의 열 이름을 기준으로 예측을 만드는 데 사용합니다. 마이닝 모델 열과 입력 열 간의 일치 하는 이름을 기반으로 조인 조건이 자동으로 생성 되기 때문에이 쿼리 문에는 **ON** 절이 필요 하지 않습니다.  
  
 빈 예측 조인  
 입력 데이터를 제공할 필요 없이 가장 가능성이 높은 예측을 찾는 데 사용합니다. 마이닝 모델의 내용만을 기준으로 예측을 반환합니다.  
  
 단일 쿼리  
 쿼리에 데이터를 제공하여 예측을 만드는 데 사용합니다. 이 문을 사용하면 한 가지 사례를 쿼리하여 신속한 결과를 얻을 수 있으므로 매우 유용합니다. 예를 들어 35세 기혼 여성의 자전거 구매 가능성을 예측하는 쿼리를 사용할 수 있습니다. 이 쿼리에는 외부 데이터 원본이 필요하지 않습니다.  
  
## <a name="query-structure"></a>쿼리 구조  
 DMX에서 예측 쿼리를 만들려면 다음 요소를 결합하여 사용합니다.  
  
-   **SELECT [평면화]**  
  
-   **맨 위로**  
  
-   **FROM*** \< 모델>* **예측 조인** 에서      
  
-   **ON**  
  
-   **위치**  
  
-   **ORDER BY**  
  
 예측 쿼리의 **SELECT** 요소는 결과 집합에 표시 되는 열과 식을 정의 하며 다음 데이터를 포함할 수 있습니다.  
  
-   마이닝 모델 **에서 열을** **예측** 합니다.  
  
-   예측을 만드는 데 사용하는 입력 데이터의 열  
  
-   데이터 열을 반환하는 함수  
  
 **FROM** * \< model>* **예측 조인** 요소는 예측을 만드는 데 사용 되는 원본 데이터를 정의 합니다. 단일 쿼리의 경우 이 요소는 열에 할당된 일련의 값입니다. 빈 예측 조인의 경우 이 요소는 빈 상태가 됩니다.  
  
 **ON** 요소는 마이닝 모델에 정의 된 열을 외부 데이터 집합의 열에 매핑합니다. 빈 예측 조인 쿼리나 자연 예측 조인을 만드는 경우에는 이 요소를 포함하지 않아도 됩니다.  
  
 **Where** 절을 사용 하 여 예측 쿼리의 결과를 필터링 할 수 있습니다. **TOP** 또는 **ORDER by** 절을 사용 하 여 가장 가능성이 높은 예측을 선택할 수 있습니다. 이러한 절을 사용 하는 방법에 대 한 자세한 내용은 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)를 참조 하세요.  
  
 예측 문의 구문에 대 한 자세한 내용은 [SELECT from &#60;model&#62; 예측 조인 &#40;dmx&#41;](../dmx/select-from-model-prediction-join-dmx.md) 및 [select FROM model &#60;dmx ](../dmx/select-from-model-dmx.md)&#62; &#40;을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [DMX&#41; 참조 &#40;데이터 마이닝 확장](../dmx/data-mining-extensions-dmx-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
