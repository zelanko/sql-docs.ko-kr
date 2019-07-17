---
title: '&lt;&gt; (같지 않음) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 032505ee0714bc10baa698b1a229e5456710c81d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088325"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; (같지 않음) (MDX)


  하나의 MDX 식의 값이 다른 MDX 식의 값과 다른지 확인하는 비교 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>매개 변수  
 *MDX_Expression*  
 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 다음 조건을 기반으로 하는 부울 값입니다.  
  
-   **true** 매개 변수가 모두 null이 아닌 경우이 고 두 번째 매개 변수를 첫 번째 매개가 아닌 경우.  
  
-   **false** 매개 변수가 모두 null이 아닌 경우이 고 첫 번째 매개 변수가 두 번째 매개 변수와 같은 경우입니다.  
  
-   매개 변수 중 하나가 Null이거나 둘 다 Null인 경우 Null입니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
