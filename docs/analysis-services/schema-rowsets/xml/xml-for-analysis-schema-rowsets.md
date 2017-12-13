---
title: XML for Analysis Schema Rowsets | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- rowsets [Analysis Services], XML for Analysis
- XML for Analysis, schema rowsets
- schema rowsets [Analysis Services], XML for Analysis
- schema rowsets [XML for Analysis]
ms.assetid: 36e3ecfd-fcc3-415a-9c43-f59921d2468a
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2f5cb613a916f2cff4ec8aca3bb67fc9c14d1b10
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="xml-for-analysis-schema-rowsets"></a>XML for Analysis Schema Rowsets
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 공급자 서버 상태, 작업 및 개체에 대 한 메타 데이터를 반환 하는 스키마 행 집합을 포함 합니다. 구조와 특성이 가변적인 Analysis Services 모델에 연결하는 클라이언트 응용 프로그램을 개발하려는 경우 메타데이터 검색이 필요합니다.  
  
 스키마 행 집합은 서버를 모니터링하고 문제를 해결하는 데 도움이 되는 내부 프로세스 및 작업에 대한 정보를 제공합니다. 임시 관리 태스크를 더욱 잘 지원하기 위해 대부분의 스키마 행 집합에 대해 DMV(동적 관리 뷰) 쿼리를 실행할 수 있습니다. DMV 쿼리는 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 볼 수 있는 읽기 가능한 테이블 형식으로 결과를 반환됩니다.  
  
 다음 표에서는 각 XMLA 스키마 행 집합을 나열하고 설명하며, 테이블 형식 데이터 모델과 관련된 정보를 반환하는지 여부를 나타냅니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|행 집합<sup>1</sup>|Description|  
