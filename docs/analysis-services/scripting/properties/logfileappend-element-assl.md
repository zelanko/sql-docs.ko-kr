---
title: "LogFileAppend 요소 (ASSL) | Microsoft Docs"
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
apiname: LogFileAppend Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: LogFileAppend
helpviewer_keywords: LogFileAppend element
ms.assetid: f85e94a9-e5c5-478a-a5a0-fc99ed19b582
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a6af2ce43451db0ed1c0eee88c6248d8487639aa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="logfileappend-element-assl"></a>LogFileAppend 요소(ASSL)
  결정 여부는 [추적](../../../analysis-services/scripting/objects/trace-element-assl.md) 요소가 해당 로깅 출력을 기존 로그 파일에 아니면 덮어쓸지가 됩니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Trace>  
  
   <LogFileAppend>...</LogFileAppend>  
  
</Trace>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|False|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[추적](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **LogFileAppend** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Trace>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Traces 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/traces-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
