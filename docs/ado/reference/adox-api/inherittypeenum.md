---
title: InheritTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 249616f2f08b8b8f6138ce13621d26c5f7af9e1e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47647811"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
개체는 사용 하 여 설정 하는 사용 권한을 상속 하는 방법 지정 [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|개체와 다른 컨테이너는 기본 개체에 포함 된 항목을 상속 합니다.|  
|**adInheritContainers**|2|다른 컨테이너는 기본 개체에 포함 된 항목을 상속 합니다.|  
|**adInheritNone**|0|기본. 상속 하지 발생합니다.|  
|**adInheritNoPropagate**|4|합니다 **adInheritObjects** 하 고 **adInheritContainers** 플래그는 상속 된 항목에 전파 되지 않습니다.|  
|**adInheritObjects**|1|컨테이너의 비-컨테이너 개체 사용 권한을 상속 합니다.|  
  
## <a name="applies-to"></a>적용 대상  
 [SetPermissions 메서드(ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
