---
title: "동적 관리 뷰 (Dmv)를 사용 하 여 Analysis Services를 모니터링할 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 22b82b2d-867f-4ebf-9288-79d1cdd62f18
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0c9faafd33f7abaee582821336dcd471d637a1c1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="use-dynamic-management-views-dmvs-to-monitor-analysis-services"></a>DMV(동적 관리 뷰)를 사용하여 Analysis Services 모니터링
  Analysis Services DMV(동적 관리 뷰)는 로컬 서버 작업 및 서버 상태에 대한 정보를 표시하는 쿼리 구조입니다. 쿼리 구조는 Analysis Services 인스턴스에 대한 메타데이터 및 모니터링 정보를 반환하는 스키마 행 집합에 대한 인터페이스입니다.  
  
 대부분의 DMV 쿼리에서는 **SELECT** 문 및 **$System** 스키마를 XML/A 스키마 행 집합과 함께 사용합니다.  
  
```  
SELECT * FROM $System.<schemaRowset>  
```  
  
 DMV 쿼리는 쿼리가 실행된 시점의 서버 상태에 대한 정보를 반환합니다. 실시간으로 작업을 모니터링하려면 대신 추적을 사용하십시오. 자세한 내용은 [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)을(를) 참조하세요.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
 [DMV 쿼리 사용의 이점](#bkmk_ben)  
  
 [예 및 시나리오](#bkmk_ex)  
  
 [쿼리 구문](#bkmk_syn)  
  
 [도구 및 사용 권한](#bkmk_tools)  
  
 [DMV 참조](#bkmk_ref)  
  
##  <a name="bkmk_ben"></a> DMV 쿼리 사용의 이점  
 DMV 쿼리는 다른 방법으로는 제공되지 않는 작업 및 리소스 소비에 대한 정보를 반환합니다.  
  
 DMV 쿼리는 XML/A Discover 명령을 실행하는 대신 사용할 수 있는 방법입니다. DMV는 쿼리 구문이 SQL에 기반을 두기 때문에 대부분의 관리자에게는 DMV 쿼리를 작성하는 것이 더 간편합니다. 또한 읽고 복사하기가 쉬운 테이블 형식으로 결과 집합이 반환됩니다.  
  
##  <a name="bkmk_ex"></a> 예 및 시나리오  
 DMV 쿼리를 사용하면 서비스 세션 및 연결에 대한 정보를 확인할 수 있으며 특정 시점에 CPU나 메모리를 가장 많이 사용하는 개체가 어떤 것인지 파악할 수 있습니다. 이 섹션에서는 DMV 쿼리가 가장 보편적으로 사용되는 시나리오의 예를 제공합니다. DMV 쿼리를 사용하여 서버 인스턴스를 모니터링하는 것에 대한 자세한 내용은 [SQL Server 2008 R2 Analysis Services 작업 가이드](http://go.microsoft.com/fwlink/?LinkID=225539&clcid=0x409) 를 참조하십시오.  
  
 `Select * from $System.discover_object_activity` /** 이 쿼리는 서비스를 마지막으로 시작한 이후의 개체 작업에 대해 보고합니다. 이 DMV를 기반으로 한 쿼리 예를 보려면 [새 System.Discover_Object_Activity](http://go.microsoft.com/fwlink/?linkid=221322)를 참조하세요.  
  
 `Select * from $System.discover_object_memory_usage` /** 이 쿼리는 개체별 메모리 사용량에 대해 보고합니다.  
  
 `Select * from $System.discover_sessions` /** 이 쿼리는 세션 사용자 및 기간을 포함하여 활성 세션에 대해 보고합니다.  
  
 `Select * from $System.discover_locks` /** 이 쿼리는 특정 시점에 사용된 잠금의 스냅숏을 반환합니다.  
  
##  <a name="bkmk_syn"></a> 쿼리 구문  
 DMV의 쿼리 엔진은 데이터 마이닝 파서입니다. DMV 쿼리 구문은 [SELECT&#40;DMX&#41;](../../dmx/select-dmx.md) 문을 기반으로 합니다.  
  
 DMV 쿼리 구문은 SQL SELECT 문에 기반을 두지만 SELECT 문의 전체 구문을 지원하지는 않습니다. 특히 JOIN, GROUP BY, LIKE, CAST 및 CONVERT는 지원되지 않습니다.  
  
```  
SELECT [DISTINCT] [TOP <n>] <select list>  
FROM $System.<schemaRowset>  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
 DISCOVER_CALC_DEPENDENCY에 대한 다음 예에서는 WHERE 절을 사용하여 쿼리에 매개 변수를 제공하는 것을 보여 줍니다.  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY  
WHERE OBJECT_TYPE = 'ACTIVE_RELATIONSHIP'  
```  
  
 또는 제한을 포함하는 스키마 행 집합의 경우 쿼리에 SYSTEMRESTRICTSCHEMA 함수를 포함해야 합니다. 다음 예에서는 테이블 형식 모드 서버에서 실행 중인 테이블 형식 모델에 대한 CSDL 메타데이터를 반환합니다. CATALOG_NAME은 대/소문자를 구분합니다.  
  
```  
Select * from SYSTEMRESTRICTSCHEMA ($System.Discover_csdl_metadata, [CATALOG_NAME] = 'Adventure Works DW')  
```  
  
##  <a name="bkmk_tools"></a> 도구 및 사용 권한  
 DMV를 쿼리하려면 Analysis Services 인스턴스에 대한 시스템 관리자 권한이 있어야 합니다.  
  
 SQL Server Management Studio, Reporting Services 보고서, PerformancePoint 대시보드 등 MDX 또는 DMX 쿼리를 지원하는 클라이언트 응용 프로그램은 모두 사용할 수 있습니다.  
  
 Management Studio에서 DMV 쿼리를 실행하려면 쿼리할 인스턴스에 연결한 다음 **새 쿼리**를 클릭합니다. MDX 또는 DMX 쿼리 창에서 쿼리를 실행할 수 있습니다.  
  
##  <a name="bkmk_ref"></a> DMV 참조  
 모든 스키마 행 집합에 DMV 인터페이스가 있는 것은 아닙니다. DMV를 사용하여 쿼리할 수 있는 모든 스키마 행 집합 목록을 반환하려면 다음 쿼리를 실행합니다.  
  
```  
SELECT * FROM $System.DBSchema_Tables   
WHERE TABLE_TYPE = 'SCHEMA'   
ORDER BY TABLE_NAME ASC  
```  
  
> [!NOTE]  
>  서버에 다음 오류가 반환 DMV 주어진된 행 집합에 대해 사용할 수 없는 경우: "는 \<w s e t > 서버에서 요청 유형을 인식할 수 없습니다". 다른 모든 오류는 구문 문제를 가리킵니다.  
  
|행 집합|Description|  
|------------|-----------------|  
|[DBSCHEMA_CATALOGS 행 집합](../../analysis-services/schema-rowsets/ole-db/dbschema-catalogs-rowset.md)|현재 연결의 Analysis Services 데이터베이스 목록을 반환합니다.|  
|[DBSCHEMA_COLUMNS 행 집합](../../analysis-services/schema-rowsets/ole-db/dbschema-columns-rowset.md)|현재 데이터베이스에 있는 모든 열 목록을 반환합니다. 이 목록을 사용하여 DMV 쿼리를 생성할 수 있습니다.|  
|[DBSCHEMA_PROVIDER_TYPES 행 집합](../../analysis-services/schema-rowsets/ole-db/dbschema-provider-types-rowset.md)|OLE DB 데이터 공급자가 지원하는 기본 데이터 형식에 대한 속성을 반환합니다.|  
|[DBSCHEMA_TABLES 행 집합](../../analysis-services/schema-rowsets/ole-db/dbschema-tables-rowset.md)|현재 데이터베이스에 있는 모든 테이블 목록을 반환합니다. 이 목록을 사용하여 DMV 쿼리를 생성할 수 있습니다.|  
|[DISCOVER_CALC_DEPENDENCY 행 집합](../../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md)|모델에 사용된 열과 테이블 중 다른 열과 테이블에 종속된 열과 테이블 목록을 반환합니다.|  
|[DISCOVER_COMMAND_OBJECTS 행 집합](../../analysis-services/schema-rowsets/xml/discover-command-objects-rowset.md)|참조된 명령에서 사용 중인 개체에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_COMMANDS 행 집합](../../analysis-services/schema-rowsets/xml/discover-commands-rowset.md)|현재 실행 중인 명령에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_CONNECTIONS 행 집합](../../analysis-services/schema-rowsets/xml/discover-connections-rowset.md)|Analysis Services에 대해 열려 있는 연결에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_CSDL_METADATA 행 집합](../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)|테이블 형식 모델에 대한 정보를 반환합니다.<br /><br /> SYSTEMRESTRICTSCHEMA 및 추가 매개 변수가 필요합니다.|  
|[DISCOVER_DB_CONNECTIONS 행 집합](../../analysis-services/schema-rowsets/xml/discover-db-connections-rowset.md)|Analysis Services에서 외부 데이터 원본으로의 열린 연결(예: 처리하는 동안 또는 가져오는 동안)에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_DIMENSION_STAT 행 집합](../../analysis-services/schema-rowsets/xml/discover-dimension-stat-rowset.md)|모델 유형에 따라 차원의 특성 또는 테이블의 열을 반환합니다.|  
|[DISCOVER_ENUMERATORS 행 집합](../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)|특정 데이터 원본에 대해 지원되는 열거자에 대한 메타데이터를 반환합니다.|  
|[DISCOVER_INSTANCES 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/discover-instances-rowset.md)|지정한 인스턴스에 대한 정보를 반환합니다.<br /><br /> SYSTEMRESTRICTSCHEMA 및 추가 매개 변수가 필요합니다.|  
|[DISCOVER_JOBS 행 집합](../../analysis-services/schema-rowsets/xml/discover-jobs-rowset.md)|현재 작업에 대한 정보를 반환합니다.|  
|[DISCOVER_KEYWORDS 행 집합&#40;XMLA&#41;](../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)|예약된 키워드 목록을 반환합니다.|  
|[DISCOVER_LITERALS 행 집합](../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)|XMLA에서 지원되는 데이터 형식 및 값을 포함하여 리터럴 목록을 반환합니다.|  
|[DISCOVER_LOCKS 행 집합](../../analysis-services/schema-rowsets/xml/discover-locks-rowset.md)|특정 시점에 사용된 잠금의 스냅숏을 반환합니다.|  
|[DISCOVER_MEMORYGRANT 행 집합](../../analysis-services/schema-rowsets/xml/discover-memorygrant-rowset.md)|시작할 때 Analysis Services에서 할당한 메모리에 대한 정보를 반환합니다.|  
|[DISCOVER_MEMORYUSAGE 행 집합](../../analysis-services/schema-rowsets/xml/discover-memoryusage-rowset.md)|특정 개체별로 메모리 사용량을 보여 줍니다.|  
|[DISCOVER_OBJECT_ACTIVITY 행 집합](../../analysis-services/schema-rowsets/xml/discover-object-activity-rowset.md)|서비스를 마지막으로 시작한 이후의 개체 작업에 대해 보고합니다.|  
|[DISCOVER_OBJECT_MEMORY_USAGE 행 집합](../../analysis-services/schema-rowsets/xml/discover-object-memory-usage-rowset.md)|개체의 메모리 사용량에 대해 보고합니다.|  
|[DISCOVER_PARTITION_DIMENSION_STAT 행 집합](../../analysis-services/schema-rowsets/xml/discover-partition-dimension-stat-rowset.md)|차원의 특성에 대한 정보를 제공합니다.<br /><br /> SYSTEMRESTRICTSCHEMA 및 추가 매개 변수가 필요합니다.|  
|[DISCOVER_PARTITION_STAT 행 집합](../../analysis-services/schema-rowsets/xml/discover-partition-stat-rowset.md)|차원, 테이블 또는 측정값 그룹의 파티션에 대한 정보를 제공합니다.<br /><br /> SYSTEMRESTRICTSCHEMA 및 추가 매개 변수가 필요합니다.|  
|[DISCOVER_PERFORMANCE_COUNTERS 행 집합](../../analysis-services/schema-rowsets/xml/discover-performance-counters-rowset.md)|성능 카운터에 사용되는 열을 나열합니다.<br /><br /> SYSTEMRESTRICTSCHEMA 및 추가 매개 변수가 필요합니다.|  
|[DISCOVER_PROPERTIES 행 집합](../../analysis-services/schema-rowsets/xml/discover-properties-rowset.md)|지정한 데이터 원본에 대해 XMLA에서 지원하는 속성에 대한 정보를 반환합니다.|  
|[DISCOVER_SCHEMA_ROWSETS 행 집합](../../analysis-services/schema-rowsets/xml/discover-schema-rowsets-rowset.md)|XMLA에서 지원하는 모든 열거 값에 대한 이름, 제한, 설명 및 기타 정보를 반환합니다.|  
|[DISCOVER_SESSIONS 행 집합](../../analysis-services/schema-rowsets/xml/discover-sessions-rowset.md)|세션 사용자 및 기간을 포함하여 활성 세션에 대해 보고합니다.|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 행 집합](../../analysis-services/schema-rowsets/xml/discover-storage-table-column-segments-rowset.md)|테이블 형식 또는 SharePoint 모드로 실행되는 Analysis Services 데이터베이스에서 사용하는 저장소 테이블에 대한 열 및 세그먼트 수준 정보를 제공합니다.|  
|[DISCOVER_STORAGE_TABLE_COLUMNS 행 집합](../../analysis-services/schema-rowsets/xml/discover-storage-table-columns-rowset.md)|클라이언트가 테이블 형식 또는 SharePoint 모드로 실행되는 Analysis Services 데이터베이스에서 사용하는 저장소 테이블에 대한 열 할당을 확인할 수 있도록 합니다.|  
|[DISCOVER_STORAGE_TABLES 행 집합](../../analysis-services/schema-rowsets/xml/discover-storage-tables-rowset.md)|테이블 형식 모델 데이터베이스에서 모델 저장소로 사용되는 테이블에 대한 정보를 반환합니다.|  
|[DISCOVER_TRACE_COLUMNS 행 집합](../../analysis-services/schema-rowsets/xml/discover-trace-columns-rowset.md)|추적에 사용할 수 있는 열에 대한 XML 설명을 반환합니다.|  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO 행 집합](../../analysis-services/schema-rowsets/xml/discover-trace-definition-providerinfo-rowset.md)|공급자의 이름 및 버전 정보를 반환합니다.|  
|[DISCOVER_TRACE_EVENT_CATEGORIES 행 집합](../../analysis-services/schema-rowsets/xml/discover-trace-event-categories-rowset.md)|사용 가능한 범주 목록을 반환합니다.|  
|[DISCOVER_TRACES 행 집합](../../analysis-services/schema-rowsets/xml/discover-traces-rowset.md)|현재 연결에서 현재 실행 중인 추적 목록을 반환합니다.|  
|[DISCOVER_TRANSACTIONS 행 집합](../../analysis-services/schema-rowsets/xml/discover-transactions-rowset.md)|현재 연결에서 현재 실행 중인 트랜잭션 목록을 반환합니다.|  
|[DISCOVER_XEVENT_TRACE_DEFINITION 행 집합](http://msdn.microsoft.com/library/e1ce2d2d-f994-4318-801a-ee0385aecd84)|현재 연결에서 현재 실행 중인 이벤트 추적 목록을 반환합니다.|  
|[DMSCHEMA_MINING_COLUMNS 행 집합](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-columns-rowset.md)|현재 연결에서 사용할 수 있는 모든 마이닝 모델의 개별 열을 나열합니다.|  
|[DMSCHEMA_MINING_FUNCTIONS 행 집합](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-functions-rowset.md)|서버의 데이터 마이닝 알고리즘이 지원하는 함수 목록을 반환합니다.|  
|[DMSCHEMA_MINING_MODEL_CONTENT 행 집합](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)|현재 모델을 설명하는 열로 구성된 행 집합을 반환합니다.|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML 행 집합](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|현재 모델을 설명하는 열로 구성된 행 집합을 PMML 형식으로 반환합니다.|  
|[DMSCHEMA_MINING_MODEL_XML 행 집합](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-xml-rowset.md)|현재 모델을 설명하는 열로 구성된 행 집합을 PMML 형식으로 반환합니다.|  
|[DMSCHEMA_MINING_MODELS 행 집합](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-models-rowset.md)|현재 데이터베이스에 있는 마이닝 모델 목록을 반환합니다.|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS 행 집합](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)|서버의 알고리즘에 대한 매개 변수 목록을 반환합니다.|  
|[DMSCHEMA_MINING_SERVICES 행 집합](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)|서버에서 사용할 수 있는 데이터 마이닝 알고리즘의 목록을 제공합니다.|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS 행 집합](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset.md)|현재 연결에서 사용할 수 있는 모든 마이닝 모델의 모든 열을 반환합니다.|  
|[DMSCHEMA_MINING_STRUCTURES 행 집합](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structures-rowset.md)|현재 연결에서 사용할 수 있는 마이닝 구조를 나열합니다.|  
|[MDSCHEMA_CUBES 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-cubes-rowset.md)|현재 데이터베이스에 정의된 큐브에 대한 정보를 반환합니다.|  
|[MDSCHEMA_DIMENSIONS 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-dimensions-rowset.md)|현재 데이터베이스에 정의된 차원에 대한 정보를 반환합니다.|  
|[MDSCHEMA_FUNCTIONS 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-functions-rowset.md)|데이터베이스에 연결된 클라이언트 응용 프로그램에 사용할 수 있는 함수 목록을 반환합니다.|  
|[MDSCHEMA_HIERARCHIES 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)|현재 데이터베이스에 정의된 계층에 대한 정보를 반환합니다.|  
|[MDSCHEMA_INPUT_DATASOURCES 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)|현재 데이터베이스에 정의된 데이터 원본 개체에 대한 정보를 반환합니다.|  
|[MDSCHEMA_KPIS 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-kpis-rowset.md)|현재 데이터베이스에 정의된 KPI에 대한 정보를 반환합니다.|  
|[MDSCHEMA_LEVELS 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-levels-rowset.md)|현재 데이터베이스에 정의된 계층 내 수준에 대한 정보를 반환합니다.|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md)|측정값 그룹의 차원을 나열합니다.|  
|[MDSCHEMA_MEASUREGROUPS 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroups-rowset.md)|현재 연결의 측정값 그룹 목록을 반환합니다.|  
|[MDSCHEMA_MEASURES 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measures-rowset.md)|현재 연결의 측정값 목록을 반환합니다.|  
|[MDSCHEMA_MEMBERS 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-members-rowset.md)|현재 연결의 모든 멤버 목록을 데이터베이스, 큐브 및 차원별로 정렬하여 반환합니다.|  
|[MDSCHEMA_PROPERTIES 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)|속성 유형, 데이터 형식 및 기타 메타데이터와 함께 각 속성의 정규화된 이름을 반환합니다.|  
|[MDSCHEMA_SETS 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-sets-rowset.md)|현재 연결에 정의된 집합 목록을 반환합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 2008 R2 Analysis Services 작업 가이드](http://go.microsoft.com/fwlink/?LinkID=225539&clcid=0x409)   
 [새 System.Discover_Object_Activity](http://go.microsoft.com/fwlink/?linkid=221322)   
 [제한 된 행 집합 및 Dmv에 대 한 새 SYSTEMRESTRICTEDSCHEMA 함수](http://go.microsoft.com/fwlink/?LinkId=231885)  
  
  
