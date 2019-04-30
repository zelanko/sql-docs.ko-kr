---
title: Wtd (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9a548f25d9114e9032f2462bbc97bda637abd6d9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251527"
---
# <a name="wtd-mdx"></a>Wtd(MDX)


  지정한 멤버와 동일한 수준의 형제 멤버 집합을 반환합니다. 이 집합은 첫 번째 형제 멤버부터 시작하여 지정된 멤버에서 끝나며 Time 차원의 Week 수준에 따라 제한됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Wtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 멤버 식을 지정 하지 않으면 기본값이 있으며 수준 유형이 인 첫 번째 계층의 현재 멤버 Time 유형의 첫 번째 차원의 주 (**Time.CurrentMember**) 측정값 그룹에 있습니다.  
  
 합니다 **Wtd** 함수는에 대 한 바로 가기 함수는 [PeriodsToDate](../mdx/periodstodate-mdx.md) 수준에 설정 되어 있는 함수 *주*합니다. 즉, `Wtd(Member_Expression)`은 `PeriodsToDate(Week_Level_Expression,Member_Expression)`과 동일합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Qtd &#40;MDX&#41;](../mdx/qtd-mdx.md)   
 [Mtd &#40;MDX&#41;](../mdx/mtd-mdx.md)   
 [Ytd &#40;MDX&#41;](../mdx/ytd-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
