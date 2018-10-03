---
title: GetSchemaObject 메서드 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe681a0f93dd88ad7f4752daf213817c21b054ad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798281"
---
# <a name="getschemaobject-method-ado-md"></a>GetSchemaObject 메서드(ADO MD)
ADO MD 스키마 개체를 검색 ([차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)를 [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)합니다 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md), 또는 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md)) 하 여 해당 [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>구문  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ObjType*  
 A [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md) 스키마 개체 (차원, 계층, 수준 또는 멤버)를 검색 하 형식을 지정 하는 값입니다.  
  
 *UniqueName*  
 A **문자열** 지정 하는 **UniqueName** 검색할 개체의 속성 값입니다.  
  
## <a name="remarks"></a>Remarks  
 **GetSchemaObject** 에 지정 된 대로, 고유한 이름을 사용 하는 개체를 검색 합니다 **UniqueName** 속성입니다. 부모 개체의 이름을 알 수 하지 않아도 및 부모 컬렉션 스키마 개체를 검색 하려면 채울 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [CubeDef 개체(ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목  
 [CubeDef 개체(ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
