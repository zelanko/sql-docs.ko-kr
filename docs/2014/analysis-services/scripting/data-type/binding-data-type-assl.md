---
title: Binding 데이터 형식 (ASSL) | Microsoft Docs
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
- Binding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- BINDING
helpviewer_keywords:
- Binding data type
ms.assetid: 0a777219-b885-4961-ac66-b76faeb520db
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a34209ea08d1cdfd0100bd5e2402edc0f592f066
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169544"
---
# <a name="binding-data-type-assl"></a>Binding 데이터 형식(ASSL)
  한 개체의 데이터 또는 메타데이터가 바인딩된 개체의 데이터 또는 메타데이터에 종속되는 두 개체 간의 종속 관계를 나타내는 추상 기본 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Binding>...</Binding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|[AttributeBinding](binding-data-type-assl.md), [ColumnBinding](columnbinding-data-type-assl.md)를 [CubeAttributeBinding](cubeattributebinding-data-type-assl.md)하십시오 [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md), [DimensionBinding](dimensionbinding-data-type-assl.md), [InheritedBinding](inheritedbinding-data-type-assl.md)를 [MeasureBinding](measurebinding-data-type-assl.md)를 [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)합니다 [ MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md), [ProactiveCachingBinding](proactivecachingbinding-data-type-assl.md)를 [RowBinding](rowbinding-data-type-assl.md)하십시오 [TabularBinding](tabularbinding-data-type-assl.md), [ TimeAttributeBinding](timeattributebinding-data-type-assl.md)하십시오 [TimeBinding](timebinding-data-type-assl.md), [UserDefinedGroupBinding](userdefinedgroupbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|InclusionThresholdSetting|  
|파생 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Binding>합니다.  
  
 데이터 바인딩에 대 한 자세한 내용은 참조 하세요. [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
## <a name="elements-of-type-binding"></a>Binding 유형의 요소  
 다음 표에서는 `Binding` 형식의 요소를 나열합니다.  
  
|부모 요소|`Binding` 형식의 요소|주석|  
|--------------------|---------------------------------|--------------|  
|[AttributeTranslation](../properties/source-element-binding-assl.md) 의 [CaptionColumn](../objects/column-element-assl.md) (형식의 [DataItem](dataitem-data-type-assl.md))|형식의 합니다 `Binding` 있어야 [AttributeBinding](binding-data-type-assl.md) 또는 [ColumnBinding](columnbinding-data-type-assl.md)|  
|[Cube](../objects/cube-element-assl.md)|[원본](../properties/source-element-binding-assl.md)|형식의 합니다 `Binding` 있어야 [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md)|  
|[CubeBinding (아웃 아웃오브 라인)](../objects/group-element-assl.md)|형식의 합니다 `Binding` 있어야 [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
|[DataItem](dataitem-data-type-assl.md)|[원본](../properties/source-element-binding-assl.md)|`Binding`은 모든 유형일 수 있습니다.|  
|[Dimension](../objects/dimension-element-assl.md)|[원본](../properties/source-element-binding-assl.md)|형식의 합니다 `Binding` 이어야 합니다 [CubeDimensionBinding](dimensionbinding-data-type-assl.md)를 [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md)를 [DimensionBinding](dimensionbinding-data-type-assl.md), 또는 [TimeBinding](timebinding-data-type-assl.md)|  
|[DimensionAttribute](dimensionattribute-data-type-assl.md)|[원본](../properties/source-element-binding-assl.md)|형식의 합니다 `Binding` 있어야 [AttributeBinding](binding-data-type-assl.md) 또는 [UserDefinedGroupBinding](userdefinedgroupbinding-data-type-assl.md)|  
|[DrillThroughAction](action-data-type-assl.md)|[열](../objects/column-element-assl.md)|형식의 합니다 `Binding` 있어야 [CubeAttributeBinding](cubeattributebinding-data-type-assl.md) 또는 [MeasureBinding](measurebinding-data-type-assl.md)|  
|[측정값](../objects/measure-element-assl.md)|[소스](../properties/source-element-binding-assl.md) (형식의 [DataItem](dataitem-data-type-assl.md))|형식의 합니다 `Binding` 이어야 합니다 [ColumnBinding](columnbinding-data-type-assl.md)를 [CubeDimensionBinding](dimensionbinding-data-type-assl.md)를 [MeasureBinding](measurebinding-data-type-assl.md), 또는 [RowBinding](rowbinding-data-type-assl.md)|  
|[측정값 그룹](../objects/measuregroup-element-assl.md)|[원본](../properties/source-element-binding-assl.md)|형식의 합니다 `Binding` 있어야 [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)|[소스](../properties/source-element-binding-assl.md) 의 [KeyColumn](../objects/keycolumn-element-assl.md) (형식의 [DataItem](dataitem-data-type-assl.md))|형식의 합니다 `Binding` 있어야 [AttributeBinding](binding-data-type-assl.md) 또는 [ColumnBinding](columnbinding-data-type-assl.md), 또는 [InheritedBinding](inheritedbinding-data-type-assl.md)|  
|[MeasureGroupBinding (아웃 아웃오브 라인)](measuregroupbinding-data-type-out-of-line-assl.md)|[Dimension](../objects/dimension-element-assl.md)|형식의 합니다 `Binding` 있어야 [MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (아웃 아웃오브 라인)](measuregroupbinding-data-type-out-of-line-assl.md)|[측정값](../objects/measure-element-assl.md)|형식의 합니다 `Binding` 있어야 [MeasureBinding](measurebinding-data-type-assl.md)|  
|[MeasureGroupBinding (아웃 아웃오브 라인)](../objects/partition-element-assl.md)|형식의 합니다 `Binding` 있어야 [PartitionBinding](partitionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (아웃 아웃오브 라인)](measuregroupbinding-data-type-out-of-line-assl.md)|[원본](../properties/source-element-binding-assl.md)|형식의 합니다 `Binding` 있어야 [TableBinding](tablebinding-data-type-assl.md)|  
|[MeasureGroupDimension](dimension-data-type-assl.md)|[원본](../properties/source-element-binding-assl.md)|형식의 합니다 `Binding` 있어야 [MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md)|[원본](../properties/source-element-binding-assl.md)|형식의 합니다 `Binding` 있어야 [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md), 또는 [DimensionBinding](dimensionbinding-data-type-assl.md)|  
|[파티션](../objects/partition-element-assl.md)|[원본](../properties/source-element-binding-assl.md)|형식의 합니다 `Binding` 있어야 [TabularBinding](tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|[원본](../properties/source-element-binding-assl.md)|형식의 합니다 `Binding` 있어야 [ProactiveCachingBinding](proactivecachingbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[원본](../properties/source-element-binding-assl.md)|형식의 합니다 `Binding` 있어야 [AttributeBinding](binding-data-type-assl.md), [CubeAttributeBinding 데이터 형식 &#40;ASSL&#41;](cubeattributebinding-data-type-assl.md), 또는 [MeasureBinding 데이터 형식 &#40;ASSL&#41;](measurebinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../objects/sourcemeasuregroup-element-assl.md)|형식의 합니다 `Binding` 있어야 [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
