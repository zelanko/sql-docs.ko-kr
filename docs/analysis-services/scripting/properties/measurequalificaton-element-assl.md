---
title: MeasureQualificaton 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 198c11e2e1b3f93f75f1f5be249350a1bd342d93
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="measurequalificaton-element-assl"></a>MeasureQualificaton 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  측정값에 대 한 접두사 적용 여부를 결정은 [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroup>  
   ...  
   <MeasureQualification>...</MeasureQualification>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*없음*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[측정값 그룹](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*없음*|이 측정값 그룹의 측정값에 접두사가 적용되지 않습니다.|  
|*PrefixMeasureGroup*|이 측정값 그룹에 있는 각 측정값의 고유한 이름 및 캡션에 측정값 그룹 및 공백 하나가 접두사로 적용됩니다.|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **MeasureQualification** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MeasureGroup>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Cube 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Dimension 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [MeasureGroup 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
