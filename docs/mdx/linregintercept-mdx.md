---
title: LinRegIntercept (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b8368039e1c8cd373ff74d66ff4b3507e5802c1
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579045"
---
# <a name="linregintercept-mdx"></a>LinRegIntercept(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  집합의 선형 회귀를 계산 하 고 회귀선에서 x 절편 값을 반환 y = ax + b 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
LinRegIntercept(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression_y*  
 Y축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *Numeric_Expression_x*  
 X축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 최소 제곱법을 사용하는 선형 회귀는 일련의 점에 대해 가장 적합한 선인 회귀선의 수식을 계산합니다. 회귀선은 다음 수식을 여기서는 기울기가 고 b는 절편:  
  
 y = ax+b  
  
 **LinRegIntercept** 함수는 y 축에 대 한 값을 가져오는 첫 번째 숫자 식에 대해 지정 된 집합을 계산 합니다. 그런 다음 두 번째 숫자 식(지정된 경우)에 대해 지정된 집합을 계산하여 X축 값을 구합니다. 두 번째 숫자 식이 지정되지 않은 경우 이 함수는 지정된 집합의 현재 셀 컨텍스트를 X축 값으로 사용합니다. X축 인수를 지정하지 않는 방식은 Time 차원에서 자주 사용됩니다.  
  
 요소의 집합을 가져온 후의 **LinRegIntercept** 함수 (위 수식의 b)는 회귀선의 절편을 반환 합니다.  
  
> [!NOTE]  
>  **LinRegIntercept** 함수는 빈 셀 이나 텍스트 또는 논리 값을 포함 하는 셀은 무시 합니다. 그러나 값이 0인 셀은 포함시킵니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Unit Sales 및 Store Sales 측정값에 대한 회귀선의 절편을 반환합니다.  
  
```  
LinRegIntercept(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
