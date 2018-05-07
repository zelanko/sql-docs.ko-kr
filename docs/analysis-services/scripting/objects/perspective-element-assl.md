---
title: Perspective 요소 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6187e2d7098b0ba284308327683204ae665e25f5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="perspective-element-assl"></a>Perspective 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  큐브 뷰에 대 한 세부 정보를 정의 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Perspectives>  
   <<Perspective>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Translations>...</Translations>  
      <DefaultMeasure>...</DefaultMeasure>  
      <Dimensions>...</Dimensions>  
            <MeasureGroups>...</MeasureGroups>  
      <Calculations>...</Calculations>  
      <Kpis>...</Kpis>  
            <Actions>...</Actions>  
      <Annotations>...</Annotations>  
   </Perspective>  
</Perspectives>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브 뷰](../../../analysis-services/scripting/collections/perspectives-element-assl.md)|  
|자식 요소|[작업](../../../analysis-services/scripting/collections/actions-element-assl.md), [주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [계산](../../../analysis-services/scripting/collections/calculations-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [DefaultMeasure](../../../analysis-services/scripting/properties/defaultmeasure-element-assl.md), [ 설명](../../../analysis-services/scripting/properties/description-element-assl.md), [차원](../../../analysis-services/scripting/collections/dimensions-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [Kpi](../../../analysis-services/scripting/collections/kpis-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [ MeasureGroups](../../../analysis-services/scripting/collections/measuregroups-element-assl.md), [이름](../../../analysis-services/scripting/properties/name-element-assl.md), [번역](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 큐브 뷰는 포함될 차원, 계층, 특성 및 다른 세부 정보를 선택하고 포함될 데이터 조각을 정의하는 큐브의 하위 집합을 제공합니다. 단일 큐브가 큐브 뷰를 소유합니다. 큐브 뷰 내에서 개체를 재정의하거나 추가할 수 없습니다. 모든 차원, 계층 및 기타 세부 정보는 기본 큐브에 있어야 합니다. 또한 개체를 포함한 다음 해당 개체가 보이지 않도록 표시할 수 없습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Perspective>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
