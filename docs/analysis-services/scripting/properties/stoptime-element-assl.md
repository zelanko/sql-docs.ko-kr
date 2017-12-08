---
title: "StopTime 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: StopTime Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: StopTime
helpviewer_keywords: StopTime element
ms.assetid: 6f863d53-033b-46e0-9837-e891e739b4b0
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 62690b30361e5f52cdc56226e31c209d60e75f1d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="stoptime-element-assl"></a>StopTime 요소(ASSL)
  날짜 및 시간을 지정 된 [추적](../../../analysis-services/scripting/objects/trace-element-assl.md) 요소를 중지 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Trace>  
   ...  
   <StopTime>...</StopTime>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|DateTime|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[추적](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|자식 요소|없음|  
  
 부모에 해당 하는 요소 **StopTime** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Trace>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Traces 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/traces-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
