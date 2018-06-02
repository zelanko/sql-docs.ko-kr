---
title: 없습니다 (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5020f461d2576bbac7d0292ca0bf75bd8033e173
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580505"
---
# <a name="not-mdx"></a>NOT(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  숫자 식에 논리 부정을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Expression1*  
 숫자 값을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 하는 부울 값 **false** 으로 계산 되는 인수 **true**, 그렇지 않으면 **true**합니다.  
  
## <a name="remarks"></a>Remarks  
 **하지** 연산자는 부울 값으로 식을 처리 (0, 0,으로 **false**, 그렇지 않으면 **true**) 연산자가 논리 부정을 수행 하기 전에. 다음 표에서 설명 방법을 **하지** 연산자가 논리 부정을 수행 합니다.  
  
|*Expression1*|반환 값|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>관련 항목  
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
