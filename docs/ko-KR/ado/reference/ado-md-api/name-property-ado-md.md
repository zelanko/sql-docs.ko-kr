---
title: Name 속성 (ADO MD) | Microsoft Docs
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
- Level::Name
- CubeDef::Name
- Member::Name
- Catalog::Name
- Dimension::Name
- Name
- Axis::Name
- Hierarchy::Name
helpviewer_keywords:
- Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb1b8cd01d08341f8ff97952284d47c575522ae2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="name-property-ado-md"></a>Name 속성 (ADO MD)
개체의 이름을 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **문자열** 읽기 전용입니다.  
  
## <a name="remarks"></a>주의  
 검색할 수 있습니다는 **이름** 을 참조할 수 있습니다를 개체 이름으로 직접 서 수 참조를 사용 하 여 개체의 속성입니다. 예를 들어 경우 `cdf.CubeDefs(0).Name` "Bobs 비디오 Store"를 생성 합니다.이를 참조할 수 있습니다 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) 으로 `cdf.CubeDefs("Bobs Video Store")`합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[Axis 개체(ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|[Catalog 개체(ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[CubeDef 개체(ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|  
|[Dimension 개체(ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Hierarchy 개체(ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|[Level 개체(ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|  
|[Member 개체(ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)|||  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 예제 (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [ADO MD caption 속성](../../../ado/reference/ado-md-api/caption-property-ado-md.md)   
 [Description 속성 (ADO MD)](../../../ado/reference/ado-md-api/description-property-ado-md.md)   
 [UniqueName 속성(ADO MD)](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)
