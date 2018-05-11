---
title: 부모-자식 계층의 특성 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5290199035e509d30bbe8cad7f99fb8411d40556
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="parent-child-dimension-attributes"></a>부모-자식 차원 특성
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 차원의 멤버 내용에 대한 일반적인 가정이 있습니다. 즉, 리프 멤버에는 기본 데이터 원본에서 직접 파생되는 데이터가 있고 리프가 아닌 멤버에는 자식 멤버에 대해 수행된 집계에서 파생되는 데이터가 있다고 가정합니다.  
  
 그러나 부모-자식 계층에서는 리프가 아닌 멤버 중 일부가 자식 멤버에서 집계된 데이터 외에도 기본 데이터 원본에서 파생된 데이터를 포함할 수 있습니다. 부모-자식 계층의 이러한 리프가 아닌 멤버에 대해서는 기본 팩트 테이블 데이터가 포함된 특별한 시스템 생성 자식 멤버가 생성됩니다. 이러한 멤버를 *데이터 멤버*라고 하며 해당 값은 리프가 아닌 멤버와 직접 연결되며 리프가 아닌 멤버의 하위 항목으로부터 계산되는 요약 값에 독립적입니다.  
  
 데이터 멤버는 부모-자식 계층이 있는 차원에만 사용할 수 있으며 부모 특성에서 허용되는 경우에만 표시됩니다. 차원 디자이너를 사용하여 데이터 멤버의 표시 여부를 제어할 수 있습니다. 데이터 멤버를 노출하려면 부모 특성의 **MembersWithData** 속성을 **NonLeafDataVisible**로 설정합니다. 부모 특성에 의해 포함된 데이터 멤버를 숨기려면 부모 특성의 **MembersWithData** 속성을 **NonLeafDataHidden**으로 설정합니다.  
  
 이 설정은 리프가 아닌 멤버의 일반 집계 동작을 재정의하지 않습니다. 데이터 멤버는 항상 집계를 위해 자식 멤버로 포함됩니다. 그러나 사용자 지정 롤업 수식을 사용하여 일반 집계 동작을 재정의할 수 있습니다. MDX(Multidimensional Expressions) [DataMember](../../mdx/datamember-mdx.md) 함수를 사용하면 **MembersWithData** 속성 값에 관계없이 연결된 데이터 멤버의 값에 액세스할 수 있습니다.  
  
 부모 특성의 **MembersWithDataCaption** 속성은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 데이터 멤버의 멤버 이름을 생성하는 데 사용되는 명명 템플릿을 제공합니다.  
  
## <a name="using-data-members"></a>데이터 멤버 사용  
 데이터 멤버는 부모-자식 계층이 있는 조직 차원의 측정값을 집계하는 경우 유용합니다. 예를 들어 아래 다이어그램에서는 제품의 총 판매량을 나타내는 세 가지 수준이 있는 차원을 보여 줍니다. 첫 번째 수준은 모든 영업 사원의 총 판매량을 보여 줍니다. 두 번째 수준에는 영업 관리자별로 그룹화된 모든 영업 담당자의 총 판매량이 포함되고 세 번째 수준에는 영업 사원별로 그룹화된 모든 영업 담당자의 총 판매량이 포함됩니다.  
  
 ![세 가지 수준이 있는 총 판매량 차원](../../analysis-services/multidimensional-models/media/agdatamember1.gif "세 가지 수준이 있는 총 판매량 차원")  
  
 일반적으로 Sales Manager 1 멤버의 값은 Salesperson 1 및 Salesperson 2 멤버의 값을 집계하여 파생됩니다. 그러나 Sales Manager 1도 제품을 판매할 수 있어 Sales Manager 1에 관련된 총 판매량이 있을 수 있으므로 팩트 테이블에서 파생된 데이터가 해당 멤버에 포함될 수 있습니다.  
  
 또한 각 영업 담당자 멤버에 대한 개별 커미션이 다를 수 있습니다. 이 경우 자신의 영업 사원이 거둔 총 판매량과는 반대로 두 가지 기준을 사용하여 영업 관리자의 개별 총 판매량에 대한 커미션을 계산합니다. 그러므로 리프가 아닌 멤버에게는 기본 팩트 테이블 데이터에 액세스할 수 있는지 여부가 중요합니다. MDX **DataMember** 함수를 사용하여 Sales Manager 1 멤버의 개별 총 판매량을 검색하고, 사용자 지정 롤업 식을 사용하여 Sales Manager 1 멤버의 집계 값에서 데이터 멤버를 제외함으로써 해당 멤버와 관련된 영업 사원의 판매량을 제공할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [차원 특성 속성 참조](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)   
 [부모-자식 차원](../../analysis-services/multidimensional-models/parent-child-dimension.md)  
  
  
