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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9a2bbb889bc0277ab01f29896d4f60eebd8236cb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759169"
---
# <a name="getpermissions-method-adox"></a>GetPermissions 메서드(ADOX)
개체 또는 개체 컨테이너의 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 또는 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 에 대 한 권한을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Return Value  
 그룹이 나 사용자가 개체에 대해 갖는 사용 권한을 포함 하는 비트 마스크를 지정 하는 **Long** 값을 반환 합니다. 이 값은 하나 이상의 [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) 상수 일 수 있습니다.  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 사용 권한을 설정할 개체의 이름을 지정 하는 **Variant** 값입니다. 개체 컨테이너에 대 한 사용 권한을 얻으려면 *이름* 을 null 값으로 설정 합니다.  
  
 *ObjectType*  
 사용 권한을 가져올 개체의 형식을 지정 하는 **Long** 값으로, [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) 상수 중 하나일 수 있습니다.  
  
 *ObjectTypeId*  
 (선택 사항) OLE DB 사양에서 정의 되지 않은 공급자 개체 유형의 GUID를 지정 하는 **변형** 값입니다. 이 매개 변수는 *ObjectType* 이 **adPermObjProviderSpecific**로 설정 된 경우에 필요 합니다. 그렇지 않은 경우에는 사용 되지 않습니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Group 개체(ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>참고 항목  
 [GetPermissions 및 SetPermissions 메서드 예제 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Name 속성 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [SetPermissions 메서드(ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
