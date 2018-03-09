---
title: CalculationCurrentPass (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: CALCULATIONCURRENTPASS
dev_langs: kbMDX
helpviewer_keywords: CalculationCurrentPass function
ms.assetid: 7069f7a0-8ec8-4293-8db3-b35b9327f437
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 24c3334682c381d3fe23c35435979a239aeafc94
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="calculationcurrentpass-mdx"></a>CalculationCurrentPass(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 쿼리 컨텍스트에 대한 큐브의 현재 계산 패스를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CalculationCurrentPass()  
```  
  
## <a name="remarks"></a>주의  
 **CalculationCurrentPass** 함수에 대 한 현재 쿼리 컨텍스트의 계산 패스의 0부터 시작 하는 인덱스를 반환 합니다. 자동 재귀 해결 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)],이 함수는 실제로 거의 사용 하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CalculationPassValue &#40; Mdx&#41;](../mdx/calculationpassvalue-mdx.md)   
 [IIf &#40; Mdx&#41;](../mdx/iif-mdx.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
