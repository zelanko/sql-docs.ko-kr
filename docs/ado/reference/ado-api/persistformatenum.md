---
description: PersistFormatEnum
title: PersistFormatEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
author: rothja
ms.author: jroth
ms.openlocfilehash: d4f83189a241b396cba613d9df0d6c0b1aa1328e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773222"
---
# <a name="persistformatenum"></a>PersistFormatEnum
[레코드 집합](./recordset-object-ado.md)을 저장할 형식을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|Microsoft ADTG (Advanced Data TableGram) 형식을 나타냅니다.|  
|**adPersistADO**|1|ADO의 자체 XML(Extensible Markup Language) (XML) 형식이 사용 됨을 나타냅니다. 이 값은 adPersistXML과 같으며 이전 버전과의 호환성을 위해 포함 되었습니다.|  
|**adPersistXML**|1|XML(Extensible Markup Language) (XML) 형식을 나타냅니다.|  
|**adPersistProviderSpecific**|2|공급자가 자체 형식을 사용 하 여 **레코드 집합** 을 유지 함을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums. ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>적용 대상  
 [Save 메서드](./save-method.md)