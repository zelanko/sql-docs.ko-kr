---
description: '&lt;&gt; (같지 않음) MDX'
title: '&lt;&gt; (같지 않음) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8c2651c7d542ac0a8707c20e8b32f4ba33ac7b54
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471795"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; (같지 않음) MDX


  하나의 MDX 식의 값이 다른 MDX 식의 값과 다른지 확인하는 비교 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>매개 변수  
 *MDX_Expression*  
 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 다음 조건을 기반으로 하는 부울 값입니다.  
  
-   두 매개 변수가 모두 null이 아니고 첫 번째 매개 변수가 두 번째 매개 변수와 같지 않으면 **true** 입니다.  
  
-   두 매개 변수가 모두 null이 아니고 첫 번째 매개 변수가 두 번째 매개 변수와 같으면 **false** 입니다.  
  
-   매개 변수 중 하나가 Null이거나 둘 다 Null인 경우 Null입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
