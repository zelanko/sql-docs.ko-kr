---
title: 없습니다 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b70068562ff24e8a1619b85fe091ab3e17da173
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278501"
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
  
## <a name="return-value"></a>반환 값  
 반환 하는 부울 값 **false** 인수가 계산 되는 경우 **true**이 고, 그렇지 않으면 **true**합니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **되지** 연산자는 식을 부울 값으로 처리 (0으로 **false**이 고, 그렇지 않으면 **true**) 연산자가 논리 부정을 수행 하기 전에 합니다. 다음 표에서 설명 하는 방법을 **되지** 연산자로 논리 부정을 수행 합니다.  
  
|*Expression1*|반환 값|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>관련 항목  
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
