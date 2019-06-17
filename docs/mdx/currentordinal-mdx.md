---
title: CurrentOrdinal (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d6fe956591b6bde0c5e6b074115fec8724995a59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248189"
---
# <a name="currentordinal-mdx"></a>CurrentOrdinal(MDX)


  반복하는 동안 집합 내의 현재 반복 번호를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set_Expression.CurrentOrdinal  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 와 같은 집합을 통해 반복 하는 경우는 [Filter (MDX)](../mdx/filter-mdx.md) 또는 [Generate (MDX)](../mdx/generate-mdx.md) 함수를 **CurrentOrdinal** 함수의 반복 수를 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 간단한 예제에서는 어떻게 **CurrentOrdinal** 사용 될 수 있습니다 **생성** 집합의 위치로 함께 집합의 각 항목의 이름을 포함 하는 문자열을 반환 하려면:  
  
 `WITH SET MySet AS [Customer].[Customer Geography].[Country].MEMBERS`  
  
 `MEMBER MEASURES.CURRENTORDINALDEMO AS`  
  
 `GENERATE(MySet, CSTR(MySet.CURRENTORDINAL) + ") " + MySet.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTORDINALDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
 CurrentOrdinal은 매우 복잡한 계산에서만 일반적으로 사용됩니다. 다음 예제에서는 고유한를 사용 하 여 집합의 제품 수를 반환 합니다.는 **순서** 함수를 활용 하기 전에 비어 있지 않은 튜플을 정렬 한를 **필터** 함수입니다. 합니다 **CurrentOrdinal** 함수 비교 하 고 ties 제거를 사용 합니다.  
  
```  
WITH MEMBER [Measures].[PrdTies] AS Count  
   (Filter  
      (Order  
        (NonEmpty  
          ([Product].[Product].[Product].Members  
          , {[Measures].[Reseller Order Quantity]}  
          )  
       , [Measures].[Reseller Order Quantity]  
       , BDESC  
       ) AS OrdPrds  
    , NOT((OrdPrds.CurrentOrdinal < OrdPrds.Count   
       AND [Measures].[Reseller Order Quantity] =   
          ( [Measures].[Reseller Order Quantity]  
            , OrdPrds.Item  
               (OrdPrds.CurrentOrdinal  
               )  
            )  
         )  
         OR (OrdPrds.CurrentOrdinal > 1   
            AND [Measures].[Reseller Order Quantity] =   
               ([Measures].[Reseller Order Quantity]  
               , OrdPrds.Item  
                  (OrdPrds.CurrentOrdinal-2)  
                )  
             )  
          ))  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
