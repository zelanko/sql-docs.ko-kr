---
title: "산술 연산자 (DMX) | Microsoft Docs"
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
helpviewer_keywords: arithmetic operators
ms.assetid: befe4f0c-e5dd-4ae1-b88e-6ac7aab2181a
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2e376910297723821351570d76c076c15748e0a2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="operators---arithmetic"></a>산술 연산자-
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  산술 계산에 대 한 산술 연산자의 확장 DMX (Data Mining)을 사용할 수 있습니다 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 더하기, 빼기, 곱하기 및 나누기 포함 합니다.  
  
 다음 표에서는 DMX에서 지원하는 산술 연산자를 설명합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|[+ &#40; 추가 &#41; &#40; DMX &#41;](../dmx/add-dmx.md)|두 수를 더합니다.|  
|[-&#40; 빼기 &#41; &#40; DMX &#41;](../dmx/subtract-dmx.md)|한 수에서 다른 수를 뺍니다.|  
|[&#42; &#40; 곱하기 &#41; &#40; DMX &#41;](../dmx/multiply-dmx.md)|두 수를 곱합니다.|  
|[&#40; 나누기 &#41; &#40; DMX &#41;](../dmx/divide-dmx.md)|한 수를 다른 수로 나눕니다.|  
  
 다음 규칙은 DMX 식에서 산술 연산자의 우선 순위를 나타냅니다.  
  
-   식에 하나 이상의 산술 연산자가 있는 경우 곱하기와 나누기를 먼저 계산한 다음 빼기와 더하기를 계산합니다.  
  
-   식에 포함된 모든 산술 연산자의 우선 순위가 동일한 경우에는 왼쪽에서 오른쪽 순으로 연산이 실행됩니다.  
  
-   괄호 안의 식은 다른 모든 연산보다 우선적으로 처리됩니다.  
  
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
  
  
