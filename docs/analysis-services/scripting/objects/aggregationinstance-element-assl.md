---
title: AggregationInstance 요소 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c8f24bbaf0660c690697dad015fa28c412a633a3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="aggregationinstance-element-assl"></a>AggregationInstance 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  파티션에 대한 집계 인스턴스를 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AggregationInstances>  
   <AggregationInstance>  
      <AggregationType>...</AggregationType>  
      <AggregationID>...</AggregationID>  
      <Source>...</Source>  
      <Dimensions>...</Dimensions>  
      <Measures>...</Measures>  
      <Annotations>...</Annotations>  
   </AggregationInstance>  
</AggregationInstances>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AggregationInstances](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md)|  
|자식 요소|[AggregationID](../../../analysis-services/scripting/properties/aggregationid-element-assl.md), [AggregationType](../../../analysis-services/scripting/properties/aggregationtype-element-assl.md), [주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [차원](../../../analysis-services/scripting/collections/dimensions-element-assl.md), [측정값](../../../analysis-services/scripting/collections/measures-element-assl.md), [소스](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
  
## <a name="remarks"></a>주의  
 경우는 [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md) 요소 사용 하 여는 [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md) 해당 파티션에 대 한 집계를 생성 하는 요소가 각 [집계](../../../analysis-services/scripting/objects/aggregation-element-assl.md) 에  **AggregationDesign** 해당 파티션에 대해 인스턴스화됩니다. 여러 파티션에서 하나의 집계 디자인을 사용하여 정의된 집계에 대한 여러 개의 인스턴스를 생성할 수 있습니다. **AggregationInstance** 요소는 정의 된 집계의 인스턴스를 나타냅니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.AggregationInstance>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
