---
title: 컬렉션 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- collections [Analysis Services Scripting Language]
- Analysis Services Scripting Language, collections
- ASSL, collections
ms.assetid: 072b8c6b-1550-4cab-ae64-ba0e3e60b059
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f549a8d84f356b9315cdf3ec03ee41234e4dd0d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48199713"
---
# <a name="collections-assl"></a>컬렉션(ASSL)
  이 참조 섹션에서는 ASSL(Analysis Services Scripting Language) 스키마에서 컬렉션으로 사용되는 각 요소에 대한 구문 및 사용 정보를 제공합니다.  
  
 ASSL 스키마는 XML 요소만 포함하지만 이 섹션에 설명된 요소는 개발자의 관점에서 볼 때 `Dimensions` 및 `Cubes` 컬렉션과 같은 개체의 컬렉션에 해당합니다.  
  
 컬렉션은 대부분 개체 요소의 모음으로서 `Cubes`와 같은 하나의 복수 명사가 해당 컬렉션을 나타내며, `Cube`와 같이 동일한 이름의 단수 명사로 표시된 요소들로 구성됩니다.  
  
 이러한 일반적인 규칙을 따르지 않는 스키마도 있습니다. 예를 들어 `ClassifiedColumns` 컬렉션은 `ClassifiedColumnID` 요소를 포함합니다.  
  
 또한 개체가 아니라 개체 속성에 해당하는 요소를 포함하는 컬렉션도 있습니다. 예를 들어 `Aliases` 컬렉션은 각각이 단순 문자열 값인 `Alias` 속성을 포함합니다.  
  
