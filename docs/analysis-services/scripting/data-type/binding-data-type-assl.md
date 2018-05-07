---
title: Binding 데이터 형식 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9bcfe09f338a711ec918735c877ae064d4c80538
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="binding-data-type-assl"></a>Binding 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  한 개체의 데이터 또는 메타데이터가 바인딩된 개체의 데이터 또는 메타데이터에 종속되는 두 개체 간의 종속 관계를 나타내는 추상 기본 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Binding>...</Binding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md), [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md), [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md), [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md), [ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md), [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md), [TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md), [TimeAttributeBinding](../../../analysis-services/scripting/data-type/timeattributebinding-data-type-assl.md), [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md), [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|없음|  
|파생 요소|없음|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Binding>합니다.  
  
 데이터 바인딩에 대 한 자세한 내용은 참조 [데이터 원본 및 바인딩 & #40; SSAS 다차원 & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="elements-of-type-binding"></a>Binding 유형의 요소  
 다음 표에서는 **Binding**유형의 요소를 나열합니다.  
  
|부모 요소|**Binding**유형의 요소|설명|  
|--------------------|---------------------------------|--------------|  
|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|[CaptionColumn](../../../analysis-services/scripting/properties/source-element-binding-assl.md) ( [DataItem](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md) 유형)의 [Source](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|입력은 **바인딩** 해야 [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) 또는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[원본](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|입력은 **바인딩** 해야 [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)|  
|[CubeBinding (아웃 아웃오브 라인)](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|[측정값 그룹](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|입력은 **바인딩** 해야 [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|[원본](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|**Binding** 은 모든 유형일 수 있습니다.|  
|[차원](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[원본](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|입력은 **바인딩** 해야 [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md), [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), 또는 [ TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[원본](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|입력은 **바인딩** 해야 [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) 또는 [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)|[열](../../../analysis-services/scripting/objects/column-element-assl.md)|입력은 **바인딩** 해야 [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md) 또는 [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[측정값](../../../analysis-services/scripting/objects/measure-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md) ( [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)유형)|입력은 **바인딩** 해야 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md), 또는 [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)|  
|[측정값 그룹](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[원본](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|입력은 **바인딩** 해야 [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/properties/source-element-binding-assl.md) ( [DataItem](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) 유형)의 [Source](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|입력은 **바인딩** 해야 [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) 또는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), 또는 [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|  
|[MeasureGroupBinding (아웃 아웃오브 라인)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[차원](../../../analysis-services/scripting/objects/dimension-element-assl.md)|입력은 **바인딩** 해야 [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (아웃 아웃오브 라인)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[측정값](../../../analysis-services/scripting/objects/measure-element-assl.md)|입력은 **바인딩** 해야 [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[MeasureGroupBinding (아웃 아웃오브 라인)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[파티션](../../../analysis-services/scripting/objects/partition-element-assl.md)|입력은 **바인딩** 해야 [PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (아웃 아웃오브 라인)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[원본](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|입력은 **바인딩** 해야 [TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)|  
|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|[원본](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|입력은 **바인딩** 해야 [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|[원본](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|입력은 **바인딩** 해야 [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md), 또는 [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|  
|[파티션](../../../analysis-services/scripting/objects/partition-element-assl.md)|[원본](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|입력은 **바인딩** 해야 [TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|[원본](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|입력은 **바인딩** 해야 [ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[원본](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|입력은 **바인딩** 해야 [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), [CubeAttributeBinding 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md), 또는 [MeasureBinding 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|[SourceMeasureGroup](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)|입력은 **바인딩** 해야 [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 & #40; analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
