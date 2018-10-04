---
title: CubeDimensionID 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubeDimensionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeDimensionID
helpviewer_keywords:
- CubeDimensionID element
ms.assetid: d1341fb2-9afe-40f1-a704-ce548bce48fc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e50506439d5820bee62015805a19323a20134e55
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076273"
---
# <a name="cubedimensionid-element-assl"></a>CubeDimensionID 요소(ASSL)
  식별 된 [CubeDimension](../data-type/dimension-data-type-assl.md) 부모 요소와 연결 된 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AggregationDesignDimension> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <CubeDimensionID>...</CubeDimensionID>  
   ...  
</AggregationDesignDimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AggregationDesignDimension](../data-type/aggregationdesigndimension-data-type-assl.md), [AggregationDimension](../data-type/aggregationdimension-data-type-assl.md)를 [AggregationInstanceCubeDimension](../data-type/aggregationinstancecubedimension-data-type-assl.md)하십시오 [CubeAttributeBinding](../data-type/binding-data-type-assl.md), [ CubeDimensionBinding](../data-type/dimensionbinding-data-type-assl.md), [CubeDimensionPermission](../data-type/permission-data-type-assl.md), [MeasureGroupDimension](../data-type/measuregroupdimension-data-type-assl.md)하십시오 [MeasureGroupDimensionBinding](../data-type/measuregroupdimensionbinding-data-type-assl.md)를 [ PerspectiveDimension](../data-type/perspectivedimension-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Object)에서 `CubeDimensionID`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.AggregationDesignDimension>, <xref:Microsoft.AnalysisServices.AggregationDimension>, <xref:Microsoft.AnalysisServices.CubeAttributeBinding>, <xref:Microsoft.AnalysisServices.CubeDimensionBinding>, <xref:Microsoft.AnalysisServices.CubeDimensionPermission>, <xref:Microsoft.AnalysisServices.MeasureGroupDimension>, <xref:Microsoft.AnalysisServices.MeasureGroupDimensionBinding> 및 <xref:Microsoft.AnalysisServices.PerspectiveDimension>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
