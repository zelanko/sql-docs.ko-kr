---
title: IF 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 41bd34fbd3d296f4aa38877e6d26e25eba9ae726
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68138687"
---
# <a name="mdx-scripting---if"></a>MDX 스크립팅 - IF


  조건이 True인 경우 문을 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 True 또는 False를 반환하는 부울로 계산되는 MDX 식입니다.  
  
 *배정을*  
 하위 큐브 또는 계산 속성에 값을 할당하는 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 [IIf &#40;mdx&#41;](../mdx/iif-mdx.md) 함수와 달리 값 이나 개체를 반환 하는 데만 사용할 수 있는 [Mdx&#41;&#40;CASE 문과](../mdx/case-statement-mdx.md) 달리 제어 흐름에 if 문을 사용 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Customers 차원에 있는 Customers Geography 계층의 Country 수준으로 범위를 제한합니다. 현재 측정값이 Internet Sales Amount이면 Internet Sales Amount는 10으로 설정됩니다.  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
