---
title: "IncrementalProcessingNotification 데이터 형식 (ASSL) | Microsoft Docs"
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
apiname: IncrementalProcessingNotification Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: IncrementalProcessingNotification data type
ms.assetid: 66e27f92-65c1-4a34-b9c2-bfbb5aeb7d7c
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: abc8dbeac5515a73ac6f0ec7549c7251362b904c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="incrementalprocessingnotification-data-type-assl"></a>IncrementalProcessingNotification 데이터 형식(ASSL)
  에 대 한 정보를 나타내는 파생된 데이터 형식을 정의 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 증분 처리의 진행률을 확인 하기 위해 실행할 쿼리에 대 한 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<IncrementalProcessingNotification>  
   <!-- The following elements extend QueryNotification -->  
   <TableID>...</TableID>  
   <ProcessingQuery>...</ProcessingQuery>  
</IncrementalProcessingNotification>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|[QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[ProcessingQuery](../../../analysis-services/scripting/properties/processingquery-element-assl.md), [TableID](../../../analysis-services/scripting/properties/tableid-element-assl.md)|  
|파생 요소|없음|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ProactiveCachingQueryBinding 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)   
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
