---
title: XML for Analysis Schema Rowsets | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- rowsets [Analysis Services], XML for Analysis
- XML for Analysis, schema rowsets
- schema rowsets [Analysis Services], XML for Analysis
- schema rowsets [XML for Analysis]
ms.assetid: 36e3ecfd-fcc3-415a-9c43-f59921d2468a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 50f95f4049d03c8d822c3e56ba5ff235705bf4de
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121183"
---
# <a name="xml-for-analysis-schema-rowsets"></a>XML for Analysis Schema Rowsets
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA(XML for Analysis) 공급자는 서버 상태, 작업 및 개체에 대한 메타데이터를 반환하는 스키마 행 집합을 포함합니다. 구조와 특성이 가변적인 Analysis Services 모델에 연결하는 클라이언트 응용 프로그램을 개발하려는 경우 메타데이터 검색이 필요합니다.  
  
 스키마 행 집합은 서버를 모니터링하고 문제를 해결하는 데 도움이 되는 내부 프로세스 및 작업에 대한 정보를 제공합니다. 임시 관리 태스크를 더욱 잘 지원하기 위해 대부분의 스키마 행 집합에 대해 DMV(동적 관리 뷰) 쿼리를 실행할 수 있습니다. DMV 쿼리는 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 볼 수 있는 읽기 가능한 테이블 형식으로 결과를 반환됩니다.  
  
 다음 표에서는 각 XMLA 스키마 행 집합을 나열하고 설명하며, 테이블 형식 데이터 모델과 관련된 정보를 반환하는지 여부를 나타냅니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|Rowset<sup>1</sup>|Description|  
