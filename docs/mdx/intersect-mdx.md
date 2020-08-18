---
description: Intersect(MDX)
title: Intersect (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9216b334caf67191e231c3ec0389da3fb7493b24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471845"
---
# <a name="intersect-mdx"></a>Intersect(MDX)


  두 입력 집합의 교집합을 반환합니다. 중복 요소를 포함시킬 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Intersect(Set_Expression1 , Set_Expression2 [ , ALL ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression1*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression2*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **Intersect** 함수는 두 집합의 교집합을 반환 합니다. 기본적으로 이 함수는 교집합을 구하기 전에 두 집합에서 중복 요소를 제거합니다. 지정된 두 집합에는 동일한 차원이 있어야 합니다.  
  
 선택적 **ALL** 플래그는 중복 항목을 유지 합니다. **ALL** 을 지정 하면 **Intersect** 함수는 일반적으로 중복 되지 않은 요소를 교차 하 고 두 번째 집합에 일치 하는 중복이 있는 첫 번째 집합의 각 중복 항목을 교차 합니다. 지정된 두 집합에는 동일한 차원이 있어야 합니다.  
  
## <a name="example"></a>예제  
 다음 쿼리는 지정된 두 집합 모두에 나타나는 두 멤버인 Year 2003과 2004를 반환합니다.  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001], [Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003]}`  
  
 `, {[Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 다음 쿼리는 지정된 두 집합에 다른 계층의 멤버가 포함되므로 실패합니다.  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001]}`  
  
 `, {[Customer].[City].&[Abingdon]&[ENG]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
