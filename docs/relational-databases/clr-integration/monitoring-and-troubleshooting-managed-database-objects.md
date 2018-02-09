---
title: "관리 되는 데이터베이스 개체 모니터링 및 문제 해결 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- monitoring [CLR integration]
- performance [CLR integration]
ms.assetid: a7b589ac-104d-4b68-b4aa-9f5fc192b13d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aed7ed72f65d504caf0ada54e9eab5ed620d5913
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="monitoring-and-troubleshooting-managed-database-objects"></a>관리되는 데이터베이스 개체 모니터링 및 문제 해결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행 중인 관리되는 데이터베이스 개체와 어셈블리를 모니터링하고 문제를 해결하는 데 사용할 수 있는 도구에 대한 정보를 제공합니다.  
  
## <a name="profiler-trace-events"></a>프로파일러 추적 이벤트  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진에서 발생 하는 이벤트를 모니터링 하는 SQL 추적 및 이벤트 알림을 제공 합니다. SQL 추적은 지정된 이벤트를 기록하여 성능 관련 문제 해결, 데이터베이스 작업 감사, 테스트 환경을 위한 샘플 데이터 수집, [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 및 저장 프로시저 디버깅, 성능 분석 도구를 위한 데이터 수집 등의 작업을 도와 줍니다. 자세한 내용은 참조 [SQL 추적](../../relational-databases/sql-trace/sql-trace.md) 및 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)합니다.  
  
|이벤트|Description|  
|-----------|-----------------|  
|[Assembly Load 이벤트 클래스](http://msdn.microsoft.com/library/cfb0b69d-4ce0-4067-a3df-d82775e57886)|어셈블리 로드 요청(성공 및 실패)을 모니터링하는 데 사용합니다.|  
|[Sql: batchstarting 이벤트 클래스](../../relational-databases/event-classes/sql-batchstarting-event-class.md), [sql: batchcompleted 이벤트 클래스](../../relational-databases/event-classes/sql-batchcompleted-event-class.md)|시작되거나 완료된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리에 대한 정보를 제공합니다.|  
|[SP: Starting 이벤트 클래스](../../relational-databases/event-classes/sp-starting-event-class.md), [SP: Completed 이벤트 클래스](../../relational-databases/event-classes/sp-completed-event-class.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저의 실행을 모니터링하는 데 사용합니다.|  
|[Sql: stmtstarting 이벤트 클래스](../../relational-databases/event-classes/sql-stmtstarting-event-class.md), [sql: stmtcompleted 이벤트 클래스](../../relational-databases/event-classes/sql-stmtcompleted-event-class.md)|CLR 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] 루틴의 실행을 모니터링하는 데 사용합니다.|  
  
## <a name="performance-counters"></a>성능 카운터  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행 하는 컴퓨터에서 작업 모니터링 시스템 모니터에서 사용할 수 있는 개체 및 카운터를 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 개체는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 잠금이나 Windows 프로세스와 같은 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스를 말합니다. 각 개체에는 모니터링할 개체의 여러 요소를 결정하는 하나 이상의 카운터가 포함됩니다. 자세한 내용은 [SQL Server 개체 사용](../../relational-databases/performance-monitor/use-sql-server-objects.md)을 참조하세요.  
  
|개체|Description|  
|------------|-----------------|  
|[SQL Server, CLR 개체](../../relational-databases/performance-monitor/sql-server-clr-object.md)|CLR 실행에 소요된 총 시간입니다.|  
  
## <a name="windows-system-monitor-perfmonexe-counters"></a>Windows 시스템 모니터(PERFMON.EXE) 카운터  
 Windows 시스템 모니터(PERFMON.EXE) 도구에는 CLR 통합 응용 프로그램을 모니터링하는 데 사용할 수 있는 여러 개의 성능 카운터가 포함되어 있습니다. .NET CLR 성능 카운터를 "sqlservr" 프로세스 이름으로 필터링하여 현재 실행 중인 CLR 통합 응용 프로그램을 추적할 수 있습니다.  
  
|성능 개체|Description|  
|------------------------|-----------------|  
|SqlServer:CLR|서버에 대한 CPU 통계를 제공합니다.|  
|.NET CLR Exceptions|초당 예외 수를 추적합니다.|  
|.NET CLR Loading|서버에 로드된 AppDomains 및 어셈블리에 대한 정보를 제공합니다.|  
|.NET CLR Memory|CLR 메모리 사용량에 대한 정보를 제공합니다. 이 개체를 사용하면 메모리 사용량이 지나치게 많을 경우 알림 플래그를 지정할 수 있습니다.|  
|.NET Data Provider for SQL Server|초당 연결 및 연결 해제 횟수를 추적합니다. 이 개체를 사용하면 데이터베이스 작업의 수준을 모니터링할 수 있습니다.|  
  
## <a name="catalog-views"></a>카탈로그 뷰  
 카탈로그 뷰는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진에서 사용하는 정보를 반환합니다. 카탈로그 뷰는 카탈로그 메타데이터에 대한 가장 일반적인 인터페이스이며 정보를 획득 및 변환하고 사용자 지정 형태로 제공하는 데 가장 효과적인 방법을 제공하므로 카탈로그 뷰를 사용하는 것이 좋습니다. 사용자가 이용할 수 있는 모든 카탈로그 메타데이터는 카탈로그 뷰를 통해 표시됩니다. 자세한 내용은 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)를 참조하세요.  
  
