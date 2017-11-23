---
title: "Name 요소 (ASSL) | Microsoft Docs"
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
apiname: Name Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Name
helpviewer_keywords: Name element
ms.assetid: caf2af86-5f9c-4e14-8168-f3a79248b4fe
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ec0f34bbcfa45f2ca704506374886c8ba591eca9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(최대 100자)|  
|기본값|상황에 따라 다름|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../../../analysis-services/scripting/objects/action-element-assl.md), [집계](../../../analysis-services/scripting/objects/aggregation-element-assl.md), [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md), [AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md), [주석](../../../analysis-services/scripting/objects/annotation-element-assl.md), [ 어셈블리](../../../analysis-services/scripting/objects/assembly-element-assl.md), [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md), [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md), [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md), [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md), [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md), [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md), [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md), [차원](../../../analysis-services/scripting/objects/dimension-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [그룹](../../../analysis-services/scripting/objects/group-element-assl.md), [계층](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [수준](../../../analysis-services/scripting/objects/level-element-assl.md), [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md), [ 측정값](../../../analysis-services/scripting/objects/measure-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MemberProperty](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md), [ MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md), [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md), [권한](../../../analysis-services/scripting/data-type/permission-data-type-assl.md), [ 큐브 뷰](../../../analysis-services/scripting/objects/perspective-element-assl.md), [PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md), [ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md), [ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md), [ 역할](../../../analysis-services/scripting/objects/role-element-assl.md), [서버](../../../analysis-services/scripting/objects/server-element-assl.md), [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md), [추적](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 개체를 정의 하는 데 사용 되는 모든 요소 (인스턴스의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 계층, 특성 및 등)에 **이름** 속성으로는 요소입니다. 값을 **이름** 요소에는 다음과 같은 제한:  
  
-   값은 선행 공백이나 후행 공백을 포함할 수 없습니다. 값에 선행 또는 후행 공백이 포함 된 경우는 **이름** 요소, 해당 공백은 암시적으로 제거 됩니다 여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
-   값에 제어 문자가 포함되어서는 안 됩니다. 이름에는 제어 문자가 없는 것이 좋습니다. 제어 문자가 있으면 XML 유효성 검사 오류가 발생할 수 있습니다.  
  
     사용 하 여 만든 개체에 대 한는 **GetNewName** 메서드에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], AMO에 대 한 확인 하 고 선행 공백 또는 후행 공백을 이름에는 제어 문자가 후 제거 합니다. 이 대 한 이유를 사용 하 여 **GetNewName** 는 개체 이름을 설정 하기 위한 권장된 방법입니다.  
  
     그러나 설정 하는 경우는 **이름** 속성을 직접 검사를 수행 하지, XML 유효성 검사 오류가 발생할 수 있으므로 동일한 유효성 검사 합니다. 오류가 실제로 발생하는지 여부에 따라 이름에 나타나는 제어 문자가 달라집니다.  
  
     개체 이름에 제어 문자를 사용하지 않아야 하지만 Analysis Services에서는 이를 명시적으로 금지하지는 않습니다. 이전 버전의 Analysis Services에서는 때에 따라 개체 이름에 제어 문자를 허용했습니다. 이 대 한 이유로 SQL Server 2016 Analysis Services 하 고 나중에 이전 솔루션을 위반을 방지 하기 위해 개체 이름에 제어 문자를 무시 합니다.  
  
-   예약된 다음 값은 사용할 수 없습니다.  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 - COM9(COM1, COM2, COM3 등)  
  
    -   CON  
  
    -   LPT1 - LPT9(LPT1, LPT2, LPT3 등)  
  
    -   NUL  
  
    -   PRN  
  
 다음 표에서 값으로 사용할 수 없는 추가 문자를 보여 줍니다.는 **이름** 부모 요소에 따라 요소입니다.  
  
|부모 요소|잘못된 문자|  
|--------------------|------------------------|  
|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|이 이름은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 컴퓨터 이름 규칙을 따라야 합니다. IP 주소는 유효하지 않습니다.|  
|[데이터 원본](../../../analysis-services/scripting/objects/datasource-element-assl.md)|:/\\*&#124;?"()[]{}<>|  
|[수준](../../../analysis-services/scripting/objects/level-element-assl.md), [요소 특성](../../../analysis-services/scripting/objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"&%$!+=[]{}<>|  
|기타 모든 부모 요소|.,;'`:/\\*&#124;?"&%$!+=()[]{}<>|  
  
## <a name="see-also"></a>관련 항목:  
 [ID 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/id-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
