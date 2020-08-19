---
description: 나누기(MDX)
title: 나누기 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0999df34ff817131e890afade89fc5daad85796b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484016"
---
# <a name="divide-mdx"></a>나누기(MDX)


  나누기를 수행하고 0으로 나누기에 대한 대체 결과 또는 BLANK()를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>인수  
 *분자*  
 피제수 또는 나누어지는 숫자입니다.  
  
 *분모*  
 제수 또는 나눌 숫자입니다.  
  
 *alternateresult*  
 (선택 사항) 0으로 나누면 오류가 발생하는 경우 반환되는 값입니다. 제공되지 않으면 기본값은 BLANK()입니다.  
  
## <a name="remarks"></a>설명  
 0으로 나누기의 대체 결과는 상수여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
