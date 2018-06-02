---
title: LastSibling (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4c6755fb77a42a1043a3847d44b1692a471d2592
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579005"
---
# <a name="lastsibling-mdx"></a>LastSibling(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 멤버 부모 항목의 마지막 자식 항목을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.LastSibling   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
### <a name="example"></a>예제  
 다음 예에서는 2002년 7월 마지막 날에 대한 기본 측정값을 반환합니다.  
  
```  
SELECT [Date].[Fiscal].[Date].&[20020717].LastSibling   
   ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
