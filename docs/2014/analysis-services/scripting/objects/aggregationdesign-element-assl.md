---
title: AggregationDesign 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationDesign Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationDesign
helpviewer_keywords:
- AggregationDesign element
ms.assetid: 80ad98d8-73a8-4353-b5ad-d2a9ac3bc531
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 430035dd83cf137cb80a5db5d159da027014e6c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075293"
---
# <a name="aggregationdesign-element-assl"></a>AggregationDesign 요소(ASSL)
  데이터베이스의 여러 파티션에서 공유할 수 있는 집계 정의의 집합을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AggregationDesigns>  
   <AggregationDesign>  
      <ID>...</ID>  
      <Name>...</Name>  
            <Description>...</Description>  
      <EstimatedRows>...</EstimatedRows>  
      <Dimensions>...</Dimensions>  
            <Aggregations>...</Aggregation>  
      <EstimatedPerformanceGain>...</EstimatedPerformanceGain>  
      <Annotations>...</Annotations>  
   </AggregationDesign>  
</AggregationDesigns>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AggregationDesigns](../collections/aggregationdesigns-element-assl.md)|  
|자식 요소|[집계](../collections/aggregations-element-assl.md), [주석을](../collections/annotations-element-assl.md)를 [설명](../properties/description-element-assl.md)를 [차원](../collections/dimensions-element-assl.md)를 [EstimatedPerformanceGain](../properties/estimatedperformancegain-element-assl.md)를 [EstimatedRows](../properties/estimatedrows-element-assl.md)하십시오 [ID](../properties/id-element-assl.md), [이름](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.AggregationDesign>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 파티션 &#40;ASSL&#41;](partition-element-assl.md)   
 [Aggregation 요소 &#40;ASSL&#41;](aggregation-element-assl.md)   
 [Aggregations 요소 &#40;ASSL&#41;](../collections/aggregations-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
