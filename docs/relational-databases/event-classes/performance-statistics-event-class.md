---
title: Performance Statistics 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Performance Statistics event class
ms.assetid: da9cd2c4-6fdd-4ada-b74f-105e3541393c
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 02db411f94695499fa0fdc3ad061ff8e0e5effe4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="performance-statistics-event-class"></a>Performance Statistics 이벤트 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Performance Statistics 이벤트 클래스는 실행 중인 쿼리, 저장 프로시저 및 트리거의 성능을 모니터링하는 데 사용할 수 있습니다. 6개의 각 이벤트 하위 클래스는 시스템 내의 쿼리, 저장 프로시저 및 트리거의 유효 기간에 있는 이벤트를 나타냅니다. 이 이벤트 하위 클래스 및 관련 sys.dm_exec_query_stats, sys.dm_exec_procedure_stats 및 sys.dm_exec_trigger_stats 동적 관리 뷰를 조합하여 사용하면 지정된 쿼리, 저장 프로시저 또는 트리거의 성능 기록을 다시 구성할 수 있습니다.  
  
## <a name="performance-statistics-event-class-data-columns"></a>Performance Statistics 이벤트 클래스 데이터 열  
 다음 표에서는 EventSubClass 0, EventSubClass 1, EventSubClass 2, EventSubClass 3, EventSubClass 4 및 EventSubClass 5와 같은 각 이벤트 하위 클래스와 관련된 이벤트 클래스 데이터 열에 대해 설명합니다.  
  
### <a name="eventsubclass-0"></a>EventSubClass 0  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|NULL|52|예|  
|BinaryData|**image**|NULL|2|예|  
|DatabaseID|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니오|  
|EventSubClass|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 0 = 현재 캐시에 없는 새로운 일괄 처리 SQL 텍스트입니다.<br /><br /> 임시 일괄 처리에 대한 추적에서 다음 EventSubClass 유형이 생성됩니다.<br /><br /> 쿼리 수가 *n* 인 임시 일괄 처리<br /><br /> 유형 0인 쿼리 한 개|21|예|  
|IntegerData2|**int**|NULL|55|예|  
|ObjectID|**int**|NULL|22|예|  
|Offset|**int**|NULL|61|예|  
|PlanHandle|**Image**|NULL|65|예|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|SqlHandle|**image**|sys.dm_exec_sql_text 동적 관리 뷰를 사용하여 일괄 처리 SQL 텍스트를 가져오는 데 사용할 수 있는 SQL 핸들입니다.|63|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**ntext**|일괄 처리의 SQL 텍스트입니다.|1|예|  
  
### <a name="eventsubclass-1"></a>EventSubClass 1  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|이 계획을 다시 컴파일한 누적 횟수입니다.|52|예|  
|BinaryData|**image**|컴파일된 계획의 이진 XML입니다.|2|예|  
|DatabaseID|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니오|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|EventSubClass|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 1 = 컴파일된 저장 프로시저 내의 쿼리입니다.<br /><br /> 저장 프로시저에 대한 추적에서 다음 EventSubClass 유형이 생성됩니다.<br /><br /> 쿼리 수가 *n* 인 저장 프로시저<br /><br /> 유형 1인 쿼리*n* 개|21|예|  
|IntegerData2|**int**|저장 프로시저 내에 있는 문의 끝입니다.<br /><br /> -1은 저장 프로시저의 끝입니다.|55|예|  
|ObjectID|**int**|시스템이 할당한 개체의 ID입니다.|22|예|  
|Offset|**int**|저장 프로시저나 일괄 처리 내에 있는 문의 시작 오프셋입니다.|61|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|SqlHandle|**image**|dm_exec_sql_text 동적 관리 뷰를 사용하여 저장 프로시저의 SQL 텍스트를 가져오는 데 사용할 수 있는 SQL 핸들입니다.|63|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**ntext**|NULL|1|예|  
|PlanHandle|**image**|저장 프로시저에 대한 컴파일된 계획의 계획 핸들입니다. sys.dm_exec_query_plan 동적 관리 뷰를 사용하여 XML 계획을 가져오는 데 사용할 수 있습니다.|65|예|  
|ObjectType|**int**|이벤트와 관련된 개체 유형을 나타내는 값입니다.<br /><br /> 8272 = 저장 프로시저|28|예|  
|BigintData2|**bigint**|컴파일 시 사용되는 총 메모리(KB)입니다.|53|예|  
|CPU|**int**|컴파일 시 소요되는 총 CPU 시간(밀리초)입니다.|18|예|  
|Duration|**int**|컴파일 시 소요되는 총 시간(마이크로초)입니다.|13|예|  
|IntegerData|**int**|컴파일된 계획의 크기(KB)입니다.|25|예|  
  
