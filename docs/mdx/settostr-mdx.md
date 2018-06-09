---
title: SetToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 57e74eb1c7db4aebdd01fde8fc48a425d7affa55
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743302"
---
# <a name="settostr-mdx"></a>SetToStr(MDX)


  지정된 집합에 해당하는 MDX 형식 문자열을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SetToStr(Set_Expression)  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 이 함수를 사용하여 집합의 문자열 표현을 구문 분석을 위해 외부 함수에 전송할 수 있습니다. 반환 되는 문자열은 중괄호로 묶여 {}, 쉼표로 구분 하 여 집합의 각 항목입니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Geography.Country 특성 계층의 모든 멤버를 포함하는 문자열을 반환합니다.  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
