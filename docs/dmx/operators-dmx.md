---
title: 연산자 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2f03c3152e3144b137c079cbdfddeff5b9cd5156
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008169"
---
# <a name="operators-dmx"></a>연산자(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  DMX (데이터 마이닝 확장) 연산자를 사용 하 여의 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]쿼리에서 산술, 비교, 연결 및 논리적 연산을 수행할 수 있습니다.  
  
 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 연산자를 사용하여 다음 동작을 수행할 수 있습니다.  
  
-   특정 조건을 만족하는 값 또는 개체를 검색합니다.  
  
-   값 또는 식 사이에서 결정할 사항을 구현합니다.  
  
 DMX에서는 아래 섹션에 설명된 것처럼 다양한 범주의 연산자를 사용합니다. 개별 연산자에 대 한 자세한 내용은 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)를 참조 하세요.  
  
|연산자 범주|작업의 유형|  
|-----------------------|-----------------------|  
|[산술 연산자 &#40;DMX&#41;](../dmx/operators-arithmetic.md)|더하기, 빼기, 곱하기 또는 나누기를 수행합니다.|  
|[DMX&#41;&#40;비교 연산자](../dmx/operators-comparison.md)|값을 다른 값 또는 식과 비교합니다.|  
|[논리 연산자 &#40;DMX&#41;](../dmx/operators-logical.md)|AND, OR 또는 NOT 등의 조건에서 진리를 검사합니다.|  
|[DMX &#40;단항 연산자&#41;](../dmx/operators-unary.md)|단일 피연산자로 연산을 수행합니다.|  
  
 간단한 DMX 식을 연산자로 결합하여 복잡한 식으로 만들 수 있습니다. 복잡한 식에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 연산자 우선 순위 정의에 따라 연산자가 처리됩니다. 우선 순위가 높은 연산자가 우선 순위가 낮은 연산자보다 먼저 수행됩니다. 식에 대 한 자세한 내용은 [expressions &#40;DMX&#41;](../dmx/expressions-dmx.md)를 참조 하세요.  
  
 간단한 식을 결합하여 복잡한 식을 만들 때 결과 식의 데이터 형식은 연산자 규칙과 데이터 형식 우선 순위 규칙에 따라 결정됩니다. 결과가 문자 또는 유니코드 값인 경우 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 결과의 데이터 정렬이 연산자 규칙과 데이터 정렬 우선 순위 규칙에 따라 결정됩니다. 간단한 식의 전체 자릿수, 소수 자릿수 및 길이를 기준으로 결과의 전체 자릿수, 소수 자릿수 및 길이를 결정하는 규칙도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [DMX&#41; 참조 &#40;데이터 마이닝 확장](../dmx/data-mining-extensions-dmx-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)   
 [DMX 예측 쿼리의 구조 및 사용법](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
