---
title: Item (멤버) (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ITEM
dev_langs:
- kbMDX
helpviewer_keywords:
- Item function
ms.assetid: 71cca249-910b-4ecd-9097-1a17b224e219
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: db417d352d7e2e30ebd81ba64afba24f1777c2ee
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="item-member-mdx"></a>Item(멤버)(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>주의  
 **항목** 함수는 지정 된 튜플 로부터 멤버를 반환 합니다. 로 지정 된 0부터 시작 위치에서 발견 된 멤버를 반환 하는 함수 *인덱스*합니다.  
  
## <a name="example"></a>예제  
 다음 예는 열에서 `[2003]` 튜플의 첫 번째 항목인 `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).` 멤버를 반환합니다.  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
