---
title: "GetObjectOwner 메서드 (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c3c6f6aa4401646f43dd303988cc151d1ed43d21
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner 메서드 (ADOX)
에 있는 개체의 소유자 반환는 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 **문자열** 지정 하는 값의 [이름](../../../ado/reference/adox-api/name-property-adox.md) 의 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 또는 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 개체를 소유 하는 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *ObjectName*  
 A **문자열** 를 소유자를 반환할 개체의 이름을 지정 하는 값입니다.  
  
 *ObjectType*  
 A **긴** 하나일 수 있는 값의는 [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) 을 소유자를 가져올 개체의 유형을 지정 하는 상수입니다.  
  
 *ObjectTypeId*  
 (선택 사항) A **Variant** OLE DB 사양에 정의 되지 공급자 개체 형식에 대 한 GUID를 지정 하는 값입니다. 경우에이 매개 변수는 필수 *ObjectType* 로 설정 되어 **adPermObjProviderSpecific**, 그렇지 않으면 사용 되지 않습니다.  
  
## <a name="remarks"></a>주의  
 공급자 개체 소유자 반환을 지원 하지 않는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Catalog 개체(ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>관련 항목:  
 [GetObjectOwner 및 SetObjectOwner 메서드 예제 (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner 메서드](../../../ado/reference/adox-api/setobjectowner-method.md)

