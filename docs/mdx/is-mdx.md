---
description: IS(MDX)
title: IS (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eab5fc86d89fccbe6ae56c4dba78ccde60e26d50
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387349"
---
# <a name="is-mdx"></a>IS(MDX)


  두 개체 식에 대해 논리 비교를 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Expression1 IS ( Expression2 | NULL )  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Expression1*  
 MDX 개체 참조를 반환하는 유효한 MDX 식입니다.  
  
 *Expression2*  
 MDX 개체 참조를 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 두 인수가 모두 동일한 개체를 참조 하면 **true** 를 반환 하는 부울 값입니다. 그렇지 않으면 **false**입니다. **Null** 키워드가 지정 된 경우 *Expression1* 가 **null**이면 연산자는 **true** 를 반환 합니다. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>설명  
 **Is** 연산자는 튜플 및 멤버가 idempotent 여부를 확인 하는 데 주로 사용 됩니다. 즉, 정확히 동일한 것입니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 **IS** 연산자를 사용 하 여 축의 현재 멤버가 특정 멤버 인지 확인 하는 방법을 보여 줍니다.  
  
 `With`  
  
 `//Returns TRUE if the currentmember is Bikes`  
  
 `Member [Measures].[IsBikes?] AS`  
  
 `[Product].[Category].CurrentMember IS [Product].[Category].&[1]`  
  
 `SELECT`  
  
 `{[Measures].[IsBikes?]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
