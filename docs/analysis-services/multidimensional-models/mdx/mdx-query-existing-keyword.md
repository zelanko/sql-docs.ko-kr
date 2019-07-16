---
title: EXISTING 키워드 (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d41b49e4585d2a256250a009b09ffa9ed94ea925
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208728"
---
# <a name="mdx-query---existing-keyword"></a>MDX 쿼리 - EXISTING 키워드
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  지정한 집합이 현재 컨텍스트 내에서 계산되도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 유효한 MDX 집합 식입니다.  
  
## <a name="remarks"></a>설명  
 기본적으로 집합은 집합의 멤버가 포함된 큐브의 컨텍스트 내에서 계산됩니다. 그러나 **Existing** 키워드는 지정된 집합이 현재 컨텍스트 내에서 계산되도록 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 사용자가 선택한 State-Province 멤버에 대해 **Aggregate** 함수를 사용하여 계산한 값에 따라 이전 기간에 비해 판매량이 감소한 대리점의 개수를 반환합니다. 그러나 [Hierarchize&#40;MDX&#41;](../../../mdx/hierarchize-mdx.md) 및 [DrilldownLevel(MDX)](../../../mdx/drilldownlevel-mdx.md) 함수는 Product 차원의 제품 범주에 대해 판매량 감소 값을 반환하는 데 사용됩니다. 합니다 **기존** 키워드의 집합을 강제로 합니다 **필터** State-province 특성 계층의 Washington 및 Oregon 멤버에 대 한 현재 컨텍스트에서-즉, 실행할 함수입니다.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
      (Filter  
         (Existing  
            (Reseller.Reseller.Reseller)  
         , [Measures].[Reseller Sales Amount] <   
            ([Measures].[Reseller Sales Amount]  
               ,[Date].Calendar.PrevMember  
            )  
        )  
      )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate   
      ( {[Geography].[State-Province].&[WA]&[US]  
         , [Geography].[State-Province].&[OR]&[US] }   
      )  
SELECT NON EMPTY HIERARCHIZE   
      (AddCalculatedMembers   
         (   
            {DrillDownLevel  
               ({[Product].[All Products]}  
               )  
            }   
         )   
      ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE   
      ( [Geography].[State-Province].x  
        , [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
        ,[Measures].[Declining Reseller Sales]  
      )  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [개수&#40;Set&#41;&#40;MDX&#41;](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers&#40;MDX&#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [집계&#40;MDX&#41;](../../../mdx/aggregate-mdx.md)   
 [필터&#40;MDX&#41;](../../../mdx/filter-mdx.md)   
 [속성&#40;MDX&#41;](../../../mdx/properties-mdx.md)   
 [DrilldownLevel&#40;MDX&#41;](../../../mdx/drilldownlevel-mdx.md)   
 [Hierarchize&#40;MDX&#41;](../../../mdx/hierarchize-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
