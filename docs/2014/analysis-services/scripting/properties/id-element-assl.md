---
title: ID 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ID
helpviewer_keywords:
- ID element
ms.assetid: ea3ce0f4-9084-45d0-8150-73afb7005af2
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0a1ad98b6b9609cf50d16816c8ae5328083a63ec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185273"
---
# <a name="id-element-assl"></a>ID 요소(ASSL)
  부모 요소의 ID(고유 식별자)를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action> <!-- or one of the elements listed in the Element Relationships table -->  
   ...  
   <ID>...</ID>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(최대 100자)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Action](../objects/action-element-assl.md), [Aggregation](../objects/aggregation-element-assl.md), [AggregationDesign](../objects/aggregationdesign-element-assl.md), [Assembly](../objects/assembly-element-assl.md), [Cube](../objects/cube-element-assl.md), [CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md), [CubeDimension](../data-type/dimension-data-type-assl.md), [Database](../objects/database-element-assl.md), [DataSource](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [Dimension](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [Hierarchy](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [Level](../objects/level-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [Measure](../objects/measure-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [MeasureGroupBinding](../data-type/binding-data-type-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [Partition](../objects/partition-element-assl.md), [Permission](../data-type/permission-data-type-assl.md), [Perspective](../objects/perspective-element-assl.md), [Role](../objects/role-element-assl.md), [Server](../objects/server-element-assl.md), [Trace](../objects/trace-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 모든 주요 개체에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 `ID` 요소가 속성으로. `ID` 요소 값에는 다음과 같은 제한 사항이 있습니다.  
  
-   값은 선행 공백이나 후행 공백을 포함할 수 없습니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 `ID` 요소 값에서 선행 공백이나 후행 공백을 암시적으로 제거합니다.  
  
-   값은 제어 문자를 포함할 수 없습니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 `ID` 요소 값에서 제어 문자를 암시적으로 제거합니다.  
  
-   예약된 다음 값은 사용할 수 없습니다.  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 - COM9(COM1, COM2, COM3 등)  
  
    -   CON  
  
    -   LPT1 - LPT9(LPT1, LPT2, LPT3 등)  
  
    -   NUL  
  
    -   PRN  
  
 다음 표에서는 부모 요소에 따라 `ID` 요소 값으로 사용할 수 없는 추가 문자를 보여 줍니다.  
  
|부모 요소|문자|  
|--------------------|----------------|  
|[Server](../objects/server-element-assl.md)|값은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 컴퓨터 이름 규칙을 따라야 합니다. IP 주소는 유효하지 않습니다.|  
|[DataSource](../objects/datasource-element-assl.md)|:/\\*&#124;?" (){}<>|  
|[수준](../objects/level-element-assl.md), [요소 특성](../objects/attribute-element-assl.md)|.,;' `:/\\*&#124;?" & % $! + ={}<>|  
|기타 모든 부모 요소|.,;' `:/\\*&#124;?" & % $! + = (){}<>|  
  
## <a name="see-also"></a>관련 항목  
 [Name 요소 &#40;ASSL&#41;](name-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  