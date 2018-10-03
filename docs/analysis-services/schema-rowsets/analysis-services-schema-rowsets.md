---
title: Analysis Services 스키마 행 집합 | Microsoft Docs
ms.date: 10/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4ec9d6c75ef1d3cdc8effdc44861eed5971ced60
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116683"
---
# <a name="analysis-services-schema-rowsets"></a>Analysis Services 스키마 행 집합
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  스키마 행 집합은 데이터베이스 스키마, 활성 세션, 연결, 명령 및 서버에서 실행 중인 작업을 비롯한 Analysis Services 개체 및 서버 상태에 대한 정보를 포함하는 미리 정의된 테이블입니다. SQL Server Management Studio의 XML/A 스크립트 창에서 스키마 행 집합 테이블을 쿼리하거나, 스키마 행 집합에 대해 DMV 쿼리를 실행하거나, 스키마 행 집합 정보를 포함하는 사용자 지정 응용 프로그램(예: 보고서를 만드는 데 사용할 수 있는 사용 가능한 차원의 목록을 검색하는 보고 응용 프로그램)을 만들 수 있습니다.  
  
> [!NOTE]  
>  XML/a에서 스키마 행 집합을 사용 하는 경우 스크립트에서 반환 되는 정보는 *결과* 의 매개 변수를 [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드가 설명 하는 행 집합 열 레이아웃에 따라 구조화 됩니다 섹션입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] XMLA(XML for Analysis) 공급자는 XML for Analysis 사양에 필요한 행 집합을 지원합니다. 또한 XMLA 공급자는 OLE DB, OLAP용 OLE DB, 데이터 마이닝용 OLE DB 데이터 원본 공급자에 대한 표준 스키마 행 집합도 일부 지원합니다. 다음 항목에서는 지원되는 행 집합에 대해 설명합니다.  

스키마 행 집합은 두 개의 SQL Server Analysis Services 프로토콜에서 설명 되어 있습니다.   

