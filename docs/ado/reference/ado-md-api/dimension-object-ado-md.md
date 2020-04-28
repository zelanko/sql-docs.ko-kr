---
title: Dimension 개체 (ADO MD) | Microsoft Docs
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
ms.openlocfilehash: f7a13ad87d56f5e7855070d8fe577bb408d6ce9e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938535"
---
# <a name="dimension-object-ado-md"></a>Dimension 개체(ADO MD)
하나 이상의 멤버 계층을 포함 하는 다차원 큐브의 차원 중 하나를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 **Dimension** 개체의 컬렉션 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) 및 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) 속성을 사용 하 여 **차원을** 식별 합니다.  
  
-   [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성을 사용 하 여 **차원을** 설명 하는 의미 있는 문자열을 반환 합니다.  
  
-   [계층](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) 컬렉션을 사용 하 여 **차원을** 구성 하는 [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) 개체를 반환 합니다.  
  
-   표준 ADO [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 **차원** 개체에 대 한 추가 정보를 가져올 수 있습니다.  
  
 **속성** 컬렉션에는 공급자가 제공한 속성이 포함 되어 있습니다. 다음 표에서는 사용할 수 있는 속성을 보여 줍니다. 실제 속성 목록은 공급자의 구현에 따라 다를 수 있습니다. 사용 가능한 속성의 전체 목록은 공급자 설명서를 참조 하세요.  
  
|속성|Description|  
|----------|-----------------|  
|CatalogName|이 큐브가 속한 카탈로그의 이름입니다.|  
|CubeName|큐브 이름입니다.|  
|DefaultHierarchy|기본 계층의 고유한 이름입니다.|  
|Description|큐브에 대 한 의미 있는 설명입니다.|  
|DimensionCaption|차원과 연결 된 레이블 또는 캡션입니다.|  
|DimensionCardinality|차원의 멤버 수입니다.|  
|DimensionGUID|차원의 GUID입니다.|  
|DimensionName|차원의 이름입니다.|  
|DimensionOrdinal|큐브를 구성 하는 차원 그룹 간의 차원 서 수입니다.|  
|DimensionType|차원 유형입니다.|  
|DimensionUniqueName|차원의 명확 하지 않은 이름입니다.|  
|SchemaName|이 큐브가 속한 스키마의 이름입니다.|  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [CubeDef 예제 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [CubeDef 개체 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [차원 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [계층 구조 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
