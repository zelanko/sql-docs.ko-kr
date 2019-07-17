---
title: Count (Set) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aac2f72cc8cd91e1964fd7734b858be8215cfdd8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047287"
---
# <a name="count-set-mdx"></a>Count(집합)(MDX)


  집합의 셀 개수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Standard syntax  
Count(Set_Expression [ , ( EXCLUDEEMPTY | INCLUDEEMPTY ) ] )  
  
Alternate syntax  
Set_Expression.Count  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 합니다 **Count (집합)** 함수를 포함 또는 사용 된 구문에 따라 빈 셀을 제외 합니다. 표준 구문이 사용 된 경우 빈 셀 수 포함 하거나 제외할 수를 사용 하 여 합니다 **EXCLUDEEMPTY** 또는 **INCLUDEEMPTY** 플래그입니다. 대체 구문이 사용된 경우 이 함수는 항상 빈 셀을 포함시킵니다.  
  
 집합 카운트에서 빈 셀을 제외 하려면 표준 구문과 선택적을 사용 하 여 **EXCLUDEEMPTY** 플래그입니다.  
  
> [!NOTE]  
>  합니다 **Count (집합)** 함수는 기본적으로 빈 셀을 계산 합니다. 반면, 합니다 **수** 집합 개수를 세는 OLE DB의 함수는 기본적으로 빈 셀을 제외 시킵니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Product 차원에 있는 Model Name 특성 계층의 자식으로 구성된 멤버 집합의 셀 수를 계산합니다.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 다음 예제에서는 사용 하 여 Product 차원의 제품 수를 계산 합니다 **DrilldownLevel** 함수를 함께 합니다 **개수** 함수.  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 다음 예제를 사용 하 여 이전 분기에 비해 보다 판매량이 저조한 대리점을 반환 합니다 **개수** 함수를 함께 **필터** 함수와 다른 많은 함수입니다. 이 쿼리에서 **집계** 함수에 같은 클라이언트 응용 프로그램의 드롭다운 목록에서 선택할 여러 개의 지리적 멤버를 선택을 지원 합니다.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
   (Filter  
      (Existing(Reseller.Reseller.Reseller),  
         [Measures].[Reseller Sales Amount]   
         < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
      )  
   )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate  
   ( {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
   )  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})  
      })  
   ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,  
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
   ,[Measures].[Declining Reseller Sales])  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [Count &#40;차원&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [Count &#40;계층 구조 수준&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Count &#40;튜플&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel&#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers&#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Hierarchize&#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [속성&#40;MDX&#41;](../mdx/properties-mdx.md)   
 [집계&#40;MDX&#41;](../mdx/aggregate-mdx.md)   
 [필터&#40;MDX&#41;](../mdx/filter-mdx.md)   
 [PrevMember&#40;MDX&#41;](../mdx/prevmember-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
