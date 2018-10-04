---
title: 부모-자식 계층의 특성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data members [Analysis Services]
- nonleaf members
- MembersWithDataCaption property
- members [Analysis Services]
- members [Analysis Services], data
- leaf members
- parent-child dimensions [Analysis Services]
- MembersWithData property
ms.assetid: 249971cc-4bcd-44f1-8241-bdacc04d3d38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 500740207ea4c020ef7845b5de9e993655d4295d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219653"
---
# <a name="attributes-in-parent-child-hierarchies"></a>부모-자식 계층의 특성
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 차원의 멤버 내용에 대한 일반적인 가정이 있습니다. 즉, 리프 멤버에는 기본 데이터 원본에서 직접 파생되는 데이터가 있고 리프가 아닌 멤버에는 자식 멤버에 대해 수행된 집계에서 파생되는 데이터가 있다고 가정합니다.  
  
 그러나 부모-자식 계층에서는 리프가 아닌 멤버 중 일부가 자식 멤버에서 집계된 데이터 외에도 기본 데이터 원본에서 파생된 데이터를 포함할 수 있습니다. 부모-자식 계층의 이러한 리프가 아닌 멤버에 대해서는 기본 팩트 테이블 데이터가 포함된 특별한 시스템 생성 자식 멤버가 생성됩니다. 이러한 멤버를 *데이터 멤버*라고 하며 해당 값은 리프가 아닌 멤버와 직접 연결되며 리프가 아닌 멤버의 하위 항목으로부터 계산되는 요약 값에 독립적입니다.  
  
 데이터 멤버는 부모-자식 계층이 있는 차원에만 사용할 수 있으며 부모 특성에서 허용되는 경우에만 표시됩니다. 차원 디자이너를 사용하여 데이터 멤버의 표시 여부를 제어할 수 있습니다. 데이터 멤버를 노출 하려면 설정 합니다 `MembersWithData` 부모 특성의 속성 `NonLeafDataVisible.` 부모 특성에 포함 된 데이터 멤버를 숨기려면 설정 합니다 `MembersWithData` 부모 특성을 속성 `NonLeafDataHidden`.  
  
 이 설정은 리프가 아닌 멤버의 일반 집계 동작을 재정의하지 않습니다. 데이터 멤버는 항상 집계를 위해 자식 멤버로 포함됩니다. 그러나 사용자 지정 롤업 수식을 사용하여 일반 집계 동작을 재정의할 수 있습니다. 다차원 식 (MDX) [DataMember](/sql/mdx/datamember-mdx) 의 값에 관계 없이 연결 된 데이터 멤버의 값에 액세스할 수 있도록 함수를 사용 합니다 `MembersWithData` 속성입니다.  
  
 합니다 `MembersWithDataCaption` 부모 특성의 속성은 제공 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터 멤버의 멤버 이름을 생성 하는 데 사용 하는 명명 템플릿을 사용 하 여 합니다.  
  
## <a name="using-data-members"></a>데이터 멤버 사용  
 데이터 멤버는 부모-자식 계층이 있는 조직 차원의 측정값을 집계하는 경우 유용합니다. 예를 들어 아래 다이어그램에서는 제품의 총 판매량을 나타내는 세 가지 수준이 있는 차원을 보여 줍니다. 첫 번째 수준은 모든 영업 사원의 총 판매량을 보여 줍니다. 두 번째 수준에는 영업 관리자별로 그룹화된 모든 영업 담당자의 총 판매량이 포함되고 세 번째 수준에는 영업 사원별로 그룹화된 모든 영업 담당자의 총 판매량이 포함됩니다.  
  
 ![세 가지 수준으로 총 판매량 차원](../media/agdatamember1.gif "세 가지 수준으로 총 판매량 차원")  
  
 일반적으로 Sales Manager 1 멤버의 값은 Salesperson 1 및 Salesperson 2 멤버의 값을 집계하여 파생됩니다. 그러나 Sales Manager 1도 제품을 판매할 수 있어 Sales Manager 1에 관련된 총 판매량이 있을 수 있으므로 팩트 테이블에서 파생된 데이터가 해당 멤버에 포함될 수 있습니다.  
  
 또한 각 영업 담당자 멤버에 대한 개별 커미션이 다를 수 있습니다. 이 경우 자신의 영업 사원이 거둔 총 판매량과는 반대로 두 가지 기준을 사용하여 영업 관리자의 개별 총 판매량에 대한 커미션을 계산합니다. 그러므로 리프가 아닌 멤버에게는 기본 팩트 테이블 데이터에 액세스할 수 있는지 여부가 중요합니다. MDX `DataMember` Sales Manager 1 멤버의 개별 총 판매량을 검색 하려면 함수를 사용할 수 있으며, 사용자 지정 롤업 식을 제공 된 gross Sales Manager 1 멤버의 집계 값에서 데이터 멤버를 제외할 수 해당 멤버와 연결 된 판매 직원의 판매 볼륨입니다.  
  
## <a name="see-also"></a>관련 항목  
 [차원 특성 속성 참조](dimension-attribute-properties-reference.md)   
 [부모-자식 계층](parent-child-dimension.md)  
  
  
