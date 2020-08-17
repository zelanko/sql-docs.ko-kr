---
description: IsAncestor(MDX)
title: IsAncestor (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ccc61de94c87972eda3dbebdba798f9b1c4028b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341489"
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
  
## <a name="remarks"></a>설명  
 **Isancestor** 함수는 지정 된 첫 번째 멤버가 지정 된 두 번째 멤버의 상위 항목인 경우 **true** 를 반환 합니다. 그렇지 않으면 함수는 **false**를 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 [Date] 인 경우 **true** 를 반환 합니다. [회계]. CurrentMember는 1 월 2003의 상위 항목입니다.  
  
 `WITH MEMBER MEASURES.ISANCESTORDEMO AS`  
  
 `IsAncestor([Date].[Fiscal].CurrentMember, [Date].[Fiscal].[Month].&[2003]&[1])`  
  
 `SELECT MEASURES.ISANCESTORDEMO ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [상위 &#40;MDX&#41;](../mdx/ancestor-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
