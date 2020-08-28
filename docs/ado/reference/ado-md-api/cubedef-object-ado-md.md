---
description: CubeDef 개체(ADO MD)
title: CubeDef 개체 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: de22ce013d94b1830ba220c318c06bbe716423bd
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987024"
---
# <a name="cubedef-object-ado-md"></a>CubeDef 개체(ADO MD)
관련 차원 집합을 포함 하는 다차원 스키마의 큐브를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 **CubeDef** 개체의 컬렉션 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name](./name-property-ado-md.md) 속성을 사용 하 여 **CubeDef** 를 식별 합니다.  
  
-   [Description](./description-property-ado-md.md) 속성을 사용 하 여 큐브를 설명 하는 문자열을 반환 합니다.  
  
-   [차원](./dimensions-collection-ado-md.md) 컬렉션을 사용 하 여 큐브를 구성 하는 차원을 반환 합니다.  
  
-   표준 ADO [속성](../ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 **CubeDef** 에 대 한 추가 정보를 얻습니다.  
  
 **속성** 컬렉션에는 공급자가 제공한 속성이 포함 되어 있습니다. 다음 표에서는 사용할 수 있는 속성을 보여 줍니다. 실제 속성 목록은 공급자의 구현에 따라 다를 수 있습니다. 사용 가능한 속성의 전체 목록은 공급자 설명서를 참조 하세요.  
  
|Name|설명|  
|----------|-----------------|  
|CatalogName|이 큐브가 속한 카탈로그의 이름입니다.|  
|Adventureworks.createdon|큐브를 만든 날짜와 시간입니다.|  
|CubeGUID|큐브 GUID입니다.|  
|CubeName|큐브 이름입니다.|  
|자세한 유형|큐브의 유형입니다.|  
|DataUpdatedBy|마지막 데이터 업데이트를 수행 하는 사용자의 사용자 ID입니다.|  
|설명|큐브에 대 한 의미 있는 설명입니다.|  
|LastSchemaUpdate|스키마가 마지막으로 업데이트 된 날짜 및 시간입니다.|  
|SchemaName|이 큐브가 속한 스키마의 이름입니다.|  
|SchemaUpdatedBy|마지막 스키마 업데이트를 수행 하는 사용자의 사용자 ID입니다.|  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](./cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [CubeDef 예제 (VBScript)](./cubedef-example-vbscript.md)   
 [Catalog 개체 (ADO MD)](./catalog-object-ado-md.md)   
 [CubeDefs Collection (ADO MD)](./cubedefs-collection-ado-md.md)   
 [차원 컬렉션 (ADO MD)](./dimensions-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../ado-api/properties-collection-ado.md)