---
title: CubeDef 개체 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CubeDef
helpviewer_keywords:
- CubeDef object [ADO MD]
ms.assetid: feb2581c-fc41-471c-bb69-29f8a55fda70
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31e2bf587c19ab8088b0ab702be60fde54247aec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="cubedef-object-ado-md"></a>ADO MD CubeDef 개체
관련된 차원 집합이 포함 된 다차원 스키마에서 큐브를 나타냅니다.  
  
## <a name="remarks"></a>주의  
 컬렉션과의 속성을 사용 하 여 한 **CubeDef** 개체를 다음을 수행할 수 있습니다.  
  
-   식별 된 **CubeDef** 와 [이름](../../../ado/reference/ado-md-api/name-property-ado-md.md) 속성입니다.  
  
-   사용 하 여 큐브를 설명 하는 문자열을 반환 합니다.는 [설명](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성입니다.  
  
-   사용 하 여 큐브를 구성 하는 차원을 반환는 [차원](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md) 컬렉션입니다.  
  
-   에 대 한 추가 정보를 가져올는 **CubeDef** 표준 ADO와 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
 **속성** 컬렉션 공급자를 제공 하는 속성을 포함 합니다. 다음 표에서 사용할 수 있는 속성을 나열 합니다. 실제 속성 목록은 공급자의 구현에 따라 달라질 수 있습니다. 사용 가능한 속성의 전체 목록은 대 한 공급자에 대 한 설명서를 참조 하십시오.  
  
|이름|Description|  
|----------|-----------------|  
|CatalogName|이 큐브 속해 있는 카탈로그의 이름입니다.|  
|CreatedOn|날짜 및 큐브를 만든 시간입니다.|  
|CubeGUID|큐브 GUID입니다.|  
|CubeName|큐브의 이름입니다.|  
|CubeType|큐브의 유형입니다.|  
|DataUpdatedBy|데이터를 마지막으로 업데이트 하는 사람의 사용자 ID입니다.|  
|Description|큐브의 의미 있는 설명입니다.|  
|LastSchemaUpdate|날짜 및 스키마의 마지막 업데이트 시간입니다.|  
|SchemaName|이 큐브 속해 있는 스키마의 이름입니다.|  
|SchemaUpdatedBy|최종 스키마 업데이트를 수행 하는 사용자의 사용자 ID입니다.|  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [CubeDef 예 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [카탈로그 개체 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)   
 [ADO MD CubeDefs 컬렉션](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)   
 [ADO MD 차원 컬렉션](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
