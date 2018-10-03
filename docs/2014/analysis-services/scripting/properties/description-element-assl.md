---
title: Description 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Description Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Description
helpviewer_keywords:
- Description element
ms.assetid: 34d67e7c-e79a-429b-8cc3-6ca13b9cf9c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 19a041d81646361d1f6eefb96604829ec1928032
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126133"
---
# <a name="description-element-assl"></a>Description 요소(ASSL)
  부모 요소에 대한 설명을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Description>...</Description>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타나는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../objects/action-element-assl.md), [집계](../objects/aggregation-element-assl.md)를 [AggregationDesign](../objects/aggregationdesign-element-assl.md)를 [어셈블리](../objects/assembly-element-assl.md)를 [AttributePermission](../objects/attributepermission-element-assl.md), [ CalculationProperty](../objects/calculationproperty-element-assl.md), [CellPermission](../objects/cellpermission-element-assl.md), [큐브](../objects/cube-element-assl.md), [CubeDimensionPermission](../data-type/permission-data-type-assl.md)하십시오 [데이터베이스](../objects/database-element-assl.md) 를 [데이터 원본](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md)를 [차원](../objects/dimension-element-assl.md)를 [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [계층](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md)를 [수준](../objects/level-element-assl.md)를 [MdxScript](../objects/mdxscript-element-assl.md)를 [측정값](../objects/measure-element-assl.md)를 [MeasureGroup](../objects/group-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)를 [MiningStructure](../objects/miningstructure-element-assl.md)하십시오 [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [ 파티션](../objects/partition-element-assl.md), [권한을](../data-type/permission-data-type-assl.md), [관점](../objects/perspective-element-assl.md)를 [역할](../objects/role-element-assl.md)를 [Server](../objects/server-element-assl.md), [ 추적](../objects/trace-element-assl.md), [번역](../objects/translation-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Description` 요소 값에는 다음과 같은 제한 사항이 있습니다.  
  
-   값은 선행 공백이나 후행 공백을 포함할 수 없습니다. `Description` 요소 값에 선행 공백이나 후행 공백이 포함될 경우 이러한 공백은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 의해 암시적으로 제거됩니다.  
  
-   값은 제어 문자를 포함할 수 없습니다. `Description` 요소 값에 제어 문자가 포함될 경우 이러한 문자는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]  에 의해 암시적으로 제거됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소의 이름을 &#40;ASSL&#41;](name-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
