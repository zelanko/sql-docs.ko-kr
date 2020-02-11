---
title: 산술 연산자 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1898f3e9807d2ea4f80f99e9a7ef27e672d58a18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017077"
---
# <a name="arithmetic-operators"></a>산술 연산자


  MDX에서 산술 연산자를 사용하여 더하기, 빼기, 곱하기 및 나누기 등의 산술 계산을 수행할 수 있습니다.  
  
 MDX는 다음 테이블에 나열된 산술 연산자를 지원합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|[+ (추가)](../mdx/add-mdx.md)|두 숫자를 더합니다.|  
|[/(나누기)](../mdx/divide-mdx-operator-reference.md)|한 수를 다른 수로 나눕니다.|  
|[* (곱하기)](../mdx/multiply-mdx.md)|두 숫자를 곱합니다.|  
|[-(빼기)](../mdx/subtract-mdx.md)|두 숫자의 차이 값을 구합니다.|  
|^ (거듭제곱)|한 수에 다른 수를 제곱합니다.|  
  
> [!NOTE]  
>  MDX에는 수의 제곱근을 구하는 함수가 포함되어 있지 않습니다. 수의 제곱근을 구하려면 ^ 연산자를 사용하여 해당 수를 0.5 지수의 거듭제곱으로 계산합니다.  
  
## <a name="order-of-precedence"></a>우선 순위  
 다음 규칙은 MDX 식에서 산술 연산자의 우선 순위를 결정합니다.  
  
-   식에 하나 이상의 산술 연산자가 있는 경우 MDX는 곱하기와 나누기를 먼저 계산한 다음 빼기와 더하기를 계산합니다.  
  
-   식에 포함된 모든 산술 연산자의 선행 규칙 수준이 동일할 경우 왼쪽에서 오른쪽 순서로 실행합니다.  
  
-   괄호 안의 식은 다른 모든 연산보다 선행됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [연산자 &#40;MDX 구문&#41;](../mdx/operators-mdx-syntax.md)  
  
  
