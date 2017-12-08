---
title: "컬렉션 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- collections [Analysis Services Scripting Language]
- Analysis Services Scripting Language, collections
- ASSL, collections
ms.assetid: 072b8c6b-1550-4cab-ae64-ba0e3e60b059
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 68be246ab77c93a910a4d37b40808a42adecb8ae
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="collections-assl"></a>컬렉션(ASSL)
  이 참조 섹션에서는 ASSL(Analysis Services Scripting Language) 스키마에서 컬렉션으로 사용되는 각 요소에 대한 구문 및 사용 정보를 제공합니다.  
  
 ASSL 스키마는 개발자의 관점에서 XML 요소만 포함 하지만이 섹션에 설명 된 요소에 해당 개체의 컬렉션 등의 **차원** 및 **큐브** 컬렉션입니다.  
  
 컬렉션은 대부분 컬렉션 복수 명사가 있는 컬렉션 개체 요소의 (예: **큐브**), 동일한 명사의 단 수에서로 지정 된 요소를 포함 하는 컬렉션 (예를 들어  **큐브**).  
  
 이러한 일반적인 규칙을 따르지 않는 스키마도 있습니다. 예를 들어는 **ClassifiedColumns** 컬렉션에 포함 되어 **ClassifiedColumnID** 요소입니다.  
  
 또한 개체가 아니라 개체 속성에 해당하는 요소를 포함하는 컬렉션도 있습니다. 예를 들어는 **별칭** 컬렉션에 포함 되어 **별칭** 속성, 각각은 간단한 문자열 값입니다.  
  
