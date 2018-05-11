---
title: CalculationReference 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ec338d5a8c1906255eae1b87283914543fccf0f7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="calculationreference-element-assl"></a>CalculationReference 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  명명 된 집합 또는 계산된 셀에서 참조의 이름이 고 [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CalculationProperty>  
   ...  
   <CalculationReference>...</CalculationReference>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 하는 경우의 값은 **CalculationReference** 가 일치 하는 이름을 기존의 명명 된 집합 또는 계산 셀 정의 **CalculationReference** 는 무시 됩니다.  
  
 부모에 해당 하는 요소 **CalculationReference** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CalculationProperty>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CalculationProperties 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [MdxScripts 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
