---
title: sys.dm_os_latch_stats (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_latch_stats_TSQL
- dm_os_latch_stats_TSQL
- dm_os_latch_stats
- sys.dm_os_latch_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_latch_stats dynamic management view
ms.assetid: 2085d9fc-828c-453e-82ec-b54ed8347ae5
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eefaf7e71a3442a9a0cd38d3f169eef09d4ddfea
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmoslatchstats-transact-sql"></a>sys.dm_os_latch_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  클래스별로 구성된 모든 래치 대기에 대한 정보를 반환합니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_latch_stats**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|latch_class|**nvarchar(120)**|래치 클래스의 이름입니다.|  
|waiting_requests_count|**bigint**|이 클래스의 래치 대기 수입니다. 이 카운터는 래치 대기가 시작될 때 증가합니다.|  
|wait_time_ms|**bigint**|이 클래스의 총 래치 대기 시간(밀리초)입니다.<br /><br /> **참고:** 이 열에는 래치 대기가 끝날 때 및 래치 대기 동안 5 분 마다 업데이트 됩니다.|  
|max_wait_time_ms|**bigint**|메모리 개체가 이 래치를 기다린 최대 시간입니다. 이 값이 지나치게 높으면 내부 교착 상태가 발생한 것일 수 있습니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   
  
## <a name="remarks"></a>주의  
 sys.dm_os_latch_stats를 사용하면 여러 래치 클래스에 대한 상대적 대기 수와 대기 시간을 조사하여 래치 경합의 원인을 확인할 수 있습니다. 어떤 경우에는 래치 경합을 해결하거나 줄일 수 있습니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 고객 지원 서비스에 연락해야 할 경우도 있습니다.  
  
 다음과 같이 `DBCC SQLPERF`를 사용하여 sys.dm_os_latch_stats의 내용을 다시 설정할 수 있습니다.  
  
```  
DBCC SQLPERF ('sys.dm_os_latch_stats', CLEAR);  
GO  
```  
  
 이렇게 하면 모든 카운터가 0으로 다시 설정됩니다.  
  
> [!NOTE]  
>  이러한 통계는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작할 경우 지속되지 않습니다. 모든 데이터는 통계가 마지막으로 다시 설정된 이후나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 시작된 이후로 누적됩니다.  
  
## <a name="latches"></a>래치  
 래치는 다양한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에서 사용하는 경량 동기화 개체이며 주로 데이터베이스 페이지 동기화에 사용됩니다. 각 래치는 단일 할당 단위와 연결되어 있습니다.  
  
 충돌 모드의 다른 스레드에서 래치를 보유하기 때문에 래치 요청에 즉시 권한을 부여할 수 없을 때 래치 대기가 발생합니다. 잠금과 달리 래치는 작업 후 즉시 해제되는데 이는 쓰기 작업에서도 마찬가지입니다.  
  
 래치는 구성 요소와 용도에 기반하여 클래스로 그룹화됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에는 언제든지 특정 클래스의 래치가 0개 이상 존재할 수 있습니다.  
  
> [!NOTE]  
>  sys.dm_os_latch_stats는 즉시 권한이 부여되었거나 대기하지 않고 실패한 래치 요청을 추적하지 않습니다.  
  
 다음 표에서는 다양한 래치 클래스에 대한 간략한 설명을 제공합니다.  
  
|래치 클래스|Description|  
|-----------------|-----------------|  
|ALLOC_CREATE_RINGBUF|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 내부적으로 할당 링 버퍼 만들기의 동기화를 초기화하는 데 사용됩니다.|  
|ALLOC_CREATE_FREESPACE_CACHE|힙에 대한 내부 사용 가능한 공간 캐시의 동기화를 초기화하는 데 사용됩니다.|  
|ALLOC_CACHE_MANAGER|내부 일관성 테스트를 동기화하는 데 사용됩니다.|  
|ALLOC_FREESPACE_CACHE|힙과 BLOB(Binary Large Object)에 대한 사용 가능한 공간이 있는 페이지의 캐시에 대한 액세스를 동기화하는 데 사용됩니다. 이 클래스의 래치에 대한 경합은 동시에 여러 연결이 힙이나 BLOB에 행을 삽입하려고 할 때 발생할 수 있습니다. 개체를 분할하여 이 경합을 줄일 수 있습니다. 각 분할에는 자체 래치가 있습니다. 분할하면 여러 래치에 삽입이 분산됩니다.|  
|ALLOC_EXTENT_CACHE|할당되지 않는 페이지를 포함하는 익스텐트의 캐시에 대한 액세스를 동기화하는 데 사용됩니다. 이 클래스의 래치에 대한 경합은 동시에 여러 연결이 같은 할당 단위로 데이터 페이지를 할당하려고 할 때 발생할 수 있습니다. 이 할당 단위가 속한 개체를 분할하여 이 경합을 줄일 수 있습니다.|  
|ACCESS_METHODS_DATASET_PARENT|병렬 작업 동안 상위 데이터 집합에 대한 하위 데이터 집합 액세스를 동기화하는 데 사용됩니다.|  
|ACCESS_METHODS_HOBT_FACTORY|내부 해시 테이블에 대한 액세스를 동기화하는 데 사용됩니다.|  
|ACCESS_METHODS_HOBT|HoBt의 메모리 내 표현에 대한 액세스를 제어하는 데 사용됩니다.|  
|ACCESS_METHODS_HOBT_COUNT|HoBt 페이지 및 행 카운터에 대한 액세스를 동기화하는 데 사용됩니다.|  
|ACCESS_METHODS_HOBT_VIRTUAL_ROOT|내부 B-트리의 루트 페이지 추상화에 대한 액세스를 동기화하는 데 사용됩니다.|  
|ACCESS_METHODS_CACHE_ONLY_HOBT_ALLOC|작업 테이블 액세스를 동기화하는 데 사용됩니다.|  
|ACCESS_METHODS_BULK_ALLOC|대량 할당자 내의 액세스를 동기화하는 데 사용됩니다.|  
|ACCESS_METHODS_SCAN_RANGE_GENERATOR|병렬 검색 동안 범위 생성자에 대한 액세스를 동기화하는 데 사용됩니다.|  
|ACCESS_METHODS_KEY_RANGE_GENERATOR|키 범위 병렬 검색 동안 미리 읽기 작업에 대한 액세스를 동기화하는 데 사용됩니다.|  
|APPEND_ONLY_STORAGE_INSERT_POINT|빠른 추가 전용 저장 단위로 삽입을 동기화하는 데 사용됩니다.|  
|APPEND_ONLY_STORAGE_FIRST_ALLOC|추가 전용 저장 단위의 첫 번째 할당을 동기화하는 데 사용됩니다.|  
|APPEND_ONLY_STORAGE_UNIT_MANAGER|빠른 추가 전용 저장 단위 관리자 내의 내부 데이터 구조 액세스 동기화에 사용됩니다.|  
|APPEND_ONLY_STORAGE_MANAGER|빠른 추가 전용 저장 단위 관리자에서 축소 작업을 동기화하는 데 사용됩니다.|  
|BACKUP_RESULT_SET|병렬 백업 결과 집합을 동기화하는 데 사용됩니다.|  
|BACKUP_TAPE_POOL|백업 테이프 풀을 동기화하는 데 사용됩니다.|  
|BACKUP_LOG_REDO|백업 로그 다시 실행 작업을 동기화하는 데 사용됩니다.|  
|BACKUP_INSTANCE_ID|백업 성능 모니터 카운터에 대한 인스턴스 ID 생성을 동기화하는 데 사용됩니다.|  
|BACKUP_MANAGER|내부 백업 관리자를 동기화하는 데 사용됩니다.|  
|BACKUP_MANAGER_DIFFERENTIAL|DBCC를 사용하여 차등 백업 작업을 동기화하는 데 사용됩니다.|  
|BACKUP_OPERATION|데이터베이스, 로그 또는 파일 백업 같은 백업 작업 내의 내부 데이터 구조 동기화에 사용됩니다.|  
|BACKUP_FILE_HANDLE|복원 작업 동안 파일 열기 작업을 동기화하는 데 사용됩니다.|  
|BUFFER|데이터베이스 페이지에 대한 단기 액세스를 동기화하는 데 사용됩니다. 데이터베이스 페이지를 읽거나 수정하기 전에 버퍼 래치가 필요합니다. 버퍼 래치 경합은 핫 페이지와 느린 I/O를 비롯하여 여러 문제를 나타낼 수 있습니다.<br /><br /> 이 래치 클래스는 페이지 래치의 가능한 모든 용도에 적용됩니다. sys.dm_os_wait_stats는 페이지 래치 대기를 I/O 작업 및 읽기 인해 및 페이지에 대 한 쓰기 작업 간에 달라를 집니다.|  
|BUFFER_POOL_GROW|버퍼 풀 증가 작업 동안 내부 버퍼 관리자 동기화에 사용됩니다.|  
|DATABASE_CHECKPOINT|데이터베이스 내의 검사점 직렬화에 사용됩니다.|  
|CLR_PROCEDURE_HASHTABLE|내부적으로만 사용됩니다.|  
|CLR_UDX_STORE|내부적으로만 사용됩니다.|  
|CLR_DATAT_ACCESS|내부적으로만 사용됩니다.|  
|CLR_XVAR_PROXY_LIST|내부적으로만 사용됩니다.|  
|DBCC_CHECK_AGGREGATE|내부적으로만 사용됩니다.|  
|DBCC_CHECK_RESULTSET|내부적으로만 사용됩니다.|  
|DBCC_CHECK_TABLE|내부적으로만 사용됩니다.|  
|DBCC_CHECK_TABLE_INIT|내부적으로만 사용됩니다.|  
|DBCC_CHECK_TRACE_LIST|내부적으로만 사용됩니다.|  
|DBCC_FILE_CHECK_OBJECT|내부적으로만 사용됩니다.|  
|DBCC_PERF|내부 성능 모니터 카운터를 동기화하는 데 사용됩니다.|  
|DBCC_PFS_STATUS|내부적으로만 사용됩니다.|  
|DBCC_OBJECT_METADATA|내부적으로만 사용됩니다.|  
|DBCC_HASH_DLL|내부적으로만 사용됩니다.|  
|EVENTING_CACHE|내부적으로만 사용됩니다.|  
|FCB|파일 제어 블록에 대한 액세스를 동기화하는 데 사용됩니다.|  
|FCB_REPLICA|내부적으로만 사용됩니다.|  
|FGCB_ALLOC|파일 그룹 내에서 라운드 로빈 할당 정보에 대한 액세스를 동기화하는 데 사용됩니다.|  
|FGCB_ADD_REMOVE|ADD 및 DROP 파일 작업을 위해 파일 그룹에 대한 액세스를 동기화하는 데 사용됩니다.|  
|FILEGROUP_MANAGER|내부적으로만 사용됩니다.|  
|FILE_MANAGER|내부적으로만 사용됩니다.|  
|FILESTREAM_FCB|내부적으로만 사용됩니다.|  
|FILESTREAM_FILE_MANAGER|내부적으로만 사용됩니다.|  
|FILESTREAM_GHOST_FILES|내부적으로만 사용됩니다.|  
|FILESTREAM_DFS_ROOT|내부적으로만 사용됩니다.|  
|LOG_MANAGER|내부적으로만 사용됩니다.|  
|FULLTEXT_DOCUMENT_ID|내부적으로만 사용됩니다.|  
|FULLTEXT_DOCUMENT_ID_TRANSACTION|내부적으로만 사용됩니다.|  
|FULLTEXT_DOCUMENT_ID_NOTIFY|내부적으로만 사용됩니다.|  
|FULLTEXT_LOGS|내부적으로만 사용됩니다.|  
|FULLTEXT_CRAWL_LOG|내부적으로만 사용됩니다.|  
|FULLTEXT_ADMIN|내부적으로만 사용됩니다.|  
|FULLTEXT_AMDIN_COMMAND_CACHE|내부적으로만 사용됩니다.|  
|FULLTEXT_LANGUAGE_TABLE|내부적으로만 사용됩니다.|  
|FULLTEXT_CRAWL_DM_LIST|내부적으로만 사용됩니다.|  
|FULLTEXT_CRAWL_CATALOG|내부적으로만 사용됩니다.|  
|FULLTEXT_FILE_MANAGER|내부적으로만 사용됩니다.|  
|DATABASE_MIRRORING_REDO|내부적으로만 사용됩니다.|  
|DATABASE_MIRRORING_SERVER|내부적으로만 사용됩니다.|  
|DATABASE_MIRRORING_CONNECTION|내부적으로만 사용됩니다.|  
|DATABASE_MIRRORING_STREAM|내부적으로만 사용됩니다.|  
|QUERY_OPTIMIZER_VD_MANAGER|내부적으로만 사용됩니다.|  
|QUERY_OPTIMIZER_ID_MANAGER|내부적으로만 사용됩니다.|  
|QUERY_OPTIMIZER_VIEW_REP|내부적으로만 사용됩니다.|  
|RECOVERY_BAD_PAGE_TABLE|내부적으로만 사용됩니다.|  
|RECOVERY_MANAGER|내부적으로만 사용됩니다.|  
|SECURITY_OPERATION_RULE_TABLE|내부적으로만 사용됩니다.|  
|SECURITY_OBJPERM_CACHE|내부적으로만 사용됩니다.|  
|SECURITY_CRYPTO|내부적으로만 사용됩니다.|  
|SECURITY_KEY_RING|내부적으로만 사용됩니다.|  
|SECURITY_KEY_LIST|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_CONNECTION_RECEIVE|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_TRANSMISSION|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_TRANSMISSION_UPDATE|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_TRANSMISSION_STATE|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_TRANSMISSION_ERRORS|내부적으로만 사용됩니다.|  
|SSBXmitWork|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_MESSAGE_TRANSMISSION|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_MAP_MANAGER|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_HOST_NAME|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_READ_CACHE|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_WAITFOR_MANAGER| 인스턴스 수준 맵을 대기자 큐 동기화 하는 데 사용 합니다. 데이터베이스 ID, 데이터베이스 버전 및 큐 ID 튜플 당 하나의 큐가 있습니다. 많은 연결이 때이 클래스의 래치 경합이 발생할 수 있습니다: WAITFOR(RECEIVE)에서 대기 상태입니다. WAITFOR(RECEIVE); 호출 WAITFOR timeout; 초과 메시지를 표시 합니다. 커밋 또는 WAITFOR(RECEIVE); 포함 하는 트랜잭션이 롤백 WAITFOR(RECEIVE) 대기 상태에 있는 스레드의 수를 줄여 경합을 줄일 수 있습니다. |  
|SERVICE_BROKER_WAITFOR_TRANSACTION_DATA|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_TRANSMISSION_TRANSACTION_DATA|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_TRANSPORT|내부적으로만 사용됩니다.|  
|SERVICE_BROKER_MIRROR_ROUTE|내부적으로만 사용됩니다.|  
|TRACE_ID|내부적으로만 사용됩니다.|  
|TRACE_AUDIT_ID|내부적으로만 사용됩니다.|  
|TRACE|내부적으로만 사용됩니다.|  
|TRACE_CONTROLLER|내부적으로만 사용됩니다.|  
|TRACE_EVENT_QUEUE|내부적으로만 사용됩니다.|  
|TRANSACTION_DISTRIBUTED_MARK|내부적으로만 사용됩니다.|  
|TRANSACTION_OUTCOME|내부적으로만 사용됩니다.|  
|NESTING_TRANSACTION_READONLY|내부적으로만 사용됩니다.|  
|NESTING_TRANSACTION_FULL|내부적으로만 사용됩니다.|  
|MSQL_TRANSACTION_MANAGER|내부적으로만 사용됩니다.|  
|DATABASE_AUTONAME_MANAGER|내부적으로만 사용됩니다.|  
|UTILITY_DYNAMIC_VECTOR|내부적으로만 사용됩니다.|  
|UTILITY_SPARSE_BITMAP|내부적으로만 사용됩니다.|  
|UTILITY_DATABASE_DROP|내부적으로만 사용됩니다.|  
|UTILITY_DYNAMIC_MANAGER_VIEW|내부적으로만 사용됩니다.|  
|UTILITY_DEBUG_FILESTREAM|내부적으로만 사용됩니다.|  
|UTILITY_LOCK_INFORMATION|내부적으로만 사용됩니다.|  
|VERSIONING_TRANSACTION|내부적으로만 사용됩니다.|  
|VERSIONING_TRANSACTION_LIST|내부적으로만 사용됩니다.|  
|VERSIONING_TRANSACTION_CHAIN|내부적으로만 사용됩니다.|  
|VERSIONING_STATE|내부적으로만 사용됩니다.|  
|VERSIONING_STATE_CHANGE|내부적으로만 사용됩니다.|  
|KTM_VIRTUAL_CLOCK|내부적으로만 사용됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 
 [DBCC SQLPERF&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 
 [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


