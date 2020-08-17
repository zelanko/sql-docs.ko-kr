---
description: 논리 함수 사용
title: 논리 함수 사용 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2a13f9fa95878277b164b37bb71e3d9af646d89f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340999"
---
# <a name="using-logical-functions"></a>논리 함수 사용


  논리 함수는 개체와 식에 대해 논리 연산이나 비교를 수행하고 부울 값을 반환합니다. MDX(Multidimensional Expressions)에서 멤버의 위치를 결정하는 데는 논리 함수가 필수적입니다.  
  
 가장 일반적으로 사용 되는 논리 함수는 **IsEmpty** 함수입니다. **IsEmpty** 함수를 사용 하는 방법에 대 한 자세한 내용은 [빈 값 작업](../mdx/working-with-empty-values.md)을 참조 하세요.  
  
 다음 쿼리에서는 **Isleaf** 및 **isleaf** 함수를 사용 하는 방법을 보여 줍니다.  
  
 `WITH`  
  
 `//Returns true if the CurrentMember on Calendar is a leaf member, ie it has no children`  
  
 `MEMBER MEASURES.[IsLeafDemo] AS IsLeaf([Date].[Calendar].CurrentMember)`  
  
 `//Returns true if the CurrentMember on Calendar is an Ancestor of July 1st 2001`  
  
 `MEMBER MEASURES.[IsAncestorDemo] AS IsAncestor([Date].[Calendar].CurrentMember, [Date].[Calendar].[Date].&[1])`  
  
 `SELECT{MEASURES.[IsLeafDemo],MEASURES.[IsAncestorDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [함수 &#40;MDX 구문&#41;](../mdx/functions-mdx-syntax.md)  
  
  
