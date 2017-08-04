---
title: VarP (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VARP
dev_langs:
- kbMDX
helpviewer_keywords:
- VarP function [MDX]
ms.assetid: feca648d-bbc8-44c8-9a0e-38f66d914c72
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4f0d30afa0147f62bea4b58661ee735deb61a429
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="varp-mdx"></a>VarP(MDX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  편향된 모집단 수식을 사용 하 여 집합에 대해 계산 된 숫자 식의 모집단 분산을 반환 합니다 (으로 나누는  *n* -1).  
  
## <a name="syntax"></a>구문  
  
```  
  
VarP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **VarP** 함수는 지정 된 집합에 대해 계산 된 지정 된 숫자 식의 편향된 분산을 반환 합니다.  
  
 **VarP** 함수는 편향된 모집단을 사용 하는 동안 수식는 [Var](../mdx/var-mdx.md) 함수는 비편향된 모집단 수식을 사용 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

