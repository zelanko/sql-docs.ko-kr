---
title: Source 요소 (바인딩) (ASSL) | Microsoft Docs
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
- Source Element (Binding)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 1032558c-7546-4ca7-888d-8139df23cb62
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 54257415a19530a82b27e759dea03a4e41dcb0cd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257245"
---
# <a name="source-element-binding-assl"></a>Source 요소(바인딩)(ASSL)
  부모 요소가 바인딩된 데이터의 원본을 식별합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AggregationInstance> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Source>...</Source>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|참조 데이터 형식 표에서|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
 **데이터 형식 및 길이**  
  
|||  
|-|-|  
|상위 항목 또는 부모|데이터 형식|  
|[AggregationInstance](../data-type/binding-data-type-assl.md)|  
|[AggregationInstanceMeasure](../data-type/columnbinding-data-type-assl.md)|  
|[Cube](../data-type/datasourceviewbinding-data-type-assl.md)|  
|[DataItem](../data-type/dataitem-data-type-assl.md)|파생 된 모든 데이터 형식 [바인딩](../data-type/binding-data-type-assl.md)의 부모에 따라 `DataItem`합니다. 자세한 내용은 설명 부분을 참조하세요.|  
|[차원](../data-type/dimensionbinding-data-type-assl.md)하십시오 [DataSourceViewBinding](../data-type/datasourceviewbinding-data-type-assl.md)를 [DimensionBinding](../data-type/dimensionbinding-data-type-assl.md), [TimeBinding](../data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../data-type/attributebinding-data-type-assl.md), [UserDefinedGroupBinding](../data-type/userdefinedgroupbinding-data-type-assl.md)|  
|[측정값 그룹](../data-type/measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupDimension](../data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md)|[CubeDimensionBinding](../data-type/cubedimensionbinding-data-type-assl.md)하십시오 [DataSourceViewBinding](../data-type/datasourceviewbinding-data-type-assl.md), [DimensionBinding](../data-type/dimensionbinding-data-type-assl.md)|  
|[파티션](../data-type/tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|파생 된 모든 데이터 형식 [ProactiveCachingBinding](../data-type/proactivecachingbinding-data-type-assl.md)의 부모에 의해 사용 된 처리 및 알림 옵션에 따라는 `ProactiveCaching` 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AggregationInstance](../objects/aggregationinstance-element-assl.md), [AggregationInstanceMeasure](../data-type/aggregationinstancemeasure-data-type-assl.md), [큐브](../objects/cube-element-assl.md)를 [DataItem](../data-type/dataitem-data-type-assl.md), [차원](../objects/dimension-element-assl.md)합니다 [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [MeasureGroup](../objects/group-element-assl.md)하십시오 [MeasureGroupDimension](../data-type/dimension-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [파티션 ](../objects/partition-element-assl.md)하십시오 [ProactiveCaching](../objects/proactivecaching-element-assl.md)합니다.|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Source` 요소의 경우 `Binding` 요소에서 허용되는 파생된 `DataItem` 데이터 형식은 `DataItem` 요소의 부모에 따라 달라집니다.  
  
|DataItem 부모|허용되는 데이터 형식|  
|---------------------|------------------------|  
|[DimensionAttribute](../data-type/attributebinding-data-type-assl.md)하십시오 [ColumnBinding](../data-type/columnbinding-data-type-assl.md), [TimeAttributeBinding](../data-type/timeattributebinding-data-type-assl.md) (동안만 [KeyColumns](../collections/columns-element-assl.md)).|  
|[MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)|[AttributeBinding](../data-type/attributebinding-data-type-assl.md)하십시오 [ColumnBinding](../data-type/columnbinding-data-type-assl.md)하십시오 [InheritedBinding](../data-type/inheritedbinding-data-type-assl.md)합니다.|  
|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|[ColumnBinding](../data-type/columnbinding-data-type-assl.md)|  
  
 에 대 한 자세한 내용은 합니다 `Binding` 형식, Analysis Services Scripting Language (ASSL) 개체 테이블을 비롯 한는 `Binding` 형식과 상속 계층 `Binding` 참조 하십시오 [바인딩 데이터 형식 &#40;ASSL &#41;](../data-type/binding-data-type-assl.md).  
  
 ASSL의 데이터 바인딩에 대 한 자세한 내용은 참조 하세요. [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
