---
title: Var (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5a9f9461f531f3a37feac40ac1f4af03f620bd3f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581695"
---
# <a name="var-mdx"></a>Var(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  비편향된 모집단 수식을 사용 하 여 집합에 대해 계산 된 숫자 식의 표본 분산을 반환 합니다 (으로 나누는 *n*).  
  
## <a name="syntax"></a>구문  
  
```  
  
Var(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 **Var** 함수는 지정 된 집합에 대해 계산 된 지정 된 숫자 식의 비편향된 분산을 반환 합니다.  
  
 **Var** 함수는 비편향된 모집단 수식을 사용 및 [VarP](../mdx/varp-mdx.md) 함수는 편향된 모집단 수식을 사용 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
