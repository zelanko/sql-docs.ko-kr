---
title: CubeDimension 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c3ea688681749a2b22f8c457fb9a5eb8ee39d8eb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059535"
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
|기본 데이터 형식|없음|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[AllMemberAggregationUsage](../properties/aggregationusage-element-assl.md), [주석](../collections/annotations-element-assl.md), [특성](../collections/attributes-element-assl.md)를 [DimensionID](../properties/id-element-assl.md), [계층](../collections/hierarchies-element-assl.md)합니다 [HierarchyUniqueNameStyle](../properties/hierarchyuniquenamestyle-element-assl.md), [ID](../properties/id-element-assl.md)를 [MemberUniqueNameStyle](../properties/memberuniquenamestyle-element-assl.md)합니다 [이름](../properties/name-element-assl.md), [표시](../properties/visible-element-assl.md), [번역](../collections/translations-element-assl.md)|  
|파생 요소|[차원](../objects/dimension-element-assl.md) ([차원](../collections/dimensions-element-assl.md) 모음인 [큐브](../objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 `CubeDimension`에 있는 차원 관계마다 하나의 `Cube`이 있습니다. `CubeDimension`은 큐브의 모든 `MeasureGroups`를 포함합니다.  
  
 A `CubeDimension` 포함 해야 합니다는 [CubeHierarchy](hierarchy-data-type-assl.md) 차원에 있는 경우 특정 계층에 대 한 설정이 포함 하 여 계층을 사용 하지 않도록 설정 (따라서는 적용할 계층 선택 허용 특정 차원 용도), 계층 숨기기 등입니다.  
  
 마찬가지로, 한 `CubeDimension` 포함 해야 합니다는 [CubeAttribute](cubeattribute-data-type-assl.md) 차원에 특성에 대 한 예를 들어 특정 경우에 합니다. 특성을 숨길 수 있지만 특정 차원 사용에 적용할 특성을 선택할 수 있는 방법은 없습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.CubeDimension>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
