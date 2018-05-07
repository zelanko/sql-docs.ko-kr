---
title: Trace 요소 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 420150dbdf4910683fc78c8c364d2cf0976adfc3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="trace-element-assl"></a>Trace 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
      <AutoRestart>...</AutoRestart>
      <XEvent>...</XEvent>  
      <Annotations>...</Annotations>  
   </Trace>  
</Traces>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[추적](../../../analysis-services/scripting/collections/traces-element-assl.md)|  
|자식 요소|[주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [감사](../../../analysis-services/scripting/properties/audit-element-assl.md), [AutoRestart](../../../analysis-services/scripting/properties/autorestart-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [설명](../../../analysis-services/scripting/properties/description-element-assl.md), [이벤트](../../../analysis-services/scripting/collections/events-element-assl.md), [필터](../../../analysis-services/scripting/properties/filter-element-trace-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [LogFileAppend](../../../analysis-services/scripting/properties/logfileappend-element-assl.md), [LogFileName](../../../analysis-services/scripting/properties/logfilename-element-assl.md), [LogFileRollover](../../../analysis-services/scripting/properties/logfilerollover-element-assl.md), [LogFileSize](../../../analysis-services/scripting/properties/logfilesize-element-assl.md), [이름](../../../analysis-services/scripting/properties/name-element-assl.md), [StopTime](../../../analysis-services/scripting/properties/stoptime-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Trace>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Server 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [개체 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
