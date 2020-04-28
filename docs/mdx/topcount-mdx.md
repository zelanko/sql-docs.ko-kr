---
title: TopCount (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0f607f3111c150bff3d5dc562c77901a381bedc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036605"
---
# <a name="topcount-mdx"></a>TopCount(MDX)


  집합을 내림차순으로 정렬하고 가장 높은 값을 갖는 요소를 지정된 수만큼 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
TopCount(Set_Expression,Count [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Count*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 숫자 식이 지정 된 경우 **TopCount** 함수는 지정 된 집합에 대해 계산 된 대로 숫자 식으로 지정 된 값에 따라 지정 된 집합의 튜플을 내림차순으로 정렬 합니다. 집합을 정렬 한 후 **TopCount** 함수는 값이 가장 높은 지정 된 수의 튜플을 반환 합니다.  
  
> [!IMPORTANT]  
>  [BottomCount](../mdx/bottomcount-mdx.md) 함수와 마찬가지로 **TopCount** 함수는 항상 계층 구조를 중단 합니다.  
  
 숫자 식이 지정 되지 않은 경우이 함수는 멤버 집합을 정렬 하지 않고 일반적인 순서로 반환 합니다. [Head (MDX)](../mdx/head-mdx.md) 함수 처럼 동작 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Internet Sales Amount를 기준으로 상위 10개 날짜를 반환합니다.  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `TOPCOUNT([Date].[Date].[Date].MEMBERS, 10, [Measures].[Internet Sales Amount])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 다음 예에서는 Bike 범주에 대해 Geography 차원의 Geography 계층에 있는 City 수준의 멤버와 Date 차원의 Fiscal 계층에 있는 모든 회계 연도의 모든 조합을 포함하는 집합을 Reseller Sales Amount 측정값을 기준으로 판매량이 가장 많은 멤버부터 정렬한 다음 이 중 처음 5개의 멤버를 반환합니다.  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopCount  
   ({[Geography].[Geography].[City].Members   
      *[Date].[Fiscal].[Fiscal Year].Members}  
   , 5  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
