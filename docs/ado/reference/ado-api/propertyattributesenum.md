---
title: PropertyAttributesEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: PropertyAttributesEnum
helpviewer_keywords: PropertyAttributesEnum enumeration [ADO]
ms.assetid: 96a01955-a6b4-4cbf-9c73-52bcd1e9fb25
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 853e63dcd520ab45a26f98091a3e48a816350d0b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
특성을 지정 하는 [속성](../../../ado/reference/ado-api/property-object-ado.md) 개체입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|속성 공급자가 지원 되지 않습니다 나타냅니다.|  
|**adPropRequired**|1.|사용자 데이터 원본이 초기화 되기 전에이 속성의 값을 지정 해야 함을 나타냅니다.|  
|**adPropOptional**|2|사용자 데이터 원본이 초기화 되기 전에이 속성에 대 한 값을 지정할 필요가 없습니다 것을 나타냅니다.|  
|**adPropRead**|512|사용자 속성을 읽을 수를 나타냅니다.|  
|**adPropWrite**|1024|사용자 속성을 설정할 수를 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.PropertyAttributes.NOTSUPPORTED|  
|AdoEnums.PropertyAttributes.REQUIRED|  
|AdoEnums.PropertyAttributes.OPTIONAL|  
|AdoEnums.PropertyAttributes.READ|  
|AdoEnums.PropertyAttributes.WRITE|  
  
## <a name="applies-to"></a>적용 대상  
 [Attributes 속성(ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
