---
title: LinRegR2 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e38df1a24b76ee40aae3a5ab3c28dd9bca2b310
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905527"
---
# <a name="linregr2-mdx"></a>LinRegR2(MDX)


  집합의 선형 회귀를 계산 하 고 결정 계수 R<sup>2</sup>를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
LinRegR2(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
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
  
 **LinRegR2** 함수는 첫 번째 숫자 expressionto 대해 지정 된 setagainst를 계산 하 여 y 축 값을 구합니다. 그런 다음 두 번째 숫자 식(지정된 경우)에 대해 지정된 집합을 계산하여 X축 값을 구합니다. 두 번째 숫자 expressionis가 지정 되지 않은 경우이 함수는 지정 된 집합에 있는 셀의 현재 컨텍스트를 x 축 값으로 사용 합니다. Axisargument를 지정 하는 것은 시간 차원에서 자주 사용 됩니다.  
  
 점의 집합을 구한 후 **LinRegR2** 함수는 요소에 대 한 선형 수식의 적합도를 설명 하는 통계 R<sup>2</sup> 를 반환 합니다.  
  
> [!NOTE]  
>  **LinRegR2** 함수는 빈 셀 이나 텍스트 또는 논리 값을 포함 하는 셀은 무시 합니다. 그러나 값이 0인 셀은 포함시킵니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 unit sales 및 store sales 측정값의 점에 대 한 선형 회귀 수식의 적합 함을 설명 하는 통계 R<sup>2</sup> 를 반환 합니다.  
  
```  
LinRegR2(LastPeriods(10), [Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
