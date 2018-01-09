---
title: "명명 된 집합에서 MDX (MDX)을 빌딩 | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], named sets
- named sets [MDX]
- sets [MDX]
- MDX [Analysis Services], named sets
- queries [MDX], named sets
- set expressions [MDX]
ms.assetid: 213b0035-e96d-4ba0-83f2-ded206905603
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: aff5c819f15c6c1117ded70fe34169811d4f3bd1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-named-sets---building-named-sets"></a>명명 된 집합-명명 된 집합 작성 MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]집합 식 길고 복잡 한 선언이 되며 따라서를 이해 하기 어려울 수 있습니다. 또는 식 집합이 너무 자주 사용되어 반복적으로 집합을 정의하는 작업이 부담이 될 수 있습니다. 이렇게 길고, 복잡하며, 일상적으로 사용되는 식을 쉽게 만들기 위해 MDX에서는 *명명된 집합*이라는 식을 사용할 수 있습니다.  
  
 기본적으로 명명된 집합은 별칭이 할당된 집합 식입니다. 명명된 집합은 일반적으로 통합이 가능한 멤버나 함수를 집합으로 통합할 수 있습니다. MDX는 명명된 집합 별칭을 집합 식으로 취급하기 때문에 집합 식이 사용되는 모든 곳에 이러한 별칭을 사용할 수 있습니다.  
  
 다음 컨텍스트 중 하나가 포함되도록 명명된 집합을 정의할 수 있습니다.  
  
-   **쿼리 범위** MDX 쿼리의 일부로 정의되는 명명된 집합을 만들어서 해당 범위가 쿼리로 제한되도록 하려면 WITH 키워드를 사용합니다. 그런 다음 MDX SELECT 문 내에서 명명된 집합을 사용할 수 있습니다. 이 방식을 사용할 경우, WITH 키워드를 사용하여 만든 명명된 집합은 SELECT 문을 배포하지 않아도 변경할 수 있습니다.  
  
     WITH 키워드를 사용하여 명명된 집합을 만드는 방법에 대한 자세한 내용은 [쿼리 범위 명명된 집합 만들기&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md)를 참조하세요.  
  
-   **세션 범위** 범위가 쿼리 컨텍스트보다 넓은 즉, 범위가 MDX 세션의 수명인 명명된 집합을 만들려면 CREATE SET 문을 사용합니다. CREATE SET 문을 사용하여 정의된 명명된 집합은 해당 세션의 모든 MDX 쿼리에서 사용할 수 있습니다. 예를 들어 CREATE SET 문은 여러 쿼리에서 하나의 집합을 계속적으로 다시 사용하는 클라이언트 응용 프로그램에 적합합니다.  
  
     CREATE SET 문을 사용하여 세션에서 명명된 집합을 만드는 방법에 대한 자세한 내용은 [세션 범위 명명된 집합 만들기&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-session-scoped-named-sets.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [SELECT 문&#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)   
 [SET 문 &#40; 만들기 Mdx&#41;](../../../mdx/mdx-data-definition-create-set.md)   
 [MDX 쿼리 기본 사항&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
