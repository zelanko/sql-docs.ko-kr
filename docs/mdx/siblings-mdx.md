---
title: Siblings (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9d8ba2dd26575ebd41f4a6c275a2668b1421dee6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036951"
---
# <a name="siblings-mdx"></a>Siblings(MDX)


  멤버 자체를 포함하여 지정한 멤버의 형제 항목을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.Siblings   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
### <a name="example"></a>예제  
 다음 예에서는 2003년 3월과 2003년 3월의 형제 항목(2003년 1월 및 2003년 2월)에 대한 기본 측정값을 반환합니다.  
  
```  
SELECT [Date].[Calendar].[Month].[March 2003].Siblings ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
