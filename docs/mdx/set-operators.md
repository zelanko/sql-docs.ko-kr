---
title: "집합 연산자 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: set operators [MDX]
ms.assetid: 83500d2e-44b3-49eb-a221-3ce5a58277a5
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 612312b3c295e2b9b3f45c4fdba9049036fd7b19
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="set-operators"></a>집합 연산자
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  MDX에서 집합 연산자는 멤버나 집합에 대한 연산을 수행하고 집합을 반환합니다. MDX 식의 여러 집합 함수에 대한 대체 방안으로 집합 연산자를 사용하는 경우도 있습니다.  
  
 MDX는 다음 표에 나열된 집합 연산자를 지원합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|[-(제외)](../mdx/except-mdx-operator.md)|두 집합 사이의 차이를 반환하여 중복 멤버를 제거합니다.<br /><br /> 이 연산자는 기능적으로 동일는 [제외한](../mdx/except-mdx-function.md) 함수입니다.|  
|[*(크로스 조인)](../mdx/crossjoin-mdx-operator-reference.md)|두 집합의 교차곱을 반환합니다.<br /><br /> 이 연산자는 기능적으로 동일는 [Crossjoin](../mdx/crossjoin-mdx.md) 함수입니다.|  
|[:(범위)](../mdx/range-mdx.md)|지정한 두 멤버를 끝점으로 하고 지정한 두 멤버 사이의 모든 멤버를 집합의 멤버로 포함하는 자연적으로 정렬된 집합을 반환합니다.|  
|[+(합집합)](../mdx/union-mdx-operator-reference.md)|두 집합의 합집합을 반환하여 중복 멤버를 제외합니다.<br /><br /> 이 연산자는 기능적으로 동일는 [Union &#40; Mdx&#41; ](../mdx/union-mdx.md) 함수입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 연산자 참조 &#40; Mdx&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [연산자 &#40; MDX 구문 &#41;](../mdx/operators-mdx-syntax.md)  
  
  
