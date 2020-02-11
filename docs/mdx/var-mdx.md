---
title: Var (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 96bb307607792a3846ee6566027457a05ce3b905
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037931"
---
# <a name="var-mdx"></a>Var(MDX)


  *N*으로 나누는 비편향 모집단 수식을 사용 하 여 집합에 대해 계산 된 숫자 식의 표본 분산을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Var(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **Var** 함수는 지정 된 집합에 대해 계산 된 지정 된 숫자 식의 비편향 분산을 반환 합니다.  
  
 **Var** 함수는 비편향 모집단 수식을 사용 하 고, [VarP](../mdx/varp-mdx.md) 함수는 편향 모집단 수식을 사용 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
