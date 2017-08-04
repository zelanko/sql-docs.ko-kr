---
title: "함수 (MDX 구문) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- MDX [Analysis Services], functions
- Multidimensional Expressions [Analysis Services], functions
- functions [MDX]
ms.assetid: 74ca5e79-1f33-4795-9d68-98eff9c190c1
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 414a3048ec4fead73ed406914d2ee042778ee2cd
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="functions-mdx-syntax"></a>함수(MDX 구문)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  MDX에는 특정 작업을 수행하는 여러 범주의 내장 함수가 있습니다. 다음 표에서는 MDX에서 사용 가능한 함수 범주를 나열합니다.  
  
> [!NOTE]  
>  개별 함수에 대 한 자세한 내용은 참조 [MDX 함수 참조 &#40; Mdx&#41; ](../mdx/mdx-function-reference-mdx.md).  
  
|함수 범주|Description|  
|-----------------------|-----------------|  
|배열 함수|저장 프로시저에서 사용할 배열을 제공합니다.<br /><br /> 자세한 내용은 참조 [를 사용 하 여 저장 프로시저 &#40; Mdx&#41; ](../mdx/using-stored-procedures-mdx.md).|  
|차원 함수|계층, 수준 또는 멤버에서 차원으로 참조를 반환합니다.<br /><br /> 자세한 내용은 참조 [를 사용 하 여 차원, 계층 및 수준 함수](../mdx/using-dimension-hierarchy-and-level-functions.md)합니다.|  
|계층 함수|수준 또는 멤버에서 계층으로 참조를 반환합니다.<br /><br /> 자세한 내용은 참조 [를 사용 하 여 차원, 계층 및 수준 함수](../mdx/using-dimension-hierarchy-and-level-functions.md)합니다.|  
|수준 함수|멤버, 차원, 계층 또는 문자열 식에서 수준으로 참조를 반환합니다.<br /><br /> 자세한 내용은 참조 [를 사용 하 여 차원, 계층 및 수준 함수](../mdx/using-dimension-hierarchy-and-level-functions.md)합니다.|  
|논리 함수|개체 및 식에 대한 논리 연산과 비교를 수행합니다.<br /><br /> 자세한 내용은 참조 [논리 함수를 사용 하 여](../mdx/using-logical-functions.md)합니다.|  
|멤버 함수|다른 개체 또는 문자열 식에서 멤버로 참조를 반환합니다.<br /><br /> 자세한 내용은 참조 [멤버 함수를 사용 하 여](../mdx/using-member-functions.md)합니다.|  
|숫자 함수|개체 및 식에 대해 수학 및 통계 함수를 수행합니다.<br /><br /> 자세한 내용은 참조 [수치 연산 함수를 사용 하 여](../mdx/using-mathematical-functions.md)합니다.|  
|집합 함수|다른 개체 또는 문자열 식에서 집합으로 참조를 반환합니다.<br /><br /> 자세한 내용은 참조 [설정 함수를 사용 하 여](../mdx/using-set-functions.md)합니다.|  
|문자열 함수|다른 개체 또는 서버에서 문자열 값을 반환합니다.<br /><br /> 자세한 내용은 참조 [문자열 함수를 사용 하 여](../mdx/using-string-functions.md)합니다.|  
|튜플 함수|집합 또는 문자열 식에서 튜플로 참조를 반환합니다.<br /><br /> 자세한 내용은 튜플 함수 사용을 참조하십시오.|  
  
## <a name="uses-of-functions"></a>함수 사용  
 임의의 MDX 식에서 함수를 사용하거나 포함시킬 수 있습니다. 함수를 중첩(어떤 함수를 다른 함수 내에서 사용하는 것)할 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 구문 요소 &#40; Mdx&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  

