---
title: Translations 요소 (ASSL) | Microsoft Docs
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
- Translations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Translations
helpviewer_keywords:
- Translations element
ms.assetid: 7f6b8ff2-e834-44d3-a176-216203158a8d
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 81a39835738064ee9ba43f801c08bcec5301c5a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082166"
---
# <a name="translations-element-assl"></a>Translations 요소(ASSL)
  컬렉션을 포함 [번역](../objects/translation-element-assl.md) 부모 요소와 관련 된 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action><!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Translations>  
      <Translation>...</Translation>  
      <!-- or -->  
      <Translation xsi:type="AttributeTranslation">...</Translation><!-- parent: DimensionAttribute or ScalarMiningStructureColumn -->  
      <!-- or -->  
      <Translation xsi:type="RelationshipEndTranslation">...</Translation><!-- parent: RelationshipEnd -->  
   </Translations>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Action](../objects/action-element-assl.md), [AttributeRelationship](../objects/attributerelationship-element-assl.md), [CalculationProperty](../objects/calculationproperty-element-assl.md), [Cube](../objects/cube-element-assl.md), [CubeDimension](../data-type/dimension-data-type-assl.md), [Database](../objects/database-element-assl.md), [Dimension](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [Hierarchy](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [Level](../objects/level-element-assl.md), [Measure](../objects/measure-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [Perspective](../objects/perspective-element-assl.md), [RelationshipEnd](../data-type/relationshipend-data-type-assl.md), [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [TableMiningStructureColumn](../data-type/tableminingstructurecolumn-data-type-assl.md)|  
  
 **자식 요소**  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|-------------------|  
|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md) 또는 [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|[번역](../objects/translation-element-assl.md) 형식의 [AttributeTranslation](../data-type/translation-data-type-assl.md)|  
|[RelationshipEnd](../data-type/relationshipendtranslation-element-assl.md) 형식의 [RelationshipEndTranslation](../data-type/relationshipendtranslation-element-assl.md)|  
|나머지|[번역](../objects/translation-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Objects) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.TranslationCollection> 및 <xref:Microsoft.AnalysisServices.AttributeTranslationCollection>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  