|카탈로그 뷰|Description|  
|------------------|-----------------|  
|[sys.assemblies &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)|데이터베이스에 등록된 어셈블리에 대한 정보를 반환합니다.|  
|[sys.assembly_references &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-assembly-references-transact-sql.md)|다른 어셈블리를 참조하는 어셈블리를 식별합니다.|  
|[sys.assembly_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|어셈블리에 정의된 각 함수, 저장 프로시저 및 트리거에 대한 정보를 반환합니다.|  
|[sys.assembly_files &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-assembly-files-transact-sql.md)|데이터베이스에 등록된 어셈블리 파일에 대한 정보를 반환합니다.|  
|[sys.assembly_types &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-assembly-types-transact-sql.md)|어셈블리로 정의된 UDT(사용자 정의 형식)를 식별합니다.|  
|[sys.module_assembly_usages &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-module-assembly-usages-transact-sql.md)|CLR 모듈이 정의되어 있는 어셈블리를 식별합니다.|  
|[sys.parameter_type_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md)|사용자 정의 형식인 매개 변수에 대한 정보를 반환합니다.|  
|[sys.server_assembly_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)|CLR 트리거가 정의되어 있는 어셈블리를 식별합니다.|  
|[sys.server_triggers&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)|CLR 트리거를 비롯하여 서버의 서버 수준 DDL 트리거를 식별합니다.|  
|[sys.type_assembly_usages &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-type-assembly-usages-transact-sql.md)|사용자 정의 형식이 정의되어 있는 어셈블리를 식별합니다.|  
|[sys.types&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)|데이터베이스에 등록된 시스템 유형 및 사용자 정의 형식을 반환합니다.|  
  
## <a name="dynamic-management-views"></a>동적 관리 뷰  
 동적 관리 뷰 및 함수는 서버 인스턴스 상태 모니터링, 문제 진단 및 성능 튜닝에 사용할 수 있는 서버 상태 정보를 반환합니다. 자세한 내용은 참조 [동적 관리 뷰 및 함수 &#40; Transact SQL &#41; ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
|DMV|Description|  
|---------|-----------------|  
|[sys.dm_clr_appdomains &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md)|서버의 각 응용 프로그램 도메인에 대한 정보를 제공합니다.|  
|[sys.dm_clr_loaded_assemblies &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)|서버에 등록된 각 관리되는 어셈블리를 식별합니다.|  
|[sys.dm_clr_properties &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-properties-transact-sql.md)|호스팅된 CLR에 대한 정보를 반환합니다.|  
|[sys.dm_clr_tasks &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-tasks-transact-sql.md)|현재 실행 중인 모든 CLR 태스크를 식별합니다.|  
|[sys.dm_exec_cached_plans&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)|더 빠른 쿼리 실행을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 캐시된 쿼리 실행 계획에 대한 정보를 반환합니다.|  
|[sys.dm_exec_query_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)|캐시된 쿼리 계획에 대한 집계 성능 통계를 반환합니다.|  
|[sys.dm_exec_requests &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행 중인 각 요청에 대한 정보를 반환합니다.|  
|[sys.dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)|CLR 메모리 클럭을 비롯하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 현재 활성 상태인 모든 메모리 클럭을 반환합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [CLR&#40;공용 언어 런타임&#41; 통합 프로그래밍 개요](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
