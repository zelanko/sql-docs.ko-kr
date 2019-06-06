---
title: ObjectTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4239cd2e62db43b4316bad5edbf989f29709213a
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706238"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
사용 권한 또는 소유권을 설정 하는 데이터베이스 개체의 형식을 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|개체에는 열입니다.|  
|**adPermObjDatabase**|3|개체는 데이터베이스입니다.|  
|**adPermObjProcedure**|4|개체는 프로시저입니다.|  
|**adPermObjProviderSpecific**|-1|개체는 공급자에 의해 정의 된 형식입니다. 오류가 발생 하는 경우는 *ObjectType* 매개 변수는 **adPermObjProviderSpecific** 와 *ObjectTypeId* 제공 하지 않으면.|  
|**adPermObjTable**|1|개체는 테이블입니다.|  
|**adPermObjView**|5|개체는 보기입니다.|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[GetObjectOwner 메서드(ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions 메서드(ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner 메서드](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions 메서드(ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
