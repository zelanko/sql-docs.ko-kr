---
title: Kpi 요소 (ASSL) | Microsoft Docs
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
- Kpi Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Kpi
helpviewer_keywords:
- Kpi element
ms.assetid: 1979a58f-97a8-4c1a-aa65-dcfb6d2404cf
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27b0bcbe2ddaabcc7b3f9ef16f3fa620a8c2db38
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235643"
---
# <a name="kpi-element-assl"></a>Kpi 요소(ASSL)
  핵심 성과 지표 (KPI) 내에서 정의 된 [큐브](cube-element-assl.md) 요소 또는 [관점](perspective-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Kpis>  
   <Kpi> <!-- ancestor: Cube -->  
            <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <Translations>...</Translations>  
      <DisplayFolder>...</DisplayFolder>  
      <AssociatedMeasureGroupID>...</AssociatedMeasureGroupID>  
      <Value>...</Value>  
            <Goal>...</Goal>  
      <Status>...</Status>  
      <Trend>...</Trend>  
      <TrendGraphic>...</TrendGraphic>  
      <StatusGraphic>...</StatusGraphic>  
      <CurrentTimeMember>...</CurrentTimeMember>  
      <Annotations>...</Annotations>  
   </Kpi>  
   <!-- or -->  
   <Kpi xsi:type="PerspectiveKpi">...</Kpi> <!-- ancestor: Perspective -->  
   </Kpi>  
</Kpis>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
|상위 항목 또는 부모|데이터 형식|  
|------------------------|---------------|  
|[Cube](cube-element-assl.md)|InclusionThresholdSetting|  
|[큐브 뷰](../data-type/perspectivekpi-data-type-assl.md)|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Kpi](../collections/kpis-element-assl.md)|  
  
## <a name="child-elements"></a>자식 요소  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|--------------------|  
|[큐브](../collections/annotations-element-assl.md), [AssociatedMeasureGroupID](../properties/id-element-assl.md), [CurrentTimeMember](member-element-assl.md)를 [설명을](../properties/description-element-assl.md)를 [DisplayFolder](../properties/displayfolder-element-assl.md)를 [목표](../properties/goal-element-assl.md), [ID](../properties/id-element-assl.md)를 [이름](../properties/name-element-assl.md)합니다 [상태](../properties/status-element-assl.md), [StatusGraphic](../properties/statusgraphic-element-assl.md), [번역 ](../collections/translations-element-assl.md)하십시오 [추세](../properties/trend-element-assl.md)합니다 [TrendGraphic](../properties/trendgraphic-element-assl.md), [값](../properties/value-element-assl.md)|  
|[큐브 뷰](perspective-element-assl.md)|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Objects) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Kpi> 및 <xref:Microsoft.AnalysisServices.PerspectiveKpi>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
