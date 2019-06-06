---
title: 차원 개체 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Dimension
helpviewer_keywords:
- Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f69acfa84272e73bcafb370eb85c6a14614a367c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709440"
---
# <a name="dimension-object-ado-md"></a>Dimension 개체(ADO MD)
멤버 하나 이상의 계층 구조를 포함 하는 다차원 큐브의 차원 중 하나를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 컬렉션 및 속성을 사용 하 여는 **차원** 개체를 다음을 수행할 수 있습니다.  
  
-   식별 된 **차원** 사용 하 여 합니다 [이름](../../../ado/reference/ado-md-api/name-property-ado-md.md) 및 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) 속성.  
  
-   설명 하는 의미 있는 문자열을 반환 합니다 **차원** 사용 하 여 합니다 [설명](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성입니다.  
  
-   반환 된 [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) 구성 하는 개체를 **차원** 사용 하 여를 [계층](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) 컬렉션.  
  
-   표준 ADO를 사용 하 여 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 대 한 추가 정보를 가져오려고 합니다 **차원** 개체입니다.  
  
 합니다 **속성** 공급자가 제공한 속성을 포함 하는 컬렉션입니다. 다음 표에서 사용할 수 있는 속성을 보여 줍니다. 실제 속성은 공급자의 구현에 따라 달라질 수 있습니다. 사용 가능한 속성의 전체 목록에 대 한 공급자에 대 한 설명서를 참조 하세요.  
  
|이름|Description|  
|----------|-----------------|  
|CatalogName|이 큐브가 속한 카탈로그의 이름입니다.|  
|CubeName|큐브 이름입니다.|  
|DefaultHierarchy|기본 계층의 고유한 이름입니다.|  
|Description|큐브의 의미 있는 설명입니다.|  
|DimensionCaption|레이블 또는 차원과 연결 된 캡션입니다.|  
|DimensionCardinality|차원의 멤버 수입니다.|  
|DimensionGUID|GUID는 차원입니다.|  
|DimensionName|차원의 이름입니다.|  
|DimensionOrdinal|차원 큐브를 형성 하는 그룹 간의 차원의 서 수입니다.|  
|DimensionType|차원 유형입니다.|  
|DimensionUniqueName|차원의 모호 하지 않은 이름입니다.|  
|SchemaName|이 큐브가 속한 스키마의 이름입니다.|  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [CubeDef 예제 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [CubeDef 개체 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [Dimensions 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Hierarchies 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
