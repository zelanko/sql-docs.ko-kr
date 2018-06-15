---
title: Analysis Services 스크립팅 언어 XML 데이터 형식 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c04f5ddfe7aa7f6fa7963d1e5fe8391089a8938
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036704"
---
# <a name="analysis-services-scripting-language-xml-data-types-assl"></a>ASSL(Analysis Services Scripting Language) XML 데이터 형식
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  이 참조 섹션에서는 ASSL(Analysis Services Scripting Language) 스키마에서 유형으로 사용되는 각 요소에 대한 구문 및 사용 정보를 제공합니다.  
  
 ASSL 스키마는 개발자의 관점에서 XML 요소만 포함 하지만이 섹션에 설명 된 요소에 해당 형식, 같은 **바인딩** 및 **권한**, 하는 데 사용 되는 자식 요소 및 다른 개체의 속성을 정의 합니다.  
  
 개체 요소와 같이 유형 요소는 ASSL 스키마에서 리프 수준 요소가 아니지만 자식 요소 및 개체 속성에 해당하는 요소를 갖습니다.  
  
 그러나 유형 요소 나타나지 정의 하거나 설명 하는 스크립트에서 요소로 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체입니다. 대신 일반적으로 사용 하 여 지정한 다른 개체 요소의 유형으로 표시 됩니다는 **형식** 특성을 사용 하 여 XML 스키마 인스턴스 스키마 **xsi: type** 또는 **xs:type**합니다. `<Assembly xsi:type="ClrAssembly">...</Assembly>`)을 입력합니다.  
  
 다른 유형에서 파생되는 유형도 있습니다. 예를 들어는 **CubeBinding** 부모에서 파생 되 **바인딩** 유형입니다.  
  
