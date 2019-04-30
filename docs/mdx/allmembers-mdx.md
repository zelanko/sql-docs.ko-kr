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
manager: kfile
ms.openlocfilehash: 92cde0acf07f62d0678da6dd96efa707dedc1a1f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63066251"
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
  
## <a name="remarks"></a>Remarks  
 합니다 **AllMembers** 함수는 지정 된 계층 이나 수준의 계산된 멤버를 포함 하는 모든 멤버가 포함 된 집합을 반환 합니다. 합니다 **AllMembers** 함수는 지정 된 계층 이나 수준에 표시 가능한 멤버가 없는 경우에 계산된 멤버를 반환 합니다.  
  
> [!IMPORTANT]  
>  차원에 표시 가능한 계층이 하나만 있는 경우 해당 차원 이름은 표시 가능한 유일한 계층으로 확인되므로 해당 계층을 차원 이름이나 계층 이름 중 하나로 참조할 수 있습니다. 예를 들어 `Measures.AllMembers`는 Measures 차원의 유일한 계층으로 확인되므로 유효한 MDX 식입니다.  
  
> [!NOTE]  
>  합니다 **AllMembers** 함수는 의미 체계가 비슷합니다 합니다 [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md) 함수입니다.  
  
## <a name="examples"></a>예  
 모든 멤버를 반환 하는 다음 예제는 [`Date].[Calendar Year]` 열 축에 특성 계층에 여기에 계산된 멤버, 및의 모든 자식 항목 집합을 `[Product].[Model Name]` 특성 계층을 행 축에는 **Adventure Works** 큐브.  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 다음 예제에서 모든 멤버를 반환 합니다 **측정값** 차원 열 축에이 모든 계산된 멤버, 및의 모든 자식 항목 집합을 포함 합니다 `[Product].[Model Name]` 특성 행 축에는 계층에서의 **Adventure Works** 큐브.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [AddCalculatedMembers&#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Children&#40;MDX&#41;](../mdx/children-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
