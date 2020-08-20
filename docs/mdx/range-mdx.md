---
description: ': (범위) (MDX)'
title: ': (범위) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d52a78a1fcdefa4ee7bf09fa4125b488165e09c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500466"
---
# <a name="-range-mdx"></a>: (범위) (MDX)


  지정한 두 멤버를 엔드포인트로 사용하고 지정한 두 멤버 사이의 모든 멤버를 집합의 멤버로 포함시켜 일반적인 순서로 정렬된 집합을 반환하는 집합 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression : Member_Expression      
```  
  
#### <a name="parameters"></a>매개 변수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 멤버를 포함하는 집합과 지정된 멤버 사이의 모든 멤버입니다.  
  
## <a name="remarks"></a>설명  
 두 매개 변수는 모두 특정 차원과 동일한 수준 및 계층 내에서 멤버를 지정해야 합니다. 두 매개 변수가 모두 동일한 멤버를 지정 하는 경우 **: (범위)** 연산자는 지정 된 멤버만 포함 하는 집합을 반환 합니다. 첫 번째 매개 변수가 Null인 경우 집합에는 두 번째 매개 변수에 지정된 멤버 수준의 처음부터 해당 멤버까지 포함하여 모든 멤버가 들어 있습니다. 두 번째 매개 변수가 Null인 경우 집합에는 첫 번째 매개 변수에 지정된 멤버에서 동일한 수준의 마지막 멤버까지 포함하여 모든 멤버가 들어 있습니다.  
  
 MDX에는 이 집합 연산자에 해당하는 기능이 없습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
-- This query returns the freight cost per user  
-- for products, averaged by month, for the first quarter.  
With Member [Measures].[Freight Per Customer] as  
 (  
     [Measures].[Internet Freight Cost]  
     /   
     [Measures].[Customer Count]  
)  
  
SELECT   
    {[Ship Date].[Calendar].[Month].&[2004]&[1] : [Ship Date].[Calendar].[Month].&[2004]&[3]} ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
