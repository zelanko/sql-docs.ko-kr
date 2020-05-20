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
author: rothja
ms.author: jroth
ms.openlocfilehash: d493218f31965c04b5a64321c4a1bf87a2518f6f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763794"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
사용 권한이 나 소유권을 설정할 데이터베이스 개체의 유형을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|개체는 열입니다.|  
|**adPermObjDatabase**|3|개체가 데이터베이스입니다.|  
|**adPermObjProcedure**|4|개체는 프로시저입니다.|  
|**adPermObjProviderSpecific**|-1|개체는 공급자에 의해 정의 되는 형식입니다. *ObjectType* 매개 변수를 **AdPermObjProviderSpecific** 하 고 *objecttypeid* 를 제공 하지 않으면 오류가 발생 합니다.|  
|**adPermObjTable**|1|개체는 테이블입니다.|  
|**adPermObjView**|5|개체가 뷰입니다.|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[GetObjectOwner 메서드(ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions 메서드(ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner 메서드](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions 메서드(ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
