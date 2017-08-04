---
title: "&lt;&gt;(같지 않음) (MDX) | Microsoft Docs"
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
- <>
dev_langs:
- kbMDX
helpviewer_keywords:
- not equal to operator (<>)
- <> (not equal to operator)
ms.assetid: b4eb3f1c-8b68-4530-a8f3-e3b8414ac789
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 94a88e2b78f577fb09396851668fcf72c7148d0e
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt;(같지 않음) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
-   **true 이면** 매개 변수가 모두 null이 고 두 번째 매개 변수를 첫 번째 매개 변수가 아닌 경우.  
  
-   **false** 경우 매개 변수가 모두 null이 고 첫 번째 매개 변수 두 번째 매개 변수입니다.  
  
-   매개 변수 중 하나가 Null이거나 둘 다 Null인 경우 Null입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 연산자 참조 &#40; Mdx&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

