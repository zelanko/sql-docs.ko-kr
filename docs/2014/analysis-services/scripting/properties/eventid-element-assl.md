---
title: EventID 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- EventID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EventID
helpviewer_keywords:
- EventID element
ms.assetid: a6b2ee50-1753-496c-af5c-206d63f2542b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d8f1f785d365b1899185297d903c81871fc3df41
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218892"
---
# <a name="eventid-element-assl"></a>EventID 요소(ASSL)
  고유 하 게 식별 하는 [이벤트](../objects/event-element-assl.md) 의 일환으로 캡처할 수 있는 요소를 [추적](../objects/trace-element-assl.md) 요소.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Event>  
  
      <EventID>...</EventID>  
  
</Event>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[이벤트](../objects/event-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 요소가 `EventID` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.TraceEvent>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Events 요소 &#40;ASSL&#41;](../collections/events-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
