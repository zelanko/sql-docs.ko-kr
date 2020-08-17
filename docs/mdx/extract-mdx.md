---
description: Extract(MDX)
title: Extract (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0b168794a38a515d4ace97d576710041eac86195
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387519"
---
# <a name="extract-mdx"></a>Extract(MDX)


  추출된 계층 요소에서 튜플 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Extract(Set_Expression, Hierarchy_Expression1 [,Hierarchy_Expression2, ...n] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Hierarchy_Expression1*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
 *Hierarchy_Expression2*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **Extract** 함수는 추출 된 계층 요소의 튜플로 구성 된 집합을 반환 합니다. 지정된 집합에 있는 각 튜플에 대해 지정된 계층의 멤버가 결과 집합의 새 튜플로 추출됩니다. 항상 중복된 튜플을 제거합니다.  
  
 **Extract** 함수는 [Crossjoin](../mdx/crossjoin-mdx.md) 함수의 반대 동작을 수행 합니다.  
  
## <a name="examples"></a>예제  
 다음 쿼리는 **비어 있지** 않은 함수에서 반환 된 튜플 집합에서 **Extract** 함수를 사용 하는 방법을 보여 줍니다.  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `//Returns the distinct combinations of Customer and Date for all purchases`  
  
 `//of Bike Racks or Bike Stands`  
  
 `EXTRACT(`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `*`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `*`  
  
 `{[Product].[Product Categories].[Subcategory].&[26],[Product].[Product Categories].[Subcategory].&[27]}`  
  
 `*`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `)`  
  
 `,  [Customer].[Customer], [Date].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
