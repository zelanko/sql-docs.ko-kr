---
title: sys.dm_exec_query_profiles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_profiles_TSQL
- sys.dm_exec_query_profiles_TSQL
- dm_exec_query_profiles
- sys.dm_exec_query_profiles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_profiles dynamic management view
ms.assetid: 54efc6cb-eea8-4f6d-a4d0-aa05eeb54081
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 87488f36a4b4b01181cd973a75d6e5c7f2e233d7
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860724"
---
# <a name="sysdmexecqueryprofiles-transact-sql"></a>sys.dm_exec_query_profiles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

쿼리가 실행되는 동안 실시간 쿼리 프로세스를 모니터링합니다. 예를 들어 이 DMV를 사용하여 느리게 실행되는 쿼리 부분을 결정합니다. 설명 필드에서 식별된 열을 사용하여 이 DMV를 다른 시스템 DMV와 조인합니다. 또는 타임스탬프 열을 사용하여 이 DMV를 다른 성능 카운터(예: 성능 모니터, xperf)와 조인합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
반환된 카운터는 연산자 및 스레드 기준입니다. 결과 동적 이며 기존 옵션의 결과 같은 일치 하지 않는 `SET STATISTICS XML ON` 는 출력을 만드는 쿼리가 완료 될 때입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|이 쿼리가 실행되는 세션을 식별합니다. dm_exec_sessions.session_id를 참조합니다.|  
|request_id|**int**|대상 요청을 식별합니다. dm_exec_sessions.request_id를 참조합니다.|  
|sql_handle|**varbinary(64)**|일괄 처리를 고유 하 게 식별 하는 토큰 또는 쿼리가 포함 된 저장된 프로시저입니다. dm_exec_query_stats.sql_handle을 참조합니다.|  
|plan_handle|**varbinary(64)**|실행 된 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 하는 토큰 및 해당 계획은 계획 캐시에 되거나 현재 실행 합니다. Dm_exec_query_stats.plan_handle를 참조합니다.|  
|physical_operator_name|**nvarchar(256)**|물리적 연산자 이름입니다.|  
|node_id|**int**|쿼리 트리에서 연산자 노드를 식별합니다.|  
|thread_id|**int**|동일한 쿼리 연산자 노드에 속하는 (병렬 쿼리)에 대한 스레드를 구분합니다.|  
|task_address|**varbinary(8)**|이 스레드가 사용하는 SQLOS 작업을 식별합니다. dm_os_tasks.task_address를 참조합니다.|  
|row_count|**bigint**|지금까지 연산자에서 반환한 행 수입니다.|  
|rewind_count|**bigint**|지금까지의 되감기 횟수입니다.|  
|rebind_count|**bigint**|지금까지의 다시 바인딩 횟수입니다.|  
|end_of_scan_count|**bigint**|지금까지의 검색 끝 수입니다.|  
|estimate_row_count|**bigint**|예상 행 수입니다. estimated_row_count를 실제 row_count와 비교하는 것이 유용할 수 있습니다.|  
|first_active_time|**bigint**|연산자가 밀리초 단위로 처음 호출된 시간입니다.|  
|last_active_time|**bigint**|연산자가 밀리초 단위로 마지막 호출된 시간입니다.|  
|open_time|**bigint**|열린 때의 타임스탬프입니다(밀리초).|  
|first_row_time|**bigint**|첫 번째 행이 열린 타임스탬프입니다(밀리초).|  
|last_row_time|**bigint**|마지막 행이 열린 타임스탬프입니다(밀리초).|  
|close_time|**bigint**|닫을 때의 타임스탬프입니다(밀리초).|  
|elapsed_time_ms|**bigint**|총 경과 시간 (밀리초) 지금까지 대상 노드의 작업으로 사용 합니다.|  
|cpu_time_ms|**bigint**|지금까지 대상 노드의 연산자 CPU 시간 (밀리초) 사용 하 여를 총입니다.|  
|database_id|**smallint**|읽기 및 쓰기를 수행하는 개체가 포함된 데이터베이스의 ID입니다.|  
|object_id|**int**|읽기 및 쓰기를 수행하는 개체의 ID입니다. sys.objects.object_id를 참조합니다.|  
|index_id|**int**|행 집합이 열린 인덱스입니다(있는 경우).|  
|scan_count|**bigint**|지금까지의 테이블/인덱스 검색 수 입니다.|  
|logical_read_count|**bigint**|지금까지의 논리적 읽기 수입니다.|  
|physical_read_count|**bigint**|지금까지의 물리적 읽기 수입니다.|  
|read_ahead_count|**bigint**|지금까지의 read-ahead 수입니다.|  
|write_page_count|**bigint**|실수로 인한 지금까지의 페이지 쓰기 수입니다.|  
|lob_logical_read_count|**bigint**|지금까지의 LOB 논리적 읽기 수입니다.|  
|lob_physical_read_count|**bigint**|지금까지의 LOB 물리적 읽기 수입니다.|  
|lob_read_ahead_count|**bigint**|지금까지의 LOB read-ahead 수입니다.|  
|segment_read_count|**int**|지금까지의 세그먼트 read-ahead 수입니다.|  
|segment_skip_count|**int**|지금까지 생략된 세그먼트 수입니다.| 
|actual_read_row_count|**bigint**|잔여 조건자가 적용 되기 전에 운영자를 읽은 행 수입니다.| 
|estimated_read_row_count|**bigint**|**적용 대상:** 부터는 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1. <br/>잔여 조건자가 적용 되기 전에 운영자가 읽을 것으로 예상 되는 행 수입니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 쿼리 계획 노드에 모든 I/O에 없는 경우 모든 O 관련 카운터가 NULL로 설정 됩니다.  
  
 이 DMV에서 보고 O 관련 카운터는에서 보고 하는 것 보다 더 세부적인 `SET STATISTICS IO` 다음 두 가지 방법으로:  
  