|------------------------|-----------------|  
|[DISCOVER_CALC_DEPENDENCY 행 집합](../../../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md)|테이블, 열, 측정값 및 계산된 열 수식 간의 종속성 정보를 반환합니다.<br /><br /> Analysis Services 인스턴스에 배포 된 테이블 형식 모델에 적용 됩니다 및 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SharePoint 환경에서 실행 되는 Excel 통합 문서에서 모델입니다.|  
|[DISCOVER_CONNECTIONS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-connections-rowset.md)|서버에서 현재 열린 연결에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_COMMAND_OBJECTS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-command-objects-rowset.md)|참조된 명령에서 사용 중인 개체에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_COMMANDS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-commands-rowset.md)|서버에 열려 있는 연결의 현재 실행 중이거나 마지막으로 실행된 명령에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_CSDL_METADATA 행 집합](../../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)|테이블 형식에서 사용할 수 있는 클라이언트에 게 데이터 원본의 XML 정의 반환 하거나 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 모델링 하 고 보고서의 일부로 원본 데이터를 표시 합니다.<br /><br /> Analysis Services 인스턴스에 배포 된 테이블 형식 모델에 적용 됩니다 및 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SharePoint 환경에서 실행 되는 Excel 통합 문서에서 모델입니다.|  
|[DISCOVER_DATASOURCES 행 집합](../../../analysis-services/schema-rowsets/xml/discover-datasources-rowset.md)|서버 또는 웹 서비스에서 사용할 수 있는 XMLA 공급자 데이터 원본 목록을 반환합니다.|  
|[DISCOVER_DB_CONNECTIONS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-db-connections-rowset.md)|서버에서 현재 열린 데이터베이스 연결에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_DIMENSION_STAT 행 집합](../../../analysis-services/schema-rowsets/xml/discover-dimension-stat-rowset.md)|지정된 차원에 대한 통계를 반환합니다.|  
|[DISCOVER_ENUMERATORS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)|특정 데이터 원본에 대해 XMLA 공급자에서 지원하는 열거자의 이름, 데이터 형식 및 열거 값 목록을 반환합니다.|  
|[DISCOVER_JOBS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-jobs-rowset.md)|서버에서 실행되는 활성 작업에 대한 정보를 제공합니다.|  
|[DISCOVER_KEYWORDS 행 집합 &#40; XMLA &#41;](../../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)|XMLA 공급자에 예약된 키워드에 대한 정보를 반환합니다.|  
|[DISCOVER_LITERALS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)|XMLA 공급자에서 지원되는 데이터 형식 및 값을 포함한 리터럴 정보를 반환합니다.|  
|[DISCOVER_LOCATIONS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-locations-rowset.md)|백업 파일의 콘텐츠에 대한 정보를 반환합니다.|  
|[DISCOVER_LOCKS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-locks-rowset.md)|서버에서 현재 고정된 잠금에 대한 정보를 제공합니다.|  
|[DISCOVER_MEMORYGRANT 행 집합](../../../analysis-services/schema-rowsets/xml/discover-memorygrant-rowset.md)|서버에서 현재 실행 중인 작업에 의해 사용되는 내부 메모리 할당량 부여 목록을 반환합니다.|  
|[DISCOVER_MEMORYUSAGE 행 집합](../../../analysis-services/schema-rowsets/xml/discover-memoryusage-rowset.md)|서버에 의해 할당된 다양한 개체에 대한 메모리 사용량 통계를 반환합니다.|  
|[DISCOVER_OBJECT_ACTIVITY 행 집합](../../../analysis-services/schema-rowsets/xml/discover-object-activity-rowset.md)|서비스가 시작된 이후의 개체별 리소스 사용량을 제공합니다.|  
|[DISCOVER_OBJECT_MEMORY_USAGE 행 집합](../../../analysis-services/schema-rowsets/xml/discover-object-memory-usage-rowset.md)|개체에서 사용하는 메모리 리소스에 대한 정보를 제공합니다.|  
|[DISCOVER_PARTITION_DIMENSION_STAT 행 집합](../../../analysis-services/schema-rowsets/xml/discover-partition-dimension-stat-rowset.md)|파티션과 연결된 차원에 대한 통계를 반환합니다.|  
|[DISCOVER_PARTITION_STAT 행 집합](../../../analysis-services/schema-rowsets/xml/discover-partition-stat-rowset.md)|특정 파티션의 집계에 대한 통계를 반환합니다.|  
|[DISCOVER_PERFORMANCE_COUNTERS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-performance-counters-rowset.md)|하나 이상의 지정된 성능 카운터의 값을 반환합니다.|  
|[DISCOVER_PROPERTIES 행 집합](../../../analysis-services/schema-rowsets/xml/discover-properties-rowset.md)|지정된 데이터 원본에 대해 XMLA 공급자에서 지원하는 표준 및 공급자별 속성에 대한 정보와 값 목록을 반환합니다.|  
|[DISCOVER_SCHEMA_ROWSETS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-schema-rowsets-rowset.md)|XMLA 공급자에서 지원하는 모든 열거 값과 추가 공급자별 열거 값에 대한 이름, 제한, 설명 및 기타 정보를 반환합니다.|  
|[DISCOVER_SESSIONS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-sessions-rowset.md)|서버에서 현재 열려 있는 세션에 대한 리소스 사용량 및 작업 정보를 제공합니다.|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-storage-table-column-segments-rowset.md)|테이블 형식에서 사용 하는 저장소 테이블에 대 한 열 및 세그먼트 수준 정보를 제공 하거나 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 데이터베이스입니다.<br /><br /> Analysis Services 인스턴스에 배포 된 테이블 형식 모델에 적용 됩니다 및 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SharePoint 환경에서 실행 되는 Excel 통합 문서에서 모델입니다.|  
|[DISCOVER_STORAGE_TABLE_COLUMNS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-storage-table-columns-rowset.md)|클라이언트가 테이블 형식에서 사용 하는 저장소 테이블에 대 한 열 할당을 확인할 수 있도록 또는 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 데이터베이스입니다.<br /><br /> Analysis Services 인스턴스에 배포 된 테이블 형식 모델에 적용 됩니다 및 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SharePoint 환경에서 실행 되는 Excel 통합 문서에서 모델입니다.|  
|[DISCOVER_STORAGE_TABLES 행 집합](../../../analysis-services/schema-rowsets/xml/discover-storage-tables-rowset.md)|모델에 사용되는 테이블에 대한 정보를 반환합니다.<br /><br /> Analysis Services 인스턴스에 배포 된 테이블 형식 모델에 적용 됩니다 및 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SharePoint 환경에서 실행 되는 Excel 통합 문서에서 모델입니다.|  
|[DISCOVER_TRACE_COLUMNS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-trace-columns-rowset.md)|추적 공급자가 제공하는 추적 열에 대해 설명합니다.|  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO 행 집합](../../../analysis-services/schema-rowsets/xml/discover-trace-definition-providerinfo-rowset.md)|추적 공급자의 이름 및 설명과 같은 추적 공급자에 대한 기본 정보를 반환합니다.|  
|[DISCOVER_TRACE_EVENT_CATEGORIES 행 집합](../../../analysis-services/schema-rowsets/xml/discover-trace-event-categories-rowset.md)|추적 공급자가 제공하는 이벤트 범주에 대해 설명합니다.|  
|[DISCOVER_TRACES 행 집합](../../../analysis-services/schema-rowsets/xml/discover-traces-rowset.md)|서버에서 실행되는 추적에 대한 정보를 반환합니다.|  
|[DISCOVER_TRANSACTIONS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-transactions-rowset.md)|시스템에서 현재 보류 중인 트랜잭션 집합을 반환합니다.|  
|[DISCOVER_XML_METADATA 행 집합](../../../analysis-services/schema-rowsets/xml/discover-xml-metadata-rowset.md)|요청된 개체를 설명하는 XML 문서를 반환합니다.|  
  
 <sup>1</sup> 여기에 나열 된 모든 스키마 행 집합 용 MSOLAP 데이터 원본 공급자에서 지원 되는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA 공급자입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services에서 XMLA를 사용 하 여 개발](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [사용 하 여 동적 관리 뷰 &#40; Dmv &#41; Analysis Services를 모니터링 하려면](../../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)   
 [분석 데이터 원본에서 메타데이터 검색](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  
