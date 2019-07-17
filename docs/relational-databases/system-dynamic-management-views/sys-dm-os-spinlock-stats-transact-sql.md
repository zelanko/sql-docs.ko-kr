---
title: sys.dm_os_spinlock_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats
- sys.dm_os_spinlock_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_spinlock_stats dynamic management view
author: bluefooted
ms.author: pamela
ms.reviewer: maghan
manager: amitban
ms.openlocfilehash: eae0057441fe6bc356c7cea6c1e6ded829bbb9e6
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265695"
---
# <a name="sysdmosspinlockstats-transact-sql"></a>sys.dm_os_spinlock_stats (Transact SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

형식별으로 구성 하는 모든 스핀 잠금 대기에 대 한 정보를 반환 합니다.  
  

|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(256)**|Spinlock 형식의 이름입니다.|  
|충돌|**bigint**|Spinlock을 획득 하 려 스레드와 다른 스레드가 현재 차단 된 횟수 만큼 spinlock을 보유 합니다.|  
|회전|**bigint**|Spinlock을 획득 하는 동안 루프를 실행 하는 스레드를 다시 시도 횟수입니다.|  
|spins_per_collision|**real**|사용자가 충돌 당 작동의 비율입니다.|  
|sleep_time|**bigint**|스레드는 백오프를 발생 시 중지 데 걸린 시간 (밀리초) 시간의 양입니다.|  
|백오프|**int**|이 "회전" 하는 스레드 spinlock을 획득 하지 못했습니다 및 스케줄러를 생성 횟수입니다.|  


## <a name="permissions"></a>사용 권한  
온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 프리미엄 계층 필요는 `VIEW DATABASE STATE` 데이터베이스의 권한. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층에 필요 합니다 **서버 관리자** 요소나 **Azure Active Directory 관리자** 계정.    
  
## <a name="remarks"></a>설명  
 
 sys.dm_os_spinlock_stats는 spinlock 경합 원본을 확인에 사용할 수 있습니다. 일부 상황에서을 해결 하거나 spinlock 경합을 줄일 수 있습니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 고객 지원 서비스에 연락해야 할 경우도 있습니다.  
  
 Sys.dm_os_spinlock_stats의 내용을 사용 하 여 다시 설정할 수 있습니다 `DBCC SQLPERF` 다음과 같습니다.  
  
```  
DBCC SQLPERF ('sys.dm_os_spinlock_stats', CLEAR);  
GO  
```  
  
 이렇게 하면 모든 카운터가 0으로 다시 설정됩니다.  
  
> [!NOTE]  
>  이러한 통계는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작할 경우 지속되지 않습니다. 모든 데이터는 통계가 마지막으로 다시 설정된 이후나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 시작된 이후로 누적됩니다.  
  
## <a name="spinlocks"></a>Spinlock  
 Spinlock은 일반적으로 짧은 기간에 대 한 보유 하는 데이터 구조에 대 한 액세스를 serialize 하는 데 사용 하는 경량 동기화 개체입니다. 스레드를 다른 스레드에 의해 열리는지는 spinlock에 의해 보호 된 리소스에 액세스 하려고 하는 경우 스레드는 루프를 실행 또는 "실행" 시도 즉시 래치 또는 다른 리소스와 마찬가지로 스케줄러를 생성 하는 대신 다시 리소스에 액세스 대기 합니다. 스레드는 회전 리소스를 사용할 수 없거나 루프가 완료 될 때까지 시점에서 스레드 스케줄러 생성 되며 실행 가능 큐로 다시 돌아가서 계속 합니다. 이 방법은 과도 한 스레드 컨텍스트 전환이 줄일 수 있습니다. 하지만 spinlock에 대 한 경합이 높은 경우 중요 한 CPU 사용률을 관찰 될 수 있습니다.
   
 다음 표에서 가장 일반적인 spinlock 형식의 일부에 대해 간략하게 설명 합니다.  
  
