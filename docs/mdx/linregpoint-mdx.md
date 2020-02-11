---
title: LinRegPoint (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3719071beca4dbd8cc991befbb7b2b74f8982c89
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905569"
---
# <a name="linregpoint-mdx"></a>LinRegPoint(MDX)


  집합의 선형 회귀를 계산 하 고 회귀선에서 y 절편의 값 (y = ax + b *)* 을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
LinRegPoint(Slice_Expression_x, Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>인수  
 *Slice_Expression_x*  
 slicer 축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로, 일반적으로 MDX 식입니다.  
  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression_y*  
 Y축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *Numeric_Expression_x*  
 X축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 최소 제곱법을 사용하는 선형 회귀는 일련의 점에 대해 가장 적합한 선인 회귀선의 수식을 계산합니다. 회귀선에는 다음과 같은 수식이 있습니다. 여기서 a는 기울기이 고 b는 절편입니다.  
  
 y = ax+b  
  
 **Linregpoint** 함수는 두 번째 숫자 식에 대해 지정 된 집합을 계산 하 여 y 축 값을 구합니다. 그런 다음 세 번째 숫자 식(지정된 경우)에 대해 지정된 집합을 계산하여 X축 값을 구합니다. 세 번째 숫자 식이 지정되지 않은 경우 이 함수는 지정된 집합의 현재 셀 컨텍스트를 X축 값으로 사용합니다. X축 인수를 지정하지 않는 방식은 Time 차원에서 자주 사용됩니다.  
  
 선형 회귀선이 계산된 후 첫 번째 숫자 식에 대해 수식 값이 계산되고 반환됩니다.  
  
> [!NOTE]  
>  **Linregpoint** 함수는 빈 셀 이나 텍스트가 포함 된 셀을 무시 합니다. 그러나 값이 0인 셀은 포함시킵니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Unit Sales와 Store Sales 간의 통계 관계를 기준으로 지난 10개의 기간과 비교한 Unit Sales의 예측 값을 반환합니다.  
  
```  
LinRegPoint([Measures].[Unit Sales],LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
