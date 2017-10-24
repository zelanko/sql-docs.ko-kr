---
title: InheritTypeEnum | Microsoft Docs
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
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 36570c508955b82ccd403e9af10895edc1584d9f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="inherittypeenum"></a>InheritTypeEnum
개체는 사용 하 여 설정 하는 사용 권한을 상속 하는 방법을 지정 [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|개체와의 주요 개체에 포함 된 다른 컨테이너의 항목을 상속 합니다.|  
|**adInheritContainers**|2|기본 개체에 포함 하는 다른 컨테이너의 항목을 상속 합니다.|  
|**adInheritNone**|0|기본. 없음 상속이 발생합니다.|  
|**adInheritNoPropagate**|4|**adInheritObjects** 및 **adInheritContainers** 플래그 상속 된 항목에 전파 되지 않습니다.|  
|**adInheritObjects**|1.|컨테이너의 아닌 컨테이너 개체 사용 권한을 상속 합니다.|  
  
## <a name="applies-to"></a>적용 대상  
 [SetPermissions 메서드(ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)

