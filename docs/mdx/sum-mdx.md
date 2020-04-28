---
title: 합계 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb4e9d55ef2228404dd9113170066e4a3612a0a1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036668"
---
# <a name="sum-mdx"></a>Sum(MDX)


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
  
## <a name="remarks"></a>설명  
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
  
 다음 예에서는 WITH MEMBER 키워드와 **SUM** 함수를 사용 하 여 Geography 차원에 있는 Country 특성 계층의 캐나다 및 미국 구성원에 대 한 재판매인 Sales Amount 측정값의 합계를 포함 하는 측정값 차원의 계산 멤버를 정의 합니다.  
  
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
  
 **합계** 함수는 **currentmember&lt** 함수 또는 계층의 currentmember&lt에 따라 달라 지는 집합을 반환 하는 **YTD** 와 같은 함수와 함께 사용 되는 경우가 많습니다. 예를 들어, 다음 쿼리는 연도의 시작부터 행 축에 표시된 날짜까지 모든 날짜에 대한 Internet Sales Amount 측정값의 합계를 반환합니다.  
  
 `WITH MEMBER MEASURES.YTDSUM AS`  
  
 `SUM(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDSUM} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
