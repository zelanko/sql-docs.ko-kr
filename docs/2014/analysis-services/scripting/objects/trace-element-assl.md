---
title: Trace 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Trace Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Trace
helpviewer_keywords:
- Trace element
ms.assetid: dda9136a-a9c1-44a1-b8d3-b0ec4dc65c87
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8951414231fa8730f1babd3638d9e468624b94a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056353"
---
# <a name="trace-element-assl"></a>Trace 요소(ASSL)
  쿼리할 수 있는 추적을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
      Profiler syntax  
<Traces>  
   <Trace>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LogFileName>...</LogFileName>  
      <LogFileAppend>...</LogFileAppend>  
      <LogFileSize>...</LogFileSize>  
      <Audit>...</Audit>  
      <LogFileRollover>...</LogFileRollover>  
      <AutoRestart>...</AutoRestart>  
      <StopTime>...</StopTime>  
      <Filter>...</Filter>  
      <Events>...</Events>  
      <Annotations>...</Annotations>  
   </Trace>  
</Traces>  
```  
  
```  
  
      Extended Events syntax  
<Traces>  
   <Trace>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <XEvent>...</XEvent>  
      <Annotations>...</Annotations>  
   </Trace>  
</Traces>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[추적](../collections/traces-element-assl.md)|  
|자식 요소|[주석을](../collections/annotations-element-assl.md), [감사](../properties/audit-element-assl.md), [AutoRestart](../properties/autorestart-element-assl.md)를 [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)를 [설명](../properties/description-element-assl.md), [이벤트](../collections/events-element-assl.md), [필터](../properties/filter-element-trace-assl.md)를 [ID](../properties/id-element-assl.md)를 [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)를 [LogFileAppend](../properties/logfileappend-element-assl.md), [LogFileName](../properties/name-element-assl.md), [LogFileRollover](../properties/logfilerollover-element-assl.md), [LogFileSize](../properties/logfilesize-element-assl.md)하십시오 [이름](../properties/name-element-assl.md), [StopTime](../properties/stoptime-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Trace>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Server 요소 &#40;ASSL&#41;](server-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
