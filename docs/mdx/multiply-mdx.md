---
title: '* 곱하기 (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 396dded86adfe8faa6b6ad58b5eb8174d4323726
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088417"
---
# <a name="-multiply-mdx"></a>*(곱하기)(MDX)


  두 수를 곱하는 산술 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Numeric_Expression * Numeric_Expression  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Numeric_Expression*  
 숫자 값을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>Return Value  
 우선 순위가 더 높은 매개 변수의 데이터 형식을 갖는 값입니다.  
  
## <a name="remarks"></a>설명  
 두 식이 모두 동일한 데이터 형식으로 되어 있거나 식 하나가 암시적으로 다른 식의 데이터 형식으로 변환될 수 있어야 합니다. 식 하나가 Null 값으로 계산되는 경우 연산자는 Null 값을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
