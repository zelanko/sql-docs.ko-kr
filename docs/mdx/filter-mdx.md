---
title: 필터 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3a70bceed4cdccf6a22f0cfea4e5093634f88f1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132687"
---
# <a name="filter-mdx"></a>Filter(MDX)


  검색 조건을 기준으로 지정한 집합을 필터링한 결과 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Filter(Set_Expression, Logical_Expression )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Logical_Expression*  
 true나 false가 되는 유효한 MDX 논리 식입니다.  
  
## <a name="remarks"></a>설명  
 합니다 **필터** 함수는 지정 된 집합의 각 튜플에 대해 지정 된 논리 식을 계산 합니다. 논리 식으로 계산 되는 위치 지정된 된 집합의 각 튜플로 구성 된 집합을 반환 **true**합니다. 경우 튜플이 **true**, 빈 집합이 반환 됩니다.  
  
 합니다 **필터** 함수는 유사한 방식으로 작동 합니다 [IIf](../mdx/iif-mdx.md) 함수입니다. **IIf** 두 가지 옵션 중 하나만 반환 하는 동안 MDX 논리 식의 평가 따라 합니다 **필터** 함수에 지정 된 검색 조건을 충족 하는 튜플 집합을 반환 합니다. 실제로 **필터** 함수를 실행 `IIf(Logical_Expression, Set_Expression.Current, NULL)` 반환 고 집합의 각 튜플에에서 해당 결과 집합입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Internet Sales Amount가 $10000보다 큰 Dates만 반환하기 위해 쿼리의 Rows 축에서 Filter 함수를 사용하는 방법을 보여 줍니다.  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 또한 Filter 함수를 계산 멤버 정의 내에서 사용할 수 있습니다. 합계를 반환 하는 다음 예제에서는 합니다 `Measures.[Order Quantity]` 에 포함 된 2003 년의 첫 9 개월 동안 집계 된 멤버를 `Date` 차원에서는 **Adventure Works** 큐브. 합니다 **PeriodsToDate** 함수는 집합의 튜플을 정의 합니다 **집계** 함수 작동 합니다. 합니다 **필터** 함수에는 이전 기간에 대 한 Reseller Sales Amount 측정값에 대 한 낮은 값으로 반환 되는 튜플을 제한 합니다.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
