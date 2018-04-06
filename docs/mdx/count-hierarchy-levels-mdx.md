---
title: Count (계층 수준) (MDX) | Microsoft Docs
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
f1_keywords:
- COUNT
dev_langs:
- kbMDX
helpviewer_keywords:
- Count function [MDX]
ms.assetid: 3de6a824-2ff3-47ac-9ceb-e3369a04f35d
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b68bb6f266fefff1274241e6f5b2860fb522fb02
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="count-hierarchy-levels-mdx"></a>Count(계층 수준)(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  계층의 수준 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Hierarchy_Expression.Levels.Count  
```  
  
## <a name="arguments"></a>인수  
 *Hierarchy_Expression*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 계층의 수준 수를 반환합니다. 해당되는 경우 `[All]` 수준이 포함됩니다.  
  
> [!IMPORTANT]  
>  차원에 표시 가능한 계층이 하나만 있는 경우 해당 차원 이름은 표시 가능한 유일한 계층으로 확인되므로 해당 계층을 차원 이름이나 계층 이름 중 하나로 참조할 수 있습니다. 예를 들어 `Measures.Levels.Count`는 Measures 차원의 유일한 계층으로 확인되므로 유효한 MDX 식입니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Adventure Works 큐브에 있는 Product Categories 사용자 정의 계층의 수준 수를 반환합니다.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Product Categories].Levels.Count   
Select Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Count &#40; 차원 &#41; &#40; Mdx&#41;](../mdx/count-dimension-mdx.md)   
 [Count &#40; 튜플 &#41; &#40; Mdx&#41;](../mdx/count-tuple-mdx.md)   
 [Count &#40; 설정 &#41; &#40; Mdx&#41;](../mdx/count-set-mdx.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
