---
description: PeriodsToDate(MDX)
title: PeriodsToDate (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8b18fe4d90a8a0c56424c5e0a7f3607ceea0eae4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471705"
---
# <a name="periodstodate-mdx"></a>PeriodsToDate(MDX)


  지정한 멤버와 동일한 수준의 형제 멤버 집합을 반환합니다. 이 집합은 첫 번째 형제 멤버부터 시작하여 지정된 멤버에서 끝나며 Time 차원의 지정된 수준에 따라 제한됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PeriodsToDate( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>인수  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 지정 된 수준의 범위 내에서 **PeriodsToDate** 함수는 지정 된 멤버와 동일한 수준의 기간 집합을 반환 합니다 .이 값은 첫 번째 기간에서 시작 하 여 지정한 멤버로 끝납니다.  
  
-   수준이 지정 된 경우 계층의 현재 멤버는 *hierarchy 계층*으로 유추 됩니다. **Currentmember**. 여기서 *hierarchy*는 지정 된 수준의 계층입니다.  
  
-   수준이나 멤버가 지정되지 않은 경우 수준은 측정값 그룹에서 Time 유형의 첫 번째 차원에 있는 첫 번째 계층의 현재 멤버의 부모 수준입니다.  
  
 `PeriodsToDate( Level_Expression, Member_Expression )`은 다음 MDX 식과 기능상 동일합니다.  
  
 `TopCount(Descendants(Ancestor(Member_Expression, Level_Expression), Member_Expression.Level), 1):Member_Expression`  
  
## <a name="examples"></a>예제  
 다음 예에서는 `Measures.[Order Quantity]` `Date` **놀이 Works** 큐브에서 차원에 포함 된 2003 년의 첫 8 개월 동안 집계 된 멤버의 합계를 반환 합니다.  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 다음 예에서는 2003년 하반기 중 첫 2개월 동안의 데이터를 집계합니다.  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Semester],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>참고 항목  
 [TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
