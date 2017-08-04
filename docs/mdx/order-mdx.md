---
title: Order (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ORDER
dev_langs:
- kbMDX
helpviewer_keywords:
- Order function
ms.assetid: 84acff52-2443-4424-a09e-694e6f14c109
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 98037f9c56523e05a1d3af44078bf8da51cd53e5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="order-mdx"></a>Order(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>주의  
 **순서** 함수 계층적 일 수 있습니다 (사용 하 여 지정 된 대로 **ASC** 또는 **DESC** 플래그) 비계층적 또는 (사용 하 여 지정 된 대로 **BASC** 또는 **BDESC** 플래그는 **B** "break hierarchy"에). 경우 **ASC** 또는 **DESC** 지정는 **순서** 함수 먼저 계층에서의 위치에 따라 멤버를 정렬 하 고 다음 각 수준을 정렬 합니다. 경우 **BASC** 또는 **BDESC** 지정는 **순서** 함수는 계층과 관계 없이 집합에서 멤버를 정렬 합니다. 플래그가 지정 경우 **ASC** 값이 기본값입니다.  
  
 경우는 **순서** 함수에 사용 되는 설정 된 둘 이상의 계층이 크로스 조인 및 **DESC** 플래그가 사용 된 집합에 있는 마지막 계층의 구성원만 정렬 됩니다. 이 사항은 집합에 있는 모든 계층이 정렬되는 Analysis Services 2000에서 변경되었습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 반환에서 **Adventure Works** 큐브에 한 Date 차원에 있는 Calendar 계층 구조의 모든 Calendar Quarters에 대 한 대리점 주문 건수 합니다. **순서** 함수는 ROWS 축에 대 한 집합을 다시 정렬 합니다. **순서** 함수에서 집합을 정렬 `[Reseller Order Count]` 내림차순 계층 순서로에서 결정 된 대로 `[Calendar]` 계층입니다.  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 공지가 예제에서는 방법 때는 **DESC** 플래그도 변경 된 **BDESC**, 계층이 및 계층 구조에 관계 없이 Calendar Quarters 목록이 반환 됩니다:  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 다음 예에서는 Reseller Gross Profit를 기준으로 계층에 관계없이 판매량이 상위 5위 안에 속하는 제품 하위 범주에 대한 Reseller Sales 측정값을 반환합니다. **하위 집합** 함수를 사용 하 여 사용 하 여 결과 정렬 한 후 집합의 처음 5 개의 튜플만를 반환 하는 **순서** 함수입니다.  
  
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
  
 다음 예제에서는 **순위** 함수 City 계층의 멤버 순위를 Reseller Sales Amount 측정값을 기반으로 하며 순위에 표시 합니다. 사용 하 여는 **순서** City 계층의 멤버 집합 함수를 첫 번째, 한 번만 수행 되며 정렬 된 순서 대로 결과가 표시 되기 전에 선형 검색이 그런 다음 정렬 합니다.  
  
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
  
 사용 하 여 고유한 집합에 제품의 수를 반환 하는 다음 예제는 **순서** 이용 하기 전에 먼저 비어 있지 않은 튜플을 정렬 하는 함수는 **필터** 함수입니다. **CurrentOrdinal** 함수를 비교 하 고 동률 제거를 사용 합니다.  
  
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
  
 이해 하는 방법을 **DESC** 튜플 집합으로 작동 하는 플래그입니다. 먼저 다음 쿼리의 결과 고려 하십시오.  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 Rows 축에서 볼 수 있습니다 내림차순으로 세 액 다음과 같이 Sales Territory Groups 정렬 되어 있는지: 북미, 유럽, Pacific, 미정으로 나타납니다. 지금은 참조 하는 경우 어떤 일이 생기 म Sales Territory groups 집합을 제품 하위 범주 집합과 크로스 조인 하 고 적용는 **순서** 함수를 동일한 방법으로, 다음과 같이:  
  
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
  
 Sales Territory Groups 이제 정렬 되지 않고 및 계층에 나타나는 순서로 표시 내림차순, 계층적 순서로 정렬 되는 집합을 제품 하위 범주, 동안: Europe, NA, North America 및 Pacific입니다. 이유는 튜플 집합의 마지막 계층인 Product Subcategories만 정렬되기 때문입니다. Analysis Services 2000의 동작을 재현 하려면는 일련의 중첩 **생성** 크로스 조인 하기 전에, 예를 들어 각 집합을 정렬 하는 기능:  
  
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
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

