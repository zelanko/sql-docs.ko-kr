---
title: 부모-자식 차원 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a9f9cda883822d093db624a4580a94093120ba41
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021430"
---
# <a name="parent-child-dimension"></a>부모-자식 차원
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  부모-자식 계층은 부모 특성이 포함된 표준 차원의 계층입니다. 부모 특성은 차원 주 테이블 내의 *자체 참조 관계*또는 *셀프 조인*을 설명합니다. 부모-자식 계층은 단일 부모 특성에서 생성됩니다. 계층에 존재하는 수준은 부모 특성과 관련된 멤버 간 부모-자식 관계에서 가져오므로 부모-자식 계층에는 하나의 수준만 할당됩니다. 부모-자식 계층의 멤버 위치는 부모 특성의 **KeyColumns** 및 **RootMemberIf** 속성에 따라 결정되지만 한 수준의 멤버 위치는 부모 특성의 **OrderBy** 속성에 따라 결정됩니다. 특성 속성에 대한 자세한 내용은 [특성 및 특성 계층](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)을 참조하세요.  
  
 부모-자식 계층의 수준 간 부모-자식 관계로 인해 일부 리프가 아닌 멤버는 자식 멤버에서 집계한 데이터뿐만 아니라 기본 데이터 원본에서 파생된 데이터를 가질 수도 있습니다.  
  
## <a name="dimension-schema"></a>차원 스키마  
 부모-자식 계층의 차원 스키마는 차원 주 테이블에 있는 자체 참조 관계에 따라 다릅니다. 예를 들어 다음 다이어그램에서는 **예제 데이터베이스의** DimOrganization [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] 차원 주 테이블을 보여 줍니다.  
  
 ![DimOrganization 테이블의 자체 참조 조인](../../analysis-services/multidimensional-models/media/dimorganization.gif "DimOrganization 테이블의 자체 참조 조인")  
  
 이 차원 테이블에서 **ParentOrganizationKey** 열은 **OrganizationKey** 기본 키 열과 외래 키 관계에 있습니다. 즉, 이 테이블의 각 레코드는 부모-자식 관계를 통해 테이블의 다른 레코드와 관련될 수 있습니다. 이러한 종류의 자체 조인은 일반적으로 부서 내 직원 관리 구조와 같은 조직 엔터티 데이터를 나타내는 데 사용됩니다.  
  
## <a name="hierarchies-and-levels"></a>계층 및 수준  
 부모-자식 관계가 없는 차원은 특성을 그룹화하고 정렬하여 계층을 구성합니다. 이러한 차원에서는 계층에 대한 수준 이름이 특성 이름에서 파생됩니다.  
  
 그러나 부모-자식 차원은 차원 주 테이블에 포함된 데이터를 검사하여 부모-자식 계층을 구성한 다음 테이블에 있는 레코드 간의 부모-자식 관계를 평가합니다. 부모-자식 계층에 대한 자세한 내용은 [사용자 계층](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)을 참조하세요.  
  
 부모-자식 계층에서는 계층의 수준 이름이 계층을 만드는 데 사용되는 특성에서 파생되지 않습니다. 대신 이러한 차원은 명명 템플릿을 사용하여 자동으로 수준 이름을 만듭니다. 명명 템플릿은 특성이 특성 계층을 생성하는 방법을 제어하는 부모 특성의 수준에서 지정할 수 있는 문자열 식입니다. 부모 특성의 명명 템플릿을 설정하는 방법에 대한 자세한 내용은 [특성 및 특성 계층](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)을 참조하세요.  
  
## <a name="data-members"></a>데이터 멤버  
 일반적으로 차원의 리프 멤버는 기본 데이터 원본에서 직접 파생된 데이터를 포함하는 반면 리프가 아닌 멤버는 자식 멤버에 대해 수행된 집계에서 파생된 데이터를 포함합니다.  
  
 그러나 부모-자식 계층에는 자식 멤버에서 집계되는 데이터뿐 아니라 기본 데이터 원본에서 파생되는 데이터를 포함하는 리프가 아닌 멤버가 있을 수 있습니다. 부모-자식 계층의 이러한 리프가 아닌 멤버에 대해서는 기본 팩트 테이블 데이터가 포함된 특별한 시스템 생성 자식 멤버를 만들 수 있습니다. *데이터 멤버*라고 하는 이러한 특수 자식 멤버에는 리프가 아닌 멤버와 직접 연결되며 리프가 아닌 멤버의 하위 항목에서 계산되는 요약 값에 독립적인 값이 포함됩니다. 데이터 멤버에 대한 자세한 내용은 [부모-자식 계층의 특성](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [부모-자식 계층의 특성](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)   
 [데이터베이스 차원 속성](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)  
  
  
