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
ms.openlocfilehash: b84c5a1902e80f8abe3828f4be1b5d570ec026ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104807"
---
# <a name="count-dimension-mdx"></a>Count(차원)(MDX)


  큐브의 계층 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>설명  
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
 [Count &#40;계층 구조 수준&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [개수&#40;Set&#41;&#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
