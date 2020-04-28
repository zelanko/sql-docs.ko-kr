---
title: Order (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d540b299fd08aa78576b19040a4cfafb9046ae7c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68055686"
---
# <a name="order-mdx"></a>Order(MDX)


  지정한 집합의 멤버를 정렬합니다. 계층을 유지하거나 바꿀 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Numeric expression syntax  
Order(Set_Expression, Numeric_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
String expression syntax  
Order(Set_Expression, String_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *String_Expression*  
 문자열로 표현된 숫자를 반환하는 셀 좌표의 유효한 문자열 식으로서, 일반적으로 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **Order** 함수는 계층적 일 수 있습니다 ( **ASC** 또는 **DESC** 플래그를 사용 하 여 지정한 대로) 또는 비계층적 인 ( **c** + + 또는 **Bdesc** 플래그를 사용 하 여 지정). **B** 는 "계층 중단"을 의미 합니다. **ASC** 또는 **DESC** 를 지정 하면 **Order** 함수는 먼저 계층에서 해당 위치에 따라 멤버를 정렬 한 다음 각 수준을 정렬 합니다. **Dec** 또는 **bdesc** 를 지정 하면 **Order** 함수는 계층에 관계 없이 집합의 멤버를 정렬 합니다. 플래그가 지정 되지 않은 경우에는 **ASC** 가 기본값입니다.  
  
 두 개 이상의 계층이 크로스 조인할 집합에 **Order** 함수를 사용 하 고 **DESC** 플래그를 사용 하는 경우 집합에서 마지막 계층의 멤버만 정렬 됩니다. 이 사항은 집합에 있는 모든 계층이 정렬되는 Analysis Services 2000에서 변경되었습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **놀이 Works** 큐브에서 Date 차원의 calendar 계층에 있는 모든 분기의 재판매인 주문 수를 반환 합니다. Order 함수는 ROWS 축에 대해 집합의 순서를 다시 **정렬** 합니다. **Order** 함수는 `[Calendar]` 계층에 의해 결정 `[Reseller Order Count]` 된 대로 내림차순 계층 순서로 집합을 정렬 합니다.  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 이 예에서는 **DESC** 플래그가 **bdesc**로 변경 될 때 계층이 중단 되 고 계층에 관계 없이 일정 사분기 목록이 반환 됩니다.  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 다음 예에서는 Reseller Gross Profit를 기준으로 계층에 관계없이 판매량이 상위 5위 안에 속하는 제품 하위 범주에 대한 Reseller Sales 측정값을 반환합니다. **하위 집합** 함수는 **Order** 함수를 사용 하 여 결과를 정렬 한 후 집합에서 처음 5 개의 튜플을 반환 하는 데 사용 됩니다.  
  
 `SELECT Subset`  
  
 `(Order`  
  
 `([Product].[Product Categories].[SubCategory].members`  
  
 `,[Measures].[Reseller Gross Profit]`  
  
 `,BDESC`  
  
 `)`  
  
 `,0`  
  
 `,5`  
  
 `) ON 0`  
  
 `FROM [Adventure Works]`  
  
 다음 예에서는 **Rank** 함수를 사용 하 여 재판매인 Sales Amount 측정값에 따라 City 계층의 멤버 순위를 지정한 다음 순위가 매겨진 순서로 표시 합니다. **Order** 함수를 사용 하 여 먼저 City 계층의 멤버 집합을 정렬 하면 정렬이 한 번만 수행 된 다음 정렬 된 순서로 표시 되기 전에 선형 검색이 수행 됩니다.  
  
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
  
 다음 예에서는 **Filter** 함수를 사용 하기 전에 **order** 함수를 사용 하 여 비어 있지 않은 튜플을 정렬 한 집합의 제품 수를 반환 합니다. **Currentordinal** 함수는 동률을 비교 하 고 제거 하는 데 사용 됩니다.  
  
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
    , (OrdPrds.CurrentOrdinal < OrdPrds.Count   
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
          )  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
 **DESC** 플래그가 튜플 집합에서 작동 하는 방식을 이해 하려면 먼저 다음 쿼리의 결과를 고려해 야 합니다.  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 행 축에서 판매 지역 그룹은 북아메리카, 유럽, 태평양, NA와 같이 내림차순으로 내림차순으로 정렬 된 것을 볼 수 있습니다. 이제 다음과 같이 제품 하위 범주 집합을 사용 하 여 영업 지역 그룹 집합을 crossjoin 하 고 동일한 방식으로 **주문** 함수를 적용 하는 경우 어떻게 되는지 확인할 수 있습니다.  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 제품 하위 범주 집합은 내림차순, 계층 순서로 정렬 되어 있지만 이제 판매 지역 그룹이 계층 구조에 표시 되는 순서 대로 표시 되지 않습니다. 유럽, NA, 북아메리카 및 태평양. 이유는 튜플 집합의 마지막 계층인 Product Subcategories만 정렬되기 때문입니다. Analysis Services 2000의 동작을 재현 하려면 일련의 중첩 된 **생성** 함수를 사용 하 여 각 집합을 크로스 조인할 전에 정렬 합니다. 예를 들면 다음과 같습니다.  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
GENERATE(  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
,  
ORDER(  
[Sales Territory].[Sales Territory].CURRENTMEMBER  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC))  
ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
