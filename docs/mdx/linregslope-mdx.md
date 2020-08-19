---
description: LinRegSlope(MDX)
title: LinRegSlope (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5443718e83084285983f3d22ff99d5931f82bad9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429815"
---
# <a name="linregslope-mdx"></a>LinRegSlope(MDX)


  집합의 선형 회귀를 계산 하 고 회귀선 y = ax + b에서 슬로프의 값을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
LinRegSlope(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression_y*  
 Y축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *Numeric_Expression_x*  
 X축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 최소 제곱법을 사용하는 선형 회귀는 일련의 점에 대해 가장 적합한 선인 회귀선의 수식을 계산합니다. 회귀선에는 다음과 같은 수식이 있습니다. 여기서 a는 기울기이 고 b는 절편입니다.  
  
 y = ax+b  
  
 **Linregslope** 함수는 첫 번째 숫자 식에 대해 지정 된 집합을 계산 하 여 y 축 값을 구합니다. 그런 다음 두 번째 숫자 식(지정된 경우)에 대해 지정된 집합 식을 계산하여 X축 값을 구합니다. 두 번째 숫자 식이 지정되지 않은 경우 이 함수는 지정된 집합의 현재 셀 컨텍스트를 X축 값으로 사용합니다. X축 인수를 지정하지 않는 방식은 Time 차원에서 자주 사용됩니다.  
  
 점의 집합을 구한 후 **Linregslope** 함수는 회귀선의 기울기 (이전 수식의 a)를 반환 합니다.  
  
> [!NOTE]  
>  **Linregslope** 함수는 빈 셀 이나 텍스트 또는 논리 값을 포함 하는 셀을 무시 합니다. 그러나 값이 0인 셀은 포함시킵니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Unit Sales 및 Store Sales 측정값에 대한 회귀선의 기울기를 반환합니다.  
  
```  
LinRegSlope(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
