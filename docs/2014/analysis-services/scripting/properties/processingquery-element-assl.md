---
title: ProcessingQuery 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ProcessingQuery Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProcessingQuery element
ms.assetid: d18e6f4b-c24c-4f73-8b85-4b6e8a82a695
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a4ade6950de95029d3eea4105bd34f636fd3632a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090253"
---
# <a name="processingquery-element-assl"></a>ProcessingQuery 요소(ASSL)
  증분 처리 상태 알림을 위해 실행할 쿼리의 매개 변수가 있는 텍스트를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<IncrementalProcessingNotification>  
   ...  
   <ProcessingQuery>...</ProcessingQuery>  
   ...  
</IncrementalProcessingNotification>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 테이블에는 [DataSourceView](../objects/datasourceview-element-assl.md) 에서 참조 하는 `ProcessingQuery` 형제 요소로 식별 됩니다 [TableID](id-element-assl.md)합니다.  
  
 부모에 해당 하는 요소 `ProcessingQuery` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  