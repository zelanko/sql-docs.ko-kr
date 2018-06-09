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
manager: kfile
ms.openlocfilehash: fa8edcf8af510a41affdcbcc9924edf69cf4c220
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743222"
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
  
 *개수*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 숫자 식이 지정 되는 **TopCount** 내림차순으로 지정된 된 집합에 대해 계산 된 숫자 식으로 지정 된 값에 따라 지정 된 집합으로 지정 된 집합의 튜플을 정렬 작동 합니다. 집합을 정렬 한 후의 **TopCount** 함수는 가장 높은 값을 갖는 튜플에의 지정 된 수를 반환 합니다.  
  
> [!IMPORTANT]  
>  마찬가지로 [BottomCount](../mdx/bottomcount-mdx.md) 함수는 **TopCount** 함수 계층을 항상 무시 합니다.  
  
 숫자 식이 지정 하지 않으면 함수는 멤버 집합 일반적인 순서로 정렬 하지 않고 반환, 처럼 동작 하는 [Head (MDX)](../mdx/head-mdx.md) 함수입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
