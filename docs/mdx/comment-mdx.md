---
title: 주석 (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '*/'
- /*
dev_langs:
- kbMDX
helpviewer_keywords:
- commenting characters
- /*...*/ (comment)
ms.assetid: 64434ae4-80ce-4634-86b8-4125dfaa7f61
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 4a4c9aa5bfbb27fd208b6f418e18b1c224451f27
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="comment-mdx"></a>주석 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  사용자가 제공한 주석 텍스트를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
/* Comment_Text */      
```  
  
#### <a name="parameters"></a>매개 변수  
 *Comment_Text*  
 주석 텍스트를 포함하는 문자열입니다.  
  
## <a name="remarks"></a>주의  
 주석 문자 사이 오는 텍스트는 계산 되지 않습니다 / * 및 \*/ 합니다. 주석은 별도의 줄 또는 MDX 문에 입력될 수 있습니다. 여러 줄로 이루어진 주석은로 표시 되어야 합니다 /\* 및 \*/ 합니다.  
  
 주석의 길이에는 제한이 없습니다. 주석은 `/* Test /*Comment*/ Text*/`와 같이 중첩될 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
/* This member returns the gross profit margin for product types  
  and reseller types crossjoined by year. */  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM /* Select from the Adventure Works cube. */  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [&#40;주석&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [-& #40; 설명 & #41; & #40; Mdx& #41;](../mdx/comment-mdx-operator-reference.md)   
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
