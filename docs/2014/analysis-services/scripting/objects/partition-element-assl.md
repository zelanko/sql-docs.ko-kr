---
title: 요소 (ASSL) 파티션 | Microsoft Docs
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
- Partition Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PARTITION
helpviewer_keywords:
- Partition element
ms.assetid: 40020840-1bb7-478f-9017-1a30342ac4c6
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c298ec80f1bb1f17d97e36f2ce93b6efbf924508
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209973"
---
# <a name="partition-element-assl"></a>Partition 요소(ASSL)
  정의 된 [MeasureGroup](group-element-assl.md) 요소나는 아웃 아웃오브 라인 파티션 바인딩을 [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Partitions>  
      <Partition> <!-- ancestor: MeasureGroup -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Source>...</Source>  
      <ProcessingPriority>...</ProcessingPriority>  
      <AggregationPrefix>...</AggregationPrefix>  
      <StorageMode>...</StorageMode>  
      <ProcessingMode>...</ProcessingMode>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <StorageLocation>...</StorageLocation>  
      <RemoteDatasourceID>...</RemoteDatasourceID>  
      <Slice>...</Slice>  
      <ProactiveCaching>...</ProactiveCaching>  
      <Type>...</Type>  
      <EstimatedSize>...</EstimatedSize>  
      <EstimatedRows>...</EstimatedRows>  
      <CurrentStorageMode>...</CurrentStorageMode>  
      <AggregationDesignID>...</AggregationDesignID>  
      <AggregationInstances>...</AggregationInstances>  
      <AggregationInstanceSource>...</AggregationInstanceSource>  
      <LastProcessed>...</LastProcessed>  
      <State>...</State>  
      <Annotations>.../Annotations>  
   </Partition>  
   <!-- or -->  
   <Partition xsi:type="PartitionBinding"> <!-- ancestor: MeasureGroupBinding -->  
   </Partition>  
</Partitions>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
|상위 항목 또는 부모|데이터 형식|  
|------------------------|---------------|  
|[측정값 그룹](group-element-assl.md)|InclusionThresholdSetting|  
|[MeasureGroupBinding](../data-type/binding-data-type-assl.md)|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[파티션](../collections/partitions-element-assl.md)|  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|--------------------|  
|[MeasureGroup](../properties/id-element-assl.md), [AggregationInstances](../collections/aggregationinstances-element-assl.md)합니다 [AggregationInstanceSource](../properties/aggregationinstancesource-element-assl.md)를 [AggregationPrefix](../properties/aggregationprefix-element-assl.md), [주석](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)합니다 [CurrentStorageMode](../properties/storagemode-element-assl.md), [설명을](../properties/description-element-assl.md), [ErrorConfiguration](errorconfiguration-element-assl.md), [EstimatedRows](../properties/estimatedrows-element-assl.md), [EstimatedSize](../properties/estimatedsize-element-assl.md)를 [ID](../properties/id-element-assl.md)합니다 [LastProcessed](../properties/lastprocessed-element-assl.md)를 [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [이름](../properties/name-element-assl.md), [ProactiveCaching](proactivecaching-element-assl.md), [ProcessingMode](../properties/processingmode-element-assl.md)하십시오 [ProcessingPriority](../properties/processingpriority-element-assl.md), [ RemoteDatasourceID](../properties/datasourceid-element-assl.md), [조각을](../properties/slice-element-assl.md), [소스](../properties/source-element-binding-assl.md)를 [상태](../properties/state-element-assl.md)를 [StorageLocation](../properties/storagelocation-element-assl.md), [ StorageMode](../properties/storagemode-element-assl.md), [형식](../properties/type-element-partition-assl.md)|  
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소는 DeploymentMode 값 2(테이블 형식 서버 모드)에서 다음과 같은 조건을 충족해야 합니다.  
  
-   다음 자식 요소는 지원되지 않으며 사용할 수 없습니다.  
  
    -   [ProcessingPriority](../properties/processingpriority-element-assl.md)  
  
    -   [AggregationPrefix](../properties/aggregationprefix-element-assl.md)  
  
    -   [StorageLocation](../properties/storagelocation-element-assl.md)  
  
    -   [ProcessingMode](../properties/processingmode-element-assl.md)  
  
    -   [ErrorConfiguration](errorconfiguration-element-assl.md)  
  
    -   [StorageLocation](../properties/storagelocation-element-assl.md)  
  
    -   [RemoteDatasourceID](../properties/datasourceid-element-assl.md)  
  
    -   [조각](../properties/slice-element-assl.md)  
  
    -   [ProactiveCaching](proactivecaching-element-assl.md)  
  
    -   [형식](../properties/type-element-partition-assl.md)  
  
    -   [CurrentStorageMode](../properties/storagemode-element-assl.md)  
  
    -   [AggregationDesignID](../properties/aggregationdesignid-element-assl.md)  
  
    -   [AggregationInstances](../collections/aggregationinstances-element-assl.md)  
  
    -   [AggregationInstanceSource](../properties/aggregationinstancesource-element-assl.md)  
  
     위의 요소를 사용할 경우 오류가 발생할 수 있습니다.  
  
-   합니다 [소스](../properties/source-element-binding-assl.md) 요소는만 수락 **쿼리** 바인딩.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Partition>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
