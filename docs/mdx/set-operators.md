---
title: "집합 연산자 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- set operators [MDX]
ms.assetid: 83500d2e-44b3-49eb-a221-3ce5a58277a5
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ed67b969d53eeb65009926cade623d2b87b9e175
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="set-operators"></a>집합 연산자
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  MDX에서 집합 연산자는 멤버나 집합에 대한 연산을 수행하고 집합을 반환합니다. MDX 식의 여러 집합 함수에 대한 대체 방안으로 집합 연산자를 사용하는 경우도 있습니다.  
  
 MDX는 다음 표에 나열된 집합 연산자를 지원합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|[-(제외)](../mdx/except-mdx-operator.md)|두 집합 사이의 차이를 반환하여 중복 멤버를 제거합니다.<br /><br /> 이 연산자는 기능적으로 동일는 [제외한](../mdx/except-mdx-function.md) 함수입니다.|  
|[* (Crossjoin)](../mdx/crossjoin-mdx-operator-reference.md)|두 집합의 교차곱을 반환합니다.<br /><br /> 이 연산자는 기능적으로 동일는 [Crossjoin](../mdx/crossjoin-mdx.md) 함수입니다.|  
|[: (범위)](../mdx/range-mdx.md)|지정한 두 멤버를 끝점으로 하고 지정한 두 멤버 사이의 모든 멤버를 집합의 멤버로 포함하는 자연적으로 정렬된 집합을 반환합니다.|  
|[+ (Union)](../mdx/union-mdx-operator-reference.md)|두 집합의 합집합을 반환하여 중복 멤버를 제외합니다.<br /><br /> 이 연산자는 기능적으로 동일는 [Union &#40; Mdx&#41; ](../mdx/union-mdx.md) 함수입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 연산자 참조 &#40; Mdx&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [연산자 &#40; MDX 구문 &#41;](../mdx/operators-mdx-syntax.md)  
  
  

