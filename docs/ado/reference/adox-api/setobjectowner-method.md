---
description: SetObjectOwner 메서드
title: SetObjectOwner 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::SetObjectOwner
- _Catalog::raw_SetObjectOwner
helpviewer_keywords:
- SetObjectOwner method [ADOX]
ms.assetid: e5170a37-9d6e-43db-bfb6-9b6631fa3048
author: rothja
ms.author: jroth
ms.openlocfilehash: acefd94f29b030a6bee724686e11023a354d8921
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769412"
---
# <a name="setobjectowner-method"></a>SetObjectOwner 메서드
[카탈로그](./catalog-object-adox.md)에 있는 개체의 소유자를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Catalog.SetObjectOwner ObjectName, ObjectType, OwnerName [,ObjectTypeId]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ObjectName*  
 소유자를 지정할 개체의 이름을 지정 하는 **문자열** 값입니다.  
  
 *ObjectType*  
 소유자 유형을 지정 하는 [ObjectTypeEnum](./objecttypeenum.md) 상수 중 하나일 수 있는 **Long** 값입니다.  
  
 *OwnerName*  
 개체를 소유할 [사용자](./user-object-adox.md) 또는 [그룹](./group-object-adox.md) 의 [이름을](./name-property-adox.md) 지정 하는 **문자열** 값입니다.  
  
 *ObjectTypeId*  
 선택 사항입니다. OLE DB 사양에서 정의 되지 않은 공급자 개체 유형의 GUID를 지정 하는 **변형** 값입니다. 이 매개 변수는 *ObjectType* 이 **adPermObjProviderSpecific**로 설정 된 경우에 필요 합니다. 그렇지 않은 경우에는 사용 되지 않습니다.  
  
## <a name="remarks"></a>설명  
 공급자가 개체 소유자 지정을 지원 하지 않는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [카탈로그 개체(ADOX)](./catalog-object-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [GetObjectOwner 및 SetObjectOwner 메서드 예제 (VB)](./getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [GetObjectOwner 메서드(ADOX)](./getobjectowner-method-adox.md)