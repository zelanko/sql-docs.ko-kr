---
title: sys.query_store_wait_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.query_store_wait_stats
- query_store_wait_stats
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_wait_stats catalog view
- sys.query_store_wait_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 43cd85210c437520d2f72b7e9a16fbe2aab84514
ms.sourcegitcommit: b51edbe07a0a2fdb5f74b5874771042400baf919
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/28/2019
ms.locfileid: "55087842"
---
# <a name="sysquerystorewaitstats-transact-sql"></a>sys.query_store_wait_stats (Transact SQL)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  쿼리에 대 한 대기 정보에 대 한 정보를 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**wait_stats_id**|**bigint**|Plan_id, runtime_stats_interval_id, execution_type 및 wait_category 대기 통계를 나타내는 행의 식별자입니다. 이 지난 런타임 통계 간격 동안만 고유 합니다. 현재 활성 간격 execution_type 및 wait_category 나타내는 대기 범주를 나타내는 실행 형식과 plan_id에서 참조 하는 계획에 대 한 대기 통계를 나타내는 여러 행 있을 수 있습니다. 일반적으로 행이 하나씩 나타냅니다 플러시 되도록 대기 통계를 디스크에 다른 (s) 메모리 내 상태를 나타냅니다. 따라서 간격에 대 한 실제 상태를 가져오려는 해야 집계 메트릭 plan_id, runtime_stats_interval_id, execution_type 및 wait_category 그룹화 합니다. |  
|**plan_id**|**bigint**|외래 키입니다. 에 조인 [sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)합니다.|  
|**runtime_stats_interval_id**|**bigint**|외래 키입니다. 에 조인 [sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)합니다.|  
|**wait_category**|**tinyint**|아래 테이블을 사용 하 여 대기 유형을 분류 되며 대기 시간 집계 한 다음 이러한 대기 범주. 대기 범주 마다 문제를 해결 하지만 유사한 문제 해결 환경의 형식을 동일한 범주 잠재 고객에서 대기 하는 다른 후속 분석 하며 완료 하려면 누락 된 부분에는 또한 대기에 영향을 받는 쿼리를 제공 합니다 대부분의 조사 했습니다.|
|**wait_category_desc**|**nvarchar(128)**|대기 범주 필드의 텍스트 설명에 대 한 아래 표를 검토 합니다.|
|**execution_type**|**tinyint**|쿼리 실행의 유형을 결정 합니다.<br /><br /> 0-일반 실행 (완료)<br /><br /> 3-클라이언트에서 시작한 실행을 중단 했습니다.<br /><br /> 4-예외 실행이 중단 됨|  
|**execution_type_desc**|**nvarchar(128)**|실행 형식 필드의 텍스트 설명:<br /><br /> 0-일반<br /><br /> 3-중단<br /><br /> 4 -  Exception|  
|**total_query_wait_time_ms**|**bigint**|총 `CPU wait` 집계 간격 내에서 쿼리 계획에 대 한 시간 및 대기 범주 (밀리초 단위로 보고 됨).|
|**avg_query_wait_time_ms**|**float**|평균 대기 시간 (밀리초 단위로 보고 됨)는 집계 간격 및 대기 범주 내에서 실행 당 쿼리 계획에 대 한입니다.|
|**last_query_wait_time_ms**|**bigint**|마지막으로 집계 간격 내에서 쿼리 계획에 대 한 기간 대기 및 대기 범주 (밀리초 단위로 보고 됨).|
|**min_query_wait_time_ms**|**bigint**|최소 `CPU wait` 집계 간격 내에서 쿼리 계획에 대 한 시간 및 대기 범주 (밀리초 단위로 보고 됨).|
|**max_query_wait_time_ms**|**bigint**|최대 `CPU wait` 집계 간격 내에서 쿼리 계획에 대 한 시간 및 대기 범주 (밀리초 단위로 보고 됨).|
|**stdev_query_wait_time_ms**|**float**|`Query wait` 쿼리에 대 한 표준 편차 기간 집계 간격 내에서 계획 하 고 대기 범주 (밀리초 단위로 보고 됨).|

## <a name="wait-categories-mapping-table"></a>대기 범주 테이블 매핑

"%"를 와일드 카드로 사용 됩니다.
  
