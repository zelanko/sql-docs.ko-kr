---
title: "필터 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: filter
dev_langs: kbMDX
helpviewer_keywords: Filter function
ms.assetid: f2df51c8-6acb-4300-b71c-2a480c9fbdf8
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: b106f1777996821a808d68a2d389161db70ce872
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="filter-mdx"></a>Filter(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>주의  
 **필터** 함수는 지정 된 집합의 각 튜플에 대해 지정된 된 논리 식을 계산 합니다. 함수는 논리 식이 지정된 된 집합의 각 튜플로 구성 된 집합을 반환 **true**합니다. 튜플이 경우 **true**, 빈 집합이 반환 됩니다.  
  
 **필터** 와 비슷한 방식으로 작동 하는 함수는 [IIf](../mdx/iif-mdx.md) 함수입니다. **IIf** 함수는 두 가지 옵션 중 하나만 반환 하는 동안 MDX 논리 식의 평가에 따라는 **필터** 함수는 지정 된 검색 조건에 맞는 튜플 집합을 반환 합니다. 실제로 **필터** 함수 실행 `IIf(Logical_Expression, Set_Expression.Current, NULL)` 집합과 반환의 각 튜플에 해당 결과 집합입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Internet Sales Amount가 $10000보다 큰 Dates만 반환하기 위해 쿼리의 Rows 축에서 Filter 함수를 사용하는 방법을 보여 줍니다.  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 또한 Filter 함수를 계산 멤버 정의 내에서 사용할 수 있습니다. 합계를 반환 하는 다음 예제에서는 `Measures.[Order Quantity]` 멤버에 포함 된 2003의 첫 9 개월 동안 집계는 `Date` 차원에서의 **Adventure Works** 큐브. **PeriodsToDate** 함수는 집합의 튜플을 정의 **집계** 함수 작동 합니다. **필터** 함수는 이전 기간에 대 한 Reseller Sales Amount 측정값에 대 한 값이 낮을수록 있는 사용자에 게 반환 되는 튜플을 제한 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