|요소|Description|  
|-------------|-----------------|  
|[Accounts 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)|에 정의 된 계정 유형의 컬렉션을 포함 한 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[Actions 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/actions-element-assl.md)|에 대 한 작업의 컬렉션을 포함 한 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 또는 [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소입니다.|  
|[AggregationDesigns 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/aggregationdesigns-element-assl.md)|데이터베이스의 여러 파티션에서 공유할 수 있는 집계 디자인의 컬렉션을 포함합니다.|  
|[AggregationInstances 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md)|에 정의 된 집계 인스턴스의 컬렉션을 포함 한 [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md) 요소입니다.|  
|[Aggregations 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/aggregations-element-assl.md)|에 대해 정의 된 집계의 컬렉션을 포함 한 [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md) 요소입니다.|  
|[AlgorithmParameters 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/algorithmparameters-element-assl.md)|사용 하는 알고리즘에 대 한 매개 변수 컬렉션을 포함 한 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) 요소입니다.|  
|[Aliases 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/aliases-element-assl.md)|컬렉션을 포함 [별칭](../../../analysis-services/scripting/properties/alias-element-assl.md) 와 관련 된 요소는 [계정](../../../analysis-services/scripting/objects/account-element-assl.md) 요소|  
|[AllMemberTranslations 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/allmembertranslations-element-assl.md)|컬렉션을 포함 [번역](../../../analysis-services/scripting/objects/translation-element-assl.md) 요소에 있는 All 멤버의 캡션에 대 한 [계층](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) 요소입니다.|  
|[Annotations 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/annotations-element-assl.md)|컬렉션을 포함 [주석](../../../analysis-services/scripting/objects/annotation-element-assl.md) 부모 요소와 관련 된 요소입니다.|  
|[Assemblies 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)|컬렉션을 포함 [어셈블리](../../../analysis-services/scripting/objects/assembly-element-assl.md) 와 관련 된 요소는 [서버](../../../analysis-services/scripting/objects/server-element-assl.md) 요소 또는 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[AttributeAllMemberTranslations 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributeallmembertranslations-element-assl.md)|차원에 있는 All 멤버의 캡션에 대한 번역의 컬렉션을 포함합니다.|  
|[AttributePermissions 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)|개인에 대 한 특성 권한의 컬렉션을 포함 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 요소의 특정 차원에는 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.|  
|[AttributeRelationships 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributerelationships-element-assl.md)|컬렉션을 포함 [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md) 특성에 대 한 요소입니다.|  
|[Attributes 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)|연결된 차원에 대한 특성의 컬렉션을 포함합니다.|  
|[Blocks 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)|이진 내용을 나타내는 이진 데이터 블록의 컬렉션을 포함 한 [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) 요소입니다.|  
|[CalculationProperties 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)|컬렉션을 포함 [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md) 와 관련 된 요소는 [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) 요소입니다.|  
|[Calculations 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/calculations-element-assl.md)|컬렉션을 포함 [PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md) 와 관련 된 요소는 [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소입니다.|  
|[CellPermissions 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/cellpermissions-element-assl.md)|연결 된 셀에 대 한 사용 권한 컬렉션을 포함 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.|  
|[ClassifiedColumns 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/classifiedcolumns-element-assl.md)|분류 되는 관련 열의 컬렉션을 포함 된 [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md) 요소입니다.|  
|[Columns 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)|부모 요소와 연결된 열의 컬렉션을 포함합니다.|  
|[Commands 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/commands-element-assl.md)|[MdxScript](../../../analysis-services/scripting/objects/command-element-assl.md) 요소와 연결된 [Command](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) 요소의 컬렉션을 포함합니다.|  
|[CubePermissions 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/cubepermissions-element-assl.md)|에 적용 가능한 권한 컬렉션을 포함 한 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.|  
|[Cubes 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/cubes-element-assl.md)|컬렉션을 포함 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 와 관련 된 요소는 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[DatabasePermissions 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/databasepermissions-element-assl.md)|컬렉션을 포함 [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md) 와 관련 된 요소는 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[Databases 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/databases-element-assl.md)|컬렉션을 포함 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 와 관련 된 요소는 [서버](../../../analysis-services/scripting/objects/server-element-assl.md) 요소입니다.|  
|[DataSources 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/datasources-element-assl.md)|컬렉션을 포함 [DataSourcePermission](../../../analysis-services/scripting/objects/datasourcepermission-element-assl.md) 와 관련 된 요소는 [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) 데이터 형식입니다.|  
|[DataSourcePermissions 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/datasourcepermissions-element-assl.md)|컬렉션을 포함 [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) 와 관련 된 요소는 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[DataSourceViews 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/datasourceviews-element-assl.md)|컬렉션을 포함 [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md) 와 관련 된 요소는 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[DimensionPermissions 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/dimensionpermissions-element-assl.md)|에 적용 가능한 권한 컬렉션을 포함 한 [차원](../../../analysis-services/scripting/objects/dimension-element-assl.md) 요소 또는 [CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md) 요소입니다.|  
|[Dimensions 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/dimensions-element-assl.md)|부모 요소와 연결된 차원의 컬렉션을 포함합니다.|  
|[Events 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/events-element-assl.md)|로 캡처할 Event 요소의 컬렉션을 정의 [추적](../../../analysis-services/scripting/objects/trace-element-assl.md)합니다.|  
|[Files 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/files-element-assl.md)|컬렉션을 포함 [파일](../../../analysis-services/scripting/objects/file-element-assl.md) 구성 하는 요소는 [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) 요소입니다.|  
|[ForeignKeyColumns 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/foreignkeycolumns-element-assl.md)|관계형 데이터 원본에 대한 부모 테이블로의 조인을 식별하는 열의 컬렉션을 포함합니다.|  
|[Groups 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/groups-element-assl.md)|특성에 바인딩되는 멤버 그룹의 컬렉션을 포함합니다.|  
|[Hierarchies 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)|컬렉션을 포함 [계층](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) 부모 요소와 관련 된 요소입니다.|  
|[IncrementalProcessingNotifications 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/incrementalprocessingnotifications-element-assl.md)|컬렉션을 포함 [IncrementalProcessingNotification](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md) 정보를 제공 하는 요소는 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 의 진행 상태를 확인 하기 위해 실행할 쿼리에 대 한 요소 증분 처리 합니다.|  
|[KeyColumns 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)|컬렉션을 포함 [KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) 부모 개체에 대 한 요소 정의 합니다.|  
|[Kpis 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/kpis-element-assl.md)|컬렉션을 포함 [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) 부모 요소와 관련 된 요소입니다.|  
|[Levels 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/levels-element-assl.md)|컬렉션을 포함 [수준](../../../analysis-services/scripting/objects/level-element-assl.md) 의 요소는 [계층](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) 요소입니다.|  
|[MdxScripts 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)|컬렉션을 포함 [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) 와 관련 된 요소는 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.|  
|[MeasureGroups 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/measuregroups-element-assl.md)|컬렉션을 포함 [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) 부모 요소와 관련 된 요소입니다.|  
|[Measures 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/measures-element-assl.md)|컬렉션을 포함 [측정값](../../../analysis-services/scripting/objects/measure-element-assl.md) 부모 요소와 관련 된 요소입니다.|  
|[Members 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/members-element-assl.md)|부모 요소에 있는 [Member](../../../analysis-services/scripting/objects/member-element-assl.md) 요소의 컬렉션을 포함합니다.|  
|[MiningModelPermissions 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/miningmodelpermissions-element-assl.md)|에 대 한 권한 컬렉션을 포함 한 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) 요소입니다.|  
|[MiningModels 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/miningmodels-element-assl.md)|컬렉션을 포함 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) 와 관련 된 요소는 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)합니다.|  
|[MiningStructurePermissions 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)|에 대 한 권한 컬렉션을 포함 한 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 요소입니다.|  
|[MiningStructures 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/miningstructures-element-assl.md)|컬렉션을 포함 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 의 요소는 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[ModelingFlags 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/modelingflags-element-assl.md)|컬렉션을 포함 [ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md) 의 열에 대 한 요소는 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 또는 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)합니다.|  
|[NamingTemplateTranslations 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md)|에 대 한 지역화 된 번역의 컬렉션을 제공 된 [NamingTemplate](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md) 부모 [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)합니다.|  
|[Partitions 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/partitions-element-assl.md)|컬렉션을 포함 [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md) 에서 사용 되는 요소는 [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) 요소나의-라인을 구성 하는 파티션 바인딩의 컬렉션을 [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)요소입니다.|  
|[Perspectives 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/perspectives-element-assl.md)|컬렉션을 포함 [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md) 와 관련 된 요소는 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.|  
|[QueryNotifications 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/querynotifications-element-assl.md)|컬렉션을 포함 [QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md) 정보를 제공 하는 요소는 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 데이터 원본이 수정 되었는지 여부를 확인 하기 위해 실행할 쿼리에 대 한 요소입니다.|  
|[ReportFormatParameters 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/reportformatparameters-element-assl.md)|[ReportAction](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md) 요소에 대한 [ReportFormatParameter](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) 요소의 컬렉션을 포함합니다.|  
|[ReportParameters 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/reportparameters-element-assl.md)|컬렉션을 포함 [ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md) 에 대 한 요소는 [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) 요소입니다.|  
|[Roles 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/roles-element-assl.md)|부모 요소 아래에 정의된 [Role](../../../analysis-services/scripting/objects/role-element-assl.md) 요소의 컬렉션을 포함합니다.|  
|[ServerProperties 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)|컬렉션을 포함 [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) 와 관련 된 요소는 [서버](../../../analysis-services/scripting/objects/server-element-assl.md) 요소입니다.|  
|[TableNotifications 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/tablenotifications-element-assl.md)|컬렉션을 포함 [TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md) 에 대 한 정보를 제공 하는 요소는 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 테이블 또는 수정 된 데이터 원본 뷰에 대 한 요소입니다.|  
|[Traces 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/traces-element-assl.md)|[Server](../../../analysis-services/scripting/objects/trace-element-assl.md) 요소와 연결된 [Trace](../../../analysis-services/scripting/objects/server-element-assl.md) 요소의 컬렉션을 포함합니다.|  
|[Translations 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/translations-element-assl.md)|컬렉션을 포함 [번역](../../../analysis-services/scripting/objects/translation-element-assl.md) 부모 요소와 관련 된 요소입니다.|  
|[UnknownMemberTranslations 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/unknownmembertranslations-element-assl.md)|캡션에 대 한 번역의 컬렉션을 포함 된 [UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md) 차원의 요소입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services Scripting Language XML 요소 계층 &#40; ASSL &#41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