|요소|Description|  
|-------------|-----------------|  
|[Action 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소 또는 [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소의 동작을 나타내는 추상 기본 데이터 형식을 정의합니다.|  
|[AggregationAttribute 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/aggregationattribute-data-type-assl.md)|[Aggregation](../../../analysis-services/scripting/objects/aggregation-element-assl.md) 요소와 특성 간의 연결을 나타내는 기본 데이터 형식을 정의합니다.|  
|[AggregationDesignAttribute 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/aggregationdesignattribute-data-type-assl.md)|특성과 [AggregationDesignDimension](../../../analysis-services/scripting/data-type/aggregationdesigndimension-data-type-assl.md) 요소 간의 연결을 나타내는 기본 데이터 형식을 정의합니다.|  
|[AggregationDesignDimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/aggregationdesigndimension-data-type-assl.md)|큐브 차원과 [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md) 요소 간의 관계를 나타내는 기본 데이터 형식을 정의합니다.|  
|[AggregationDimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/aggregationdimension-data-type-assl.md)|차원과 [Aggregation](../../../analysis-services/scripting/objects/aggregation-element-assl.md) 요소 간의 관계를 나타내는 기본 데이터 형식을 정의합니다.|  
|[AggregationInstanceAttribute 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/aggregationinstanceattribute-data-type-assl.md)|집계 인스턴스에서 사용하는 특성에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[AggregationInstanceCubeDimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md)|집계 인스턴스에서 사용하는 큐브 차원에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[AggregationInstanceMeasure 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/aggregationinstancemeasure-data-type-assl.md)|집계 인스턴스에서 사용하는 측정값에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[Assembly 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/assembly-data-type-assl.md)|나타내는 추상 기본 데이터 형식을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 어셈블리 또는 연결 된 COM 동적 연결 라이브러리 (DLL)는 [서버](../../../analysis-services/scripting/objects/server-element-assl.md) 또는 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[AttributeBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) 요소에 대한 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[AttributeTranslation 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) 요소와 연결된 번역을 나타내는 파생 데이터 형식을 정의합니다.|  
|[Binding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|한 개체의 데이터 또는 메타데이터가 바인딩된 개체의 데이터 또는 메타데이터에 종속되는 두 개체 간의 종속 관계를 나타내는 추상 기본 데이터 형식을 정의합니다.|  
|[ClrAssembly 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)|나타내는 파생된 데이터 형식을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 와 연결 된 어셈블리는 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 또는 [서버](../../../analysis-services/scripting/objects/server-element-assl.md) 요소|  
|[ClrAssemblyFile 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)|구성 하는 파일 중 하나를 나타내는 기본 데이터 형식을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 어셈블리 ([ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) 요소).|  
|[ColumnBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md) 요소에 대한 데이터 원본 뷰의 열 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[ComAssembly 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)|[Server](../../../analysis-services/scripting/objects/server-element-assl.md) 또는 [Database](../../../analysis-services/scripting/objects/database-element-assl.md) 요소와 연결된 COM 라이브러리를 나타내는 파생 데이터 형식을 정의합니다.|  
|[CubeAttribute 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소와 연결된 특성을 나타내는 기본 데이터 형식을 정의합니다.|  
|[CubeAttributeBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)|동작 또는 마이닝 구조 열에 대한 큐브 차원의 특성 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[CubeBinding 데이터 형식 & #40; 아웃오브 라인 & #41; & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소와 [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) 요소 간의 관계를 나타내는 기본 데이터 형식을 정의합니다.|  
|[CubeDimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|차원과 큐브 간의 관계를 나타내는 기본 데이터 형식을 정의합니다.|  
|[CubeDimensionBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)|큐브 차원에 대한 [Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md), [Measure](../../../analysis-services/scripting/objects/measure-element-assl.md)또는 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) 요소의 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[CubeDimensionPermission 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)|큐브의 특정 차원에서 단일 역할에 대한 사용 권한을 나타내는 기본 데이터 형식을 정의합니다.|  
|[CubeHierarchy 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)|[Cube](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) 요소의 [Hierarchy](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[DataBlock 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)|[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) 요소의 이진 내용을 저장하는 데 사용되는 데이터 블록의 컬렉션을 나타내는 기본 데이터 형식을 정의합니다.|  
|[DataItem 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|열 또는 특성과 같은 데이터 항목의 데이터 관련 특성을 나타내는 기본 데이터 형식을 정의합니다.|  
|[DataMiningMeasureGroupDimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/dataminingmeasuregroupdimension-data-type-assl.md)|측정값 그룹과 데이터 마이닝 차원 간의 관계를 나타내는 파생 데이터 형식을 정의합니다.|  
|[DataSource 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|[Database](../../../analysis-services/scripting/objects/database-element-assl.md) 요소의 데이터 원본을 나타내는 추상 기본 데이터 형식을 정의합니다.|  
|[DataSourceViewBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)|데이터 원본 뷰와 부모 요소 간의 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[DegenerateMeasureGroupDimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/degeneratemeasuregroupdimension-data-type-assl.md)|중복 제거 차원(팩트 차원)과 측정값 그룹 간의 관계를 나타내는 파생 데이터 형식을 정의합니다.|  
|[Dimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/dimension-data-type-assl.md)|데이터베이스 차원을 나타내는 기본 데이터 형식을 정의합니다.|  
|[DimensionAttribute 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|차원의 특성을 나타내는 기본 데이터 형식을 정의합니다.|  
|[DimensionBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|데이터 원본과 [Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md) 요소 간의 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[DimensionPermission 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/dimensionpermission-data-type-assl.md)|데이터베이스 차원에 할당된 사용 권한을 나타내는 파생 데이터 형식을 정의합니다.|  
|[DrillThroughAction 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)|드릴스루 동작을 나타내는 파생 데이터 형식을 정의합니다.|  
|[DSVTableBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/dsvtablebinding-data-type-assl.md)|테이블과 [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md) 요소 간의 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[EventColumn 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|[Event](../../../analysis-services/scripting/objects/event-element-assl.md) 요소에 대해 [Trace](../../../analysis-services/scripting/objects/trace-element-assl.md) 요소의 일부로 캡처할 정보 열을 나타내는 기본 데이터 형식을 정의합니다.|  
|[Hierarchy 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/hierarchy-data-type-assl.md)|차원의 계층을 나타내는 기본 데이터 형식을 정의합니다.|  
|[ImpersonationInfo 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|사용자 가장에 사용된 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[IncrementalProcessingNotification 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/incrementalprocessingnotification-data-type-assl.md)|에 대 한 정보를 나타내는 파생된 데이터 형식을 정의 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 증분 처리의 진행률을 확인 하기 위해 실행할 쿼리에 대 한 요소입니다.|  
|[InheritedBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md) 요소가 특성에서 해당 바인딩을 상속함을 나타내는 파생 데이터 형식을 정의합니다.|  
|[ManyToManyMeasureGroupDimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md)|다 대 다 차원과 측정값 그룹 간의 관계를 나타내는 파생 데이터 형식을 정의합니다.|  
|[MeasureBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|부모 요소에 대한 측정값의 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[Measuregroupattribute _ 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|특성과 측정값 그룹 간의 관계를 나타내는 기본 데이터 형식을 정의합니다.|  
|[MeasureGroupBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) 요소에 대한 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[MeasureGroupBinding 데이터 형식 & #40; 아웃오브 라인 & #41; & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|측정값 그룹에 대한 바인딩을 나타내는 기본 데이터 형식을 정의합니다.|  
|[MeasureGroupDimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|차원과 측정값 그룹 간의 관계를 나타내는 추상 기본 데이터 형식을 정의합니다.|  
|[MeasureGroupDimensionBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|차원과 측정값 그룹 간의 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[MeasureGroupHierarchy 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/measuregrouphierarchy-data-type-assl.md)|측정값 그룹의 계층에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[MiningModelColumn 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) 요소의 열에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[MiningModelingFlag 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/miningmodelingflag-data-type-assl.md)|[ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md) 요소에서 사용 가능한 모델링 플래그를 나타내는 기본 데이터 형식을 정의합니다.|  
|[MiningStructureColumn 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 요소의 열에 대한 정보를 나타내는 추상 기본 데이터 형식을 정의합니다.|  
|[OlapDataSource 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/olapdatasource-data-type-assl.md)|다차원 [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) 요소를 나타내는 파생 데이터 형식을 정의합니다.|  
|[PartitionBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|에 대 한 바인딩을 나타내는 파생된 데이터 형식을 정의 [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md) 요소입니다.|  
|[Permission 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|개별 사용 권한에 대한 정보를 나타내는 추상 기본 데이터 형식을 정의합니다.|  
|[PerspectiveAction 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)|[Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소의 동작에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[PerspectiveAttribute 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)|[PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md) 요소의 특성에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[PerspectiveCalculation 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md)|계산과 [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소 간의 관계를 나타내는 기본 데이터 형식을 정의합니다.|  
|[PerspectiveDimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|큐브 뷰의 차원에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[PerspectiveHierarchy 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md)|[PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md) 요소의 계층에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[PerspectiveKpi 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/perspectivekpi-data-type-assl.md)|[Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소의 KPI(핵심 성과 지표)에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[PerspectiveMeasure 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/perspectivemeasure-data-type-assl.md)|[PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md) 요소의 측정값에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[PerspectiveMeasureGroup 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)|[Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소의 측정값 그룹에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[ProactiveCachingBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|캐시를 다시 작성해야 하는 데이터 원본 변경 내용이나 다시 작성 프로세스의 상태에 대한 정보를 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 요소에 나타내는 추상 파생 데이터 형식을 정의합니다.|  
|[ProactiveCachingIncrementalProcessingBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/proactivecachingincrementalprocessingbinding-data-type-assl.md)|캐시 다시 작성 프로세스의 상태에 대한 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 요소 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[ProactiveCachingInheritedBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/proactivecachinginheritedbinding-data-type-assl.md)|캐시를 다시 작성해야 하는 기존 데이터 바인딩을 통해 식별되는 테이블 및 뷰의 데이터 원본 변경 내용에 대한 정보를 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 요소에 나타내는 파생 데이터 형식을 정의합니다.|  
|[ProactiveCachingObjectNotificationBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)|지정된 테이블 및 뷰 또는 캐시를 다시 작성해야 하는 기존 데이터 바인딩을 통해 식별되는 테이블 및 뷰의 데이터 원본 변경 내용에 대한 정보를 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 요소에 나타내는 추상 파생 데이터 형식을 정의합니다.|  
|[ProactiveCachingQueryBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)|캐시를 다시 작성해야 하는 지정된 쿼리의 실행을 통해 식별되는 테이블 및 뷰의 데이터 원본 변경 내용에 대한 정보를 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 요소에 나타내는 파생 데이터 형식을 정의합니다.|  
|[ProactiveCachingTablesBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/proactivecachingtablesbinding-data-type-assl.md)|캐시를 다시 작성해야 하는 지정된 테이블 및 뷰의 데이터 원본 변경 내용에 대한 정보를 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 요소에 나타내는 파생 데이터 형식을 정의합니다.|  
|[PushedDataSource 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/pusheddatasource-data-type-assl.md)|데이터 소스를 나타내는 기본 데이터 형식을 정의 (같은 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 패키지) 데이터를 "밀어 넣는" 데는 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.|  
|[QueryBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/querybinding-data-type-assl.md)|[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) 요소와 [QueryDefinition](../../../analysis-services/scripting/properties/querydefinition-element-assl.md) 요소의 연결을 나타내는 파생 데이터 형식을 정의합니다.|  
|[ReferenceMeasureGroupDimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md)|중간 차원을 통해 팩트 테이블과 간접적으로 관련된 차원을 나타내는 파생 데이터 형식을 정의합니다. 예를 들어 Sales 측정값 그룹은 Geography 차원을 참조할 수 있으며 이 차원은 Customer 차원을 통해 관련됩니다.|  
|[RegularMeasureGroupDimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)|차원과 측정값 그룹 간의 일반 관계를 나타내는 파생 데이터 형식을 정의합니다.|  
|[RelationalDataSource 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/relationaldatasource-data-type-assl.md)|관계형 데이터 원본을 기반으로 [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) 요소를 나타내는 파생 데이터 형식을 정의합니다.|  
|[ReportAction 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서를 생성하는 동작을 나타내는 파생 데이터 형식을 정의합니다.|  
|[RowBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)|[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md) 요소의 테이블 행에 대한 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[ScalarMiningStructureColumn 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|중첩 테이블을 포함하는 [TableMiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md) 요소와 연결된 중첩 테이블과 달리 스칼라 값을 포함하는 [MiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md) 요소를 나타내는 파생 데이터 형식을 정의합니다.|  
|[StandardAction 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|[DrillThroughAction](../../../analysis-services/scripting/objects/action-element-assl.md) 요소 또는 [ReportAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md) 요소 이외의 모든 [Action](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) 요소를 나타내는 파생 데이터 형식을 정의합니다.|  
|[TableBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)|테이블에 대한 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[TableMiningStructureColumn 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|스칼라 값을 포함하는 [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md) 요소와 연결된 스칼라 값과 달리 중첩 테이블을 포함하는 [MiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md) 요소를 나타내는 파생 데이터 형식을 정의합니다.|  
|[TabularBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|테이블 또는 큐브 차원과 같은 테이블 형식 항목에 대한 바인딩을 나타내는 추상 파생 데이터 형식을 정의합니다.|  
|[TimeAttributeBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/timeattributebinding-data-type-assl.md)|특성의 키 열과 같이 서버 시간 차원에서 생성된 데이터 항목에 대한 "자리 표시자" 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[TimeBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|기간에 대한 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[Translation 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)|지역화된 번역을 나타내는 기본 데이터 형식을 정의합니다.|  
|[UserDefinedGroupBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|특성에 대한 사용자 정의 그룹화를 나타내는 파생 데이터 형식을 정의합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services Scripting Language XML 요소 계층 & #40; ASSL & #41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
