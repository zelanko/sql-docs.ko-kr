---
description: Qtd(MDX)
title: Qtd (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea3bd80fa85d95dd3adf52793d5895425b40b9fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500456"
---
# <a name="qtd-mdx"></a>Qtd(MDX)


  지정 된 멤버와 동일한 수준의 형제 멤버 집합을 반환 합니다 .이 집합은 첫 번째 형제부터 시작 하 여 지정 된 멤버로 끝나는 시간 차원의 *Quarter* 수준에 따라 제한 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 Expressionis를 지정 하지 않은 경우 기본값은 측정값 그룹에서 *Time* 유형의 첫 번째 차원에서 *분기* 형식의 수준을 가진 첫 번째 계층의 현재 멤버입니다.  
  
 **Qtd** 함수는 수준 식 인수가 *Quarter*로 설정 된 [PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md) 함수에 대 한 바로 가기 함수입니다. 즉, `Qtd(Member_Expression)`은 `PeriodsToDate(Quarter_Level_Expression, Member_Expression)`과 동일합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `Measures.[Order Quantity]` `Date` **놀이 Works** 큐브에서 차원에 포함 되어 있는 2003 년 3 분기의 처음 2 개월 동안 집계 된 멤버의 합계를 반환 합니다.  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        QTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
