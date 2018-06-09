---
title: sys.query_store_wait_stats (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 18
author: AndrejsAnt
ms.author: AndrejsAnt
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: d4a7afdca88de97188577e726d203040e33c8c71
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "33182019"
---
# <a name="sysquerystorewaitstats-transact-sql"></a>sys.query_store_wait_stats (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  쿼리에 대 한 대기 정보에 대 한 정보를 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**wait_stats_id**|**bigint**|Plan_id, runtime_stats_interval_id, execution_type 및 wait_category에 대 한 대기 통계를 나타내는 행의 식별자입니다. 이 지난 런타임 통계 간격에 대 한 고유 합니다. 현재 활성 간격에 대 한 실행 유형을 execution_type 및 wait_category 나타내는 대기 범주를 사용 하 여 plan_id에서 참조 하는 계획에 대 한 대기 통계를 나타내는 여러 행 있을 수 있습니다. 일반적으로 한 행 나타냅니다 플러시 되도록 대기 통계를 디스크에 반면 다른 (s) 메모리 내 상태를 나타냅니다. 따라서 모든 간격에 대 한 실제 상태를 가져오려는 해야 집계 메트릭을 plan_id, runtime_stats_interval_id, execution_type 및 wait_category로 그룹화 합니다. |  
|**plan_id**|**bigint**|외래 키입니다. 조인 [sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)합니다.|  
|**runtime_stats_interval_id**|**bigint**|외래 키입니다. 조인 [sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)합니다.|  
|**wait_category**|**tinyint**|아래 표를 사용 하 여 대기 유형을 분류 하 고 대기 시간에서 집계 되는 다음 이러한 범주를 대기 합니다. 대기 범주마다 문제 해결을 위해 다른 후속 분석이 필요하지만 동일한 범주의 대기 유형은 매우 유사한 문제 해결 경험을 생성하므로 대기를 기반으로 해서 영향을 받는 쿼리를 제공하면 대부분의 조사를 성공적으로 완료할 수 있습니다.|
|**wait_category_desc**|**nvarchar(128)**|대기 범주 필드에 대 한 텍스트 설명을 아래 표를 검토 하십시오.|
|**execution_type**|**tinyint**|쿼리 실행의 형식을 결정합니다.<br /><br /> 0 – 일반적인 실행 (완료)<br /><br /> 3 – 클라이언트에서 시작 된 실행이 중단 됨<br /><br /> 4-예외 실행이 중단 됨|  
|**execution_type_desc**|**nvarchar(128)**|실행 형식 필드의 텍스트 설명:<br /><br /> 0 – 일반<br /><br /> 3 – 중단<br /><br /> 4-예외|  
|**total_query_wait_time_ms**|**bigint**|총 CPU 대기 시간 집계 간격 내에서 쿼리 계획에 대 한 범주 (밀리초 단위로 보고)를 기다립니다.|
|**avg_query_wait_time_ms**|**float**|평균 대기 기간 (밀리초 단위로 보고) 집계 간격 및 대기 범주 내에서 실행 당 쿼리 계획입니다.|
|**last_query_wait_time_ms**|**bigint**|마지막 대기 기간입니다. 집계 간격 내에서 쿼리 계획에 대 한 범주 (보고 밀리초에서)을 기다립니다.|
|**min_query_wait_time_ms**|**bigint**|최소 CPU 대기 시간 집계 간격 내에서 쿼리 계획에 대 한 범주 (밀리초 단위로 보고)를 기다립니다.|
|**max_query_wait_time_ms**|**bigint**|최대 CPU 대기 시간 집계 간격 내에서 쿼리 계획에 대 한 범주 (밀리초 단위로 보고)를 기다립니다.|
|**stdev_query_wait_time_ms**|**float**|쿼리와 집계 간격 내에서 쿼리 계획에 대 한 표준 편차 기간 대기 범주별 (보고 밀리초에서)입니다.|

 ## <a name="wait-categories-mapping-table"></a>매핑 테이블 범주를 대기 합니다.  
  *"%"를 와일드 카드로 사용 됩니다.*
  
|정수 값|대기 범주|대기 유형 범주에 포함|  
|-----------------|---------------|-----------------|  
|**0**|**알 수 없음**|Unknown |  
|**1**|**CPU**|SOS_SCHEDULER_YIELD|
|**2**|**작업자 스레드**|THREADPOOL|
|**3**|**잠금**|LCK_M_%|
|**4**|**래치**|LATCH_%|
|**5**|**버퍼 래치**|PAGELATCH_%|
|**6**|**버퍼 IO**|PAGEIOLATCH_%|
|**7**|**컴파일***|RESOURCE_SEMAPHORE_QUERY_COMPILE|
|**8**|**SQL CLR**|CLR%, SQLCLR%|
|**9**|**미러링**|DBMIRROR %|
|**10**|**트랜잭션**|XACT%, DTC%, TRAN_MARKLATCH_%, MSQL_XACT_%, TRANSACTION_MUTEX|
|**11**|**Idle**|SLEEP_%, LAZYWRITER_SLEEP, SQLTRACE_BUFFER_FLUSH, SQLTRACE_INCREMENTAL_FLUSH_SLEEP, SQLTRACE_WAIT_ENTRIES, FT_IFTS_SCHEDULER_IDLE_WAIT, XE_DISPATCHER_WAIT, REQUEST_FOR_DEADLOCK_SEARCH, LOGMGR_QUEUE, ONDEMAND_TASK_QUEUE, CHECKPOINT_QUEUE, XE_TIMER_EVENT|
|**12**|**선점형**|PREEMPTIVE_%|
|**13**|**Service Broker**|BROKER_ % **(않음 하지 BROKER_RECEIVE_WAITFOR)**|
|**14**|**트랜잭션 로그 IO**|LOGMGR, LOGBUFFER, LOGMGR_RESERVE_APPEND, LOGMGR_FLUSH, LOGMGR_PMM_LOG, CHKPT, WRITELOGF|
|**15**|**네트워크 IO**|ASYNC_NETWORK_IO, NET_WAITFOR_PACKET, PROXY_NETWORK_IO, EXTERNAL_SCRIPT_NETWORK_IOF|
|**16**|**Parallelism**|CXPACKET, EXCHANGE|
|**17**|**메모리**|RESOURCE_SEMAPHORE, CMEMTHREAD, CMEMPARTITIONED, EE_PMOLOCK, MEMORY_ALLOCATION_EXT, RESERVED_MEMORY_ALLOCATION_EXT, MEMORY_GRANT_UPDATE|
|**18**|**사용자 대기**|WAITFOR, WAIT_FOR_RESULTS, BROKER_RECEIVE_WAITFOR|
|**19**|**추적**|TRACEWRITE, SQLTRACE_LOCK, SQLTRACE_FILE_BUFFER, SQLTRACE_FILE_WRITE_IO_COMPLETION, SQLTRACE_FILE_READ_IO_COMPLETION, SQLTRACE_PENDING_BUFFER_WRITERS, SQLTRACE_SHUTDOWN, QUERY_TRACEOUT, TRACE_EVTNOTIFF|
|**20**|**전체 텍스트 검색**|FT_RESTART_CRAWL, 전체 텍스트 GATHERER, MSSEARCH, FT_METADATA_MUTEX, FT_IFTSHC_MUTEX, FT_IFTSISM_MUTEX, FT_IFTS_RWLOCK, FT_COMPROWSET_RWLOCK, FT_MASTER_MERGE, FT_PROPERTYLIST_CACHE FT_MASTER_MERGE_COORDINATOR, PWAIT_RESOURCE_SEMAPHORE_FT_ PARALLEL_QUERY_SYNC|
|**21**|**다른 디스크 IO**|ASYNC_IO_COMPLETION, IO_COMPLETION, BACKUPIO, WRITE_COMPLETION, IO_QUEUE_LIMIT, IO_RETRY|
|**22**|**복제**|SE_REPL_ %, REPL_ %, HADR_ % **(않음 하지 HADR_THROTTLE_LOG_RATE_GOVERNOR)**, REPLICA_WRITES, FCB_REPLICA_WRITE, FCB_REPLICA_READ, PWAIT_HADRSIM PWAIT_HADR_ %|
|**23**|**로그 속도 관리자**|LOG_RATE_GOVERNOR, POOL_LOG_RATE_GOVERNOR, HADR_THROTTLE_LOG_RATE_GOVERNOR, INSTANCE_LOG_RATE_GOVERNOR|

***컴파일** 대기 범주는 현재 지원 되지 않습니다. 

  
## <a name="permissions"></a>사용 권한  
 필요는 **VIEW DATABASE STATE** 권한.  
  
## <a name="see-also"></a>관련 항목  
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [쿼리 저장소 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
