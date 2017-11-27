---
title: Value (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Value
dev_langs:
- kbMDX
helpviewer_keywords:
- Value function
ms.assetid: ff76628e-2d49-49f6-a6cb-f6da07d83d65
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 63e24e0f701332747e3129a57768bfe1b6fbb45d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="value-mdx"></a>Value(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  쿼리 컨텍스트에서 특성 계층의 현재 멤버와 교차하는 Measures 차원의 현재 멤버 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **값** 함수를 문자열로 지정된 된 멤버의 값을 반환 합니다. **값** 인수는 선택 사항 때문 멤버의 값은 멤버의 기본 속성은 다른 값을 지정 하지 경우 멤버에 대해 반환 되는 값입니다. 멤버의 속성에 대 한 자세한 내용은 참조 [내장 멤버 속성 &#40; Mdx&#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md) 및 [사용자 정의 멤버 속성 &#40; Mdx&#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [MemberValue &#40; Mdx&#41;](../mdx/membervalue-mdx.md)   
 [속성 &#40; Mdx&#41;](../mdx/properties-mdx.md)   
 [이름 &#40; Mdx&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40; Mdx&#41;](../mdx/uniquename-mdx.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