|정수 값|대기 범주|대기 형식 범주에 포함 됩니다.|  
|-----------------|---------------|-----------------|  
|**0**|**알 수 없음**|알 수 없음 |  
|**1**|**CPU**|SOS_SCHEDULER_YIELD|
|**2**|**작업자 스레드**|THREADPOOL|
|**3**|**잠금**|LCK_M_%|
|**4**|**Latch**|LATCH_%|
|**5**|**버퍼 래치**|PAGELATCH_%|
|**6**|**버퍼 IO**|PAGEIOLATCH_%|
|**7**|**컴파일***|RESOURCE_SEMAPHORE_QUERY_COMPILE|
|**8**|**SQL CLR**|CLR%, SQLCLR%|
|**9**|**미러링**|DBMIRROR%|
|**10**|**트랜잭션**|XACT%, DTC%, TRAN_MARKLATCH_%, MSQL_XACT_%, TRANSACTION_MUTEX|
|**11**|**Idle**|SLEEP_%, LAZYWRITER_SLEEP, SQLTRACE_BUFFER_FLUSH, SQLTRACE_INCREMENTAL_FLUSH_SLEEP, SQLTRACE_WAIT_ENTRIES, FT_IFTS_SCHEDULER_IDLE_WAIT, XE_DISPATCHER_WAIT, REQUEST_FOR_DEADLOCK_SEARCH, LOGMGR_QUEUE, ONDEMAND_TASK_QUEUE, CHECKPOINT_QUEUE, XE_TIMER_EVENT|
|**12**|**Preemptive**|PREEMPTIVE_%|
|**13**|**Service Broker**|BROKER_ % **(하지만 하지 BROKER_RECEIVE_WAITFOR)**|
|**14**|**Tran Log IO**|LOGMGR, LOGBUFFER, LOGMGR_RESERVE_APPEND, LOGMGR_FLUSH, LOGMGR_PMM_LOG, CHKPT, WRITELOGF|
|**15**|**네트워크 IO**|ASYNC_NETWORK_IO, NET_WAITFOR_PACKET, PROXY_NETWORK_IO, EXTERNAL_SCRIPT_NETWORK_IOF|
|**16**|**Parallelism**|CXPACKET, EXCHANGE|
|**17**|**메모리**|RESOURCE_SEMAPHORE, CMEMTHREAD, CMEMPARTITIONED, EE_PMOLOCK, MEMORY_ALLOCATION_EXT, RESERVED_MEMORY_ALLOCATION_EXT, MEMORY_GRANT_UPDATE|
|**18**|**사용자의 대기 시간**|WAITFOR, WAIT_FOR_RESULTS, BROKER_RECEIVE_WAITFOR|
|**19**|**추적**|TRACEWRITE, SQLTRACE_LOCK, SQLTRACE_FILE_BUFFER, SQLTRACE_FILE_WRITE_IO_COMPLETION, SQLTRACE_FILE_READ_IO_COMPLETION, SQLTRACE_PENDING_BUFFER_WRITERS, SQLTRACE_SHUTDOWN, QUERY_TRACEOUT, TRACE_EVTNOTIFF|
|**20**|**전체 텍스트 검색**|FT_RESTART_CRAWL, 전체 텍스트 GATHERER, MSSEARCH, FT_METADATA_MUTEX, FT_IFTSHC_MUTEX, FT_IFTSISM_MUTEX, FT_IFTS_RWLOCK, FT_COMPROWSET_RWLOCK, FT_MASTER_MERGE, FT_PROPERTYLIST_CACHE FT_MASTER_MERGE_COORDINATOR, PWAIT_RESOURCE_SEMAPHORE_FT_ PARALLEL_QUERY_SYNC|
|**21**|**다른 디스크 IO**|ASYNC_IO_COMPLETION, IO_COMPLETION, BACKUPIO, WRITE_COMPLETION, IO_QUEUE_LIMIT, IO_RETRY|
|**22**|**복제**|SE_REPL_ REPL_ %, %, %HADR_ **(하지만 하지 HADR_THROTTLE_LOG_RATE_GOVERNOR)**, REPLICA_WRITES FCB_REPLICA_WRITE, FCB_REPLICA_READ, PWAIT_HADRSIM PWAIT_HADR_ %|
|**23**|**로그 Rate Governor**|LOG_RATE_GOVERNOR, POOL_LOG_RATE_GOVERNOR, HADR_THROTTLE_LOG_RATE_GOVERNOR, INSTANCE_LOG_RATE_GOVERNOR|

**컴파일** 대기 범주는 현재 지원 되지 않습니다.

## <a name="permissions"></a>사용 권한

 `VIEW DATABASE STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목

- [sys.database_query_store_options&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)
- [sys.query_context_settings&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)
- [sys.query_store_plan&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)
- [sys.query_store_query&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)
- [sys.query_store_query_text&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)
- [sys.query_store_runtime_stats_interval&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)
- [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)
- [쿼리 저장소 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
