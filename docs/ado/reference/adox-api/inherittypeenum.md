---
description: InheritTypeEnum
title: InheritTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 37c6eba57eb7efb05d2b718e294e33b9616cac77
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984104"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
개체가 [SetPermissions](./setpermissions-method-adox.md)로 설정 된 사용 권한을 상속 하는 방법을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|주 개체에 포함 된 개체와 기타 컨테이너는 모두 항목을 상속 합니다.|  
|**adInheritContainers**|2|주 개체에 포함 된 다른 컨테이너는 항목을 상속 합니다.|  
|**adInheritNone**|0|기본값 상속이 발생 하지 않습니다.|  
|**adInheritNoPropagate**|4|**AdInheritObjects** 및 **adInheritContainers** 플래그는 상속 된 항목으로 전파 되지 않습니다.|  
|**adInheritObjects**|1|컨테이너의 컨테이너가 아닌 개체는 권한을 상속 합니다.|  
  
## <a name="applies-to"></a>적용 대상  
 [SetPermissions 메서드(ADOX)](./setpermissions-method-adox.md)