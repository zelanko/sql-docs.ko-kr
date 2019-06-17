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
manager: kfile
ms.openlocfilehash: ff7ffb1b57c8af38e1b2eeebc64f2a3e753fc5b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278492"
---
# <a name="membertostr-mdx"></a>MemberToStr(MDX)


  지정된 된 멤버에 해당 하는 MDX 형식 문자열을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 이 함수는 멤버의 고유 이름을 포함한 문자열을 반환합니다. 일반적으로 멤버의 고유 이름을 외부 함수에 전달 하는 것이 됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 문자열 [Geography]를 반환합니다. [Geography]입니다. [Country]. & [United States]:  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
