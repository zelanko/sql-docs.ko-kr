---
title: This (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: THIS
dev_langs: kbMDX
helpviewer_keywords: This function [MDX]
ms.assetid: 87acddee-ae54-49ee-8923-1b760606e8b7
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7065d192cf9b02f827753b8e0b50191d6daf30b8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="this-mdx"></a>This(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  MDX 계산 스크립트에서 할당에 사용할 수 있도록 현재 하위 큐브를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
This   
```  
  
## <a name="remarks"></a>주의  
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
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)   
 [계산](../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
