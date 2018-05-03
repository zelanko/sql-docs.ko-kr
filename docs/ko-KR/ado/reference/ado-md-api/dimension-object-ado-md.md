---
title: ADO MD 개체 차원 | Microsoft Docs
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
- Dimension
helpviewer_keywords:
- Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8019ecec9222e1e6bb67633d225e3859734dcb7b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dimension-object-ado-md"></a>차원 개체 (ADO MD)
하나 이상의 멤버 계층 구조를 포함 하는 다차원 큐브의 차원 중 하나를 나타냅니다.  
  
## <a name="remarks"></a>주의  
 컬렉션과의 속성을 사용 하 여 한 **차원** 개체를 다음을 수행할 수 있습니다.  
  
-   식별 된 **차원** 와 [이름](../../../ado/reference/ado-md-api/name-property-ado-md.md) 및 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) 속성입니다.  
  
-   설명 하는 의미 있는 문자열을 반환 된 **차원** 와 [설명](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성입니다.  
  
-   반환 된 [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) 구성 하는 개체는 **차원** 와 [계층](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) 컬렉션입니다.  
  
-   표준 ADO를 사용 하 여 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 대 한 추가 정보를 가져올 수는 **차원** 개체입니다.  
  
 **속성** 컬렉션 공급자를 제공 하는 속성을 포함 합니다. 다음 표에서 사용할 수 있는 속성을 나열 합니다. 실제 속성 목록은 공급자의 구현에 따라 달라질 수 있습니다. 사용 가능한 속성의 전체 목록은 대 한 공급자에 대 한 설명서를 참조 하십시오.  
  
|이름|Description|  
|----------|-----------------|  
|CatalogName|이 큐브 속해 있는 카탈로그의 이름입니다.|  
|CubeName|큐브의 이름입니다.|  
|DefaultHierarchy|기본 계층의 고유한 이름입니다.|  
|Description|큐브의 의미 있는 설명입니다.|  
|DimensionCaption|레이블 또는 해당 차원과 연결 된 캡션입니다.|  
|DimensionCardinality|차원의 멤버 수입니다.|  
|DimensionGUID|차원의의 GUID입니다.|  
|DimensionName|차원의 이름입니다.|  
|DimensionOrdinal|차원 큐브를 구성 하는 그룹 간의 차원의 서 수입니다.|  
|DimensionType|차원 유형입니다.|  
|DimensionUniqueName|차원의 모호 하지 않은 이름입니다.|  
|SchemaName|이 큐브 속해 있는 스키마의 이름입니다.|  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [CubeDef 예 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [ADO MD CubeDef 개체](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [ADO MD 차원 컬렉션](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Hierarchies 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
