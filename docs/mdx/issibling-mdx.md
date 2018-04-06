---
title: IsSibling (MDX) | Microsoft Docs
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
- ISSIBLING
dev_langs:
- kbMDX
helpviewer_keywords:
- IsSibling function
ms.assetid: 12f302f0-141e-4ec0-ad5f-329aade17a4d
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8a318fd05502dfc9051c51542dcf864fe914d915
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="issibling-mdx"></a>IsSibling(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 멤버가 지정한 다른 멤버의 형제 항목인지 여부를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsSibling(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression1*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Member_Expression2*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **IsSibling** 함수에서 반환 **true** 첫 번째 멤버는 지정된 된 두 번째 멤버의 형제를 지정 합니다. 그렇지 않으면 함수가 반환 **false**합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Date 차원의 Fiscal 계층에 있는 현재 멤버가 2002년 7월의 형제인 경우 TRUE를 반환합니다.  
  
 `WITH MEMBER MEASURES.ISSIBLINGDEMO AS`  
  
 `IsSibling([Date].[Fiscal].CURRENTMEMBER, [Date].[Fiscal].[Month].&[2002]&[7])`  
  
 `SELECT {MEASURES.ISSIBLINGDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
