---
title: EXISTING 키워드 (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- EXISTING
helpviewer_keywords:
- Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a781fb58f45c478b6a3611132a210b14012ffb72
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228393"
---
# <a name="existing-keyword-mdx"></a>EXISTING 키워드(MDX)
  지정한 집합이 현재 컨텍스트 내에서 계산되도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 유효한 MDX 집합 식입니다.  
  
## <a name="remarks"></a>Remarks  
 기본적으로 집합은 집합의 멤버가 포함된 큐브의 컨텍스트 내에서 계산됩니다. `Existing` 키워드는 지정 된 집합이 현재 컨텍스트 내에서 대신 평가 강제로 수행 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 사용자가 선택한 State-Province 멤버에 대해 `Aggregate` 함수를 사용하여 계산한 값에 따라 이전 기간에 비해 판매량이 감소한 대리점의 수를 반환합니다. 그러나 [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx) 및 [DrilldownLevel(MDX)](/sql/mdx/drilldownlevel-mdx) 함수는 Product 차원의 제품 범주에 대해 판매량 감소 값을 반환하는 데 사용됩니다. 합니다 `Existing` 키워드는 집합을 `Filter` State-province 특성 계층의 Washington 및 Oregon 멤버에 대 한 현재 컨텍스트에서-즉, 실행할 함수입니다.  
  
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
 [Count &#40;설정&#41; &#40;MDX&#41;](/sql/mdx/count-set-mdx)   
 [AddCalculatedMembers &#40;MDX&#41;](/sql/mdx/addcalculatedmembers-mdx)   
 [집계 &#40;MDX&#41;](/sql/mdx/aggregate-mdx)   
 [필터 &#40;MDX&#41;](/sql/mdx/filter-mdx)   
 [속성 &#40;MDX&#41;](/sql/mdx/properties-mdx)   
 [DrilldownLevel &#40;MDX&#41;](/sql/mdx/drilldownlevel-mdx)   
 [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx)   
 [MDX 함수 참조 &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
