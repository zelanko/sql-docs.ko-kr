---
title: 집합 연산자 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df58b5c7f6da05700f00b4ec5fd46b81926dd3bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150166"
---
# <a name="set-operators"></a>집합 연산자


  MDX에서 집합 연산자는 멤버나 집합에 대한 연산을 수행하고 집합을 반환합니다. MDX 식의 여러 집합 함수에 대한 대체 방안으로 집합 연산자를 사용하는 경우도 있습니다.  
  
 MDX는 다음 표에 나열된 집합 연산자를 지원합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|[-(제외)](../mdx/except-mdx-operator.md)|두 집합 사이의 차이를 반환하여 중복 멤버를 제거합니다.<br /><br /> 이 연산자는 기능적으로 동일 합니다 [제외한](../mdx/except-mdx-function.md) 함수입니다.|  
|[*(크로스 조인)](../mdx/crossjoin-mdx-operator-reference.md)|두 집합의 교차곱을 반환합니다.<br /><br /> 이 연산자는 기능적으로 동일 합니다 [Crossjoin](../mdx/crossjoin-mdx.md) 함수입니다.|  
|[: (범위)](../mdx/range-mdx.md)|지정한 두 멤버를 엔드포인트로 하고 지정한 두 멤버 사이의 모든 멤버를 집합의 멤버로 포함하는 자연적으로 정렬된 집합을 반환합니다.|  
|[+(합집합)](../mdx/union-mdx-operator-reference.md)|두 집합의 합집합을 반환하여 중복 멤버를 제외합니다.<br /><br /> 이 연산자는 기능적으로 동일 합니다 [Union &#40;MDX&#41; ](../mdx/union-mdx.md) 함수입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [연산자 &#40;MDX 구문&#41;](../mdx/operators-mdx-syntax.md)  
  
  
