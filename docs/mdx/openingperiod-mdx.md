---
title: OpeningPeriod (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OPENINGPERIOD
dev_langs:
- kbMDX
helpviewer_keywords:
- OpeningPeriod function
ms.assetid: bebf55cf-e5c6-42b1-98f2-1d6e54093d4c
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 6f0ceb660009214e341c423261620d749e3ed1c6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="openingperiod-mdx"></a>OpeningPeriod(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 수준 또는 지정한 멤버의 하위 항목 중 첫 번째 형제를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
OpeningPeriod( [ Level_Expression [ , Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>인수  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 이 함수는 주로 Time 차원에 대해 사용되지만 모든 차원에 대해 사용할 수도 있습니다.  
  
-   수준 식이 지정 되는 **OpeningPeriod** 함수는 지정된 된 수준을 포함 하 고 지정된 된 수준에서 기본 멤버의 하위 항목 중 첫 번째 형제를 반환 하 고 있는 계층을 사용 합니다.  
  
-   수준 식과 멤버 식이 모두 지정 된 경우는 **OpeningPeriod** 함수는 지정 된 수준이 들어 있는 계층 내에서 지정된 된 수준에서 지정 된 멤버의 하위 항목 중 첫 번째 형제를 반환 합니다.  
  
-   수준 식과 멤버 식이 모두 지정 된 경우는 **OpeningPeriod** 함수는 기본 수준 및 차원의 멤버를 사용 하 여 Time 형식의 합니다.  
  
> [!NOTE]  
>  [ClosingPeriod](../mdx/closingperiod-mdx.md) 함수는 비슷합니다는 **OpeningPeriod** 함수와 **ClosingPeriod** 함수는 첫 번째 형제 대신 마지막 형제를 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Time 형식인 Date 차원의 FY2002 멤버에 대한 기본 측정값의 값을 반환합니다. Fiscal Year 수준이 [All] 수준의 첫 번째 하위 항목이고, Fiscal 계층이 계층 컬렉션의 첫 번째 사용자 정의 계층이라서 해당 계층이 기본 계층이며, FY 2002 멤버가 이 계층에서 이 수준의 첫 번째 형제이므로 이 멤버가 반환됩니다.  
  
```  
SELECT OpeningPeriod() ON 0  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 Date.Date 특성 계층의 Date.Date.Date 수준에서 July 1, 2001 멤버의 기본 측정값에 대한 값을 반환합니다. 이 멤버는 Date.Date 특성 계층에서 [All] 수준의 하위 항목에 대한 첫 번째 형제입니다.  
  
```  
SELECT OpeningPeriod([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 January, 2003 멤버의 기본 측정값에 대한 값을 반환합니다. 이 멤버는 Calendar 사용자 정의 계층의 Year 수준에서 2003 멤버의 하위 항목에 대한 첫 번째 형제입니다.  
  
```  
SELECT OpeningPeriod([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 July, 2002 멤버의 기본 측정값에 대한 값을 반환합니다. 이 멤버는 Fiscal 사용자 정의 계층의 Year 수준에서 2003 멤버의 하위 항목에 대한 첫 번째 형제입니다.  
  
```  
SELECT OpeningPeriod([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)   
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling &#40;MDX&#41;](../mdx/firstsibling-mdx.md)  
  
  
