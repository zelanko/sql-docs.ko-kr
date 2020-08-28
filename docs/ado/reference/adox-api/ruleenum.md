---
description: RuleEnum
title: RuleEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 66367d872e27629f1bf437961b99908d0c42e9f2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983374"
---
# <a name="ruleenum"></a>RuleEnum
[키](./key-object-adox.md) 를 삭제할 때 따라야 하는 규칙을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|Cascade 변경|  
|**adRINone**|0|기본값 아무 동작도 수행되지 않습니다.|  
|**adRISetDefault**|3|외래 키 값이 기본값으로 설정 됩니다.|  
|**adRISetNull**|2|외래 키 값이 null로 설정 됩니다.|  
  
## <a name="applies-to"></a>적용 대상  
 [DeleteRule 속성(ADOX)](./deleterule-property-adox.md)