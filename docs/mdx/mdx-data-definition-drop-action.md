---
title: DROP ACTION 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f47eaad9a13966abd1d08b0121fdd9c0a64a7438
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63285056"
---
# <a name="mdx-data-definition---drop-action"></a>MDX 데이터 정의 - DROP ACTION


  지정한 큐브에서 특정 동작을 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP ACTION CURRENTCUBE | Cube_Name  
   .Action_Name   
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브 이름을 지정하는 유효한 문자열 식입니다.  
  
 *Action_Name*  
 삭제할 동작의 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="see-also"></a>관련 항목  
 [CREATE ACTION 문 &#40;MDX&#41;](../mdx/mdx-data-definition-create-action.md)   
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
