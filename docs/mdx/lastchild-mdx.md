---
title: LastChild (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 29edcf11644f316a3ab57ea304b785567abc2653
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578845"
---
# <a name="lastchild-mdx"></a>LastChild(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 멤버의 마지막 자식 항목을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.LastChild   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
### <a name="example"></a>예제  
 다음 예에서는 2002 회계 연도에서 첫 번째 회계 분기의 마지막 자식 항목인 2001년 9월의 값을 반환합니다.  
  
```  
SELECT [Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002].LastChild ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [FirstChild &#40;MDX&#41;](../mdx/firstchild-mdx.md)   
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
