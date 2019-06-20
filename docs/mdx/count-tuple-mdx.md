---
title: Count (튜플) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3775af63181489b982778d40ddd69ebc12872271
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63285042"
---
# <a name="count-tuple-mdx"></a>Count(튜플)(MDX)


  튜플의 차원 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Tuple_Expression.Count  
```  
  
## <a name="arguments"></a>인수  
 *Tuple_Expression*  
 튜플을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 튜플의 차원 수를 반환합니다.  
  
## <a name="example"></a>예제  
 다음 쿼리에서 계산 측정값은 `([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001])` 튜플에 표시된 계층 수인 값 2를 반환합니다.  
  
```  
WITH MEMBER MEASURES.COUNTTUPLE AS  
COUNT(([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001]))  
SELECT MEASURES.COUNTTUPLE ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [Count &#40;차원&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [Count &#40;계층 구조 수준&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [개수&#40;Set&#41;&#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
