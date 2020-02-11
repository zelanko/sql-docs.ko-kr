---
title: 문자열 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d6cde1f60274d1437517d89e48b111e9e7298b9d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097370"
---
# <a name="tupletostr-mdx"></a>TupleToStr(MDX)


  지정 된 튜플에 해당 하는 MDX (Multidimensional Expressions) 형식 문자열을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
TupleToStr(Tuple_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Tuple_Expression*  
 튜플을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 이 함수를 사용하여 튜플의 문자열 표현을 구문 분석을 위해 외부 함수에 전송할 수 있습니다. 반환 되는 문자열은 중괄호로 {} 묶이고 각 멤버는 튜플에 명시적으로 정의 되어 있는 경우 쉼표로 구분 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 문자열 ([Date]. [ Calendar Year]. & [2001], [Geography]. [Geography]. [Country]. & [미국]):  
  
```  
WITH MEMBER Measures.x AS TupleToStr   
   (   
      ([Date].[Calendar Year].&[2001]  
         , [Geography].[Geography].[Country].&[United States]  
      )  
   )     
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 이전 예와 동일한 문자열을 반환합니다.  
  
```  
WITH SET s AS   
   {  
      ([Date].[Calendar Year].&[2001],  
         [Geography].[Geography].[Country].&[United States]  
      )   
   }  
MEMBER Measures.x AS TupleToStr ( s.Item(0) )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
