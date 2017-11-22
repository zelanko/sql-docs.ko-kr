---
title: "IF 문 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: statements [MDX], IF
ms.assetid: 8830cce5-9e06-4f89-a555-295bb0d0a8a1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c5eaeffbc4ede2bedf0d85d8ef0ec4b40fb1993b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-scripting---if"></a>MDX 스크립팅-IF
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  조건이 True인 경우 문을 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 True 또는 False를 반환하는 부울로 계산되는 MDX 식입니다.  
  
 *할당*  
 하위 큐브 또는 계산 속성에 값을 할당하는 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 IF 문은 달리 제어 흐름에 사용 된 [IIf &#40; Mdx&#41; ](../mdx/iif-mdx.md) 함수 및 [CASE 문 &#40; Mdx&#41; ](../mdx/case-statement-mdx.md) 있는 수에 사용할 값 이나 개체를 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Customers 차원에 있는 Customers Geography 계층의 Country 수준으로 범위를 제한합니다. 현재 측정값이 Internet Sales Amount이면 Internet Sales Amount는 10으로 설정됩니다.  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
