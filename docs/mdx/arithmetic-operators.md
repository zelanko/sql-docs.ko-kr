---
title: 산술 연산자 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- arithmetic operators
ms.assetid: 1dff3e20-fe9d-4155-bf06-27d6458188e9
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6e835905fb1d51d4918c3d382ad6268925d469e4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="arithmetic-operators"></a>산술 연산자
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  MDX에서 산술 연산자를 사용하여 더하기, 빼기, 곱하기 및 나누기 등의 산술 계산을 수행할 수 있습니다.  
  
 MDX는 다음 테이블에 나열된 산술 연산자를 지원합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|[+(더하기)](../mdx/add-mdx.md)|두 숫자를 더합니다.|  
|[/ (나누기)](../mdx/divide-mdx-operator-reference.md)|한 수를 다른 수로 나눕니다.|  
|[*(곱하기)](../mdx/multiply-mdx.md)|두 숫자를 곱합니다.|  
|[-(빼기)](../mdx/subtract-mdx.md)|두 숫자의 차이 값을 구합니다.|  
|^ (거듭제곱)|한 수에 다른 수를 제곱합니다.|  
  
> [!NOTE]  
>  MDX에는 수의 제곱근을 구하는 함수가 포함되어 있지 않습니다. 수의 제곱근을 구하려면 ^ 연산자를 사용하여 해당 수를 0.5 지수의 거듭제곱으로 계산합니다.  
  
## <a name="order-of-precedence"></a>우선 순위  
 다음 규칙은 MDX 식에서 산술 연산자의 우선 순위를 결정합니다.  
  
-   식에 하나 이상의 산술 연산자가 있는 경우 MDX는 곱하기와 나누기를 먼저 계산한 다음 빼기와 더하기를 계산합니다.  
  
-   식에 포함된 모든 산술 연산자의 선행 규칙 수준이 동일할 경우 왼쪽에서 오른쪽 순서로 실행합니다.  
  
-   괄호 안의 식은 다른 모든 연산보다 선행됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 연산자 참조 &#40; Mdx&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [연산자 &#40; MDX 구문 &#41;](../mdx/operators-mdx-syntax.md)  
  
  
