---
title: 상관 관계 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 35227d129f70a505a33157d1aa945da5acb219d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68045210"
---
# <a name="correlation-mdx"></a>Correlation(MDX)


  집합에 대해 계산된 x-y 값 쌍의 상관 계수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Correlation( Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression_y*  
 Y축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *Numeric_Expression_x*  
 X축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **상관 관계** 함수는 첫 번째 숫자 식에 대해 지정 된 집합을 먼저 평가 하 여 y 축 값을 구하는 방법으로 두 값 쌍의 상관 계수를 계산 합니다. 그런 다음 두 번째 숫자 식(지정된 경우)에 대해 지정된 집합을 계산하여 X축 값 집합을 구합니다. 두 번째 숫자 식이 지정되지 않은 경우 이 함수는 지정된 집합의 현재 셀 컨텍스트를 X축 값으로 사용합니다.  
  
> [!NOTE]  
>  **상관 관계** 함수는 빈 셀 이나 텍스트 또는 논리 값을 포함 하는 셀을 무시 합니다. 그러나 값이 0인 셀은 포함시킵니다.  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
