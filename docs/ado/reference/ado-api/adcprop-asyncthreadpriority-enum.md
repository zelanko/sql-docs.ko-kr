---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11e7151dea1e522b1c265313043f840c2cced8a4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="adcpropasyncthreadpriorityenum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
에 RDS [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체, 데이터를 검색 하는 비동기 스레드의 실행 우선 순위를 지정 합니다.  
  
 이러한 상수를 사용 하 여는 **레코드 집합** "**백그라운드 스레드 우선 순위**" ADO OLE DB의 동적 속성 인덱스에서 참조 되며에 설명 되어 있는 동적 속성은 [ OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 설명서입니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|보통 및 높은 우선 순위를 설정입니다.|  
|**adPriorityBelowNormal**|2|및 가장 낮은 우선 순위를 설정합니다.|  
|**adPriorityHighest**|5|가능한 가장 높은 우선 순위를 설정합니다.|  
|**AdPriorityLowest**|1.|가능한 가장 낮은 우선 순위를 설정합니다.|  
|**adPriorityNormal**|3|우선 순위를 normal로 설정합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.AdcPropAsyncThreadPriority.ABOVENORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.BELOWNORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.HIGHEST|  
|AdoEnums.AdcPropAsyncThreadPriority.LOWEST|  
|AdoEnums.AdcPropAsyncThreadPriority.NORMAL|
