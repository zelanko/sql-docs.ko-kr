---
title: Analysis Services Scripting Language XML 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Analysis Services Scripting Language XML Data Types
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ASSL, data types
- Analysis Services Scripting Language, data types
- data types [Analysis Services Scripting Language]
ms.assetid: 8e527916-932e-48ec-9010-f22cd4b721e2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f5ff2f0989aa2c88a69351d698c847ca6e835285
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48179253"
---
# <a name="analysis-services-scripting-language-xml-data-types-assl"></a>ASSL(Analysis Services Scripting Language) XML 데이터 형식
  이 참조 섹션에서는 ASSL(Analysis Services Scripting Language) 스키마에서 유형으로 사용되는 각 요소에 대한 구문 및 사용 정보를 제공합니다.  
  
 ASSL 스키마는 XML 요소만 포함하지만 이 섹션에 설명된 요소는 개발자의 관점에서 볼 때 `Binding` 및 `Permission`과 같은 유형에 해당합니다. 이러한 유형은 다른 개체의 자식 요소 및 속성을 정의하는 데 사용됩니다.  
  
 개체 요소와 같이 유형 요소는 ASSL 스키마에서 리프 수준 요소가 아니지만 자식 요소 및 개체 속성에 해당하는 요소를 갖습니다.  
  
 그러나 유형 요소 나타나지 않으며 정의 하거나 설명 하는 스크립트에서 요소로 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체입니다. 대신 일반적으로 `type` 또는 `xsi:type`을 사용하여 XML 스키마 인스턴스 스키마의 `xs:type` 특성으로 지정하는 다른 개체 요소의 유형으로 나타납니다. `<Assembly xsi:type="ClrAssembly">...</Assembly>`) 을 입력합니다.  
  
 다른 유형에서 파생되는 유형도 있습니다. 예를 들어 `CubeBinding` 유형은 부모 `Binding` 유형에서 파생됩니다.  
  
