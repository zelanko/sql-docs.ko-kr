---
title: Item (멤버) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d7afa88f9d6239c8da7cb9c406ef11f0764f8dcf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905917"
---
# <a name="item-member-mdx"></a>Item(멤버)(MDX)


  지정한 튜플에서 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Tuple_Expression.Item( Index )  
```  
  
## <a name="arguments"></a>인수  
 *Tuple_Expression*  
 튜플을 반환하는 유효한 MDX 식입니다.  
  
 *Index*  
 반환할 튜플 내의 위치로 특정 멤버를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>설명  
 합니다 **항목** 함수는 지정 된 튜플 로부터 멤버를 반환 합니다. 함수에 지정 된 0부터 시작 위치에서 발견 된 멤버를 반환 합니다. *인덱스*합니다.  
  
## <a name="example"></a>예제  
 다음 예는 열에서 `[2003]` 튜플의 첫 번째 항목인 `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).` 멤버를 반환합니다.  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
