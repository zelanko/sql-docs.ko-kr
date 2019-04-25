---
title: IsGeneration (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a726470f89f2d3ea1677259e849735a09909a42d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62629410"
---
# <a name="isgeneration-mdx"></a>IsGeneration(MDX)


  지정한 멤버가 지정한 세대에 속하는지 여부를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Generation_Number*  
 지정된 멤버가 평가되는 기준 세대를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **IsGeneration** 함수에서 반환 **true** 지정된 된 멤버는 지정 된 세대 번호를 하는 경우. 반환이 고, 그렇지 **false**합니다. 또한 지정 된 멤버가 빈 멤버를 평가 하는 경우는 **IsGeneration** 함수에서 반환 **false**합니다.  
  
 세대 인덱싱을 위해 리프 멤버는 세대 인덱스 0입니다. 리프가 아닌 멤버의 세대 인덱스는 지정된 멤버에 대한 모든 자식 멤버의 합집합에서 가장 높은 세대 인덱스를 가져와서 1을 더하는 방식으로 결정됩니다. 리프가 아닌 멤버의 세대 인덱스의 결정 방법으로 인해 리프가 아닌 특정 멤버는 둘 이상의 세대에 속할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 [Date].[Fiscal].CurrentMember가 두 번째 세대에 속하는 경우 TRUE를 반환합니다.  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
