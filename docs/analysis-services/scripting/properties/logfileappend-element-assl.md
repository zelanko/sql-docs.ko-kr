---
title: LogFileAppend 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a00ea15629d1ffe52dad20fad84d52a242bf900f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="logfileappend-element-assl"></a>LogFileAppend 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Traces 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/collections/traces-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
