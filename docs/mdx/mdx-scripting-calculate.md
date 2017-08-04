---
title: "CALCULATE 문 (MDX) | Microsoft Docs"
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
- CALCULATE
dev_langs:
- kbMDX
helpviewer_keywords:
- CALCULATE statement
ms.assetid: 41e196a1-d49e-487b-a42a-73e5d441ed1b
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d8e74fd0cd09e050c11d2eb403d31527402f008b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-scripting---calculate"></a>MDX 스크립팅-계산
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  큐브의 각 셀에 집계 값을 채웁니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>인수  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 사용하여 큐브를 만들면 큐브의 MDX 스크립트에 CALCULATE 문이 첫 번째 문으로 자동으로 포함됩니다. CALCULATE 문은 큐브의 각 셀이 세분성이 보다 낮은 셀에서 집계되도록 지정합니다. 셀이 집계된 후 식을 사용하여 세분성이 낮은 셀을 채우면 세분성이 높은 셀의 집계 값에 영향이 미칩니다. 대부분은 이 집계 방법을 사용하지만 이 문을 제거하거나 이 문보다 다른 문이 먼저 실행되도록 할 수도 있습니다.  
  
 MDX 스크립트 내의 중첩된 하위 큐브에는 CALCULATE 문을 포함할 수 없습니다. 중첩된 하위 큐브는 SCOPE 문을 사용하여 정의합니다. SCOPE 문에 대 한 자세한 내용은 참조 하십시오. [SCOPE 문 &#40; Mdx&#41; ](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  계산 멤버는 집계되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 스크립팅 문 &#40; Mdx&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [MDX 스크립팅 기본 사항 &#40; Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [할당 및 기타 스크립트 명령 정의](../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md)  
  
  

