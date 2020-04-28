---
title: Level 개체 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level
helpviewer_keywords:
- Level object [ADO MD]
ms.assetid: 37815869-ed30-45fd-9aea-0a986c1b305c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a44060ae4ffd9399c34d4cd8133f5ad7404ed5a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949607"
---
# <a name="level-object-ado-md"></a>Level 개체(ADO MD)
에는 계층 구조 내에서 순위가 동일한 멤버 집합이 포함 되어 있습니다.  
  
## <a name="remarks"></a>설명  
 **수준** 개체의 컬렉션 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) 및 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) 속성을 사용 하 여 **수준을** 식별 합니다.  
  
-   [Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md) 속성을 사용 하 여 **수준을** 표시할 때 사용할 문자열을 반환 합니다.  
  
-   [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성을 사용 하 여 **수준을** 설명 하는 의미 있는 문자열을 반환 합니다.  
  
-   [Members](../../../ado/reference/ado-md-api/members-collection-ado-md.md) 컬렉션을 사용 하 여 **수준을** 구성 하는 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 개체를 반환 합니다.  
  
-   **수준** 의 루트에서 수준 수 만큼 [깊이](../../../ado/reference/ado-md-api/depth-property-ado-md.md) 속성을 반환 합니다.  
  
-   표준 ADO [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 **수준** 개체에 대 한 추가 정보를 가져올 수 있습니다.  
  
 **속성** 컬렉션에는 공급자가 제공한 속성이 포함 되어 있습니다. 다음 표에서는 사용할 수 있는 속성을 보여 줍니다. 실제 속성 목록은 공급자의 구현에 따라 다를 수 있습니다. 사용 가능한 속성의 전체 목록은 공급자 설명서를 참조 하세요.  
  
|속성|Description|  
|----------|-----------------|  
|CatalogName|이 큐브가 속한 카탈로그의 이름입니다.|  
|CubeName|큐브 이름입니다.|  
|Description|수준에 대 한 의미 있는 설명입니다.|  
|DimensionUniqueName|[차원의](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)명확 하지 않은 이름입니다.|  
|HierarchyUniqueName|계층의 모호 하지 않은 이름입니다.|  
|LevelCaption|수준과 연결 된 레이블 또는 캡션입니다.|  
|LevelCardinality|수준의 멤버 수입니다.|  
|LevelGUID|수준의 GUID입니다.|  
|LevelName|수준의 이름입니다.|  
|LevelNumber|계층의 수준과 루트 사이의 거리입니다.|  
|LevelType|수준의 유형입니다.|  
|LevelUniqueName|수준의 명확 하지 않은 이름입니다.|  
|SchemaName|이 큐브가 속한 스키마의 이름입니다.|  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [CubeDef 예제 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Hierarchy 개체 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [수준 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Members 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
