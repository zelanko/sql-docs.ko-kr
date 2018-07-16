---
title: Perspective 요소 (ASSL) | Microsoft Docs
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
- Perspective Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Perspective
helpviewer_keywords:
- Perspective element
ms.assetid: 0442334c-8b00-4451-ad81-02e58c735e8f
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b006d7d48c072cb98a68e42c04cf75c4aaa9e04
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297403"
---
# <a name="perspective-element-assl"></a>Perspective 요소(ASSL)
  큐브 뷰에 대 한 세부 정보를 정의 된 [큐브](cube-element-assl.md) 요소입니다.  
  
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브 뷰](../collections/perspectives-element-assl.md)|  
|자식 요소|[작업](../collections/actions-element-assl.md), [주석을](../collections/annotations-element-assl.md)를 [계산](../collections/calculations-element-assl.md)를 [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)를 [DefaultMeasure](measure-element-assl.md), [ 설명을](../properties/description-element-assl.md), [차원](../collections/dimensions-element-assl.md)를 [ID](../properties/id-element-assl.md)를 [Kpi](../collections/kpis-element-assl.md)를 [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [ MeasureGroups](../collections/groups-element-assl.md)하십시오 [이름](../properties/name-element-assl.md), [번역](../collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 큐브 뷰는 포함될 차원, 계층, 특성 및 다른 세부 정보를 선택하고 포함될 데이터 조각을 정의하는 큐브의 하위 집합을 제공합니다. 단일 큐브가 큐브 뷰를 소유합니다. 큐브 뷰 내에서 개체를 재정의하거나 추가할 수 없습니다. 모든 차원, 계층 및 기타 세부 정보는 기본 큐브에 있어야 합니다. 또한 개체를 포함한 다음 해당 개체가 보이지 않도록 표시할 수 없습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Perspective>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
