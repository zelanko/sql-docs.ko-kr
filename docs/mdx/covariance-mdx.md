---
title: 공분산 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea3755fb103362b797735d74c9cbe67523aace59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68047192"
---
# <a name="covariance-mdx"></a>Covariance(MDX)


  x-y 값 쌍의 개수로 나누는 편향 모집단 수식을 사용하여 집합에 대해 계산된 x-y 값 쌍의 모집단 공변성(covariance)을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Covariance(Set_Expression,Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression_y*  
 Y축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *Numeric_Expression_x*  
 X축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **공분산** 함수는 첫 번째 숫자 식에 대해 지정 된 집합을 계산 하 여 y 축 값을 구합니다. 그런 다음 두 번째 숫자 식(지정된 경우)에 대해 지정된 집합을 계산하여 X축 값 집합을 구합니다. 두 번째 숫자 expressionis가 지정 되지 않은 경우이 함수는 지정 된 집합에 있는 셀의 현재 컨텍스트를 x 축 값으로 사용 합니다.  
  
 **공분산** 함수는 편향 모집단 수식을 사용 합니다. 이는 x-y 쌍의 수를 나눈 다음 1을 빼서 비편향 모집단 수식을 사용 하는 [Covarc](../mdx/covariancen-mdx.md) # 함수와는 대조적입니다.  
  
> [!NOTE]  
>  **공분산** 함수는 빈 셀을 무시 하거나 텍스트 또는 논리 값을 포함 하는 셀은 무시 됩니다. 그러나 값이 0인 셀은 포함시킵니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Covariance 함수를 사용하는 방법을 보여 줍니다.  
  
```  
WITH   
MEMBER [Measures].[CovarianceDemo] AS  
COVARIANCE([Date].[Date].[Date].Members, [Measures].[Internet Sales Amount], [Measures].[Internet Order Count])   
SELECT {[Measures].[CovarianceDemo]} ON 0   
FROM  
[Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
