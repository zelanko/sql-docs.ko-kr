---
title: FontSize 요소 (ASSL) | Microsoft Docs
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
- FontSize Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- FontSize
helpviewer_keywords:
- FontSize element
ms.assetid: 49f66a73-946a-4fbd-9749-a3ca1b717ff3
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1eaf29caf869de81e397b92f9953d9b673d17019
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081184"
---
# <a name="fontsize-element-assl"></a>FontSize 요소(ASSL)
  글꼴 관련 표시 특성을 설명는 [CalculationProperty](../objects/calculationproperty-element-assl.md) 또는 [측정값](../objects/measure-element-assl.md) 부모 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <FontSize>...</FontSize>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CalculationProperty](../objects/calculationproperty-element-assl.md), [측정값](../objects/measure-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `FontSize` 속성에 적용 하는 MDX (Multidimensional Expressions) 식을 포함 `CalculationProperty` 않은 요소는 [CalculationType](calculationtype-element-assl.md) 의 *멤버* 또는 *셀* .  
  
 부모에 해당 하는 요소 `FontSize` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CalculationProperty> 및 <xref:Microsoft.AnalysisServices.Measure>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CalculationProperties 요소 &#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [MdxScript 요소 &#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [MdxScripts 요소 &#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  