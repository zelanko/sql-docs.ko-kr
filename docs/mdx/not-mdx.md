---
title: NOT (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4031b887eb0a42580d6ae8debf6c9177ff67efc3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088232"
---
# <a name="not-mdx"></a>NOT(MDX)


  숫자 식에 논리 부정을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Expression1*  
 숫자 값을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>Return Value  
 인수가 **true**로 평가 되는 경우 **false** 를 반환 하는 부울 값입니다. 그렇지 않으면 **true**입니다.  
  
## <a name="remarks"></a>설명  
 **Not** 연산자는 연산자가 논리 부정을 수행 하기 전에 식을 부울 값 (0, 0, 0, 0, **0, 0)으로**처리 **합니다.** 다음 표에서는 **not** 연산자가 논리 부정을 수행 하는 방법을 보여 줍니다.  
  
|*Expression1*|Return Value|  
|-------------------|------------------|  
|**true**|**허위**|  
|**허위**|**true**|  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
