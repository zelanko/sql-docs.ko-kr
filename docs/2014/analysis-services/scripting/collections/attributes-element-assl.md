---
title: 특성을 요소 (ASSL) | Microsoft Docs
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
- Attributes Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Attributes
helpviewer_keywords:
- Attributes element
ms.assetid: d6b545e6-1521-496f-a731-f2c2c44118e4
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2e3dda6122030b789f9cccbf9f300a0a41a37ec5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183116"
---
# <a name="attributes-element-assl"></a>Attributes 요소(ASSL)
  연결된 차원에 대한 특성의 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AggregationDesignDimension> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Attributes>  
      <Attribute>...</Attribute>  
  </Attributes>  
   ...  
</AggregationDesignDimension>  
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
|부모 요소|[AggregationDesignDimension](../data-type/dimension-data-type-assl.md), [AggregationDimension](../data-type/aggregationdimension-data-type-assl.md), [AggregationInstanceCubeDimension](../data-type/cubedimension-data-type-assl.md), [CubeDimension](../data-type/cubedimension-data-type-assl.md), [차원 ](../objects/dimension-element-assl.md), [PerspectiveDimension](../data-type/perspectivedimension-data-type-assl.md), [RegularMeasureGroupDimension](../data-type/measuregroupdimension-data-type-assl.md), [RelationshipEnd](../data-type/relationshipend-data-type-assl.md)|  
|자식 요소|[Attribute](../objects/attribute-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Objects) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.AggregationAttributeCollection>, <xref:Microsoft.AnalysisServices.AggregationDesignAttributeCollection>, <xref:Microsoft.AnalysisServices.AggregationInstanceAttributeCollection>, <xref:Microsoft.AnalysisServices.CubeAttributeCollection>, <xref:Microsoft.AnalysisServices.DimensionAttributeCollection>, <xref:Microsoft.AnalysisServices.MeasureGroupAttributeCollection> 및 <xref:Microsoft.AnalysisServices.PerspectiveAttributeCollection>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  