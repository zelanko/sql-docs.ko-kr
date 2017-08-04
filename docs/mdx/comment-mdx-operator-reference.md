---
title: "-(주석) (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- --
dev_langs:
- kbMDX
helpviewer_keywords:
- commenting characters
- -- (comment character)
ms.assetid: 02aec133-6809-4829-b9a2-102c376e21da
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 720b1d7c90e65dbfdd365e5cabf5368e27da7ef8
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="comment---mdx-operator-reference"></a>메모-MDX 연산자 참조
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용자가 제공한 주석 텍스트를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>매개 변수  
 *Comment_Text*  
 주석 텍스트를 포함하는 문자열입니다.  
  
## <a name="remarks"></a>주의  
 설명은 별도의 줄에 삽입하거나 MDX 스크립트 줄 끝에 중첩하거나 MDX 문 내에 중첩할 수 있습니다. 서버는 주석을 평가하지 않습니다.  
  
 이 연산자는 한 줄로 된 주석 또는 중첩된 주석에 사용합니다.  --으로 입력된 주석은 새 줄 문자로 구분됩니다.  
  
 주석의 길이에는 제한이 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
-- This member returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM -- Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [설명 &#40; Mdx&#41;](../mdx/comment-mdx.md)   
 [&#40; 설명 &#41; &#40; Mdx&#41;](../mdx/comment-mdx-double-slash.md)   
 [MDX 연산자 참조 &#40; Mdx&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

