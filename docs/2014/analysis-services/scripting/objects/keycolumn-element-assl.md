---
title: KeyColumn 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- KeyColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KeyColumn
helpviewer_keywords:
- KeyColumn element
ms.assetid: 7b03eeb3-d478-4c38-822e-8cdfcc485039
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e27744d2c8e2d54d44318ceac7b79dc4e4e10e4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247763"
---
# <a name="keycolumn-element-assl"></a>KeyColumn 요소(ASSL)
  특성의 키 또는 키의 일부인 열의 정의를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<KeyColumns>  
   <KeyColumn xsi:type="DataItem">...</KeyColumn>  
<KeyColumns>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[KeyColumns](../collections/columns-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 자세한 내용은 합니다 `DataItem` 형식, Analysis Services Scripting Language (ASSL) 개체의 속성을 테이블을 포함 하는 `DataItem` 입력을 참조 하십시오 [DataItem 데이터 형식 &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 AMO(Analysis Management Object) 개체 모델에서 `KeyColumns` 컬렉션의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, <xref:Microsoft.AnalysisServices.MeasureGroupAttribute> 및 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [AggregationInstanceAttribute 데이터 형식 &#40;ASSL&#41;](../data-type/aggregationinstanceattribute-data-type-assl.md)   
 [AggregationInstanceCubeDimension 데이터 형식 &#40;ASSL&#41;](../data-type/dimension-data-type-assl.md)   
 [DimensionAttribute 데이터 형식 &#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [Measuregroupattribute _ 데이터 형식 &#40;ASSL&#41;](../data-type/measuregroupattribute-data-type-assl.md)   
 [ScalarMiningStructureColumn 데이터 형식 &#40;ASSL&#41;](../data-type/miningstructurecolumn-data-type-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
