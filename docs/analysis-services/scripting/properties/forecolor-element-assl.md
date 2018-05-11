---
title: ForeColor 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 35ee05a74dc833f3f2785d7933323eeb1ce3042d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="forecolor-element-assl"></a>ForeColor 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  색 관련 표시 특성을 설명는 [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md) 또는 [측정값](../../../analysis-services/scripting/objects/measure-element-assl.md) 부모 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <ForeColor>...</ForeColor>  
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
|부모 요소|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md), [측정값](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **ForeColor** 속성에 적용 하는 MDX (Multidimensional Expressions) 식을 포함 **CalculationProperty** 않은 요소는 [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md) 의 *멤버* 또는 *셀*합니다.  
  
 부모에 해당 하는 요소 **ForeColor** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CalculationProperty> 및 <xref:Microsoft.AnalysisServices.Measure>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CalculationProperties 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [MdxScripts 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
