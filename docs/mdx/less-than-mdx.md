---
title: '&lt; (보다 작음) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 111c3aae92839ff9f1574da6420d096d31517c80
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241045"
---
# <a name="lt-less-than-mdx"></a>&lt; (보다 작음) (MDX)


  하나의 MDX 식의 값이 다른 MDX 식의 값보다 작은지 확인하는 비교 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
MDX_Expression < MDX_Expression  
```  
  
#### <a name="parameters"></a>매개 변수  
 *MDX_Expression*  
 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 다음 조건을 기반으로 하는 부울 값입니다.  
  
-   **true** 두 매개 변수는 null이 아닌 경우 및 첫 번째 매개 변수가 두 번째 매개 변수의 값 보다 낮은 값이 있습니다.  
  
-   **false** 경우 매개 변수가 모두 null이 아닌 경우이 있고 첫 번째 매개 변수 값 같음 또는 두 번째 매개 변수의 값 보다 큽니다.  
  
-   매개 변수 중 하나가 Null이거나 둘 다 Null인 경우 Null입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for clothing sales where the GPM is less than 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] < .3,  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
