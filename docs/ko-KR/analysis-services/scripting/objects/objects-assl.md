---
title: 개체 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- ASSL, objects
- objects [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
ms.assetid: 0f672b93-c317-47e5-b44d-ecea9b587c98
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d45d482ecb50e0215b9d0ad5d57f537e8899d5c5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="objects-assl"></a>개체(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  이 참조 섹션에서는 ASSL(Analysis Services Scripting Language) 스키마에서 개체로 사용되는 각 요소에 대한 구문 및 사용 정보를 제공합니다.  
  
 ASSL 스키마는 개발자의 관점에서 XML 요소만 포함 하지만이 섹션에 설명 된 요소에 해당 개체와 같은 **데이터베이스**, **큐브**, 및  **차원** 의 인스턴스에서 포함 된 개체의 계층 구조에서 개체 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
 개체는 ASSL 스키마에서 리프 수준 요소가 아니지만 자식 요소 및 개체 속성에 해당하는 요소를 갖습니다.  
  
 속성으로 나타날 수 있는 스키마의 리프 수준 요소가 개체 유형이어서 개체로 분류되는 경우도 있습니다. 예를 들어는 **소스** 의 **차원** 형식의 개체는 **DimensionBinding**합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|요소|Description|  
|-------------|-----------------|  
|[요소 계정 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/account-element-assl.md)|내의 계정 유형에 대 한 세부 정보를 포함 한 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[Action 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/action-element-assl.md)|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소 또는 [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소에서 사용 가능한 동작에 대한 정보를 포함합니다.|  
|[Aggregation 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)|에 대 한 단일 집계를 정의 [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md) 요소입니다.|  
|[AggregationDesign 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)|데이터베이스의 여러 파티션에서 공유할 수 있는 집계 정의의 집합을 정의합니다.|  
|[AggregationInstance 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|파티션에 대한 집계 인스턴스를 정의합니다.|  
|[AlgorithmParameter 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|사용 하는 알고리즘에 대 한 매개 변수 정의 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) 요소입니다.|  
|[AllMemberTranslation 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/allmembertranslation-element-assl.md)|All 멤버의 캡션에 대 한 번역을 포함 한 [계층](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) 요소입니다.|  
|[주석 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/annotation-element-assl.md)|ASSL 스키마를 확장하는 데 사용되는 요소를 포함합니다.|  
|[Assembly 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)|나타냅니다는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 어셈블리 또는 연결 된 COM 동적 연결 라이브러리 (DLL)는 [서버](../../../analysis-services/scripting/objects/server-element-assl.md) 요소 또는 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[요소 특성 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attribute-element-assl.md)|특성에 대한 설명을 포함합니다.|  
|[AttributeAllMemberTranslation 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attributeallmembertranslation-element-assl.md)|All 멤버의 캡션에 대 한 번역을 포함 한 [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) 요소입니다.|  
|[AttributePermission 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|사용 권한을 해당 멤버의 정의 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 내 개별 차원의 특성에 있는 요소는 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.|  
|[AttributeRelationship 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|두 특성 간의 관계에 대한 세부 정보를 제공합니다.|  
|[요소를 차단 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/block-element-assl.md)|전체 또는 일부의 이진 내용을 포함 한 [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) 요소입니다.|  
|[Calculation 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/calculation-element-assl.md)|와 연결 된 계산을 [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소입니다.|  
|[CalculationProperty 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)|사용 되는 계산에 대 한 사용자 인터페이스 속성의 컬렉션을 포함 한 [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) 요소입니다.|  
|[CaptionColumn 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md)|특성의 캡션을 제공하는 열을 정의합니다.|  
|[CellPermission 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)|멤버는 사용 권한을 설명는 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 요소 내의 개별 셀에 있는 한 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.|  
|[Column 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/column-element-assl.md)|부모 요소와 연결된 열의 컬렉션에 있는 열을 설명합니다.|  
|[Command 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/command-element-assl.md)|Commands 컬렉션의 부모 요소 컨텍스트 내에서 사용할 수 있는 명령을 정의합니다.|  
|[큐브 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)|일반, 가상 또는 연결 된 큐브를 정의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[CubePermission 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)|특정 멤버의 사용 권한을 정의 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 요소의 특정 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.|  
|[CustomRollupColumn 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)|사용자 지정 롤업 수식을 제공하는 열의 세부 정보를 정의합니다.|  
|[CustomRollupPropertiesColumn 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md)|사용자 지정 롤업 수식의 속성을 제공하는 열의 세부 정보를 정의합니다.|  
|[데이터 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/data-element-assl.md)|포함 된 (자식 컬렉션에 **블록** 요소)의 이진 내용을 [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) 요소입니다.|  
|[Database 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스를 정의합니다.|  
|[DatabasePermission 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)|기본 사용 권한을 정의 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소는 특정 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 요소입니다.|  
|[DataSource 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/datasource-element-assl.md)|데이터 원본을 정의 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[DataSourcePermission 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/datasourcepermission-element-assl.md)|기본 사용 권한을 정의 [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) 는 특정 데이터 형식을 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 요소입니다.|  
|[DataSourceView 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)|사용 하는 데이터 원본 뷰 정의 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.|  
|[요소를 차원 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)|차원을 정의합니다.|  
|[DimensionPermission 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|특정 데이터베이스 차원 또는 큐브 차원에 대해 특정 [Role](../../../analysis-services/scripting/objects/role-element-assl.md) 요소에 속하는 사용 권한을 정의합니다.|  
|[ErrorConfiguration 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|부모 요소가 처리될 때 발생할 수 있는 오류 처리에 대한 설정을 지정합니다.|  
|[Event 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/event-element-assl.md)|일부로 캡처할 이벤트 정의 [추적](../../../analysis-services/scripting/objects/trace-element-assl.md) 요소입니다.|  
|[파일 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/file-element-assl.md)|구성 하는 파일 중 하나를 정의 [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) 요소입니다.|  
|[ForeignKeyColumn 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md)|관계형 데이터 원본에 대한 부모 테이블로의 조인을 식별합니다.|  
|[요소 그룹화 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/group-element-assl.md)|특성에 바인딩되는 멤버 그룹을 정의합니다.|  
|[Hierarchy 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|차원의 계층을 정의합니다.|  
|[IncrementalProcessingNotification 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md)|에 대 한 정보가 포함 되어는 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 증분 처리의 진행률을 확인 하기 위해 실행할 쿼리에 대 한 요소입니다.|  
|[KeyColumn 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|특성의 키 또는 키의 일부인 열의 정의를 포함합니다.|  
|[Kpi 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/kpi-element-assl.md)|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소 또는 [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소 내에서 KPI(핵심 성과 지표)를 정의합니다.|  
|[수준 요소가 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/level-element-assl.md)|수준을 정의 [계층](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) 요소입니다.|  
|[MdxScript 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|연결 된 MDX (Multidimensional Expressions) 스크립트에 대 한 정보를 포함 한 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.|  
|[요소를 측정 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measure-element-assl.md)|측정값을 정의합니다.|  
|[MeasureGroup 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|동일한 세분성 수준에서 측정값 집합을 정의합니다.|  
|[Member 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/member-element-assl.md)|[Group](../../../analysis-services/scripting/objects/group-element-assl.md) 요소 멤버 또는 [Role](../../../analysis-services/scripting/objects/role-element-assl.md) 요소 멤버의 이름을 포함합니다.|  
|[MiningModel 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|단일 데이터 마이닝 모델을 정의합니다.|  
|[MiningModelPermission 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)|사용 권한 멤버를 정의 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 요소 가지는 개별 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) 요소입니다.|  
|[MiningStructure 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|마이닝 모델 집합에 대한 구조를 정의합니다.|  
|[MiningStructurePermission 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|사용 권한을 해당 멤버의 정의 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 요소 가지는 개별 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 요소입니다.|  
|[ModelingFlag 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/modelingflag-element-assl.md)|마이닝 구조 또는 마이닝 모델의 열에 대한 모델링 플래그를 포함합니다.|  
|[NameColumn 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|부모 요소의 이름을 제공하는 열을 식별합니다.|  
|[NamingTemplateTranslation 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/namingtemplatetranslation-element-assl.md)|지역화 된 번역을 제공 된 **NamingTemplate** 요소는 부모에 대 한 [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) 데이터 형식입니다.|  
|[요소를 파티션 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|파티션을 정의 [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) 요소 또는의-라인 파티션 바인딩을 [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)요소입니다.|  
|[Perspective 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/perspective-element-assl.md)|큐브 뷰에 대 한 세부 정보를 정의 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.|  
|[ProactiveCaching 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|부모 요소에 대한 자동 관리 캐싱 설정을 정의합니다.|  
|[QueryNotification 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/querynotification-element-assl.md)|에 대 한 정보가 포함 되어는 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 데이터 원본이 수정 되었는지 여부를 확인 하기 위해 실행할 쿼리에 대 한 요소입니다.|  
|[ReportFormatParameter 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)|이름 및 지정 하는 매개 변수 값을 포함 방법을 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서가 런타임에 서식이 지정 됩니다.|  
|[ReportParameter 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)|런타임에 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서로 전달되는 매개 변수의 이름 및 값을 포함합니다.|  
|[Role 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/role-element-assl.md)|보안 역할에 대한 정보를 포함합니다.|  
|[서버 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/server-element-assl.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스를 설명합니다.|  
|[ServerProperty 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|와 연결 된 서버 속성을 정의 [서버](../../../analysis-services/scripting/objects/server-element-assl.md) 요소입니다.|  
|[SkippedLevelsColumn 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md)|각 멤버와 해당 부모 간의 건너뛴(빈) 수준 수를 저장하는 열의 세부 정보를 제공합니다.|  
|[SourceMeasureGroup 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)|마이닝 구조 열의 데이터 원본으로 사용되는 측정값 그룹을 나타냅니다.|  
|[TableNotification 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|에 대 한 정보가 포함 되어는 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 의 수정 된 데이터 원본 뷰나 테이블에 대 한 요소입니다.|  
|[Trace 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/trace-element-assl.md)|쿼리할 수 있는 추적을 정의합니다.|  
|[Translation 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)|[Translations](../../../analysis-services/scripting/collections/translations-element-assl.md) 컬렉션의 부모에 대해 지역화된 번역을 제공합니다.|  
|[UnaryOperatorColumn 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md)|단항 연산자를 제공하는 열의 세부 정보를 정의합니다.|  
|[UnknownMemberTranslation 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md)|캡션에 대 한 번역을 포함 된 [UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md) 에 대 한 요소는 [차원](../../../analysis-services/scripting/objects/dimension-element-assl.md) 요소입니다.|  
|[ValueColumn 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/valuecolumn-element-assl.md)|부모 요소의 값을 제공하는 열을 식별합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services Scripting Language XML 요소 계층 & #40; ASSL & #41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
