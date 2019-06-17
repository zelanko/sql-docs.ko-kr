---
title: Extract (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a3c58799cc3e95efd7d49b3aff0bf31a1fce22b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63155214"
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
  
## <a name="remarks"></a>Remarks  
 합니다 **추출** 함수 추출 된 계층 요소의 튜플로 구성 된 집합을 반환 합니다. 지정된 집합에 있는 각 튜플에 대해 지정된 계층의 멤버가 결과 집합의 새 튜플로 추출됩니다. 항상 중복된 튜플을 제거합니다.  
  
 합니다 **추출** 의 반대 작업을 수행 하는 함수는 [Crossjoin](../mdx/crossjoin-mdx.md) 함수입니다.  
  
## <a name="examples"></a>예  
 다음 쿼리를 사용 하는 방법을 보여 줍니다 합니다 **추출** 함수에서 반환 된 튜플의 집합에는 **비어 있지 않은** 함수:  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
