---
title: IS (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aaf4151d8291ccd4249892c6ef8fce8a3d280f6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905985"
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
 반환 하는 부울 값 **true** 인수가 모두 동일한 개체;를 참조 하는 경우이 고, 그렇지 **false**합니다. 경우는 **NULL** 키워드를 지정 하는 연산자를 반환 합니다 **true** 하는 경우 *Expression1* 됩니다 **null**고, 그렇지 않으면 **false** .  
  
## <a name="remarks"></a>설명  
 합니다 **IS** 연산자는 대개 지 여부를 확인할 튜플 및 멤버가 멱 등 원, 정확히 동일한 지를 의미 합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 사용 하는 방법을 보여 줍니다 합니다 **IS** 연산자 축에 있는 현재 멤버가 특정 멤버 인지 확인 하려면:  
  
 `With`  
  
 `//Returns TRUE if the currentmember is Bikes`  
  
 `Member [Measures].[IsBikes?] AS`  
  
 `[Product].[Category].CurrentMember IS [Product].[Category].&[1]`  
  
 `SELECT`  
  
 `{[Measures].[IsBikes?]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
