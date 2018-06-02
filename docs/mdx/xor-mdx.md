---
title: XOR (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb0a91faaec7e5c2b6a7b2289e65989ba19b33e3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581875"
---
# <a name="xor-mdx"></a>XOR(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  두 숫자 식에 대해 논리 제외를 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Expression1 XOR Expression2  
  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Expression1*  
 숫자 값을 반환하는 유효한 MDX 식입니다.  
  
 *Expression2*  
 숫자 값을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 하는 부울 값 **true** 에 단 하나의 인수가 계산 되 면 **true**, 그렇지 않으면 **false**합니다.  
  
## <a name="remarks"></a>Remarks  
 **XOR** 연산자는 매개 변수가 모두 부울 값으로 취급 (0, 0으로 **false**, 그렇지 않으면 **true**) 연산자는 논리 제외를 수행 하기 전에. 다음 표에서 설명 방법을 **XOR** 연산자로 논리 제외를 수행 합니다.  
  
|*Expression1*|*Expression2*|반환 값|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**false**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="see-also"></a>관련 항목  
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
