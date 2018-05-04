---
title: MemberToStr (MDX) | Microsoft Docs
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
- MEMBERTOSTR
dev_langs:
- kbMDX
helpviewer_keywords:
- MemberToStr function
ms.assetid: 2076b24a-603a-4d74-91bd-a3d347739bcd
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5f9d5cb18739fd7d84671ce553e1898321ad6cea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="membertostr-mdx"></a>MemberToStr(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정된 멤버에 해당하는 MDX(Multidimensional Expressions) 형식 문자열을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 이 함수는 멤버의 고유 이름을 포함한 문자열을 반환합니다. 이 함수는 멤버의 고유 이름을 외부 함수에 전달하는 데 사용됩니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 문자열 [Geography].[Geography].[Country].&[United States]를 반환합니다.  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
