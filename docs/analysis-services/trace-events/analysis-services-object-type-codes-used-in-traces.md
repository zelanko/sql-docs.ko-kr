---
title: Analysis Services 개체 형식 코드를 추적에 사용 되는 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c21695966f39e0b1629ad58e0616aa42495d1caa
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="analysis-services-object-type-codes-used-in-traces"></a>추적에 사용되는 Analysis Services 개체 형식 코드
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  이 페이지에는 Analysis Services 데이터 모델에 있는 각 개체의 개체 형식(6자리 숫자)이 나열됩니다. 이러한 코드는 추적 로그에 표시되며 특정 잠금과 연관된 개체 형식을 식별하는 데 사용됩니다. 예를 들어 데이터베이스에 대한 잠금 시간 제한은 데이터베이스 개체 형식인 개체 형식 100002를 나타냅니다.  
  
> [!NOTE]  
>  아래에 나열된 코드는 추적 로그에 실제로 표시되는 코드보다 많습니다. 아래 목록은 모든 개체에 대한 형식 코드를 포함하는 포괄적인 목록이지만 잠금이 있는 개체만 추적 로그의 개체 형식 코드를 표시합니다.  
  
## <a name="object-type-reference"></a>개체 형식 참조  
  
|개체 유형|개체 이름|  
|-----------------|-----------------|  
|100000|Server|  
|100001|Command|  
|100002|데이터베이스|  
|100003|DataSource|  
|100004|DatabasePermission|  
|100005|역할|  
|100006|차원|  
|100007|DimensionAttribute|  
|100008|계층|  
|100009|Level|  
|100010|Cube|  
|100011|CubePermission|  
|100012|CubeDimension|  
|100013|CubeAttribute|  
|100014|CubeHierarchy|  
|100016|MeasureGroup|  
|100017|MeasureGroupDimension|  
|100018|MeasureGroupAttribute|  
|100020|이름|  
|100021|Partition|  
|100025|AggregationDesign|  
|100026|AggregationDesignDimension|  
|100027|AggregationDesignAttribute|  
|100028|집계|  
|100029|AggregationDimension|  
|100030|AggregationAttribute|  
|100032|MiningStructure|  
|100033|TableMiningStructureColumn|  
|100037|MiningModel|  
|100038|MiningModelColumn|  
|100039|AlgorithmParameter|  
|100041|MiningModelPermission|  
|100042|DimensionPermission|  
|100043|MiningStructurePermission|  
|100044|어셈블리|  
|100045|DatabaseRole|  
|100046|AttributePermission|  
|100047|CubeAttributePermission|  
|100048|CellPermission|  
|100049|CubeDimensionPermission|  
|100050|추적|  
|100051|ServerAssembly|  
|100052|CubeAssembly|  
|100053|Command|  
|100054|KPI|  
|100055|DataSourceView|  
|100056|Cube|  
|100100|CommandCollection|  
|100101|DatabaseCollection|  
|100102|DataSourceCollection|  
|100103|DatabasePermission|  
|100104|RoleCollection|  
|100105|DimensionCollection|  
|100106|DimensionAttributeCollection|  
|100107|HierarchyCollection|  
|100108|LevelCollection|  
|100109|CubeCollection|  
|100110|CubePermissionCollection|  
|100111|CubeDimensionCollection|  
|100112|CubeAttributeCollection|  
|100113|CubeHierarchyCollection|  
|100115|MeasureGroupCollection|  
|100116|MeasureGroupDimensionCollection|  
|100117|MeasureGroupAttributeCollection|  
|100119|MeasureCollection|  
|100120|PartitionCollection|  
|100124|AggregationDesignCollection|  
|100125|AggregationDesignDimensionCollection|  
|100126|AggregationDesignAttributeCollection|  
|100127|AggregationCollection|  
|100128|AggregationDimensionCollection|  
|100129|AggregationAttributeCollection|  
|100131|MiningStructureCollection|  
|100132|MiningStructureColumnCollection|  
|100136|MiningModelCollection|  
|100137|MiningModelColumnCollection|  
|100138|AlgorithmParameterCollection|  
|100140|MiningModelPermissionCollection|  
|100141|DimensionPermissionCollection|  
|100142|MiningStructurePermissionCollection|  
|100143|AssemblyCollection|  
|100144|DatabaseRoleCollecction|  
|100145|AttributePermissionCollection|  
|100146|CubeAttributePermissionCollection|  
|100147|CellPermissionCollection|  
|100148|CubeDimensionPermissionCollection|  
|100149|TraceCollection|  
|100150|ServerAssemblyCollection|  
|100151|CubeAssemblyCollection|  
|100152|CommandCollection|  
|100153|KpiCollection|  
|100154|DataSourceViewCollection|  
|100155|PerspectiveCollection|  
  
  
