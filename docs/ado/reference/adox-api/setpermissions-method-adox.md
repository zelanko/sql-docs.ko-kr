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
ms.openlocfilehash: 3a13e1dc23556888c2d4ee5c013472614b764d57
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769402"
---
# <a name="setpermissions-method-adox"></a>SetPermissions 메서드(ADOX)
개체의 [그룹](./group-object-adox.md) 또는 [사용자](./user-object-adox.md) 에 대 한 사용 권한을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Name*  
 사용 권한을 설정할 개체의 이름을 지정 하는 **문자열** 값입니다.  
  
 *ObjectType*  
 사용 권한을 가져올 개체의 형식을 지정 하는 **Long** 값으로, [ObjectTypeEnum](./objecttypeenum.md) 상수 중 하나일 수 있습니다.  
  
 *작업*  
 사용 권한을 설정할 때 수행할 동작의 유형을 지정 하는 [Actionenum](./actionenum.md) 상수 중 하나일 수 있는 **Long** 값입니다.  
  
 *권한*  
 설정할 권한을 나타내는 하나 이상의 [RightsEnum](./rightsenum.md) 상수에 대 한 비트 마스크 일 수 있는 **Long** 값입니다.  
  
 *계승*  
 선택 사항입니다. 개체에서 이러한 사용 권한을 상속 하는 방법을 지정 하는 **Long** 값 ( [InheritTypeEnum](./inherittypeenum.md) 상수 중 하나일 수 있음) 기본값은 **adInheritNone**입니다.  
  
 *ObjectTypeId*  
 선택 사항입니다. OLE DB 사양에서 정의 되지 않은 공급자 개체 유형의 GUID를 지정 하는 **변형** 값입니다. 이 매개 변수는 *ObjectType* 이 **adPermObjProviderSpecific**로 설정 된 경우에 필요 합니다. 그렇지 않은 경우에는 사용 되지 않습니다.  
  
## <a name="remarks"></a>설명  
 공급자가 그룹 또는 사용자에 대 한 액세스 권한을 설정 하는 것을 지원 하지 않으면 오류가 발생 합니다.  
  
> [!NOTE]
>  **SetPermissions**를 호출할 때 **Adaccessrevoke** 로 작업을 설정 하면 *Rights* 매개 변수의 모든 설정이 재정의 됩니다. *Rights* 매개 변수에 지정 된 권한이 적용 되도록 하려면 *작업* 을 **adaccessrevoke** 로 설정 하지 마세요.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [그룹 개체(ADOX)](./group-object-adox.md)  
    :::column-end:::
    :::column:::
        [사용자 개체(ADOX)](./user-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [GetPermissions 및 SetPermissions 메서드 예제 (VB)](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions 메서드 (ADOX)](./getpermissions-method-adox.md)   
 [Name 속성(ADOX)](./name-property-adox.md)