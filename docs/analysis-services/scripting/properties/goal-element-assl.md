---
title: Goal 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 234bbcfa1d4bcb2a0d95489b71fee10555057b6e
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="goal-element-assl"></a>Goal 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  원하는 목표를 식별 한 [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Kpi>  
   ...  
   <Goal>...</Goal>  
   ...  
</Kpi>  
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
|부모 요소|[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **Goal** 요소는 MDX(Multidimensional Expressions) 식을 포함합니다.  
  
 부모에 해당 하는 요소 **목표** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Kpi>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Status 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/status-element-assl.md)   
 [요소 추세 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/trend-element-assl.md)   
 [요소 값 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/value-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
