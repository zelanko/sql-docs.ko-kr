---
title: "논리 함수를 사용 하 여 | Microsoft Docs"
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
dev_langs: kbMDX
helpviewer_keywords: logical functions [MDX]
ms.assetid: 0cb34d53-9146-4924-9c9b-607afcb7a2be
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a752a7af9a1c24fa600adfbf969f99f5176acbde
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
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
  
## <a name="see-also"></a>관련 항목:  
 [함수 &#40; MDX 구문 &#41;](../mdx/functions-mdx-syntax.md)  
  
  
