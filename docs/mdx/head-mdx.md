---
title: Head (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6e6d8da7a5813f7e99c022e19f18de2800598885
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67906004"
---
# <a name="head-mdx"></a>Head(MDX)


  집합에서 중복된 항목을 포함하여 처음 나오는 지정한 수만큼의 요소를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *수*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>설명  
 **Head** 함수는 지정 된 집합의 처음부터 지정 된 수 만큼의 튜플을 반환 합니다. 요소의 순서는 유지됩니다. Count의 기본값은 1입니다. 지정 된 튜플 수가 1 보다 작은 경우 **Head** 함수는 빈 집합을 반환 합니다. 지정된 튜플 수가 집합의 튜플 수를 초과할 경우에는 원래 집합을 반환합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Reseller Gross Profit를 기준으로 계층에 관계없이 판매량이 상위 5위 안에 속하는 제품 하위 범주를 반환합니다. **Head** 함수는 **Order** 함수를 사용 하 여 결과를 정렬 한 후 결과에서 처음 5 개 집합만 반환 하는 데 사용 됩니다.  
  
```  
SELECT   
[Measures].[Reseller Gross Profit] ON 0,  
Head  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,5  
   ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [테일 &#40;MDX&#41;](../mdx/tail-mdx.md)   
 [MDX&#41; &#40;항목 &#40;튜플&#41;](../mdx/item-tuple-mdx.md)   
 [MDX&#41; &#40;항목 &#40;멤버&#41;](../mdx/item-member-mdx.md)   
 [MDX &#40;순위&#41;](../mdx/rank-mdx.md)   
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
