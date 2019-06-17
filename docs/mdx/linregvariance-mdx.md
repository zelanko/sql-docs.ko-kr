---
title: LinRegVariance (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b3ae56238623c41d29ccb388a5aaa178352af196
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208746"
---
# <a name="linregvariance-mdx"></a>LinRegVariance(MDX)


  집합의 선형 회귀를 계산 하 고 회귀선을 사용 하 여 연관 된 분산을 반환 합니다 y = ax + b입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
LinRegVariance(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression_y*  
 Y축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *Numeric_Expression_x*  
 X축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 최소 제곱법을 사용하는 선형 회귀는 일련의 점에 대해 가장 적합한 선인 회귀선의 수식을 계산합니다. 회귀선은 다음 수식을 여기서는 기울기 하 고 b는 절편입니다.  
  
 y = ax+b  
  
 합니다 **LinRegVariance** 함수 계산 지정된 setagainst y 축에 대 한 값을 가져오는 첫 번째 숫자 식입니다. 다음 함수를 지정 하 여 x 축 값을 가져오려면 지정된 setagainst는 두 번째 숫자 식에를 평가 합니다. 두 번째 숫자 expressionis 지정 하지 않으면 함수는 x 축에 대 한 지정된 된 집합에서 셀의 현재 컨텍스트 값으로 사용 합니다. X축 인수를 지정하지 않는 방식은 Time 차원에서 자주 사용됩니다.  
  
 점의 집합을 구한 후 합니다 **LinRegVariance** 함수 지점에 대 한 선형 수식의 적합도 설명 하는 통계 분산을 반환 합니다.  
  
> [!NOTE]  
>  합니다 **LinRegVariance** 함수는 빈 셀 이나 텍스트 또는 논리 값을 포함 하는 셀은 무시 합니다. 그러나 값이 0인 셀은 포함시킵니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Unit Sales 및 Store Sales 측정값의 점에 대한 선형 수식의 적합도를 설명하는 통계 분산을 반환합니다.  
  
```  
LinRegVariance(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
