---
title: Var (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: VAR
dev_langs: kbMDX
helpviewer_keywords: Var function [MDX]
ms.assetid: 5575b68e-ebc1-4eaf-9547-1321d495ea62
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 49076ba34e8f6ffb193c2e285cd9a67766d1d987
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="var-mdx"></a>Var(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  비편향된 모집단 수식을 사용 하 여 집합에 대해 계산 된 숫자 식의 표본 분산을 반환 합니다 (으로 나누는  *n* ).  
  
## <a name="syntax"></a>구문  
  
```  
  
Var(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **Var** 함수는 지정 된 집합에 대해 계산 된 지정 된 숫자 식의 비편향된 분산을 반환 합니다.  
  
 **Var** 함수는 비편향된 모집단 수식을 사용 및 [VarP](../mdx/varp-mdx.md) 함수는 편향된 모집단 수식을 사용 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
