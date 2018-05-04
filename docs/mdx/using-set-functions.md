---
title: 집합 함수를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- set functions [MDX]
ms.assetid: b08ddc9d-38f8-41aa-b791-b5352f1a8783
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: bdc98dee4f56d940042e57620ea94ebf7611197a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-set-functions"></a>집합 함수 사용
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  집합 함수는 차원, 계층 및 수준에서 집합을 검색하거나 이들 개체에서 멤버의 절대 위치 및 상대 위치를 탐색하는 등의 다양한 방법으로 집합을 생성합니다.  
  
 집합 함수는 멤버 함수 및 튜플 함수와 마찬가지로 Analysis Services에서 사용되는 다차원 구조를 처리하는 데 필수적입니다. 집합 식은 MDX(Multidimensional Expressions) 쿼리의 축을 정의하므로 MDX 쿼리의 결과를 얻는 데도 필수적입니다.  
  
 가장 일반적인 집합 함수 중 하나는 [멤버 &#40;설정&#41; &#40;MDX&#41; ](../mdx/members-set-mdx.md) 모든 차원, 계층 또는 수준에서 멤버를 포함 하는 집합을 검색 하는 함수입니다. 다음은 쿼리 내에서 집합 함수를 사용하는 예입니다.  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns all of the members on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 자주 사용 되는 또 다른 함수는는 [Crossjoin &#40;MDX&#41; ](../mdx/crossjoin-mdx.md) 함수입니다. 이 함수는 함수에 매개 변수로 전달된 집합의 카티션 곱을 나타내는 튜플 집합을 반환합니다. 실제로 이 함수를 사용하면 쿼리에서 '중첩' 축 또는 '크로스탭' 축을 만들 수 있습니다.  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns a set containing every combination of all of the members`  
  
 `//on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension and all of the members on the Category level`  
  
 `//of the Category hierarchy on the Product dimension`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 [하위 항목 &#40;MDX&#41; ](../mdx/descendants-mdx.md) 함수는는 **자식** 작동 하지만 보다 강력 합니다. 이 함수는 계층의 하나 이상의 수준에서 모든 멤버의 하위 항목을 반환합니다.  
  
 SELECT  
  
 [Measures].[Internet Sales Amount]  
  
 ON Columns,  
  
 //Returns a set containing all of the Dates beneath Calendar Year  
  
 //2004 in the Calendar hierarchy of the Date dimension  
  
 DESCENDANTS(  
  
 [Date]입니다. [Calendar]입니다. [Calendar Year]. & [2004]  
  
 , [Date].[Calendar].[Date])  
  
 ON Rows  
  
 FROM [Adventure Works]  
  
 [순서 &#40;MDX&#41; ](../mdx/order-mdx.md) 함수를 사용 하면를 오름차순 또는 내림차순 키를 눌러 특정 숫자 식에 따라 집합의 내용을 요청 합니다. 다음 쿼리에서는 이전 쿼리에서와 동일한 행 멤버를 반환하지만 여기서는 해당 멤버를 Internet Sales Amount 측정값에 따라 정렬합니다.  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//ordered by Internet Sales Amount`  
  
 `ORDER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount], BDESC)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 또한 이 쿼리에서는 Descendants라는 한 설정 함수에서 반환한 집합을 Order라는 다른 집합 함수에 매개 변수로 전달하는 방법을 보여 줍니다.  
  
 특정 조건에 따라 집합 필터링은 쿼리를 작성할 때 매우 유용 하 고이 목적을 위해 사용할 수 있습니다는 [필터 &#40;MDX&#41; ](../mdx/filter-mdx.md) 다음 예제에 나와 있는 것 처럼 작동 합니다.  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//where Internet Sales Amount is greater than $70000`  
  
 `FILTER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount]>70000)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 집합을 다른 방식으로 필터링하는 보다 복잡한 다른 함수도 있습니다. 예를 들어 다음 쿼리 표시는 [TopCount &#40;MDX&#41; ](../mdx/topcount-mdx.md) 함수 집합의 상위 n 개 항목을 반환 합니다.  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing the top 10 Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension by Internet Sales Amount`  
  
 `TOPCOUNT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,10, [Measures].[Internet Sales Amount])`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 다양 한 논리적 집합 작업 등의 함수를 사용 하 여 수행할 수는 마지막으로 [Intersect &#40;MDX&#41;](../mdx/intersect-mdx.md), [Union &#40;MDX&#41; ](../mdx/union-mdx.md) 및 [ &#40;MDX&#41; ](../mdx/except-mdx-function.md) 함수입니다. 다음 쿼리에서는 이러한 함수 중 마지막 두 함수의 예를 보여 줍니다.  
  
 `SELECT`  
  
 `//Returns a set containing the Measures Internet Sales Amount, Internet Tax Amount and`  
  
 `//Internet Total Product Cost`  
  
 `UNION(`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}`  
  
 `, {[Measures].[Internet Total Product Cost]}`  
  
 `)`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//except the January 1st 2004`  
  
 `EXCEPT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,{[Date].[Calendar].[Date].&[915]})`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [함수 &#40;MDX 구문&#41;](../mdx/functions-mdx-syntax.md)   
 [멤버 함수를 사용 하 여](../mdx/using-member-functions.md)   
 [튜플 함수 사용](../mdx/using-tuple-functions.md)  
  
  
