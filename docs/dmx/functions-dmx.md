---
title: 함수 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 891bad9f62174ec00451e533fe94063a21dc62af
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971690"
---
# <a name="functions-dmx"></a>함수(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  DMX (데이터 마이닝 확장)를 사용 하 여에서 개체를 쿼리 하는 경우 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 함수를 사용 하 여 데이터 마이닝 모델 또는 입력 데이터 집합의 열 값 뿐만 아니라 추가 정보를 반환할 수 있습니다. 예를 들어 DMX 쿼리를 사용하여 열의 예측 값뿐만 아니라 예측의 정확성에 대한 확률도 반환할 수 있습니다. 또한 DMX 함수를 비롯하여 Microsoft VBA(Visual Basic for Applications), Microsoft Excel 및 저장 프로시저의 함수도 사용할 수 있습니다.  
  
## <a name="dmx-functions"></a>DMX 함수  
 DMX 함수를 사용하여 다음과 같은 태스크를 수행할 수 있습니다.  
  
-   예측을 반환합니다.  
  
-   확률 및 지원과 같은 예측에 대한 통계를 반환합니다.  
  
-   쿼리 결과를 필터링합니다.  
  
-   테이블 식을 다시 정렬합니다.  
  
 대부분의 DMX 함수는 예측에 대한 지원과 같은 스칼라 값을 반환하지만 일부 함수는 테이블 형식 결과를 반환합니다. 예를 들어 PredictHistogram 함수는 지정 된 예측 가능한 열의 각 상태에 대 한 지원 및 확률을 포함 하는 테이블을 반환 합니다. 그 결과는 새 테이블 형식의 열로 표시됩니다.  
  
 **자세한 내용은** [일반 예측 함수 &#40;dmx&#41;](../dmx/general-prediction-functions-dmx.md), [데이터 마이닝 확장 &#40;Dmx&#41; 함수 참조를 참조](../dmx/data-mining-extensions-dmx-function-reference.md) 하세요.  
  
## <a name="visual-basic-for-applications-vba-and-excel-functions"></a>VBA(Visual Basic for Applications) 및 Excel 함수  
 DMX 문에서는 DMX 함수 외에도 다양한 VBA 및 Excel 함수를 호출할 수 있습니다. 예를 들어 lCase 함수를 사용 하 여 TM_Decision_Tree 모델 콘텐츠의 Attribute_Name 열이 표시 되는 방식을 수정할 수 있습니다. 예를 들어 다음과 같은 코드 샘플을 사용할 수 있습니다.  
  
```  
SELECT lCase([Attribute_Name])   
FROM [TM_Decision_Tree].CONTENT  
```  
  
 VBA와 Excel 모두에 동일한 함수가 있는 경우 DMX 문의 함수 이름에 **vba** 또는 **excel**을 접두사로 붙여야 합니다. 예를 들어 `VBA!Log` 또는 `Excel!Log`와 같이 사용합니다. 사용할 VBA 또는 Excel 함수가 DMX 또는 MDX(Multidimensional Expressions)에도 있는 경우 또는 함수에 달러 기호($)가 포함된 경우에는 함수를 대괄호([])로 묶어야 합니다. 예를 들어 `[VBA!Format]`과 같이 함수를 호출할 수 있습니다.  
  
## <a name="stored-procedures"></a>저장 프로시저  
 공용 언어 런타임 프로그래밍 언어를 사용하여 DMX 기능을 확장하는 저장 프로시저를 만들 수 있습니다. 예를 들어 회귀 트리 마이닝 모델은 회귀 수식을 설명 하는 A, B 등의 계수를 반환 하지만 모델은 A + Bx = y와 같은 수식 자체를 반환 하지 않습니다. 그러나 데이터 마이닝 모델 개체를 사용하여 내용 스키마를 탐색하고 회귀 수식을 출력으로 반환하는 저장 프로시저를 만들 수 있습니다. 즉 DMX 문에서는 회귀 수식 목록을 쿼리 결과의 일부로 반환할 수 있습니다.  
  
 **자세한 내용:** [다차원 모델 어셈블리 관리](https://docs.microsoft.com/analysis-services/multidimensional-models/multidimensional-model-assemblies-management)  
  
## <a name="see-also"></a>참고 항목  
 [DMX&#41; 참조 &#40;데이터 마이닝 확장](../dmx/data-mining-extensions-dmx-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)   
 [DMX 예측 쿼리의 구조 및 사용법](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
