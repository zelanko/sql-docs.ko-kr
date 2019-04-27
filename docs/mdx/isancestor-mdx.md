---
title: IsAncestor (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8aacd6825a81ff172d8fdf79373f5b251d6e18b9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653473"
---
# <a name="isancestor-mdx"></a>IsAncestor(MDX)


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
 합니다 **IsAncestor** 함수에서 반환 **true** 지정 된 첫 번째 멤버가 지정 된 두 번째 멤버의 상위 항목이 면 합니다. 반환이 고, 그렇지 **false**합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 반환 **true** 경우 [Date]. [ Fiscal]. CurrentMember는 2003 년 1 월의 상위 같습니다.  
  
 `WITH MEMBER MEASURES.ISANCESTORDEMO AS`  
  
 `IsAncestor([Date].[Fiscal].CurrentMember, [Date].[Fiscal].[Month].&[2003]&[1])`  
  
 `SELECT MEASURES.ISANCESTORDEMO ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [상위 &#40;MDX&#41;](../mdx/ancestor-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
