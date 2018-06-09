---
title: This (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77db403ee016283a565a6bc86d2f6857de0eff45
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743252"
---
# <a name="this-mdx"></a>This(MDX)


  MDX 계산 스크립트에서 할당에 사용할 수 있도록 현재 하위 큐브를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
This   
```  
  
## <a name="remarks"></a>Remarks  
 **이** 함수는 MDX 계산 스크립트의 현재 범위 내의 현재 하위 큐브를 제공 하는 하위 큐브 식 대신 사용할 수 있습니다. **이** 대입문의 왼쪽에 함수를 사용 해야 합니다.  
  
## <a name="examples"></a>예  
 다음 MDX 스크립트 조각에서는 SCOPE 문에 This 키워드를 사용하여 하위 큐브에 할당하는 방법을 보여 줍니다.  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2005],`  
  
 `[Date].[Fiscal].[Fiscal Quarter].Members,`  
  
 `[Measures].[Sales Amount Quota]`  
  
 `) ;`  
  
 `This = ParallelPeriod`  
  
 `(`  
  
 `[Date].[Fiscal].[Fiscal Year], 1,`  
  
 `[Date].[Fiscal].CurrentMember`  
  
 `) * 1.35 ;`  
  
 `/*-- Allocate equally to months in FY 2002 -----------------------------*/`  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2002],`  
  
 `[Date].[Fiscal].[Month].Members`  
  
 `) ;`  
  
 `This = [Date].[Fiscal].CurrentMember.Parent / 3 ;`  
  
 `End Scope ;`  
  
 `End Scope;`  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [계산](../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
