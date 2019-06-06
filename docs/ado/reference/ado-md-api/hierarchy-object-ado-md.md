---
title: Hierarchy 개체 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Hierarchy
helpviewer_keywords:
- Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5915102164afccd8e2055e14d0ef9d63b2cf5937
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709148"
---
# <a name="hierarchy-object-ado-md"></a>Hierarchy 개체(ADO MD)
한 가지 방식을의 멤버는 [차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md) 집계 되거나 "롤업 합니다." 차원 하나 이상의 계층 구조에 따라 집계할 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 컬렉션 및 속성을 사용 하 여는 **계층** 개체를 다음을 수행할 수 있습니다.  
  
-   식별 된 **계층** 사용 하 여는 [이름](../../../ado/reference/ado-md-api/name-property-ado-md.md) 및 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) 속성입니다.  
  
-   설명 하는 의미 있는 문자열을 반환 합니다 **계층 구조** 사용 하 여 합니다 [설명](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성.  
  
-   반환 합니다 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 구성 하는 개체를 **계층** 사용 하 여는 [수준](../../../ado/reference/ado-md-api/levels-collection-ado-md.md) 컬렉션입니다.  
  
-   표준 ADO를 사용 하 여 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 대 한 추가 정보를 가져오려고 합니다 **계층** 개체입니다.  
  
 합니다 **속성** 공급자가 제공한 속성을 포함 하는 컬렉션입니다. 다음 표에서 사용할 수 있는 속성을 보여 줍니다. 실제 속성은 공급자의 구현에 따라 달라질 수 있습니다. 사용 가능한 속성의 전체 목록에 대 한 공급자에 대 한 설명서를 참조 하세요.  
  
|이름|Description|  
|----------|-----------------|  
|AllMember|계층 구조에서 롤업의 가장 높은 수준에서 멤버입니다.|  
|CatalogName|이 큐브가 속한 카탈로그의 이름입니다.|  
|CubeName|큐브 이름입니다.|  
|DefaultMember|이 계층에 대 한 기본 멤버의 고유 이름입니다.|  
|Description|계층의 의미 있는 설명입니다.|  
|DimensionType|이 계층이 속한 차원의 형식입니다.|  
|DimensionUniqueName|차원의 모호 하지 않은 이름입니다.|  
|HierarchyCaption|계층과 연결된 레이블 또는 캡션입니다.|  
|HierarchyCardinality|계층의 멤버 수입니다.|  
|HierarchyGUID|계층의 GUID입니다.|  
|HierarchyName|계층의 이름입니다.|  
|HierarchyUniqueName|계층의 명확한 이름입니다.|  
|SchemaName|이 큐브가 속한 스키마의 이름입니다.|  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [CubeDef 예제 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Dimension 개체 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Hierarchies 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Levels 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
