---
title: 멤버 개체 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member
helpviewer_keywords:
- Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f8d11e97fd31745752449c5649e1096d0bb667a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66709022"
---
# <a name="member-object-ado-md"></a>Member 개체(ADO MD)
셀 집합의 축 따라 위치 멤버나 수준의 멤버의 자식을 큐브의 수준의 멤버를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 속성을 **멤버** 사용 되는 컨텍스트에 따라 달라 집니다. **멤버** 의 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 에서 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) 에 [자식](../../../ado/reference/ado-md-api/children-property-ado-md.md) 반환 하는 속성을 **멤버** 에서 현재에서 계층 구조에서 다음 하위 수준의 **멤버**합니다. 에 대 한는 **멤버** 의 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md)의 **자식** 컬렉션은 항상 비어 있습니다. 또한 합니다 [형식](../../../ado/reference/ado-md-api/type-property-ado-md.md) 속성에만 적용 됩니다 **멤버** 의 **수준**합니다.  
  
 A **멤버** 의 **위치** 에 두 속성을 표시 하는 경우에 유용 합니다 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md): [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) 하 고 [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)합니다. 이러한 속성에 액세스 하는 경우 오류가 발생 한 **멤버** 의 **수준**합니다.  
  
 컬렉션 및 속성을 사용 하 여는 **멤버** 의 개체를 **수준**, 다음을 수행할 수 있습니다:  
  
-   식별 된 **멤버** 사용 하 여 합니다 [이름](../../../ado/reference/ado-md-api/name-property-ado-md.md) 및 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) 속성.  
  
-   표시할 때 사용할 문자열을 반환 합니다 **멤버** 사용 하 여 합니다 [캡션](../../../ado/reference/ado-md-api/caption-property-ado-md.md) 속성입니다.  
  
-   측정값 또는 수식을 설명 하는 의미 있는 문자열을 반환 **멤버** 사용 하 여 합니다 [설명](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성입니다.  
  
-   특성을 확인 합니다 **멤버** 사용 하 여 합니다 [형식](../../../ado/reference/ado-md-api/type-property-ado-md.md) 속성입니다.  
  
-   에 대 한 정보를 가져올는 **수준** 의 합니다 **멤버** 사용 하 여는 [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) 및 [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) 속성입니다.  
  
-   가져올 관련 **멤버** 에 [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) 사용 하 여는 [부모](../../../ado/reference/ado-md-api/parent-property-ado-md.md) 및 [자식](../../../ado/reference/ado-md-api/children-property-ado-md.md) 속성입니다.  
  
-   자식의 수를 **멤버** 사용 하 여 합니다 [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) 속성입니다.  
  
-   표준 ADO를 사용 하 여 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 대 한 추가 정보를 가져오려고 합니다 **수준** 개체입니다.  
  
 컬렉션 및 속성을 사용 하 여는 **멤버** 의 **위치** 따라는 [축](../../../ado/reference/ado-md-api/axis-object-ado-md.md), 다음을 수행할 수 있습니다:  
  
-   식별 된 **멤버** 사용 하 여 합니다 [이름](../../../ado/reference/ado-md-api/name-property-ado-md.md) 및 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) 속성.  
  
-   표시할 때 사용할 문자열을 반환 합니다 **멤버** 사용 하 여 합니다 [캡션](../../../ado/reference/ado-md-api/caption-property-ado-md.md) 속성입니다.  
  
-   측정값 또는 수식을 설명 하는 의미 있는 문자열을 반환 **멤버** 사용 하 여 합니다 [설명](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성입니다.  
  
-   에 대 한 정보를 가져올는 **수준** 의 합니다 **멤버** 사용 하 여는 [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) 및 [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) 속성입니다.  
  
-   자식의 수를 **멤버** 사용 하 여 합니다 [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) 속성입니다.  
  
-   사용 하 여 합니다 [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) 속성에 자식이 하나 이상 있는지 여부를 확인 하는 **축** 직후이 **멤버**합니다.  
  
-   사용 하 여는 [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md) 속성을 확인 하는지 여부를이 부모 **멤버** 바로 앞의 부모와 같습니다 **멤버**합니다.  
  
-   표준 ADO를 사용 하 여 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 대 한 추가 정보를 가져오려고 합니다 **수준** 개체입니다.  
  
 합니다 **속성** 공급자가 제공한 속성을 포함 하는 컬렉션입니다. 다음 표에서 사용할 수 있는 속성을 보여 줍니다. 실제 속성은 공급자의 구현에 따라 달라질 수 있습니다. 사용 가능한 속성의 전체 목록에 대 한 공급자에 대 한 설명서를 참조 하세요.  
  
|이름|Description|  
|----------|-----------------|  
|CatalogName|이 큐브가 속한 카탈로그의 이름입니다.|  
|ChildrenCardinality|멤버의 자식 수입니다.|  
|CubeName|큐브 이름입니다.|  
|Description|멤버의 의미 있는 설명입니다.|  
|DimensionUniqueName|모호 하지 않은 이름의 합니다 [차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)합니다.|  
|HierarchyUniqueName|계층의 명확한 이름입니다.|  
|LevelNumber|계층의 루트 수준 사이의 거리입니다.|  
|LevelUniqueName|수준의 모호 하지 않은 이름입니다.|  
|MemberCaption|멤버에 연결된 레이블 또는 캡션입니다.|  
|MemberGUID|멤버의 GUID입니다.|  
|MemberName|멤버의 이름입니다.|  
|MemberOrdinal|멤버의 서 수입니다.|  
|MemberType|멤버의 유형입니다.|  
|MemberUniqueName|모호 하지 않은 멤버의 이름입니다.|  
|ParentCount|이 멤버에 있는 부모의 개수 횟수입니다.|  
|ParentLevel|멤버의 부모 수준 수입니다.|  
|ParentUniqueName|멤버의 부모의 모호 하지 않은 이름입니다.|  
|SchemaName|이 큐브가 속한 스키마의 이름입니다.|  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Catalog 예제 (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Members 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
