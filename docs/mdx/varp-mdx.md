---
title: VarP (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bb28851863864520a67cacbb2cb9a2a84d9fd6a1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135063"
---
# <a name="varp-mdx"></a>VarP(MDX)


  편향된 모집단 수식을 사용 하 여 집합에 대해 계산 된 숫자 식의 모집단 분산을 반환 합니다 (나누어 *n*-1).  
  
## <a name="syntax"></a>구문  
  
```  
  
VarP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 합니다 **VarP** 함수는 지정 된 집합에 대해 계산 된 지정 된 숫자 식의 편향된 분산을 반환 합니다.  
  
 **VarP** 함수는 편향된 모집단을 사용 하는 동안 수식 합니다 [Var](../mdx/var-mdx.md) 함수는 비편향된 모집단 수식을 사용 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
