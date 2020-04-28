---
title: 값 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f373f626d778c4d77ec5843dca5bb11da728451d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68887449"
---
# <a name="value-mdx"></a>Value(MDX)


  쿼리 컨텍스트에서 특성 계층의 현재 멤버와 교차하는 Measures 차원의 현재 멤버 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **Value** 함수는 지정 된 멤버의 값을 문자열로 반환 합니다. 멤버의 값은 멤버의 기본 속성이 고 다른 값이 지정 되지 않은 경우 멤버에 대해 반환 되는 값 이므로 **value** 인수는 선택 사항입니다. 멤버의 속성에 대 한 자세한 내용은 [기본 멤버 속성 &#40;mdx&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) 및 [Mdx&#41;&#40;사용자 정의 멤버 속성 ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties)을 참조 하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 멤버 값을 반환하고 멤버 이름을 명시적으로 반환합니다.  
  
```  
WITH MEMBER [Date].[Calendar].NumericValue as [Date].[Calendar].[July 1, 2001].Value  
MEMBER [Date].[Calendar].MemberName AS [Date].[Calendar].[July 1, 2001].Name  
  
SELECT {[Date].[Calendar].NumericValue, [Date].[Calendar].MemberName} ON 0  
from [Adventure Works]  
```  
  
 다음 예에서는 축의 멤버에 대해 반환되는 기본값으로 멤버 값을 반환합니다.  
  
```  
SELECT {[Date].[Calendar].[July 1, 2001]} ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MemberValue &#40;MDX&#41;](../mdx/membervalue-mdx.md)   
 [MDX &#40;속성&#41;](../mdx/properties-mdx.md)   
 [이름 &#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