|------------------------|-----------------|  
|[DISCOVER_CALC_DEPENDENCY 행 집합](discover-calc-dependency-rowset.md)|테이블, 열, 측정값 및 계산된 열 수식 간의 종속성 정보를 반환합니다.<br /><br /> Analysis Services 인스턴스에 배포되는 테이블 형식 모델과 SharePoint 환경에서 실행되는 Excel 통합 문서의 PowerPivot 모델에 적용됩니다.|  
|[DISCOVER_CONNECTIONS 행 집합](discover-connections-rowset.md)|서버에서 현재 열린 연결에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_COMMAND_OBJECTS 행 집합](discover-command-objects-rowset.md)|참조된 명령에서 사용 중인 개체에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_COMMANDS 행 집합](discover-commands-rowset.md)|서버에 열려 있는 연결의 현재 실행 중이거나 마지막으로 실행된 명령에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_CSDL_METADATA 행 집합](discover-csdl-metadata-rowset.md)|테이블 형식 모델 또는 PowerPivot 모델을 소비하고 원본 데이터를 보고서의 일부로 제시할 수 있는 클라이언트에게 데이터 원본의 XML 정의를 반환합니다.<br /><br /> Analysis Services 인스턴스에 배포되는 테이블 형식 모델과 SharePoint 환경에서 실행되는 Excel 통합 문서의 PowerPivot 모델에 적용됩니다.|  
|[DISCOVER_DATASOURCES 행 집합](discover-datasources-rowset.md)|서버 또는 웹 서비스에서 사용할 수 있는 XMLA 공급자 데이터 원본 목록을 반환합니다.|  
|[DISCOVER_DB_CONNECTIONS 행 집합](discover-db-connections-rowset.md)|서버에서 현재 열린 데이터베이스 연결에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_DIMENSION_STAT 행 집합](discover-dimension-stat-rowset.md)|지정된 차원에 대한 통계를 반환합니다.|  
|[DISCOVER_ENUMERATORS 행 집합](discover-enumerators-rowset.md)|특정 데이터 원본에 대해 XMLA 공급자에서 지원하는 열거자의 이름, 데이터 형식 및 열거 값 목록을 반환합니다.|  
|[DISCOVER_JOBS 행 집합](discover-jobs-rowset.md)|서버에서 실행되는 활성 작업에 대한 정보를 제공합니다.|  
|[DISCOVER_KEYWORDS 행 집합 &#40;XMLA&#41;](discover-keywords-rowset-xmla.md)|XMLA 공급자에 예약된 키워드에 대한 정보를 반환합니다.|  
|[DISCOVER_LITERALS 행 집합](discover-literals-rowset.md)|XMLA 공급자에서 지원되는 데이터 형식 및 값을 포함한 리터럴 정보를 반환합니다.|  
|[DISCOVER_LOCATIONS 행 집합](discover-locations-rowset.md)|백업 파일의 콘텐츠에 대한 정보를 반환합니다.|  
|[DISCOVER_LOCKS 행 집합](discover-locks-rowset.md)|서버에서 현재 고정된 잠금에 대한 정보를 제공합니다.|  
|[DISCOVER_MEMORYGRANT 행 집합](discover-memorygrant-rowset.md)|서버에서 현재 실행 중인 작업에 의해 사용되는 내부 메모리 할당량 부여 목록을 반환합니다.|  
|[DISCOVER_MEMORYUSAGE 행 집합](discover-memoryusage-rowset.md)|서버에 의해 할당된 다양한 개체에 대한 메모리 사용량 통계를 반환합니다.|  
|[DISCOVER_OBJECT_ACTIVITY 행 집합](discover-object-activity-rowset.md)|서비스가 시작된 이후의 개체별 리소스 사용량을 제공합니다.|  
|[DISCOVER_OBJECT_MEMORY_USAGE 행 집합](discover-object-memory-usage-rowset.md)|개체에서 사용하는 메모리 리소스에 대한 정보를 제공합니다.|  
|[DISCOVER_PARTITION_DIMENSION_STAT 행 집합](discover-partition-dimension-stat-rowset.md)|파티션과 연결된 차원에 대한 통계를 반환합니다.|  
|[DISCOVER_PARTITION_STAT 행 집합](discover-partition-stat-rowset.md)|특정 파티션의 집계에 대한 통계를 반환합니다.|  
|[DISCOVER_PERFORMANCE_COUNTERS 행 집합](discover-performance-counters-rowset.md)|하나 이상의 지정된 성능 카운터의 값을 반환합니다.|  
|[DISCOVER_PROPERTIES 행 집합](discover-properties-rowset.md)|지정된 데이터 원본에 대해 XMLA 공급자에서 지원하는 표준 및 공급자별 속성에 대한 정보와 값 목록을 반환합니다.|  
|[DISCOVER_SCHEMA_ROWSETS 행 집합](discover-schema-rowsets-rowset.md)|XMLA 공급자에서 지원하는 모든 열거 값과 추가 공급자별 열거 값에 대한 이름, 제한, 설명 및 기타 정보를 반환합니다.|  
|[DISCOVER_SESSIONS 행 집합](discover-sessions-rowset.md)|서버에서 현재 열려 있는 세션에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 행 집합](discover-storage-table-column-segments-rowset.md)|테이블 형식 데이터베이스 또는 PowerPivot 데이터베이스에서 사용되는 저장소 테이블에 대한 열 및 세그먼트 수준 정보를 제공합니다.<br /><br /> Analysis Services 인스턴스에 배포되는 테이블 형식 모델과 SharePoint 환경에서 실행되는 Excel 통합 문서의 PowerPivot 모델에 적용됩니다.|  
|[DISCOVER_STORAGE_TABLE_COLUMNS 행 집합](discover-storage-table-columns-rowset.md)|클라이언트가 테이블 형식 데이터베이스 또는 PowerPivot 데이터베이스에서 사용되는 저장소 테이블에 대한 열 할당을 결정할 수 있도록 합니다.<br /><br /> Analysis Services 인스턴스에 배포되는 테이블 형식 모델과 SharePoint 환경에서 실행되는 Excel 통합 문서의 PowerPivot 모델에 적용됩니다.|  
|[DISCOVER_STORAGE_TABLES 행 집합](discover-storage-tables-rowset.md)|모델에 사용되는 테이블에 대한 정보를 반환합니다.<br /><br /> Analysis Services 인스턴스에 배포되는 테이블 형식 모델과 SharePoint 환경에서 실행되는 Excel 통합 문서의 PowerPivot 모델에 적용됩니다.|  
|[DISCOVER_TRACE_COLUMNS 행 집합](discover-trace-columns-rowset.md)|추적 공급자가 제공하는 추적 열에 대해 설명합니다.|  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO 행 집합](discover-trace-definition-providerinfo-rowset.md)|추적 공급자의 이름 및 설명과 같은 추적 공급자에 대한 기본 정보를 반환합니다.|  
|[DISCOVER_TRACE_EVENT_CATEGORIES 행 집합](discover-trace-event-categories-rowset.md)|추적 공급자가 제공하는 이벤트 범주에 대해 설명합니다.|  
|[DISCOVER_TRACES 행 집합](discover-traces-rowset.md)|서버에서 실행되는 추적에 대한 정보를 반환합니다.|  
|[DISCOVER_TRANSACTIONS 행 집합](discover-transactions-rowset.md)|시스템에서 현재 보류 중인 트랜잭션 집합을 반환합니다.|  
|[DISCOVER_XML_METADATA 행 집합](discover-xml-metadata-rowset.md)|요청된 개체를 설명하는 XML 문서를 반환합니다.|  
  
 <sup>1</sup> 여기에 나열 된 모든 스키마 행 집합 용 MSOLAP 데이터 원본 공급자에서 지원 되는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA 공급자입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services에서 XMLA를 사용 하 여 개발](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [동적 관리 뷰를 사용 하 여 &#40;Dmv&#41; 모니터는 분석 서비스](../../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)   
 [분석 데이터 원본에서 메타데이터 검색](../../multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  
