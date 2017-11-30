---
title: "MDX 연산자 참조 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], operators
- operators [MDX]
- MDX [Analysis Services], operators
ms.assetid: 1cdb8c31-a5f6-4430-b509-f81344f4622a
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: ddbddfefdaf6b51cbd9cc60eb9111a6c07cfaac8
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="mdx-operator-reference-mdx"></a>MDX 연산자 참조(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  MDX 언어는 산술, 논리, 비교, 집합, 문자열 및 단항 연산자를 지원합니다. 다음 표에서는 지원되는 연산자와 해당 설명을 나열합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[-&#40; 설명 &#41; &#40; Mdx&#41;](../mdx/comment-mdx-operator-reference.md)|사용자가 제공한 주석 텍스트를 나타냅니다.|  
|[-&#40; 제외 하 고 &#41; &#40; Mdx&#41;](../mdx/except-mdx-operator.md)|중복된 멤버를 제거하고 두 집합 간의 차집합을 반환하는 집합 연산을 수행합니다.|  
|[-&#40; 음수 &#41; &#40; Mdx&#41;](../mdx/negative-mdx.md)|숫자 식의 음수 값을 반환하는 단항 연산을 수행합니다.|  
|[-&#40; 빼기 &#41; &#40; Mdx&#41;](../mdx/subtract-mdx.md)|한 수에서 다른 수를 빼는 산술 연산을 수행합니다.|  
|[&#42; &#40; 크로스 조인 &#41; &#40; Mdx&#41;](../mdx/crossjoin-mdx-operator-reference.md)|두 집합의 교차곱을 반환하는 집합 연산을 수행합니다.|  
|[&#42; &#40; 곱하기 &#41; &#40; Mdx&#41;](../mdx/multiply-mdx.md)|두 수를 곱하는 산술 연산을 수행합니다.|  
|[&#40; 나누기 &#41; &#40; Mdx&#41;](../mdx/divide-mdx-operator-reference.md)|한 수를 다른 수로 나누는 산술 연산을 수행합니다.|  
|[^ &#40; 전원 &#41; &#40; Mdx&#41;](../mdx/power-mdx.md)|한 수에 다른 수를 제곱하는 산술 연산을 수행합니다.|  
|[설명 &#40; Mdx&#41;](../mdx/comment-mdx.md)|사용자가 제공한 주석 텍스트를 나타냅니다.|  
|[&#40; 설명 &#41; &#40; Mdx&#41;](../mdx/comment-mdx-double-slash.md)|사용자가 제공하는 텍스트를 나타냅니다.|  
|[: &#40; 범위 &#41; &#40; Mdx&#41;](../mdx/range-mdx.md)|지정한 두 멤버를 끝점으로 사용하고 지정한 두 멤버 사이의 모든 멤버를 집합의 멤버로 포함시켜 일반적인 순서로 정렬된 집합을 반환하는 집합 연산을 수행합니다.|  
|[+ &#40; 추가 &#41; &#40; Mdx&#41;](../mdx/add-mdx.md)|두 수를 더하는 산술 연산을 수행합니다.|  
|[+ &#40; 양수 &#41; &#40; Mdx&#41;](../mdx/positive-mdx.md)|숫자 식의 양수 값을 반환하는 단항 연산을 수행합니다.|  
|[+ &#40; 문자열 연결 &#41; &#40; Mdx&#41;](../mdx/string-concatenation-mdx.md)|둘 이상의 문자열, 튜플 또는 문자열과 튜플의 조합을 연결하는 문자열 연산을 수행합니다.|  
|[+ &#40; Union &#41; &#40; Mdx&#41;](../mdx/union-mdx-operator-reference.md)|중복된 요소를 제거하고 두 집합의 합집합을 반환하는 집합 연산을 수행합니다.|  
|[&#60; &#40; 보다 작거나 &#41; &#40; Mdx&#41;](../mdx/less-than-mdx.md)|하나의 MDX 식의 값이 다른 MDX 식의 값보다 작은지 확인하는 비교 연산을 수행합니다.|  
|[&#60; = &#40; 보다 작거나 같으면 &#41; &#40; Mdx&#41;](../mdx/less-than-or-equal-to-mdx.md)|하나의 MDX 식의 값이 다른 MDX 식의 값보다 작거나 같은지 확인하는 비교 연산을 수행합니다.|  
|[&#60; &#62; &#40; 하지 같음 &#41; &#40; Mdx&#41;](../mdx/not-equal-to-mdx.md)|하나의 MDX 식의 값이 다른 MDX 식의 값과 다른지 확인하는 비교 연산을 수행합니다.|  
|[= &#40; Equal To &#41; &#40; Mdx&#41;](../mdx/equal-to-mdx.md)|하나의 MDX 식의 값이 다른 MDX 식의 값과 동일한지 확인하는 비교 연산을 수행합니다.|  
|[&#62; &#40; 보다 큰 &#41; &#40; Mdx&#41;](../mdx/greater-than-mdx.md)|하나의 MDX 식의 값이 다른 MDX 식의 값보다 큰지 확인하는 비교 연산을 수행합니다.|  
|[&#62; = &#40; 보다 큼 또는 같음 &#41; &#40; Mdx&#41;](../mdx/greater-than-or-equal-to-mdx.md)|하나의 MDX 식의 값이 다른 MDX 식의 값보다 크거나 같은지 확인하는 비교 연산을 수행합니다.|  
|[및 &#40; MDX&#41;](../mdx/and-mdx.md)|두 숫자 식에 논리 결합을 수행합니다.|  
|[&#40; MDX&#41;](../mdx/is-mdx.md)|두 개체 식에 대해 논리 비교를 수행합니다.|  
|[하지 &#40; MDX&#41;](../mdx/not-mdx.md)|숫자 식에 논리 부정을 수행합니다.|  
|[또는 &#40; MDX&#41;](../mdx/or-mdx.md)|두 숫자 식에 논리 분리를 수행합니다.|  
|[XOR &#40; MDX&#41;](../mdx/xor-mdx.md)|두 숫자 식에 대해 논리 제외를 수행합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 언어 참조 &#40; Mdx&#41;](../mdx/mdx-language-reference-mdx.md)  
  
  
