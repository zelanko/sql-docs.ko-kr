---
title: "SetObjectOwner 메서드 | Microsoft Docs"
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
- _Catalog::SetObjectOwner
- _Catalog::raw_SetObjectOwner
helpviewer_keywords:
- SetObjectOwner method [ADOX]
ms.assetid: e5170a37-9d6e-43db-bfb6-9b6631fa3048
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 33226468d9d1f556d2cf7ec3edac37375b0c8d84
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setobjectowner-method"></a>SetObjectOwner 메서드
에 있는 개체의 소유자를 지정 된 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Catalog.SetObjectOwner ObjectName, ObjectType, OwnerName [,ObjectTypeId]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ObjectName*  
 A **문자열** 소유자를 지정 하는 작업에 대 한 개체의 이름을 지정 하는 값입니다.  
  
 *ObjectType*  
 A **긴** 하나일 수 있는 값의는 [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) 소유자 유형을 지정 하는 상수입니다.  
  
 *OwnerName*  
 A **문자열** 지정 하는 값은 [이름](../../../ado/reference/adox-api/name-property-adox.md) 의 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 또는 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 는 개체를 소유 합니다.  
  
 *ObjectTypeId*  
 (선택 사항) A **Variant** OLE DB 사양에 정의 되지 않은 공급자 개체 형식에 대 한 GUID를 지정 하는 값입니다. 경우에이 매개 변수는 필수 *ObjectType* 로 설정 되어 **adPermObjProviderSpecific**, 그렇지 않으면 사용 되지 않습니다.  
  
## <a name="remarks"></a>주의  
 공급자 개체 소유자를 지정 하 여 지원 하지 않는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Catalog 개체(ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>관련 항목:  
 [GetObjectOwner 및 SetObjectOwner 메서드 예제 (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [GetObjectOwner 메서드(ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)

