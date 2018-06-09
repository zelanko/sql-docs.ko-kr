---
title: Count (차원) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6ee8fe09f7a840d32511d3a208a4621612ee9939
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740152"
---
# <a name="count-dimension-mdx"></a>Count(차원)(MDX)


  큐브의 계층 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>Remarks  
 `[Measures].[Measures]` 계층을 포함하여 큐브의 계층 수를 반환합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Adventure Works 큐브의 계층 수를 반환합니다.  
  
```  
WITH MEMBER measures.X AS  
  dimensions.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [Count &#40;튜플&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [Count &#40;계층 수준&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Count &#40;설정&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
