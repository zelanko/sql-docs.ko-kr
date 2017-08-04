---
title: Mtd (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MTD
dev_langs:
- kbMDX
helpviewer_keywords:
- Mtd function
ms.assetid: 07d8fd65-f9e6-42d4-868d-fccfac6bdb70
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b177ad5ade9a3c73299fa675674eb5c783df79d4
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="mtd-mdx"></a>Mtd(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 멤버와 동일한 수준의 형제 멤버 집합을 반환합니다. 이 집합은 첫 번째 형제 멤버부터 시작하여 지정된 멤버에서 끝나며 Time 차원의 Year 수준에 따라 제한됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Mtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 기본값은 있으며 수준 유형이 인 첫 번째 계층의 현재 멤버 멤버 식이 지정 되지 않은 경우 *개월* 유형의 첫 번째 차원에 *시간* 측정값 그룹에 있습니다.  
  
 **Mtd** 함수에 대 한 바로 가기 함수는는 [PeriodsToDate](../mdx/periodstodate-mdx.md) 수준을 기준으로 특성 계층의 Type 속성이로 설정 되는 경우에 작동 *개월*합니다. 즉, `Mtd(Member_Expression)`은 `PeriodsToDate(Month_Level_Expression,Member_Expression)`과 동일합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 2002년 7월 중 7월 20일까지의 일별 인터넷 판매 운송 비용의 합계를 반환합니다.  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [Sum &#40; Mdx&#41;](../mdx/sum-mdx.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

