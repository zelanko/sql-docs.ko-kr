---
title: CubeDimension 데이터 형식 (ASSL) | Microsoft Docs
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
- CubeDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeDimension
helpviewer_keywords:
- CubeDimension data type
ms.assetid: 128ac790-65a1-4e35-b909-8dba2a61b24c
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4a043895929e09a59d3ae14c5995804c4fa5c7eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079671"
---
# <a name="cubedimension-data-type-assl"></a>CubeDimension 데이터 형식(ASSL)
  차원과 큐브 간의 관계를 나타내는 기본 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeDimension>  
      <ID>...</ID>  
   <Name>...</Name>  
   <Translations>...</Translations>  
   <DimensionID>...</DimensionID>  
   <Visible>...</Visible>  
   <AllMemberAggregationUsage>...</AllMemberAggregationUsage>  
   <HierarchyUniqueNameStyle>...</HierarchyUniqueNameStyle>  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
      <Attributes>...</Attributes>  
   <Hierarchies>...</Hierarchies>  
      <Annotations>...</Annotation>  
</CubeDimension>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[AllMemberAggregationUsage](../properties/aggregationusage-element-assl.md), [주석](../collections/annotations-element-assl.md), [특성](../collections/attributes-element-assl.md), [DimensionID](../properties/id-element-assl.md), [계층](../collections/hierarchies-element-assl.md), [HierarchyUniqueNameStyle](../properties/hierarchyuniquenamestyle-element-assl.md), [ID](../properties/id-element-assl.md), [MemberUniqueNameStyle](../properties/memberuniquenamestyle-element-assl.md), [이름](../properties/name-element-assl.md), [표시](../properties/visible-element-assl.md), [번역](../collections/translations-element-assl.md)|  
|파생 요소|[차원](../objects/dimension-element-assl.md) ([차원](../collections/dimensions-element-assl.md) 컬렉션 [큐브](../objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 `CubeDimension`에 있는 차원 관계마다 하나의 `Cube`이 있습니다. `CubeDimension`은 큐브의 모든 `MeasureGroups`를 포함합니다.  
  
 A `CubeDimension` 포함 되어야 합니다는 [CubeHierarchy](hierarchy-data-type-assl.md) 차원에 계층 구조에 대 한 특정 항목을 포함 하 여 계층 해제 (선택 허용 적용할 계층을 특정 차원 용도), 계층 숨기기 또는 합니다.  
  
 마찬가지로, 한 `CubeDimension` 포함 되어야 합니다는 [CubeAttribute](cubeattribute-data-type-assl.md) 차원에 특성에 대 한 특정를 하는 경우에 합니다. 특성을 숨길 수 있지만 특정 차원 사용에 적용할 특성을 선택할 수 있는 방법은 없습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.CubeDimension>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 스크립팅 언어 XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  