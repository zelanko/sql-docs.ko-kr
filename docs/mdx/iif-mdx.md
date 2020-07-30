---
title: IIf (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ca6449308f9683bccf55e58d9cec6d5d5a97a59e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247137"
---
# <a name="iif-mdx"></a>IIf(MDX)


  Boolean 조건이 true 또는 false인지에 따라 다른 분기 식을 계산합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>인수  
 IIf 함수는 세 가지 인수인 iif ( \<condition> , \<then branch> ,)를 사용 \<else branch> 합니다.  
  
 *Logical_Expression*  
 **True** (1) 또는 **false** (0)로 계산 되는 조건입니다. 유효한 MDX(Multidimensional Expressions) 논리식이어야 합니다.  
  
 *Expression1 힌트 [즉시 | Strict | Lazy]]*  
 논리 식이 **true**로 평가 될 때 사용 됩니다. Expression1은 유효한 MDX(Multidimensional Expressions) 식이어야 합니다.  
  
 *식 2 힌트 [즉시 | Strict | Lazy]]*  
 논리 식이 **false**로 계산 될 때 사용 됩니다. Expression2는 유효한 MDX(Multidimensional Expressions) 식이어야 합니다.  
  
## <a name="remarks"></a>설명  
 이 식의 값이 0 인 경우 논리 식으로 지정 된 조건이 **false** 로 평가 됩니다. 다른 모든 값은 **true**로 평가 됩니다.  
  
 조건이 **true**인 경우 **IIf** 함수는 첫 번째 식을 반환 합니다. 그렇지 않은 경우 이 함수는 두 번째 식을 반환합니다.  
  
 지정된 식은 값이나 MDX 개체를 반환할 수 있습니다. 또한 지정된 식은 형식이 일치할 필요가 없습니다.  
  
 검색 조건에 따라 멤버 집합을 만드는 경우 **IIf** 함수를 사용 하지 않는 것이 좋습니다. 대신 [Filter](../mdx/filter-mdx.md) 함수를 사용 하 여 지정 된 집합의 각 멤버를 논리 식에 대해 평가 하 고 멤버의 하위 집합을 반환 합니다.  
  
> [!NOTE]  
>  두 식 중 하나가 NULL인 경우 조건을 만족하면 결과 집합은 NULL이 됩니다.  
  
 힌트는 식이 계산되는 방식과 시기를 결정하는 선택적 한정자입니다. 식이 계산되는 방법을 지정하여 기본 쿼리 계획을 재정의할 수 있습니다.  
  
-   EAGER는 원래 IIF 하위 공간으로 식을 계산합니다.  
  
-   STRICT는 논리적 조건식으로 만든 제한된 하위 공간에서만 식을 계산합니다.  
  
-   LAZY는 셀별 모드에서 식을 계산합니다.  
  
 EAGER 및 STRICT는 IIF의 then-else 분기에만 적용되지만 LAZY는 모든 MDX 식에 적용됩니다. 모든 MDX 식은 셀별 모드에서 해당 식을 계산하는 HINT LAZY 뒤에 올 수도 있습니다.  
  
 EAGER 및 STRICT는 힌트에서 함께 사용할 수 없으며 동일한 IIF(,,)에서 서로 다른 식에 대해 사용할 수 있습니다.  
  
 자세한 내용은 [SQL Server Analysis Services 2008의 IIF 함수 쿼리 힌트](http://www.ssas-info.com/analysis-services-articles/50-mdx/1103-iif-function-query-hints-in-sql-server-analysis-services-2008) 및 [MDX IIF 함수 및 CASE 문에 대 한 실행 계획 및 계획 힌트](https://go.microsoft.com/fwlink/?LinkId=269565)를 참조 하세요.  
  
## <a name="examples"></a>예제  
 다음 쿼리에서는 계산 측정값 내에서 **IIF** 를 간단 하 게 사용 하 여 측정값 Internet Sales Amount가 $1만 보다 크거나 작은 경우 두 개의 다른 문자열 값 중 하나를 반환 하는 방법을 보여 줍니다.  
  
 `WITH MEMBER MEASURES.IIFDEMO AS`  
  
 `IIF([Measures].[Internet Sales Amount]>10000`  
  
 `, "Sales Are High", "Sales Are Low")`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.IIFDEMO} ON 0,`  
  
 `[Date].[Date].[Date].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 IIF가 매우 일반적으로 사용되는 경우는 다음 예와 같이 계산 측정값 내에서 '0으로 나누기' 오류를 처리하는 경우입니다.  
  
 `WITH`  
  
 `//Returns 1.#INF when the previous period contains no value`  
  
 `//but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth With Errors] AS`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `,FORMAT_STRING='PERCENT'`  
  
 `//Traps division by zero and returns null when the previous period contains`  
  
 `//no value but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth] AS`  
  
 `IIF(([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)=0,`  
  
 `NULL,`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `),FORMAT_STRING='PERCENT'`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.[Previous Period Growth With Errors], MEASURES.[Previous Period Growth]} ON 0,`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004],`  
  
 `[Date].[Calendar].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 다음은 행에 대 한 복잡 한 튜플 집합을 만들기 위해 Generate 함수 내의 두 집합 중 하나를 반환 하는 **IIF** 의 예입니다.  
  
 `SELECT {[Measures].[Internet Sales Amount]} ON 0,`  
  
 `//If Internet Sales Amount is zero or null`  
  
 `//returns the current year and the All Customers member`  
  
 `//else returns the current year broken down by Country`  
  
 `GENERATE(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `, IIF([Measures].[Internet Sales Amount]=0,`  
  
 `{([Date].[Calendar Year].CURRENTMEMBER, [Customer].[Country].[All Customers])}`  
  
 `, {{[Date].[Calendar Year].CURRENTMEMBER} * [Customer].[Country].[Country].MEMBERS}`  
  
 `))`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 마지막으로 이 예에서는 Plan Hints를 사용하는 방법을 보여 줍니다.  
  
 `WITH MEMBER MEASURES.X AS`  
  
 `IIF(`  
  
 `[Measures].[Internet Sales Amount]=0`  
  
 `, NULL`  
  
 `, (1/[Measures].[Internet Sales Amount]) HINT EAGER)`  
  
 `SELECT {[Measures].x} ON 0,`  
  
 `[Customer].[Customer Geography].[Country].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
