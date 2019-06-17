---
title: GetPermissions 메서드 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::GetPermissions
- _Group25::raw_GetPermissions
- _Group25::GetPermissions
- _User25::raw_GetPermissions
helpviewer_keywords:
- GetPermissions method [ADOX]
ms.assetid: df201c1f-c76a-465d-98f0-83b7fc36e6e3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8bff406485266af99a1c2538a4df237fd5bf43bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712085"
---
# <a name="getpermissions-method-adox"></a>GetPermissions 메서드(ADOX)
에 대 한 사용 권한을 반환 하는 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 또는 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 개체 또는 개체 컨테이너에 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 **긴** 그룹 또는 사용자 개체에는 권한을 포함 하는 비트 마스크를 지정 하는 값입니다. 이 값 중 하나 이상을 수는 [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) 상수입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 A **Variant** 사용 권한을 설정할 개체의 이름을 지정 하는 값입니다. 설정할 *이름을* 개체 컨테이너에 대 한 사용 권한을 확보 하려는 경우 null 값입니다.  
  
 *ObjectType*  
 A **긴** 하나일 수 있는 값의는 [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) 권한을 가져올 개체의 형식을 지정 하는 상수입니다.  
  
 *ObjectTypeId*  
 (선택 사항) A **Variant** OLE DB 사양에 정의 되지 공급자 개체 형식의 GUID를 지정 하는 값입니다. 이 매개 변수는 필요한 경우 *ObjectType* 로 설정 된 **adPermObjProviderSpecific**고, 그렇지 않으면 사용 되지 않습니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Group 개체(ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>관련 항목  
 [GetPermissions 및 SetPermissions 메서드 예제 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Name 속성 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [SetPermissions 메서드(ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
