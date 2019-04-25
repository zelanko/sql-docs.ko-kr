---
title: 비교 연산자 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8049f2bad6e78ff301b460b1375a0a73807ccd8d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62501983"
---
# <a name="operators---comparison"></a>연산자 - 비교
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  비교 연산자를 사용 하 여 모든 확장 DMX (Data Mining) 식에서 스칼라 데이터와 함께 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]합니다. 비교 연산자는 Boolean 데이터 형식으로 평가되며 검사된 조건의 결과를 기준으로 TRUE 또는 FALSE를 반환합니다.  
  
 다음 표에서는 DMX가 지원하는 비교 연산자를 설명합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|[&#60;&#40;보다 작거나&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|인수가 Null이 아닌 값으로 계산되고 왼쪽의 인수 값이 오른쪽의 인수 값보다 작으면 TRUE를 반환하고 크거나 같으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[&#62;&#40;보다 큰&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|인수가 Null이 아닌 값으로 계산되고 왼쪽의 인수 값이 오른쪽의 인수 값보다 크면 TRUE를 반환하고 작거나 같으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[= &#40;같음&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|인수가 Null이 아닌 값으로 계산되고 왼쪽의 인수 값과 오른쪽의 인수 값이 같으면 TRUE를 반환하고 다르면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[&#60;&#62;&#40;같지 않음&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|인수가 Null이 아닌 값으로 계산되고 왼쪽의 인수 값과 오른쪽의 인수 값이 다르면 TRUE를 반환하고 같으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[&#60;= &#40;보다 작거나 같음&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|인수가 Null이 아닌 값으로 계산되고 왼쪽의 인수 값이 오른쪽의 인수 값보다 작거나 같으면 TRUE를 반환하고 크면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[&#62;= &#40;크거나 같거나&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|인수가 Null이 아닌 값으로 계산되고 왼쪽의 인수 값이 오른쪽의 인수 값보다 크거나 같으면 TRUE를 반환하고 작으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
  
 DMX 문과 함수에 비교 연산자를 사용하여 조건을 찾을 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions & #40; DMX & #41; 참조](../dmx/data-mining-extensions-dmx-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 표기 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [식 &#40;DMX&#41;](../dmx/expressions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [연산자 &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [DMX 예측 쿼리의 구조 및 사용법](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
