---
title: Distinct (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fc3e4680991f88743bbab8eec1de3bb629c94b66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248258"
---
# <a name="distinct-mdx"></a>Distinct(MDX)


  지정된 집합을 계산하고 집합에서 중복 튜플을 제거하여 결과 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Distinct(Set_Expression)  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 경우는 **Distinct** 함수는 지정된 된 집합에서 중복 튜플의 찾을, 함수 집합의 순서를 그대로 유지 하면서 중복 튜플의 첫 번째 인스턴스만 유지 합니다.  
  
## <a name="examples"></a>예  
 다음 예제 쿼리에서는 Distinct 함수를 명명된 집합과 함께 사용하는 방법과 이 함수를 Count 함수와 함께 사용하여 집합에서 중복 제외 튜플 수를 찾는 방법을 보여 줍니다.  
  
 `WITH SET MySet AS`  
  
 `{[Customer].[Customer Geography].[Country].&[Australia],[Customer].[Customer Geography].[Country].&[Australia],`  
  
 `[Customer].[Customer Geography].[Country].&[Canada],[Customer].[Customer Geography].[Country].&[France],`  
  
 `[Customer].[Customer Geography].[Country].&[United Kingdom],[Customer].[Customer Geography].[Country].&[United Kingdom]}`  
  
 `MEMBER MEASURES.SETCOUNT AS`  
  
 `COUNT(MySet)`  
  
 `MEMBER MEASURES.SETDISTINCTCOUNT AS`  
  
 `COUNT(DISTINCT(MySet))`  
  
 `SELECT {MEASURES.SETCOUNT, MEASURES.SETDISTINCTCOUNT} ON 0,`  
  
 `DISTINCT(MySet) ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
