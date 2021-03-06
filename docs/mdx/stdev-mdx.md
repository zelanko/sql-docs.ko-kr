---
description: Stdev(MDX)
title: Stdev (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e443cd7be9301dc5b5907e49fd967b1507feae03
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386949"
---
# <a name="stdev-mdx"></a>Stdev(MDX)


  n으로 나누는 비편향 모집단 수식을 사용하여 집합에 대해 계산되는 숫자 식의 표본 표준 편차를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stdev(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **Stdev** 함수는 비편향 모집단 수식을 사용 하는 반면 [StdevP](../mdx/stdevp-mdx.md) 함수는 편향 모집단 수식을 사용 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 비편향 모집단 수식을 사용하여 2003년의 처음 3개월 동안 계산된 Internet Order Quantity의 표준 편차를 반환합니다.  
  
```  
WITH MEMBER Measures.x AS   
   Stdev   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
