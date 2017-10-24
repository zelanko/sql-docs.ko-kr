---
title: "MeasureGroupDimension 데이터 형식 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MeasureGroupDimension Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MeasureGroupDimension
helpviewer_keywords:
- MeasureGroupDimension data type
ms.assetid: 9d1c1c19-31ce-4c42-b2e6-4c1b08875a83
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6f2d7763bd8d4d5ee42714ac102cc5ebdf37ba71
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="measuregroupdimension-data-type-assl"></a>MeasureGroupDimension 데이터 형식(ASSL)
  차원과 측정값 그룹 간의 관계를 나타내는 추상 기본 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroupDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
      <Annotations>...</Annotations>  
   <Source>...</Source>  
</MeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|[DataMiningMeasureGroupDimension](../../../analysis-services/scripting/data-type/dataminingmeasuregroupdimension-data-type-assl.md), [DegenerateMeasureGroupDimension](../../../analysis-services/scripting/data-type/degeneratemeasuregroupdimension-data-type-assl.md), [ManyToManyMeasureGroupDimension](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md), [ReferenceMeasureGroupDimension](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md), [RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md), [Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
|파생 요소|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md) ([MeasureGroup](../../../analysis-services/scripting/collections/dimensions-element-assl.md) 의 [Dimensions](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)컬렉션)|  
  
## <a name="remarks"></a>주의  
 각 **MeasureGroupDimension** 은 큐브의 차원 중 하나에 대한 참조입니다. 이들은 측정값 그룹에 적용되는 큐브 차원을 정의합니다.  
  
 제공되는 특성 집합에 따라 측정값 그룹의 측정값이 알려지는 세분성(범위)이 결정됩니다. 예를 들어 제품 판매량을 나타내는 측정값은 Sales 측정값 그룹에 포함됩니다. 이러한 측정값에 대한 정보는 주간 또는 일간 세분성이 아닌 월간 세분성으로 기본 데이터 원본에 저장됩니다. 이 경우 시간 차원과 Sales 측정값 그룹 간의 관계를 설명하는 **MeasureGroupDimension** 에 대해 Month 특성만 나열됩니다. 드물게 세분성이 특성 집합으로 정의되는 경우도 있습니다. 예를 들어 Day는 Week 및 Month를 나타내지만 Week는 Month를 나타내지 않는 특성 집합 {Day, Week, Month, Year}의 경우 Forecasts 측정값 그룹에 포함된 측정값은 Month 및 Week에 의해 알려질 수 있지만 Day에 의해 알려질 수는 없습니다.  
  
 특성을 제공하지 않으면 차원의 키 특성만 나열된 것과 같게 됩니다(세분성의 최하위 수준 정의). 측정값 그룹의 각 파티션은 같은 세분성을 가져야 합니다. 나열된 특성 집합은 특성 간의 관계와 관련하여 중복되지 않아야 합니다. 예를 들어 Month가 Year를 나타내는 경우 세분성은 Month 및 Year가 아닌 Month로 정의됩니다.  
  
 **MeasureGroupDimension** 은 특정 정보를 나타내야 하는 경우에만 계층을 포함해야 합니다. 특정 측정값 그룹에 적용할 계층을 선택할 수 있는 방법은 없습니다. 마찬가지로 특정 정보를 나타내야 하는 경우에만 [MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md) 를 포함해야 합니다.  
  
 각 계층은 [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)에 포함된 계층의 하위 집합이어야 합니다. 측정값 그룹의 세분성에 따라 일부 수준이 자동으로 비활성화될 수 있지만 수준을 선택할 수는 없습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.MeasureGroupDimension>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

