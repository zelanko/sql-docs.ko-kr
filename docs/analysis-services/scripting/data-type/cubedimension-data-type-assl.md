---
title: "CubeDimension 데이터 형식 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CubeDimension Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CubeDimension
helpviewer_keywords:
- CubeDimension data type
ms.assetid: 128ac790-65a1-4e35-b909-8dba2a61b24c
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6e66f279cfff5bd8f80cacedf014eb318c7ad9a4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

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
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[AllMemberAggregationUsage](../../../analysis-services/scripting/properties/allmemberaggregationusage-element-assl.md), [주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [특성](../../../analysis-services/scripting/collections/attributes-element-assl.md), [DimensionID](../../../analysis-services/scripting/properties/dimensionid-element-assl.md), [계층](../../../analysis-services/scripting/collections/hierarchies-element-assl.md), [HierarchyUniqueNameStyle](../../../analysis-services/scripting/properties/hierarchyuniquenamestyle-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [MemberUniqueNameStyle](../../../analysis-services/scripting/properties/memberuniquenamestyle-element-assl.md), [이름](../../../analysis-services/scripting/properties/name-element-assl.md), [표시](../../../analysis-services/scripting/properties/visible-element-assl.md), [번역](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|파생 요소|[차원](../../../analysis-services/scripting/objects/dimension-element-assl.md) ([차원](../../../analysis-services/scripting/collections/dimensions-element-assl.md) 컬렉션 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>주의  
 **CubeDimension** 에 있는 차원 관계마다 하나의 **Cube**이 있습니다. **CubeDimension** 은 큐브의 모든 **MeasureGroups** 를 포함합니다.  
  
 A **CubeDimension** 포함 되어야 합니다는 [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md) 차원에 계층 구조에 대 한 특정 항목을 포함 하 여 계층 해제 (선택 허용는 에 적용할 계층 특정 차원 사용), 계층 숨기기 또는 합니다.  
  
 마찬가지로, 한 **CubeDimension** 포함 되어야 합니다는 [CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md) 차원에 특성에 대 한 특정를 하는 경우에 합니다. 특성을 숨길 수 있지만 특정 차원 사용에 적용할 특성을 선택할 수 있는 방법은 없습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.CubeDimension>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

