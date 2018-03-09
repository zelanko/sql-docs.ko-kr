---
title: "EventColumn 데이터 형식 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: EventColumn Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: EventColumn
helpviewer_keywords: EventColumn data type
ms.assetid: c0009f1d-d136-4155-9a1b-7baacda4b552
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cb58ea2676265b5dcd5b67819b70020c365ec7ed
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="eventcolumn-data-type-assl"></a>EventColumn 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]에 대해 캡처할 정보 열을 나타내는 기본 데이터 형식을 정의 [이벤트](../../../analysis-services/scripting/objects/event-element-assl.md) 의 일환으로 요소는 [추적](../../../analysis-services/scripting/objects/trace-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[ColumnID](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md)|  
|파생 요소|[열](../../../analysis-services/scripting/objects/column-element-assl.md) ([열](../../../analysis-services/scripting/collections/columns-element-assl.md) 컬렉션 [추적](../../../analysis-services/scripting/objects/trace-element-assl.md))|  
  
## <a name="see-also"></a>관련 항목:  
 [Events 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
