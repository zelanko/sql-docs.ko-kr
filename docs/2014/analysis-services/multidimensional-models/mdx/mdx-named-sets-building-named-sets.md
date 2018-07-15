---
title: 구성 집합을 MDX (MDX) 라는 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], named sets
- named sets [MDX]
- sets [MDX]
- MDX [Analysis Services], named sets
- queries [MDX], named sets
- set expressions [MDX]
ms.assetid: 213b0035-e96d-4ba0-83f2-ded206905603
caps.latest.revision: 27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f990def60c377ca84b5dde593470634f3927b496
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297463"
---
# <a name="building-named-sets-in-mdx-mdx"></a>명명된 집합을 MDX로 작성(MDX)
  식 집합은 길고 복잡한 선언이 될 수 있으므로 이해하기 어려울 수 있습니다. 또는 식 집합이 너무 자주 사용되어 반복적으로 집합을 정의하는 작업이 부담이 될 수 있습니다. 이렇게 길고, 복잡하며, 일상적으로 사용되는 식을 쉽게 만들기 위해 MDX에서는 *명명된 집합*이라는 식을 사용할 수 있습니다.  
  
 기본적으로 명명된 집합은 별칭이 할당된 집합 식입니다. 명명된 집합은 일반적으로 통합이 가능한 멤버나 함수를 집합으로 통합할 수 있습니다. MDX는 명명된 집합 별칭을 집합 식으로 취급하기 때문에 집합 식이 사용되는 모든 곳에 이러한 별칭을 사용할 수 있습니다.  
  
 다음 컨텍스트 중 하나가 포함되도록 명명된 집합을 정의할 수 있습니다.  
  
-   **쿼리 범위** MDX 쿼리의 일부로 정의되는 명명된 집합을 만들어서 해당 범위가 쿼리로 제한되도록 하려면 WITH 키워드를 사용합니다. 그런 다음 MDX SELECT 문 내에서 명명된 집합을 사용할 수 있습니다. 이 방식을 사용할 경우, WITH 키워드를 사용하여 만든 명명된 집합은 SELECT 문을 배포하지 않아도 변경할 수 있습니다.  
  
     WITH 키워드를 사용하여 명명된 집합을 만드는 방법에 대한 자세한 내용은 [쿼리 범위 명명된 집합 만들기&#40;MDX&#41;](mdx-named-sets-creating-query-scoped-named-sets.md)를 참조하세요.  
  
-   **세션 범위** 범위가 쿼리 컨텍스트보다 넓은 즉, 범위가 MDX 세션의 수명인 명명된 집합을 만들려면 CREATE SET 문을 사용합니다. CREATE SET 문을 사용하여 정의된 명명된 집합은 해당 세션의 모든 MDX 쿼리에서 사용할 수 있습니다. 예를 들어 CREATE SET 문은 여러 쿼리에서 하나의 집합을 계속적으로 다시 사용하는 클라이언트 응용 프로그램에 적합합니다.  
  
     CREATE SET 문을 사용하여 세션에서 명명된 집합을 만드는 방법에 대한 자세한 내용은 [세션 범위 명명된 집합 만들기&#40;MDX&#41;](mdx-named-sets-creating-session-scoped-named-sets.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [SELECT 문의 &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [CREATE SET 문 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-set)   
 [MDX 쿼리 기본 사항 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
