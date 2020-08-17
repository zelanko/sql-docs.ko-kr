---
description: + (문자열 연결) MDX
title: + (문자열 연결) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e92751cb709a93d3d5d8d05ac76361c22bee5fa7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386869"
---
# <a name="-string-concatenation-mdx"></a>+ (문자열 연결)(MDX)


  둘 이상의 문자열, 튜플 또는 문자열과 튜플의 조합을 연결하는 문자열 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
String_Expression + String_Expression  
```  
  
#### <a name="parameters"></a>매개 변수  
 *String_Expression*  
 문자열 값을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 우선 순위가 더 높은 매개 변수의 데이터 형식을 갖는 값입니다.  
  
## <a name="remarks"></a>설명  
 두 식이 모두 동일한 데이터 형식으로 되어 있거나 식 하나가 암시적으로 다른 식의 데이터 형식으로 변환될 수 있어야 합니다. 한 식이 Null 값으로 계산되는 경우 이 연산자는 다른 식의 결과를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
