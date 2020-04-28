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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
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
 **Count (Set)** 함수는 사용 된 구문에 따라 빈 셀을 포함 하거나 제외 합니다. 표준 구문을 사용 하는 경우에는 각각 **excludeempty** 또는 **includeempty** 플래그를 사용 하 여 빈 셀을 제외 하거나 포함할 수 있습니다. 대체 구문이 사용된 경우 이 함수는 항상 빈 셀을 포함시킵니다.  
  
 집합 개수에서 빈 셀을 제외 하려면 표준 구문과 선택적 **Excludeempty** 플래그를 사용 합니다.  
  
> [!NOTE]  
>  **Count (Set)** 함수는 기본적으로 빈 셀을 계산 합니다. 반면 집합을 계산 하는 OLE DB의 **Count** 함수는 기본적으로 빈 셀을 제외 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Product 차원에 있는 Model Name 특성 계층의 자식으로 구성된 멤버 집합의 셀 수를 계산합니다.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 **Count** 함수와 함께 **DrilldownLevel** 함수를 사용 하 여 Product 차원의 제품 수를 계산 합니다.  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 다음 예에서는 **Count** 함수를 **필터** 함수와 함께 사용 하 고 다른 여러 함수를 사용 하 여 이전 분기와 비교한 판매를 거부 하는 대리점을 반환 합니다. 이 쿼리에서는 **집계** 함수를 사용 하 여 클라이언트 응용 프로그램의 드롭다운 목록에서 선택과 같은 여러 지리 멤버의 선택을 지원 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [MDX&#41; &#40;&#40;차원 수&#41;](../mdx/count-dimension-mdx.md)   
 [MDX&#41; &#40;&#40;계층 수준 수&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [MDX&#41; &#40;&#40;수&#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [MDX &#40;속성&#41;](../mdx/properties-mdx.md)   
 [MDX &#40;집계&#41;](../mdx/aggregate-mdx.md)   
 [MDX &#40;필터&#41;](../mdx/filter-mdx.md)   
 [PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
