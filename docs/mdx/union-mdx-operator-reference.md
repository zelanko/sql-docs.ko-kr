---
title: + (합집합) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cd352b95853cc5fe52857a080b6ca2e515f5c013
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097351"
---
# <a name="union---mdx-operator-reference"></a>공용 구조체-MDX 연산자 참조


  중복된 멤버를 제거하고 두 집합의 합집합을 반환하는 집합 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set_Expression + Set_Expression      
```  
  
#### <a name="parameters"></a>매개 변수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 두 집합의 멤버가 포함된 집합입니다.  
  
## <a name="remarks"></a>설명  
 합니다 **+ (Union)** 연산자는 기능적으로 동일 합니다 [Union &#40;MDX&#41; ](../mdx/union-mdx.md) 함수입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
-- This member returns the gross profit margin for each year for North American countries.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members ON 0,  
    {[Sales Territory].[Sales Territory].[Country].[United States]} +  
     {[Sales Territory].[Sales Territory].[Country].[Canada]} ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
