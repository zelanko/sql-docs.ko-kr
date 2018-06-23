---
title: 속성 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- properties [Analysis Services Scripting Language]
- Analysis Services Scripting Language, properties
- ASSL, properties
ms.assetid: 9a38cdc9-a210-421a-90e9-6391876765fa
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 72ec08342256fecbd63c791b6db6e343479bca65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092778"
---
# <a name="properties-assl"></a>속성(ASSL)
  이 참조 섹션에서는 ASSL(Analysis Services Scripting Language) 스키마에서 개체 속성으로 사용되는 각 요소에 대한 구문 및 사용 정보를 제공합니다.  
  
 ASSL 스키마는 XML 요소만 포함하지만 이 섹션에 설명된 요소는 개발자의 관점에서 볼 때 개체를 설명하는 속성에 해당합니다.  
  
 속성은 ASSL 스키마에서 리프 수준 요소이며 자식 요소 또는 자체 속성에 해당하는 요소를 갖지 않습니다.  
  
 속성으로 나타날 수 있는 스키마의 리프 수준 요소가 개체 유형이어서 개체로 분류되는 경우도 있습니다. 예를 들어 `Source` 개체의 `Dimension`는 `DimensionBinding` 유형입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|요소|Description|  
|-------------|-----------------|  
|[요소에 액세스 &#40;ASSL&#41;](access-element-assl.md)|에 지정 된 액세스 수준을 나타냅니다는 [CellPermission](../objects/cellpermission-element-assl.md) 요소입니다.|  
|[요소 계정 &#40;ImpersonationInfo&#41; &#40;ASSL&#41;](account-element-impersonationinfo-assl.md)|에 대 한 사용자 계정의 이름을 포함 된 [ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md) 데이터 형식입니다.|  
|[AccountType 요소 &#40;ASSL&#41;](accounttype-element-assl.md)|에 정의 된 계정 유형의 이름을 포함 한 [데이터베이스](../objects/database-element-assl.md) 요소입니다.|  
|[ActionID 요소 &#40;ASSL&#41;](id-element-assl.md)|이름을 포함 한 [작업](../objects/action-element-assl.md) 에 정의 된 요소는 [큐브](../objects/cube-element-assl.md) 요소에서 사용할 수 있는 [관점](../objects/perspective-element-assl.md) 요소도는 [PerspectiveAction](../data-type/action-data-type-assl.md) 요소입니다.|  
|[Administer 요소 &#40;ASSL&#41;](administer-element-assl.md)|관련된 권한에 `Database` 요소 관리 권한이 포함되어 있는지 여부를 나타냅니다.|  
|[AggregateFunction 요소 &#40;ASSL&#41;](aggregatefunction-element-assl.md)|사용 하는 집계 함수의 유형을 정의 [측정값](../objects/measure-element-assl.md) 요소입니다.|  
|[AggregationDesignID 요소 &#40;ASSL&#41;](aggregationdesignid-element-assl.md)|식별 된 [AggregationDesign](../objects/aggregationdesign-element-assl.md) 요소와 연관 된는 [파티션](../objects/partition-element-assl.md) 요소입니다.|  
|[AggregationFunction 요소 &#40;ASSL&#41;](aggregationfunction-element-assl.md)|계정 유형에 사용할 집계 함수를 포함합니다.|  
|[AggregationID 요소 &#40;ASSL&#41;](aggregationid-element-assl.md)|집계 인스턴스를 만드는 데 사용되는 `AggregationDesign` 요소에서 집계 정의를 식별합니다.|  
|[AggregationInstanceSource 요소 &#40;ASSL&#41;](aggregationinstancesource-element-assl.md)|`Partition` 요소에 바인딩된 사용자 정의 집계 인스턴스의 데이터 원본을 식별합니다.|  
|[AggregationPrefix 요소 &#40;ASSL&#41;](aggregationprefix-element-assl.md)|관련 부모 요소 전체에서 집계 이름에 사용할 공통 접두사를 정의합니다.|  
|[AggregationStorage 요소 &#40;ASSL&#41;](aggregationstorage-element-assl.md)|집계 저장 방법을 식별합니다.|  
|[AggregationType 요소 &#40;ASSL&#41;](aggregationtype-element-assl.md)|`Partition` 요소에 의해 저장되는 집계 유형을 정의합니다.|  
|[AggregationUsage 요소 &#40;ASSL&#41;](aggregationusage-element-assl.md)|컨트롤 어떻게에서 집계 디자이너로 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 집계를 디자인 합니다.|  
|[Algorithm 요소 &#40;ASSL&#41;](algorithm-element-assl.md)|사용 되는 알고리즘 정의 [MiningModel](../objects/miningmodel-element-assl.md) 요소입니다.|  
|[Alias 요소 &#40;ASSL&#41;](alias-element-assl.md)|에 대 한 별칭을 정의 [계정](../objects/account-element-assl.md) 요소입니다.|  
|[AllMemberAggregationUsage 요소 &#40;ASSL&#41;](allmemberaggregationusage-element-assl.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 집계 디자이너로 집계를 디자인하는 방식을 제어합니다.|  
|[AllMemberName 요소 &#40;ASSL&#41;](name-element-assl.md)|모든 구성원에 대 한 캡션을 기본 언어로 포함 한 [계층](../objects/hierarchy-element-assl.md) 요소입니다.|  
|[AllowBrowsing 요소 &#40;ASSL&#41;](allowbrowsing-element-assl.md)|정의 여부의 멤버는 [역할](../objects/role-element-assl.md) 요소에 대 한 찾아보기 권한이 `MiningModel` 요소입니다.|  
|[AllowDrillThrough 요소 &#40;ASSL&#41;](allowdrillthrough-element-assl.md)|부모 요소에서 드릴스루가 허용되는지 여부를 결정합니다.|  
|[AllowDuplicateNames 요소 &#40;ASSL&#41;](allowduplicatenames-element-assl.md)|`Hierarchy` 요소에서 중복 이름이 허용되는지 여부를 결정합니다.|  
|[AllowedSet 요소 &#40;ASSL&#41;](allowedset-element-assl.md)|특성에서 `Role` 요소에 허용되는 사용 권한 집합을 정의하는 집합 식을 포함합니다.|  
|[Application 요소 &#40;ASSL&#41;](application-element-assl.md)|`Action` 요소와 연결된 응용 프로그램을 식별합니다.|  
|[AssociatedMeasureGroupID 요소 &#40;ASSL&#41;](measuregroupid-element-assl.md)|식별자 (ID)가 포함 된 [MeasureGroup](../objects/group-element-assl.md) 요소와 연관 된는 [CalculationProperty](../objects/calculationproperty-element-assl.md) 요소 또는 [Kpi](../objects/kpi-element-assl.md) 요소입니다.|  
|[AttributeAllMemberName 요소 &#40;ASSL&#41;](attributeallmembername-element-assl.md)|차원의 All 멤버에 대한 캡션을 기본 언어로 포함합니다.|  
|[AttributeHierarchyDisplayFolder 요소 &#40;ASSL&#41;](displayfolder-element-assl.md)|연관된 특성 계층을 표시할 폴더를 식별합니다.|  
|[AttributeHierarchyEnabled 요소 &#40;ASSL&#41;](enabled-element-assl.md)|특성에 대한 특성 계층을 설정할지 여부를 결정합니다.|  
|[AttributeHierarchyOptimizedState 요소 &#40;ASSL&#41;](state-element-assl.md)|특성 계층에 적용되는 최적화 수준을 결정합니다.|  
|[AttributeHierarchyOrdered 요소 &#40;ASSL&#41;](attributehierarchyordered-element-assl.md)|연관된 특성 계층의 정렬 여부를 결정합니다.|  
|[AttributeHierarchyVisible 요소 &#40;ASSL&#41;](visible-element-assl.md)|클라이언트 응용 프로그램에서 특성 계층을 볼 수 있는지 여부를 결정합니다.|  
|[AttributeID 요소 &#40;ASSL&#41;](attributeid-element-assl.md)|부모 요소와 연결된 특성의 ID를 포함합니다.|  
|[Audit 요소 &#40;ASSL&#41;](audit-element-assl.md)|지정 하는 [추적](../objects/trace-element-assl.md) 요소 서버의 성능이 저하 되는 경우에 이벤트를 삭제할 수 없습니다.|  
|[AutoRestart 요소 &#40;ASSL&#41;](autorestart-element-assl.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서비스가 중지되고 다시 시작되는 경우 `Trace` 요소를 자동으로 다시 시작할지 여부를 결정합니다.|  
|[BackColor 요소 &#40;ASSL&#41;](backcolor-element-assl.md)|부모 요소의 색 관련 표시 특징을 설명합니다.|  
|[CacheMode 요소 &#40;ASSL&#41;](cachemode-element-assl.md)|마이닝 구조를 처리하는 동안 검색된 학습 데이터에 사용되는 캐싱 메커니즘을 결정합니다.|  
|[CalculationReference 요소 &#40;ASSL&#41;](calculationreference-element-assl.md)|`CalculationProperty` 요소가 참조하는 명명된 집합 또는 계산 셀의 이름을 포함합니다.|  
|[CalculationType 요소 &#40;ASSL&#41;](calculationtype-element-assl.md)|연결된 `CalculationProperty` 요소에 정의된 계산의 유형을 설명합니다.|  
|[CalendarEndDate 요소 &#40;ASSL&#41;](calendarenddate-element-assl.md)|정의 대 한 달력 기간의 종료 날짜는 [TimeBinding](../data-type/binding-data-type-assl.md) 요소입니다.|  
|[CalendarLanguage 요소 &#40;ASSL&#41;](language-element-assl.md)|`TimeBinding` 요소에 사용되는 달력 언어를 정의합니다.|  
|[CalendarStartDate 요소 &#40;ASSL&#41;](calendarstartdate-element-assl.md)|`TimeBinding` 요소에 대한 달력 기간의 시작 날짜를 정의합니다.|  
|[캡션 요소가 &#40;ASSL&#41;](caption-element-assl.md)|연결된 부모 요소에 대한 캡션을 포함합니다.|  
|[CaptionIsMdx 요소 &#40;ASSL&#41;](captionismdx-element-assl.md)|`Action` 요소에 대한 캡션이 MDX(Multidimensional Expressions) 식인지 여부를 정의합니다.|  
|[Cardinality 요소 &#40;ASSL&#41;](cardinality-element-assl.md)|설명 되는 관계의 카디널리티를 나타냅니다는 [AttributeRelationship](../objects/attributerelationship-element-assl.md) 또는 [RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md)합니다.|  
|[CaseCubeDimensionID 요소 &#40;ASSL&#41;](dimensionid-element-assl.md)|데이터 마이닝 차원을 측정값 그룹에 연결하는 큐브 차원의 ID를 포함합니다.|  
|[ClassifiedColumnID 요소 &#40;ASSL&#41;](classifiedcolumnid-element-assl.md)|분류 되는 관련 열의 ID가 포함 된 [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) 요소입니다.|  
|[Collation 요소 &#40;ASSL&#41;](collation-element-assl.md)|부모 요소에 사용되는 데이터 정렬을 결정합니다.|  
|[ColumnID 요소 &#40;ColumnBinding&#41; &#40;ASSL&#41;](columnid-element-columnbinding-assl.md)|데이터 항목이 바인딩된 테이블 내 열의 ID를 포함합니다.|  
|[ColumnID 요소 &#40;EventColumn&#41; &#40;ASSL&#41;](columnid-element-eventcolumn-assl.md)|`Trace` 요소의 일부로 이벤트에 대해 캡처할 정보 열의 ID를 포함합니다.|  
|[요소를 조건 &#40;ASSL&#41;](condition-element-assl.md)|`Action` 부모 요소가 대상에 적용되는지 여부를 확인하는 MDX 식을 포함합니다.|  
|[ConnectionString 요소 &#40;ASSL&#41;](connectionstring-element-assl.md)|암호화 된 연결 문자열을 포함 한 [DataSource](../objects/datasource-element-assl.md) 요소입니다.|  
|[ConnectionStringSecurity 요소 &#40;ASSL&#41;](connectionstringsecurity-element-assl.md)|보안을 위해 데이터 원본 연결 문자열에서 사용자 암호를 제거할지 여부를 지정합니다.|  
|[요소 콘텐츠 &#40;ASSL&#41;](content-element-assl.md)|에 있는 열의 내용을 설명는 [MiningStructure](../objects/miningstructure-element-assl.md) 요소입니다.|  
|[CreatedTimestamp 요소 &#40;ASSL&#41;](createdtimestamp-element-assl.md)|부모 요소의 읽기 전용 생성 타임스탬프를 포함합니다.|  
|[CubeDimensionID 요소 &#40;ASSL&#41;](cubedimensionid-element-assl.md)|식별 된 [CubeDimension](../data-type/cubedimension-data-type-assl.md) 부모 요소와 연결 된 요소입니다.|  
|[CubeID 요소 &#40;ASSL&#41;](cubeid-element-assl.md)|식별 된 `Cube` 요소와 연관 된는 [바인딩](../data-type/binding-data-type-assl.md) 요소입니다.|  
|[CurrentStorageMode 요소 &#40;ASSL&#41;](storagemode-element-assl.md)|부모 요소에 대한 현재 저장소 모드를 결정합니다.|  
|[CurrentTimeMember 요소 &#40;ASSL&#41;](../objects/member-element-assl.md)|`Kpi` 요소와 연결된 시간 차원의 현재 멤버를 정의합니다.|  
|[DataAggregation 요소 &#40;ASSL&#41;](../objects/aggregation-element-assl.md)|인스턴스가 `MeasureGroup`의 영구 데이터나 캐시된 데이터를 집계할 수 있는지 여부를 결정합니다.|  
|[DatabaseID 요소 &#40;ASSL&#41;](databaseid-element-assl.md)|아웃오브 라인 `Database` 요소와 연결된 `Binding` 요소를 식별합니다.|  
|[DataSize 요소 &#40;ASSL&#41;](datasize-element-assl.md)|바이트의 크기를 포함 한 [DataItem](../data-type/dataitem-data-type-assl.md) 요소입니다.|  
|[DataSourceID 요소 &#40;ASSL&#41;](datasourceid-element-assl.md)|부모 요소와 연결된 `DataSource` 요소를 식별합니다.|  
|[DataSourceImpersonationInfo 요소 &#40;ASSL&#41;](impersonationinfo-element-assl.md)|`Database` 요소의 데이터 원본에 연결할 때 가장 동작을 확인하는 데 사용되는 정보를 포함합니다.|  
|[DataSourceViewID 요소 &#40;ASSL&#41;](datasourceviewid-element-assl.md)|식별 된 [DataSourceView](../objects/datasourceview-element-assl.md) 요소와 연관 된는 `Binding` 부모 요소입니다.|  
|[DataType 요소 &#40;ASSL&#41;](datatype-element-assl.md)|연결된 요소의 데이터 형식을 정의합니다.|  
|[DbSchemaName 요소 &#40;ASSL&#41;](dbschemaname-element-assl.md)|로 식별 된 테이블의 부모 요소에 사용 되는 스키마의 이름이 고 [DbTableName](dbtablename-element-assl.md) 요소입니다.|  
|[DbTableName 요소 &#40;ASSL&#41;](dbtablename-element-assl.md)|부모 요소가 바인딩된 테이블의 이름을 포함합니다.|  
|[요소를 기본 &#40;ASSL&#41;](default-element-assl.md)|`DrillThroughAction`이 기본 드릴스루 동작인지 여부를 결정합니다.|  
|[DefaultMeasure 요소 &#40;ASSL&#41;](defaultmeasure-element-assl.md)|`Cube` 또는 `Perspective` 요소에 대한 기본 측정값을 정의하는 MDX 언어 식을 포함합니다.|  
|[DefaultMember 요소 &#40;ASSL&#41;](defaultmember-element-assl.md)|부모 요소의 기본 멤버를 식별하는 MDX 식을 포함합니다.|  
|[DefaultScript 요소 &#40;ASSL&#41;](defaultscript-element-assl.md)|기본값을 식별 [MdxScript](../objects/mdxscript-element-assl.md) 요소에는 [MdxScripts](../collections/mdxscripts-element-assl.md) 컬렉션입니다.|  
|[DefaultValue 요소 &#40;ASSL&#41;](value-element-assl.md)|연결된 된 읽기 전용 기본 값이 포함 된 [ServerProperty](../objects/serverproperty-element-assl.md) 요소입니다.|  
|[DeniedSet 요소 &#40;ASSL&#41;](deniedset-element-assl.md)|연관된 특성에 대해 거부된 권한 목록을 정의하는 집합 식을 포함합니다.|  
|[DependsOnDimensionID 요소 &#40;ASSL&#41;](dependsondimensionid-element-assl.md)|부모 차원이 종속된 다른 차원의 ID를 포함합니다.|  
|[Description 요소 &#40;ASSL&#41;](description-element-assl.md)|부모 요소에 대한 설명을 포함합니다.|  
|[DimensionID 요소 &#40;ASSL&#41;](dimensionid-element-assl.md)|차원의 ID를 포함합니다.|  
|[DiscretizationBucketCount 요소 &#40;ASSL&#41;](discretizationbucketcount-element-assl.md)|불연속화할 버킷의 수를 포함합니다.|  
|[DiscretizationMethod 요소 &#40;ASSL&#41;](discretizationmethod-element-assl.md)|불연속화에 사용할 방법을 정의합니다.|  
|[DisplayFlag 요소 &#40;ASSL&#41;](displayflag-element-assl.md)|사용자 인터페이스 구성 요소가 연결된 `ServerProperty` 요소를 표시해야 하는지 여부를 나타내는 읽기 전용 힌트를 포함합니다.|  
|[DisplayFolder 요소 &#40;ASSL&#41;](displayfolder-element-assl.md)|부모 요소를 나열할 폴더를 지정합니다. 개발자 및 관리자용 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 응용 프로그램에서는 표시 폴더를 사용하여 여러 요소를 시각적으로 범주화할 수 있습니다.|  
|[Distribution 요소 &#40;ASSL&#41;](distribution-element-assl.md)|`MiningStructure` 요소의 열 내에서 스칼라 값이 분산되는 방법을 설명하는 공급자별 값을 포함합니다.|  
|[Edition 요소 &#40;ASSL&#41;](edition-element-assl.md)|인스턴스의 읽기 전용 버전을 포함 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 나타내는 [서버](../objects/server-element-assl.md) 요소입니다.|  
|[요소를 사용 하도록 설정 &#40;ASSL&#41;](enabled-element-assl.md)|부모 요소를 사용할 수 있는지 여부를 나타냅니다.|  
|[EndOfData 요소 &#40;ASSL&#41;](../objects/data-element-assl.md)|받은 데이터의 끝을 나타냅니다.는 [PushedDataSource](../data-type/datasource-data-type-assl.md) 요소입니다.|  
|[EstimatedCount 요소 &#40;ASSL&#41;](estimatedcount-element-assl.md)|특성의 예상 멤버 수를 포함합니다.|  
|[EstimatedPerformanceGain 요소 &#40;ASSL&#41;](estimatedperformancegain-element-assl.md)|파티션의 읽기 전용 예상 성능 향상률을 포함합니다.|  
|[EstimatedRows 요소 &#40;ASSL&#41;](estimatedrows-element-assl.md)|부모 요소가 나타내는 예상 행 수를 포함합니다.|  
|[EstimatedSize 요소 &#40;ASSL&#41;](estimatedsize-element-assl.md)|부모 요소의 읽기 전용 예상 크기(바이트)를 포함합니다.|  
|[EventID 요소 &#40;ASSL&#41;](eventid-element-assl.md)|고유 하 게 식별 하는 [이벤트](../objects/event-element-assl.md) 의 일환으로 캡처할 수 있는 요소는 `Trace` 요소입니다.|  
|[Expression 요소 &#40;ASSL&#41;](expression-element-assl.md)|부모 요소의 내용을 정의하는 MDX 식을 포함합니다.|  
|[Filter 요소 &#40;바인딩&#41; &#40;ASSL&#41;](filter-element-binding-assl.md)|부모 요소의 내용을 필터링하는 MDX 식을 포함합니다.|  
|[Filter 요소 &#40;추적&#41; &#40;ASSL&#41;](filter-element-trace-assl.md)|`Trace` 필터를 설명하는 XML 문서 조각을 포함합니다.|  
|[FirstDayOfWeek 요소 &#40;ASSL&#41;](firstdayofweek-element-assl.md)|`TimeBinding` 요소에 대한 주의 첫 번째 요일을 정의합니다.|  
|[FiscalFirstDayOfMonth 요소 &#40;ASSL&#41;](fiscalfirstdayofmonth-element-assl.md)|`TimeBinding` 요소에 대한 회계 월의 첫 번째 날을 정의합니다.|  
|[FiscalFirstMonth 요소 &#40;ASSL&#41;](fiscalfirstmonth-element-assl.md)|`TimeBinding` 요소에 대한 회계 기간의 첫 번째 월을 정의합니다.|  
|[FiscalYearName 요소 &#40;ASSL&#41;](fiscalyearname-element-assl.md)|`TimeBinding` 요소에 대한 회계 연도 이름의 명명 규칙을 정의합니다.|  
|[FontFlags 요소 &#40;ASSL&#41;](fontflags-element-assl.md)|`CalculationProperty` 또는 `Measure` 부모 요소의 글꼴 관련 표시 특성을 설명합니다.|  
|[FontName 요소 &#40;ASSL&#41;](fontname-element-assl.md)|`CalculationProperty` 또는 `Measure` 부모 요소의 글꼴 관련 표시 특성을 설명합니다.|  
|[FontSize 요소 &#40;ASSL&#41;](fontsize-element-assl.md)|`CalculationProperty` 또는 `Measure` 부모 요소의 글꼴 관련 표시 특성을 설명합니다.|  
|[ForceRebuildInterval 요소 &#40;ASSL&#41;](forcerebuildinterval-element-assl.md)|새로운 MOLAP(다차원 OLAP) 이미지가 사용 가능해질 때부터 MOLAP 이미징이 무조건 시작되기 전까지의 기간을 결정합니다.|  
|[ForeColor 요소 &#40;ASSL&#41;](forecolor-element-assl.md)|`CalculationProperty` 또는 `Measure` 부모 요소의 색 관련 표시 특성을 설명합니다.|  
|[요소의 서식을 지정 &#40;ASSL&#41;](format-element-assl.md)|`DataItem` 요소의 필수 형식을 포함합니다.|  
|[FormatString 요소 &#40;ASSL&#41;](formatstring-element-assl.md)|`CalculationProperty` 요소 또는 `Measure` 요소의 표시 형식을 설명합니다.|  
|[Goal 요소 &#40;ASSL&#41;](goal-element-assl.md)|`Kpi` 요소의 원하는 목표를 식별합니다.|  
|[GranularityAttributeID 요소 &#40;ASSL&#41;](granularityattributeid-element-assl.md)|부모와 연결 된 특성의 ID를 포함 [MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md) 데이터 형식입니다.|  
|[HideMemberIf 요소 &#40;ASSL&#41;](hidememberif-element-assl.md)|클라이언트 응용 프로그램에서 수준의 멤버를 숨길지 여부와 숨길 조건을 나타냅니다.|  
|[HierarchyID 요소 &#40;ASSL&#41;](hierarchyid-element-assl.md)|에 대 한 ID를 포함 한 [CubeHierarchy](../data-type/hierarchy-data-type-assl.md), [MeasureGroupHierarchy](../data-type/measuregrouphierarchy-data-type-assl.md), 또는 [PerspectiveHierarchy](../data-type/perspectivehierarchy-data-type-assl.md) 요소입니다.|  
|[HierarchyUniqueNameStyle 요소 &#40;ASSL&#41;](hierarchyuniquenamestyle-element-assl.md)|`CubeDimension` 내에 포함된 계층에 대해 고유한 이름이 생성되는 방식을 결정합니다.|  
|[ID 요소 &#40;ASSL&#41;](id-element-assl.md)|부모 요소의 고유 ID를 포함합니다.|  
|[IgnoreUnrelatedDimensions 요소 &#40;ASSL&#41;](../collections/dimensions-element-assl.md)|측정값 그룹과 관련이 없는 차원의 멤버가 쿼리에 포함될 때 관련이 없는 차원이 최상위로 강제되는지 결정합니다.|  
|[ImpersonationInfo 요소 &#40;ASSL&#41;](impersonationinfo-element-assl.md)|어셈블리에 액세스하거나 이를 실행할 때 가장 동작을 확인하는 데 사용되는 정보를 포함합니다.|  
|[ImpersonationInfoSecurity 요소 &#40;ASSL&#41;](impersonationinfosecurity-element-assl.md)|`ImpersonationInfo` 데이터 형식에 제공된 보안 자격 증명이 변경되었는지 여부를 나타내는 읽기 전용 값을 포함합니다.|  
|[ImpersonationMode 요소 &#40;ASSL&#41;](impersonationmode-element-assl.md)|`ImpersonationInfo` 데이터 형식에서 파생된 요소에 대한 가장 방법을 나타내는 값을 포함합니다.|  
|[InstanceSelection 요소 &#40;ASSL&#41;](instanceselection-element-assl.md)|목록의 예상 항목 수를 기반으로 항목 목록의 표시 방법을 제안하는 힌트를 클라이언트 응용 프로그램에 제공합니다.|  
|[IntermediateCubeDimensionID 요소 &#40;ASSL&#41;](intermediatecubedimensionid-element-assl.md)|참조 차원을 측정값 그룹에 연결하는 차원의 ID를 포함합니다.|  
|[IntermediateGranularityAttributeID 요소 &#40;ASSL&#41;](intermediategranularityattributeid-element-assl.md)|참조 차원을 중간 차원에 연결하는 데 사용되는 중간 큐브 차원에 있는 세분성 특성의 ID를 포함합니다.|  
|[InvalidXmlCharacters 요소 &#40;ASSL&#41;](invalidxmlcharacters-element-assl.md)|원본 데이터에 있는 잘못된 XML 문자에 대한 처리 방식을 지정합니다.|  
|[Invocation 요소 &#40;ASSL&#41;](invocation-element-assl.md)|`Action` 호출 방법을 지정합니다.|  
|[IsAggregatable 요소 &#40;ASSL&#41;](isaggregatable-element-assl.md)|지정 여부의 값은 [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md) 요소를 집계할 수 합니다.|  
|[IsKey 요소 &#40;ASSL&#41;](iskey-element-assl.md)|열이 `MiningStructure` 요소의 사례에 대한 키를 제공하는지 여부를 나타냅니다.|  
|[Isolation 요소 &#40;ASSL&#41;](isolation-element-assl.md)|파생 된 요소에 대 한 격리 수준을 나타냅니다는 [DataSource](../data-type/datasource-data-type-assl.md) 데이터 형식입니다.|  
|[KeyDuplicate 요소 &#40;ASSL&#41;](keyduplicate-element-assl.md)|처리 중 중복 키 오류가 발생하는 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]가 이러한 오류를 처리하는 방법을 결정합니다.|  
|[KeyErrorAction 요소 &#40;ASSL&#41;](keyerroraction-element-assl.md)|키에 오류가 발생하는 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]가 수행할 동작을 지정합니다.|  
|[KeyErrorLimit 요소 &#40;ASSL&#41;](keyerrorlimit-element-assl.md)|처리 중 허용 가능한 오류 수를 포함합니다.|  
|[KeyErrorLimitAction 요소 &#40;ASSL&#41;](keyerrorlimitaction-element-assl.md)|작업을 지정 하는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 지정 된 키 오류 수 하는 경우는 [KeyErrorLimit](keyerrorlimit-element-assl.md) 요소에 도달할 때.|  
|[KeyErrorLogFile 요소 &#40;ASSL&#41;](../objects/file-element-assl.md)|처리 오류를 기록할 파일 이름을 포함합니다.|  
|[KeyNotFound 요소 &#40;ASSL&#41;](keynotfound-element-assl.md)|참조 무결성 오류가 발생하는 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]가 반응하는 방식을 지정합니다.|  
|[KeyUniquenessGuarantee 요소 &#40;ASSL&#41;](keyuniquenessguarantee-element-assl.md)|특성 키와 해당 이름 간의 관계와 관련 특성에 대한 관계가 유효하도록 보장되는지 여부를 나타냅니다.|  
|[KpiID 요소 &#40;ASSL&#41;](kpiid-element-assl.md)|`Kpi` 요소와 `Perspective` 요소를 연결하는 ID를 포함합니다.|  
|[언어 요소 &#40;ASSL&#41;](language-element-assl.md)|부모 요소의 언어 식별자를 포함합니다.|  
|[LastProcessed 요소 &#40;ASSL&#41;](lastprocessed-element-assl.md)|부모 요소를 포함하는 데이터베이스가 마지막으로 처리된 시간을 나타내는 읽기 전용 타임스탬프를 포함합니다.|  
|[LastSchemaUpdate 요소 &#40;ASSL&#41;](lastschemaupdate-element-assl.md)|부모 요소의 읽기 전용 메타데이터 업데이트 타임스탬프를 포함합니다.|  
|[LastUpdate 요소 &#40;ASSL&#41;](lastupdate-element-assl.md)|연결된 `Database` 또는 데이터베이스에 포함된 주요 개체 중 하나가 마지막으로 변경된 시간을 나타내는 읽기 전용 타임스탬프를 포함합니다.|  
|[Latency 요소 &#40;ASSL&#41;](latency-element-assl.md)|가장 이른 알림과 MOLAP 이미지가 삭제된 시점 사이의 "유예 기간"을 정의합니다.|  
|[LogFileAppend 요소 &#40;ASSL&#41;](logfileappend-element-assl.md)|`Trace` 요소가 해당 로깅 출력을 기존 로그 파일에 추가할지, 아니면 기존 로그 파일을 덮어쓸지를 결정합니다.|  
|[LogFileName 요소 &#40;ASSL&#41;](logfilename-element-assl.md)|`Trace` 요소에 대한 로그 파일의 파일 이름을 포함합니다.|  
|[LogFileRollover 요소 &#40;ASSL&#41;](logfilerollover-element-assl.md)|지정의 로깅을 `Trace` 해야에 지정 된 최대 로그 파일 크기를 중지할지 또는 출력을 새 파일로 롤오버할 [LogFileSize](logfilesize-element-assl.md) 에 도달 합니다.|  
|[LogFileSize 요소 &#40;ASSL&#41;](logfilesize-element-assl.md)|최대 로그 파일 크기(MB)를 지정합니다.|  
|[ManagedProvider 요소 &#40;ASSL&#41;](managedprovider-element-assl.md)|`DataSource` 데이터 형식에서 파생된 요소에 사용되는 관리 공급자의 이름을 포함합니다.|  
|[ManufacturingExtraMonthQuarter 요소 &#40;ASSL&#41;](manufacturingextramonthquarter-element-assl.md)|`TimeBinding` 요소에 대한 추가 월이 할당된 제조 기간의 월을 정의합니다.|  
|[ManufacturingFirstMonth 요소 &#40;ASSL&#41;](manufacturingfirstmonth-element-assl.md)|`TimeBinding` 요소에 대한 첫 번째 제조 월을 정의합니다.|  
|[ManufacturingFirstWeekOfMonth 요소 &#40;ASSL&#41;](manufacturingfirstweekofmonth-element-assl.md)|`TimeBinding` 요소에 대한 제조 월의 첫 번째 주를 정의합니다.|  
|[MasterDatasourceID 요소 &#40;ASSL&#41;](masterdatasourceid-element-assl.md)|`Database` 요소의 마스터 데이터 원본 ID를 포함합니다.|  
|[Materialization 요소 &#40;ASSL&#41;](materialization-element-assl.md)|측정값 그룹과 참조 차원 간의 관계 유형을 나타냅니다.|  
|[MaxActiveConnections 요소 &#40;ASSL&#41;](maxactiveconnections-element-assl.md)|`DataSource` 데이터 형식에서 파생된 요소에 허용되는 최대 동시 연결 수를 포함합니다.|  
|[MdxMissingMemberMode 요소 &#40;ASSL&#41;](mdxmissingmembermode-element-assl.md)|MDX 문에 대해 누락된 멤버가 처리되는 방식을 결정합니다.|  
|[MeasureExpression 요소 &#40;ASSL&#41;](measureexpression-element-assl.md)|측정값을 정의하는 MDX 식을 포함합니다.|  
|[MeasureGroupID 요소 &#40;ASSL&#41;](measuregroupid-element-assl.md)|`MeasureGroup`을 부모 요소, 바인딩 또는 아웃오브 라인 바인딩과 연결합니다.|  
|[MeasureID 요소 &#40;ASSL&#41;](measureid-element-assl.md)|`Measure` 요소를 부모 요소와 연결합니다.|  
|[MeasureQualificaton 요소 &#40;ASSL&#41;](measurequalificaton-element-assl.md)|`MeasureGroup`의 측정값에 접두사를 적용할지 여부를 결정합니다.|  
|[MemberNamesUnique 요소 &#40;ASSL&#41;](membernamesunique-element-assl.md)|부모 요소의 멤버 이름이 고유해야 하는지 여부를 결정합니다.|  
|[MemberUniqueNameStyle 요소 &#40;ASSL&#41;](memberuniquenamestyle-element-assl.md)|`CubeDimension` 요소 내에 포함된 계층의 멤버에 대해 고유한 이름이 생성되는 방식을 결정합니다.|  
|[MembersWithData 요소 &#40;ASSL&#41;](memberswithdata-element-assl.md)|비-리프 멤버에 대한 데이터 멤버를 부모 특성에 표시할지 여부를 결정합니다.|  
|[MembersWithDataCaption 요소 &#40;ASSL&#41;](memberswithdatacaption-element-assl.md)|시스템 생성 데이터 멤버에 대한 캡션을 만드는 데 사용되는 템플릿 문자열을 제공합니다.|  
|[MimeType 요소 &#40;ASSL&#41;](mimetype-element-assl.md)|부모 `DataItem` 요소가 나타내는 데이터의 MIME(Multipurpose Internet Mail Extensions) 형식(적용 가능한 경우)을 포함합니다.|  
|[MiningModelID 요소 &#40;ASSL&#41;](miningmodelid-element-assl.md)|마이닝 모델을 데이터 마이닝 차원과 연결합니다.|  
|[Name 요소 &#40;ASSL&#41;](name-element-assl.md)|부모 요소의 이름을 포함합니다.|  
|[NamingTemplate 요소 &#40;ASSL&#41;](namingtemplate-element-assl.md)|`DimensionAttribute` 부모 요소에서 생성된 부모-자식 계층에서 수준의 이름이 지정되는 방식을 정의합니다.|  
|[NonEmptyBehavior 요소 &#40;ASSL&#41;](nonemptybehavior-element-assl.md)|`CalculationProperty` 요소의 부모와 연결된 비어 있지 않은 동작을 결정합니다.|  
|[NotificationTechnique 요소 &#40;ASSL&#41;](notificationtechnique-element-assl.md)|지정 여부 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 외부 클라이언트 응용 프로그램의 알림을 처리 합니다.|  
|[NullKeyConvertedToUnknown 요소 &#40;ASSL&#41;](nullkeyconvertedtounknown-element-assl.md)|Null 변환 오류가 발생할 때 수행할 동작을 지정합니다.|  
|[NullKeyNotAllowed 요소 &#40;ASSL&#41;](nullkeynotallowed-element-assl.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 처리 엔진이 처리 중 발생하는 Null 키 오류를 처리하는 방법을 결정합니다.|  
|[NullProcessing 요소 &#40;ASSL&#41;](nullprocessing-element-assl.md)|Null 값이 처리되는 방식을 정의합니다.|  
|[OnlineMode 요소 &#40;ASSL&#41;](onlinemode-element-assl.md)|캐시를 다시 작성하기 시작할 때 바로 데이터베이스를 다시 온라인 상태로 만들지, 아니면 캐시를 다시 작성한 후에만 데이터베이스를 다시 온라인 상태로 만들지를 지정합니다.|  
|[OptimizedState 요소 &#40;ASSL&#41;](state-element-assl.md)|계층에 적용되는 최적화 수준을 결정합니다.|  
|[Optionality 요소 &#40;ASSL&#41;](optionality-element-assl.md)|`AttributeRelationship` 요소에 대한 멤버의 옵션을 나타냅니다.|  
|[OrderBy 요소 &#40;ASSL&#41;](orderby-element-assl.md)|특성에 포함된 멤버의 정렬 방식을 설명합니다.|  
|[OrderByAttributeID 요소 &#40;ASSL&#41;](orderbyattributeid-element-assl.md)|멤버를 정렬 하는 기준인 다른 특성을 식별 된 [차원](../data-type/dimensionattribute-data-type-assl.md) 특성입니다.|  
|[Ordinal 요소 &#40;ASSL&#41;](ordinal-element-assl.md)|키 및 번역과 같은 컬렉션에서 바인딩할 서수를 나타냅니다.|  
|[OverrideBehavior 요소 &#40;ASSL&#41;](overridebehavior-element-assl.md)|`AttributeRelationship` 요소로 설명되는 관계의 재정의 동작을 나타냅니다.|  
|[PartitionID 요소 &#40;ASSL&#41;](partitionid-element-assl.md)|`Partition` 요소를 부모 요소, 바인딩 또는 아웃오브 라인 바인딩과 연결합니다.|  
|[Password 요소 &#40;ASSL&#41;](password-element-assl.md)|`ImpersonationInfo` 요소에 대한 사용자 계정의 암호를 포함합니다.|  
|[경로 요소 &#40;ASSL&#41;](path-element-assl.md)|인스턴스에서 제공 된 경로 포함 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], 사용 된 보고서의는 [ReportAction](../data-type/reportaction-data-type-assl.md) 요소입니다.|  
|[PendingValue 요소 &#40;ASSL&#41;](pendingvalue-element-assl.md)|연결된 `ServerProperty` 요소의 읽기 전용 보류 값을 포함합니다.|  
|[PermissionSet 요소 &#40;ASSL&#41;](permissionset-element-assl.md)|와 연결 된 권한 집합을 식별 한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 어셈블리입니다.|  
|[Persistence 요소 &#40;ASSL&#41;](persistence-element-assl.md)|바인딩된 원본 데이터의 어떤 부분에는 동적 이며 지정 된 빈도 사용 하 여 업데이트 확인 결정는 [RefreshPolicy](refreshpolicy-element-assl.md) 요소입니다.|  
|[요소를 처리할 &#40;ASSL&#41;](process-element-assl.md)|사용자가 부모 요소의 소유자를 처리할 수 있는지 여부를 결정합니다.|  
|[ProcessingMode 요소 &#40;ASSL&#41;](processingmode-element-assl.md)|인스턴스에서 인덱싱 및 집계를 처리 중에 수행할지 아니면 처리 후에 수행할지를 나타냅니다.|  
|[ProcessingPriority 요소 &#40;ASSL&#41;](processingpriority-element-assl.md)|지연 집계, 인덱싱 또는 클러스터링과 같은 백그라운드 작업을 수행하는 동안 부모 개체의 처리 우선 순위를 결정합니다.|  
|[ProcessingQuery 요소 &#40;ASSL&#41;](query-element-assl.md)|증분 처리 상태 알림을 위해 실행할 쿼리의 매개 변수가 있는 텍스트를 포함합니다.|  
|[ProductName 요소 &#40;ASSL&#41;](productname-element-assl.md)|`Server` 요소와 연결된 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스의 읽기 전용 제품 이름을 포함합니다.|  
|[쿼리 요소 &#40;ASSL&#41;](query-element-assl.md)|알림을 위해 실행할 쿼리의 텍스트를 포함합니다.|  
|[QueryDefinition 요소 &#40;ASSL&#41;](querydefinition-element-assl.md)|와 연결 된 쿼리에 대 한 불투명 식을 포함 한 `DataSource` 요소에는 [QueryBinding](../data-type/querybinding-data-type-assl.md) 요소입니다.|  
|[요소를 읽을 &#40;ASSL&#41;](read-element-assl.md)|데이터 또는 메타 데이터에 대 한 읽을 수 있는지 여부를 결정 한 주어진 [CubeDimensionPermission](../data-type/permission-data-type-assl.md) 또는 [권한](../data-type/permission-data-type-assl.md) 요소입니다.|  
|[ReadDefinition 요소 &#40;ASSL&#41;](readdefinition-element-assl.md)|멤버가 데이터베이스의 정의 또는 데이터베이스의 개체 정의를 읽을 수 있는지 여부를 결정합니다.|  
|[ReadSourceData 요소 &#40;ASSL&#41;](readsourcedata-element-assl.md)|`CubePermission` 내에 포함된 계층에 대해 고유한 이름이 생성되는 방식을 결정합니다.|  
|[RefreshInterval 요소 &#40;ASSL&#41;](refreshinterval-element-assl.md)|부모 요소와 연결된 바인딩된 데이터를 새로 고치는 간격을 지정합니다.|  
|[RefreshPolicy 요소 &#40;ASSL&#41;](refreshpolicy-element-assl.md)|빈도 결정 차원 또는 측정값 그룹의 동적 부분 (에 지정 된 대로 [지 속성](persistence-element-assl.md) 요소)의 변경 사항을 검사 합니다.|  
|[RelationshipType 요소 &#40;ASSL&#41;](relationshiptype-element-assl.md)|`AttributeRelationship`에 대한 멤버 관계를 변경할 수 있는지 여부를 나타냅니다.|  
|[RemoteDatasourceID 요소 &#40;ASSL&#41;](remotedatasourceid-element-assl.md)|원격 파티션을 저장하는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스를 가리키는 OLAP 데이터 원본의 ID를 지정합니다.|  
|[ReportingFirstMonth 요소 &#40;ASSL&#41;](reportingfirstmonth-element-assl.md)|`TimeBinding` 요소에 대한 첫 번째 보고 월을 정의합니다.|  
|[ReportingFirstWeekOfMonth 요소 &#40;ASSL&#41;](reportingfirstweekofmonth-element-assl.md)|`TimeBinding` 요소에 대한 보고 월의 첫 번째 주를 정의합니다.|  
|[ReportingWeekToMonthPattern 요소 &#40;ASSL&#41;](reportingweektomonthpattern-element-assl.md)|`TimeBinding` 요소에 대한 보고 주-월 패턴을 정의합니다.|  
|[ReportServer 요소 &#40;ASSL&#41;](reportserver-element-assl.md)|`ReportAction`에 사용되는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
|[RequiresRestart 요소 &#40;ASSL&#41;](requiresrestart-element-assl.md)|서버 속성 값을 변경한 후 변경 내용을 적용하기 위해 해당 인스턴스를 다시 시작해야 하는지 여부를 확인하는 `ServerProperty` 요소와 연결된 읽기 전용 값을 포함합니다.|  
|[RoleID 요소 &#40;ASSL&#41;](roleid-element-assl.md)|정의된 권한에 대한 역할을 식별합니다.|  
|[루트 요소를 &#40;ASSL&#41;](root-element-assl.md)|데이터 원본의 데이터(행 집합)를 포함합니다.|  
|[RootMemberIf 요소 &#40;ASSL&#41;](rootmemberif-element-assl.md)|부모 특성의 멤버 또는 루트 멤버를 식별하는 방법을 결정합니다.|  
|[스키마 요소 &#40;ASSL&#41;](schema-element-assl.md)|데이터 원본 뷰의 스키마를 포함합니다.|  
|[ScriptCacheProcessingMode 요소 &#40;ASSL&#41;](scriptcacheprocessingmode-element-assl.md)|서버에서 스크립트 캐시를 처리 중에 작성할지, 아니면 처리 후에 작성할지를 나타냅니다.|  
|[SilenceInterval 요소 &#40;ASSL&#41;](silenceinterval-element-assl.md)|MOLAP 이미징 처리를 시작하기 전에 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스를 일시 중지하는 최소 시간을 정의합니다.|  
|[SilenceOverrideInterval 요소 &#40;ASSL&#41;](silenceoverrideinterval-element-assl.md)|MOLAP 이미징을 무조건 시작하기 전에 초기 알림을 받은 후 경과해야 하는 시간을 정의합니다.|  
|[Slice 요소 &#40;ASSL&#41;](slice-element-assl.md)|파티션에 포함된 조각을 정의하는 MDX 식을 포함합니다.|  
|[SolveOrder 요소 &#40;ASSL&#41;](solveorder-element-assl.md)|계산 멤버 또는 계산 셀 정의에 `CalculationProperty` 요소가 적용되는 계산 순서를 나타냅니다.|  
|[Source 요소 &#40;바인딩&#41; &#40;ASSL&#41;](source-element-binding-assl.md)|부모 요소가 바인딩된 데이터의 원본을 식별합니다.|  
|[Source 요소 &#40;ComAssembly&#41; &#40;ASSL&#41;](source-element-comassembly-assl.md)|COM(구성 요소 개체 모델) 구성 요소의 파일 이름 또는 ProgID(프로그래밍 식별자)를 포함합니다.|  
|[Source 요소 &#40;측정값&#41; &#40;ASSL&#41;](source-element-measure-assl.md)|`Measure` 요소의 값을 포함하는 원본에 대한 세부 정보를 포함합니다.|  
|[SourceAttributeID 요소 &#40;ASSL&#41;](sourceattributeid-element-assl.md)|원본 특성 ID가 포함 된 [수준](../objects/level-element-assl.md) 요소의 기반이 되 합니다.|  
|[SourceColumnID 요소 &#40;ASSL&#41;](sourcecolumnid-element-assl.md)|상위 `MiningStructure` 요소에 있는 원본 마이닝 구조 열의 ID를 포함합니다.|  
|[상태 요소 &#40;ASSL&#41;](state-element-assl.md)|부모 요소의 현재 처리 상태를 나타내는 읽기 전용 값을 포함합니다.|  
|[Status 요소 &#40;ASSL&#41;](status-element-assl.md)|`Kpi` 요소에 대한 상태 표시를 반환하는 MDX 식을 포함합니다.|  
|[StatusGraphic 요소 &#40;ASSL&#41;](statusgraphic-element-assl.md)|`Kpi` 요소의 상태에 대해 권장되는 그래픽 표현을 포함합니다.|  
|[StopTime 요소 &#40;ASSL&#41;](stoptime-element-assl.md)|`Trace` 요소를 중지할 날짜 및 시간을 지정합니다.|  
|[StorageLocation 요소 &#40;ASSL&#41;](storagelocation-element-assl.md)|부모 요소의 내용에 대한 파일 시스템 저장소 위치를 포함합니다.|  
|[StorageMode 요소 &#40;ASSL&#41;](storagemode-element-assl.md)|부모 요소의 저장소 모드를 결정합니다.|  
|[TableID 요소 &#40;ASSL&#41;](tableid-element-assl.md)|부모 요소와 연결된 `DataSourceView` 요소의 테이블 ID를 포함합니다.|  
|[요소를 대상 &#40;ASSL&#41;](target-element-assl.md)|`Action` 요소의 대상을 식별합니다.|  
|[TargetType 요소 &#40;ASSL&#41;](targettype-element-assl.md)|식별 된 항목의 유형을 식별 된 [대상](target-element-assl.md) 요소입니다.|  
|[텍스트 요소 &#40;ASSL&#41;](text-element-assl.md)|텍스트를 포함 한 [명령](../objects/command-element-assl.md) 요소입니다.|  
|[Timeout 요소 &#40;ASSL&#41;](timeout-element-assl.md)|데이터 검색 시도의 제한 시간(초)을 지정합니다.|  
|[요소 추세 &#40;ASSL&#41;](trend-element-assl.md)|`Kpi` 요소에 대한 추세 표시를 반환하는 MDX 식을 포함합니다.|  
|[TrendGraphic 요소 &#40;ASSL&#41;](trendgraphic-element-assl.md)|`Kpi` 요소의 추세에 대해 권장되는 그래픽 표현을 포함합니다.|  
|[Trimming 요소 &#40;ASSL&#41;](trimming-element-assl.md)|데이터 원본의 데이터가 잘리는 방법을 지정합니다.|  
|[E Element &#40;동작&#41; &#40;ASSL&#41;](type-element-action-assl.md)|`Action` 요소의 유형을 포함합니다.|  
|[E Element &#40;바인딩&#41; &#40;ASSL&#41;](type-element-binding-assl.md)|특성 바인딩의 유형을 포함합니다.|  
|[E Element &#40;ClrAssemblyFile&#41; &#40;ASSL&#41;](type-element-clrassemblyfile-assl.md)|.NET Framework 어셈블리에 속하는 파일 중 하나의 파일 유형을 지정 합니다.|  
|[E Element &#40;차원&#41; &#40;ASSL&#41;](type-element-dimension-assl.md)|차원의 내용에 대한 정보를 제공합니다.|  
|[E Element &#40;DimensionAttribute&#41; &#40;ASSL&#41;](type-element-dimensionattribute-assl.md)|특성의 유형을 포함합니다.|  
|[E Element &#40;MeasureGroup&#41; &#40;ASSL&#41;](type-element-measuregroup-assl.md)|`MeasureGroup`의 유형을 지정합니다.|  
|[E Element &#40;MeasureGroupAttribute&#41; &#40;ASSL&#41;](type-element-measuregroupattribute-assl.md)|형식을 포함 한 [MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md) 요소입니다.|  
|[E Element &#40;MiningStructureColumn&#41; &#40;ASSL&#41;](type-element-miningstructurecolumn-assl.md)|유형을 포함 된 [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) 요소입니다.|  
|[E Element &#40;파티션&#41; &#40;ASSL&#41;](type-element-partition-assl.md)|`Partition` 요소의 유형을 포함합니다.|  
|[E Element &#40;PerspectiveCalculation&#41; &#40;ASSL&#41;](type-element-perspectivecalculation-assl.md)|유형을 나타냅니다는 [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md) 요소입니다.|  
|[UnknownMember 요소 &#40;ASSL&#41;](unknownmember-element-assl.md)|알 수 없는 멤버의 표시 여부를 나타냅니다.|  
|[UnknownMemberName 요소 &#40;ASSL&#41;](unknownmembername-element-assl.md)|차원의 알 수 없는 멤버에 대한 캡션을 차원의 기본 언어로 포함합니다.|  
|[Usage 요소 &#40;DimensionAttribute&#41; &#40;ASSL&#41;](usage-element-dimensionattribute-assl.md)|특성의 사용 방식을 설명합니다.|  
|[Usage 요소 &#40;MiningModelColumn&#41; &#40;ASSL&#41;](usage-element-miningmodelcolumn-assl.md)|부모 `MiningStructure`에 있는 연결된 열의 사용 방식을 설명합니다.|  
|[요소 값 &#40;ASSL&#41;](value-element-assl.md)|부모 요소의 값을 포함합니다.|  
|[버전 요소 &#40;ASSL&#41;](version-element-assl.md)|`Server` 요소가 나타내는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스의 읽기 전용 버전 번호를 포함합니다.|  
|[Visibility 요소 &#40;ASSL&#41;](visibility-element-assl.md)|표시 유형을 정의 [주석](../objects/annotation-element-assl.md) 요소입니다.|  
|[Visible 요소 &#40;ASSL&#41;](visible-element-assl.md)|부모 요소의 표시 유형을 결정합니다.|  
|[VisualTotals 요소 &#40;ASSL&#41;](visualtotals-element-assl.md)|이 특성의 멤버에 대해 보이는 값 합계를 표시할지 여부를 확인하는 MDX 식을 포함합니다.|  
|[Write 요소 &#40;ASSL&#41;](write-element-assl.md)|지정된 `CubeDimensionPermission` 또는 `Permission` 요소에 대해 데이터 또는 메타데이터를 쓸 수 있는지 여부를 결정합니다.|  
|[WriteEnabled 요소 &#40;ASSL&#41;](writeenabled-element-assl.md)|보안 권한에 따라 차원 쓰기 저장(writeback)을 사용할 수 있는지 여부를 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 요소 계층 &#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  