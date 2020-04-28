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
ms.openlocfilehash: 35e02e4823d0a3abf245e1885b95176d6350d712
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949691"
---
# <a name="hierarchy-object-ado-md"></a>Hierarchy 개체(ADO MD)
[차원의](../../../ado/reference/ado-md-api/dimension-object-ado-md.md) 멤버를 집계 하거나 "롤업" 할 수 있는 한 가지 방법을 나타냅니다. 하나 이상의 계층 구조를 따라 차원을 집계할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 **Hierarchy** 개체의 컬렉션 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) 및 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) 속성을 사용 하 여 **계층 구조** 를 식별 합니다.  
  
-   [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성을 사용 하 여 **계층 구조** 를 설명 하는 의미 있는 문자열을 반환 합니다.  
  
-   [수준](../../../ado/reference/ado-md-api/levels-collection-ado-md.md) 컬렉션을 사용 하 여 **계층** 을 구성 하는 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 개체를 반환 합니다.  
  
-   표준 ADO [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 **계층** 개체에 대 한 추가 정보를 가져올 수 있습니다.  
  
 **속성** 컬렉션에는 공급자가 제공한 속성이 포함 되어 있습니다. 다음 표에서는 사용할 수 있는 속성을 보여 줍니다. 실제 속성 목록은 공급자의 구현에 따라 다를 수 있습니다. 사용 가능한 속성의 전체 목록은 공급자 설명서를 참조 하세요.  
  
|속성|Description|  
|----------|-----------------|  
|AllMember|계층에서 가장 높은 수준의 롤업 멤버입니다.|  
|CatalogName|이 큐브가 속한 카탈로그의 이름입니다.|  
|CubeName|큐브 이름입니다.|  
|DefaultMember|이 계층에 대 한 기본 멤버의 고유한 이름입니다.|  
|Description|계층 구조에 대 한 의미 있는 설명입니다.|  
|DimensionType|이 계층이 속한 차원의 유형입니다.|  
|DimensionUniqueName|차원의 명확 하지 않은 이름입니다.|  
|HierarchyCaption|계층과 연결된 레이블 또는 캡션입니다.|  
|HierarchyCardinality|계층의 멤버 수입니다.|  
|계층 Guid|계층의 GUID입니다.|  
|HierarchyName|계층 이름입니다.|  
|HierarchyUniqueName|계층의 모호 하지 않은 이름입니다.|  
|SchemaName|이 큐브가 속한 스키마의 이름입니다.|  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [CubeDef 예제 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Dimension 개체 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [계층 구조 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [수준 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
