---
title: CubeDef 개체 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CubeDef
helpviewer_keywords:
- CubeDef object [ADO MD]
ms.assetid: feb2581c-fc41-471c-bb69-29f8a55fda70
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1027fc76cb09f7b846e1b8edad52a3cb5dbf2bc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694067"
---
# <a name="cubedef-object-ado-md"></a>CubeDef 개체(ADO MD)
관련된 차원 집합이 포함 된 다차원 스키마에서 큐브를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 컬렉션 및 속성을 사용 하 여는 **CubeDef** 개체를 다음을 수행할 수 있습니다.  
  
-   식별을 **CubeDef** 사용 하 여 합니다 [이름](../../../ado/reference/ado-md-api/name-property-ado-md.md) 속성입니다.  
  
-   사용 하 여 큐브를 설명 하는 문자열을 반환 합니다 [설명을](../../../ado/reference/ado-md-api/description-property-ado-md.md) 속성입니다.  
  
-   사용 하 여 큐브를 구성 하는 차원을 반환 합니다 [차원](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md) 컬렉션입니다.  
  
-   에 대 한 추가 정보를 얻으려면 합니다 **CubeDef** 표준 ADO를 사용 하 여 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
 합니다 **속성** 공급자가 제공한 속성을 포함 하는 컬렉션입니다. 다음 표에서 사용할 수 있는 속성을 보여 줍니다. 실제 속성은 공급자의 구현에 따라 달라질 수 있습니다. 사용 가능한 속성의 전체 목록에 대 한 공급자에 대 한 설명서를 참조 하세요.  
  
|이름|Description|  
|----------|-----------------|  
|CatalogName|이 큐브가 속한 카탈로그의 이름입니다.|  
|CreatedOn|날짜 및 큐브를 만든 시간입니다.|  
|CubeGUID|GUID 큐브입니다.|  
|CubeName|큐브의 이름입니다.|  
|CubeType|큐브의 유형입니다.|  
|DataUpdatedBy|마지막 데이터 업데이트를 수행 하는 사용자의 사용자 ID입니다.|  
|Description|큐브의 의미 있는 설명입니다.|  
|LastSchemaUpdate|날짜 및 시간 최종 스키마 업데이트입니다.|  
|SchemaName|이 큐브가 속한 스키마의 이름입니다.|  
|SchemaUpdatedBy|최종 스키마 업데이트를 수행 하는 사용자의 사용자 ID입니다.|  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [CubeDef 예제 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Catalog 개체 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)   
 [CubeDefs 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)   
 [Dimensions 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
