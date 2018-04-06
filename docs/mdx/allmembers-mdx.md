---
title: AllMembers (MDX) | Microsoft Docs
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
- ALLMEMBERS
dev_langs:
- kbMDX
helpviewer_keywords:
- AllMembers function
ms.assetid: 202e81d4-d2ee-4ec1-a019-4835eb19f446
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 67b0b2071e03d3b66daa1a34a6af4159cee89cea
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="allmembers-mdx"></a>AllMembers(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>주의  
 **AllMembers** 함수는 지정 된 계층 이나 수준에 계산된 멤버를 포함 하는 모든 멤버가 포함 된 집합을 반환 합니다. **AllMembers** 함수는 지정 된 계층 이나 수준에 표시 가능한 멤버가 없는 경우에 계산된 멤버를 반환 합니다.  
  
> [!IMPORTANT]  
>  차원에 표시 가능한 계층이 하나만 있는 경우 해당 차원 이름은 표시 가능한 유일한 계층으로 확인되므로 해당 계층을 차원 이름이나 계층 이름 중 하나로 참조할 수 있습니다. 예를 들어 `Measures.AllMembers`는 Measures 차원의 유일한 계층으로 확인되므로 유효한 MDX 식입니다.  
  
> [!NOTE]  
>  **AllMembers** 함수는 의미 체계가 비슷합니다는 [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md) 함수입니다.  
  
## <a name="examples"></a>예  
 모든 멤버를 반환 하는 다음 예제는 [`Date].[Calendar Year]` 열 축에 특성 계층, 여기에 계산된 멤버, 및의 모든 자식 항목 집합은 `[Product].[Model Name]` 특성 계층에서 행 축에는 **Adventure Works** 큐브.  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 모든 멤버를 반환 하는 다음 예제는 **측정값** 차원 열 축에 여기에 모든 계산된 멤버와의 모든 자식 항목 집합의 `[Product].[Model Name]` 특성 계층에서 행 축에는 **Adventure Works** 큐브.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [AddCalculatedMembers &#40; Mdx&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [자식 &#40; Mdx&#41;](../mdx/children-mdx.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
