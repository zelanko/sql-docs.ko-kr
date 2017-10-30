---
title: CalculationCurrentPass (MDX) | Microsoft Docs
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
- CALCULATIONCURRENTPASS
dev_langs:
- kbMDX
helpviewer_keywords:
- CalculationCurrentPass function
ms.assetid: 7069f7a0-8ec8-4293-8db3-b35b9327f437
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f2510f0db6f5a2895ce00514595306ac4849b357
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="calculationcurrentpass-mdx"></a>CalculationCurrentPass(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
  

