---
title: MemberToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9a33aede54557491dea50a557ed581929c5383e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68001461"
---
# <a name="membertostr-mdx"></a>MemberToStr(MDX)


  지정 된 멤버에 해당 하는 MDX (Multidimensional Expressions) 형식 문자열을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 이 함수는 멤버의 고유 이름을 포함한 문자열을 반환합니다. 일반적으로이 함수는 멤버의 uniquename을 외부 함수에 전달 하는 데 사용 됩니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 [Geography] 문자열을 반환 합니다. [Geography]. [Country]. & [미국]:  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
