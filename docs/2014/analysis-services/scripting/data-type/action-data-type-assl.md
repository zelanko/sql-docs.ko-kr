---
title: Action 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Action Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Action data type
ms.assetid: 8c4d2ff7-17e1-4e74-bec7-637e0b191acf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 21c13562fa53c0ba396a4c3826889e8d275f7d9a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197493"
---
# <a name="action-data-type-assl"></a>Action 데이터 형식(ASSL)
  동작을 나타내는 추상 기본 데이터 형식을 정의 [큐브](../objects/cube-element-assl.md) 요소 또는 [관점](../objects/perspective-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Caption>...</Caption>  
      <CaptionIsMdx>...</CaptionIsMdx>  
      <Translations>...</Translations>  
   <TargetType>...</TargetType>  
   <Target>...</Target>  
   <Condition>...</Condition>  
   <Type>...</Type>  
   <Invocation>...</Invocation>  
   <Application>...</Application>  
      <Description>...</Description>  
      <Annotations>...</Annotations>  
</Action>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|[DrillThroughAction](action-data-type-assl.md)하십시오 [ReportAction](reportaction-data-type-assl.md), [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../collections/actions-element-assl.md)|  
|자식 요소|[주석을](../collections/annotations-element-assl.md), [응용 프로그램](../properties/application-element-assl.md)를 [캡션](../properties/caption-element-assl.md)를 [CaptionIsMdx](../properties/captionismdx-element-assl.md)를 [조건](../properties/condition-element-assl.md), [설명 ](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md)를 [호출](../properties/invocation-element-assl.md)를 [이름](../properties/name-element-assl.md)를 [대상](../properties/target-element-assl.md)를 [TargetType](../properties/targettype-element-assl.md), [번역](../collections/translations-element-assl.md), [형식](../properties/type-element-action-assl.md)|  
|파생 요소|[DrillThroughAction](action-data-type-assl.md)하십시오 [ReportAction](reportaction-data-type-assl.md), [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 동작에 대한 자세한 내용은 [동작&#40;Analysis Services - 다차원 데이터&#41;](../../multidimensional-models/actions-analysis-services-multidimensional-data.md)을 참조하세요.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [큐브 요소 &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Perspective 요소의 &#40;ASSL&#41;](../objects/perspective-element-assl.md)   
 [PerspectiveAction 데이터 형식 &#40;ASSL&#41;](perspectiveaction-data-type-assl.md)   
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