|스핀 잠금 유형|설명|  
|-----------------|-----------------|  
|ABR|내부적으로만 사용됩니다.|
|ADB_CACHE|내부적으로만 사용됩니다.|
|ALLOC_CACHES_HASH|내부적으로만 사용됩니다.|
|APPENDONLY_STORAGE|내부적으로만 사용됩니다.|
|APRC_BACK_OFF_STATS|내부적으로만 사용됩니다.|
|APRC_EVENT_LIST|내부적으로만 사용됩니다.|
|APRC_QUEUE_LIST|내부적으로만 사용됩니다.|
|APRC_VALIDATION_QUEUE_LIST|내부적으로만 사용됩니다.|
|ASYNC_OP_ADMIN_CLIENT_REGISTRATION_LIST|내부적으로만 사용됩니다.|
|ASYNC_OP_ADMIN_WORK_REGISTRATION_HASH_TABLE|내부적으로만 사용됩니다.|
|ASYNCSTATSLIST|내부적으로만 사용됩니다.|
|BACKUP|내부적으로만 사용됩니다.|
|BACKUP_COPY_CONTEXT|내부적으로만 사용됩니다.|
|BACKUP_CTX|내부적으로만 사용됩니다.|
|BASE_XACT_HASH|내부적으로만 사용됩니다.|
|BLOCKER_ENUM|내부적으로만 사용됩니다.|
|BPREPARTITION|내부적으로만 사용됩니다.|
|BPWORKFILE|내부적으로만 사용됩니다.|
|BUF_HASH|내부적으로만 사용됩니다.|
|BUF_LINK|내부적으로만 사용됩니다.|
|BUF_WRITE_LOG|내부적으로만 사용됩니다.|
|CACHEOBJ_DBG|내부적으로만 사용됩니다.|
|CHANNELFORCECLOSEMANAGER|내부적으로만 사용됩니다.|
|CHECK_AGGREGATE_STATE|내부적으로만 사용됩니다.|
|CLR_HOSTTASK|내부적으로만 사용됩니다.|
|CLR_SPIN_LOCK|내부적으로만 사용됩니다.|
|CMED_DATABASE|내부적으로만 사용됩니다.|
|CMED_HASH_SET|내부적으로만 사용됩니다.|
|COLUMNDATASETSESSIONLIST|내부적으로만 사용됩니다.|
|COLUMNSTORE_HASHTABLE|내부적으로만 사용됩니다.|
|COLUMNSTOREBUILDSTATE_LIST|내부적으로만 사용됩니다.|
|COM_INIT|내부적으로만 사용됩니다.|
|커밋할 수|내부적으로만 사용됩니다.|
|COMPPLAN_SKELETON|내부적으로만 사용됩니다.|
|CONNECTION_MANAGER|내부적으로만 사용됩니다.|
|연결|내부적으로만 사용됩니다.|
|CSIBUILDMEM|내부적으로만 사용됩니다.|
|커서|내부적으로만 사용됩니다.|
|CURSQL|내부적으로만 사용됩니다.|
|DATAPORTCONSUMER|내부적으로만 사용됩니다.|
|DATAPORTSOURCEINFOCREDIT|내부적으로만 사용됩니다.|
|DATAPORTSOURCEINFOQUEUE|내부적으로만 사용됩니다.|
|DATASET_FREELIST|내부적으로만 사용됩니다.|
|DBCC_CHECK|내부적으로만 사용됩니다.|
|DBSEEDING_OPERATION|내부적으로만 사용됩니다.|
|DBT_HASH|내부적으로만 사용됩니다.|
|DBT_IO_LIST|내부적으로만 사용됩니다.|
|DBTABLE|메모리 내 데이터 구조에 해당 데이터베이스의 속성을 포함 하는 SQL Server의 모든 데이터베이스에 대 한 액세스를 제어 합니다. 참조 [이 문서에서는](https://techcommunity.microsoft.com/t5/SQL-Server/Improving-Concurrency-Scalability-of-SQL-Server-workload-by/ba-p/384789) 자세한 내용은 합니다. |
|DEFERRED_WF_EXT_DROP|내부적으로만 사용됩니다.|
|DEK_INSTANCE|내부적으로만 사용됩니다.|
|DELAYED_PARTITIONED_STACK|내부적으로만 사용됩니다.|
|DELETEBITMAP|내부적으로만 사용됩니다.|
|DIAG_MANAGER|내부적으로만 사용됩니다.|
|DIAG_OBJECT|내부적으로만 사용됩니다.|
|DIGEST_CACHE|내부적으로만 사용됩니다.|
|DINPBUF|내부적으로만 사용됩니다.|
|DIRECTLOGCONSUMER|내부적으로만 사용됩니다.|
|DP_LIST|남은 더티 페이지의 목록에 설정 하는 간접 검사점이 있는 데이터베이스에 대 한 액세스를 제어 합니다. 참조 [이 문서에서는](https://techcommunity.microsoft.com/t5/SQL-Server/Indirect-Checkpoint-and-tempdb-8211-the-good-the-bad-and-the-non/ba-p/385510) 자세한 내용은 합니다.|
|DROP|내부적으로만 사용됩니다.|
|DROP_TEMPO|내부적으로만 사용됩니다.|
|DROPPED_ALLOC_UNIT|내부적으로만 사용됩니다.|
|DTC_HASHTABLE|내부적으로만 사용됩니다.|
|DTT_LIST|내부적으로만 사용됩니다.|
|ENDD_LIST|내부적으로만 사용됩니다.|
|EXT_CACHE|내부적으로만 사용됩니다.|
|EXTENT_ACTIVATION|내부적으로만 사용됩니다.|
|FABRIC_DB_MGR_PTR|내부적으로만 사용됩니다.|
|FABRIC_LOG_MANAGEMENT_INPUT_VALUE|내부적으로만 사용됩니다.|
|FABRIC_REPLICA_TRANSPORT|내부적으로만 사용됩니다.|
|FABRIC_TVF_DATA_CONSUMER_LIST|내부적으로만 사용됩니다.|
|FABRIC_TVF_LOAD_LIB|내부적으로만 사용됩니다.|
|FCB_REPLICA_SYNC|내부적으로만 사용됩니다.|
|FGCB_PRP_FILL|내부적으로만 사용됩니다.|
|FILE_HANDLE_CACHE|내부적으로만 사용됩니다.|
|FILE_TABLE|내부적으로만 사용됩니다.|
|FILESTREAM_CHUNKER|내부적으로만 사용됩니다.|
|FREE_SPACE_CACHE_ENTRY|내부적으로만 사용됩니다.|
|FS_CONTAINER_LIST_WITH_DELETE|내부적으로만 사용됩니다.|
|FS_DELETED_FOLDER_CLEANUP|내부적으로만 사용됩니다.|
|FSAGENT|내부적으로만 사용됩니다.|
|FSGHOST_STATUS|내부적으로만 사용됩니다.|
|FT_INIT|내부적으로만 사용됩니다.|
|GHOST_FREE|내부적으로만 사용됩니다.|
|GHOST_HASH|내부적으로만 사용됩니다.|
|GLOBAL_SCHEDULER_LIST|내부적으로만 사용됩니다.|
|GLOBAL_TRACE_FLAGS|내부적으로만 사용됩니다.|
|GLOBALTRANS|내부적으로만 사용됩니다.|
|GROUP_COMMIT_FEEDBACK_LOOP|내부적으로만 사용됩니다.|
|GUARDIAN|내부적으로만 사용됩니다.|
|HADR_AGH_X_ACCESS|내부적으로만 사용됩니다.|
|HADR_AR_CONTROLLER_COLLECTION|내부적으로만 사용됩니다.|
|HADR_AR_DB_MGR|내부적으로만 사용됩니다.|
|HADR_AR_TRANSPORT|내부적으로만 사용됩니다.|
|HADR_COMPRESSION_MGR_POOL|내부적으로만 사용됩니다.|
|HADR_FABRIC_FACTORY|내부적으로만 사용됩니다.|
|HADR_PRIORITY_QUEUE|내부적으로만 사용됩니다.|
|HADR_TRANSPORT_CONTROL|내부적으로만 사용됩니다.|
|HADR_TRANSPORT_LIST|내부적으로만 사용됩니다.|
|HADRSEEDINGLIST|내부적으로만 사용됩니다.|
|HOBT_DROPPED|내부적으로만 사용됩니다.|
|HOBT_HASH|내부적으로만 사용됩니다.|
|HTTP|내부적으로만 사용됩니다.|
|HTTP_CONNCACHE|내부적으로만 사용됩니다.|
|HTTP_ENDPOINT|내부적으로만 사용됩니다.|
|IDENTITY|내부적으로만 사용됩니다.|
|INDEX_CREATE|내부적으로만 사용됩니다.|
|IO_DISPENSER_PAUSE|내부적으로만 사용됩니다.|
|IO_RG_VOLUME_HASHTABLE|내부적으로만 사용됩니다.|
|IOREQ|내부적으로만 사용됩니다.|
|ISSRESOURCE|내부적으로만 사용됩니다.|
|KTM_ENLISTMENT|내부적으로만 사용됩니다.|
|LANG_RES_LOAD|내부적으로만 사용됩니다.|
|LIVE_TARGET_TVF|내부적으로만 사용됩니다.|
|LOCK_FREE_LIST|내부적으로만 사용됩니다.|
|LOCK_HASH|데이터베이스에서 대기 중인 잠금에 대 한 정보를 저장 하는 잠금 관리자 해시 테이블에 대 한 액세스를 보호 합니다. 참조 [이 문서에서는](https://support.microsoft.com/kb/2926217) 자세한 내용은 합니다.|
|LOCK_NOTIFICATION|내부적으로만 사용됩니다.|
|LOCK_RESOURCE_ID|내부적으로만 사용됩니다.|
|LOCK_RW_ABTX_HASH_SET|내부적으로만 사용됩니다.|
|LOCK_RW_AGDB_HEALTH_DIAG|내부적으로만 사용됩니다.|
|LOCK_RW_CMED_HASH_SET|내부적으로만 사용됩니다.|
|LOCK_RW_DPT_TABLE|내부적으로만 사용됩니다.|
|LOCK_RW_IN_ROW_TRACKER|내부적으로만 사용됩니다.|
|LOCK_RW_LOGIN_RATE_STATS|내부적으로만 사용됩니다.|
|LOCK_RW_PVS_PAGE_TRACKER|내부적으로만 사용됩니다.|
|LOCK_RW_RBIO_REQ|내부적으로만 사용됩니다.|
|LOCK_RW_SECURITY_CACHE|내부적으로만 사용됩니다.|
|LOCK_RW_TEST|내부적으로만 사용됩니다.|
|LOCK_RW_WPR_BUCKET|내부적으로만 사용됩니다.|
|LOCK_SORT_STREAM|내부적으로만 사용됩니다.|
|LOCK_SQLSATELLITE_MESSAGE|내부적으로만 사용됩니다.|
|LOG_CONSOLIDATION|내부적으로만 사용됩니다.|
|LOG_RG_GOVERNOR|내부적으로만 사용됩니다.|
|LOGCACHE_ACCESS|내부적으로만 사용됩니다.|
|LOGFLUSHQ|내부적으로만 사용됩니다.|
|LOGIOSEQ|내부적으로만 사용됩니다.|
|LOGIOSEQMAPPENDINGMESSAGEQUEUE|내부적으로만 사용됩니다.|
|LOGLC|내부적으로만 사용됩니다.|
|LOGLFM|내부적으로만 사용됩니다.|
|LOGON_TRIGGER_CACHE|내부적으로만 사용됩니다.|
|LOGPOOL_HASHBUCKET|내부적으로만 사용됩니다.|
|LOGPOOL_REFCOUNTEDOBJECT|내부적으로만 사용됩니다.|
|LOGPOOL_SHAREDCACHEBUFFER|내부적으로만 사용됩니다.|
|LOGPOOL_SIZEPERRESOURCEPOOL|내부적으로만 사용됩니다.|
|LPE_BATCH|내부적으로만 사용됩니다.|
|LPE_SESSION|내부적으로만 사용됩니다.|
|LPE_SXTP|내부적으로만 사용됩니다.|
|LSID|내부적으로만 사용됩니다.|
|LSLIST|내부적으로만 사용됩니다.|
|LSNREFLIST|내부적으로만 사용됩니다.|
|LSS_SYNC_DTC|내부적으로만 사용됩니다.|
|MD_CHANGE_NOTIFICATION|내부적으로만 사용됩니다.|
|MDB_REMOTE_BATCH_STATS_HASH_TABLE|내부적으로만 사용됩니다.|
|MDB_REMOTE_SESSION_HASH_TABLE|내부적으로만 사용됩니다.|
|MEM_MGR|내부적으로만 사용됩니다.|
|MGR_CACHE|내부적으로만 사용됩니다.|
|MIGRATION_BUF_LIST|내부적으로만 사용됩니다.|
|NETCONN_ADDRESS|내부적으로만 사용됩니다.|
|ONDEMAND_TASK|내부적으로만 사용됩니다.|
|ONE_PROC_SIM_NODE_CONTEXT|내부적으로만 사용됩니다.|
|ONE_PROC_SIM_NODE_CONTEXT_LIST|내부적으로만 사용됩니다.|
|ONE_PROC_SIM_REPLICA_CONTEXT|내부적으로만 사용됩니다.|
|ONE_PROC_SIM_SERVICE_PARTITION|내부적으로만 사용됩니다.|
|OPT_IDX_MISS_ID|내부적으로만 사용됩니다.|
|OPT_IDX_MISS_KEY|내부적으로만 사용됩니다.|
|OPT_IDX_STATS|내부적으로만 사용됩니다.|
|OPT_INFO_MGR|내부적으로만 사용됩니다.|
|PAGE_WORKITEMLIST|내부적으로만 사용됩니다.|
|PAGECOPIER|내부적으로만 사용됩니다.|
|PARALLELREDOCACHE|내부적으로만 사용됩니다.|
|PARTITIONED_HEAP_FREE_LIST|내부적으로만 사용됩니다.|
|PROGRESS_REPORT|내부적으로만 사용됩니다.|
|QE_SHUTDOWN|내부적으로만 사용됩니다.|
|QSCAN_CACHE|내부적으로만 사용됩니다.|
|QUERY_EXEC_STATS|내부적으로만 사용됩니다.|
|QUERY_STORE_ASYNC_PERSIST|내부적으로만 사용됩니다.|
|QUERY_STORE_ASYNC_QUEUE_TLIST|내부적으로만 사용됩니다.|
|QUERY_STORE_CAPTURE_POLICY_INTERVAL|내부적으로만 사용됩니다.|
|QUERY_STORE_CAPTURE_POLICY_STATS|내부적으로만 사용됩니다.|
|QUERY_STORE_CAPTURE_POLICY_THRESHOLD|내부적으로만 사용됩니다.|
|QUERY_STORE_CURRENT_INTERVAL|내부적으로만 사용됩니다.|
|QUERY_STORE_HT_CACHE|내부적으로만 사용됩니다.|
|QUERY_STORE_LIST|내부적으로만 사용됩니다.|
|QUERY_STORE_PLAN_COMP_AGG|내부적으로만 사용됩니다.|
|QUERY_STORE_PLAN_LIST|내부적으로만 사용됩니다.|
|QUERY_STORE_READ_ONLY_FLAGS|내부적으로만 사용됩니다.|
|QUERY_STORE_SELF_AGG|내부적으로만 사용됩니다.|
|QUERY_STORE_STMT_COMP_AGG|내부적으로만 사용됩니다.|
|QUERYEXEC|내부적으로만 사용됩니다.|
|QUERYSCAN|내부적으로만 사용됩니다.|
|RANGE_GENERATION|내부적으로만 사용됩니다.|
|READ_AHEAD|내부적으로만 사용됩니다.|
|REDOMGRSTATE|내부적으로만 사용됩니다.|
|REMOTE_SESSION_CACHE|내부적으로만 사용됩니다.|
|REMOTEBLOCKIO|내부적으로만 사용됩니다.|
|REMOTEOP|내부적으로만 사용됩니다.|
|REPL_LOGREADER_HISTORY_CACHE|내부적으로만 사용됩니다.|
|REPL_LOGREADER_PERDB_HISTORY_CACHE|내부적으로만 사용됩니다.|
|RESMANAGER|내부적으로만 사용됩니다.|
|리소스|내부적으로만 사용됩니다.|
|RESQUEUE|내부적으로만 사용됩니다.|
|RFS_THREAD_QUEUE|내부적으로만 사용됩니다.|
|RG_TIMER|내부적으로만 사용됩니다.|
|ROWGROUP_VERSIONS|내부적으로만 사용됩니다.|
|RPCCHANNELPOOL|내부적으로만 사용됩니다.|
|RPCPACKAGE|내부적으로만 사용됩니다.|
|RPCREQUESTORCONTEXT|내부적으로만 사용됩니다.|
|RWLOCK_LAST|내부적으로만 사용됩니다.|
|SATELLITE_CONNECTION|내부적으로만 사용됩니다.|
|SBS_CLIENT_ENDPOINTS|내부적으로만 사용됩니다.|
|SBS_CLIENT_REQUESTS|내부적으로만 사용됩니다.|
|SBS_DISPATCH|내부적으로만 사용됩니다.|
|SBS_PENDING|내부적으로만 사용됩니다.|
|SBS_SERVER_XACT_TASK_PROXY|내부적으로만 사용됩니다.|
|SBS_TRANSPORT|내부적으로만 사용됩니다.|
|SBS_UCS_DISPATCH|내부적으로만 사용됩니다.|
|보안|내부적으로만 사용됩니다.|
|SECURITY_CACHE|내부적으로만 사용됩니다.|
|SECURITY_FEDAUTH_AAD_BECWSCONNS|내부적으로만 사용됩니다.|
|SEMANTIC_TICACHE|내부적으로만 사용됩니다.|
|SEQUENCED_OBJECT|내부적으로만 사용됩니다.|
|SEQUEUE_SIZED_THREADSAFE|내부적으로만 사용됩니다.|
|SESSION_KILLER|내부적으로만 사용됩니다.|
|SESSION_MANAGER|내부적으로만 사용됩니다.|
|SESSION_SEC_CONTEXT|내부적으로만 사용됩니다.|
|SETRANGE_SYNC|내부적으로만 사용됩니다.|
|SHARABLE_SESSION_OBJECTS|내부적으로만 사용됩니다.|
|SLO_INFO_LIST|내부적으로만 사용됩니다.|
|SNI|내부적으로만 사용됩니다.|
|SNI_NODE_PENDING_IO_QUEUE|내부적으로만 사용됩니다.|
|SOAPSESSIONS|내부적으로만 사용됩니다.|
|SOS_ABORT_TASK|내부적으로만 사용됩니다.|
|SOS_ACTIVEDESCRIPTOR|내부적으로만 사용됩니다.|
|SOS_BLOCKALLOCPARTIALLIST|내부적으로만 사용됩니다.|
|SOS_BLOCKDESCRIPTORBUCKET|내부적으로만 사용됩니다.|
|SOS_CACHESTORE|SQL Server 계획 캐시, 임시 테이블 캐시 등 다양 한 메모리 내 캐시에 대 한 액세스를 동기화합니다. 이 스핀 잠금 유형에 대 한 심각한 경합이 경합에서 특정 캐시에 따라 여러 가지를 의미할 수 있습니다. 연락처 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 이 스핀 잠금 유형 문제 해결 도움말에 대 한 고객 지원 서비스. |
|SOS_CACHESTORE_CLOCK|내부적으로만 사용됩니다.|
|SOS_CLOCKALG_INTERNODE_SYNC|내부적으로만 사용됩니다.|
|SOS_DEBUG_HOOK|내부적으로만 사용됩니다.|
|SOS_DESCDATABUFFERLIST|내부적으로만 사용됩니다.|
|SOS_LARGEPAGE_ALLOCATOR|내부적으로만 사용됩니다.|
|SOS_MINITHREAD|내부적으로만 사용됩니다.|
|SOS_NODE|내부적으로만 사용됩니다.|
|SOS_OBJECT_POOL|내부적으로만 사용됩니다.|
|SOS_OBJECT_STORE|내부적으로만 사용됩니다.|
|SOS_OOM_CHECK|내부적으로만 사용됩니다.|
|SOS_PHYS_PAGE_CACHE|내부적으로만 사용됩니다.|
|SOS_RESOURCE_CLERK_LIST|내부적으로만 사용됩니다.|
|SOS_RINGBUFFER_RECORD|내부적으로만 사용됩니다.|
|SOS_RW|내부적으로만 사용됩니다.|
|SOS_SATELLITE_USER_POOL|내부적으로만 사용됩니다.|
|SOS_SCHEDULER|내부적으로만 사용됩니다.|
|SOS_SELIST_SIZED_SLOCK|내부적으로만 사용됩니다.|
|SOS_SUSPEND_QUEUE|내부적으로만 사용됩니다.|
|SOS_SYSTHREAD|내부적으로만 사용됩니다.|
|SOS_SYSTHREAD_DISPATCHER|내부적으로만 사용됩니다.|
|SOS_TASK|내부적으로만 사용됩니다.|
|SOS_TLIST|내부적으로만 사용됩니다.|
|SOS_VM_LOW|내부적으로만 사용됩니다.|
|SOS_WAIT_STATS|내부적으로만 사용됩니다.|
|SOS_WAITABLE_ADDRESS_HASHBUCKET|내부적으로만 사용됩니다.|
|SPIN_EVENT_MUTEX|내부적으로만 사용됩니다.|
|SPL_DISPATCHER_LIST|내부적으로만 사용됩니다.|
|SPL_DISPATCHER_QUEUE|내부적으로만 사용됩니다.|
|SPL_NONYIELD_ANALYSIS|내부적으로만 사용됩니다.|
|SPL_QUERY_STORE_CTX_INITIALIZED|내부적으로만 사용됩니다.|
|SPL_QUERY_STORE_EXEC_STATS_AGG|내부적으로만 사용됩니다.|
|SPL_QUERY_STORE_EXEC_STATS_READ|내부적으로만 사용됩니다.|
|SPL_QUERY_STORE_STATS_COOKIE_CACHE|내부적으로만 사용됩니다.|
|SPL_SOS_DISPATCHER|내부적으로만 사용됩니다.|
|SPL_TDS_PKT_QUEUE|내부적으로만 사용됩니다.|
|SPL_XE_BUFFER_MGR|내부적으로만 사용됩니다.|
|SPL_XE_DISPATCHER_QUEUE|내부적으로만 사용됩니다.|
|SPL_XE_NOTIFICATION_CALLBACK_LIST|내부적으로만 사용됩니다.|
|SPL_XE_SESSION_EVENT_MGR|내부적으로만 사용됩니다.|
|SPL_XE_SESSION_MGR|내부적으로만 사용됩니다.|
|SPL_XE_SESSION_TARGET_MGR|내부적으로만 사용됩니다.|
|SPT_PROFILE|내부적으로만 사용됩니다.|
|SQL_MGR|내부적으로만 사용됩니다.|
|SQL_NORM|내부적으로만 사용됩니다.|
|SQLTRACE_FILE_BUFFER|내부적으로만 사용됩니다.|
|SRVPROC|내부적으로만 사용됩니다.|
|STACK_HASHER|내부적으로만 사용됩니다.|
|SUBLATCH|내부적으로만 사용됩니다.|
|SUBPDESC|내부적으로만 사용됩니다.|
|SUBPDESC_LIST|내부적으로만 사용됩니다.|
|SVC_BROKER_CTRL|내부적으로만 사용됩니다.|
|SVC_BROKER_DEBUG_LIST|내부적으로만 사용됩니다.|
|SVC_BROKER_LIST|내부적으로만 사용됩니다.|
|SVC_BROKER_OBJECT|내부적으로만 사용됩니다.|
|SYNCPOINT_RESOURCE|내부적으로만 사용됩니다.|
|TaskElapsedExecutionMonitor|내부적으로만 사용됩니다.|
|TDS_TVP|내부적으로만 사용됩니다.|
|TESTTEAM|내부적으로만 사용됩니다.|
|TESTTEAMEXPONENTIAL|내부적으로만 사용됩니다.|
|TESTTEAMEXPONENTIALTASTAS|내부적으로만 사용됩니다.|
|TESTTEAMTASTAS|내부적으로만 사용됩니다.|
|TMP_SESS_KEY|내부적으로만 사용됩니다.|
|TSQL_DEBUG|내부적으로만 사용됩니다.|
|TXFRM_REPL|내부적으로만 사용됩니다.|
|VDI_OPERATION|내부적으로만 사용됩니다.|
|WINFAB_REPORT_FAULT|내부적으로만 사용됩니다.|
|WRITE_PAGE_RECORDER|내부적으로만 사용됩니다.|
|X_PACKET_LIST|내부적으로만 사용됩니다.|
|X_PIPE|내부적으로만 사용됩니다.|
|X_PIPE_DEMAND|내부적으로만 사용됩니다.|
|X_PORT|내부적으로만 사용됩니다.|
|XACT_LOCK_INFO|내부적으로만 사용됩니다.|
|XACT_LOCKINFO_TASK|내부적으로만 사용됩니다.|
|XACT_WORKSPACE|내부적으로만 사용됩니다.|
|XCB|내부적으로만 사용됩니다.|
|XCB_FREE_LIST|내부적으로만 사용됩니다.|
|XCB_HASH|내부적으로만 사용됩니다.|
|XCHNG_TRACE|내부적으로만 사용됩니다.|
|XDES|내부적으로만 사용됩니다.|
|XDES_HASH|내부적으로만 사용됩니다.|
|XDESMGR|내부적으로만 사용됩니다.|
|XDESTABLELIST|내부적으로만 사용됩니다.|
|XE_RATE_LIMITER_STRETCHDB|내부적으로만 사용됩니다.|
|XE_SESSION_STORAGE|내부적으로만 사용됩니다.|
|XID_ARRAY|내부적으로만 사용됩니다.|
|XIO_BLOCKLIST|내부적으로만 사용됩니다.|
|XIO_REQSTR|내부적으로만 사용됩니다.|
|XIO_SEQNUMBUMP|내부적으로만 사용됩니다.|
|XIOSTATS|내부적으로만 사용됩니다.|
|XTP_RT_DATA_LIST|내부적으로만 사용됩니다.|
|XTS_MGR|내부적으로만 사용됩니다.|
|XVB_CSN|내부적으로만 사용됩니다.|
|XVB_LIST|내부적으로만 사용됩니다.|
 

  
## <a name="see-also"></a>관련 항목  
 
 [DBCC SQLPERF&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 
 [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  

 [SQL Server에서 중요 한 드라이버의 CPU 사용률이 Spinlock 있습니까?](https://techcommunity.microsoft.com/t5/SQL-Server-Support/When-is-Spinlock-a-Significant-Driver-of-CPU-utilization-in-SQL/ba-p/530142)

 [진단 및 해결 SQL Server에 대 한 Spinlock 경합](https://www.microsoft.com/download/details.aspx?id=26666)
  
  


