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
manager: kfile
ms.openlocfilehash: 67df625611f2451c3442d5d59b56c76dfc14a74a
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743862"
---
# <a name="ytd-mdx"></a>Ytd(MDX)


  첫 번째 형제 항목부터 지정 된 멤버에서 끝나며 하 여 제한 된 지정된 된 멤버와 같은 수준에서 멤버의 형제 집합을 반환 된 *연도* 시간 차원의 수준입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 기본값은 있으며 수준 유형이 인 첫 번째 계층의 현재 멤버 멤버 식이 지정 되지 않은 경우 *년* 유형의 첫 번째 차원에 *시간* 측정값 그룹에 있습니다.  
  
 **Ytd** 함수에 대 한 바로 가기 함수는는 [PeriodsToDate](../mdx/periodstodate-mdx.md) 함수에는 수준 기반이 되는 특성 계층의 Type 속성이 설정 되어 있는 *년*합니다. 즉, `Ytd(Member_Expression)`은 `PeriodsToDate(Year_Level_Expression,Member_Expression)`과 동일합니다. Type 속성 설정 된 경우에이 기능이 작동 하지 것입니다는 *FiscalYears*합니다.  
  
## <a name="example"></a>예제  
 합계를 반환 하는 다음 예제에서는 `Measures.[Order Quantity]` 멤버에 포함 된 2003 년의 첫 8 개월 동안 집계는 `Date` 차원에서의 **Adventure Works** 큐브.  
  
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
  
 **Ytd** 매개 변수 없이 지정 된, 즉 조합에서 자주 사용 된 [CurrentMember &#40;MDX&#41; ](../mdx/currentmember-mdx.md) 에 표시 된 대로 함수가 보고서에서 연도-날짜까지 누적 합계 표시 됩니다는 다음 쿼리:  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
