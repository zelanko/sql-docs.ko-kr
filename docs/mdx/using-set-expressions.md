---
title: 집합 식을 사용 하 여 | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b384bffc84140b966ea510834054c65986ba292
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581725"
---
# <a name="using-set-expressions"></a>집합 식 사용
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  집합은 0개 이상의 튜플이 순서대로 나열된 목록으로 구성되며 튜플을 전혀 포함하지 않은 집합을 빈 집합이라고 합니다.  
  
 집합의 전체 식은 중괄호로 묶인 0개 이상의 명시적으로 지정된 튜플로 구성됩니다.  
  
 {[{ *Tuple_expression* | *Member_expression* } [, { *Tuple_expression* | *Member_expression* }]...]을 (를)  
  
 집합 식에서 지정된 멤버 식은 멤버가 하나인 튜플 식으로 변환됩니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 쿼리의 Columns 및 Rows 축에 사용되는 두 집합 식을 보여 줍니다.  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]} ON COLUMNS,`  
  
 `{([Product].[Product Categories].[Category].&[4], [Date].[Calendar].[Calendar Year].&[2004]),`  
  
 `([Product].[Product Categories].[Category].&[1], [Date].[Calendar].[Calendar Year].&[2003]),`  
  
 `([Product].[Product Categories].[Category].&[3], [Date].[Calendar].[Calendar Year].&[2004])}`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Columns 축에서  
  
 {[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}  
  
 집합은 Measures 차원의 두 멤버로 구성됩니다. Rows 축에서  
  
 {([Product].[Product Categories].[Category].&[4], [Date].[Calendar].[Calendar Year].&[2004]),  
  
 ([Product].[Product Categories].[Category].&[1], [Date].[Calendar].[Calendar Year].&[2003]),  
  
 ([Product].[Product Categories].[Category].&[3], [Date].[Calendar].[Calendar Year].&[2004])}  
  
 집합은 3개의 튜플로 구성됩니다. 각 튜플은 Product 차원의 Product Categories 계층 및 Date 차원의 Calendar 계층에 있는 멤버에 대한 두 개의 명시적 참조를 포함합니다.  
  
 집합을 반환 하는 함수의 예 참조 [멤버, 튜플 및 집합 작업 &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [식 &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
