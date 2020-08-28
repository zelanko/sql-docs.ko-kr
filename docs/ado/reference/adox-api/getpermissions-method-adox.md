---
description: GetPermissions 메서드(ADOX)
title: GetPermissions 메서드 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 31d2bd1d17f790a29674b99ee24a668876e53492
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984424"
---
# <a name="getpermissions-method-adox"></a>GetPermissions 메서드(ADOX)
개체 또는 개체 컨테이너의 [그룹](./group-object-adox.md) 또는 [사용자](./user-object-adox.md) 에 대 한 권한을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Return Value  
 그룹이 나 사용자가 개체에 대해 갖는 사용 권한을 포함 하는 비트 마스크를 지정 하는 **Long** 값을 반환 합니다. 이 값은 하나 이상의 [RightsEnum](./rightsenum.md) 상수 일 수 있습니다.  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 사용 권한을 설정할 개체의 이름을 지정 하는 **Variant** 값입니다. 개체 컨테이너에 대 한 사용 권한을 얻으려면 *이름* 을 null 값으로 설정 합니다.  
  
 *ObjectType*  
 사용 권한을 가져올 개체의 형식을 지정 하는 **Long** 값으로, [ObjectTypeEnum](./objecttypeenum.md) 상수 중 하나일 수 있습니다.  
  
 *ObjectTypeId*  
 선택 사항입니다. OLE DB 사양에서 정의 되지 않은 공급자 개체 유형의 GUID를 지정 하는 **변형** 값입니다. 이 매개 변수는 *ObjectType* 이 **adPermObjProviderSpecific**로 설정 된 경우에 필요 합니다. 그렇지 않은 경우에는 사용 되지 않습니다.  
  
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
 [Name 속성 (ADOX)](./name-property-adox.md)   
 [SetPermissions 메서드(ADOX)](./setpermissions-method-adox.md)