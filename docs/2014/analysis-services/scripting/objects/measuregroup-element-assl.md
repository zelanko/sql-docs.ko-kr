---
title: MeasureGroup 요소 (ASSL) | Microsoft Docs
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
- MeasureGroup Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroup
helpviewer_keywords:
- MeasureGroup element
ms.assetid: 7aa099db-5dc7-4cac-b437-f73fc0921b24
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee73b594fde5e3a9e915615d1a343296ce846d52
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37163374"
---
# <a name="measuregroup-element-assl"></a>MeasureGroup 요소(ASSL)
  동일한 세분성 수준에서 측정값 집합을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroups>  
   <MeasureGroup> <!-- ancestor: Cube -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</<Create  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <LastProcessed>...</LastProcessed>  
      <Translations>...</Translations>  
      <Type>...</Type>  
      <State>...</State>  
      <MeasureQualification>...</MeasureQualification>  
      <Measures>...</Measures>  
      <DataAggregation>...</DataAggregation>  
      <Source>...</Source>  
            <StorageMode>...</StorageMode>  
      <StorageLocation>...</StorageLocation>  
      <IgnoreUnrelatedDimensions>...</IgnoreUnrelatedDimensions>  
            <ProactiveCaching>...</ProactiveCaching>  
      <EstimatedRows>...</EstimatedRows>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <EstimatedSize>...</EstimatedSize>  
      <ProcessingMode>...</ProcessingMode>  
      <Dimensions>...</Dimensions>  
      <Partitions>...</Partitions>  
      <AggregationPrefix>...</AggregationPrefix>  
      <ProcessingPriority>...</ProcessingPriority>  
            <AggregationDesigns>...</AggregationDesigns>  
      <Annotations>...</Annotations>  
   </MeasureGroup>  
   <!-- or  -->  
   <MeasureGroup xsi:type="MeasureGroupBinding">...</MeasureGroup> <!-- ancestor: CubeBinding -->  
   <!-- or  -->  
   <MeasureGroup xsi:type="PerspectiveMeasureGroup">...</MeasureGroup> <!-- ancestor: Perspective -->  
</MeasureGroups>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
|상위 항목 또는 부모|데이터 형식|  
|------------------------|---------------|  
|[Cube](cube-element-assl.md)|InclusionThresholdSetting|  
|[CubeBinding](../data-type/binding-data-type-assl.md)|  
|[큐브 뷰](../data-type/perspectivemeasuregroup-data-type-assl.md)|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MeasureGroups](../collections/groups-element-assl.md)|  
|자식 요소||  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|--------------------|  
|[큐브](../collections/aggregationdesigns-element-assl.md), [AggregationPrefix](../properties/aggregationprefix-element-assl.md)를 [주석](../collections/annotations-element-assl.md)를 [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)를 [DataAggregation](aggregation-element-assl.md), [ 설명을](../properties/description-element-assl.md), [차원](../collections/dimensions-element-assl.md)를 [ErrorConfiguration](errorconfiguration-element-assl.md)를 [EstimatedRows](../properties/estimatedrows-element-assl.md)를 [EstimatedSize](../properties/estimatedsize-element-assl.md), [ID](../properties/id-element-assl.md), [IgnoreUnrelatedDimensions](../properties/ignoreunrelateddimensions-element-assl.md)를 [LastProcessed](../properties/lastprocessed-element-assl.md)하십시오 [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [ MeasureQualification](../properties/measurequalificaton-element-assl.md), [측정값](../collections/measures-element-assl.md)를 [이름](../properties/name-element-assl.md)를 [파티션](../collections/partitions-element-assl.md)를 [ProactiveCaching](proactivecaching-element-assl.md), [ ProcessingMode](../properties/processingmode-element-assl.md), [ProcessingPriority](../properties/processingpriority-element-assl.md)를 [소스](../properties/source-element-measure-assl.md)를 [상태](../properties/state-element-assl.md)를 [StorageLocation](../properties/storagelocation-element-assl.md), [ StorageMode](../properties/storagemode-element-assl.md)하십시오 [번역](../collections/translations-element-assl.md), [형식](../properties/type-element-measuregroup-assl.md)|  
|[CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md)|InclusionThresholdSetting|  
|[큐브 뷰](perspective-element-assl.md)|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 측정값 그룹의 모든 측정값은 단일 테이블을 기반으로 해야 합니다. 측정값 그룹은 기본 바인딩을 정의할 수 있으며 이는 나중에 각 파티션에서 재정의할 수 있습니다.  
  
 `MeasureGroup` 요소는 일반 큐브와 가상 큐브의 측정값 그룹에 공통된 세부 정보를 정의합니다. 개별 하위 유형은 유형별 세부 정보를 정의합니다.  
  
 `State`의 `MeasureGroup` 속성 값은 다음과 같습니다.  
  
-   *FullyProcessed* : 모든 파티션을 처리하는 경우  
  
-   *PartiallyProcessed* : 하나 이상의 파티션을 처리하는 경우  
  
-   *Unprocessed* : 파티션을 처리하지 않는 경우  
  
 AMO(Analysis Management Objects) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.MeasureGroup> 및 <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
