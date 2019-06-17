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
manager: kfile
ms.openlocfilehash: 43a75f4a42193c231c1acc710512b05537675991
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63277852"
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
  
## <a name="remarks"></a>Remarks  
 **순서** 함수 계층적 일 수 있습니다 (사용 하 여 지정 된 대로 합니다 **ASC** 또는 **DESC** 플래그) 비계층적일 또는 (사용 하 여 지정 된 대로 **BASC**  또는 **BDESC** 플래그를 **B** "break 계층"는 의미). 하는 경우 **ASC** 또는 **DESC** 를 지정 합니다 **순서** 함수는 먼저 계층의 해당 위치에 따라 멤버를 정렬 하 고 다음 각 수준을 정렬 합니다. 경우 **BASC** 또는 **BDESC** 를 지정 합니다 **순서** 함수는 계층과 관계 없이 집합에서 멤버를 정렬 합니다. 플래그가 지정 경우 **ASC** 가 기본값입니다.  
  
 경우는 **순서** 함수는 집합을 사용 하 여 둘 이상의 계층이 크로스 조인 되 고 **DESC** 플래그를 사용 하는 집합의 마지막 계층의 멤버만 정렬 됩니다. 이 사항은 집합에 있는 모든 계층이 정렬되는 Analysis Services 2000에서 변경되었습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 반환에서 합니다 **Adventure Works** 큐브에 Date 차원의 Calendar 계층의 모든 Calendar Quarters에 대 한 대리점 주문 수입니다. 합니다 **순서** 함수 ROWS 축에 대 한 집합을 다시 정렬 합니다. 합니다 **순서** 함수에서 집합을 정렬 `[Reseller Order Count]` 기준으로 계층적 순서를 내림차순는 `[Calendar]` 계층.  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 알림 방법을이 예제에서는 때 합니다 **DESC** 플래그 변경 됩니다 **BDESC**는 계층이 끊어지고 계층에 관계 없이 Calendar Quarters 목록이 반환 됩니다:  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 다음 예에서는 Reseller Gross Profit를 기준으로 계층에 관계없이 판매량이 상위 5위 안에 속하는 제품 하위 범주에 대한 Reseller Sales 측정값을 반환합니다. 합니다 **하위 집합** 함수를 사용 하 여 결과 정렬 한 후 집합에서 처음 5 개의 튜플만 반환 되는 **순서** 함수입니다.  
  
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
  
 다음 예제에서는 합니다 **순위** 함수 City 계층의 멤버 순위를 Reseller Sales Amount 측정값을 기반으로 하 고 순위 순서로 표시 합니다. 사용 하 여 합니다 **순서** City 계층의 멤버 집합 함수를 첫 번째, 한 번만 수행 되며 순서 대로 정렬 된 결과가 표시 되기 전에 선형 검색이 다음 정렬 합니다.  
  
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
  
 다음 예제에서는 고유한를 사용 하 여 집합의 제품 수를 반환 합니다.는 **순서** 함수를 활용 하기 전에 비어 있지 않은 튜플을 정렬 한를 **필터** 함수입니다. 합니다 **CurrentOrdinal** 함수 비교 하 고 ties 제거를 사용 합니다.  
  
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
  
 알아야 하는 방법을 **DESC** 튜플 집합을 사용 하 여 작동 플래그, 먼저 다음 쿼리의 결과 것이 좋습니다.  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 Rows 축에서 내림차순으로 Tax Amount를 다음과 같이 Sales Territory Groups가 주문 있는지 확인할 수 있습니다. North America, Europe, Pacific, 미정으로 나타납니다. 이제 참조 하는 경우 어떻게 되나요에서는 Sales Territory Groups 집합 제품 하위 범주 집합과 크로스 조인 적용 합니다 **순서** 다음과 같은 방법으로 함수:  
  
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
  
 하지만 Product Subcategories 집합 내림차순의 계층 순서로 정렬 되었지만 Sales Territory Groups는 이제 정렬 되지 및 계층에 나타나는 순서로 표시: Europe, NA, North America 및 Pacific입니다. 이유는 튜플 집합의 마지막 계층인 Product Subcategories만 정렬되기 때문입니다. Analysis Services 2000의 동작을 재현 하려면는 일련의 중첩 **생성** 크로스 조인 하기 전에, 예를 들어 각 집합을 정렬 하는 함수:  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
