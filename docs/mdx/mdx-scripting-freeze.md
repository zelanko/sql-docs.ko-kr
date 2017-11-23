---
title: "FREEZE 문 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: FREEZE
dev_langs: kbMDX
helpviewer_keywords:
- FREEZE statement
- locking cell values [MDX]
ms.assetid: 59f1e860-6f37-41af-97d6-7708bdaac933
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f0be995f39d3498ad8bcfe6a010de0c0b5c8c293
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-scripting---freeze"></a>MDX 스크립팅-고정
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 하위 큐브의 셀 값을 현재 값으로 잠급니다. 셀 값이 잠기면 이 셀은 다른 셀이 변경되어도 영향을 받지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>인수  
 *Subcube_Expression*  
 하위 큐브를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **고정** 문은 지정 된 하위 큐브에서 셀 값을 잠가서, 이후 계산에 해당 값을 변경 스크립트 전달는 MDX의 이후 문이 방지 합니다.  
  
 다음 예에서 A와 B는 MDX 계산 스크립트의 하위 큐브를 나타냅니다.  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 여기서 A와 B 모두 3과 같습니다.  
  
 이제 삽입는 **고정** 함수를 A 하위 큐브를 잠급니다.  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 그러면 A는 2가 되고 B는 3이 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 스크립팅 문 &#40; Mdx&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
