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
ms.openlocfilehash: 22a8cd4bb8d1bdddbaaa68e92349d9c728557ac0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921462"
---
# <a name="adcprop_asyncthreadpriority_enum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
RDS [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 경우 데이터를 검색 하는 비동기 스레드의 실행 우선 순위를 지정 합니다.  
  
 이러한 상수를 **레코드 집합** "**백그라운드 스레드 우선 순위**"와 함께 사용 합니다. 동적 속성은 ADO to OLE DB 동적 속성 인덱스에서 참조 되며 [Microsoft Cursor Service for OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 설명서에 설명 되어 있습니다.  
  
|지속적임|값|Description|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|보통에서 가장 높은 우선 순위를 설정 합니다.|  
|**adPriorityBelowNormal**|2|우선 순위를 최저에서 보통 사이로 설정 합니다.|  
|**adPriorityHighest**|5|우선 순위를 최대한 높게 설정 합니다.|  
|**AdPriorityLowest**|1|우선 순위를 가장 낮은 수로 설정 합니다.|  
|**adPriorityNormal**|3|우선 순위를 보통으로 설정 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|지속적임|  
|--------------|  
|AdoEnums을 ABOVENORMAL 합니다.|  
|AdoEnums을 BELOWNORMAL 합니다.|  
|AdoEnums입니다. 가장 높음|  
|AdoEnums. AdcPropAsyncThreadPriority. 최하위|  
|AdoEnums (영문). 보통|
