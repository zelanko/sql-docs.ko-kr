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
ms.openlocfilehash: eee40829c72394bf95a1bc06540a434a1c74e166
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125809"
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
  
## <a name="remarks"></a>설명  
 멤버 식이 지정 되지 않은 경우 기본값은 측정값 그룹에서 Time (**CurrentMember**) 유형의 첫 번째 차원에 있는 첫 번째 계층의 현재 멤버입니다.  
  
 **Wtd** 함수는 Level이 *주*로 설정 된 [PeriodsToDate](../mdx/periodstodate-mdx.md) 함수에 대 한 바로 가기 함수입니다. 즉, `Wtd(Member_Expression)`은 `PeriodsToDate(Week_Level_Expression,Member_Expression)`과 동일합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Qtd &#40;MDX&#41;](../mdx/qtd-mdx.md)   
 [Mtd &#40;MDX&#41;](../mdx/mtd-mdx.md)   
 [Ytd &#40;MDX&#41;](../mdx/ytd-mdx.md)   
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
