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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905569"
---
# <a name="linregpoint-mdx"></a>LinRegPoint(MDX)


  집합의 선형 회귀를 계산 하 고 값을 반환 합니다 *y 절편* 고 회귀선 y = ax + b를 특정 x 값에 대 한.  
  
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
 최소 제곱법을 사용하는 선형 회귀는 일련의 점에 대해 가장 적합한 선인 회귀선의 수식을 계산합니다. 회귀선은 다음 수식을 여기서는 기울기 하 고 b는 절편입니다.  
  
 y = ax+b  
  
 합니다 **LinRegPoint** 함수 y 축에 대 한 값을 얻는 데는 두 번째 숫자 식에 대해 지정 된 집합을 계산 합니다. 그런 다음 세 번째 숫자 식(지정된 경우)에 대해 지정된 집합을 계산하여 X축 값을 구합니다. 세 번째 숫자 식이 지정되지 않은 경우 이 함수는 지정된 집합의 현재 셀 컨텍스트를 X축 값으로 사용합니다. X축 인수를 지정하지 않는 방식은 Time 차원에서 자주 사용됩니다.  
  
 선형 회귀선이 계산된 후 첫 번째 숫자 식에 대해 수식 값이 계산되고 반환됩니다.  
  
> [!NOTE]  
>  합니다 **LinRegPoint** 함수는 빈 셀 이나 텍스트를 포함 하는 셀은 무시 합니다. 그러나 값이 0인 셀은 포함시킵니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Unit Sales와 Store Sales 간의 통계 관계를 기준으로 지난 10개의 기간과 비교한 Unit Sales의 예측 값을 반환합니다.  
  
```  
LinRegPoint([Measures].[Unit Sales],LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
