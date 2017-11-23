---
title: "요소 (ASSL) 측정 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Measure Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Measure
helpviewer_keywords: Measure element
ms.assetid: 4c2c2ed1-7f78-4564-982a-132f13bea36f
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9942b67b7877e337f34667b90a49bd7c33595592
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|아래 표를 참조 합니다.|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
|상위 항목 또는 부모|데이터 형식|  
|------------------------|---------------|  
|[AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|[AggregationInstanceMeasure](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[측정값 그룹](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|없음|  
|[MeasureGroupBinding (아웃 아웃오브 라인)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)|[PerspectiveMeasure](../../../analysis-services/scripting/data-type/perspectivemeasure-data-type-assl.md)|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[측정값](../../../analysis-services/scripting/collections/measures-element-assl.md)|  
|자식 요소|아래 표를 참조 합니다.|  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|--------------------|  
|[측정값 그룹](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[AggregateFunction](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md), [주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [BackColor](../../../analysis-services/scripting/properties/backcolor-element-assl.md), [DataType](../../../analysis-services/scripting/properties/datatype-element-assl.md), [설명](../../../analysis-services/scripting/properties/description-element-assl.md), [ DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md), [FontFlags](../../../analysis-services/scripting/properties/fontflags-element-assl.md), [FontName](../../../analysis-services/scripting/properties/fontname-element-assl.md), [FontSize](../../../analysis-services/scripting/properties/fontsize-element-assl.md), [ForeColor](../../../analysis-services/scripting/properties/forecolor-element-assl.md), [ FormatString](../../../analysis-services/scripting/properties/formatstring-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [MeasureExpression](../../../analysis-services/scripting/properties/measureexpression-element-assl.md), [이름](../../../analysis-services/scripting/properties/name-element-assl.md), [소스](../../../analysis-services/scripting/properties/source-element-measure-assl.md), [ 번역](../../../analysis-services/scripting/collections/translations-element-assl.md), [표시](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
|나머지|없음|  
  
## <a name="remarks"></a>주의  
 측정값에 대한 바인딩 세부 정보가 제공될 수 있습니다. 이때 이러한 세부 정보는 파티션마다 기본값으로 동작합니다.  
  
 보다 큰 큐브에는 수백 개의 측정값과 계층이 있을 수 있습니다. **DisplayFolder** 속성은 클라이언트의 사용자 모양을 정의합니다. **DisplayFolder** 속성의 값은 다음 옵션 중 하나를 포함할 수 있습니다.  
  
-   비워 둡니다. 측정값이 폴더에 속하지 않음을 나타냅니다.  
  
-   단일 폴더 이름을 포함합니다. 측정값이 동일한 이름의 폴더에 속하는 것으로 렌더링되어야 함을 나타냅니다.  
  
-   백슬래시로 구분 된 여러 폴더 이름을 포함 (\\), 포함된 된 폴더 계층을 나타냅니다.  
  
 **DisplayFolder** 속성도 계산 측정값 및 계층에 적용됩니다.  
  
 AMO(Analysis Management Objects) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Measure> 및 <xref:Microsoft.AnalysisServices.PerspectiveMeasure>입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
