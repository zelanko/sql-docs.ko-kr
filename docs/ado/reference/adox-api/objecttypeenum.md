---
title: ObjectTypeEnum | Microsoft Docs
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
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8eb88d7f3df60d8c54782d20af73e3fd5e917db3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="objecttypeenum"></a>ObjectTypeEnum
사용 권한 또는 소유권을 설정 하는 데이터베이스 개체의 유형을 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|개체에는 열입니다.|  
|**adPermObjDatabase**|3|개체는 데이터베이스입니다.|  
|**adPermObjProcedure**|4|개체는 프로시저입니다.|  
|**adPermObjProviderSpecific**|-1|개체는 공급자에 의해 정의 된 형식입니다. 경우 오류가 발생 합니다는 *ObjectType* 매개 변수는 **adPermObjProviderSpecific** 및 *ObjectTypeId* 제공 되지 않았습니다.|  
|**adPermObjTable**|1.|개체는 테이블입니다.|  
|**adPermObjView**|5|뷰는 개체가입니다.|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[GetObjectOwner 메서드(ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions 메서드(ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner 메서드](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions 메서드(ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
