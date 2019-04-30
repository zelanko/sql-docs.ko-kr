---
title: Count (계층 수준) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 657ce658704b519c31dfaa2186429a7df4110308
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306805"
---
# <a name="count-hierarchy-levels-mdx"></a>Count(계층 수준)(MDX)


  계층의 수준 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Hierarchy_Expression.Levels.Count  
```  
  
## <a name="arguments"></a>인수  
 *Hierarchy_Expression*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>관련 항목  
 [Count &#40;차원&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [Count &#40;튜플&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [개수&#40;Set&#41;&#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
