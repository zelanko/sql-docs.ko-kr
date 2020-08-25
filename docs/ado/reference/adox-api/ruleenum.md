---
description: RuleEnum
title: RuleEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RuleEnum
helpviewer_keywords:
- RuleEnum enumeration [ADOX]
ms.assetid: 738fd3ff-3daf-483d-a0b9-88bef1be54c1
author: rothja
ms.author: jroth
ms.openlocfilehash: da49bbacf8ba59ba12f59fb072e9b5ec8c2ec2ea
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769462"
---
# <a name="ruleenum"></a>RuleEnum
[키](./key-object-adox.md) 를 삭제할 때 따라야 하는 규칙을 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|Cascade 변경|  
|**adRINone**|0|기본값 아무 동작도 수행되지 않습니다.|  
|**adRISetDefault**|3|외래 키 값이 기본값으로 설정 됩니다.|  
|**adRISetNull**|2|외래 키 값이 null로 설정 됩니다.|  
  
## <a name="applies-to"></a>적용 대상  
 [DeleteRule 속성(ADOX)](./deleterule-property-adox.md)