---
title: 요소 (ASSL) 측정 | Microsoft Docs
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
- Measure Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Measure
helpviewer_keywords:
- Measure element
ms.assetid: 4c2c2ed1-7f78-4564-982a-132f13bea36f
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: da78700e32c81dab11d6609ca4aa12efd2204bcb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079136"
---
# <a name="measure-element-assl"></a>Measure 요소(ASSL)
  측정값을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Measures>  
   <Measure> <!-- ancestor: MeasureGroup -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <AggregateFunction>...</AggregateFunction>  
            <DataType>...</DataType>  
            <Source>...</Source>  
      <Visible>...</Visible>  
      <MeasureExpression>...</MeasureExpression>  
      <DisplayFolder>...</DisplayFolder>  
      <FormatString>...</FormatString>  
      <BackColor>...</BackColor>  
      <ForeColor>...</ForeColor>  
            <FontName>...</FontName>  
            <FontSize>...</FontSize>  
            <FontFlags>...</FontFlags>  
            <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Measure>  
   <!-- or  -->  
   <Measure xsi:type="AggregationInstanceMeasure">...</Measure> <!-- parent: AggregationInstance -->  
      <!-- or  -->  
   <Measure xsi:type="MeasureBinding">...</Measure> <!-- ancestor: MeasureGroupBinding (out-of-line) -->  
   <!-- or  -->  
   <Measure xsi:type="PerspectiveMeasure">...</Measure> <!-- ancestor: PerspectiveMeasureGroup -->  
</Measures>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
|상위 항목 또는 부모|데이터 형식|  
|------------------------|---------------|  
|[AggregationInstance](../data-type/binding-data-type-assl.md)|  
|[측정값 그룹](group-element-assl.md)|InclusionThresholdSetting|  
|[MeasureGroupBinding (아웃 아웃오브 라인)](../data-type/measurebinding-data-type-assl.md)|  
|[PerspectiveMeasureGroup](../data-type/perspectivemeasure-data-type-assl.md)|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[측정값](../collections/measures-element-assl.md)|  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|--------------------|  
|[MeasureGroup](../properties/aggregatefunction-element-assl.md), [Annotations](../collections/annotations-element-assl.md), [BackColor](../properties/backcolor-element-assl.md), [DataType](../properties/datatype-element-assl.md), [Description](../properties/description-element-assl.md), [DisplayFolder](../properties/displayfolder-element-assl.md), [FontFlags](../properties/fontflags-element-assl.md), [FontName](../properties/name-element-assl.md), [FontSize](../properties/fontsize-element-assl.md), [ForeColor](../properties/forecolor-element-assl.md), [FormatString](../properties/formatstring-element-assl.md), [ID](../properties/id-element-assl.md), [MeasureExpression](../properties/expression-element-assl.md), [Name](../properties/name-element-assl.md), [Source](../properties/source-element-measure-assl.md), [Translations](../collections/translations-element-assl.md), [Visible](../properties/visible-element-assl.md)|  
|나머지|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 측정값에 대한 바인딩 세부 정보가 제공될 수 있습니다. 이때 이러한 세부 정보는 파티션마다 기본값으로 동작합니다.  
  
 보다 큰 큐브에는 수백 개의 측정값과 계층이 있을 수 있습니다. `DisplayFolder` 속성은 클라이언트의 사용자 모양을 정의합니다. `DisplayFolder` 속성의 값은 다음 옵션 중 하나를 포함할 수 있습니다.  
  
-   비워 둡니다. 측정값이 폴더에 속하지 않음을 나타냅니다.  
  
-   단일 폴더 이름을 포함합니다. 측정값이 동일한 이름의 폴더에 속하는 것으로 렌더링되어야 함을 나타냅니다.  
  
-   백슬래시로 구분 된 여러 폴더 이름을 포함 (\\), 포함된 된 폴더 계층을 나타냅니다.  
  
 `DisplayFolder` 속성도 계산 측정값 및 계층에 적용됩니다.  
  
 AMO(Analysis Management Objects) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Measure> 및 <xref:Microsoft.AnalysisServices.PerspectiveMeasure>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  