|요소|Description|  
|-------------|-----------------|  
|[요소를 계정 &#40;ASSL&#41;](accounts-element-assl.md)|에 정의 된 계정 유형의 컬렉션을 포함 한 [데이터베이스](../objects/database-element-assl.md) 요소입니다.|  
|[Actions 요소 &#40;ASSL&#41;](actions-element-assl.md)|에 대 한 작업의 컬렉션을 포함 한 [큐브](../objects/cube-element-assl.md) 또는 [관점](../objects/perspective-element-assl.md) 요소입니다.|  
|[AggregationDesigns 요소 &#40;ASSL&#41;](aggregationdesigns-element-assl.md)|데이터베이스의 여러 파티션에서 공유할 수 있는 집계 디자인의 컬렉션을 포함합니다.|  
|[AggregationInstances 요소 &#40;ASSL&#41;](aggregationinstances-element-assl.md)|에 정의 된 집계 인스턴스의 컬렉션을 포함 한 [파티션](../objects/partition-element-assl.md) 요소입니다.|  
|[Aggregations 요소 &#40;ASSL&#41;](aggregations-element-assl.md)|에 대해 정의 된 집계의 컬렉션을 포함 한 [AggregationDesign](../objects/aggregationdesign-element-assl.md) 요소입니다.|  
|[AlgorithmParameters 요소 &#40;ASSL&#41;](algorithmparameters-element-assl.md)|사용 되는 알고리즘에 대 한 매개 변수 컬렉션을 포함 한 [MiningModel](../objects/miningmodel-element-assl.md) 요소입니다.|  
|[Aliases 요소 &#40;ASSL&#41;](aliases-element-assl.md)|컬렉션을 포함 [별칭](../properties/alias-element-assl.md) 와 관련 된 요소를 [계정](../objects/account-element-assl.md) 요소|  
|[AllMemberTranslations 요소 &#40;ASSL&#41;](translations-element-assl.md)|컬렉션을 포함 [번역](../objects/translation-element-assl.md) 의 모든 멤버의 캡션에 대 한 요소를 [계층](../objects/hierarchy-element-assl.md) 요소입니다.|  
|[Annotations 요소 &#40;ASSL&#41;](annotations-element-assl.md)|컬렉션을 포함 [주석](../objects/annotation-element-assl.md) 부모 요소와 관련 된 요소입니다.|  
|[Assemblies 요소 &#40;ASSL&#41;](assemblies-element-assl.md)|컬렉션을 포함 [어셈블리](../objects/assembly-element-assl.md) 와 관련 된 요소를 [Server](../objects/server-element-assl.md) 요소 또는 [데이터베이스](../objects/database-element-assl.md) 요소입니다.|  
|[AttributeAllMemberTranslations 요소 &#40;ASSL&#41;](attributeallmembertranslations-element-assl.md)|차원에 있는 All 멤버의 캡션에 대한 번역의 컬렉션을 포함합니다.|  
|[AttributePermissions 요소 &#40;ASSL&#41;](attributepermissions-element-assl.md)|개인에 대 한 특성 권한의 컬렉션을 포함 [역할](../objects/role-element-assl.md) 의 특정 차원에서 요소를 [큐브](../objects/cube-element-assl.md) 요소입니다.|  
|[AttributeRelationships 요소 &#40;ASSL&#41;](relationships-element-assl.md)|컬렉션을 포함 [AttributeRelationship](../objects/attributerelationship-element-assl.md) 특성에 대 한 요소입니다.|  
|[요소 특성 &#40;ASSL&#41;](attributes-element-assl.md)|연결된 차원에 대한 특성의 컬렉션을 포함합니다.|  
|[요소를 차단 &#40;ASSL&#41;](blocks-element-assl.md)|이진 내용을 나타내는 이진 데이터 블록의 컬렉션을 포함 한 [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md) 요소입니다.|  
|[CalculationProperties 요소 &#40;ASSL&#41;](calculationproperties-element-assl.md)|컬렉션을 포함 [CalculationProperty](../objects/calculationproperty-element-assl.md) 와 관련 된 요소를 [MdxScript](../objects/mdxscript-element-assl.md) 요소입니다.|  
|[Calculations 요소 &#40;ASSL&#41;](calculations-element-assl.md)|컬렉션을 포함 [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md) 와 관련 된 요소를 [관점](../objects/perspective-element-assl.md) 요소입니다.|  
|[CellPermissions 요소 &#40;ASSL&#41;](cellpermissions-element-assl.md)|연결 된 셀에 대 한 사용 권한의 컬렉션을 포함 [큐브](../objects/cube-element-assl.md) 요소입니다.|  
|[ClassifiedColumns 요소 &#40;ASSL&#41;](columns-element-assl.md)|분류 되는 관련 열의 컬렉션을 포함 합니다 [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) 요소입니다.|  
|[Columns 요소 &#40;ASSL&#41;](columns-element-assl.md)|부모 요소와 연결된 열의 컬렉션을 포함합니다.|  
|[요소는 명령 &#40;ASSL&#41;](commands-element-assl.md)|[MdxScript](../objects/command-element-assl.md) 요소와 연결된 [Command](../objects/mdxscript-element-assl.md) 요소의 컬렉션을 포함합니다.|  
|[CubePermissions 요소 &#40;ASSL&#41;](cubepermissions-element-assl.md)|에 적용 가능한 권한 컬렉션을 포함 한 [큐브](../objects/cube-element-assl.md) 요소입니다.|  
|[큐브 요소 &#40;ASSL&#41;](cubes-element-assl.md)|컬렉션을 포함 [큐브](../objects/cube-element-assl.md) 와 관련 된 요소를 [데이터베이스](../objects/database-element-assl.md) 요소입니다.|  
|[DatabasePermissions 요소 &#40;ASSL&#41;](databasepermissions-element-assl.md)|컬렉션을 포함 [DatabasePermission](../objects/databasepermission-element-assl.md) 와 관련 된 요소를 [데이터베이스](../objects/database-element-assl.md) 요소입니다.|  
|[Databases 요소 &#40;ASSL&#41;](databases-element-assl.md)|컬렉션을 포함 [데이터베이스](../objects/database-element-assl.md) 와 관련 된 요소를 [Server](../objects/server-element-assl.md) 요소입니다.|  
|[DataSources 요소 &#40;ASSL&#41;](datasources-element-assl.md)|컬렉션을 포함 [DataSourcePermission](../objects/datasourcepermission-element-assl.md) 와 관련 된 요소를 [DataSource](../data-type/datasource-data-type-assl.md) 데이터 형식입니다.|  
|[DataSourcePermissions 요소 &#40;ASSL&#41;](datasourcepermissions-element-assl.md)|컬렉션을 포함 [데이터 원본](../objects/datasource-element-assl.md) 와 관련 된 요소를 [데이터베이스](../objects/database-element-assl.md) 요소입니다.|  
|[DataSourceViews 요소 &#40;ASSL&#41;](datasourceviews-element-assl.md)|컬렉션을 포함 [DataSourceView](../objects/datasourceview-element-assl.md) 와 관련 된 요소를 [데이터베이스](../objects/database-element-assl.md) 요소입니다.|  
|[DimensionPermissions 요소 &#40;ASSL&#41;](dimensionpermissions-element-assl.md)|에 적용 가능한 권한 컬렉션을 포함 한 [차원](../objects/dimension-element-assl.md) 요소 또는 [CubePermission](../objects/cubepermission-element-assl.md) 요소입니다.|  
|[Dimensions 요소 &#40;ASSL&#41;](dimensions-element-assl.md)|부모 요소와 연결된 차원의 컬렉션을 포함합니다.|  
|[Events 요소 &#40;ASSL&#41;](events-element-assl.md)|가 캡처할 Event 요소의 컬렉션을 정의 [추적](../objects/trace-element-assl.md)합니다.|  
|[파일 요소 &#40;ASSL&#41;](files-element-assl.md)|컬렉션을 포함 [파일](../objects/file-element-assl.md) 구성 하는 요소는 [ClrAssembly](../data-type/assembly-data-type-assl.md) 요소입니다.|  
|[ForeignKeyColumns 요소 &#40;ASSL&#41;](keycolumns-element-assl.md)|관계형 데이터 원본에 대한 부모 테이블로의 조인을 식별하는 열의 컬렉션을 포함합니다.|  
|[Groups 요소 &#40;ASSL&#41;](groups-element-assl.md)|특성에 바인딩되는 멤버 그룹의 컬렉션을 포함합니다.|  
|[Hierarchies 요소 &#40;ASSL&#41;](hierarchies-element-assl.md)|컬렉션을 포함 [계층](../objects/hierarchy-element-assl.md) 부모 요소와 관련 된 요소입니다.|  
|[IncrementalProcessingNotifications 요소 &#40;ASSL&#41;](incrementalprocessingnotifications-element-assl.md)|컬렉션을 포함 [IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md) 정보를 제공 하는 요소는 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 의 진행률을 확인 하기 위해 실행할 쿼리에 대 한 요소 증분 처리 합니다.|  
|[KeyColumns 요소 &#40;ASSL&#41;](keycolumns-element-assl.md)|컬렉션을 포함 [KeyColumn](../objects/column-element-assl.md) 부모 개체에 대 한 요소를 정의 합니다.|  
|[Kpis 요소 &#40;ASSL&#41;](kpis-element-assl.md)|컬렉션을 포함 [Kpi](../objects/kpi-element-assl.md) 부모 요소와 관련 된 요소입니다.|  
|[요소 수준 &#40;ASSL&#41;](levels-element-assl.md)|컬렉션을 포함 [수준](../objects/level-element-assl.md) 의 요소를 [계층](../objects/hierarchy-element-assl.md) 요소입니다.|  
|[MdxScripts 요소 &#40;ASSL&#41;](mdxscripts-element-assl.md)|컬렉션을 포함 [MdxScript](../objects/mdxscript-element-assl.md) 와 관련 된 요소를 [큐브](../objects/cube-element-assl.md) 요소입니다.|  
|[MeasureGroups 요소 &#40;ASSL&#41;](measuregroups-element-assl.md)|컬렉션을 포함 [MeasureGroup](../objects/group-element-assl.md) 부모 요소와 관련 된 요소입니다.|  
|[요소를 측정 합니다. &#40;ASSL&#41;](measures-element-assl.md)|컬렉션을 포함 [측정값](../objects/measure-element-assl.md) 부모 요소와 관련 된 요소입니다.|  
|[Members 요소 &#40;ASSL&#41;](members-element-assl.md)|부모 요소에 있는 [Member](../objects/member-element-assl.md) 요소의 컬렉션을 포함합니다.|  
|[MiningModelPermissions 요소 &#40;ASSL&#41;](miningmodelpermissions-element-assl.md)|에 대 한 사용 권한의 컬렉션을 포함 한 [MiningModel](../objects/miningmodel-element-assl.md) 요소입니다.|  
|[MiningModels 요소 &#40;ASSL&#41;](miningmodels-element-assl.md)|컬렉션을 포함 [MiningModel](../objects/miningmodel-element-assl.md) 와 관련 된 요소를 [MiningStructure](../objects/miningstructure-element-assl.md)합니다.|  
|[MiningStructurePermissions 요소 &#40;ASSL&#41;](miningstructurepermissions-element-assl.md)|에 대 한 권한 컬렉션을 포함 한 [MiningStructure](../objects/miningstructure-element-assl.md) 요소입니다.|  
|[MiningStructures 요소 &#40;ASSL&#41;](miningstructures-element-assl.md)|컬렉션을 포함 [MiningStructure](../objects/miningstructure-element-assl.md) 의 요소를 [데이터베이스](../objects/database-element-assl.md) 요소입니다.|  
|[ModelingFlags 요소 &#40;ASSL&#41;](modelingflags-element-assl.md)|컬렉션을 포함 [ModelingFlag](../objects/modelingflag-element-assl.md) 의 열에 대 한 요소를 [MiningStructure](../objects/miningstructure-element-assl.md) 또는 [MiningModel](../objects/miningmodel-element-assl.md)합니다.|  
|[NamingTemplateTranslations 요소 &#40;ASSL&#41;](namingtemplatetranslations-element-assl.md)|지역화 된 번역의 컬렉션을 제공 합니다 [NamingTemplate](../properties/namingtemplate-element-assl.md) 부모 요소의 [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)합니다.|  
|[요소를 분할 &#40;ASSL&#41;](partitions-element-assl.md)|컬렉션을 포함 [파티션](../objects/partition-element-assl.md) 에서 사용 되는 요소는 [MeasureGroup](../objects/group-element-assl.md) 요소나는 아웃 아웃오브 라인을 구성 하는 파티션 바인딩의 컬렉션 [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)요소입니다.|  
|[Perspectives 요소 &#40;ASSL&#41;](perspectives-element-assl.md)|컬렉션을 포함 [관점](../objects/perspective-element-assl.md) 와 관련 된 요소를 [큐브](../objects/cube-element-assl.md) 요소입니다.|  
|[QueryNotifications 요소 &#40;ASSL&#41;](querynotifications-element-assl.md)|컬렉션을 포함 [QueryNotification](../objects/querynotification-element-assl.md) 정보를 제공 하는 요소는 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 데이터 원본이 수정 되었는지 여부를 확인 하기 위해 실행할 쿼리에 대 한 요소입니다.|  
|[ReportFormatParameters 요소 &#40;ASSL&#41;](reportformatparameters-element-assl.md)|[ReportAction](../objects/reportformatparameter-element-asl.md) 요소에 대한 [ReportFormatParameter](../data-type/action-data-type-assl.md) 요소의 컬렉션을 포함합니다.|  
|[ReportParameters 요소 &#40;ASSL&#41;](reportparameters-element-assl.md)|컬렉션을 포함 [ReportParameter](../objects/reportparameter-element-assl.md) 에 대 한 요소를 [ReportAction](../data-type/action-data-type-assl.md) 요소입니다.|  
|[Roles 요소 &#40;ASSL&#41;](roles-element-assl.md)|부모 요소 아래에 정의된 [Role](../objects/role-element-assl.md) 요소의 컬렉션을 포함합니다.|  
|[ServerProperties 요소 &#40;ASSL&#41;](serverproperties-element-assl.md)|컬렉션을 포함 [ServerProperty](../objects/serverproperty-element-assl.md) 와 관련 된 요소를 [Server](../objects/server-element-assl.md) 요소입니다.|  
|[TableNotifications 요소 &#40;ASSL&#41;](tablenotifications-element-assl.md)|컬렉션을 포함 [TableNotification](../objects/tablenotification-element-assl.md) 에 대 한 정보를 제공 하는 요소는 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 테이블이 나 수정 된 데이터 원본 뷰에 대 한 요소입니다.|  
|[요소를 추적 합니다. &#40;ASSL&#41;](traces-element-assl.md)|[Server](../objects/trace-element-assl.md) 요소와 연결된 [Trace](../objects/server-element-assl.md) 요소의 컬렉션을 포함합니다.|  
|[Translations 요소 &#40;ASSL&#41;](translations-element-assl.md)|컬렉션을 포함 [번역](../objects/translation-element-assl.md) 부모 요소와 관련 된 요소입니다.|  
|[UnknownMemberTranslations 요소 &#40;ASSL&#41;](unknownmembertranslations-element-assl.md)|캡션에 대 한 번역의 컬렉션을 포함 합니다 [UnknownMember](../properties/unknownmember-element-assl.md) 차원의 요소입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 요소 계층 &#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
