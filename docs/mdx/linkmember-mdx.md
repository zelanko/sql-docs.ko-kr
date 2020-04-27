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
ms.openlocfilehash: 8a00388e067878d9c2165cbae6844f8020b7c63e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905598"
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
  
## <a name="remarks"></a>설명  
 **Linkmember** 함수는 관련 계층에서 지정 된 멤버의 각 수준에서 키 값과 일치 하는 지정 된 계층의 멤버를 반환 합니다. 각 수준의 특성은 키 카디널리티와 데이터 형식이 동일해야 합니다. 비자연 계층에서 특성의 키 값에 대해 일치하는 항목이 둘 이상 있을 경우 오류가 발생하거나 결과를 알 수 없게 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **Linkmember** 함수를 사용 하 여 Calendar 계층의 상위 항목 특성 계층에 있는 2002 년 7 월 1 일에 해당 하는 데이터에 대 한 놀이 Works 큐브의 기본 측정값을 반환 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [상위 항목 &#40;MDX&#41;](../mdx/ascendants-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
