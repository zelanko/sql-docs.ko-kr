---
title: ClosingPeriod (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3d082ec7958ab1b29b5b42108d6f9c5c78fc3470
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577365"
---
# <a name="closingperiod-mdx"></a>ClosingPeriod(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정된 수준에서 지정된 멤버의 하위 항목 중 마지막 형제 항목인 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ClosingPeriod( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>인수  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 이 함수는 주로 Time 형식의 차원에 대해 사용되지만 모든 차원에 대해 사용할 수도 있습니다.  
  
-   수준 식이 지정 되는 **ClosingPeriod** 함수는 지정 된 수준을 포함 하 고 지정된 된 수준에서 기본 멤버의 하위 항목 중 마지막 형제 항목을 반환 하는 차원을 사용 하 여 합니다.  
  
-   수준 식과 멤버 식이 모두 지정 된 경우는 **ClosingPeriod** 함수는 지정 된 수준에서 지정 된 멤버의 하위 항목 중 마지막 형제 항목을 반환 합니다.  
  
-   수준 식과 멤버 식이 모두 지정 하는 경우는 **ClosingPeriod** 함수 사용 하 여 기본 수준 및 차원 멤버 (있는 경우) 해당 큐브에 있는 Time 형식입니다.  
  
 **ClosingPeriod** 함수는 다음과 같은 MDX 문과 동일 합니다.  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`을 참조하세요.  
  
> [!NOTE]  
>  [OpeningPeriod](../mdx/openingperiod-mdx.md) 함수는 비슷합니다는 **ClosingPeriod** 함수와 **OpeningPeriod** 함수는 마지막 형제 대신 첫 번째 형제를 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 의미적으로 Time 형식인 Date 차원의 FY2007 멤버에 대한 기본 측정값의 값을 반환합니다. Fiscal Year 수준이 [All] 수준의 첫 번째 하위 항목이고, Fiscal 계층이 계층 컬렉션의 첫 번째 사용자 정의 계층이라서 해당 계층이 기본 계층이며, FY 2007 멤버가 이 계층에서 이 수준의 마지막 형제이므로 이 멤버가 반환됩니다.  
  
```  
SELECT ClosingPeriod() ON 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 Date.Date 특성 계층의 Date.Date.Date 수준에서 November 30, 2006 멤버의 기본 측정값에 대한 값을 반환합니다. 이 멤버는 Date.Date 특성 계층에서 [All] 수준의 하위 항목에 대한 마지막 형제입니다.  
  
```  
SELECT ClosingPeriod ([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 December, 2003 멤버의 기본 측정값에 대한 값을 반환합니다. 이 멤버는 Calendar 사용자 정의 계층의 Year 수준에서 2003 멤버의 하위 항목에 대한 마지막 형제입니다.  
  
```  
SELECT ClosingPeriod ([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 June, 2003 멤버의 기본 측정값에 대한 값을 반환합니다. 이 멤버는 Fiscal 사용자 정의 계층의 Year 수준에서 2003 멤버의 하위 항목에 대한 마지막 형제입니다.  
  
```  
SELECT ClosingPeriod ([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [OpeningPeriod &#40;MDX&#41;](../mdx/openingperiod-mdx.md)   
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling &#40;MDX&#41;](../mdx/lastsibling-mdx.md)  
  
  
