---
description: Union (MDX)
title: Union (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b0b4240d6c646761c5d962e4b9fa1ca54e0dcc0e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341209"
---
# <a name="union--mdx"></a>Union (MDX)


  두 집합의 합집합을 반환합니다. 필요에 따라 중복된 멤버를 포함할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Standard syntax  
Union(Set_Expression1, Set_Expression2 [,...n][, ALL])  
  
Alternate syntax 1  
Set_Expression1 + Set_Expression2 [+...n]  
  
Alternate syntax 2  
{Set_Expression1 , Set_Expression2 [,...n]}  
```  
  
## <a name="arguments"></a>인수  
 *식 1 설정*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *식 2 설정*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 이 함수는 지정 된 두 집합의 합집합을 반환 합니다. 표준 구문을 사용 하 고 대체 구문 1을 사용 하면 기본적으로 중복 항목이 제거 됩니다. 표준 구문을 사용 하는 경우 **ALL** 플래그를 사용 하면 조인 된 집합에 중복이 유지 됩니다. 중복 항목은 집합의 뒷부분부터 삭제됩니다. 대체 구문 2를 사용하면 중복 항목이 항상 유지됩니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 각 구문을 사용 하는 **Union** 함수의 동작을 보여 줍니다.  
  
### <a name="standard-syntax-duplicates-eliminated"></a>중복 항목을 제거하는 표준 구문  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="standard-syntax-duplicates-retained"></a>중복 항목을 유지하는 표준 구문  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   , ALL  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-1-duplicates-eliminated"></a>중복 항목을 제거하는 대체 구문 1  
  
```  
SELECT   
   [Date].[Calendar Year].children   
   + {[Date].[Calendar Year].[CY 2002]}   
   + {[Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-2-duplicates-retained"></a>중복 항목을 유지하는 대체 구문 2  
  
```  
SELECT   
   {[Date].[Calendar Year].children  
   , [Date].[Calendar Year].[CY 2002]  
   , [Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [+ &#40;Union&#41; &#40;MDX&#41;](../mdx/union-mdx-operator-reference.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
