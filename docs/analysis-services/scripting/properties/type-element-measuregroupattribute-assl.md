---
title: 요소 (MeasureGroupAttribute) (ASSL)를 입력 합니다. | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 70d5cc25e8733c2e7bf17dc5250ab074f937cc2a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="type-element-measuregroupattribute-assl"></a>Type 요소(MeasureGroupAttribute)(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  형식을 포함 한 [MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroupAttribute>  
   ...  
   <Type>...</Type>  
   ...  
</MeasureGroupAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*Regular*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*Regular*|일반 특성을 나타냅니다.|  
|*세분성*|세분성 특성을 나타냅니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MeasureGroupAttributeType>합니다.  
  
 부모에 해당 하는 요소 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [요소 특성 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)   
 [RegularMeasureGroupDimension 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
