---
description: Count(차원)(MDX)
title: Count (Dimension) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: afa58c330210e4fdb34d13892101e210f54cd3bd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429965"
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
  
## <a name="see-also"></a>참고 항목  
 [MDX&#41; &#40;&#40;수&#41;](../mdx/count-tuple-mdx.md)   
 [MDX&#41; &#40;&#40;계층 수준 수&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [MDX&#41; &#40;&#40;집합 수&#41;](../mdx/count-set-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
