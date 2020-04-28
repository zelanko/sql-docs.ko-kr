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
ms.openlocfilehash: 04c7b1d1cb5d07a300b82d13a7e80158498bbd5f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965657"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
사용 권한이 나 소유권을 설정할 데이터베이스 개체의 유형을 지정 합니다.  
  
|상수|값|Description|  
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
