---
description: PrevMember(MDX)
title: PrevMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6f02dfca925fce4399bb9f0c4a8c7ff1e005e598
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471665"
---
# <a name="prevmember-mdx"></a>PrevMember(MDX)


  지정한 멤버를 포함하고 있는 수준에서 이전 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.PrevMember   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **PrevMember** 함수는 지정 된 멤버와 같은 수준의 이전 멤버를 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 **PrevMember** 함수를 사용 하 여 rows 축에서 현재 멤버 바로 앞에 멤버 이름을 표시 하는 간단한 쿼리를 보여 줍니다.  
  
 `WITH MEMBER MEASURES.PREVMEMBERDEMO AS`  
  
 `[Date].[Calendar].CURRENTMEMBER.PREVMEMBER.NAME`  
  
 `SELECT MEASURES.PREVMEMBERDEMO ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 다음 예에서는 사용자가 선택한 State-Province 멤버에 대해 Aggregate 함수를 사용하여 계산한 값에 따라 이전 기간에 비해 판매량이 감소한 대리점의 수를 반환합니다. **Hierarchize** 및 **DrillDownLevel** 함수는 product 차원의 제품 범주에 대 한 판매량 감소 값을 반환 하는 데 사용 됩니다. **PrevMember** 함수는 현재 기간의 이전 기간을 비교 하는 데 사용 됩니다.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS   
   Count(  
      Filter(  
         Existing(Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
            )  
         )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate (   
      {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
         )  
SELECT NON EMPTY Hierarchize (  
   AddCalculatedMembers (  
      {DrillDownLevel({[Product].[All Products]})}  
         )  
   )  
        DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
    [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
    [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