-   `SET STATISTICS IO` 모든 I/O를 함께 지정된 된 테이블에 대 한 카운터를 그룹화합니다. 이 DMV를 사용 하 여 테이블에 I/O를 수행 하는 쿼리 계획의 모든 노드에 대해 별도 카운터를 가져옵니다는 있습니다.  
  
-   병렬 스캔이 있는 경우 이 DMV는 스캔에 대해 작동하는 각 병렬 스레드의 카운터를 보고합니다.
 
부터 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1에는 *인프라를 프로 파일링 하는 표준 쿼리 실행 통계* 나란히 사용 하 여 존재를 *인프라를 프로 파일링 하는 간단한 쿼리 실행 통계* . `SET STATISTICS XML ON` 및 `SET STATISTICS PROFILE ON` 항상 사용 합니다 *인프라를 프로 파일링 하는 표준 쿼리 실행 통계*합니다. 에 대 한 `sys.dm_exec_query_profiles` 채울 인프라를 프로 파일링 하는 쿼리 중 하나 사용 해야 합니다. 자세한 내용은 [쿼리 프로파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)를 참조하세요.    

>[!NOTE]
> 조사 중인 쿼리를 시작 해야 **한 후** 인프라를 프로 파일링 하는 쿼리를 사용 하도록 설정 된, 쿼리가 시작 된 후 사용 하도록 설정 하면에서 결과가 나오지 않습니다 `sys.dm_exec_query_profiles`합니다. 인프라를 프로 파일링 하는 쿼리를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [인프라를 프로 파일링 하는 쿼리](../../relational-databases/performance/query-profiling-infrastructure.md)합니다.

## <a name="permissions"></a>사용 권한  

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   
   
## <a name="examples"></a>예  
 1단계: 사용 하 여 분석 쿼리를 실행 하려는 세션에 로그인 `sys.dm_exec_query_profiles`합니다. 프로 파일링을 위한 쿼리를 구성 하려면 `SET STATISTICS PROFILE ON`합니다. 동일한 세션에서 쿼리를 실행합니다.  
  
```sql  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above (not needed in SQL Server 2019)  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 2단계: 쿼리가 실행 되는 세션에서 다른 두 번째 세션에 로그인 합니다.  
  
 다음 문은 세션 54에서 현재 실행 중인 쿼리의 진행률을 요약합니다. 진행률을 요약하기 위해 이 문은 각 노드에 대한 모든 스레드의 총 출력 행 수를 계산하고 해당 노드의 추정된 출력 행 수와 비교합니다.  
  
```sql  
--Run this in a different session than the session in which your query is running. 
--Note that you may need to change session id 54 below with the session id you want to monitor.
SELECT node_id,physical_operator_name, SUM(row_count) row_count, 
  SUM(estimate_row_count) AS estimate_row_count, 
  CAST(SUM(row_count)*100 AS float)/SUM(estimate_row_count)  
FROM sys.dm_exec_query_profiles   
WHERE session_id=54
GROUP BY node_id,physical_operator_name  
ORDER BY node_id;  
```  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
 
