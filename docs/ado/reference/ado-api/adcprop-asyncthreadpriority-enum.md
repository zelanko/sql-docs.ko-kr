---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0b9d4e0e6f844ef2dda18e95aadfcf3b910995d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47824651"
---
# <a name="adcpropasyncthreadpriorityenum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
rds [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체, 데이터를 검색 하는 비동기 스레드 실행 우선 순위를 지정 합니다.  
  
 사용 하 여 이러한 상수를 사용 합니다 **레코드 집합** "**백그라운드 스레드 우선 순위**" ADO-OLE DB의 동적 속성 인덱스에서 참조 되며에 설명 된 동적 속성을 [ OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 설명서.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|보통 및 높은 사이의 우선 순위를 설정합니다.|  
|**adPriorityBelowNormal**|2|최저 및 일반 사이의 우선 순위를 설정합니다.|  
|**adPriorityHighest**|5|가능한 가장 높은 우선 순위를 설정합니다.|  
|**AdPriorityLowest**|1|가능한 가장 낮은 우선 순위를 설정합니다.|  
|**adPriorityNormal**|3|Normal 우선 순위를 설정합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.AdcPropAsyncThreadPriority.ABOVENORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.BELOWNORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.HIGHEST|  
|AdoEnums.AdcPropAsyncThreadPriority.LOWEST|  
|AdoEnums.AdcPropAsyncThreadPriority.NORMAL|
