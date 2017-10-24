---
title: "큐브 셀 (Analysis Services-다차원 데이터) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- storing data [Analysis Services], cells
- hierarchies [Analysis Services], cells
- OLAP objects [Analysis Services], cells
- data members [Analysis Services]
- cubes [Analysis Services], cells
- empty cells [Analysis Services]
- nonleaf members
- cubes [Analysis Services], examples
- storage [Analysis Services], cells
- nonleaf cells
- calculated cells [Analysis Services]
- dimensions [Analysis Services], cells
- cells [Analysis Services]
- leaf members
- leaf cells
ms.assetid: 9945773c-a43b-40d4-91cf-3d2ebc90bca5
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7da5c513675b85a209e76da5787828eb31be24f8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="cube-cells-analysis-services---multidimensional-data"></a>큐브 셀(Analysis Services - 다차원 데이터)
  큐브는 셀로 이루어져 있으며 셀은 측정값 그룹과 차원으로 구성됩니다. 셀은 큐브의 모든 차원에서 한 멤버 큐브의 고유한 논리적 교집합을 나타냅니다. 예를 들어 아래 다이어그램의 큐브는 Source, Route 및 Time이라는 세 차원으로 이루어지며 두 측정값을 갖는 측정값 그룹을 하나 포함합니다.  
  
 ![단일 셀을 식별 하는 큐브 다이어그램](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro5.gif "단일 셀을 식별 하는 큐브 다이어그램")  
  
 이 다이어그램에서 회색으로 표시된 단일 셀은 다음 멤버의 교집합입니다.  
  
-   경로 차원의 항공 멤버  
  
-   원본 유형 차원의 아프리카 멤버  
  
-   시간 차원의 4사분기 멤버  
  
-   패키지 측정값  
  
## <a name="leaf-and-nonleaf-cells"></a>리프 셀 및 리프가 아닌 셀  
 큐브의 셀 값은 여러 방법을 사용하여 얻을 수 있습니다. 이전 예에서 셀 값 수 직접 검색할 수는 큐브의 팩트 테이블에서 해당 셀을 식별 하는 데 사용 하는 모든 멤버는 *리프 멤버*합니다. 리프 멤버에는 계층적으로 자식 멤버가 없으며 대개 차원 테이블의 단일 레코드를 참조합니다. 이러한 유형의 셀 라고는 *리프 셀*합니다.  
  
 하지만 셀을 사용 하 여 식별할 수도 있습니다 *리프가 아닌 멤버*합니다. 리프가 아닌 멤버는 하나 이상의 자식 멤버가 있는 멤버입니다. 이 경우 셀 값은 대개 리프가 아닌 멤버와 연결된 자식 멤버의 집계에서 파생됩니다. 예를 들어 다음과 같은 멤버와 차원의 교집합은 집계를 통해 값이 제공되는 셀을 참조합니다.  
  
-   경로 차원의 항공 멤버  
  
-   원본 유형 차원의 아프리카 멤버  
  
-   Time 차원의 하반기 멤버  
  
-   패키지 멤버  
  
 Time 차원의 하반기 멤버는 리프가 아닌 멤버입니다. 따라서 이 멤버와 연결된 모든 값은 다음 다이어그램에서와 같이 집계된 값이어야 합니다.  
  
 ![하반기 멤버에 대 한 세 번째 및 네 번째 분기 셀](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro6.gif "하반기 멤버에 대 한 세 번째 및 네 번째 분기 셀")  
  
 3사분기와 4사분기 멤버에 대한 집계가 합계라고 가정하면 지정한 셀 값은 위 다이어그램에서 회색으로 표시된 리프 셀을 모두 합한 값인 400입니다. 셀의 값이 다른 셀의 집계에서 파생 된, 있기 때문에 지정된 된 셀 간주 되는 *리프가 아닌 셀*합니다.  
  
 사용자 지정 롤업 및 멤버 그룹을 사용하는 멤버와 사용자 지정 멤버에 대해 파생된 셀 값도 비슷한 방식으로 처리됩니다. 그러나 계산 멤버에 대해 파생된 셀 값은 계산 멤버를 정의하는 데 사용하는 MDX(Multidimensional Expressions)만을 기반으로 합니다. 실제로 관련된 셀 데이터가 없는 경우도 있습니다. 자세한 내용은 참조 [부모-자식 차원의 사용자 지정 롤업 연산자](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-custom-rollup-operators.md), [사용자 지정 멤버 수식 정의](../../analysis-services/multidimensional-models/attribute-properties-define-custom-member-formulas.md), 및 [계산](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)합니다.  
  
## <a name="empty-cells"></a>빈 셀  
 큐브의 모든 셀에 값이 있어야 하는 것은 아닙니다. 큐브에 데이터가 없는 교집합이 있을 수 있습니다. 빈 셀이라고 하는 이러한 교집합은 큐브 내에 측정값이 있는 차원 특성의 모든 교집합에 팩트 테이블의 해당 레코드가 포함되는 것이 아니기 때문에 큐브에서 종종 나타납니다. 큐브에서 큐브 셀의 총 수에 빈 셀의 비율 자주 라고는 *희박도* 큐브의 합니다.  
  
 예를 들어 아래 다이어그램에 표시된 큐브의 구조는 이 항목의 다른 예제와 비슷합니다. 그러나 이 예제에서는 3사분기 아프리카행 항공 수송 또는 4사분기 오스트레일리아행 항공 수송이 없습니다. 이러한 차원과 측정값의 교집합을 지원하는 데이터가 팩트 테이블에 없으므로 해당 교집합의 셀은 빈 셀이 됩니다.  
  
 ![빈 셀을 식별 하는 큐브 다이어그램](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro7.gif "빈 셀을 식별 하는 큐브 다이어그램")  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], 빈 셀에는 특별 한 특징이 있습니다. 빈 셀은 크로스 조인, 카운트 등의 결과를 달라지게 할 수 있으므로 많은 MDX 함수가 계산을 위한 목적으로 빈 셀을 무시할 수 있는 기능을 제공합니다. 자세한 내용은 참조 [다차원 식 &#40; Mdx&#41; 참조](../../mdx/multidimensional-expressions-mdx-reference.md), 및 [주요 MDX &#40; 개념 Analysis Services &#41; ](../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md).  
  
## <a name="security"></a>보안  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 셀 데이터에 대한 액세스는 역할 수준에서 관리되며 MDX 식을 사용하여 정밀하게 제어할 수 있습니다. 자세한 내용은 참조 [데이터 &#40; 차원에 대 한 사용자 지정 액세스 부여 Analysis Services &#41; ](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md), 및 [데이터 &#40; 셀에 대 한 사용자 지정 액세스 부여 Analysis Services &#41; ](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md).  
  
## <a name="see-also"></a>관련 항목:  
 [큐브 저장소 &#40; Analysis Services-다차원 데이터 &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)   
 [집계 및 집계 디자인](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  

