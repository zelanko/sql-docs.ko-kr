---
title: 속성 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- properties [Analysis Services Scripting Language]
- Analysis Services Scripting Language, properties
- ASSL, properties
ms.assetid: 9a38cdc9-a210-421a-90e9-6391876765fa
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 593d3c772375011264f5ceda56e41b910b140c31
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="properties-assl"></a>속성(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  이 참조 섹션에서는 ASSL(Analysis Services Scripting Language) 스키마에서 개체 속성으로 사용되는 각 요소에 대한 구문 및 사용 정보를 제공합니다.  
  
 ASSL 스키마는 XML 요소만 포함하지만 이 섹션에 설명된 요소는 개발자의 관점에서 볼 때 개체를 설명하는 속성에 해당합니다.  
  
 속성은 ASSL 스키마에서 리프 수준 요소이며 자식 요소 또는 자체 속성에 해당하는 요소를 갖지 않습니다.  
  
 속성으로 나타날 수 있는 스키마의 리프 수준 요소가 개체 유형이어서 개체로 분류되는 경우도 있습니다. 예를 들어는 **소스** 의 **차원** 형식의 개체는 **DimensionBinding**합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|요소|Description|  
|-------------|-----------------|  
|[요소에 액세스 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/access-element-assl.md)|에 지정 된 액세스 수준을 나타냅니다는 [CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md) 요소입니다.|  
|[요소 계정 &#40;ImpersonationInfo&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/account-element-impersonationinfo-assl.md)|에 대 한 사용자 계정의 이름을 포함 된 [ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md) 데이터 형식입니다.|  
|[AccountType 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/accounttype-element-assl.md)|에 정의 된 계정 유형의 이름을 포함 한 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[ActionID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/actionid-element-assl.md)|이름을 포함 한 [작업](../../../analysis-services/scripting/objects/action-element-assl.md) 에 정의 된 요소는 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소에서 사용할 수 있는 [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소도는 [PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md) 요소입니다.|  
|[Administer 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/administer-element-assl.md)|연결 된 사용 권한 관리 권한이 포함 되는지 여부를 나타냅니다는 **데이터베이스** 요소입니다.|  
|[AggregateFunction 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md)|사용 하는 집계 함수의 유형을 정의 [측정값](../../../analysis-services/scripting/objects/measure-element-assl.md) 요소입니다.|  
|[AggregationDesignID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationdesignid-element-assl.md)|식별 된 [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md) 요소와 연관 된는 [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md) 요소입니다.|  
|[AggregationFunction 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationfunction-element-assl.md)|계정 유형에 사용할 집계 함수를 포함합니다.|  
|[AggregationID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationid-element-assl.md)|집계 정의 식별 하는 **AggregationDesign** 요소를 집계 인스턴스를 만드는 데 사용 합니다.|  
|[AggregationInstanceSource 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationinstancesource-element-assl.md)|소스에 바인딩된 사용자 정의 집계 인스턴스의 데이터를 식별 한 **파티션** 요소입니다.|  
|[AggregationPrefix 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md)|관련 부모 요소 전체에서 집계 이름에 사용할 공통 접두사를 정의합니다.|  
|[AggregationStorage 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationstorage-element-assl.md)|집계 저장 방법을 식별합니다.|  
|[AggregationType 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationtype-element-assl.md)|저장 되는 집계 유형을 정의 **파티션** 요소입니다.|  
|[AggregationUsage 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md)|컨트롤 어떻게에서 집계 디자이너로 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 집계를 디자인 합니다.|  
|[Algorithm 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/algorithm-element-assl.md)|사용 되는 알고리즘 정의 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) 요소입니다.|  
|[Alias 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/alias-element-assl.md)|에 대 한 별칭을 정의 [계정](../../../analysis-services/scripting/objects/account-element-assl.md) 요소입니다.|  
|[AllMemberAggregationUsage 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/allmemberaggregationusage-element-assl.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 집계 디자이너로 집계를 디자인하는 방식을 제어합니다.|  
|[AllMemberName 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/allmembername-element-assl.md)|모든 구성원에 대 한 캡션을 기본 언어로 포함 한 [계층](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) 요소입니다.|  
|[AllowBrowsing 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/allowbrowsing-element-assl.md)|정의 여부의 멤버는 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 요소에 대 한 찾아보기 권한이 **MiningModel** 요소입니다.|  
|[AllowDrillThrough 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)|부모 요소에서 드릴스루가 허용되는지 여부를 결정합니다.|  
|[AllowDuplicateNames 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/allowduplicatenames-element-assl.md)|중복 이름이 허용 되는지 여부를 결정 한 **계층** 요소입니다.|  
|[AllowedSet 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/allowedset-element-assl.md)|에 대 한 허용 된 권한 집합을 정의 하는 집합 식을 포함 한 **역할** 특성에 대 한 요소입니다.|  
|[Application 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/application-element-assl.md)|와 연결 된 응용 프로그램을 식별 한 **동작** 요소입니다.|  
|[AssociatedMeasureGroupID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/associatedmeasuregroupid-element-assl.md)|식별자 (ID)가 포함 된 [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) 요소와 연관 된는 [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md) 요소 또는 [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) 요소입니다.|  
|[AttributeAllMemberName 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributeallmembername-element-assl.md)|차원의 All 멤버에 대한 캡션을 기본 언어로 포함합니다.|  
|[AttributeHierarchyDisplayFolder 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchydisplayfolder-element-assl.md)|연관된 특성 계층을 표시할 폴더를 식별합니다.|  
|[AttributeHierarchyEnabled 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)|특성에 대한 특성 계층을 설정할지 여부를 결정합니다.|  
|[AttributeHierarchyOptimizedState 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md)|특성 계층에 적용되는 최적화 수준을 결정합니다.|  
|[AttributeHierarchyOrdered 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchyordered-element-assl.md)|연관된 특성 계층의 정렬 여부를 결정합니다.|  
|[AttributeHierarchyVisible 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md)|클라이언트 응용 프로그램에서 특성 계층을 볼 수 있는지 여부를 결정합니다.|  
|[AttributeID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributeid-element-assl.md)|부모 요소와 연결된 특성의 ID를 포함합니다.|  
|[Audit 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/audit-element-assl.md)|서버의 성능이 저하되는 경우에도 [Trace](../../../analysis-services/scripting/objects/trace-element-assl.md) 요소가 이벤트를 삭제할 수 없도록 지정합니다.|  
|[AutoRestart 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/autorestart-element-assl.md)|결정 여부는 **추적** 요소는 경우 자동으로 다시 시작 해야는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서비스가 중지 되었다가 다시 시작 합니다.|  
|[BackColor 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/backcolor-element-assl.md)|부모 요소의 색 관련 표시 특징을 설명합니다.|  
|[CacheMode 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/cachemode-element-assl.md)|마이닝 구조를 처리하는 동안 검색된 학습 데이터에 사용되는 캐싱 메커니즘을 결정합니다.|  
|[CalculationReference 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/calculationreference-element-assl.md)|명명 된 집합 또는 계산된 셀에서 참조의 이름이 고 **CalculationProperty** 요소입니다.|  
|[CalculationType 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/calculationtype-element-assl.md)|연결 된 정의 된 계산 유형을 설명 **CalculationProperty** 요소입니다.|  
|[CalendarEndDate 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/calendarenddate-element-assl.md)|정의 대 한 달력 기간의 종료 날짜는 [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md) 요소입니다.|  
|[CalendarLanguage 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/calendarlanguage-element-assl.md)|에 사용 되는 달력 언어를 정의 고 **TimeBinding** 요소입니다.|  
|[CalendarStartDate 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/calendarstartdate-element-assl.md)|정의 대 한 달력 기간의 시작 날짜는 **TimeBinding** 요소입니다.|  
|[캡션 요소가 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/caption-element-assl.md)|연결된 부모 요소에 대한 캡션을 포함합니다.|  
|[CaptionIsMdx 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/captionismdx-element-assl.md)|정의 여부에 대 한 캡션은 **동작** 요소는 MDX (Multidimensional Expressions) 식입니다.|  
|[Cardinality 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/cardinality-element-assl.md)|설명 되는 관계의 카디널리티를 나타냅니다는 [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md) 또는 [RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)합니다.|  
|[CaseCubeDimensionID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/casecubedimensionid-element-assl.md)|데이터 마이닝 차원을 측정값 그룹에 연결하는 큐브 차원의 ID를 포함합니다.|  
|[ClassifiedColumnID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/classifiedcolumnid-element-assl.md)|분류 되는 관련 열의 ID가 포함 된 [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md) 요소입니다.|  
|[Collation 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/collation-element-assl.md)|부모 요소에 사용되는 데이터 정렬을 결정합니다.|  
|[ColumnID 요소 &#40;ColumnBinding&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/columnid-element-columnbinding-assl.md)|데이터 항목이 바인딩된 테이블 내 열의 ID를 포함합니다.|  
|[ColumnID 요소 &#40;EventColumn&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md)|일부로 이벤트에 대해 캡처할 정보 열의 ID를 포함 한 **추적** 요소입니다.|  
|[요소를 조건 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/condition-element-assl.md)|결정 하는 MDX 식을 포함 여부는 **동작** 부모 요소는 대상에 적용 됩니다.|  
|[ConnectionString 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/connectionstring-element-assl.md)|암호화 된 연결 문자열을 포함 한 [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) 요소입니다.|  
|[ConnectionStringSecurity 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/connectionstringsecurity-element-assl.md)|보안을 위해 데이터 원본 연결 문자열에서 사용자 암호를 제거할지 여부를 지정합니다.|  
|[요소 콘텐츠 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/content-element-assl.md)|에 있는 열의 내용을 설명는 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 요소입니다.|  
|[CreatedTimestamp 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)|부모 요소의 읽기 전용 생성 타임스탬프를 포함합니다.|  
|[CubeDimensionID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md)|식별 된 [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md) 부모 요소와 연결 된 요소입니다.|  
|[CubeID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/cubeid-element-assl.md)|식별 된 **큐브** 요소와 연관 된는 [바인딩](../../../analysis-services/scripting/data-type/binding-data-type-assl.md) 요소입니다.|  
|[CurrentStorageMode 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md)|부모 요소에 대한 현재 저장소 모드를 결정합니다.|  
|[CurrentTimeMember 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/currenttimemember-element-assl.md)|현재 멤버와 연결 된 차원 한 번의 정의 **Kpi** 요소입니다.|  
|[DataAggregation 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/dataaggregation-element-assl.md)|인스턴스가 영구 데이터 나 캐시 된 데이터를 집계할 수 있는지 여부를 결정은 **MeasureGroup**합니다.|  
|[DatabaseID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/databaseid-element-assl.md)|식별 된 **데이터베이스** 의-라인와 연관 된 요소의 **바인딩** 요소입니다.|  
|[DataSize 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/datasize-element-assl.md)|바이트의 크기를 포함 한 [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md) 요소입니다.|  
|[DataSourceID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/datasourceid-element-assl.md)|부모 요소와 연결된 **DataSource** 요소를 식별합니다.|  
|[DataSourceImpersonationInfo 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md)|에 대 한 데이터 원본에 연결할 때 가장 동작을 확인 하는 데 사용 되는 정보를 포함 한 **데이터베이스** 요소입니다.|  
|[DataSourceViewID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/datasourceviewid-element-assl.md)|식별 된 [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md) 요소와 연관 된는 **바인딩** 부모 요소입니다.|  
|[DataType 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/datatype-element-assl.md)|연결된 요소의 데이터 형식을 정의합니다.|  
|[DbSchemaName 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/dbschemaname-element-assl.md)|로 식별 된 테이블의 부모 요소에 사용 되는 스키마의 이름이 고 [DbTableName](../../../analysis-services/scripting/properties/dbtablename-element-assl.md) 요소입니다.|  
|[DbTableName 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/dbtablename-element-assl.md)|부모 요소가 바인딩된 테이블의 이름을 포함합니다.|  
|[요소를 기본 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/default-element-assl.md)|결정 여부는 **DrillThroughAction** 이 기본 드릴스루 동작 합니다.|  
|[DefaultMeasure 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/defaultmeasure-element-assl.md)|에 대 한 기본 측정값을 정의 하는 MDX 언어 식을 포함 한 **큐브** 또는 **관점** 요소입니다.|  
|[DefaultMember 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/defaultmember-element-assl.md)|부모 요소의 기본 멤버를 식별하는 MDX 식을 포함합니다.|  
|[DefaultScript 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/defaultscript-element-assl.md)|기본값을 식별 [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) 요소에는 [MdxScripts](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md) 컬렉션입니다.|  
|[DefaultValue 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/defaultvalue-element-assl.md)|연결된 된 읽기 전용 기본 값이 포함 된 [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) 요소입니다.|  
|[DeniedSet 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/deniedset-element-assl.md)|연관된 특성에 대해 거부된 권한 목록을 정의하는 집합 식을 포함합니다.|  
|[DependsOnDimensionID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/dependsondimensionid-element-assl.md)|부모 차원이 종속된 다른 차원의 ID를 포함합니다.|  
|[Description 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/description-element-assl.md)|부모 요소에 대한 설명을 포함합니다.|  
|[DimensionID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/dimensionid-element-assl.md)|차원의 ID를 포함합니다.|  
|[DiscretizationBucketCount 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/discretizationbucketcount-element-assl.md)|불연속화할 버킷의 수를 포함합니다.|  
|[DiscretizationMethod 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md)|불연속화에 사용할 방법을 정의합니다.|  
|[DisplayFlag 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/displayflag-element-assl.md)|사용자 인터페이스 구성 요소는 연결 된 표시 해야 하는지 여부를 나타내는 읽기 전용 힌트를 포함 **ServerProperty** 요소입니다.|  
|[DisplayFolder 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/displayfolder-element-assl.md)|부모 요소를 나열할 폴더를 지정합니다. 개발자 및 관리자용 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 응용 프로그램에서는 표시 폴더를 사용하여 여러 요소를 시각적으로 범주화할 수 있습니다.|  
|[Distribution 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/distribution-element-assl.md)|어떻게 스칼라 값을 설명 하는 공급자별 값이 포함 된 열에서이 배포 되는 **MiningStructure** 요소입니다.|  
|[Edition 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/edition-element-assl.md)|인스턴스의 읽기 전용 버전을 포함 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 나타내는 [서버](../../../analysis-services/scripting/objects/server-element-assl.md) 요소입니다.|  
|[요소를 사용 하도록 설정 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/enabled-element-assl.md)|부모 요소를 사용할 수 있는지 여부를 나타냅니다.|  
|[EndOfData 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/endofdata-element-assl.md)|받은 데이터의 끝을 나타냅니다.는 [PushedDataSource](../../../analysis-services/scripting/data-type/pusheddatasource-data-type-assl.md) 요소입니다.|  
|[EstimatedCount 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/estimatedcount-element-assl.md)|특성의 예상 멤버 수를 포함합니다.|  
|[EstimatedPerformanceGain 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/estimatedperformancegain-element-assl.md)|파티션의 읽기 전용 예상 성능 향상률을 포함합니다.|  
|[EstimatedRows 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md)|부모 요소가 나타내는 예상 행 수를 포함합니다.|  
|[EstimatedSize 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/estimatedsize-element-assl.md)|부모 요소의 읽기 전용 예상 크기(바이트)를 포함합니다.|  
|[EventID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/eventid-element-assl.md)|고유 하 게 식별 하는 [이벤트](../../../analysis-services/scripting/objects/event-element-assl.md) 의 일환으로 캡처할 수 있는 요소는 **추적** 요소입니다.|  
|[Expression 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/expression-element-assl.md)|부모 요소의 내용을 정의하는 MDX 식을 포함합니다.|  
|[Filter 요소 &#40;바인딩&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/filter-element-binding-assl.md)|부모 요소의 내용을 필터링하는 MDX 식을 포함합니다.|  
|[Filter 요소 &#40;추적&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/filter-element-trace-assl.md)|설명 하는 XML 문서 부분을 포함 된 **추적** 필터입니다.|  
|[FirstDayOfWeek 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/firstdayofweek-element-assl.md)|시작 요일에 대 한 정의 **TimeBinding** 요소입니다.|  
|[FiscalFirstDayOfMonth 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/fiscalfirstdayofmonth-element-assl.md)|에 대 한 회계 월의 첫 번째 날을 정의 **TimeBinding** 요소입니다.|  
|[FiscalFirstMonth 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/fiscalfirstmonth-element-assl.md)|**TimeBinding** 요소에 대한 회계 기간의 첫 번째 월을 정의합니다.|  
|[FiscalYearName 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/fiscalyearname-element-assl.md)|에 대 한 회계 연도 이름에 대 한 명명 규칙을 정의 **TimeBinding** 요소입니다.|  
|[FontFlags 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/fontflags-element-assl.md)|글꼴 관련 표시 특성을 설명는 **CalculationProperty** 또는 **측정값** 부모 요소입니다.|  
|[FontName 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/fontname-element-assl.md)|글꼴 관련 표시 특성을 설명는 **CalculationProperty** 또는 **측정값** 부모 요소입니다.|  
|[FontSize 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/fontsize-element-assl.md)|글꼴 관련 표시 특성을 설명는 **CalculationProperty** 또는 **측정값** 부모 요소입니다.|  
|[ForceRebuildInterval 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/forcerebuildinterval-element-assl.md)|새로운 MOLAP(다차원 OLAP) 이미지가 사용 가능해질 때부터 MOLAP 이미징이 무조건 시작되기 전까지의 기간을 결정합니다.|  
|[ForeColor 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/forecolor-element-assl.md)|색 관련 표시 특성을 설명는 **CalculationProperty** 또는 **측정값** 부모 요소입니다.|  
|[요소의 서식을 지정 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/format-element-assl.md)|필수 형식을 포함 된 **DataItem** 요소입니다.|  
|[FormatString 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/formatstring-element-assl.md)|에 대 한 표시 형식을 설명는 **CalculationProperty** 요소 또는 **측정값** 요소입니다.|  
|[Goal 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/goal-element-assl.md)|원하는 목표를 식별 한 **Kpi** 요소입니다.|  
|[GranularityAttributeID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/granularityattributeid-element-assl.md)|부모와 연결 된 특성의 ID를 포함 [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md) 데이터 형식입니다.|  
|[HideMemberIf 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/hidememberif-element-assl.md)|클라이언트 응용 프로그램에서 수준의 멤버를 숨길지 여부와 숨길 조건을 나타냅니다.|  
|[HierarchyID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/hierarchyid-element-assl.md)|에 대 한 ID를 포함 한 [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md), [MeasureGroupHierarchy](../../../analysis-services/scripting/data-type/measuregrouphierarchy-data-type-assl.md), 또는 [PerspectiveHierarchy](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md) 요소입니다.|  
|[HierarchyUniqueNameStyle 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/hierarchyuniquenamestyle-element-assl.md)|얼마나 고유한 이름을 결정에 포함 된 계층에 대해 생성 되는 **CubeDimension**합니다.|  
|[ID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/id-element-assl.md)|부모 요소의 고유 ID를 포함합니다.|  
|[IgnoreUnrelatedDimensions 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/ignoreunrelateddimensions-element-assl.md)|측정값 그룹과 관련이 없는 차원의 멤버가 쿼리에 포함될 때 관련이 없는 차원이 최상위로 강제되는지 결정합니다.|  
|[ImpersonationInfo 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/impersonationinfo-element-assl.md)|어셈블리에 액세스하거나 이를 실행할 때 가장 동작을 확인하는 데 사용되는 정보를 포함합니다.|  
|[ImpersonationInfoSecurity 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/impersonationinfosecurity-element-assl.md)|에 제공 된 보안 자격 증명에이 변경 사항이 여부를 나타내는 읽기 전용 값이 포함 된 **ImpersonationInfo** 데이터 형식입니다.|  
|[ImpersonationMode 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/impersonationmode-element-assl.md)|파생 된 요소에 대 한 가장 방법을 나타내는 값이 포함 된 **ImpersonationInfo** 데이터 형식입니다.|  
|[InstanceSelection 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/instanceselection-element-assl.md)|목록의 예상 항목 수를 기반으로 항목 목록의 표시 방법을 제안하는 힌트를 클라이언트 응용 프로그램에 제공합니다.|  
|[IntermediateCubeDimensionID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/intermediatecubedimensionid-element-assl.md)|참조 차원을 측정값 그룹에 연결하는 차원의 ID를 포함합니다.|  
|[IntermediateGranularityAttributeID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/intermediategranularityattributeid-element-assl.md)|참조 차원을 중간 차원에 연결하는 데 사용되는 중간 큐브 차원에 있는 세분성 특성의 ID를 포함합니다.|  
|[InvalidXmlCharacters 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/invalidxmlcharacters-element-assl.md)|원본 데이터에 있는 잘못된 XML 문자에 대한 처리 방식을 지정합니다.|  
|[Invocation 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/invocation-element-assl.md)|**Action** 을 호출할 방법을 지정합니다.|  
|[IsAggregatable 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/isaggregatable-element-assl.md)|지정 여부의 값은 [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) 요소를 집계할 수 합니다.|  
|[IsKey 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/iskey-element-assl.md)|열에 사례에 대 한 키를 제공 하는지 여부를 나타냅니다는 **MiningStructure** 요소입니다.|  
|[Isolation 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/isolation-element-assl.md)|파생 된 요소에 대 한 격리 수준을 나타냅니다는 [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) 데이터 형식입니다.|  
|[KeyDuplicate 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/keyduplicate-element-assl.md)|처리 중 중복 키 오류가 발생하는 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]가 이러한 오류를 처리하는 방법을 결정합니다.|  
|[KeyErrorAction 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/keyerroraction-element-assl.md)|키에 오류가 발생하는 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]가 수행할 동작을 지정합니다.|  
|[KeyErrorLimit 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/keyerrorlimit-element-assl.md)|처리 중 허용 가능한 오류 수를 포함합니다.|  
|[KeyErrorLimitAction 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/keyerrorlimitaction-element-assl.md)|작업을 지정 하는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 지정 된 키 오류 수 하는 경우는 [KeyErrorLimit](../../../analysis-services/scripting/properties/keyerrorlimit-element-assl.md) 요소에 도달할 때.|  
|[KeyErrorLogFile 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/keyerrorlogfile-element-assl.md)|처리 오류를 기록할 파일 이름을 포함합니다.|  
|[KeyNotFound 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/keynotfound-element-assl.md)|참조 무결성 오류가 발생하는 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]가 반응하는 방식을 지정합니다.|  
|[KeyUniquenessGuarantee 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/keyuniquenessguarantee-element-assl.md)|특성 키와 해당 이름 간의 관계와 관련 특성에 대한 관계가 유효하도록 보장되는지 여부를 나타냅니다.|  
|[KpiID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/kpiid-element-assl.md)|연결 하는 ID를 포함 한 **Kpi** 인 요소는 **관점** 요소입니다.|  
|[언어 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/language-element-assl.md)|부모 요소의 언어 식별자를 포함합니다.|  
|[LastProcessed 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md)|부모 요소를 포함하는 데이터베이스가 마지막으로 처리된 시간을 나타내는 읽기 전용 타임스탬프를 포함합니다.|  
|[LastSchemaUpdate 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)|부모 요소의 읽기 전용 메타데이터 업데이트 타임스탬프를 포함합니다.|  
|[LastUpdate 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/lastupdate-element-assl.md)|읽기 전용 포함 마지막을 나타내는 타임 스탬프에 연결 된 **데이터베이스** 변경 된 데이터베이스에 포함 된 주요 개체 중 하나 또는 합니다.|  
|[Latency 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/latency-element-assl.md)|가장 이른 알림과 MOLAP 이미지가 삭제된 시점 사이의 "유예 기간"을 정의합니다.|  
|[LogFileAppend 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/logfileappend-element-assl.md)|결정 여부는 **추적** 요소가 해당 로깅 출력을 기존 로그 파일에 아니면 덮어쓸지가 됩니다.|  
|[LogFileName 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/logfilename-element-assl.md)|에 대 한 로그 파일의 파일 이름이 포함 된 **추적** 요소입니다.|  
|[LogFileRollover 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/logfilerollover-element-assl.md)|지정의 로깅을 **추적** 해야에 지정 된 최대 로그 파일 크기를 중지할지 또는 출력을 새 파일로 롤오버할 [LogFileSize](../../../analysis-services/scripting/properties/logfilesize-element-assl.md) 에 도달 합니다.|  
|[LogFileSize 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/logfilesize-element-assl.md)|최대 로그 파일 크기(MB)를 지정합니다.|  
|[ManagedProvider 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/managedprovider-element-assl.md)|파생 된 요소에 의해 사용 되는 관리 되는 공급자의 이름을 포함 된 **DataSource** 데이터 형식입니다.|  
|[ManufacturingExtraMonthQuarter 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/manufacturingextramonthquarter-element-assl.md)|에 대 한 추가 월이 할당 된 제조 기간의 월을 정의 **TimeBinding** 요소입니다.|  
|[ManufacturingFirstMonth 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/manufacturingfirstmonth-element-assl.md)|**TimeBinding** 요소에 대한 첫 번째 제조 월을 정의합니다.|  
|[ManufacturingFirstWeekOfMonth 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/manufacturingfirstweekofmonth-element-assl.md)|에 대 한 제조 월의 첫째 주를 정의 **TimeBinding** 요소입니다.|  
|[MasterDatasourceID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/masterdatasourceid-element-assl.md)|에 대 한 마스터 데이터 원본 ID를 포함 한 **데이터베이스** 요소입니다.|  
|[Materialization 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/materialization-element-assl.md)|측정값 그룹과 참조 차원 간의 관계 유형을 나타냅니다.|  
|[MaxActiveConnections 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/maxactiveconnections-element-assl.md)|파생 된 요소에 의해 허용 되는 동시 연결의 최대 수를 포함 된 **DataSource** 데이터 형식입니다.|  
|[MdxMissingMemberMode 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/mdxmissingmembermode-element-assl.md)|MDX 문에 대해 누락된 멤버가 처리되는 방식을 결정합니다.|  
|[MeasureExpression 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/measureexpression-element-assl.md)|측정값을 정의하는 MDX 식을 포함합니다.|  
|[MeasureGroupID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/measuregroupid-element-assl.md)|연결 된 **MeasureGroup** 부모 요소, 바인딩 또는 아웃오브 라인 바인딩을 사용 합니다.|  
|[MeasureID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/measureid-element-assl.md)|연결 된 **측정값** 부모 요소와 요소입니다.|  
|[MeasureQualificaton 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/measurequalificaton-element-assl.md)|측정값에 대 한 접두사 적용 여부를 결정은 **MeasureGroup**합니다.|  
|[MemberNamesUnique 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/membernamesunique-element-assl.md)|부모 요소의 멤버 이름이 고유해야 하는지 여부를 결정합니다.|  
|[MemberUniqueNameStyle 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/memberuniquenamestyle-element-assl.md)|얼마나 고유한 이름을 결정에 포함 된 계층의 멤버에 대해 생성 되는 **CubeDimension** 요소입니다.|  
|[MembersWithData 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)|비-리프 멤버에 대한 데이터 멤버를 부모 특성에 표시할지 여부를 결정합니다.|  
|[MembersWithDataCaption 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md)|시스템 생성 데이터 멤버에 대한 캡션을 만드는 데 사용되는 템플릿 문자열을 제공합니다.|  
|[MimeType 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/mimetype-element-assl.md)|부모에서 나타내는 데이터의 해당 하는 경우 MIME Multipurpose Internet Mail Extensions () 형식을 포함 **DataItem** 요소입니다.|  
|[MiningModelID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/miningmodelid-element-assl.md)|마이닝 모델을 데이터 마이닝 차원과 연결합니다.|  
|[Name 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/name-element-assl.md)|부모 요소의 이름을 포함합니다.|  
|[NamingTemplate 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md)|생성 된 부모-자식 계층에서 수준의 이름이 지정 되는 방식을 정의 **DimensionAttribute** 부모 요소입니다.|  
|[NonEmptyBehavior 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/nonemptybehavior-element-assl.md)|부모와 연결 된 비어 있지 않은 동작을 결정 하는 **CalculationProperty** 요소입니다.|  
|[NotificationTechnique 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/notificationtechnique-element-assl.md)|지정 여부 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 외부 클라이언트 응용 프로그램의 알림을 처리 합니다.|  
|[NullKeyConvertedToUnknown 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md)|Null 변환 오류가 발생할 때 수행할 동작을 지정합니다.|  
|[NullKeyNotAllowed 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 처리 엔진이 처리 중 발생하는 Null 키 오류를 처리하는 방법을 결정합니다.|  
|[NullProcessing 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md)|Null 값이 처리되는 방식을 정의합니다.|  
|[OnlineMode 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/onlinemode-element-assl.md)|캐시를 다시 작성하기 시작할 때 바로 데이터베이스를 다시 온라인 상태로 만들지, 아니면 캐시를 다시 작성한 후에만 데이터베이스를 다시 온라인 상태로 만들지를 지정합니다.|  
|[OptimizedState 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/optimizedstate-element-assl.md)|계층에 적용되는 최적화 수준을 결정합니다.|  
|[Optionality 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/optionality-element-assl.md)|에 대 한 멤버의 옵션을 나타냅니다는 **AttributeRelationship** 요소입니다.|  
|[OrderBy 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/orderby-element-assl.md)|특성에 포함된 멤버의 정렬 방식을 설명합니다.|  
|[OrderByAttributeID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md)|멤버를 정렬 하는 기준인 다른 특성을 식별 된 [차원](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) 특성입니다.|  
|[Ordinal 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/ordinal-element-assl.md)|키 및 번역과 같은 컬렉션에서 바인딩할 서수를 나타냅니다.|  
|[OverrideBehavior 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/overridebehavior-element-assl.md)|설명 되는 관계의 재정의 동작을 나타냅니다는 **AttributeRelationship** 요소입니다.|  
|[PartitionID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/partitionid-element-assl.md)|연결 된 **파티션** 을 부모 요소, 바인딩 또는 아웃오브 라인 바인딩 요소입니다.|  
|[Password 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/password-element-assl.md)|에 대 한 사용자 계정의 암호를 포함 된 **ImpersonationInfo** 요소입니다.|  
|[경로 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/path-element-assl.md)|인스턴스에서 제공 된 경로 포함 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], 사용 된 보고서의는 [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) 요소입니다.|  
|[PendingValue 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/pendingvalue-element-assl.md)|연결된 **ServerProperty** 요소의 보류 중인 읽기 전용 값을 포함합니다.|  
|[PermissionSet 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/permissionset-element-assl.md)|와 연결 된 권한 집합을 식별 한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 어셈블리입니다.|  
|[Persistence 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/persistence-element-assl.md)|바인딩된 원본 데이터의 어떤 부분에는 동적 이며 지정 된 빈도 사용 하 여 업데이트 확인 결정는 [RefreshPolicy](../../../analysis-services/scripting/properties/refreshpolicy-element-assl.md) 요소입니다.|  
|[요소를 처리할 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/process-element-assl.md)|사용자가 부모 요소의 소유자를 처리할 수 있는지 여부를 결정합니다.|  
|[ProcessingMode 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/processingmode-element-assl.md)|인스턴스에서 인덱싱 및 집계를 처리 중에 수행할지 아니면 처리 후에 수행할지를 나타냅니다.|  
|[ProcessingPriority 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/processingpriority-element-assl.md)|지연 집계, 인덱싱 또는 클러스터링과 같은 백그라운드 작업을 수행하는 동안 부모 개체의 처리 우선 순위를 결정합니다.|  
|[ProcessingQuery 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/processingquery-element-assl.md)|증분 처리 상태 알림을 위해 실행할 쿼리의 매개 변수가 있는 텍스트를 포함합니다.|  
|[ProductName 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/productname-element-assl.md)|인스턴스의 읽기 전용 제품 이름을 포함 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 과 연관 된 **서버** 요소입니다.|  
|[쿼리 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/query-element-assl.md)|알림을 위해 실행할 쿼리의 텍스트를 포함합니다.|  
|[QueryDefinition 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/querydefinition-element-assl.md)|와 연결 된 쿼리에 대 한 불투명 식을 포함 한 **DataSource** 요소에는 [QueryBinding](../../../analysis-services/scripting/data-type/querybinding-data-type-assl.md) 요소입니다.|  
|[요소를 읽을 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/read-element-assl.md)|지정된 [CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md) 또는 [Permission](../../../analysis-services/scripting/data-type/permission-data-type-assl.md) 요소에 대해 데이터 또는 메타데이터를 읽을 수 있는지 여부를 결정합니다.|  
|[ReadDefinition 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/readdefinition-element-assl.md)|멤버가 데이터베이스의 정의 또는 데이터베이스의 개체 정의를 읽을 수 있는지 여부를 결정합니다.|  
|[ReadSourceData 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/readsourcedata-element-assl.md)|얼마나 고유한 이름을 결정에 포함 된 계층에 대해 생성 되는 **CubePermission**합니다.|  
|[RefreshInterval 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/refreshinterval-element-assl.md)|부모 요소와 연결된 바인딩된 데이터를 새로 고치는 간격을 지정합니다.|  
|[RefreshPolicy 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/refreshpolicy-element-assl.md)|[Persistence](../../../analysis-services/scripting/properties/persistence-element-assl.md) 요소로 지정된 차원 또는 측정값 그룹의 동적 부분에 대한 변경 내용이 확인되는 빈도를 결정합니다.|  
|[RelationshipType 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/relationshiptype-element-assl.md)|나타냅니다 여부에 대 한 멤버 관계는 **AttributeRelationship** 변경할 수 있습니다.|  
|[RemoteDatasourceID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/remotedatasourceid-element-assl.md)|원격 파티션을 저장하는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스를 가리키는 OLAP 데이터 원본의 ID를 지정합니다.|  
|[ReportingFirstMonth 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/reportingfirstmonth-element-assl.md)|첫 번째 보고 월을 정의 **TimeBinding** 요소입니다.|  
|[ReportingFirstWeekOfMonth 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/reportingfirstweekofmonth-element-assl.md)|에 대 한 보고 월의 첫째 주를 정의 고 **TimeBinding** 요소입니다.|  
|[ReportingWeekToMonthPattern 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/reportingweektomonthpattern-element-assl.md)|에 대 한 보고 주-월 패턴 정의 **TimeBinding** 요소입니다.|  
|[ReportServer 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/reportserver-element-assl.md)|이름을 포함 된 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 에서 사용 되는 인스턴스는 **ReportAction**합니다.|  
|[RequiresRestart 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/requiresrestart-element-assl.md)|와 연결 된 읽기 전용 값을 포함 한 **ServerProperty** 결정를 인스턴스에 변경 내용을 적용 하기 위해 다시 시작 해야 하는지 여부를 서버 속성의 값을 변경 해야 하는 요소입니다.|  
|[RoleID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/roleid-element-assl.md)|정의된 권한에 대한 역할을 식별합니다.|  
|[루트 요소를 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/root-element-assl.md)|데이터 원본의 데이터(행 집합)를 포함합니다.|  
|[RootMemberIf 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/rootmemberif-element-assl.md)|부모 특성의 멤버 또는 루트 멤버를 식별하는 방법을 결정합니다.|  
|[스키마 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/schema-element-assl.md)|데이터 원본 뷰의 스키마를 포함합니다.|  
|[ScriptCacheProcessingMode 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/scriptcacheprocessingmode-element-assl.md)|서버에서 스크립트 캐시를 처리 중에 작성할지, 아니면 처리 후에 작성할지를 나타냅니다.|  
|[SilenceInterval 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/silenceinterval-element-assl.md)|MOLAP 이미징 처리를 시작하기 전에 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스를 일시 중지하는 최소 시간을 정의합니다.|  
|[SilenceOverrideInterval 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/silenceoverrideinterval-element-assl.md)|MOLAP 이미징을 무조건 시작하기 전에 초기 알림을 받은 후 경과해야 하는 시간을 정의합니다.|  
|[Slice 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/slice-element-assl.md)|파티션에 포함된 조각을 정의하는 MDX 식을 포함합니다.|  
|[SolveOrder 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/solveorder-element-assl.md)|계산 순서를 나타냅니다는 **CalculationProperty** 요소는 계산된 멤버 또는 계산된 셀 정의에 적용 합니다.|  
|[Source 요소 &#40;바인딩&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|부모 요소가 바인딩된 데이터의 원본을 식별합니다.|  
|[Source 요소 &#40;ComAssembly&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/source-element-comassembly-assl.md)|COM(구성 요소 개체 모델) 구성 요소의 파일 이름 또는 ProgID(프로그래밍 식별자)를 포함합니다.|  
|[Source 요소 &#40;측정값&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/source-element-measure-assl.md)|값을 포함 하는 원본에 대 한 정보가 포함 된 **측정값** 요소입니다.|  
|[SourceAttributeID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/sourceattributeid-element-assl.md)|원본 특성 ID가 포함 된 [수준](../../../analysis-services/scripting/objects/level-element-assl.md) 요소의 기반이 되 합니다.|  
|[SourceColumnID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/sourcecolumnid-element-assl.md)|상위에서 원본 마이닝 구조 열의 ID를 포함 **MiningStructure** 요소입니다.|  
|[상태 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/state-element-assl.md)|부모 요소의 현재 처리 상태를 나타내는 읽기 전용 값을 포함합니다.|  
|[Status 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/status-element-assl.md)|에 대 한 상태 표시를 반환 하는 MDX 식을 포함 한 **Kpi** 요소입니다.|  
|[StatusGraphic 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/statusgraphic-element-assl.md)|**Kpi** 요소의 상태에 대해 권장되는 그래픽 표현을 포함합니다.|  
|[StopTime 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/stoptime-element-assl.md)|날짜 및 시간을 지정 된 **추적** 요소를 중지 합니다.|  
|[StorageLocation 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)|부모 요소의 내용에 대한 파일 시스템 저장소 위치를 포함합니다.|  
|[StorageMode 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/storagemode-element-assl.md)|부모 요소의 저장소 모드를 결정합니다.|  
|[TableID 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/tableid-element-assl.md)|테이블의 ID를 포함 (에서 **DataSourceView** 요소) 부모 요소와 연결 합니다.|  
|[요소를 대상 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/target-element-assl.md)|대상을 식별 하는 **동작** 요소입니다.|  
|[TargetType 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/targettype-element-assl.md)|식별 된 항목의 유형을 식별 된 [대상](../../../analysis-services/scripting/properties/target-element-assl.md) 요소입니다.|  
|[텍스트 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/text-element-assl.md)|텍스트를 포함 한 [명령](../../../analysis-services/scripting/objects/command-element-assl.md) 요소입니다.|  
|[Timeout 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/timeout-element-assl.md)|데이터 검색 시도의 제한 시간(초)을 지정합니다.|  
|[요소 추세 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/trend-element-assl.md)|에 대 한 추세 표시를 반환 하는 MDX 식을 포함 한 **Kpi** 요소입니다.|  
|[TrendGraphic 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/trendgraphic-element-assl.md)|추세에 대 한 권장된 그래픽 표현을 포함 된 **Kpi** 요소입니다.|  
|[Trimming 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/trimming-element-assl.md)|데이터 원본의 데이터가 잘리는 방법을 지정합니다.|  
|[E Element &#40;동작&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-action-assl.md)|유형을 포함 된 **동작** 요소입니다.|  
|[E Element &#40;바인딩&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-binding-assl.md)|특성 바인딩의 유형을 포함합니다.|  
|[E Element &#40;ClrAssemblyFile&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-clrassemblyfile-assl.md)|.NET Framework 어셈블리에 속하는 파일 중 하나의 파일 유형을 지정 합니다.|  
|[E Element &#40;차원&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-dimension-assl.md)|차원의 내용에 대한 정보를 제공합니다.|  
|[E Element &#40;DimensionAttribute&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-dimensionattribute-assl.md)|특성의 유형을 포함합니다.|  
|[E Element &#40;MeasureGroup&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-measuregroup-assl.md)|형식을 지정 된 **MeasureGroup**합니다.|  
|[E Element &#40;MeasureGroupAttribute&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-measuregroupattribute-assl.md)|형식을 포함 한 [MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md) 요소입니다.|  
|[E Element &#40;MiningStructureColumn&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-miningstructurecolumn-assl.md)|유형을 포함 된 [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md) 요소입니다.|  
|[E Element &#40;파티션&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-partition-assl.md)|유형을 포함 된 **파티션** 요소입니다.|  
|[E Element &#40;PerspectiveCalculation&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-perspectivecalculation-assl.md)|유형을 나타냅니다는 [PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md) 요소입니다.|  
|[UnknownMember 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/unknownmember-element-assl.md)|알 수 없는 멤버의 표시 여부를 나타냅니다.|  
|[UnknownMemberName 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/unknownmembername-element-assl.md)|차원의 알 수 없는 멤버에 대한 캡션을 차원의 기본 언어로 포함합니다.|  
|[Usage 요소 &#40;DimensionAttribute&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md)|특성의 사용 방식을 설명합니다.|  
|[Usage 요소 &#40;MiningModelColumn&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/usage-element-miningmodelcolumn-assl.md)|설명 어떻게 부모에 연결 된 열 **MiningStructure** 사용 됩니다.|  
|[요소 값 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/value-element-assl.md)|부모 요소의 값을 포함합니다.|  
|[버전 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/version-element-assl.md)|인스턴스의 읽기 전용 버전 번호를 포함 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 나타내는 **서버** 요소입니다.|  
|[Visibility 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/visibility-element-assl.md)|표시 유형을 정의 [주석](../../../analysis-services/scripting/objects/annotation-element-assl.md) 요소입니다.|  
|[Visible 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/visible-element-assl.md)|부모 요소의 표시 유형을 결정합니다.|  
|[VisualTotals 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/visualtotals-element-assl.md)|이 특성의 멤버에 대해 보이는 값 합계를 표시할지 여부를 확인하는 MDX 식을 포함합니다.|  
|[Write 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/write-element-assl.md)|데이터 또는 메타 데이터를 쓸 수 있는지 여부를 결정 한 주어진 **CubeDimensionPermission** 또는 **권한** 요소입니다.|  
|[WriteEnabled 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/writeenabled-element-assl.md)|보안 권한에 따라 차원 쓰기 저장(writeback)을 사용할 수 있는지 여부를 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services Scripting Language XML 요소 계층 & #40; ASSL & #41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
