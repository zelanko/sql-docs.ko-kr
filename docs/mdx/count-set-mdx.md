---
title: "Count (집합) (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: COUNT
dev_langs: kbMDX
helpviewer_keywords: Count function [MDX]
ms.assetid: 22f530e9-f8e1-4608-affa-9a2bc0821591
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 21b41a98a21a9b3561358bf18c65ceb606facae0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="count-set-mdx"></a>Count(집합)(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>주의  
 **Count (집합)** 함수 포함 시키거나 사용 되는 구문에 따라 빈 셀을 제외 시킵니다. 빈 셀을 제외 또는 사용 하 여 포함 해야 표준 구문을 사용 하는 경우는 **EXCLUDEEMPTY** 또는 **INCLUDEEMPTY** 각각 플래그 지정 합니다. 대체 구문이 사용된 경우 이 함수는 항상 빈 셀을 포함시킵니다.  
  
 집합 카운트에서 빈 셀을 제외 하려면 표준 구문과 선택적인을 사용 하 여 **EXCLUDEEMPTY** 플래그입니다.  
  
> [!NOTE]  
>  **Count (집합)** 함수는 기본적으로 빈 셀을 계산 합니다. 반면,는 **개수** 집합 개수를 세는 OLE DB 함수는 기본적으로 빈 셀을 제외 시킵니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Product 차원에 있는 Model Name 특성 계층의 자식으로 구성된 멤버 집합의 셀 수를 계산합니다.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 사용 하 여 Product 차원의 제품 수를 계산 하는 다음 예제는 **DrilldownLevel** 와 함께에서 함수는 **Count** 함수입니다.  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 다음 예제에서는 반환 저조한 대리점을 사용 하 여 이전 분기에 비해 판매량 감소는 **Count** 와 함께에서 함수는 **필터** 함수 및 여러 다른 기능입니다. 이 쿼리에서 사용 하 여는 **집계** 클라이언트 응용 프로그램에서 드롭 다운 목록에서 선택할와 같은 여러 명의 지리적 멤버 선택을 지 원하는 함수입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [Count &#40; 차원 &#41; &#40; Mdx&#41;](../mdx/count-dimension-mdx.md)   
 [Count &#40; 계층 수준 &#41; &#40; Mdx&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Count &#40; 튜플 &#41; &#40; Mdx&#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel &#40; Mdx&#41;](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers &#40; Mdx&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Hierarchize &#40; Mdx&#41;](../mdx/hierarchize-mdx.md)   
 [속성 &#40; Mdx&#41;](../mdx/properties-mdx.md)   
 [집계 &#40; Mdx&#41;](../mdx/aggregate-mdx.md)   
 [필터 &#40; Mdx&#41;](../mdx/filter-mdx.md)   
 [PrevMember &#40; Mdx&#41;](../mdx/prevmember-mdx.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
