---
description: GetObjectOwner 메서드(ADOX)
title: GetObjectOwner 메서드 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f065e2625afa088489f08ade9f4ef00c5eb7d4d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984544"
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner 메서드(ADOX)
[카탈로그](./catalog-object-adox.md)에 있는 개체의 소유자를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Return Value  
 개체를 소유 하는 [사용자](./user-object-adox.md) 또는 [그룹](./group-object-adox.md) 의 [이름을](./name-property-adox.md) 지정 하는 **문자열** 값을 반환 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *ObjectName*  
 소유자를 반환할 개체의 이름을 지정 하는 **문자열** 값입니다.  
  
 *ObjectType*  
 [ObjectTypeEnum](./objecttypeenum.md) 상수 중 하나일 수 있는 **Long** 값으로, 소유자를 가져올 개체의 형식을 지정 합니다.  
  
 *ObjectTypeId*  
 선택 사항입니다. OLE DB 사양에서 정의 되지 않은 공급자 개체 유형의 GUID를 지정 하는 **변형** 값입니다. 이 매개 변수는 *ObjectType* 이 **adPermObjProviderSpecific**로 설정 된 경우에 필요 합니다. 그렇지 않은 경우에는 사용 되지 않습니다.  
  
## <a name="remarks"></a>설명  
 공급자가 개체 소유자 반환을 지원 하지 않으면 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [카탈로그 개체(ADOX)](./catalog-object-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [GetObjectOwner 및 SetObjectOwner 메서드 예제 (VB)](./getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner 메서드](./setobjectowner-method.md)