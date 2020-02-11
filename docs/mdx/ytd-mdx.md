---
title: Ytd (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e3fcd823dea5d651cd7be9295fa4c6bba25380c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125758"
---
# <a name="ytd-mdx"></a>Ytd(MDX)


  지정 된 멤버와 동일한 수준의 형제 멤버 집합을 반환 합니다 .이 집합은 첫 번째 형제부터 시작 하 여 지정 된 멤버로 끝나는 시간 차원의 *Year* 수준에 의해 제한 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 멤버 식이 지정 되지 않은 경우 기본값은 측정값 그룹에서 *Time* 형식의 첫 번째 차원에서 *year 형식의 수준을* 가진 첫 번째 계층의 현재 멤버입니다.  
  
 **Ytd** 함수는 수준을 기반으로 하는 특성 계층의 Type 속성이 *Years*로 설정 된 [PeriodsToDate](../mdx/periodstodate-mdx.md) 함수에 대 한 바로 가기 함수입니다. 즉, `Ytd(Member_Expression)`은 `PeriodsToDate(Year_Level_Expression,Member_Expression)`과 동일합니다. Type 속성이 *fiscalyears 유형의*로 설정 된 경우에는이 함수가 작동 하지 않습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 **놀이 Works** 큐브에서 `Date` 차원에 `Measures.[Order Quantity]` 포함 된 2003 년의 첫 8 개월 동안 집계 된 멤버의 합계를 반환 합니다.  
  
```  
WITH MEMBER [Date].[Calendar].[First8MonthsCY2003] AS  
    Aggregate(  
        YTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First8MonthsCY2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 **Ytd** 는 매개 변수를 지정 하지 않고 조합 하 여 자주 사용 됩니다. 즉, 다음 쿼리와 같이 [CURRENTMEMBER &#40;MDX&#41;](../mdx/currentmember-mdx.md) 함수는 보고서의 누적 연간 누계 누계를 표시 합니다.  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
