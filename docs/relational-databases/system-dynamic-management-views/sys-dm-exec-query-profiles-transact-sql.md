---
description: sys.dm_exec_query_profiles(Transact-SQL)
title: sys.dm_exec_query_profiles (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/25/2019
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
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 332b554797282510463ae3ec837fb00256db31b3
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97330891"
---
# <a name="sysdm_exec_query_profiles-transact-sql"></a>sys.dm_exec_query_profiles(Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

쿼리가 실행되는 동안 실시간 쿼리 프로세스를 모니터링합니다. 예를 들어 이 DMV를 사용하여 느리게 실행되는 쿼리 부분을 결정합니다. 설명 필드에서 식별된 열을 사용하여 이 DMV를 다른 시스템 DMV와 조인합니다. 또는 타임스탬프 열을 사용하여 이 DMV를 다른 성능 카운터(예: 성능 모니터, xperf)와 조인합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
반환된 카운터는 연산자 및 스레드 기준입니다. 결과는 동적 이며 `SET STATISTICS XML ON` 쿼리가 완료 될 때만 출력을 만드는 것과 같은 기존 옵션의 결과와 일치 하지 않습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|이 쿼리가 실행되는 세션을 식별합니다. dm_exec_sessions.session_id를 참조합니다.|  
|request_id|**int**|대상 요청을 식별합니다. dm_exec_sessions.request_id를 참조합니다.|  
|sql_handle|**varbinary(64)**|쿼리가 속하는 일괄 처리 또는 저장 프로시저를 고유 하 게 식별 하는 토큰입니다. dm_exec_query_stats.sql_handle을 참조합니다.|  
|plan_handle|**varbinary(64)**|실행 된 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 하는 토큰 이며 계획 캐시에 있거나 현재 실행 중인 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 합니다. Dm_exec_query_stats. plan_handle를 참조 하세요.|  
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
|elapsed_time_ms|**bigint**|지금까지 대상 노드의 작업에서 사용한 총 경과 시간 (밀리초)입니다.|  
|cpu_time_ms|**bigint**|지금까지 대상 노드의 작업에서 사용 하는 총 CPU 시간 (밀리초)입니다.|  
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
|actual_read_row_count|**bigint**|잔여 조건자를 적용 하기 전에 연산자가 읽은 행 수입니다.| 
|estimated_read_row_count|**bigint**|**적용 대상:** S p [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 1 부터는 <br/>나머지 조건자가 적용 되기 전에 연산자에서 읽을 수 있는 것으로 예상 되는 행 수입니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 쿼리 계획 노드에 i/o가 없는 경우 모든 i/o 관련 카운터가 NULL로 설정 됩니다.  
  
 이 DMV에서 보고 하는 i/o 관련 카운터는 `SET STATISTICS IO` 다음 두 가지 방법으로에서 보고 되는 것 보다 더 세분화 됩니다.  
  
-   `SET STATISTICS IO` 지정 된 테이블에 대 한 모든 i/o의 카운터를 그룹화 합니다. 이 DMV를 사용 하 여 테이블에 i/o를 수행 하는 쿼리 계획의 모든 노드에 대해 별도의 카운터를 가져옵니다.  
  
-   병렬 스캔이 있는 경우 이 DMV는 스캔에 대해 작동하는 각 병렬 스레드의 카운터를 보고합니다.
 
S p 1 부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] *표준 쿼리 실행 통계를 프로 파일링* 하는 것이 *경량 쿼리 실행 통계 프로 파일링 인프라* 와 나란히 있습니다. `SET STATISTICS XML ON` 및는 `SET STATISTICS PROFILE ON` 항상 *표준 쿼리 실행 통계 프로 파일링 인프라* 를 사용 합니다. 를 `sys.dm_exec_query_profiles` 채우도록 쿼리 프로 파일링 인프라 중 하나를 사용 하도록 설정 해야 합니다. 자세한 내용은 [쿼리 프로파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)를 참조하세요.    

>[!NOTE]
> 조사 중인 쿼리는 쿼리 프로 파일링 인프라를 사용 하도록 설정한 **후** 시작 해야 합니다. 쿼리를 시작한 후에 사용 하도록 설정 하면에서 결과가 생성 되지 않습니다 `sys.dm_exec_query_profiles` . 쿼리 프로 파일링 인프라를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [쿼리 프로 파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)를 참조 하세요.

## <a name="permissions"></a>사용 권한  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]및 AZURE SQL Managed Instance에는 `VIEW DATABASE STATE` 데이터베이스 역할의 권한 및 멤버 자격이 필요 `db_owner` 합니다.   
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에서 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   
   
## <a name="examples"></a>예제  
 1 단계: 분석할 쿼리를 실행 하려는 세션에 로그인 `sys.dm_exec_query_profiles` 합니다. 프로 파일링 사용을 위해 쿼리를 구성 `SET STATISTICS PROFILE ON` 합니다. 동일한 세션에서 쿼리를 실행합니다.  
  
```sql  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above (not needed in SQL Server 2019)  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 2 단계: 쿼리가 실행 중인 세션과 다른 두 번째 세션에 로그인 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
 
