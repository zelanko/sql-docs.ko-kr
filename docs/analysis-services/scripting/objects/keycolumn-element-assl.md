---
title: KeyColumn 요소 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e22b3b5872ce75f7b93ce334df2d4214df176eb0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="keycolumn-element-assl"></a>KeyColumn 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  특성의 키 또는 키의 일부인 열의 정의를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<KeyColumns>  
   <KeyColumn xsi:type="DataItem">...</KeyColumn>  
<KeyColumns>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|기본값|없음|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 에 대 한 자세한 내용은 **DataItem** 테이블의 Analysis Services Scripting Language (ASSL) 개체 및 속성을 포함 하 여는 **DataItem** 입력을 참조 하십시오. [DataItem 데이터 형식 & #40; ASSL & #41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 부모에 해당 하는 요소는 **KeyColumns** Analysis Management Objects (AMO) 개체 모델에서 컬렉션은 <xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>, 및 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [AggregationInstanceAttribute 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/aggregationinstanceattribute-data-type-assl.md)   
 [AggregationInstanceCubeDimension 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md)   
 [DimensionAttribute 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [Measuregroupattribute _ 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)   
 [ScalarMiningStructureColumn 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)   
 [개체 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
