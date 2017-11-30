---
title: LinkMember (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LINKMEMBER
dev_langs: kbMDX
helpviewer_keywords: LinkMember function
ms.assetid: b9106f07-8ea2-4933-aed3-ee9c63acf7ac
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a6fafec6febad45fe226bb9b96abd8c1ad3bd6da
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="linkmember-mdx"></a>LinkMember(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 계층에서 지정한 멤버와 동일한 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
LinkMember(Member_Expression, Hierarchy_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Hierarchy_Expression*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **LinkMember** 함수 관련된 계층에 지정된 된 멤버의 각 수준에서 키 값과 일치 하는 지정 된 계층에서 멤버를 반환 합니다. 각 수준의 특성은 키 카디널리티와 데이터 형식이 동일해야 합니다. 비자연 계층에서 특성의 키 값에 대해 일치하는 항목이 둘 이상 있을 경우 오류가 발생하거나 결과를 알 수 없게 됩니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 **LinkMember** Adventure Works 큐브의 Calendar 계층에서 Date.Date 특성 계층의 2002년 7월 1일 멤버의 상위 항목에 대 한 기본 측정값을 반환 하는 함수입니다.  
  
```  
SELECT  Hierarchize  
   (Ascendants   
      (LinkMember   
         ([Date].[Date].[July 1, 2002], [Date].[Calendar]  
         )  
       )  
    ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Hierarchize &#40; Mdx&#41;](../mdx/hierarchize-mdx.md)   
 [상위 항목 &#40; Mdx&#41;](../mdx/ascendants-mdx.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
