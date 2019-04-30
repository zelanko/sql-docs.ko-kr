---
title: SetToArray (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0e545cb4b41f1a0d60e471c15753a82079978ee5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149304"
---
# <a name="settoarray-mdx"></a>SetToArray(MDX)


  사용자 정의 함수에서 사용하기 위해 하나 이상의 집합을 배열로 변환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SetToArray(Set_Expression1 [ ,Set_Expression2,...n ][ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression1*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression2*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **SetToArray** 함수 집합 하나 이상의 사용자 정의 함수에서 사용할 배열로 변환 합니다. 결과 배열의 차원 수는 지정된 집합의 수와 같습니다.  
  
 숫자 식(옵션)은 배열 셀에 값을 제공할 수 있습니다. 숫자 식이 지정되지 않은 경우 현재 컨텍스트에서 집합의 크로스 조인이 계산됩니다.  
  
 결과 배열의 셀 좌표는 목록에서 집합의 위치에 해당됩니다. 예를 들어 `SA`, `SB` 및 `SC`라는 3개의 집합이 있다고 가정해 보십시오. 이러한 각 집합에는 두 개의 요소가 포함됩니다. MDX 문인 `SetToArray(SA, SB, SC)`는 다음과 같은 3차원 배열을 만듭니다.  
  
```  
(SA1, SB1, SC1) (SA2, SB1, SC1) (SA1, SB2, SC1) (SA2, SB2, SC1)   
(SA1, SB1, SC2) (SA2, SB1, SC2) (SA1, SB2, SC2) (SA2, SB2, SC2)   
```  
  
> [!NOTE]  
>  반환 형식은 합니다 **SetToArray** 함수는 VARIANT 형식의 VT_ARRAY입니다. 따라서 출력은 **SetToArray** 함수는 사용자 정의 함수에 대 한 입력 으로만 사용 해야 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 배열을 반환합니다.  
  
```  
SetToArray([Geography].[Geography].Members, [Measures].[Internet Sales Amount])  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
