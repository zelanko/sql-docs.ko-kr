---
title: Action 데이터 형식 (ASSL) | Microsoft Docs
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
- Action Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Action data type
ms.assetid: 8c4d2ff7-17e1-4e74-bec7-637e0b191acf
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 18047bc8a33c92e6bcd434e1a472917c269272e5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36173200"
---
# <a name="action-data-type-assl"></a>Action 데이터 형식(ASSL)
  작업을 나타내는 추상 기본 데이터 형식을 정의 [큐브](../objects/cube-element-assl.md) 요소 또는 [관점](../objects/perspective-element-assl.md) 요소입니다.  
  
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
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|[DrillThroughAction](action-data-type-assl.md), [ReportAction](reportaction-data-type-assl.md), [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../collections/actions-element-assl.md)|  
|자식 요소|[Annotations](../collections/annotations-element-assl.md), [Application](../properties/application-element-assl.md), [Caption](../properties/caption-element-assl.md), [CaptionIsMdx](../properties/captionismdx-element-assl.md), [Condition](../properties/condition-element-assl.md), [Description](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [Invocation](../properties/invocation-element-assl.md), [Name](../properties/name-element-assl.md), [Target](../properties/target-element-assl.md), [TargetType](../properties/targettype-element-assl.md), [Translations](../collections/translations-element-assl.md), [Type](../properties/type-element-action-assl.md)|  
|파생 요소|[DrillThroughAction](action-data-type-assl.md), [ReportAction](reportaction-data-type-assl.md), [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 동작에 대한 자세한 내용은 [동작&#40;Analysis Services - 다차원 데이터&#41;](../../multidimensional-models/actions-analysis-services-multidimensional-data.md)을 참조하세요.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [큐브 요소 &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Perspective 요소 &#40;ASSL&#41;](../objects/perspective-element-assl.md)   
 [PerspectiveAction 데이터 형식 &#40;ASSL&#41;](perspectiveaction-data-type-assl.md)   
 [Analysis Services 스크립팅 언어 XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  