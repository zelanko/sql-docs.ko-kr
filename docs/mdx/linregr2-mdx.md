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
manager: kfile
ms.openlocfilehash: 42c703e703e8c557b4de8466a0cd1b686217fd4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63136211"
---
# <a name="linregr2-mdx"></a>LinRegR2(MDX)


  집합의 선형 회귀를 계산 하 고 R 결정 계수를 반환 합니다<sup>2</sup>합니다.  
  
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
  
## <a name="remarks"></a>Remarks  
 최소 제곱법을 사용하는 선형 회귀는 일련의 점에 대해 가장 적합한 선인 회귀선의 수식을 계산합니다. 회귀선은 다음 수식을 여기서는 기울기 하 고 b는 절편입니다.  
  
 y = ax+b  
  
 합니다 **LinRegR2** 함수 계산 지정된 setagainst 첫 번째 숫자 expressionto y 축에 대 한 값을 가져옵니다. 그런 다음 두 번째 숫자 식(지정된 경우)에 대해 지정된 집합을 계산하여 X축 값을 구합니다. 두 번째 숫자 expressionis 지정 하지 않으면 함수는 x 축에 대 한 지정된 된 집합에서 셀의 현재 컨텍스트 값으로 사용 합니다. X-axisargument를 지정 하지 않는 시간 차원의 자주 사용 됩니다.  
  
 점의 집합을 구한 후 합니다 **LinRegR2** 통계를 반환<sup>2</sup> 지점에 대 한 선형 수식의 적합도 설명 하는 합니다.  
  
> [!NOTE]  
>  합니다 **LinRegR2** 함수는 빈 셀 이나 텍스트 또는 논리 값을 포함 하는 셀은 무시 합니다. 그러나 값이 0인 셀은 포함시킵니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 통계를 반환<sup>2</sup> unit sales 및 store sales 측정값에 대 한 지점에 대 한 선형 회귀 수식의 적합도 설명 하는 합니다.  
  
```  
LinRegR2(LastPeriods(10), [Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
