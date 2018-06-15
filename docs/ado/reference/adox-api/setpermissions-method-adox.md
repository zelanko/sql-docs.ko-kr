---
title: SetPermissions 메서드 (ADOX) | Microsoft Docs
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
- User25::SetPermissions
- User25::raw_SetPermissions
- _Group25::SetPermissions
- _Group25::raw_SetPermissions
helpviewer_keywords:
- SetPermissions method [ADOX]
ms.assetid: b7f925d7-b05c-4376-bb49-f8d2c17b8b24
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cb3bb780109c61b5d481d0d0d3bae56badea819
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35286814"
---
# <a name="setpermissions-method-adox"></a>SetPermissions 메서드 (ADOX)
에 대 한 사용 권한을 지정는 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 또는 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 개체에 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 A **문자열** 사용 권한을 설정 하려는 개체의 이름을 지정 하는 값입니다.  
  
 *ObjectType*  
 A **긴** 하나일 수 있는 값의는 [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) 권한을 얻을 수 있는 작업에 대 한 개체의 유형을 지정 하는 상수입니다.  
  
 *동작*  
 A **긴** 하나일 수 있는 값의는 [ActionEnum](../../../ado/reference/adox-api/actionenum.md) 권한을 설정할 때 수행할 작업의 유형을 지정 하는 상수입니다.  
  
 *권한*  
 A **긴** 비트 마스크 될 수 있는 값의 하나 이상의 [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) 설정에 대 한 권한을 나타내는 상수입니다.  
  
 *상속*  
 (선택 사항) A **긴** 하나일 수 있는 값의는 [InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md) 개체는 이러한 사용 권한을 상속 하는 방법을 지정 하는 상수입니다. 기본값은 **adInheritNone**합니다.  
  
 *ObjectTypeId*  
 (선택 사항) A **Variant** OLE DB 사양에 정의 되지 않은 공급자 개체 형식에 대 한 GUID를 지정 하는 값입니다. 경우에이 매개 변수는 필수 *ObjectType* 로 설정 되어 **adPermObjProviderSpecific**, 그렇지 않으면 사용 되지 않습니다.  
  
## <a name="remarks"></a>Remarks  
 공급자 그룹 또는 사용자에 대 한 액세스 권한 설정을 지원 하지 않는 경우 오류가 발생 합니다.  
  
> [!NOTE]
>  호출할 때 **SetPermissions**, 동작 설정 하는 **adAccessRevoke** 의 설정을 재정의 *권한* 매개 변수입니다. 설정 하지 않으면 *동작* 를 **adAccessRevoke** 에 지정 된 권한을 하려는 경우는 *권한* 매개 변수를 적용 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Group 개체(ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>관련 항목  
 [GetPermissions 및 SetPermissions 메서드 예제 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions 메서드 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Name 속성(ADOX)](../../../ado/reference/adox-api/name-property-adox.md)
