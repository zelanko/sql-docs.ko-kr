---
description: PropertyAttributesEnum
title: PropertyAttributesEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PropertyAttributesEnum
helpviewer_keywords:
- PropertyAttributesEnum enumeration [ADO]
ms.assetid: 96a01955-a6b4-4cbf-9c73-52bcd1e9fb25
author: rothja
ms.author: jroth
ms.openlocfilehash: fec6a7ccb1b097a4927e7c82d4b0e31265cba1a1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989954"
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
[속성](./property-object-ado.md) 개체의 특성을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|공급자가 속성을 지원 하지 않음을 나타냅니다.|  
|**adPropRequired**|1|사용자가 데이터 소스가 초기화 되기 전에이 속성의 값을 지정 해야 함을 나타냅니다.|  
|**adPropOptional**|2|사용자가 데이터 원본이 초기화 되기 전에이 속성의 값을 지정할 필요가 없음을 나타냅니다.|  
|**adPropRead**|512|사용자가 속성을 읽을 수 있음을 나타냅니다.|  
|**adPropWrite**|1024|사용자가 속성을 설정할 수 있음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums가 지원 됩니다.|  
|AdoEnums 특성이 필요 합니다.|  
|AdoEnums 특성을 선택 합니다.|  
|AdoEnums|  
|AdoEnums|  
  
## <a name="applies-to"></a>적용 대상  
 [Attributes 속성(ADO)](./attributes-property-ado.md)