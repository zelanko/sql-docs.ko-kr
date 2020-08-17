---
description: Members(집합)(MDX)
title: Members (Set) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0358f20d0aeba0e4d455fabadb6dc1e4361081e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341399"
---
# <a name="members-set-mdx"></a>Members(집합)(MDX)


  차원, 수준 또는 계층의 멤버 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Hierarchy expression syntax  
Hierarchy_Expression.Members  
  
Level expression Syntax  
Level_Expression.Members  
```  
  
## <a name="arguments"></a>인수  
 *Hierarchy_Expression*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 계층 식이 지정 된 경우 **Members (Set)** 함수는 계산 멤버를 포함 하지 않고 지정 된 계층 내의 모든 멤버 집합을 반환 합니다. 계층에서 계산 되거나 다른 모든 멤버 집합을 가져오려면 [allmembers &#40;MDX&#41;](../mdx/allmembers-mdx.md) 함수를 사용 합니다.  
  
 수준 식이 지정 된 경우 **members (Set)** 함수는 지정 된 수준 내의 모든 멤버 집합을 반환 합니다.  
  
> [!IMPORTANT]  
>  차원에 표시 가능한 계층이 하나만 있는 경우 해당 차원 이름은 표시 가능한 유일한 계층으로 확인되므로 해당 계층을 차원 이름이나 계층 이름 중 하나로 참조할 수 있습니다. 예를 들어 Measures.Members는 Measures 차원의 유일한 계층으로 확인되므로 유효한 MDX 식입니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 Adventure Works 큐브에 있는 Calendar Year 계층의 모든 멤버 집합을 반환합니다.  
  
```  
SELECT   
   [Date].[Calendar].[Calendar Year].Members ON 0  
FROM  
   [Adventure Works]  
  
```  
  
 다음 예에서는 `[Product].[Products].[Product Line]` 수준의 각 멤버에 대해 2003년 주문 수량을 반환합니다. **Members** 함수는 수준의 모든 멤버를 나타내는 집합을 반환 합니다.  
  
```  
SELECT   
   {Measures.[Order Quantity]} ON COLUMNS,  
   [Product].[Product Line].[Product Line].Members ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
