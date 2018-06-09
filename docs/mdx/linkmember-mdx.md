---
title: LinkMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 71235953f592572bd7ac0dcb2493d97dd509f8b7
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741502"
---
# <a name="linkmember-mdx"></a>LinkMember(MDX)


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
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>관련 항목  
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [Ascendants &#40;MDX&#41;](../mdx/ascendants-mdx.md)   
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
