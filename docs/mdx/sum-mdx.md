---
title: Sum (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: SUM
dev_langs: kbMDX
helpviewer_keywords: Sum function [MDX]
ms.assetid: 6c3db1e3-2c02-49f2-a0bf-cab0fb78c622
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 7a921a664db1dddb265e1cba632e8d688c7847d2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="sum-mdx"></a>Sum(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 집합에 대해 계산된 숫자 식의 합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Sum( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 유효한 MDX 집합 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 숫자 식이 지정된 경우 지정된 숫자 식이 집합에 대해 계산된 다음 합계가 계산됩니다. 숫자 식이 지정되지 않은 경우 지정된 집합은 해당 집합에 포함된 멤버의 현재 컨텍스트에서 계산된 다음 합계가 계산됩니다. SUM 함수를 숫자가 아닌 식에 적용하는 경우 결과가 정의되지 않습니다.  
  
> [!NOTE]  
>  Analysis Services는 숫자 집합의 합을 계산할 때 Null을 무시합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 2001년 및 2002년의 Product.Category 특성 계층에 대한 모든 멤버의 Reseller Sales Amount 합계를 반환합니다.  
  
```  
WITH MEMBER Measures.x AS SUM  
   ( { [Date].[Calendar Year].&[2001]  
         , [Date].[Calendar Year].&[2002] }  
      , [Measures].[Reseller Sales Amount]  
    )  
SELECT Measures.x ON 0  
,[Product].[Category].Members ON 1  
FROM [Adventure Works]  
```  
  
 다음 예에서는 2002년 7월 중 7월 20일까지의 일별 인터넷 판매 운송 비용의 합계를 반환합니다.  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 WITH MEMBER 키워드를 사용 하 고 **SUM** Geography 차원에 Country 특성 계층의 Canada 및 United States 멤버에 대 한 Reseller Sales Amount 측정값의 합계를 포함 하는 Measures 차원의 계산된 멤버를 정의 하는 함수입니다.  
  
```  
WITH MEMBER Measures.NorthAmerica AS SUM   
      (  
         {[Geography].[Country].&[Canada]  
            , [Geography].[Country].&[United States]}  
       ,[Measures].[Reseller Sales Amount]  
      )  
SELECT {[Measures].[NorthAmerica]} ON 0,  
[Product].[Category].members ON 1  
FROM [Adventure Works]  
```  
  
 대개는 **SUM** 함수는 함께 사용는 **CURRENTMEMBER** 함수 또는 함수 같은 **YTD** currentmember 계층 구조에 따라 달라 지는 집합을 반환 하는 합니다. 예를 들어, 다음 쿼리는 연도의 시작부터 행 축에 표시된 날짜까지 모든 날짜에 대한 Internet Sales Amount 측정값의 합계를 반환합니다.  
  
 `WITH MEMBER MEASURES.YTDSUM AS`  
  
 `SUM(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDSUM} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
