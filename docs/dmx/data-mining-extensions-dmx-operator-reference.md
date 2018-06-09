---
title: Data Mining Extensions (DMX) 연산자 참조 | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7a85644328591f037ee342866ca7dfb5e887ed17
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842766"
---
# <a name="data-mining-extensions-dmx-operator-reference"></a>DMX(Data Mining Extensions) 연산자 참조
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  확장 DMX (Data Mining) 언어 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 산술, 대입, 비교, 논리 및 단항 연산자를 지원 합니다. 다음 표에서는 DMX에서 지원하는 연산자를 설명합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|[+ &#40;추가&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|두 개의 수를 더하는 산술 연산자|  
|[- &#40;빼기&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|한 수에서 다른 수를 빼는 산술 연산자|  
|[&#42;&#40;곱하기&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|두 개의 수를 곱하는 산술 연산자|  
|[&#40;나누기&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|한 수를 다른 수로 나누는 산술 연산자|  
|[&#60;&#40;미만&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|비교 연산자. Null이 아닌 값으로 계산되는 인수의 경우 왼쪽의 인수 값이 오른쪽의 인수 값보다 작으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[&#62;&#40;보다 큰&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|비교 연산자. Null이 아닌 값으로 계산되는 인수의 경우 왼쪽의 인수 값이 오른쪽의 인수 값보다 크면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[= &#40;같음&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|비교 연산자. Null이 아닌 값으로 계산되는 인수의 경우 왼쪽의 인수 값과 오른쪽의 인수 값이 같으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[&#60;&#62;&#40;같지 않은&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|비교 연산자. Null이 아닌 값으로 계산되는 인수의 경우 왼쪽의 인수 값과 오른쪽의 인수 값이 다르면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[&#60;= &#40;보다 작거나&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|비교 연산자. Null이 아닌 값으로 계산되는 인수의 경우 왼쪽의 인수 값이 오른쪽의 인수 값보다 작거나 같으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[&#62;= &#40;보다 크거나 같음&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|비교 연산자. Null이 아닌 값으로 계산되는 인수의 경우 왼쪽의 인수 값이 오른쪽의 인수 값보다 크거나 같으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[및 &AMP;#40;DMX&AMP;#41;](../dmx/and-dmx.md)|두 숫자 식에서 결합을 수행하는 논리 연산자|  
|[하지 &AMP;#40;DMX&AMP;#41;](../dmx/not-dmx.md)|숫자 식에서 부정을 수행하는 논리 연산자|  
|[또는 &AMP;#40;DMX&AMP;#41;](../dmx/or-dmx.md)|두 숫자 식에서 분리를 수행하는 논리 연산자|  
|[+ &#40;양의&#41; &#40;DMX&#41;](../dmx/positive-dmx.md)|숫자 식의 양수 값을 반환하는 단항 연산자|  
|[- &#40;음수&#41; &#40;DMX&#41;](../dmx/negative-dmx.md)|숫자 식의 음수 값을 반환하는 단항 연산자|  
|[이중 슬래시 &#40;주석&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 실행되지 않는 텍스트 문자열을 나타냅니다. 주석을 DMX 문 안에 중첩하거나 코드 줄 끝에 포함하거나 별도의 줄에 삽입할 수 있습니다.|  
|[- &#40;주석&#41; &#40;DMX&#41; 요약](../dmx/comment-dmx-summary.md)|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 실행되지 않는 텍스트 문자열을 나타냅니다. 주석을 DMX 문 안에 중첩하거나 코드 줄 끝에 포함하거나 별도의 줄에 삽입할 수 있습니다.|  
|[별 슬래시 &#40;주석&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 실행되지 않는 텍스트 문자열을 나타냅니다. 주석을 DMX 문 안에 중첩하거나 코드 줄 끝에 포함하거나 별도의 줄에 삽입할 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 참조](../dmx/data-mining-extensions-dmx-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 표기 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [연산자 &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
