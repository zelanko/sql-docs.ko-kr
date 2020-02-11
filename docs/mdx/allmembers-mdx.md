---
title: AllMembers (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 770d66941af9b42be3c7b26f7e04a60d2a95cac2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017154"
---
# <a name="allmembers-mdx"></a>AllMembers(MDX)


  계층 또는 수준 식을 계산하고 지정된 계층이나 수준의 계산 멤버를 비롯한 모든 멤버가 들어 있는 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.AllMembers  
  
Level syntax  
Level_Expression.AllMembers  
```  
  
## <a name="arguments"></a>인수  
 *Hierarchy_Expression*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **Allmembers** 함수는 지정 된 계층 또는 수준에서 계산 멤버를 포함 하는 모든 멤버를 포함 하는 집합을 반환 합니다. **Allmembers** 함수는 지정 된 계층 이나 수준에 표시 가능한 멤버가 없는 경우에도 계산 멤버를 반환 합니다.  
  
> [!IMPORTANT]  
>  차원에 표시 가능한 계층이 하나만 있는 경우 해당 차원 이름은 표시 가능한 유일한 계층으로 확인되므로 해당 계층을 차원 이름이나 계층 이름 중 하나로 참조할 수 있습니다. 예를 들어 `Measures.AllMembers`는 Measures 차원의 유일한 계층으로 확인되므로 유효한 MDX 식입니다.  
  
> [!NOTE]  
>  **Allmembers** 함수는 [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md) 함수와 의미상 유사 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 열 축에 있는 [`Date].[Calendar Year]` 특성 계층]의 모든 멤버를 반환 합니다. 여기에는 계산 멤버와 **어드벤처 Works** 큐브의 행 축 `[Product].[Model Name]` 에 있는 특성 계층의 모든 자식 항목이 포함 됩니다.  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 다음 예에서는 열 축에서 **측정값** 차원의 모든 멤버를 반환 합니다. 여기에는 모든 계산 멤버와 `[Product].[Model Name]` **어드벤처 Works** 큐브의 행 축에 있는 특성 계층의 모든 자식 집합이 포함 됩니다.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [MDX &#40;자식&#41;](../mdx/children-mdx.md)   
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
