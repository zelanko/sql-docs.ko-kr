---
title: Hierarchy 개체 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Hierarchy
helpviewer_keywords:
- Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b920f2235a0e259194165692278ed55cac304b3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="hierarchy-object-ado-md"></a>Hierarchy 개체 (ADO MD)
한 가지 방식을 보여의 멤버는 [차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md) 집계 되거나 "롤업 합니다." 차원은 하나 이상의 계층 구조에 따라 집계 될 수 있습니다.  
  
## <a name="remarks"></a>주의  
 컬렉션과의 속성을 사용 하 여 한 **계층** 개체를 다음을 수행할 수 있습니다.  
  
-   식별 된 **계층** 와 [이름](../../../ado/reference/ado-md-api/name-property-ado-md.md) 및 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) 속성.  
  
-   설명 하는 의미 있는 문자열을 반환 된 **계층** 와 [설명](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성입니다.  
  
-   반환 된 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 구성 하는 개체는 **계층** 와 [수준](../../../ado/reference/ado-md-api/levels-collection-ado-md.md) 컬렉션입니다.  
  
-   표준 ADO를 사용 하 여 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 대 한 추가 정보를 가져올 수는 **계층** 개체입니다.  
  
 **속성** 컬렉션 공급자를 제공 하는 속성을 포함 합니다. 다음 표에서 사용할 수 있는 속성을 나열 합니다. 실제 속성 목록은 공급자의 구현에 따라 달라질 수 있습니다. 사용 가능한 속성의 전체 목록은 대 한 공급자에 대 한 설명서를 참조 하십시오.  
  
|이름|Description|  
|----------|-----------------|  
|AllMember|계층에서 rollup의 최상위 수준의 멤버입니다.|  
|CatalogName|이 큐브 속해 있는 카탈로그의 이름입니다.|  
|CubeName|큐브의 이름입니다.|  
|DefaultMember|이 계층에 대 한 기본 멤버의 고유 이름입니다.|  
|Description|계층의 의미 있는 설명입니다.|  
|DimensionType|이 계층이 속한 차원의 형식입니다.|  
|DimensionUniqueName|차원의 모호 하지 않은 이름입니다.|  
|HierarchyCaption|계층과 연결된 레이블 또는 캡션입니다.|  
|HierarchyCardinality|계층의 멤버 수입니다.|  
|HierarchyGUID|계층의 GUID입니다.|  
|HierarchyName|계층 이름입니다.|  
|HierarchyUniqueName|계층의 명확한 이름입니다.|  
|SchemaName|이 큐브 속해 있는 스키마의 이름입니다.|  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [CubeDef 예 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [차원 개체 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Hierarchies 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [ADO MD 수준 컬렉션](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
