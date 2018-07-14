---
title: IncrementalProcessingNotification 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IncrementalProcessingNotification Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- IncrementalProcessingNotification data type
ms.assetid: 66e27f92-65c1-4a34-b9c2-bfbb5aeb7d7c
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 38ca951d727e32f576e4dc65bc005a5b423e90c0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231813"
---
# <a name="incrementalprocessingnotification-data-type-assl"></a>IncrementalProcessingNotification 데이터 형식(ASSL)
  에 대 한 정보를 나타내는 파생된 데이터 형식을 정의 합니다 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 증분 처리의 진행률을 확인 하기 위해 실행할 쿼리에 대 한 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<IncrementalProcessingNotification>  
   <!-- The following elements extend QueryNotification -->  
   <TableID>...</TableID>  
   <ProcessingQuery>...</ProcessingQuery>  
</IncrementalProcessingNotification>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[QueryNotification](../objects/querynotification-element-assl.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[ProcessingQuery](../properties/query-element-assl.md), [TableID](../properties/id-element-assl.md)|  
|파생 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ProactiveCachingQueryBinding 데이터 형식 &#40;ASSL&#41;](binding-data-type-assl.md)   
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
