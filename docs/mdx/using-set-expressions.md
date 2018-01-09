---
title: "집합 식을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- expressions [MDX], set
- tuples
- set expressions [MDX]
ms.assetid: 88d65872-0cbe-4c95-b36f-e1aa4ac8ed07
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ba59d13932b4d93f7d4992b8f26b6830ba67b395
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
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
  
 집합을 반환 하는 함수의 예 참조 [멤버, 튜플 및 집합 &#40; 사용 Mdx&#41; ](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
## <a name="see-also"></a>관련 항목:  
 [식 &#40; Mdx&#41;](../mdx/expressions-mdx.md)  
  
  
