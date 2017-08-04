---
title: "차원 식을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- expressions [MDX], dimensions
- dimensions [Analysis Services], MDX
ms.assetid: 1d40cffb-e88f-4284-93cf-d62ab4f08395
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 66a955b547f5760ae1193b541fde5f3dc13d323f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="using-dimension-expressions"></a>차원 식 사용
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  일반적으로 MDX(Multidimensional Expressions)에서 함수에 매개 변수를 전달할 때 차원 식과 계층 식을 사용하여 계층의 멤버, 집합 또는 튜플을 반환합니다.  
  
 차원 식은 개체 식별자이므로 간단한 식만 될 수 있습니다. 참조 [식 &#40; Mdx&#41; ](../mdx/expressions-mdx.md) 에 대 한 설명은 간단한 식 및 복잡 한 식입니다.  
  
## <a name="dimension-expressions"></a>차원 식  
 차원 식에는 차원 식별자 또는 차원 함수가 포함됩니다.  
  
 차원 식은 자체적으로는 거의 사용되지 않습니다. 대신 사용자가 일반적으로 차원에 계층을 지정하려고 합니다. 단, 계층이 없는 Measures 차원을 사용할 때는 예외입니다.  
  
 다음 예에서는 [Measures] 식을 .Members 및 Count() 함수와 함께 사용하여 Measures 차원의 멤버 수를 반환하는 계산 멤버를 보여 줍니다.  
  
 `WITH MEMBER [Measures].[MeasureCount] AS`  
  
 `COUNT([Measures].MEMBERS)`  
  
 `SELECT [Measures].[MeasureCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 차원 식별자로 표시 *Dimension_Name* MDX 문을 설명 하는 데 사용 되는 BNF 표기법의 합니다.  
  
## <a name="hierarchy-expressions"></a>계층 식  
 마찬가지로 계층 식에는 계층 식별자 또는 계층 함수가 들어 있습니다. 다음 예에서는 [Date].[Calendar] 계층 식을 .Levels 및 .Count 함수와 함께 사용하여 Date 차원의 Calendar 계층에 있는 수준 수를 반환하는 방법을 보여 줍니다.  
  
 `WITH MEMBER [Measures].[CalendarLevelCount] AS`  
  
 `[Date].[Calendar].Levels.Count`  
  
 `SELECT [Measures].[CalendarLevelCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 계층 식이 사용되는 가장 일반적인 시나리오는 .Members 함수와 함께 사용되어 계층의 모든 멤버를 반환하는 것입니다. 다음 예에서는 Rows 축에 있는 [Date].[Calendar]의 모든 멤버를 반환합니다.  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 계층 식별자로 표시 *Dimension_Name**.* *Hierarchy_Name* MDX 문을 설명 하는 데 사용 되는 BNF 표기법의 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [식 &#40; Mdx&#41;](../mdx/expressions-mdx.md)  
  
  

