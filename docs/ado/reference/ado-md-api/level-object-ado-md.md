---
title: 수준 개체 (ADO MD) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 27e789c4eb34ed275d6f18f62325287febb73422
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740193"
---
# <a name="level-object-ado-md"></a>Level 개체(ADO MD)
계층에서 순위가 동일한 멤버 집합이 포함 되어 있습니다.  
  
## <a name="remarks"></a>Remarks  
 컬렉션 및 속성을 사용 하 여는 **수준** 개체를 다음을 수행할 수 있습니다.  
  
-   식별 된 **수준** 사용 하 여는 [이름](../../../ado/reference/ado-md-api/name-property-ado-md.md) 및 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) 속성입니다.  
  
-   표시할 때 사용할 문자열을 반환 합니다 **수준** 사용 하 여 합니다 [캡션](../../../ado/reference/ado-md-api/caption-property-ado-md.md) 속성입니다.  
  
-   설명 하는 의미 있는 문자열을 반환 합니다 **수준** 사용 하 여 합니다 [설명](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성입니다.  
  
-   반환 된 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 구성 하는 개체를 **수준** 사용 하 여를 [멤버](../../../ado/reference/ado-md-api/members-collection-ado-md.md) 컬렉션.  
  
-   루트에서 수준 수를 반환 합니다 **수준** 사용 하 여 합니다 [깊이](../../../ado/reference/ado-md-api/depth-property-ado-md.md) 속성입니다.  
  
-   표준 ADO를 사용 하 여 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 대 한 추가 정보를 가져오려고 합니다 **수준** 개체입니다.  
  
 합니다 **속성** 공급자가 제공한 속성을 포함 하는 컬렉션입니다. 다음 표에서 사용할 수 있는 속성을 보여 줍니다. 실제 속성은 공급자의 구현에 따라 달라질 수 있습니다. 사용 가능한 속성의 전체 목록에 대 한 공급자에 대 한 설명서를 참조 하세요.  
  
|이름|Description|  
|----------|-----------------|  
|CatalogName|이 큐브가 속한 카탈로그의 이름입니다.|  
|CubeName|큐브 이름입니다.|  
|Description|수준의 의미 있는 설명입니다.|  
|DimensionUniqueName|모호 하지 않은 이름의 합니다 [차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)합니다.|  
|HierarchyUniqueName|계층의 명확한 이름입니다.|  
|LevelCaption|레이블 또는 캡션입니다 수준과 사용 하 여 연결 합니다.|  
|LevelCardinality|수준의 멤버 수입니다.|  
|LevelGUID|GUID는 수준입니다.|  
|LevelName|수준의 이름입니다.|  
|LevelNumber|계층의 루트 수준 사이의 거리입니다.|  
|LevelType|유형 수준입니다.|  
|LevelUniqueName|수준의 모호 하지 않은 이름입니다.|  
|SchemaName|이 큐브가 속한 스키마의 이름입니다.|  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [CubeDef 예제 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Hierarchy 개체 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [Levels 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Members 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
