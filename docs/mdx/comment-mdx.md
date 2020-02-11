---
title: 주석 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f0aa1455ffd9f52fd917f68d2bb0bb80e3f25a94
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006277"
---
# <a name="comment-mdx"></a>주석 (MDX)


  사용자가 제공한 주석 텍스트를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
/* Comment_Text */      
```  
  
#### <a name="parameters"></a>매개 변수  
 *Comment_Text*  
 주석 텍스트를 포함하는 문자열입니다.  
  
## <a name="remarks"></a>설명  
 서버는 주석 문자/* 및 \*/사이의 텍스트를 평가 하지 않습니다. 주석은 별도의 줄 또는 MDX 문에 입력될 수 있습니다. 여러 줄로 된 주석은/\* 및 \*/로 표시 되어야 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [MDX&#41; &#40;&#40;설명&#41;](../mdx/comment-mdx-double-slash.md)   
 [--&#40;주석&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
