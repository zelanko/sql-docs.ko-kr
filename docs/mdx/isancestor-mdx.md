---
title: IsAncestor (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 59c997398ce7a3e4477136d1c5ef2ebcd2686e2d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578625"
---
# <a name="isancestor-mdx"></a>IsAncestor(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 멤버가 지정한 다른 멤버의 상위 항목인지 여부를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsAncestor(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression1*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Member_Expression2*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 **IsAncestor** 함수에서 반환 **true** 지정 된 첫 번째 멤버가 지정 된 두 번째 멤버의 상위 항목이 면 합니다. 그렇지 않으면 함수가 반환 **false**합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 반환 **true** 경우 [Date]. [ Fiscal]. CurrentMember은 2003 년 1 월의 상위 항목입니다.  
  
 `WITH MEMBER MEASURES.ISANCESTORDEMO AS`  
  
 `IsAncestor([Date].[Fiscal].CurrentMember, [Date].[Fiscal].[Month].&[2003]&[1])`  
  
 `SELECT MEASURES.ISANCESTORDEMO ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [상위 &#40;MDX&#41;](../mdx/ancestor-mdx.md)   
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
