---
title: AND (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 930fe19abe7b1d783b4c69ef54b9b2550a05d538
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017090"
---
# <a name="and-mdx"></a>AND(MDX)


  두 숫자 식에 논리 결합을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Expression1*  
 숫자 값을 반환하는 유효한 MDX 식입니다.  
  
 *Expression2*  
 숫자 값을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>Return Value  
 두 매개 변수가 모두 **true**로 평가 되 면 true를 반환 하는 부울 값입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>설명  
 연산자 **는 논리** 결합을 수행 하기 전에 두 식을 모두 부울 값 (0, 0, 0, **0, 0)으로**처리 **합니다.** 다음 표에서는 **AND** 연산자가 논리 결합을 수행 하는 방법을 보여 줍니다.  
  
|*Expression1*|*Expression2*|Return Value|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**false**|  
|**false**|**true**|**false**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>예제  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for clothing sales where the GPM is between 20% and 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] <= .3 AND   
      [Measures].[Gross Profit Margin] >= .2,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT NON EMPTY  
    [Sales Territory].[Sales Territory Country].Members ON 0,  
    [Product].[Category].[Clothing] ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[LowGPM])  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
