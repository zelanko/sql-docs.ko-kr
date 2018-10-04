---
title: ForeColor 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ForeColor Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ForeColor
helpviewer_keywords:
- ForeColor element
ms.assetid: 5125520c-3bce-40e6-a722-8d4d47306fed
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 53436deea642942f7110b542d07312ba78256989
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216533"
---
# <a name="forecolor-element-assl"></a>ForeColor 요소(ASSL)
  색 관련 표시 특징을 설명 합니다 [CalculationProperty](../objects/calculationproperty-element-assl.md) 하거나 [측정값](../objects/measure-element-assl.md) 부모 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <ForeColor>...</ForeColor>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CalculationProperty](../objects/calculationproperty-element-assl.md), [측정값](../objects/measure-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 합니다 `ForeColor` 속성이 MDX (Multidimensional Expressions) 식을 포함 하 고 적용할 `CalculationProperty` 요소를 [CalculationType](calculationtype-element-assl.md) 의 *멤버* 또는 *셀* .  
  
 부모에 해당 하는 요소가 `ForeColor` Analysis Management Objects (AMO) 개체 모델 <xref:Microsoft.AnalysisServices.CalculationProperty> 및 <xref:Microsoft.AnalysisServices.Measure>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CalculationProperties 요소 &#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [MdxScript 요소 &#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [MdxScripts 요소 &#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
