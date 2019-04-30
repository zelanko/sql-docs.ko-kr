---
title: (주석) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6570694bc38eb6f32f660006f1ed1b6797793b7b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306335"
---
# <a name="comment-mdx-double-slash"></a>주석 MDX 이중 슬래시


  사용자가 제공하는 텍스트를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
// Comment_Text   
```  
  
#### <a name="parameters"></a>매개 변수  
 *Comment_Text*  
 주석 텍스트를 포함하는 문자열입니다.  
  
## <a name="remarks"></a>Remarks  
 설명은 별도의 줄에 삽입하거나 MDX 스크립트 줄 끝에 중첩하거나 MDX 문 내에 중첩할 수 있습니다. 서버는 주석을 평가하지 않습니다.  
  
 한 줄로 된 주석에만 //를 사용합니다. //로 입력된 주석은 새 줄 문자로 구분됩니다.  
  
 주석의 길이에는 제한이 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
// This member returns the gross profit margin for product types  
// and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM // Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>관련 항목  
 [설명&#40;MDX&#41;](../mdx/comment-mdx.md)   
 [-- &#40;설명&#41;&#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
