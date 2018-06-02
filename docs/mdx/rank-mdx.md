---
title: Rank (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ac8b41545063caa123eb678e5b2b0bda3b3a1e09
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580995"
---
# <a name="rank-mdx"></a>Rank(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 집합에 있는 지정한 튜플의 순위(1부터 시작)를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Rank(Tuple_Expression, Set_Expression [ ,Numeric Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Tuple_Expression*  
 튜플을 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 숫자 식이 지정 되는 **순위** 함수 튜플에 대해 지정된 된 숫자 식을 계산 하 여 1부터 지정 된 튜플 순위를 결정 합니다. 숫자 식이 지정 되는 **순위** 함수를 집합에 중복 값을 갖는 튜플에 같은 순위를 할당 합니다. 중복 값에 이렇게 같은 순위를 할당하면 집합의 이후 튜플 순위에 영향을 줍니다. 예를 들어 `{(a,b), (e,f), (c,d)}`와 같은 튜플로 구성된 집합을 고려해 보십시오. 튜플 `(a,b)`는 튜플 `(c,d)`와 값이 동일합니다. 튜플 `(a,b)`의 순위가 1이면 `(a,b)`와 `(c,d)` 모두 순위가 1이 됩니다. 하지만 튜플 `(e,f)`는 순위가 3이 됩니다. 이 집합에서는 순위가 2인 튜플이 있을 수 없습니다.  
  
 숫자 식이 지정 하지 않으면는 **순위** 함수는 지정 된 튜플의 순서 위치 1부터 반환 합니다.  
  
 **순위** 함수 집합 순서를 지정 하지 않습니다.  
  
## <a name="example"></a>예제  
 사용 하 여 고객과 구입 날짜가 들어 있는 튜플 집합을 반환 하는 다음 예제는 **필터**, **NonEmpty**, **항목**, 및 **순위** 마지막 날짜를 찾고 각 고객이 제품을 구매 하는 함수입니다.  
  
```  
WITH SET MYROWS AS FILTER  
   (NONEMPTY  
      ([Customer].[Customer Geography].MEMBERS  
         * [Date].[Date].[Date].MEMBERS  
         , [Measures].[Internet Sales Amount]  
      ) AS MYSET  
   , NOT(MYSET.CURRENT.ITEM(0)  
      IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))  
   )  
SELECT [Measures].[Internet Sales Amount] ON 0,  
MYROWS ON 1  
FROM [Adventure Works]  
```  
  
 다음 예제에서는 **순서** 함수 보다는 **순위** 함수 City 계층의 멤버 순위를 Reseller Sales Amount 측정값에 따라 한 순위에 표시 합니다. 사용 하 여는 **순서** City 계층의 멤버 집합 함수를 첫 번째, 한 번만 수행 되며 정렬 된 순서 대로 결과가 표시 되기 전에 선형 검색이 그런 다음 정렬 합니다.  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [주문 &#40;MDX&#41;](../mdx/order-mdx.md)   
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