[[MS-SSAS-T]: SQL Server Analysis Services 테이블 형식 프로토콜](https://msdn.microsoft.com/library/mt719260) -1200 이상 호환성 수준의 테이블 형식 모델에 대 한 스키마 행 집합에 설명 합니다.

[[MS-SSAS]: SQL Server Analysis Services 프로토콜](https://msdn.microsoft.com/library/ee320606) -1100 및 1103 호환성 수준 테이블 형식 모델과 다차원 모델에 대 한 스키마 행 집합에 설명 합니다.

## <a name="rowsets-described-in-the-ms-ssas-t-sql-server-analysis-services-tabular-protocol"></a>행 집합 [MS-SSAS-T]에 설명 된: SQL Server Analysis Services 테이블 형식 프로토콜

|행 집합  |Description  |
|---------|---------|
|[TMSCHEMA_ANNOTATIONS](https://msdn.microsoft.com/library/mt704370)|주석 개체 모델에 대 한 정보를 제공 합니다.|
|[TMSCHEMA_ATTRIBUTE_HIERARCHIES](https://msdn.microsoft.com/library/mt704362)     |   열에 대해 AttributeHierarchy 개체에 대 한 정보를 제공합니다.      |
|[TMSCHEMA_COLUMNS](https://msdn.microsoft.com/library/mt704373)    |  각 테이블의 열 개체에 대 한 정보를 제공합니다.       |
|[TMSCHEMA_COLUMN_PERMISSIONS](https://msdn.microsoft.com/library/mt842440)|각 테이블 권한 ColumnPermission 개체에 대 한 정보를 제공합니다.|
|[TMSCHEMA_CULTURES](https://msdn.microsoft.com/library/mt719125)|모델의 Culture 개체에 대 한 정보를 제공합니다.|
|[TMSCHEMA_DATA_SOURCES](https://msdn.microsoft.com/library/mt719191)   |   모델의 데이터 원본 개체에 대 한 정보를 제공합니다.      |
|[TMSCHEMA_DETAIL_ROWS_DEFINITIONS](https://msdn.microsoft.com/library/mt825017)|DetailRowsDefinition 개체 모델에 대 한 정보를 제공 합니다.|
|[TMSCHEMA_EXPRESSIONS](https://msdn.microsoft.com/library/mt825015)|식은 개체 모델에 대 한 정보를 제공 합니다.|
|[TMSCHEMA_EXTENDED_PROPERTIES](https://msdn.microsoft.com/library/mt842451)|ExtendedProperty 개체 모델에 대 한 정보를 제공 합니다.|
|[TMSCHEMA_HIERARCHIES](https://msdn.microsoft.com/library/mt719136)    |    각 테이블의 계층 개체에 대 한 정보를 제공합니다.     |
|[TMSCHEMA_KPIS](https://msdn.microsoft.com/library/mt719002)     |    모델에서 KPI 개체에 대 한 정보를 제공합니다.     |
|[TMSCHEMA_LEVELS](https://msdn.microsoft.com/library/mt719038)     |   각 계층의 수준 개체에 대 한 정보를 제공합니다.      |
|[TMSCHEMA_LINGUISTIC_METADATA](https://msdn.microsoft.com/library/mt719169)|특정 문화권에 대 한 모델의 개체에 대 한 동의어에 대 한 정보를 제공합니다.|
|[TMSCHEMA_MEASURES](https://msdn.microsoft.com/library/mt719218)     |    각 테이블의 측정값 개체에 대 한 정보를 제공합니다.     |
|[TMSCHEMA_MODEL](https://msdn.microsoft.com/library/mt719042)    |  데이터베이스에서 모델 개체를 지정합니다.       |
|[TMSCHEMA_OBJECT_TRANSLATIONS](https://msdn.microsoft.com/library/mt719119)|문화권에 대 한 다른 개체의 번역에 대 한 정보를 제공합니다.|
|[TMSCHEMA_PARTITIONS](https://msdn.microsoft.com/library/mt704375)     |     각 테이블의 파티션 개체에 대 한 정보를 제공합니다.    |
|[TMSCHEMA_PERSPECTIVE_COLUMNS](https://msdn.microsoft.com/library/mt719164)     |   PerspectiveColumn 개체 각 PerspectiveTable 개체에 대 한 정보를 제공 합니다.      |
|[TMSCHEMA_PERSPECTIVE_HIERARCHIES](https://msdn.microsoft.com/library/mt719104)     |  PerspectiveHierarchy 개체 각 PerspectiveTable 개체에 대 한 정보를 제공 합니다.       |
|[TMSCHEMA_PERSPECTIVE_MEASURES](https://msdn.microsoft.com/library/mt719135)     |    PerspectiveMeasure 개체 각 PerspectiveTable 개체에 대 한 정보를 제공 합니다.     |
|[TMSCHEMA_PERSPECTIVE_TABLES](https://msdn.microsoft.com/library/mt719272)     |    큐브 뷰 테이블 개체에 대 한 정보를 제공합니다.     |
|[TMSCHEMA_PERSPECTIVES](https://msdn.microsoft.com/library/mt704340)     |     모델의 큐브 뷰 개체에 대 한 정보를 제공합니다.    |
|[TMSCHEMA_RELATIONSHIPS](https://msdn.microsoft.com/library/mt704355)     |    모델에서 관계 개체에 대 한 정보를 제공합니다.     |
|[TMSCHEMA_ROLE_MEMBERSHIPS](https://msdn.microsoft.com/library/mt704584)     |  각 역할의 RoleMembership 개체에 대 한 정보를 제공합니다.      |
|[TMSCHEMA_ROLES](https://msdn.microsoft.com/library/mt719267)    |   모델 역할 개체에 대 한 정보를 제공합니다.      |
|[TMSCHEMA_TABLE_PERMISSIONS](https://msdn.microsoft.com/library/mt704347)    |    각 역할의 TablePermission 개체에 대 한 정보를 제공합니다.     |
|[TMSCHEMA_TABLES](https://msdn.microsoft.com/library/mt719250)     |   모델에서 테이블 개체에 대 한 정보를 제공합니다.      |
|[TMSCHEMA_VARIATIONS](https://msdn.microsoft.com/library/mt825008)|각 열에 있는 변형 개체에 대 한 정보를 제공합니다.|

## <a name="rowsets-described-in-the-ms-ssas-sql-server-analysis-services-protocol"></a>행 집합 [MS-SSAS]에 설명 된: SQL Server Analysis Services 프로토콜

|행 집합|Description|  
|------------|-----------------|  
|[DBSCHEMA_CATALOGS](https://msdn.microsoft.com/library/ee302115)|서버에 액세스할 수 있는 카탈로그를 설명 합니다.|  
|[DBSCHEMA_COLUMNS](https://msdn.microsoft.com/library/ee301789)|각 측정값, 각 큐브 차원의 특성 및 열으로 노출 된 각 스키마 행 집합 열에 대 한 행을 반환 합니다.|  
|[DBSCHEMA_PROVIDER_TYPES](https://msdn.microsoft.com/library/ee301696)|서버에서 지 원하는 기본 데이터 형식을 식별 합니다.|  
|[DBSCHEMA_TABLES](https://msdn.microsoft.com/library/ee320843)|차원, 측정값 그룹 또는 테이블 처럼 노출 하는 스키마 행 집합을 반환 합니다.|  
|[DISCOVER_CALC_DEPENDENCY](https://msdn.microsoft.com/library/hh770226)| 테이블 형식 데이터베이스 또는 테이블 형식 데이터베이스에 대해 실행 되는 DAX 쿼리에서 지정 된 개체에 대 한 계산 종속성에 대 한 정보를 반환 합니다. |  
|[DISCOVER_COMMAND_OBJECTS](https://msdn.microsoft.com/library/ee320662)|참조된 명령에서 사용 중인 개체에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_COMMANDS](https://msdn.microsoft.com/library/ee320715)|서버에 열려 있는 연결의 현재 실행 중이거나 마지막으로 실행된 명령에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_CONNECTIONS](https://msdn.microsoft.com/library/ee301889)|서버에서 현재 열린 연결에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_CSDL_METADATA](https://msdn.microsoft.com/library/gg587670)|메모리 내 데이터베이스에 대 한 데이터베이스 메타 데이터에 대 한 정보를 반환합니다.|  
|[DISCOVER_DATASOURCES](https://msdn.microsoft.com/library/ee320285)|서버에서 사용할 수 있는 데이터 원본의 목록을 반환 합니다.|
|[DISCOVER_DB_CONNECTIONS](https://msdn.microsoft.com/library/ee320467)|서버에서 현재 열린 데이터베이스 연결에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_DIMENSION_STAT](https://msdn.microsoft.com/library/ee320284)|지정된 된 차원에 통계를 반환합니다.|  
|[DISCOVER_ENUMERATORS](https://msdn.microsoft.com/library/ee302012)|특정 데이터 원본에 대해 XMLA 공급자에서 지원하는 열거자의 이름, 데이터 형식 및 열거 값 목록을 반환합니다.|  
|[DISCOVER_INSTANCES](https://msdn.microsoft.com/library/ee320541)|서버의 인스턴스를 설명합니다.|  
|[DISCOVER_JOBS](https://msdn.microsoft.com/library/ee320363)|서버에서 실행되는 활성 작업에 대한 정보를 제공합니다. 작업은 명령을 대신하여 특정 태스크를 실행하는 명령의 일부입니다.|  
|[DISCOVER_KEYWORDS &AMP;#40;XMLA&AMP;#41;](https://msdn.microsoft.com/library/ee301719)|XMLA 서버에서 예약 된 키워드에 대 한 정보를 반환 합니다.|  
|[DISCOVER_LITERALS](https://msdn.microsoft.com/library/ee301320)|서버에서 지 원하는 리터럴에 대 한 정보를 반환 합니다.|  
|[DISCOVER_LOCATIONS](https://msdn.microsoft.com/library/ee302024)|백업 파일의 콘텐츠에 대한 정보를 반환합니다. |
|[DISCOVER_LOCKS](https://msdn.microsoft.com/library/ee320398)|서버에서 현재 고정된 잠금에 대한 정보를 제공합니다.|  
|[DISCOVER_MASTER_KEY](https://msdn.microsoft.com/library/ee301825)|서버 마스터 암호화 키를 반환합니다.|
|[DISCOVER_MEMORYGRANT](https://msdn.microsoft.com/library/ee320945)|서버에서 현재 실행 중인 작업에 의해 사용되는 내부 메모리 할당량 부여 목록을 반환합니다.|  
|[DISCOVER_MEMORYUSAGE](https://msdn.microsoft.com/library/ee320910)|서버에 의해 할당된 다양한 개체에 대한 DISCOVER_MEMORYUSAGE 통계를 반환합니다.|  
|[DISCOVER_OBJECT_ACTIVITY](https://msdn.microsoft.com/library/ee320661)|서비스가 시작된 이후의 개체별 리소스 사용량을 제공합니다.|  
|[DISCOVER_OBJECT_MEMORY_USAGE](https://msdn.microsoft.com/library/ee320910)|서버에 의해 할당된 다양한 개체에 대한 DISCOVER_MEMORYUSAGE 통계를 반환합니다.|  
|[DISCOVER_PARTITION_DIMENSION_STAT](https://msdn.microsoft.com/library/ee320268)|파티션과 연결된 차원에 대한 통계를 반환합니다.|  
|[DISCOVER_PARTITION_STAT](https://msdn.microsoft.com/library/ee320483)|특정 파티션의 집계에 대한 통계를 반환합니다.|  
|[DISCOVER_PERFORMANCE_COUNTERS](https://msdn.microsoft.com/library/ee320809)|하나 이상의 지정된 성능 카운터의 값을 반환합니다. |  
|[DISCOVER_PROPERTIES](https://msdn.microsoft.com/library/ee320589)|정보 및 지정된 된 데이터 원본에 대 한 서버에서 지원 되는 속성에 대 한 값의 목록을 반환 합니다.|  
|[DISCOVER_RING_BUFFERS](https://msdn.microsoft.com/library/mt719204)|서버의 현재 XEvent 링 버퍼에 대 한 정보를 반환합니다.|
|[DISCOVER_SCHEMA_ROWSETS](https://msdn.microsoft.com/library/ee320478)|이름, 제한, 설명 및 모든 검색 요청에 대 한 다른 정보를 반환합니다.|  
|[DISCOVER_SESSIONS](https://msdn.microsoft.com/library/ee301962)|서버에서 현재 열려 있는 세션에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS](https://msdn.microsoft.com/library/ee320710)|메모리 내 테이블에 대 한 데이터를 저장 하는 데 사용 되는 열 세그먼트에 대 한 정보를 반환 합니다.|  
|[DISCOVER_STORAGE_TABLE_COLUMNS](https://msdn.microsoft.com/library/ee302101)|메모리 내 테이블의 열을 나타내는 사용 되는 열에 대 한 정보를 포함 합니다.|  
|[DISCOVER_STORAGE_TABLES](https://msdn.microsoft.com/library/ee302014)|서버에 사용할 수 있는 메모리 내 테이블에 대 한 통계를 반환합니다.|  
|[DISCOVER_TRACE_COLUMNS]()||  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO](https://msdn.microsoft.com/library/ee301342)|DISCOVER_TRACE_COLUMNS 스키마 행 집합을 포함합니다.|  
|[DISCOVER_TRACE_EVENT_CATEGORIES](https://msdn.microsoft.com/library/ee320442)|DISCOVER_TRACE_EVENT_CATEGORIES 스키마 행 집합을 포함합니다.|  
|[DISCOVER_TRACES](https://msdn.microsoft.com/library/ee301643)|DISCOVER_TRACES 스키마 행 집합을 포함합니다.|  
|[DISCOVER_TRANSACTIONS](https://msdn.microsoft.com/library/ee301363)|시스템에서 현재 보류 중인 트랜잭션 집합을 반환합니다.|  
|[DISCOVER_XEVENT_TRACE_DEFINITION](https://msdn.microsoft.com/library/mt704568)|서버에서 현재 활성 상태인 XEvent 추적에 대 한 정보를 제공 합니다.|  
|[DISCOVER_XEVENT_PACKAGES](https://msdn.microsoft.com/library/mt704569)|서버에 설명 된 XEvent 패키지에 대 한 정보를 제공 합니다.|
|[DISCOVER_XEVENT_OBJECTS](https://msdn.microsoft.com/library/mt704543)|서버에 설명 된 XEvent 개체에 대 한 정보를 제공 합니다.|
|[DISCOVER_XEVENT_OBJECT_COLUMNS](https://msdn.microsoft.com/library/mt719352)|서버에 설명 된 XEvent 개체의 스키마에 대 한 정보를 제공 합니다.|
|[DISCOVER_XEVENT_SESSIONS](https://msdn.microsoft.com/library/mt704397)|서버의 현재 XEvent 세션에 대 한 정보를 제공합니다.|
|[DISCOVER_XEVENT_SESSION_TARGETS](https://msdn.microsoft.com/library/mt704564)|서버의 현재 XEvent 세션 대상에 대 한 정보를 제공합니다.|
|[DISCOVER_XML_METADATA](https://msdn.microsoft.com/library/ee301560)|하나의 행과 열이 하나를 사용 하 여 행 집합을 반환 합니다. |
|[DMSCHEMA_MINING_COLUMNS](https://msdn.microsoft.com/library/ee301664)|서버에 배포 되는 모든 설명된 데이터 마이닝 모델의 개별 열을 설명 합니다.|  
|[DMSCHEMA_MINING_FUNCTIONS](https://msdn.microsoft.com/library/ee320415)|Analysis Services를 실행 하는 서버에서 사용할 수 있는 데이터 마이닝 알고리즘에서 지원 되는 데이터 마이닝 함수를 설명 합니다.|  
|[DMSCHEMA_MINING_MODEL_CONTENT](https://msdn.microsoft.com/library/ee302124)|클라이언트 응용 프로그램이 학습된 데이터 마이닝 모델의 콘텐츠를 찾아볼 수 있습니다.|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML](https://msdn.microsoft.com/library/ee320692)|마이닝 모델의 XML 구조를 반환합니다. XML 문자열의 형식은 PMML 2.1 표준을 따릅니다.|  
|[DMSCHEMA_MINING_MODEL_XML](https://msdn.microsoft.com/library/ee301916)|마이닝 모델의 XML 구조를 반환합니다. XML 문자열의 형식은 PMML 2.1 표준을 따릅니다.|  
|[DMSCHEMA_MINING_MODELS](https://msdn.microsoft.com/library/ee320603)|서버에 배포된 데이터 마이닝 모델을 열거합니다.|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS](https://msdn.microsoft.com/library/ee320378)|서버에 설치된 각 데이터 마이닝 알고리즘의 동작을 구성하는 데 사용할 수 있는 매개 변수 목록을 제공합니다.|  
|[DMSCHEMA_MINING_SERVICES](https://msdn.microsoft.com/library/ee320487)|서버에서 지 원하는 각 데이터 마이닝 알고리즘에 대 한 정보를 제공 합니다.|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS](https://msdn.microsoft.com/library/ee320277)|서버에 배포된 모든 마이닝 구조의 개별 열에 대해 설명합니다.|  
|[DMSCHEMA_MINING_STRUCTURES](https://msdn.microsoft.com/library/ee320704)|현재 카탈로그의 마이닝 구조에 대한 정보를 열거합니다.|  
|[MDSCHEMA_ACTIONS](https://msdn.microsoft.com/library/ee320890)|클라이언트 응용 프로그램에 사용할 수 있는 작업을 설명 합니다.|
|[MDSCHEMA_CUBES](https://msdn.microsoft.com/library/ee301304)|데이터베이스 내의 큐브 구조를 설명합니다. 큐브 뷰는이 스키마에도 반환 됩니다.|
|[MDSCHEMA_DIMENSIONS](https://msdn.microsoft.com/library/ee301366)|데이터베이스 내의 차원을 설명합니다.|  
|[MDSCHEMA_FUNCTIONS](https://msdn.microsoft.com/library/mt719467)|DAX 및 MDX 언어에서 사용 하기 위해 현재 사용할 수 있는 함수에 대 한 정보를 반환 합니다.|
|[MDSCHEMA_HIERARCHIES](https://msdn.microsoft.com/library/ee320250)|특정 차원 내의 각 계층을 설명합니다.|  
|[MDSCHEMA_INPUT_DATASOURCES](https://msdn.microsoft.com/library/ee301386)|데이터베이스 내에서 설명 된 데이터 원본 개체를 설명 합니다.|  
|[MDSCHEMA_KPIS](https://msdn.microsoft.com/library/ee320406)|데이터베이스 내에서 Kpi를 설명합니다.|  
|[MDSCHEMA_LEVELS](https://msdn.microsoft.com/library/ee320746)|특정 계층 내의 각 수준을 설명합니다.|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS](https://msdn.microsoft.com/library/ee320977)|측정값 그룹의 차원을 열거합니다.|  
|[MDSCHEMA_MEASUREGROUPS](https://msdn.microsoft.com/library/ee320601)|데이터베이스 내의 측정값 그룹을 설명합니다.|  
|[MDSCHEMA_MEASURES](https://msdn.microsoft.com/library/ee301871)|각 측정값을 설명합니다.|  
|[MDSCHEMA_MEMBERS](https://msdn.microsoft.com/library/ee320960)|데이터베이스 내의 멤버를 설명합니다.|  
|[MDSCHEMA_PROPERTIES](https://msdn.microsoft.com/library/ee320393)|멤버의 속성 및 셀 속성에 설명합니다.|  
|[MDSCHEMA_SETS](https://msdn.microsoft.com/library/ee301356)|현재 세션 범위 집합을 포함 하 여 데이터베이스에 설명 된 모든 집합에 설명 합니다.|  

  
  
