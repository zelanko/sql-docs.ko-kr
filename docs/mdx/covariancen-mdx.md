---
title: CovarianceN (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 054acaaca417ca7d3fa5303fb31b5ea027bfcd72
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740182"
---
# <a name="covariancen-mdx"></a>CovarianceN(MDX)


  x-y 값 쌍의 개수로 나누는 비편향 모집단 수식을 사용하여 집합에 대해 계산된 x-y 값 쌍의 표본 공변성(covariance)을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CovarianceN(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression_y*  
 Y축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *Numeric_Expression_x*  
 X축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 **CovarianceN** 함수는 y 축에 대 한 값을 가져오려는 첫 번째 숫자 식에 대해 지정 된 집합을 계산 합니다. 그런 다음 두 번째 숫자 식(지정된 경우)에 대해 지정된 집합을 계산하여 X축 값 집합을 구합니다. 두 번째 숫자 식이 지정되지 않은 경우 이 함수는 지정된 집합의 현재 셀 컨텍스트를 X축 값으로 사용합니다.  
  
 **CovarianceN** 함수는 비편향된 모집단 수식을 사용 합니다. 이 달리는 [공](../mdx/covariance-mdx.md) 함수는 (x, y 쌍의 개수로 나누는) 편향된 모집단 수식을 사용 합니다.  
  
> [!NOTE]  
>  **CovarianceN** 함수는 빈 셀 이나 텍스트 또는 논리 값을 포함 하는 셀은 무시 합니다. 그러나 값이 0인 셀은 포함시킵니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
