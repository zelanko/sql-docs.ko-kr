---
title: Qtd (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 182a86a05cd0dae6adf85d2168fe884ace910a82
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742592"
---
# <a name="qtd-mdx"></a>Qtd(MDX)


  첫 번째 형제 항목부터 지정 된 멤버에서 끝나며 하 여 제한 된 지정된 된 멤버와 같은 수준에서 멤버의 형제 집합을 반환 된 *분기* 시간 차원의 수준입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 경우 지정 되지 않은 멤버 expressionis, 기본값은 있으며 수준 유형이 인 첫 번째 계층의 현재 멤버 *분기* 유형의 첫 번째 차원에 *시간* 측정값 그룹에 있습니다.  
  
 **Qtd** 함수에 대 한 바로 가기 함수는는 [PeriodsToDate &#40;MDX&#41; ](../mdx/periodstodate-mdx.md) 함수는 수준 식 인수가 설정은 *분기*합니다. 즉, `Qtd(Member_Expression)`은 `PeriodsToDate(Quarter_Level_Expression, Member_Expression)`과 동일합니다.  
  
## <a name="example"></a>예제  
 합계를 반환 하는 다음 예제는 `Measures.[Order Quantity]` 멤버에 포함 된 2003 년 3 분기의 첫 2 개월에 걸쳐 집계는 `Date` 차원에서는 **Adventure Works** 큐브.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
