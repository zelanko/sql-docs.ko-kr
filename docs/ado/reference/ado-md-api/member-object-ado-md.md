---
title: "멤버 개체 (ADO MD) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Member
helpviewer_keywords: Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6624e44343ef680c317338ea1fe32ead2aa0d9d0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="member-object-ado-md"></a>멤버 개체 (ADO MD)
멤버, 수준 또는 열 집합의 축 따라 위치의 멤버의 자식을 큐브에서 수준의 멤버를 나타냅니다.  
  
## <a name="remarks"></a>주의  
 속성을 **멤버** 에 사용 되는 컨텍스트에 따라 달라 집니다. A **멤버** 의 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 에 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) 에 [자식](../../../ado/reference/ado-md-api/children-property-ado-md.md) 속성을 반환 하는 **멤버** 에 다음 하위 수준의 멤버는 계층에서 현재 **멤버**합니다. 에 대 한는 **멤버** 의 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md), **자식** 컬렉션은 항상 비어 있습니다. 또한는 [형식](../../../ado/reference/ado-md-api/type-property-ado-md.md) 속성에만 적용 됩니다 **멤버** 의 **수준**합니다.  
  
 A **멤버** 의 **위치** 두 가지 유용한 속성을 표시할 때에 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md): [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) 및 [ ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)합니다. 이러한 속성에 액세스 되는 경우 오류가 발생 합니다는 **멤버** 의 **수준**합니다.  
  
 컬렉션과의 속성을 사용 하 여는 **멤버** 의 개체는 **수준**, 다음을 수행할 수 있습니다.  
  
-   식별 된 **멤버** 와 [이름](../../../ado/reference/ado-md-api/name-property-ado-md.md) 및 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) 속성입니다.  
  
-   표시할 때 사용할 문자열을 반환 하는 **멤버** 와 [캡션](../../../ado/reference/ado-md-api/caption-property-ado-md.md) 속성입니다.  
  
-   측정값 또는 수식을 설명 하는 의미 있는 문자열을 반환할 **멤버** 와 [설명](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성입니다.  
  
-   특성을 확인는 **멤버** 와 [형식](../../../ado/reference/ado-md-api/type-property-ado-md.md) 속성입니다.  
  
-   에 대 한 정보를 가져올는 **수준** 의 **멤버** 와 [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) 및 [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) 속성입니다.  
  
-   가져올 관련 **멤버** 에 [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) 와 [부모](../../../ado/reference/ado-md-api/parent-property-ado-md.md) 및 [자식](../../../ado/reference/ado-md-api/children-property-ado-md.md) 속성입니다.  
  
-   자식 수는 **멤버** 와 [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) 속성입니다.  
  
-   표준 ADO를 사용 하 여 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 대 한 추가 정보를 가져올 수는 **수준** 개체입니다.  
  
 컬렉션과의 속성을 사용 하 여는 **멤버** 의 **위치** 따라는 [축](../../../ado/reference/ado-md-api/axis-object-ado-md.md), 다음을 수행할 수 있습니다.  
  
-   식별 된 **멤버** 와 [이름](../../../ado/reference/ado-md-api/name-property-ado-md.md) 및 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) 속성입니다.  
  
-   표시할 때 사용할 문자열을 반환 하는 **멤버** 와 [캡션](../../../ado/reference/ado-md-api/caption-property-ado-md.md) 속성입니다.  
  
-   측정값 또는 수식을 설명 하는 의미 있는 문자열을 반환할 **멤버** 와 [설명](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성입니다.  
  
-   에 대 한 정보를 가져올는 **수준** 의 **멤버** 와 [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) 및 [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) 속성입니다.  
  
-   자식 수는 **멤버** 와 [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) 속성입니다.  
  
-   사용 하 여는 [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) 속성에 자식이 하나 이상 있는지 여부를 확인 하 고 **축** 바로이 다음 **멤버**합니다.  
  
-   사용 하 여는 [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md) 속성을 확인 하는지 여부를이 부모 **멤버** 바로 앞의 부모와 같습니다 **멤버**합니다.  
  
-   표준 ADO를 사용 하 여 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 대 한 추가 정보를 가져올 수는 **수준** 개체입니다.  
  
 **속성** 컬렉션 공급자를 제공 하는 속성을 포함 합니다. 다음 표에서 사용할 수 있는 속성을 나열 합니다. 실제 속성 목록은 공급자의 구현에 따라 달라질 수 있습니다. 사용 가능한 속성의 전체 목록은 대 한 공급자에 대 한 설명서를 참조 하십시오.  
  
|속성|Description|  
|----------|-----------------|  
|CatalogName|이 큐브 속해 있는 카탈로그의 이름입니다.|  
|ChildrenCardinality|멤버의 자식 수입니다.|  
|CubeName|큐브의 이름입니다.|  
|Description|멤버의 의미 있는 설명입니다.|  
|DimensionUniqueName|모호 하지 않은 이름을 [차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)합니다.|  
|HierarchyUniqueName|계층의 명확한 이름입니다.|  
|LevelNumber|계층의 루트 수준 사이의 거리입니다.|  
|LevelUniqueName|수준의 모호 하지 않은 이름입니다.|  
|MemberCaption|멤버에 연결된 레이블 또는 캡션입니다.|  
|MemberGUID|멤버의 GUID입니다.|  
|MemberName|멤버의 이름입니다.|  
|MemberOrdinal|멤버의 서 수입니다.|  
|MemberType|멤버의 유형입니다.|  
|MemberUniqueName|모호 하지 않은 멤버의 이름입니다.|  
|ParentCount|이 멤버에 있는 부모 수의 수입니다.|  
|ParentLevel|멤버의 부모 수준 수입니다.|  
|ParentUniqueName|멤버의 부모의 모호 하지 않은 이름입니다.|  
|SchemaName|이 큐브 속해 있는 스키마의 이름입니다.|  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 예제 (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [(ADO MD) members 컬렉션](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
