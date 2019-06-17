---
title: SetPermissions 메서드 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User25::SetPermissions
- User25::raw_SetPermissions
- _Group25::SetPermissions
- _Group25::raw_SetPermissions
helpviewer_keywords:
- SetPermissions method [ADOX]
ms.assetid: b7f925d7-b05c-4376-bb49-f8d2c17b8b24
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fcc44037ac746621c044bca755fd9b957356dc38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705798"
---
# <a name="setpermissions-method-adox"></a>SetPermissions 메서드(ADOX)
에 대 한 사용 권한을 지정 하는 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 또는 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 개체에 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 A **문자열** 사용 권한을 설정할 개체의 이름을 지정 하는 값입니다.  
  
 *ObjectType*  
 A **긴** 하나일 수 있는 값의는 [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) 권한을 가져올 개체의 형식을 지정 하는 상수입니다.  
  
 *동작*  
 A **긴** 하나일 수 있는 값의 합니다 [ActionEnum](../../../ado/reference/adox-api/actionenum.md) 권한을 설정할 때 수행 하는 동작의 유형을 지정 하는 상수입니다.  
  
 *권한*  
 A **긴** 비트 마스크 일 수 있는 값의 하나 이상의 합니다 [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) 설정에 대 한 권한을 나타내는 상수입니다.  
  
 *상속*  
 (선택 사항) A **긴** 하나일 수 있는 값의는 [InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md) 개체는 이러한 사용 권한을 상속 하는 방법을 지정 하는 상수입니다. 기본값은 **adInheritNone**합니다.  
  
 *ObjectTypeId*  
 (선택 사항) A **Variant** OLE DB 사양에 정의 되지 않은 공급자 개체 형식의 GUID를 지정 하는 값입니다. 이 매개 변수는 필요한 경우 *ObjectType* 로 설정 된 **adPermObjProviderSpecific**고, 그렇지 않으면 사용 되지 않습니다.  
  
## <a name="remarks"></a>Remarks  
 공급자 그룹 또는 사용자에 대 한 액세스 권한 설정을 지원 하지 않는 경우 오류가 발생 합니다.  
  
> [!NOTE]
>  호출할 때 **SetPermissions**, 동작 설정 하는 **adAccessRevoke** 설정을 재정의 합니다 *Rights* 매개 변수입니다. 설정 하지 마세요 *작업* 에 **adAccessRevoke** 에 지정 된 권한을 원하는 경우를 *Rights* 매개 변수를 적용 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Group 개체(ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>관련 항목  
 [GetPermissions 및 SetPermissions 메서드 예제 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions 메서드 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Name 속성(ADOX)](../../../ado/reference/adox-api/name-property-adox.md)
