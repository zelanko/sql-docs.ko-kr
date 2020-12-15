---
description: sys.query_store_wait_stats (Transact-sql)
title: sys.query_store_wait_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2ab48b6155e26873c22a3b951ef65705d3addd79
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466924"
---
# <a name="sysquery_store_wait_stats-transact-sql"></a>sys.query_store_wait_stats (Transact-sql)

[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

  쿼리의 대기 정보에 대 한 정보를 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**wait_stats_id**|**bigint**|Plan_id, runtime_stats_interval_id execution_type 및 wait_category에 대 한 대기 통계를 나타내는 행의 식별자입니다. 이전 런타임 통계 간격에 대해서만 고유 합니다. 현재 활성 간격의 경우 plan_id에서 참조 하는 계획에 대 한 대기 통계를 나타내는 여러 행이 있을 수 있으며 execution_type로 표시 되는 실행 유형과 wait_category 표시 되는 대기 범주가 있습니다. 일반적으로 한 행은 디스크로 플러시된 대기 통계를 나타내고 다른 하나는 메모리 내 상태를 나타냅니다. 따라서 모든 간격에 대 한 실제 상태를 가져오려면 메트릭을 집계 해야 합니다. plan_id, runtime_stats_interval_id, execution_type 및 wait_category를 기준으로 그룹화 합니다. |  
|**plan_id**|**bigint**|외래 키입니다. [Transact-sql&#41;&#40;sys.query_store_plan ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)에 조인 합니다.|  
|**runtime_stats_interval_id**|**bigint**|외래 키입니다. [Transact-sql&#41;&#40;sys.query_store_runtime_stats_interval ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)에 조인 합니다.|  
|**wait_category**|**tinyint**|대기 유형은 아래 표를 사용 하 여 분류 되 고, 대기 시간은 이러한 대기 범주에 걸쳐 집계 됩니다. 다른 대기 범주에는 문제를 해결 하기 위해 다른 추가 분석이 필요 하지만 동일한 범주의 대기 유형은 유사한 문제 해결 환경을 제공 하며, 대기와 함께 영향을 받는 쿼리를 제공 하는 것은 이러한 조사를 모두 성공적으로 완료 하는 것입니다.|
|**wait_category_desc**|**nvarchar(128)**|대기 범주 필드에 대 한 텍스트 설명을 보려면 아래 표를 검토 하십시오.|
|**execution_type**|**tinyint**|쿼리 실행 유형을 결정 합니다.<br /><br /> 0-일반 실행 (완료 됨)<br /><br /> 3-클라이언트에서 시작한 실행 중단<br /><br /> 4-예외 실행 중단|  
|**execution_type_desc**|**nvarchar(128)**|실행 형식 필드에 대 한 텍스트 설명입니다.<br /><br /> 0-일반<br /><br /> 3-중단 됨<br /><br /> 4-예외|  
|**total_query_wait_time_ms**|**bigint**|`CPU wait`집계 간격 및 대기 범주 (밀리초 단위로 보고) 내의 쿼리 계획에 대 한 총 시간입니다.|
|**avg_query_wait_time_ms**|**float**|집계 간격 및 대기 범주 (밀리초 단위로 보고) 내에 실행 되는 쿼리 계획의 평균 대기 기간입니다.|
|**last_query_wait_time_ms**|**bigint**|집계 간격 및 대기 범주 (밀리초 단위로 보고) 내의 쿼리 계획에 대 한 마지막 대기 기간입니다.|
|**min_query_wait_time_ms**|**bigint**|`CPU wait`집계 간격 및 대기 범주 (밀리초 단위로 보고) 내의 쿼리 계획에 대 한 최소 시간입니다.|
|**max_query_wait_time_ms**|**bigint**|`CPU wait`집계 간격 및 대기 범주 (밀리초 단위로 보고) 내의 쿼리 계획에 대 한 최대 시간입니다.|
|**stdev_query_wait_time_ms**|**float**|`Query wait` 집계 간격 및 대기 범주 (밀리초 단위로 보고) 내의 쿼리 계획에 대 한 기간 표준 편차입니다.|

## <a name="wait-categories-mapping-table"></a>대기 범주 매핑 테이블

"%"는 와일드 카드로 사용 됩니다.
  
|정수 값|대기 범주|대기 유형은 범주에 포함 됩니다.|  
|-----------------|---------------|-----------------|  
|**0**|**알 수 없음**|알 수 없음 |  
|**1**|**CPU**|SOS_SCHEDULER_YIELD|
|**2**|**작업자 스레드**|THREADPOOL|
|**3**|**잠금**|LCK_M_%|
|**4**|**래치**|LATCH_%|
|**5**|**버퍼 래치**|PAGELATCH_%|
|**6**|**버퍼 IO**|PAGEIOLATCH_%|
|**7**|**컴파일** _|RESOURCE_SEMAPHORE_QUERY_COMPILE|
|_ *8**|**SQL CLR**|CLR%, SQLCLR%|
|**9**|**미러링**|DBMIRROR%|
|**10**|**트랜잭션**|XACT%, DTC%, TRAN_MARKLATCH_%, MSQL_XACT_%, TRANSACTION_MUTEX|
|**11**|**유휴 상태**|SLEEP_%, LAZYWRITER_SLEEP, SQLTRACE_BUFFER_FLUSH, SQLTRACE_INCREMENTAL_FLUSH_SLEEP, SQLTRACE_WAIT_ENTRIES, FT_IFTS_SCHEDULER_IDLE_WAIT, XE_DISPATCHER_WAIT, REQUEST_FOR_DEADLOCK_SEARCH, LOGMGR_QUEUE, ONDEMAND_TASK_QUEUE, CHECKPOINT_QUEUE, XE_TIMER_EVENT|
|**12**|**선점형**|PREEMPTIVE_%|
|**13**|**Service Broker**|BROKER_% **(BROKER_RECEIVE_WAITFOR 하지 않음)**|
|**14**|**트랜잭션 로그 IO**|LOGMGR, LOGMGR, LOGMGR_RESERVE_APPEND, LOGMGR_FLUSH, LOGMGR_PMM_LOG, CHKPT, WRITELOG|
|**15**|**네트워크 IO**|ASYNC_NETWORK_IO, NET_WAITFOR_PACKET, PROXY_NETWORK_IO, EXTERNAL_SCRIPT_NETWORK_IOF|
|**16**|**Parallelism**|CXPACKET, EXCHANGE, HT%, BMP%, BP%|
|**17**|**메모리**|RESOURCE_SEMAPHORE, CMEMTHREAD, CMEMTHREAD, EE_PMOLOCK, MEMORY_ALLOCATION_EXT, RESERVED_MEMORY_ALLOCATION_EXT, MEMORY_GRANT_UPDATE|
|**개가**|**사용자 대기**|WAITFOR, WAIT_FOR_RESULTS, BROKER_RECEIVE_WAITFOR|
|**mb**|**추적**|TRACEWRITE, SQLTRACE_LOCK, SQLTRACE_FILE_BUFFER, SQLTRACE_FILE_WRITE_IO_COMPLETION, SQLTRACE_FILE_READ_IO_COMPLETION, SQLTRACE_PENDING_BUFFER_WRITERS, SQLTRACE_SHUTDOWN, QUERY_TRACEOUT, TRACE_EVTNOTIFF|
|**20**|**전체 텍스트 검색**|FT_RESTART_CRAWL, 전체 텍스트 GATHERER, MSSEARCH, FT_METADATA_MUTEX, FT_IFTSHC_MUTEX, FT_IFTSISM_MUTEX, FT_IFTS_RWLOCK, FT_COMPROWSET_RWLOCK, FT_MASTER_MERGE, FT_PROPERTYLIST_CACHE, FT_MASTER_MERGE_COORDINATOR|
|**일**|**기타 디스크 IO**|ASYNC_IO_COMPLETION, IO_COMPLETION, BACKUPIO, WRITE_COMPLETION, IO_QUEUE_LIMIT, IO_RETRY|
|**22**|**복제**|SE_REPL_%, REPL_%, HADR_% **(HADR_THROTTLE_LOG_RATE_GOVERNOR는 아님)**, PWAIT_HADR_%, REPLICA_WRITES, FCB_REPLICA_WRITE, FCB_REPLICA_READ, PWAIT_HADRSIM|
|**23**|**로그 전송률 관리자**|LOG_RATE_GOVERNOR, POOL_LOG_RATE_GOVERNOR, HADR_THROTTLE_LOG_RATE_GOVERNOR, INSTANCE_LOG_RATE_GOVERNOR|

**컴파일** 대기 범주는 현재 지원 되지 않습니다.

## <a name="permissions"></a>사용 권한

 `VIEW DATABASE STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목

- [sys.database_query_store_options&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)
- [sys.query_context_settings&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)
- [sys.query_store_plan&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)
- [sys.query_store_query&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)
- [sys.query_store_query_text&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)
- [sys.query_store_runtime_stats_interval&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)
- [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)
- [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
