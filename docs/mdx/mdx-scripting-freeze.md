---
title: FREEZE 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cd652a9f308bd7a564a61d165f9c47875a900737
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741972"
---
# <a name="mdx-scripting---freeze"></a>MDX 스크립팅-고정


  지정한 하위 큐브의 셀 값을 현재 값으로 잠급니다. 셀 값이 잠기면 이 셀은 다른 셀이 변경되어도 영향을 받지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>인수  
 *Subcube_Expression*  
 하위 큐브를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 스크립팅 문 &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
