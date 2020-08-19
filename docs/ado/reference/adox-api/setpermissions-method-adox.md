---
description: SetPermissions 메서드(ADOX)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3d5af996442e0451a80265b7fbd9fb31450f9475
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439525"
---
# <a name="setpermissions-method-adox"></a>SetPermissions 메서드(ADOX)
개체의 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 또는 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 에 대 한 사용 권한을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 사용 권한을 설정할 개체의 이름을 지정 하는 **문자열** 값입니다.  
  
 *ObjectType*  
 사용 권한을 가져올 개체의 형식을 지정 하는 **Long** 값으로, [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) 상수 중 하나일 수 있습니다.  
  
 *동작*  
 사용 권한을 설정할 때 수행할 동작의 유형을 지정 하는 [Actionenum](../../../ado/reference/adox-api/actionenum.md) 상수 중 하나일 수 있는 **Long** 값입니다.  
  
 *권한*  
 설정할 권한을 나타내는 하나 이상의 [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) 상수에 대 한 비트 마스크 일 수 있는 **Long** 값입니다.  
  
 *계승*  
 (선택 사항) 개체에서 이러한 사용 권한을 상속 하는 방법을 지정 하는 **Long** 값 ( [InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md) 상수 중 하나일 수 있음) 기본값은 **adInheritNone**입니다.  
  
 *ObjectTypeId*  
 (선택 사항) OLE DB 사양에서 정의 되지 않은 공급자 개체 유형의 GUID를 지정 하는 **변형** 값입니다. 이 매개 변수는 *ObjectType* 이 **adPermObjProviderSpecific**로 설정 된 경우에 필요 합니다. 그렇지 않은 경우에는 사용 되지 않습니다.  
  
## <a name="remarks"></a>설명  
 공급자가 그룹 또는 사용자에 대 한 액세스 권한을 설정 하는 것을 지원 하지 않으면 오류가 발생 합니다.  
  
> [!NOTE]
>  **SetPermissions**를 호출할 때 **Adaccessrevoke** 로 작업을 설정 하면 *Rights* 매개 변수의 모든 설정이 재정의 됩니다. *Rights* 매개 변수에 지정 된 권한이 적용 되도록 하려면 *작업* 을 **adaccessrevoke** 로 설정 하지 마세요.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Group 개체(ADOX)](../../../ado/reference/adox-api/group-object-adox.md)  
    :::column-end:::
    :::column:::
        [User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [GetPermissions 및 SetPermissions 메서드 예제 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions 메서드 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Name 속성(ADOX)](../../../ado/reference/adox-api/name-property-adox.md)
