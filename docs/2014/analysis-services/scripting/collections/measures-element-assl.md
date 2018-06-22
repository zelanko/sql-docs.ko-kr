---
title: 요소 (ASSL)를 측정 합니다. | Microsoft Docs
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
- Measures Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Measures
helpviewer_keywords:
- Measures element
ms.assetid: d2107112-f620-4fd7-a05f-bb2606b4be18
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 38b21b53bf8173b709a43393710256b7040648b7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081425"
---
# <a name="measures-element-assl"></a>Measures 요소(ASSL)
  컬렉션을 포함 [측정값](../objects/measure-element-assl.md) 부모 요소와 관련 된 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroup> <!-- or AggregationInstance, MeasureGroupBinding (out-of-line), PerspectiveMeasureGroup -->  
   ...  
   <Measures>  
      <Measure>...</Measure>  
   </Measures>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AggregationInstance](../objects/aggregationinstance-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [MeasureGroupBinding (아웃 아웃오브 라인)](../data-type/measuregroupbinding-data-type-out-of-line-assl.md), [PerspectiveMeasureGroup](../data-type/perspectivemeasuregroup-data-type-assl.md)|  
|자식 요소|[측정값](../objects/measure-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Objects) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.MeasureCollection> 및 <xref:Microsoft.AnalysisServices.PerspectiveMeasureCollection>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  