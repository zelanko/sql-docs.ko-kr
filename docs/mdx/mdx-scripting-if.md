---
title: IF 문 (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e7426c609de80ab249cd71e4364979ff07165598
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579865"
---
# <a name="mdx-scripting---if"></a>MDX 스크립팅-IF
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  조건이 True인 경우 문을 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 True 또는 False를 반환하는 부울로 계산되는 MDX 식입니다.  
  
 *할당*  
 하위 큐브 또는 계산 속성에 값을 할당하는 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 과 달리 제어 흐름에 IF 문을 사용는 [IIf &#40;MDX&#41; ](../mdx/iif-mdx.md) 함수 및 [CASE 문에 &#40;MDX&#41; ](../mdx/case-statement-mdx.md) 있는 수에 사용할 값 이나 개체를 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Customers 차원에 있는 Customers Geography 계층의 Country 수준으로 범위를 제한합니다. 현재 측정값이 Internet Sales Amount이면 Internet Sales Amount는 10으로 설정됩니다.  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
