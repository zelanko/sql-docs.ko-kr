---
title: PropertyAttributesEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 99acfb2507701f0e4b47aff5b0595b61fc45c425
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719140"
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
특성을 지정 하는 [속성](../../../ado/reference/ado-api/property-object-ado.md) 개체입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|속성 공급자가 지원 되지 않습니다 나타냅니다.|  
|**adPropRequired**|1|사용자 데이터 소스가 초기화 되기 전에이 속성에 값을 지정 해야 함을 나타냅니다.|  
|**adPropOptional**|2|사용자 데이터 소스가 초기화 되기 전에이 속성의 값을 지정할 필요가 없습니다 나타냅니다.|  
|**adPropRead**|512|사용자 속성을 읽을 수 있는지를 나타냅니다.|  
|**adPropWrite**|1024|사용자 속성을 설정할 수 있는지를 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.PropertyAttributes.NOTSUPPORTED|  
|AdoEnums.PropertyAttributes.REQUIRED|  
|AdoEnums.PropertyAttributes.OPTIONAL|  
|AdoEnums.PropertyAttributes.READ|  
|AdoEnums.PropertyAttributes.WRITE|  
  
## <a name="applies-to"></a>적용 대상  
 [Attributes 속성(ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