|요소|Description|  
|-------------|-----------------|  
|[Action 데이터 형식 &#40;ASSL&#41;](action-data-type-assl.md)|동작을 나타내는 추상 기본 데이터 형식을 정의 [큐브](../objects/cube-element-assl.md) 요소 또는 [관점](../objects/perspective-element-assl.md) 요소입니다.|  
|[AggregationAttribute 데이터 형식 &#40;ASSL&#41;](aggregationattribute-data-type-assl.md)|간의 연결을 나타내는 기본 데이터 형식을 정의 하는 [집계](../objects/aggregation-element-assl.md) 요소와 특성입니다.|  
|[AggregationDesignAttribute 데이터 형식 &#40;ASSL&#41;](aggregationdesignattribute-data-type-assl.md)|특성 간의 연결을 나타내는 기본 데이터 형식을 정의 및 [AggregationDesignDimension](dimension-data-type-assl.md) 요소입니다.|  
|[AggregationDesignDimension 데이터 형식 &#40;ASSL&#41;](dimension-data-type-assl.md)|큐브 차원 간의 관계를 나타내는 기본 데이터 형식을 정의 및 [AggregationDesign](../objects/aggregationdesign-element-assl.md) 요소입니다.|  
|[AggregationDimension 데이터 형식 &#40;ASSL&#41;](aggregationdimension-data-type-assl.md)|차원 간의 관계를 나타내는 기본 데이터 형식을 정의 및 [집계](../objects/aggregation-element-assl.md) 요소입니다.|  
|[AggregationInstanceAttribute 데이터 형식 &#40;ASSL&#41;](aggregationinstanceattribute-data-type-assl.md)|집계 인스턴스에서 사용하는 특성에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[AggregationInstanceCubeDimension 데이터 형식 &#40;ASSL&#41;](cubedimension-data-type-assl.md)|집계 인스턴스에서 사용하는 큐브 차원에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[AggregationInstanceMeasure 데이터 형식 &#40;ASSL&#41;](aggregationinstancemeasure-data-type-assl.md)|집계 인스턴스에서 사용하는 측정값에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[Assembly 데이터 형식 &#40;ASSL&#41;](assembly-data-type-assl.md)|나타내는 추상 기본 데이터 형식을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 어셈블리나와 연결 된 COM 동적 연결 라이브러리 (DLL)는 [Server](../objects/server-element-assl.md) 또는 [데이터베이스](../objects/database-element-assl.md) 요소입니다.|  
|[AttributeBinding 데이터 형식 &#40;ASSL&#41;](binding-data-type-assl.md)|에 대 한 바인딩을 나타내는 파생된 데이터 형식을 정의 [특성](../objects/attribute-element-assl.md) 요소입니다.|  
|[AttributeTranslation 데이터 형식 &#40;ASSL&#41;](translation-data-type-assl.md)|연결 된 번역을 나타내는 파생된 데이터 형식을 정의 [특성](../objects/attribute-element-assl.md) 요소|  
|[Binding 데이터 형식 &#40;ASSL&#41;](binding-data-type-assl.md)|한 개체의 데이터 또는 메타데이터가 바인딩된 개체의 데이터 또는 메타데이터에 종속되는 두 개체 간의 종속 관계를 나타내는 추상 기본 데이터 형식을 정의합니다.|  
|[ClrAssembly 데이터 형식 &#40;ASSL&#41;](clrassembly-data-type-assl.md)|나타내는 파생된 데이터 형식을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 와 연결 된 어셈블리를 [데이터베이스](../objects/database-element-assl.md) 또는 [Server](../objects/server-element-assl.md) 요소|  
|[ClrAssemblyFile 데이터 형식 &#40;ASSL&#41;](clrassemblyfile-data-type-assl.md)|구성 하는 파일 중 하나를 나타내는 기본 데이터 형식을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 어셈블리 ([ClrAssembly](clrassembly-data-type-assl.md) 요소).|  
|[ColumnBinding 데이터 형식 &#40;ASSL&#41;](columnbinding-data-type-assl.md)|데이터 원본 뷰의 열 바인딩을 나타내는 파생된 데이터 형식을 정의 [DataItem](dataitem-data-type-assl.md) 요소입니다.|  
|[ComAssembly 데이터 형식 &#40;ASSL&#41;](comassembly-data-type-assl.md)|연결 된 COM 라이브러리를 나타내는 파생된 데이터 형식을 정의 [Server](../objects/server-element-assl.md) 하거나 [데이터베이스](../objects/database-element-assl.md) 요소입니다.|  
|[CubeAttribute 데이터 형식 &#40;ASSL&#41;](cubeattribute-data-type-assl.md)|연결 된 특성을 나타내는 기본 데이터 형식을 정의 [큐브](../objects/cube-element-assl.md) 요소입니다.|  
|[CubeAttributeBinding 데이터 형식 &#40;ASSL&#41;](cubebinding-data-type-out-of-line-assl.md)|동작 또는 마이닝 구조 열에 대한 큐브 차원의 특성 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[CubeBinding 데이터 형식 &#40;아웃오브 라인&#41; &#40;ASSL&#41;](cubebinding-data-type-out-of-line-assl.md)|간의 관계를 나타내는 기본 데이터 형식을 정의 [큐브](../objects/cube-element-assl.md) 요소와 [DataSource](../objects/datasource-element-assl.md) 요소입니다.|  
|[CubeDimension 데이터 형식 &#40;ASSL&#41;](cubedimension-data-type-assl.md)|차원과 큐브 간의 관계를 나타내는 기본 데이터 형식을 정의합니다.|  
|[CubeDimensionBinding 데이터 형식 &#40;ASSL&#41;](dimensionbinding-data-type-assl.md)|바인딩을 나타내는 파생된 데이터 형식을 정의 [차원](../objects/dimension-element-assl.md)를 [측정값](../objects/measure-element-assl.md), 또는 [MiningModel](../objects/miningmodel-element-assl.md) 큐브 차원에 대 한 요소입니다.|  
|[CubeDimensionPermission 데이터 형식 &#40;ASSL&#41;](permission-data-type-assl.md)|큐브의 특정 차원에서 단일 역할에 대한 사용 권한을 나타내는 기본 데이터 형식을 정의합니다.|  
|[CubeHierarchy 데이터 형식 &#40;ASSL&#41;](hierarchy-data-type-assl.md)|에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [계층 구조](../objects/hierarchy-element-assl.md) 요소에는 [큐브](../objects/cube-element-assl.md) 요소입니다.|  
|[DataBlock 데이터 형식 &#40;ASSL&#41;](datablock-data-type-assl.md)|이진 내용을 저장 하는 데 사용 되는 데이터 블록의 컬렉션을 나타내는 기본 데이터 형식을 정의 [ClrAssemblyFile](clrassemblyfile-data-type-assl.md) 요소입니다.|  
|[DataItem 데이터 형식 &#40;ASSL&#41;](dataitem-data-type-assl.md)|열 또는 특성과 같은 데이터 항목의 데이터 관련 특성을 나타내는 기본 데이터 형식을 정의합니다.|  
|[DataMiningMeasureGroupDimension 데이터 형식 &#40;ASSL&#41;](measuregroupdimension-data-type-assl.md)|측정값 그룹과 데이터 마이닝 차원 간의 관계를 나타내는 파생 데이터 형식을 정의합니다.|  
|[DataSource 데이터 형식 &#40;ASSL&#41;](datasource-data-type-assl.md)|데이터 원본을 나타내는 추상 기본 데이터 형식을 정의 [데이터베이스](../objects/database-element-assl.md) 요소입니다.|  
|[DataSourceViewBinding 데이터 형식 &#40;ASSL&#41;](datasourceviewbinding-data-type-assl.md)|데이터 원본 뷰와 부모 요소 간의 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[DegenerateMeasureGroupDimension 데이터 형식 &#40;ASSL&#41;](degeneratemeasuregroupdimension-data-type-assl.md)|중복 제거 차원(팩트 차원)과 측정값 그룹 간의 관계를 나타내는 파생 데이터 형식을 정의합니다.|  
|[차원 데이터 유형 &#40;ASSL&#41;](dimension-data-type-assl.md)|데이터베이스 차원을 나타내는 기본 데이터 형식을 정의합니다.|  
|[DimensionAttribute 데이터 형식 &#40;ASSL&#41;](dimensionattribute-data-type-assl.md)|차원의 특성을 나타내는 기본 데이터 형식을 정의합니다.|  
|[DimensionBinding 데이터 형식 &#40;ASSL&#41;](dimensionbinding-data-type-assl.md)|데이터 원본 간의 바인딩을 나타내는 파생된 데이터 형식을 정의 및 [차원](../objects/dimension-element-assl.md) 요소입니다.|  
|[DimensionPermission 데이터 형식 &#40;ASSL&#41;](permission-data-type-assl.md)|데이터베이스 차원에 할당된 사용 권한을 나타내는 파생 데이터 형식을 정의합니다.|  
|[DrillThroughAction 데이터 형식 &#40;ASSL&#41;](drillthroughaction-data-type-assl.md)|드릴스루 동작을 나타내는 파생 데이터 형식을 정의합니다.|  
|[DSVTableBinding 데이터 형식 &#40;ASSL&#41;](tablebinding-data-type-assl.md)|테이블 간의 바인딩을 나타내는 파생된 데이터 형식을 정의 및 [DataSourceView](../objects/datasourceview-element-assl.md) 요소입니다.|  
|[EventColumn 데이터 형식 &#40;ASSL&#41;](eventcolumn-data-type-assl.md)|캡처할 정보 열을 나타내는 기본 데이터 형식을 정의 [이벤트](../objects/event-element-assl.md) 일환으로 요소를 [추적](../objects/trace-element-assl.md) 요소입니다.|  
|[Hierarchy 데이터 형식 &#40;ASSL&#41;](hierarchy-data-type-assl.md)|차원의 계층을 나타내는 기본 데이터 형식을 정의합니다.|  
|[ImpersonationInfo 데이터 형식 &#40;ASSL&#41;](impersonationinfo-data-type-assl.md)|사용자 가장에 사용된 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[IncrementalProcessingNotification 데이터 형식 &#40;ASSL&#41;](incrementalprocessingnotification-data-type-assl.md)|에 대 한 정보를 나타내는 파생된 데이터 형식을 정의 합니다 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 증분 처리의 진행률을 확인 하기 위해 실행할 쿼리에 대 한 요소입니다.|  
|[InheritedBinding 데이터 형식 &#40;ASSL&#41;](inheritedbinding-data-type-assl.md)|함을 나타내는 파생된 데이터 형식을 정의 [MeasureGroupAttribute](measuregroupattribute-data-type-assl.md) 요소가 특성에서 해당 바인딩을 상속 합니다.|  
|[ManyToManyMeasureGroupDimension 데이터 형식 &#40;ASSL&#41;](manytomanymeasuregroupdimension-data-type-assl.md)|다 대 다 차원과 측정값 그룹 간의 관계를 나타내는 파생 데이터 형식을 정의합니다.|  
|[MeasureBinding 데이터 형식 &#40;ASSL&#41;](measurebinding-data-type-assl.md)|부모 요소에 대한 측정값의 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[Measuregroupattribute _ 데이터 형식 &#40;ASSL&#41;](measuregroupattribute-data-type-assl.md)|특성과 측정값 그룹 간의 관계를 나타내는 기본 데이터 형식을 정의합니다.|  
|[MeasureGroupBinding 데이터 형식 &#40;ASSL&#41;](measuregroupbinding-data-type-assl.md)|에 대 한 바인딩을 나타내는 파생된 데이터 형식을 정의 [MeasureGroup](../objects/group-element-assl.md) 요소입니다.|  
|[MeasureGroupBinding 데이터 형식 &#40;아웃오브 라인&#41; &#40;ASSL&#41;](measuregroupbinding-data-type-out-of-line-assl.md)|측정값 그룹에 대한 바인딩을 나타내는 기본 데이터 형식을 정의합니다.|  
|[MeasureGroupDimension 데이터 형식 &#40;ASSL&#41;](measuregroupdimension-data-type-assl.md)|차원과 측정값 그룹 간의 관계를 나타내는 추상 기본 데이터 형식을 정의합니다.|  
|[MeasureGroupDimensionBinding 데이터 형식 &#40;ASSL&#41;](measuregroupdimensionbinding-data-type-assl.md)|차원과 측정값 그룹 간의 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[MeasureGroupHierarchy 데이터 형식 &#40;ASSL&#41;](measuregrouphierarchy-data-type-assl.md)|측정값 그룹의 계층에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[MiningModelColumn 데이터 형식 &#40;ASSL&#41;](miningmodelcolumn-data-type-assl.md)|열에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [MiningModel](../objects/miningmodel-element-assl.md) 요소입니다.|  
|[MiningModelingFlag 데이터 형식 &#40;ASSL&#41;](miningmodelingflag-data-type-assl.md)|사용 가능한 모델링 플래그를 나타내는 기본 데이터 형식을 정의 [ModelingFlag](../objects/modelingflag-element-assl.md) 요소입니다.|  
|[MiningStructureColumn 데이터 형식 &#40;ASSL&#41;](miningstructurecolumn-data-type-assl.md)|열에 대 한 정보를 나타내는 추상 기본 데이터 형식을 정의 [MiningStructure](../objects/miningstructure-element-assl.md) 요소입니다.|  
|[OlapDataSource 데이터 형식 &#40;ASSL&#41;](olapdatasource-data-type-assl.md)|다차원 나타내는 파생된 데이터 형식을 정의 [DataSource](../objects/datasource-element-assl.md) 요소입니다.|  
|[PartitionBinding 데이터 형식 &#40;ASSL&#41;](partitionbinding-data-type-assl.md)|에 대 한 바인딩을 나타내는 파생된 데이터 형식을 정의 [파티션](../objects/partition-element-assl.md) 요소입니다.|  
|[Permission 데이터 형식 &#40;ASSL&#41;](permission-data-type-assl.md)|개별 사용 권한에 대한 정보를 나타내는 추상 기본 데이터 형식을 정의합니다.|  
|[PerspectiveAction 데이터 형식 &#40;ASSL&#41;](perspectiveaction-data-type-assl.md)|동작에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [관점](../objects/perspective-element-assl.md) 요소입니다.|  
|[PerspectiveAttribute 데이터 형식 &#40;ASSL&#41;](perspectiveattribute-data-type-assl.md)|특성에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [PerspectiveDimension](perspectivedimension-data-type-assl.md) 요소입니다.|  
|[PerspectiveCalculation 데이터 형식 &#40;ASSL&#41;](perspectivecalculation-data-type-assl.md)|계산 간의 관계를 나타내는 기본 데이터 형식을 정의 및 [관점](../objects/perspective-element-assl.md) 요소입니다.|  
|[PerspectiveDimension 데이터 형식 &#40;ASSL&#41;](perspectivedimension-data-type-assl.md)|큐브 뷰의 차원에 대한 정보를 나타내는 기본 데이터 형식을 정의합니다.|  
|[PerspectiveHierarchy 데이터 형식 &#40;ASSL&#41;](perspectivehierarchy-data-type-assl.md)|계층에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [PerspectiveDimension](perspectivedimension-data-type-assl.md) 요소입니다.|  
|[PerspectiveKpi 데이터 형식 &#40;ASSL&#41;](perspectivekpi-data-type-assl.md)|핵심 성과 지표 (KPI)에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [관점](../objects/perspective-element-assl.md) 요소입니다.|  
|[PerspectiveMeasure 데이터 형식 &#40;ASSL&#41;](perspectivemeasure-data-type-assl.md)|측정값에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [PerspectiveMeasureGroup](perspectivemeasuregroup-data-type-assl.md) 요소입니다.|  
|[PerspectiveMeasureGroup 데이터 형식 &#40;ASSL&#41;](perspectivemeasuregroup-data-type-assl.md)|측정값 그룹에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [관점](../objects/perspective-element-assl.md) 요소입니다.|  
|[ProactiveCachingBinding 데이터 형식 &#40;ASSL&#41;](proactivecachingbinding-data-type-assl.md)|정보를 나타내는 추상 파생된 데이터 형식을 정의 합니다 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 캐시를 다시 작성 해야 하는 데이터 원본 변경 내용 또는 다시 작성 프로세스의 상태에 대 한 요소입니다.|  
|[ProactiveCachingIncrementalProcessingBinding 데이터 형식 &#40;ASSL&#41;](proactivecachingincrementalprocessingbinding-data-type-assl.md)|에 대 한 바인딩을 나타내는 파생된 데이터 형식을 정의 합니다 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 캐시를 다시 작성 프로세스의 상태에 대 한 요소입니다.|  
|[ProactiveCachingInheritedBinding 데이터 형식 &#40;ASSL&#41;](proactivecachinginheritedbinding-data-type-assl.md)|정보를 나타내는 파생된 데이터 형식을 정의 합니다 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 테이블 및 뷰의 캐시를 다시 작성 해야 하는 기존 데이터 바인딩을 통해 식별 되는 데이터 원본 변경 내용에 대 한 요소입니다.|  
|[ProactiveCachingObjectNotificationBinding 데이터 형식 &#40;ASSL&#41;](proactivecachingobjectnotificationbinding-data-type-assl.md)|정보를 나타내는 추상 파생된 데이터 형식을 정의 합니다 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 지정 된 테이블 및 뷰 또는 테이블 및 뷰의 기존 데이터 바인딩을 통해 식별 되는 데이터 원본 변경에 대 한 요소 캐시 재작성이 필요한입니다.|  
|[ProactiveCachingQueryBinding 데이터 형식 &#40;ASSL&#41;](querybinding-data-type-assl.md)|정보를 나타내는 파생된 데이터 형식을 정의 합니다 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 테이블 및 뷰의 캐시 재작성이 필요한 지정 된 쿼리의 실행을 통해 식별 된 데이터 원본 변경 내용에 대 한 요소입니다.|  
|[ProactiveCachingTablesBinding 데이터 형식 &#40;ASSL&#41;](proactivecachingtablesbinding-data-type-assl.md)|정보를 나타내는 파생된 데이터 형식을 정의 합니다 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 캐시를 다시 작성 해야 하는 뷰와 지정 된 테이블에서 데이터 원본 변경 내용에 대 한 요소입니다.|  
|[PushedDataSource 데이터 형식 &#40;ASSL&#41;](pusheddatasource-data-type-assl.md)|데이터 소스를 나타내는 기본 데이터 형식을 정의 (예는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 패키지) 데이터를 "밀어 넣는" 데를 [큐브](../objects/cube-element-assl.md) 요소.|  
|[QueryBinding 데이터 형식 &#40;ASSL&#41;](querybinding-data-type-assl.md)|연결을 나타내는 파생된 데이터 형식을 정의 [데이터 원본](../objects/datasource-element-assl.md) 요소를 [QueryDefinition](../properties/querydefinition-element-assl.md) 요소입니다.|  
|[ReferenceMeasureGroupDimension 데이터 형식 &#40;ASSL&#41;](referencemeasuregroupdimension-data-type-assl.md)|중간 차원을 통해 팩트 테이블과 간접적으로 관련된 차원을 나타내는 파생 데이터 형식을 정의합니다. 예를 들어 Sales 측정값 그룹은 Geography 차원을 참조할 수 있으며 이 차원은 Customer 차원을 통해 관련됩니다.|  
|[RegularMeasureGroupDimension 데이터 형식 &#40;ASSL&#41;](regularmeasuregroupdimension-data-type-assl.md)|차원과 측정값 그룹 간의 일반 관계를 나타내는 파생 데이터 형식을 정의합니다.|  
|[RelationalDataSource 데이터 형식 &#40;ASSL&#41;](relationaldatasource-data-type-assl.md)|나타내는 파생된 데이터 형식을 정의 [DataSource](../objects/datasource-element-assl.md) 요소는 관계형 데이터 원본을 기반으로 합니다.|  
|[ReportAction 데이터 형식 &#40;ASSL&#41;](reportaction-data-type-assl.md)|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서를 생성하는 동작을 나타내는 파생 데이터 형식을 정의합니다.|  
|[RowBinding 데이터 형식 &#40;ASSL&#41;](rowbinding-data-type-assl.md)|테이블의 행에 대 한 바인딩을 나타내는 파생된 데이터 형식을 정의 [DataSourceView](../objects/datasourceview-element-assl.md) 요소입니다.|  
|[ScalarMiningStructureColumn 데이터 형식 &#40;ASSL&#41;](scalarminingstructurecolumn-data-type-assl.md)|나타내는 파생된 데이터 형식을 정의 [MiningStructureColumn](miningstructurecolumn-data-type-assl.md) 와 연결 된 중첩된 테이블과 달리 스칼라 값을 포함 하는 요소는 [TableMiningStructureColumn](tableminingstructurecolumn-data-type-assl.md) 요소 중첩된 테이블이 들어 있는입니다.|  
|[StandardAction 데이터 형식 &#40;ASSL&#41;](standardaction-data-type-assl.md)|나타내는 파생된 데이터 형식을 정의 [동작](../objects/action-element-assl.md) 이외의 다른 요소를 [DrillThroughAction](drillthroughaction-data-type-assl.md) 요소 또는 [ReportAction](reportaction-data-type-assl.md) 요소입니다.|  
|[TableBinding 데이터 형식 &#40;ASSL&#41;](tablebinding-data-type-assl.md)|테이블에 대한 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[TableMiningStructureColumn 데이터 형식 &#40;ASSL&#41;](tableminingstructurecolumn-data-type-assl.md)|나타내는 파생된 데이터 형식을 정의 [MiningStructureColumn](miningstructurecolumn-data-type-assl.md) 연결 된 스칼라 값과 달리 중첩된 테이블을 포함 하는 요소는 [ScalarMiningStructureColumn](scalarminingstructurecolumn-data-type-assl.md) 요소 스칼라 값을 포함 합니다.|  
|[TabularBinding 데이터 형식 &#40;ASSL&#41;](tabularbinding-data-type-assl.md)|테이블 또는 큐브 차원과 같은 테이블 형식 항목에 대한 바인딩을 나타내는 추상 파생 데이터 형식을 정의합니다.|  
|[TimeAttributeBinding 데이터 형식 &#40;ASSL&#41;](timebinding-data-type-assl.md)|특성의 키 열과 같이 서버 시간 차원에서 생성된 데이터 항목에 대한 "자리 표시자" 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[TimeBinding 데이터 형식 &#40;ASSL&#41;](timebinding-data-type-assl.md)|기간에 대한 바인딩을 나타내는 파생 데이터 형식을 정의합니다.|  
|[Translation 데이터 형식 &#40;ASSL&#41;](translation-data-type-assl.md)|지역화된 번역을 나타내는 기본 데이터 형식을 정의합니다.|  
|[UserDefinedGroupBinding 데이터 형식 &#40;ASSL&#41;](userdefinedgroupbinding-data-type-assl.md)|특성에 대한 사용자 정의 그룹화를 나타내는 파생 데이터 형식을 정의합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 요소 계층 &#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
