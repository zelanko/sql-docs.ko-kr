---
title: Wtd (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: WTD
dev_langs: kbMDX
helpviewer_keywords: Wtd function
ms.assetid: 41066e1b-e802-4582-be4b-3ed7807b033e
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ef274decb624474873e3efa3f0a8860dfdbfff80
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="wtd-mdx"></a>Wtd(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 멤버와 동일한 수준의 형제 멤버 집합을 반환합니다. 이 집합은 첫 번째 형제 멤버부터 시작하여 지정된 멤버에서 끝나며 Time 차원의 Week 수준에 따라 제한됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Wtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 멤버 식이 지정 되지 않은 경우 기본값인 있으며 수준 유형이 인 첫 번째 계층의 현재 멤버에서 Time 유형의 첫 번째 차원 주 (**Time.CurrentMember**) 측정값 그룹에 있습니다.  
  
 **Wtd** 함수에 대 한 바로 가기 함수는는 [PeriodsToDate](../mdx/periodstodate-mdx.md) 경우 수준으로 설정 되어 함수 *주*합니다. 즉, `Wtd(Member_Expression)`은 `PeriodsToDate(Week_Level_Expression,Member_Expression)`과 동일합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Qtd &#40; Mdx&#41;](../mdx/qtd-mdx.md)   
 [Mtd &#40; Mdx&#41;](../mdx/mtd-mdx.md)   
 [Ytd &#40; Mdx&#41;](../mdx/ytd-mdx.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