### <a name="eventsubclass-2"></a>EventSubClass 2  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|이 계획을 다시 컴파일한 누적 횟수입니다.|52|예|  
|BinaryData|**image**|컴파일된 계획의 이진 XML입니다.|2|예|  
|DatabaseID|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니오|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|EventSubClass|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 2 = 컴파일된 임의 SQL 문 내의 쿼리입니다.<br /><br /> 임시 일괄 처리에 대한 추적에서 다음 EventSubClass 유형이 생성됩니다.<br /><br /> 쿼리 수가 *n* 인 임시 일괄 처리<br /><br /> 유형 2인 쿼리*n* 개|21|예|  
|IntegerData2|**int**|일괄 처리 내에 있는 문의 끝입니다.<br /><br /> -1은 일괄 처리의 끝입니다.|55|예|  
|ObjectID|**int**|해당 사항 없음|22|예|  
|Offset|**int**|일괄 처리 내에 있는 문의 시작 오프셋입니다.<br /><br /> 0은 일괄 처리의 시작입니다.|61|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|SqlHandle|**image**|SQL 핸들입니다. dm_exec_sql_text 동적 관리 뷰를 사용하여 일괄 처리 SQL 텍스트를 가져오는 데 사용할 수 있습니다.|63|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**ntext**|NULL|1|예|  
|PlanHandle|**image**|일괄 처리에 대한 컴파일된 계획의 계획 핸들입니다. dm_exec_query_plan 동적 관리 뷰를 사용하여 일괄 처리 XML 계획을 가져오는 데 사용할 수 있습니다.|65|예|  
|BigintData2|**bigint**|컴파일 시 사용되는 총 메모리(KB)입니다.|53|예|  
|CPU|**int**|컴파일 시 소요되는 총 CPU 시간(마이크로초)입니다.|18|예|  
|Duration|**int**|컴파일 시 소요되는 총 시간(밀리초)입니다.|13|예|  
|IntegerData|**int**|컴파일된 계획의 크기(KB)입니다.|25|예|  
  
### <a name="eventsubclass-3"></a>EventSubClass 3  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|이 계획을 다시 컴파일한 누적 횟수입니다.|52|예|  
|BinaryData|**image**|NULL|2|예|  
|DatabaseID|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니오|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|EventSubClass|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 3 = 캐시된 쿼리가 소멸되었으며 계획과 관련된 기록 성능 데이터도 소멸될 예정입니다.<br /><br /> 추적에서 다음 EventSubClass 유형이 생성됩니다.<br /><br /> 쿼리 수가 *n* 인 임시 일괄 처리<br /><br /> 쿼리가 캐시에서 플러시될 때 유형 3인 쿼리 한 개<br /><br /> 쿼리 수가 *n* 인 저장 프로시저<br /><br /> 쿼리가 캐시에서 플러시될 때 유형 3인 쿼리 한 개|21|예|  
|IntegerData2|**int**|저장 프로시저나 일괄 처리 내에 있는 문의 끝입니다.<br /><br /> -1은 저장 프로시저나 일괄 처리의 끝입니다.|55|예|  
|ObjectID|**int**|NULL|22|예|  
|Offset|**int**|저장 프로시저나 일괄 처리 내에 있는 문의 시작 오프셋입니다.<br /><br /> 0은 저장 프로시저나 일괄 처리의 시작입니다.|61|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|SqlHandle|**image**|dm_exec_sql_text 동적 관리 뷰를 사용하여 저장 프로시저나 일괄 처리 SQL 텍스트를 가져오는 데 사용할 수 있는 SQL 핸들입니다.|63|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**ntext**|QueryExecutionStats|1|예|  
|PlanHandle|**image**|저장 프로시저나 일괄 처리에 대한 컴파일된 계획의 계획 핸들입니다. dm_exec_query_plan 동적 관리 뷰를 사용하여 XML 계획을 가져오는 데 사용할 수 있습니다.|65|예|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
  
### <a name="eventsubclass-4"></a>EventSubClass 4  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|NULL|52|예|  
|BinaryData|**image**|NULL|2|예|  
|DatabaseID|**int**|지정된 저장 프로시저가 있는 데이터베이스의 ID입니다.|3|예|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니오|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|EventSubClass|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 4 = 캐시된 저장 프로시저가 캐시에서 제거되었으며 관련된 기록 성능 데이터도 소멸될 예정입니다.|21|예|  
|IntegerData2|**int**|NULL|55|예|  
|ObjectID|**int**|저장 프로시저의 ID입니다. sys.proceduresdml object_id 열과 동일합니다.|22|예|  
|Offset|**int**|NULL|61|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|SqlHandle|**image**|dm_exec_sql_text 동적 관리 뷰를 사용하여 실행된 저장 프로시저 SQL 텍스트를 가져오는 데 사용할 수 있는 SQL 핸들입니다.|63|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**ntext**|ProcedureExecutionStats|1|예|  
|PlanHandle|**image**|저장 프로시저에 대한 컴파일된 계획의 계획 핸들입니다. dm_exec_query_plan 동적 관리 뷰를 사용하여 XML 계획을 가져오는 데 사용할 수 있습니다.|65|예|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
  
### <a name="eventsubclass-5"></a>EventSubClass 5  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|NULL|52|예|  
|BinaryData|**image**|NULL|2|예|  
|DatabaseID|**int**|지정된 트리거가 있는 데이터베이스의 ID입니다.|3|예|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니오|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|EventSubClass|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 5 = 캐시된 트리거가 캐시에서 제거되었으며 관련된 기록 성능 데이터도 소멸될 예정입니다.|21|예|  
|IntegerData2|**int**|NULL|55|예|  
|ObjectID|**int**|트리거의 ID입니다. sys.triggers/sys.server_triggers 카탈로그 뷰의 object_id 열과 동일합니다.|22|예|  
|Offset|**int**|NULL|61|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|SqlHandle|**image**|dm_exec_sql_text 동적 관리 뷰를 사용하여 트리거의 SQL 텍스트를 가져오는 데 사용할 수 있는 SQL 핸들입니다.|63|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**ntext**|TriggerExecutionStats|1|예|  
|PlanHandle|**image**|트리거에 대한 컴파일된 계획의 계획 핸들입니다. dm_exec_query_plan 동적 관리 뷰를 사용하여 XML 계획을 가져오는 데 사용할 수 있습니다.|65|예|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Showplan XML for Query Compile 이벤트 클래스](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  
