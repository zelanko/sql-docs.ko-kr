---
description: Crossjoin-MDX 연산자 참조
title: '* Crossjoin (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c957b72736fa8038f01175e3c65898a85704a56b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413149"
---
# <a name="crossjoin----mdx-operator-reference"></a>Crossjoin-MDX 연산자 참조


  두 집합의 교차곱을 반환하는 집합 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set_Expression * Set_Expression  
```  
  
## <a name="parameter"></a>매개 변수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 두 매개 변수의 교차곱을 포함하는 집합입니다.  
  
## <a name="remarks"></a>설명  
 ** \* (Crossjoin)** 연산자는 [Crossjoin](../mdx/crossjoin-mdx.md) 함수와 기능적으로 동일 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
-- This query returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
