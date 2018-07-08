---
title: MDX (MDX)로 셀 계산 작성 | Microsoft Docs
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
- calculated cells [MDX]
- queries [MDX], cell calculations
- cells [MDX]
- MDX [Analysis Services], calculations
- calculation subcubes [MDX]
- calculated values [MDX]
- Multidimensional Expressions [Analysis Services], cell calculations
ms.assetid: 068aea63-d419-4791-a960-3d74e76f808e
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b0a689858d4012f360e7f3893cfa844f3ecbdcf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161354"
---
# <a name="building-cell-calculations-in-mdx-mdx"></a>MDX로 셀 계산 작성(MDX)
  MDX는 계산 멤버, 사용자 지정 롤업, 사용자 지정 멤버 등 계산 값을 생성하기 위한 여러 가지 도구를 제공합니다. 하지만 이러한 기능을 사용하여 특정 셀 집합 또는 문제가 되는 단일 셀에 영향을 주기는 어렵습니다.  
  
 셀에 맞게 특별히 계산된 값을 생성하려면 MDX에서 계산 셀 기능을 사용해야 합니다. 계산 셀을 이용하면 *계산 하위 큐브*라는 특정 셀 조각을 정의하고 각 셀에 적용될 수 있는 선택 조건에 따라 계산 하위 큐브 내에 있는 각각의 모든 셀에 수식을 적용할 수 있습니다.  
  
 또한 계산 셀은 KPI에 사용되는 것과 같은 목표값 찾기 수식 또는 이론적인 분석 수식과 같은 복잡한 기능도 제공합니다. 이 정도 수준의 기능은 패스 순서의 특정 패스에 계산 수식을 적용하여 계산된 셀을 이용하여 재귀적 패스를 만들 수 있는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 의 패스 순서 기능에서 가져옵니다. 패스 순서에 대한 자세한 내용은 [패스 순서 및 계산 순서 이해&#40;MDX&#41;](mdx-data-manipulation-understanding-pass-order-and-solve-order.md)를 참조하세요.  
  
 작성 범위 측면에서, 계산 셀은 한 세션 또는 단일 쿼리 중에만 임시로 만들거나 큐브의 일부로 전체적으로 사용할 수 있다는 점에서 명명된 집합 및 계산 멤버 모두와 비슷합니다.  
  
-   **쿼리 범위** MDX 쿼리의 일부로 정의되는 계산 셀을 만들어서 해당 범위가 쿼리로 제한되도록 하려면 WITH 키워드를 사용합니다. 그런 다음 MDX SELECT 문 내에서 계산 셀을 사용할 수 있습니다. 이 방법을 사용 하 여 만든 계산된 셀을 `WITH` 키워드는 SELECT 문을 배포 하지 않아도 변경할 수 있습니다.  
  
     WITH 키워드를 사용하여 계산 멤버를 만드는 방법에 대한 자세한 내용은 [쿼리 범위 셀 계산 만들기&#40;MDX&#41;](../../multidimensional-models-olap-logical-cube-objects/calculations.md)를 참조하세요.  
  
-   **세션 범위** 범위가 쿼리 컨텍스트보다 넓은 계산 멤버, 즉 범위가 MDX 세션의 수명인 계산 멤버를 만들려면 CREATE CELL CALCULATION 또는 ALTER CUBE 문을 사용합니다.  
  
     CREATE CELL CALCULATION 또는 ALTER CUBE 문을 사용하여 세션에서 계산 셀을 만드는 방법에 대한 자세한 내용은 [세션 범위 계산 셀 만들기](mdx-cell-calculations-session-scoped-calculated-cells.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER CUBE 문 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-alter-cube)   
 [CREATE CELL CALCULATION 문 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-cell-calculation)   
 [쿼리 범위 셀 계산 만들기 &#40;MDX&#41;](../../multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [MDX 쿼리 기본 사항 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
