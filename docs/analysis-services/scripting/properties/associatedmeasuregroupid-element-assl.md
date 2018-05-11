---
title: AssociatedMeasureGroupID 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2a0f733799edd1eb8357d5893e89a146d6987608
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="associatedmeasuregroupid-element-assl"></a>AssociatedMeasureGroupID 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  ID를 포함 된 [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) 요소와 연관 된는 [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md) 요소 또는 [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CalculationProperty> <!-- or Kpi -->  
   ...  
   <AssociatedMeasureGroupID>...</AssociatedMeasureGroupID>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 에 적용 될 때 **CalculationProperty** 요소는 **AssociatedMeasureGroupID** 속성이 있는 요소에 적용 됩니다. 한 [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md) 의 *멤버* .  
  
 부모에 해당 하는 요소 **AssociatedMeasureGroupID** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CalculationProperty> 및 <xref:Microsoft.AnalysisServices.Kpi>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CalculationProperties 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [MdxScripts 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
