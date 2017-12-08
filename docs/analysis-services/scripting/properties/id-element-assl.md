---
title: "ID 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
apiname: ID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ID
helpviewer_keywords: ID element
ms.assetid: ea3ce0f4-9084-45d0-8150-73afb7005af2
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e0f489f02475053495704cdf82c30d5253abf949
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(최대 100자)|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../../../analysis-services/scripting/objects/action-element-assl.md), [집계](../../../analysis-services/scripting/objects/aggregation-element-assl.md), [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md), [어셈블리](../../../analysis-services/scripting/objects/assembly-element-assl.md), [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md), [CubeBinding](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md), [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md), [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md), [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md), [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md), [차원 ](../../../analysis-services/scripting/objects/dimension-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [계층](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [수준](../../../analysis-services/scripting/objects/level-element-assl.md), [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md), [측정값](../../../analysis-services/scripting/objects/measure-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [ MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md), [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md), [권한](../../../analysis-services/scripting/data-type/permission-data-type-assl.md), [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md), [역할](../../../analysis-services/scripting/objects/role-element-assl.md), [서버](../../../analysis-services/scripting/objects/server-element-assl.md), [추적](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 모든 주요 개체에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 **ID** 속성으로는 요소입니다. 값은 **ID** 요소에는 다음과 같은 제한 사항이 있습니다.  
  
-   값은 선행 공백이나 후행 공백을 포함할 수 없습니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]값에서 선행 또는 후행 공백을 암시적으로 제거 됩니다는 **ID** 요소입니다.  
  
-   값은 제어 문자를 포함할 수 없습니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]값에서 제어 문자를 암시적으로 제거 됩니다는 **ID** 요소입니다.  
  
-   예약된 다음 값은 사용할 수 없습니다.  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 - COM9(COM1, COM2, COM3 등)  
  
    -   CON  
  
    -   LPT1 - LPT9(LPT1, LPT2, LPT3 등)  
  
    -   NUL  
  
    -   PRN  
  
 다음 표에서 값으로 사용할 수 없는 추가 문자는 **ID** 부모 요소에 따라 요소입니다.  
  
|부모 요소|문자|  
|--------------------|----------------|  
|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|값은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 컴퓨터 이름 규칙을 따라야 합니다. IP 주소는 유효하지 않습니다.|  
|[데이터 원본](../../../analysis-services/scripting/objects/datasource-element-assl.md)|:/\\*&#124;?"()[]{}<>|  
|[수준](../../../analysis-services/scripting/objects/level-element-assl.md), [요소 특성](../../../analysis-services/scripting/objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"&%$!+=[]{}<>|  
|기타 모든 부모 요소|.,;'`:/\\*&#124;?"&%$!+=()[]{}<>|  
  
## <a name="see-also"></a>관련 항목:  
 [Name 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/name-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
