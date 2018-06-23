---
title: Name 요소 (ASSL) | Microsoft Docs
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
- Name Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Name
helpviewer_keywords:
- Name element
ms.assetid: caf2af86-5f9c-4e14-8168-f3a79248b4fe
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cb2185d9d2a87a2abc3ebb96ad8186fe288e6190
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093616"
---
# <a name="name-element-assl"></a>Name 요소(ASSL)
  부모 요소의 이름을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Name>...</Name>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(최대 100자)|  
|기본값|상황에 따라 다름|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Action](../objects/action-element-assl.md), [Aggregation](../objects/aggregation-element-assl.md), [AggregationDesign](../objects/aggregationdesign-element-assl.md), [AlgorithmParameter](../objects/algorithmparameter-element-assl.md), [Annotation](../objects/annotation-element-assl.md), [Assembly](../objects/assembly-element-assl.md), [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md), [Cube](../objects/cube-element-assl.md), [CubeDimension](../data-type/dimension-data-type-assl.md), [CubeHierarchy](../data-type/hierarchy-data-type-assl.md), [Database](../objects/database-element-assl.md), [DataSource](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [Dimension](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [Group](../objects/group-element-assl.md), [Hierarchy](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [Level](../objects/level-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [Measure](../objects/measure-element-assl.md), [MeasureGroup](../objects/measuregroup-element-assl.md), [MemberProperty](../objects/attributerelationship-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [Partition](../objects/partition-element-assl.md), [Permission](../data-type/permission-data-type-assl.md), [Perspective](../objects/perspective-element-assl.md), [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md), [ReportFormatParameter](../objects/reportformatparameter-element-asl.md), [ReportParameter](../objects/reportparameter-element-assl.md), [Role](../objects/role-element-assl.md), [Server](../objects/server-element-assl.md), [ServerProperty](../objects/serverproperty-element-assl.md), [Trace](../objects/trace-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 개체를 정의 하는 데 사용 되는 모든 요소 (인스턴스의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 계층, 특성 및 등)에 `Name` 요소가 속성으로. `Name` 요소 값에는 다음과 같은 제한 사항이 있습니다.  
  
-   값은 선행 공백이나 후행 공백을 포함할 수 없습니다. `Name` 요소 값에 선행 공백이나 후행 공백이 포함될 경우 이러한 공백은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 의해 암시적으로 제거됩니다.  
  
-   값에 제어 문자가 포함되어서는 안 됩니다. 이름에는 제어 문자가 없는 것이 좋습니다. 제어 문자가 있으면 XML 유효성 검사 오류가 발생할 수 있습니다.  
  
     [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 `GetNewName` 메서드를 사용하여 만든 개체의 경우 AMO는 이름에서 제어 문자, 선행 공백 또는 후행 공백을 검사한 후 제거합니다. 따라서 개체 이름을 설정할 때에는 `GetNewName`을 사용하는 것이 좋습니다.  
  
     그러나 `Name` 속성을 직접 설정하는 경우 XML 유효성 검사 오류가 발생할 수 있으므로 동일한 유효성 검사는 수행되지 않습니다. 오류가 실제로 발생하는지 여부에 따라 이름에 나타나는 제어 문자가 달라집니다.  
  
     개체 이름에 제어 문자를 사용하지 않아야 하지만 Analysis Services에서는 이를 명시적으로 금지하지는 않습니다. 이전 버전의 Analysis Services에서는 때에 따라 개체 이름에 제어 문자를 허용했습니다. 따라서 이전 솔루션을 위반하지 않기 위해 [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)]는 개체 이름에서 제어 문자를 무시합니다.  
  
-   예약된 다음 값은 사용할 수 없습니다.  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 - COM9(COM1, COM2, COM3 등)  
  
    -   CON  
  
    -   LPT1 - LPT9(LPT1, LPT2, LPT3 등)  
  
    -   NUL  
  
    -   PRN  
  
 다음 표에서는 부모 요소에 따라 `Name` 요소 값으로 사용할 수 없는 추가 문자를 보여 줍니다.  
  
|부모 요소|잘못된 문자|  
|--------------------|------------------------|  
|[Server](../objects/server-element-assl.md)|이 이름은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 컴퓨터 이름 규칙을 따라야 합니다. IP 주소는 유효하지 않습니다.|  
|[DataSource](../objects/datasource-element-assl.md)|:/\\*&#124;?" (){}<>|  
|[수준](../objects/level-element-assl.md), [요소 특성](../objects/attribute-element-assl.md)|.,;' `:/\\*&#124;?" & % $! + ={}<>|  
|기타 모든 부모 요소|.,;' `:/\\*&#124;?" & % $! + = (){}<>|  
  
## <a name="see-also"></a>관련 항목  
 [ID 요소 &#40;ASSL&#41;](id-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  