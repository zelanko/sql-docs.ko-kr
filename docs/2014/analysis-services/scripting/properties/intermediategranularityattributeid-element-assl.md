---
title: IntermediateGranularityAttributeID 요소 (ASSL) | Microsoft Docs
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
- IntermediateGranularityAttributeID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- IntermediateGranularityAttributeID
helpviewer_keywords:
- IntermediateGranularityAttributeID element
ms.assetid: 49895ff0-cb0d-4bcc-ab73-8cb3d5961e12
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 680104347b19e1a7b541ab2eae84f9a6587d1d73
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172979"
---
# <a name="intermediategranularityattributeid-element-assl"></a>IntermediateGranularityAttributeID 요소(ASSL)
  참조 차원을 중간 차원에 연결하는 데 사용되는 중간 큐브 차원의 세분성 특성 ID를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ReferenceMeasureGroupDimension>  
   ...  
   <IntermediateGranularityAttributeID>...  
   </IntermediateGranularityAttributeID>  
   ...  
</ReferenceMeasureGroupDimension>  
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
|부모 요소|[ReferenceMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소 `IntermediateGranularityAttributeID` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  