---
title: "비교 연산자 (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords: comparison operators [DMX]
ms.assetid: eea3cf90-9683-4453-b1f3-da740f3a4885
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4ac50c6884356bf98384d330e85afbc837a0c2f5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="operators---comparison"></a>연산자-비교
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  비교 연산자를 사용 하 여에 있는 모든 확장 DMX (Data Mining) 식의 스칼라 데이터와 함께 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]합니다. 비교 연산자는 Boolean 데이터 형식으로 평가되며 검사된 조건의 결과를 기준으로 TRUE 또는 FALSE를 반환합니다.  
  
 다음 표에서는 DMX가 지원하는 비교 연산자를 설명합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|[&#60; &#40; 보다 작거나 &#41; &#40; DMX &#41;](../dmx/less-than-dmx.md)|인수가 Null이 아닌 값으로 계산되고 왼쪽의 인수 값이 오른쪽의 인수 값보다 작으면 TRUE를 반환하고 크거나 같으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[&#62; &#40; 보다 큰 &#41; &#40; DMX &#41;](../dmx/greater-than-dmx.md)|인수가 Null이 아닌 값으로 계산되고 왼쪽의 인수 값이 오른쪽의 인수 값보다 크면 TRUE를 반환하고 작거나 같으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[= &#40; Equal To &#41; &#40; DMX &#41;](../dmx/equal-to-dmx.md)|인수가 Null이 아닌 값으로 계산되고 왼쪽의 인수 값과 오른쪽의 인수 값이 같으면 TRUE를 반환하고 다르면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[&#60; &#62; &#40; 하지 같음 &#41; &#40; DMX &#41;](../dmx/not-equal-to-dmx.md)|인수가 Null이 아닌 값으로 계산되고 왼쪽의 인수 값과 오른쪽의 인수 값이 다르면 TRUE를 반환하고 같으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[&#60; = &#40; 보다 작거나 같으면 &#41; &#40; DMX &#41;](../dmx/less-than-or-equal-to-dmx.md)|인수가 Null이 아닌 값으로 계산되고 왼쪽의 인수 값이 오른쪽의 인수 값보다 작거나 같으면 TRUE를 반환하고 크면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
|[&#62; = &#40; 보다 큼 또는 같음 &#41; &#40; DMX &#41;](../dmx/greater-than-or-equal-to-dmx.md)|인수가 Null이 아닌 값으로 계산되고 왼쪽의 인수 값이 오른쪽의 인수 값보다 크거나 같으면 TRUE를 반환하고 작으면 FALSE를 반환합니다. 인수 중 하나 또는 둘 다가 Null 값으로 계산되면 연산자는 Null 값을 반환합니다.|  
  
 DMX 문과 함수에 비교 연산자를 사용하여 조건을 찾을 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 참조](../dmx/data-mining-extensions-dmx-reference.md)   
 [Data Mining Extensions &#40; DMX &#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Data Mining Extensions &#40; DMX &#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40; DMX &#41; 구문 표기 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40; DMX &#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [식 &#40; DMX &#41;](../dmx/expressions-dmx.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [연산자 &#40; DMX &#41;](../dmx/operators-dmx.md)   
 [구조 및 DMX 예측 쿼리 사용](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
