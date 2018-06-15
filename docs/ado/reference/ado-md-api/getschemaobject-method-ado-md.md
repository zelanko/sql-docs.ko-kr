---
title: ADO MD GetSchemaObject 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3068635d252b4c79f08bc88102796f0fc85a1315
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35283872"
---
# <a name="getschemaobject-method-ado-md"></a>ADO MD GetSchemaObject 메서드
ADO MD 스키마 개체를 검색 ([차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md), 또는 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md)) 하 여 해당 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>구문  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ObjType*  
 A [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md) 스키마 개체 (차원, 계층, 수준 또는 멤버)를 검색의 유형을 지정 하는 값입니다.  
  
 *UniqueName*  
 A **문자열** 지정 하는 **UniqueName** 검색할 개체의 속성 값입니다.  
  
## <a name="remarks"></a>Remarks  
 **GetSchemaObject** 에 지정 된 대로, 고유한 이름을 사용 하는 개체 검색은 **UniqueName** 속성입니다. 부모 개체의 이름을 알면 됩니다 필요 없고 부모 컬렉션 스키마 개체를 가져와 채울 필요는 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [CubeDef 개체(ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목  
 [CubeDef 개체(ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
