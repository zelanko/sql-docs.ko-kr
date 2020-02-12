---
title: GetObjectOwner 메서드 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ff85491cf7ca30e3f95526aa7043f321a65cccc5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966273"
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner 메서드(ADOX)
[카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md)에 있는 개체의 소유자를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Return Value  
 개체를 소유 하는 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 또는 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 의 [이름을](../../../ado/reference/adox-api/name-property-adox.md) 지정 하는 **문자열** 값을 반환 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *ObjectName*  
 소유자를 반환할 개체의 이름을 지정 하는 **문자열** 값입니다.  
  
 *ObjectType*  
 [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) 상수 중 하나일 수 있는 **Long** 값으로, 소유자를 가져올 개체의 형식을 지정 합니다.  
  
 *ObjectTypeId*  
 (선택 사항) OLE DB 사양에서 정의 되지 않은 공급자 개체 유형의 GUID를 지정 하는 **변형** 값입니다. 이 매개 변수는 *ObjectType* 이 **adPermObjProviderSpecific**로 설정 된 경우에 필요 합니다. 그렇지 않은 경우에는 사용 되지 않습니다.  
  
## <a name="remarks"></a>설명  
 공급자가 개체 소유자 반환을 지원 하지 않으면 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [카탈로그 개체(ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [GetObjectOwner 및 SetObjectOwner 메서드 예제 (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner 메서드](../../../ado/reference/adox-api/setobjectowner-method.md)
