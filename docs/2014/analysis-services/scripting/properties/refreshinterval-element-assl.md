---
title: RefreshInterval 요소 (ASSL) | Microsoft Docs
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
- RefreshInterval Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RefreshInterval
helpviewer_keywords:
- RefreshInterval element
ms.assetid: 2761d26a-5fb0-452c-9a89-12f8dc658c33
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f3fecbe3eef6eb68af256dfcc0a94ddef1ba3aee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315053"
---
# <a name="refreshinterval-element-assl"></a>RefreshInterval 요소(ASSL)
  부모 요소와 연결된 바인딩된 데이터를 새로 고치는 간격을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding, ProactiveCachingIncrementalProcessingBinding, ProactiveCachingQueryBinding -->  
   ...  
   <RefreshInterval>...</RefreshInterval>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|XML 기간|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
|기본값|[ProactiveCachingIncrementalProcessingBinding](../data-type/binding-data-type-assl.md) 나 [ProactiveCachingQueryBinding](../data-type/querybinding-data-type-assl.md) PT-1 =|  
|기본값|나머지 = PT1m|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionBinding](../data-type/dimensionbinding-data-type-assl.md)하십시오 [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)하십시오 [ProactiveCachingIncrementalProcessingBinding](../data-type/binding-data-type-assl.md), [ProactiveCachingQueryBinding](../data-type/querybinding-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Objects) 개체 모델에서 `RefreshInterval`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.DimensionBinding>, <xref:Microsoft.AnalysisServices.MeasureGroupBinding>, <xref:Microsoft.AnalysisServices.ProactiveCachingIncrementalProcessingBinding> 및 <xref:Microsoft.AnalysisServices.ProactiveCachingQueryBinding>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
