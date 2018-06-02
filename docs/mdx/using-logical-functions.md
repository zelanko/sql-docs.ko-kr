---
title: 논리 함수를 사용 하 여 | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6bd427ebfca1fbf2f546603853b2352d6dcf4c90
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582465"
---
# <a name="using-logical-functions"></a>논리 함수 사용
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  논리 함수는 개체와 식에 대해 논리 연산이나 비교를 수행하고 부울 값을 반환합니다. MDX(Multidimensional Expressions)에서 멤버의 위치를 결정하는 데는 논리 함수가 필수적입니다.  
  
 가장 일반적으로 사용 되는 논리 함수는는 **IsEmpty** 함수입니다. 사용 하는 방법에 대 한 자세한 내용은 **IsEmpty** 함수, 참조 [빈 값 작업](../mdx/working-with-empty-values.md)합니다.  
  
 다음 쿼리를 사용 하는 방법을 보여 줍니다는 **IsLeaf** 및 **IsAncestor** 함수:  
  
 `WITH`  
  
 `//Returns true if the CurrentMember on Calendar is a leaf member, ie it has no children`  
  
 `MEMBER MEASURES.[IsLeafDemo] AS IsLeaf([Date].[Calendar].CurrentMember)`  
  
 `//Returns true if the CurrentMember on Calendar is an Ancestor of July 1st 2001`  
  
 `MEMBER MEASURES.[IsAncestorDemo] AS IsAncestor([Date].[Calendar].CurrentMember, [Date].[Calendar].[Date].&[1])`  
  
 `SELECT{MEASURES.[IsLeafDemo],MEASURES.[IsAncestorDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [함수 &#40;MDX 구문&#41;](../mdx/functions-mdx-syntax.md)  
  
  
