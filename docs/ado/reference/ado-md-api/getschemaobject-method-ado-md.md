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
ms.openlocfilehash: 690c81a46c62c8844780e82b5c82a0ff7301105d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949763"
---
# <a name="getschemaobject-method-ado-md"></a>GetSchemaObject 메서드(ADO MD)
[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)에 의해 ADO MD 스키마 개체 ([차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md)또는 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md))를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ObjType*  
 검색할 스키마 개체 (차원, 계층, 수준 또는 멤버)의 유형을 지정 하는 [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md) 값입니다.  
  
 *UniqueName*  
 검색할 개체의 **UniqueName** 속성 값을 지정 하는 **문자열** 입니다.  
  
## <a name="remarks"></a>설명  
 **Getschemaobject** 는 **UniqueName** 속성에 지정 된 고유 이름을 사용 하 여 개체를 검색 합니다. 부모 개체의 이름을 알 필요는 없으며 스키마 개체를 검색 하기 위해 부모 컬렉션을 채울 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [CubeDef 개체(ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>참고 항목  
 [CubeDef 개체(ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
