---
description: Current(MDX)
title: Current (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 105bb306cb84f151024a288f5aa15eb09ddbf5c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387549"
---
# <a name="current-mdx"></a>Current(MDX)


  반복하는 동안 집합에서 현재 튜플을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set_Expression.Current   
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 반복 중 각 단계에서 수행되는 튜플은 현재 튜플입니다. **현재** 함수는 해당 튜플을 반환 합니다. 이 함수는 집합에 대해 반복하는 동안에만 유효합니다.  
  
 집합을 반복 하는 MDX 함수에는 [Generate](../mdx/generate-mdx.md) 함수가 포함 됩니다.  
  
> [!NOTE]  
>  이 함수는 집합 별칭을 사용하거나 명명된 집합을 정의함으로써 명명된 집합에 대해서만 사용할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예제에서는 **생성**내에서 **현재** 함수를 사용 하는 방법을 보여 줍니다.  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of all Calendar Years crossjoined with`  
  
 `//all Product Categories`  
  
 `SET MyTuples AS CROSSJOIN(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `//Iterates through each tuple in the set and returns the name of the Calendar`  
  
 `//Year in each tuple`  
  
 `MEMBER MEASURES.CURRENTDEMO AS`  
  
 `GENERATE(MyTuples, MyTuples.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
