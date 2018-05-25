---
title: sys.dm_db_wait_stats (Azure SQL 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_wait_stats_TSQL
- dm_db_wait_stats
- sys.dm_db_wait_stats
- sys.dm_db_wait_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_wait_stats dynamic management view
- dm_db_wait_stats
ms.assetid: 00abd0a5-bae0-4d71-b173-f7a14cddf795
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: af54ac9890cf903e0646d9b6d8eefe031924ffce
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmdbwaitstats-azure-sql-database"></a>sys.dm_db_wait_stats(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  작업 중 실행 중인 스레드로 인해 발생한 모든 대기에 대한 정보를 반환합니다. 이 집계 뷰를 사용하여 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]와 관련된 성능 문제뿐 아니라 특정 쿼리 및 일괄 처리와 관련된 성능 문제도 진단할 수 있습니다.  
  
 쿼리 실행 중에 특정 유형의 대기 시간이 쿼리 내의 병목 또는 대기 지점을 나타낼 수 있습니다. 마찬가지로 높은 대기 시간이나 서버 전체의 대기 횟수가 서버 인스턴스 내의 쿼리 상호 작용에서 병목 또는 핫 스폿을 나타낼 수 있습니다. 예를 들어 잠금 대기는 쿼리의 데이터 경합을, 페이지 IO 래치 대기는 느린 IO 응답 시간을, 페이지 래치 업데이트 대기는 잘못된 파일 레이아웃을 나타냅니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar(60)**|대기 유형의 이름입니다. 자세한 내용은 참조 [대기 유형](#WaitTypes)이 항목의 뒷부분에 나오는 합니다.|  
|waiting_tasks_count|**bigint**|이 대기 유형의 대기 수입니다. 이 카운터는 각 대기가 시작될 때 증가합니다.|  
|wait_time_ms|**bigint**|이 대기 유형의 총 대기 시간(밀리초)입니다. 이 시간은 signal_wait_time_ms를 포함합니다.|  
|max_wait_time_ms|**bigint**|이 대기 유형의 최대 대기 시간입니다.|  
|signal_wait_time_ms|**bigint**|대기 스레드가 신호를 받은 시간과 실행을 시작한 시간 사이의 차이입니다.|  
  
## <a name="remarks"></a>주의  
  
-   이 동적 관리 뷰에는 현재 데이터베이스에 대한 데이터만 표시됩니다.  
  
-   이 동적 관리 뷰는 완료된 대기 시간을 보여 줍니다. 현재 대기 시간은 표시되지 않습니다.  
  
-   카운터는 데이터베이스가 이동되거나 오프라인 상태인 경우 언제든지 0으로 다시 설정됩니다.  
  
-   다음 중 하나라도 해당되면 SQL Server 작업자 스레드가 대기하는 것으로 간주되지 않습니다.  
  
    -   리소스를 사용 가능합니다.  
  
    -   큐가 비어 있지 않습니다.  
  
    -   외부 프로세스가 완료됩니다.  
  
-   이러한 통계는 SQL Database 장애 조치(failover) 이벤트 발생 시 지속되지 않으며 모든 데이터는 통계가 마지막으로 다시 설정된 이후로 누적됩니다.  
  
## <a name="permissions"></a>Permissions  
 서버에 대한 VIEW DATABASE STATE 권한이 필요합니다.  
  
##  <a name="WaitTypes"></a> 대기 유형  
 리소스 대기  
 리소스 대기는 다른 작업자가 사용하고 있거나 아직 제공되지 않아서 사용할 수 없는 리소스에 대한 액세스를 요청하는 경우에 발생합니다. 리소스 대기의 예로는 잠금, 래치, 네트워크 및 디스크 I/O 대기가 있습니다. 잠금 및 래치 대기는 동기화 개체에 대한 대기입니다.  
  
 큐 대기  
 큐 대기는 작업자가 유휴 상태로 작업이 할당될 때까지 대기하는 경우에 발생합니다. 큐 대기는 교착 상태 모니터 및 삭제된 레코드 정리 작업 같은 시스템 백그라운드 태스크에서 가장 많이 발생합니다. 이러한 태스크는 작업 큐에 작업 요청이 배치될 때까지 대기합니다. 큐에 새 패킷이 배치되지 않았어도 큐 대기가 정기적으로 활성화될 수 있습니다.  
  
 외부 대기  
 외부 대기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업자가 확장 저장 프로시저 호출 또는 연결된 서버 쿼리 같은 외부 이벤트가 완료될 때까지 대기하는 경우에 발생합니다. 차단 문제를 진단할 때는 작업자가 외부 코드를 일부 실행하고 있을 수 있기 때문에 외부 대기가 항상 작업자가 유휴 상태임을 의미하지는 않는다는 점을 유념하세요.  
  
 스레드가 더 이상 대기하지 않더라도 즉시 스레드 실행을 시작하지는 않습니다. 그와 같은 스레드가 실행 가능한 작업자 큐의 첫 번째 항목이고 퀀텀이 스케줄러에서 실행될 때까지 대기해야 하기 때문입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대기 시간 카운터는 **bigint** 값 및 많지 않기 같이 카운터가 쉽게 롤오버의 이전 버전에서의 해당 카운터 만큼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 다음 표에서는 태스크에서 발생한 대기 유형을 나열합니다.  
  
|대기 유형|Description|  
|---------------|-----------------|  
|ABR|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|ASSEMBLY_LOAD|어셈블리 로드에 대한 단독 액세스 중에 발생합니다.|  
|ASYNC_DISKPOOL_LOCK|파일 만들기 또는 초기화 같은 태스크를 수행하고 있는 병렬 스레드를 동기화하려고 하는 경우에 발생합니다.|  
|ASYNC_IO_COMPLETION|태스크가 I/O가 완료될 때까지 대기하는 경우에 발생합니다.|  
|ASYNC_NETWORK_IO|태스크가 네트워크 뒤에서 차단되는 경우에 네트워크 쓰기 중에 발생합니다. 클라이언트가 서버의 데이터를 처리하고 있는지 확인합니다.|  
|AUDIT_GROUPCACHE_LOCK|특수 캐시에 대한 액세스를 제어하는 잠금을 기다리는 경우에 발생합니다. 캐시에는 각 감사 동작 그룹을 감사하는 데 사용되는 감사에 대한 정보가 포함되어 있습니다.|  
|AUDIT_LOGINCACHE_LOCK|특수 캐시에 대한 액세스를 제어하는 잠금을 기다리는 경우에 발생합니다. 캐시에는 로그인 감사 동작 그룹을 감사하는 데 사용되는 감사에 대한 정보가 포함되어 있습니다.|  
|AUDIT_ON_DEMAND_TARGET_LOCK|감사와 관련된 확장 이벤트 대상의 단일 초기화를 위한 잠금을 기다리는 경우에 발생합니다.|  
|AUDIT_XE_SESSION_MGR|감사와 관련된 확장 이벤트 세션의 시작 및 중지를 동기화하는 데 사용되는 잠금을 기다리는 경우에 발생합니다.|  
|BACKUP|태스크가 백업 처리의 일부로 차단되는 경우에 발생합니다.|  
|BACKUP_OPERATOR|태스크가 테이프 탑재를 대기하는 경우에 발생합니다. 테이프 상태를 보려면 쿼리 [sys.dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md)합니다. 탑재 작업이 보류된 상태가 아니라면 이 대기 유형이 테이프 드라이브의 하드웨어 문제를 나타낼 수 있습니다.|  
|BACKUPBUFFER|백업 태스크가 데이터를 기다리거나 데이터를 저장할 버퍼를 기다리는 경우에 발생합니다. 이 유형은 태스크가 테이프 탑재를 기다리는 경우 외에는 일반적이지 않습니다.|  
|BACKUPIO|백업 태스크가 데이터를 기다리거나 데이터를 저장할 버퍼를 기다리는 경우에 발생합니다. 이 유형은 태스크가 테이프 탑재를 기다리는 경우 외에는 일반적이지 않습니다.|  
|BACKUPTHREAD|태스크가 백업 작업이 완료될 때까지 대기하는 경우에 발생합니다. 대기 시간은 몇 분에서 몇 시간까지 걸릴 수 있습니다. 대기 중인 태스크가 I/O 프로세스에 위치하면 문제가 있는 것이 아닙니다.|  
|BAD_PAGE_PROCESS|백그라운드의 주의 대상 페이지 로거가 5초보다 긴 간격으로 실행되는 것을 방지하려는 경우에 발생합니다. 주의 대상 페이지가 너무 많으면 로거가 자주 실행됩니다.|  
|BROKER_CONNECTION_RECEIVE_TASK|연결 끝점에서 메시지를 받기 위한 액세스를 대기하는 경우에 발생합니다. 끝점에 대한 수신 액세스는 직렬화됩니다.|  
|BROKER_ENDPOINT_STATE_MUTEX|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 연결 끝점의 상태에 액세스하려는 경합이 있는 경우에 발생합니다. 변경 내용의 상태에 대한 액세스는 직렬화됩니다.|  
|BROKER_EVENTHANDLER|태스크가 [!INCLUDE[ssSB](../../includes/sssb-md.md)]의 기본 이벤트 처리기에서 대기하는 경우에 발생합니다. 매우 짧게 발생해야 합니다.|  
|BROKER_INIT|각 활성 데이터베이스에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 초기화하는 경우에 발생합니다. 자주 발생하면 안 됩니다.|  
|BROKER_MASTERSTART|태스크가 [!INCLUDE[ssSB](../../includes/sssb-md.md)]의 기본 이벤트 처리기가 시작될 때까지 대기하는 경우에 발생합니다. 매우 짧게 발생해야 합니다.|  
|BROKER_RECEIVE_WAITFOR|RECEIVE WAITFOR가 대기 중인 경우에 발생합니다. 받을 준비가 된 메시지가 없는 경우에 주로 발생합니다.|  
|BROKER_REGISTERALLENDPOINTS|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 연결 끝점의 초기화 중에 발생합니다. 매우 짧게 발생해야 합니다.|  
|BROKER_SERVICE|대상 서비스와 연결된 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대상 목록이 업데이트되거나 우선 순위가 다시 매겨지는 경우에 발생합니다.|  
|BROKER_SHUTDOWN|계획된 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 종료 시 발생합니다. 가능하면 매우 짧게 발생해야 합니다.|  
|BROKER_TASK_STOP|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 큐 태스크 처리기가 태스크를 종료하려고 하는 경우에 발생합니다. 상태 검사가 직렬화되고 먼저 실행 상태에 있어야 합니다.|  
|BROKER_TO_FLUSH|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 지연 플러셔가 메모리 내 전송 개체를 작업 테이블에 플러시하는 경우에 발생합니다.|  
|BROKER_TRANSMITTER|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 전송기가 작동될 때까지 대기하는 경우에 발생합니다.|  
|BUILTIN_HASHKEY_MUTEX|내부 데이터 구조를 초기화하는 동안 인스턴스 시작 후 발생할 수 있습니다. 데이터 구조가 초기화되면 되풀이되지 않습니다.|  
|CHECK_PRINT_RECORD|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|CHECKPOINT_QUEUE|검사점 태스크가 다음 검사점 요청을 대기하는 동안 발생합니다.|  
|CHKPT|검사점 스레드에 시작할 수 있음을 알리기 위해 서버 시작 시 발생합니다.|  
|CLEAR_DB|데이터베이스를 열거나 닫는 등과 같이 데이터베이스의 상태를 변경하는 작업 중에 발생합니다.|  
|CLR_AUTO_EVENT|태스크가 현재 CLR(공용 언어 런타임) 실행 중이며 특정 자동 이벤트가 시작될 때까지 대기하는 경우에 발생합니다. 긴 대기는 일반적인 것이며 문제가 있는 것은 아닙니다.|  
|CLR_CRST|태스크가 현재 CLR 실행 중이며 현재 다른 작업에서 사용 중인 중요한 섹션을 시작하기 위해 대기하는 경우에 발생합니다.|  
|CLR_JOIN|태스크가 현재 CLR 실행 중이며 다른 작업이 끝날 때까지 대기하는 경우에 발생합니다. 이 대기 상태는 태스크 간에 조인이 있는 경우에 발생합니다.|  
|CLR_MANUAL_EVENT|태스크가 현재 CLR 실행 중이며 특정 수동 이벤트가 시작될 때까지 대기하는 경우에 발생합니다.|  
|CLR_MEMORY_SPY|CLR에서 발생하는 모든 가상 메모리 할당을 기록하는 데 사용되는 데이터 구조에 대한 잠금 획득 대기 중에 발생합니다. 병렬 액세스가 있는 경우 무결성이 유지되도록 데이터 구조가 잠깁니다.|  
|CLR_MONITOR|태스크가 현재 CLR 실행 중이며 모니터 잠금을 획득하려고 대기하는 경우에 발생합니다.|  
|CLR_RWLOCK_READER|태스크가 현재 CLR 실행 중이며 판독기 잠금으로 인해 대기하는 경우에 발생합니다.|  
|CLR_RWLOCK_WRITER|태스크가 현재 CLR 실행 중이며 기록기 잠금으로 인해 대기하는 경우에 발생합니다.|  
|CLR_SEMAPHORE|태스크가 현재 CLR 실행 중이며 세마포를 기다리는 경우에 발생합니다.|  
|CLR_TASK_START|CLR 태스크 시작이 완료될 때까지 대기하는 동안 발생합니다.|  
|CLRHOST_STATE_ACCESS|CLR 호스팅 데이터 구조를 단독으로 사용하려고 대기하는 경우에 발생합니다. 이 대기 유형은 CLR 런타임을 설정 또는 중지하는 동안 발생합니다.|  
|CMEMTHREAD|태스크가 스레드로부터 안전한 메모리 개체를 기다리는 경우에 발생합니다. 여러 태스크가 같은 메모리 개체의 메모리를 할당하려고 하여 경합이 발생할 때 대기 시간이 증가할 수 있습니다.|  
|CXPACKET|쿼리 프로세서 교환 반복기를 동기화하려고 하는 경우에 발생합니다. 이 대기 유형에 대한 경합이 문제가 되면 병렬 처리 수준을 낮출 것을 고려할 수 있습니다.|  
|CXROWSET_SYNC|병렬 범위 검색 중에 발생합니다.|  
|DAC_INIT|관리자 전용 연결이 초기화되는 동안 발생합니다.|  
|DBMIRROR_DBM_EVENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|DBMIRROR_DBM_MUTEX|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|DBMIRROR_EVENTS_QUEUE|데이터베이스 미러링이 이벤트가 처리될 때까지 대기하는 경우에 발생합니다.|  
|DBMIRROR_SEND|태스크가 네트워크 계층의 통신 백로그가 지워져서 메시지를 보낼 수 있을 때까지 대기하는 경우에 발생합니다. 통신 계층의 로드가 많아져 데이터베이스 미러링 데이터 처리량에 영향을 미치기 시작했음을 나타냅니다.|  
|DBMIRROR_WORKER_QUEUE|데이터베이스 미러링 작업자 태스크가 추가 작업을 대기하는 경우를 나타냅니다.|  
|DBMIRRORING_CMD|태스크가 로그 레코드가 디스크로 플러시될 때까지 대기하는 경우에 발생합니다. 이 대기 상태는 오랜 시간 동안 유지됩니다.|  
|DEADLOCK_ENUM_MUTEX|교착 상태 모니터와 sys.dm_os_waiting_tasks가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 동시에 여러 개의 교착 상태 검색을 실행하고 있지 않도록 하려고 하는 경우에 발생합니다.|  
|DEADLOCK_TASK_SEARCH|이 리소스의 대기 시간이 길면 서버가 sys.dm_os_waiting_tasks 위에서 쿼리를 실행하고 있으며 이러한 쿼리가 교착 상태 모니터의 교착 상태 검색을 차단하고 있음을 나타냅니다. 이 대기 유형은 교착 상태 모니터에만 사용됩니다. sys.dm_os_waiting_tasks 위의 쿼리는 DEADLOCK_ENUM_MUTEX를 사용합니다.|  
|DEBUG|내부 동기화에 대한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 CLR 디버깅 작업 중에 발생합니다.|  
|DISABLE_VERSIONING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 가장 오래된 활성 트랜잭션의 타임스탬프가 상태 변경이 시작될 때의 타임스탬프보다 나중인지 확인하기 위해 버전 트랜잭션 관리자를 폴링하는 경우에 발생합니다. 이 경우 ALTER DATABASE 문이 실행되기 전에 시작된 모든 스냅숏 트랜잭션은 완료되었습니다. 이 대기 상태는 ALTER DATABASE 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 버전 관리를 해제하는 경우에 사용됩니다.|  
|DISKIO_SUSPEND|외부 백업이 활성 상태일 때 태스크가 파일에 액세스하려고 대기하는 경우에 발생합니다. 대기 중인 모든 사용자 프로세스에 대해 보고됩니다. 사용자 프로세스당 값이 5보다 크면 외부 백업을 완료하는 데 걸리는 시간이 너무 긴 것일 수 있습니다.|  
|DISPATCHER_QUEUE_SEMAPHORE|디스패처 풀의 스레드가 처리할 추가 작업을 기다리는 경우에 발생합니다. 이 대기 유형의 대기 시간은 디스패처가 유휴 상태일 때 증가됩니다.|  
|DLL_LOADING_MUTEX|XML 파서 DLL이 로드될 때까지 대기하는 동안 한 번 발생합니다.|  
|DROPTEMP|이전 시도가 실패한 경우 임시 개체 삭제를 다시 시도하기 전에 발생합니다. 삭제 시도가 실패할 때마다 대기 시간이 기하급수적으로 증가합니다.|  
|DTC|태스크가 상태 전환 관리에 사용되는 이벤트를 기다리는 경우에 발생합니다. 이 상태는 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서 MS DTC([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Transaction Coordinator) 서비스가 사용할 수 없게 되었다는 알림을 받은 후 MS DTC 트랜잭션 복구가 발생할 때 제어됩니다.<br /><br /> 또한 이 상태는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 MS DTC 트랜잭션 커밋이 시작되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 MS DTC 커밋이 완료되기를 기다릴 때 대기 태스크를 정의합니다.|  
|DTC_ABORT_REQUEST|MS DTC 작업자 세션이 MS DTC 트랜잭션의 소유권을 획득하려고 대기하는 경우에 MS DTC 작업자 세션에서 발생합니다. MS DTC가 트랜잭션의 소유권을 획득한 후에는 세션이 트랜잭션을 롤백할 수 있습니다. 일반적으로 세션은 트랜잭션을 사용하고 있는 다른 세션을 기다립니다.|  
|DTC_RESOLVE|복구 태스크가 트랜잭션의 결과물을 쿼리할 수 있도록 데이터베이스 간 트랜잭션에서 master 데이터베이스를 대기하는 경우에 발생합니다.|  
|DTC_STATE|태스크가 내부 MS DTC 전역 상태 개체의 변경을 방지하는 이벤트를 기다리는 경우에 발생합니다. 이 상태는 매우 짧은 시간 동안 유지되어야 합니다.|  
|DTC_TMDOWN_REQUEST|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 MS DTC 서비스가 사용할 수 없게 되었다는 알림을 받는 경우에 MS DTC 작업자 세션에서 발생합니다. 먼저 작업자는 MS DTC 복구 프로세스가 시작될 때까지 기다렸다가 작업자가 작업하고 있는 분산 트랜잭션의 결과물을 획득하기 위해 대기합니다. 이것은 MS DTC 서비스와의 연결이 다시 설정될 때까지 계속될 수 있습니다.|  
|DTC_WAITFOR_OUTCOME|복구 태스크가 MS DTC가 활성화되어 준비된 트랜잭션을 해결할 수 있을 때까지 대기하는 경우에 발생합니다.|  
|DUMP_LOG_COORDINATOR|주 태스크가 하위 작업이 데이터를 생성할 때까지 대기하는 경우에 발생합니다. 일반적으로 이 상태는 발생하지 않습니다. 대기 시간이 길면 예상하지 못했던 차단이 발생한 것일 수 있으므로 하위 태스크를 조사해야 합니다.|  
|DUMPTRIGGER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|EC|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|EE_PMOLOCK|문 실행 중 특정 유형의 메모리 할당을 동기화하는 경우에 발생합니다.|  
|EE_SPECPROC_MAP_INIT|내부 프로시저 해시 테이블 생성을 동기화하는 경우에 발생합니다. 이 대기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작된 후 해시 테이블에 처음 액세스하는 경우에만 발생합니다.|  
|ENABLE_VERSIONING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스를 스냅숏 격리 허용 상태로 전환할 준비가 되었다고 선언하기 전에 이 데이터베이스의 모든 업데이트 트랜잭션이 완료될 때까지 대기하는 경우에 발생합니다. 이 상태는 ALTER DATABASE 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 스냅숏 격리를 설정하는 경우에 사용됩니다.|  
|ERROR_REPORTING_MANAGER|여러 개의 동시 오류 로그 초기화를 동기화하는 경우에 발생합니다.|  
|EXCHANGE|병렬 쿼리 중 쿼리 프로세서 교환 반복기에서 동기화 중에 발생합니다.|  
|EXECSYNC|병렬 쿼리 중 쿼리 프로세서 교환 반복기와 관련되지 않은 영역에서 동기화 중에 발생합니다. 이러한 영역의 예에는 비트맵, LOB(Large Binary Object) 및 스풀 반복기가 있습니다. LOB는 이 대기 상태를 자주 사용할 수 있습니다.|  
|EXECUTION_PIPE_EVENT_INTERNAL|연결 컨텍스트를 통해 전송되는 일괄 처리 실행의 제작자 부분과 소비자 부분 동기화 중에 발생합니다.|  
|FAILPOINT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|FCB_REPLICA_READ|스냅숏이나 DBCC에서 만든 임시 스냅숏 스파스 파일의 읽기가 동기화되는 경우에 발생합니다.|  
|FCB_REPLICA_WRITE|스냅숏이나 DBCC에서 만든 임시 스냅숏 스파스 파일에 대한 페이지 밀어넣기 또는 끌어오기가 동기화되는 경우에 발생합니다.|  
|FS_FC_RWLOCK|다음 중 하나를 수행하기 위해 FILESTREAM 가비지 수집기가 대기하는 경우에 발생합니다.<br /><br /> 백업 및 복원에 사용되는 가비지 수집 사용 안 함<br /><br /> FILESTREAM 가비지 수집기의 한 주기 실행|  
|FS_GARBAGE_COLLECTOR_SHUTDOWN|FILESTREAM 가비지 수집기가 정리 태스크 완료를 기다리는 경우에 발생합니다.|  
|FS_HEADER_RWLOCK|FILESTREAM 헤더 파일(Filestream.hdr)에서 내용을 읽거나 업데이트하기 위해 FILESTREAM 데이터 컨테이너의 FILESTREAM 헤더에 대한 액세스를 얻으려고 대기하는 경우에 발생합니다.|  
|FS_LOGTRUNC_RWLOCK|다음 중 하나를 수행하기 위해 FILESTREAM 로그 잘림에 대한 액세스를 얻으려고 대기하는 경우에 발생합니다.<br /><br /> 백업 및 복원에 사용되는 FSLOG(FILESTREAM 로그) 잘림 일시적으로 사용 안 함<br /><br /> FSLOG 잘림의 한 주기 실행|  
|FSA_FORCE_OWN_XACT|FILESTREAM 파일 I/O 작업을 관련 트랜잭션에 바인딩해야 하지만 현재 다른 세션에서 해당 트랜잭션을 소유하고 있는 경우에 발생합니다.|  
|FSAGENT|FILESTREAM 파일 I/O 작업이 다른 파일 I/O 작업에 사용되는 FILESTREAM 에이전트 리소스를 기다리는 경우에 발생합니다.|  
|FSTR_CONFIG_MUTEX|다른 FILESTREAM 기능 다시 구성 작업이 완료될 때까지 대기하는 경우에 발생합니다.|  
|FSTR_CONFIG_RWLOCK|FILESTREAM 구성 매개 변수에 대한 액세스 직렬화를 대기하는 경우에 발생합니다.|  
|FT_METADATA_MUTEX|정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.|  
|FT_RESTART_CRAWL|임시 오류로부터 복구하기 위해 마지막으로 알려진 양호 지점부터 전체 텍스트 탐색을 다시 시작해야 하는 경우에 발생합니다. 이 대기를 사용하면 해당 채우기에서 현재 작동 중인 작업자 태스크가 현재 단계를 완료하거나 종료할 수 있습니다.|  
|FULLTEXT GATHERER|전체 텍스트 작업을 동기화하는 경우에 발생합니다.|  
|GUARDIAN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|HTTP_ENUMERATION|시스템 시작 시에 HTTP를 시작할 HTTP 끝점을 열거하기 위해 발생합니다.|  
|HTTP_START|연결이 HTTP 초기화가 완료될 때까지 대기하는 경우에 발생합니다.|  
|IMPPROV_IOWAIT|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 대량 로드 I/O가 완료될 때까지 대기하는 경우에 발생합니다.|  
|INTERNAL_TESTING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|IO_AUDIT_MUTEX|추적 이벤트 버퍼 동기화 중에 발생합니다.|  
|IO_COMPLETION|I/O 작업이 완료될 때까지 대기하는 동안 발생합니다. 이 대기 유형은 일반적으로 비데이터 페이지 I/O를 나타냅니다. 데이터 페이지 I/O 완료 대기는 PAGEIOLATCH_* 대기로 표시됩니다.|  
|IO_QUEUE_LIMIT|[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 비동기 IO 큐에 보류 중인 IO가 너무 많은 경우에 발생합니다. 보류 중인 IO 수가 임계값 아래로 떨어질 때까지 다른 IO를 실행하려는 작업은 이 대기 유형에서 차단됩니다. 임계값은 데이터베이스에 할당된 DTU에 비례합니다.|  
|IO_RETRY|리소스 부족으로 인해 읽기 또는 쓰기와 같은 디스크 I/O 작업이 실패하여 다시 시도되는 경우에 발생합니다.|  
|IOAFF_RANGE_QUEUE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|KSOURCE_WAKEUP|서비스 제어 관리자의 요청을 대기하는 동안 서비스 제어 태스크에 사용됩니다. 긴 대기가 예상되며 문제가 있는 것은 아닙니다.|  
|KTM_ENLISTMENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|KTM_RECOVERY_MANAGER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|KTM_RECOVERY_RESOLUTION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|LATCH_DT|DT(삭제) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. sys.dm_os_latch_stats에서 LATCH_* 대기 목록을 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.|  
|LATCH_EX|EX(배타) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. sys.dm_os_latch_stats에서 LATCH_* 대기 목록을 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.|  
|LATCH_KP|KP(유지) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. sys.dm_os_latch_stats에서 LATCH_* 대기 목록을 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.|  
|LATCH_NL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|LATCH_SH|SH(공유) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. sys.dm_os_latch_stats에서 LATCH_* 대기 목록을 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.|  
|LATCH_UP|UP(업데이트) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. sys.dm_os_latch_stats에서 LATCH_* 대기 목록을 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.|  
|LAZYWRITER_SLEEP|지연 기록기 태스크가 일시 중지되는 경우에 발생합니다. 대기 중인 백그라운드 태스크에서 사용한 시간을 측정한 것입니다. 사용자 대기를 찾을 때 이 상태는 고려하지 마세요.|  
|LCK_M_BU|태스크가 대량 업데이트(BU) 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_IS|태스크가 내재된 공유(IS) 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_IU|태스크가 의도 업데이트(IU) 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_IX|태스크가 의도 배타(IX) 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_RIn_NL|태스크가 현재 키 값의 NULL 잠금 및 현재 키와 이전 키 간의 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 키의 NULL 잠금은 즉시 해제 잠금입니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_RIn_S|태스크가 현재 키 값의 공유 잠금 및 현재 키와 이전 키 간의 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_RIn_U|태스크가 현재 키 값의 업데이트 잠금 및 현재 키와 이전 키 간의 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_RIn_X|태스크가 현재 키 값의 배타 잠금 및 현재 키와 이전 키 간의 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_RS_S|태스크가 현재 키 값의 공유 잠금 및 현재 키와 이전 키 간의 공유 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_RS_U|태스크가 현재 키 값의 업데이트 잠금 및 현재 키와 이전 키 간의 업데이트 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_RX_S|태스크가 현재 키 값의 공유 잠금 및 현재 키와 이전 키 간의 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_RX_U|태스크가 현재 키 값의 업데이트 잠금 및 현재 키와 이전 키 간의 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_RX_X|태스크가 현재 키 값의 배타 잠금 및 현재 키와 이전 키 간의 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_S|태스크가 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_SCH_M|태스크가 스키마 수정 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_SCH_S|태스크가 스키마 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_SIU|태스크가 의도 업데이트 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_SIX|태스크가 의도 배타 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_U|태스크가 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_UIX|태스크가 의도 배타 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LCK_M_X|태스크가 배타 잠금을 획득하려고 대기하는 경우에 발생합니다. 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.|  
|LOG_RATE_GOVERNOR|DB에서 견적을 로그에 작성할 때까지 기다릴 때 발생합니다.|  
|LOGBUFFER|태스크가 로그 버퍼의 공간에 로그 레코드가 저장될 때까지 대기하는 경우에 발생합니다. 값이 계속 높게 나타나면 로그 장치가 서버에서 생성하는 로그의 양을 따라갈 수 없는 것일 수 있습니다.|  
|LOGGENERATION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|LOGMGR|데이터베이스를 닫는 동안 태스크가 로그 종료 전에 처리 중인 로그 I/O가 완료될 때까지 대기하는 경우에 발생합니다.|  
|LOGMGR_FLUSH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|LOGMGR_QUEUE|로그 쓰기 태스크가 작업 요청을 대기하는 동안 발생합니다.|  
|LOGMGR_RESERVE_APPEND|태스크가 로그 잘림으로 인해 로그 공간이 확보되어 작업이 새 로그 레코드를 쓸 수 있는지 확인하려고 대기하는 경우에 발생합니다. 이 대기를 줄이려면 영향을 받는 데이터베이스의 로그 파일 크기를 늘리세요.|  
|LOWFAIL_MEMMGR_QUEUE|메모리를 사용할 수 있을 때까지 대기하는 동안 발생합니다.|  
|MSQL_DQ|분산 쿼리 작업이 완료될 때까지 태스크가 대기하는 경우에 발생합니다. 발생 가능한 MARS(Multiple Active Result Set) 응용 프로그램 교착 상태를 감지하는 데 사용됩니다. 대기는 분산 쿼리 호출이 완료될 때 끝납니다.|  
|MSQL_XACT_MGR_MUTEX|태스크가 세션 트랜잭션 관리자의 소유권을 획득하여 세션 수준 트랜잭션 작업을 수행하려고 대기하는 경우에 발생합니다.|  
|MSQL_XACT_MUTEX|트랜잭션 사용 동기화 중에 발생합니다. 요청에서 트랜잭션을 사용하려면 먼저 뮤텍스를 획득해야 합니다.|  
|MSQL_XP|태스크가 확장 저장 프로시저가 끝날 때까지 대기하는 경우에 발생합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 대기 상태를 사용하여 잠재적 MARS 응용 프로그램 교착 상태를 감지합니다. 대기는 확장 저장 프로시저 호출이 끝날 때 중지됩니다.|  
|MSSEARCH|전체 텍스트 검색 호출 중에 발생합니다. 이 대기는 전체 텍스트 작업이 완료될 때 끝나며 경합이 아니라 전체 텍스트 작업 기간을 나타냅니다.|  
|NET_WAITFOR_PACKET|네트워크 읽기 중 연결이 네트워크 패킷을 대기하는 경우에 발생합니다.|  
|OLEDB|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider를 호출할 때 발생합니다. 이 대기 유형은 동기화에 사용되지 않습니다. 대신 OLE DB Provider에 대한 호출 기간을 나타냅니다.|  
|ONDEMAND_TASK_QUEUE|백그라운드 태스크가 우선 순위가 높은 시스템 작업 요청을 대기하는 동안 발생합니다. 대기 시간이 길면 우선 순위가 높은 처리할 요청이 없는 것이므로 염려할 필요가 없습니다.|  
|PAGEIOLATCH_DT|태스크가 I/O 요청에 있는 버퍼를 래치에서 기다리는 경우에 발생합니다. 래치 요청이 삭제 모드에 있습니다. 대기 수가 많으면 디스크 하위 시스템에 문제가 있을 수 있습니다.|  
|PAGEIOLATCH_EX|태스크가 I/O 요청에 있는 버퍼를 래치에서 기다리는 경우에 발생합니다. 래치 요청이 배타 모드에 있습니다. 대기 수가 많으면 디스크 하위 시스템에 문제가 있을 수 있습니다.|  
|PAGEIOLATCH_KP|태스크가 I/O 요청에 있는 버퍼를 래치에서 기다리는 경우에 발생합니다. 래치 요청이 유지 모드에 있습니다. 대기 수가 많으면 디스크 하위 시스템에 문제가 있을 수 있습니다.|  
|PAGEIOLATCH_NL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PAGEIOLATCH_SH|태스크가 I/O 요청에 있는 버퍼를 래치에서 기다리는 경우에 발생합니다. 래치 요청이 공유 모드에 있습니다. 대기 수가 많으면 디스크 하위 시스템에 문제가 있을 수 있습니다.|  
|PAGEIOLATCH_UP|태스크가 I/O 요청에 있는 버퍼를 래치에서 기다리는 경우에 발생합니다. 래치 요청이 업데이트 모드에 있습니다. 대기 수가 많으면 디스크 하위 시스템에 문제가 있을 수 있습니다.|  
|PAGELATCH_DT|태스크가 I/O 요청에 없는 버퍼를 래치에서 대기하는 경우에 발생합니다. 래치 요청이 삭제 모드에 있습니다.|  
|PAGELATCH_EX|태스크가 I/O 요청에 없는 버퍼를 래치에서 대기하는 경우에 발생합니다. 래치 요청이 배타 모드에 있습니다.|  
|PAGELATCH_KP|태스크가 I/O 요청에 없는 버퍼를 래치에서 대기하는 경우에 발생합니다. 래치 요청이 유지 모드에 있습니다.|  
|PAGELATCH_NL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PAGELATCH_SH|태스크가 I/O 요청에 없는 버퍼를 래치에서 대기하는 경우에 발생합니다. 래치 요청이 공유 모드에 있습니다.|  
|PAGELATCH_UP|태스크가 I/O 요청에 없는 버퍼를 래치에서 대기하는 경우에 발생합니다. 래치 요청이 업데이트 모드에 있습니다.|  
|PARALLEL_BACKUP_QUEUE|RESTORE HEADERONLY, RESTORE FILELISTONLY 또는 RESTORE LABELONLY에서 직렬화 출력이 생성되는 경우에 발생합니다.|  
|PREEMPTIVE_ABR|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG|Windows 이벤트 로그에 감사 이벤트를 기록하기 위해 SQLOS([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 운영 체제) 스케줄러가 우선 모드로 전환된 경우에 발생합니다.|  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG|Windows 보안 로그에 감사 이벤트를 기록하기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.|  
|PREEMPTIVE_CLOSEBACKUPMEDIA|백업 미디어를 닫기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.|  
|PREEMPTIVE_CLOSEBACKUPTAPE|테이프 백업 장치를 닫기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.|  
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE|가상 백업 장치를 닫기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.|  
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL|Windows 장애 조치(Failover) 클러스터 작업을 수행하기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.|  
|PREEMPTIVE_COM_COCREATEINSTANCE|COM 개체를 만들기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.|  
|PREEMPTIVE_HADR_LEASE_MECHANISM|Always On 가용성 그룹 임대 관리자 CSS 진단에 대 한 일정입니다.|  
|PREEMPTIVE_SOSTESTING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PREEMPTIVE_STRESSDRIVER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PREEMPTIVE_TESTING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PREEMPTIVE_XETESTING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PRINT_ROLLBACK_PROGRESS|ALTER DATABASE termination 절을 사용하여 전환된 데이터베이스에서 사용자 프로세스가 끝나기를 기다리는 데 사용됩니다. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.|  
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC|백그라운드 태스크가 폴링을 통해 Windows Server 장애 조치(Failover) 클러스터링 알림을 받는 백그라운드 태스크가 종료될 때까지 기다리는 경우에 발생합니다.  내부적으로만 사용됩니다.|  
|PWAIT_HADR_CLUSTER_INTEGRATION|추가, 바꾸기 및/또는 제거 작업이 Alwayson 내부 목록 (예: 네트워크, 네트워크 주소 또는 가용성 그룹 수신기의 목록)에 대 한 쓰기 잠금을 가져올 기다리고 있습니다.  내부적으로만 사용됩니다.|  
|PWAIT_HADR_OFFLINE_COMPLETED|오프 라인으로 Windows Server 장애 조치 클러스터링 개체를 삭제 하기 전에 대상 가용성 그룹에 대 한 Always On 가용성 그룹 삭제 작업이 대기 중입니다.|  
|PWAIT_HADR_ONLINE_COMPLETED|Always On 만들거나 가용성 그룹 장애 조치 작업이 대상 가용성 그룹이 온라인 상태가 될 때까지 기다리고 있습니다.|  
|PWAIT_HADR_POST_ONLINE_COMPLETED|Always On 가용성 그룹 삭제 작업이 이전 명령의 일부로 예약 된 백그라운드 태스크가 종료 될 때까지 기다리고 있습니다. 예를 들어 가용성 데이터베이스를 주 역할로 전환 중인 백그라운드 작업이 있을 수 있습니다. 경합 상태를 방지하기 위해 DROP AVAILABILITY GROUP DDL이 이 백그라운드 태스크가 종료될 때까지 기다려야 합니다.|  
|PWAIT_HADR_WORKITEM_COMPLETED|비동기 작업 태스크가 완료될 때까지 기다리는 스레드에 의한 내부 대기입니다. 이는 예상되는 대기이며 CSS용으로 사용됩니다.|  
|PWAIT_MD_LOGIN_STATS|로그인 상태에서 메타데이터의 내부 동기화 중에 발생합니다.|  
|PWAIT_MD_RELATION_CACHE|테이블 또는 인덱스에서 메타데이터의 내부 동기화 중에 발생합니다.|  
|PWAIT_MD_SERVER_CACHE|연결된 서버에서 메타데이터의 내부 동기화 중에 발생합니다.|  
|PWAIT_MD_UPGRADE_CONFIG|업그레이드하는 서버 차원 구성의 내부 동기화 중에 발생합니다.|  
|PWAIT_METADATA_LAZYCACHE_RWLOCk|테이블의 반복 인덱스 또는 통계와 함께 메타데이터 캐시의 내부 동기화 중에 발생합니다.|  
|QPJOB_KILL|업데이트가 실행되기 시작할 때 KILL 호출을 통해 비동기 자동 통계 업데이트가 취소되었음을 나타냅니다. 종료하는 스레드는 일시 중지 상태로, KILL 명령을 수신하기 시작할 때까지 대기합니다. 1초보다 작은 값이 좋습니다.|  
|QPJOB_WAITFOR_ABORT|실행되고 있을 때 KILL 호출을 통해 비동기 자동 통계 업데이트가 취소되었음을 나타냅니다. 업데이트는 이제 완료되었지만 종료하는 스레드 메시지 조정이 완료될 때까지 일시 중지됩니다. 이 상태는 일반적이지만 거의 발생하지 않으며 매우 짧아야 합니다. 1초보다 작은 값이 좋습니다.|  
|QRY_MEM_GRANT_INFO_MUTEX|쿼리 실행 메모리 관리 기능이 정적 권한 부여 정보 목록에 대한 액세스를 제어하려고 하는 경우에 발생합니다. 이 상태는 현재 권한이 부여된 메모리 요청과 대기 중인 메모리 요청에 대한 정보를 나열합니다. 이 상태는 단순 액세스 제어 상태입니다. 이 상태에 대한 긴 대기가 있으면 안 됩니다. 이 뮤텍스가 해제되지 않으면 새로운 메모리 사용 쿼리의 응답이 모두 중지됩니다.|  
|QUERY_ERRHDL_SERVICE_DONE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN|오프라인 인덱스 빌드 생성이 병렬로 실행되고 정렬되는 여러 작업자 스레드가 정렬 파일에 대한 액세스를 동기화하는 특정 경우에 발생합니다.|  
|QUERY_NOTIFICATION_MGR_MUTEX|쿼리 알림 관리자에서 가비지 수집 큐 동기화 중에 발생합니다.|  
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX|쿼리 알림의 트랜잭션 상태 동기화 중에 발생합니다.|  
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX|쿼리 알림 관리자의 내부 동기화 중에 발생합니다.|  
|QUERY_NOTIFICATION_UNITTEST_MUTEX|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|QUERY_OPTIMIZER_PRINT_MUTEX|쿼리 최적화 프로그램의 진단 출력 생성 동기화 중에 발생합니다. 이 대기 유형은 진단 설정이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 기술 지원 서비스의 지시대로 설정된 경우에만 발생합니다.|  
|QUERY_TRACEOUT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|QUERY_WAIT_ERRHDL_SERVICE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|RECOVER_CHANGEDB|웜 대기 데이터베이스의 데이터베이스 상태 동기화 중에 발생합니다.|  
|REPL_CACHE_ACCESS|복제 아티클 캐시 동기화 중에 발생합니다. 이 대기 중에는 복제 로그 판독기가 정지되고 게시된 테이블에 대한 DDL(데이터 정의 언어) 문이 차단됩니다.|  
|REPL_SCHEMA_ACCESS|복제 스키마 버전 정보 동기화 중에 발생합니다. 복제된 개체에 대해 DDL 문을 실행하고 로그 판독기가 DDL 발생을 기반으로 버전이 지정된 스키마를 작성하거나 사용할 때 이 상태가 됩니다.|  
|REPLICA_WRITES|태스크가 데이터베이스 스냅숏 또는 DBCC 복제본에 대한 페이지 쓰기가 완료될 때까지 대기하는 동안 발생합니다.|  
|REQUEST_DISPENSER_PAUSE|스냅숏 백업을 위해 파일 I/O를 고정할 수 있도록 태스크가 처리 중인 모든 I/O가 완료될 때까지 대기하는 경우에 발생합니다.|  
|REQUEST_FOR_DEADLOCK_SEARCH|교착 상태 모니터가 다음 교착 상태 검색을 시작하기 위해 대기하는 동안 발생합니다. 이 대기는 교착 상태 감지 사이에 발생하며 이 리소스에 대한 총 대기 시간이 길어도 문제가 있는 것은 아닙니다.|  
|RESMGR_THROTTLED|새 쿼리가 GROUP_MAX_REQUESTS 설정에 따라 들어오고 정체되는 경우 발생합니다.|  
|RESOURCE_QUEUE|다양한 내부 리소스 큐 동기화 중에 발생합니다.|  
|RESOURCE_SEMAPHORE|다른 동시 쿼리로 인해 쿼리 메모리 요청을 즉시 허용할 수 없는 경우에 발생합니다. 대기 수가 많고 대기 시간이 길면 동시 쿼리 수 또는 메모리 요청 양이 과도하게 많은 것입니다.|  
|RESOURCE_SEMAPHORE_MUTEX|쿼리가 스레드 예약 요청이 수행될 때까지 대기하는 동안 발생합니다. 또한 쿼리 컴파일 및 메모리 부여 요청을 동기화하는 경우에 발생합니다.|  
|RESOURCE_SEMAPHORE_QUERY_COMPILE|동시 쿼리 컴파일 수가 조절 한계에 도달한 경우에 발생합니다. 대기 수가 많고 대기 시간이 길면 컴파일, 다시 컴파일 또는 캐싱할 수 없는 계획 수가 과도하게 많은 것입니다.|  
|RESOURCE_SEMAPHORE_SMALL_QUERY|다른 동시 쿼리로 인해 작은 쿼리의 메모리 요청을 즉시 허용할 수 없는 경우에 발생합니다. 서버는 몇 초 내에 요청된 메모리를 부여하지 못하면 주 쿼리 메모리 풀로 요청을 전송하기 때문에 대기 시간은 몇 초를 넘지 않아야 합니다. 대기 수가 많으면 대기 중인 쿼리가 주 메모리 풀을 차단하는 동안 작은 동시 쿼리 수가 과도하게 많은 것입니다.|  
|SE_REPL_CATCHUP_THROTTLE|트랜잭션이 보조 데이터베이스 중 하나가 진행되도록 기다리는 경우에 발생합니다.|  
|SE_REPL_COMMIT_ACK|트랜잭션이 보조 복제본에서 쿼럼 커밋 승인을 기다리는 경우에 발생합니다.|  
|SE_REPL_COMMIT_TURN|트랜잭션이 쿼럼 커밋 승인을 받은 후 커밋을 기다리는 경우에 발생합니다.|  
|SE_REPL_ROLLBACK_ACK|트랜잭션이 보조 복제본에서 쿼럼 롤백 승인을 기다리는 경우에 발생합니다.|  
|SE_REPL_SLOW_SECONDARY_THROTTLE|스레드가 보조 복제본 중 하나에 대해 기다리는 경우에 발생합니다.|  
|SEC_DROP_TEMP_KEY|임시 보안 키 삭제 시도가 실패한 후 다시 시도하기 전에 발생합니다.|  
|SECURITY_MUTEX|EKM(확장 가능 키 관리) 암호화 공급자의 전역 목록 및 EKM 세션의 세션 범위 목록에 대한 액세스를 제어하는 뮤텍스를 기다리는 경우에 발생합니다.|  
|SEQUENTIAL_GUID|새 순차적 GUID를 가져오는 동안 발생합니다.|  
|SERVER_IDLE_CHECK|리소스 모니터가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 유휴 상태나 켜는 중 상태로 선언하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 유휴 상태 동기화 중에 발생합니다.|  
|SHUTDOWN|종료 문이 활성 연결이 종료될 때까지 대기하는 동안 발생합니다.|  
|SLEEP_BPOOL_FLUSH|검사점이 디스크 하위 시스템의 폭주를 방지하기 위해 새 I/O의 실행을 조절하는 경우에 발생합니다.|  
|SLEEP_DBSTARTUP|모든 데이터베이스가 복구될 때까지 대기하는 동안 데이터베이스 시작 중에 발생합니다.|  
|SLEEP_DCOMSTARTUP|DCOM 초기화가 완료될 때까지 대기하는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 시작 중에 많아야 한 번 발생합니다.|  
|SLEEP_MSDBSTARTUP|SQL 추적이 msdb 데이터베이스 시작이 완료될 때까지 대기하는 경우에 발생합니다.|  
|SLEEP_SYSTEMTASK|tempdb 시작이 완료될 때까지 대기하는 동안 백그라운드 태스크 시작 중에 발생합니다.|  
|SLEEP_TASK|일반 이벤트가 발생할 때까지 대기하는 동안 태스크가 중지되는 경우에 발생합니다.|  
|SLEEP_TEMPDBSTARTUP|태스크가 tempdb 시작이 완료될 때까지 대기하는 동안 발생합니다.|  
|SNI_CRITICAL_SECTION|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네트워킹 구성 요소의 내부 동기화 중에 발생합니다.|  
|SNI_HTTP_WAITFOR_0_DISCON|처리 중인 HTTP 연결이 종료될 때까지 대기하는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 종료 중에 발생합니다.|  
|SNI_LISTENER_ACCESS|NUMA(비균일 메모리 액세스) 노드의 상태 변경 업데이트 작업을 대기하는 동안 발생합니다. 상태 변경에 대한 액세스는 직렬화됩니다.|  
|SNI_TASK_COMPLETION|NUMA 노드 상태 변경 동안 모든 태스크가 완료될 때까지 대기하는 중에 발생합니다.|  
|SOAP_READ|HTTP 네트워크 읽기가 완료될 때까지 대기하는 동안 발생합니다.|  
|SOAP_WRITE|HTTP 네트워크 쓰기가 완료될 때까지 대기하는 동안 발생합니다.|  
|SOS_CALLBACK_REMOVAL|콜백을 제거하기 위해 콜백 목록에 대한 동기화를 수행하는 동안 발생합니다. 서버 초기화가 완료된 후에는 이 카운터가 변경되지 않습니다.|  
|SOS_DISPATCHER_MUTEX|디스패처 풀의 내부 동기화 중에 발생합니다. 풀이 조정되는 경우도 포함됩니다.|  
|SOS_LOCALALLOCATORLIST|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 관리자의 내부 동기화 중에 발생합니다.|  
|SOS_MEMORY_USAGE_ADJUSTMENT|메모리 사용량이 풀 사이에서 조절될 경우 발생합니다.|  
|SOS_OBJECT_STORE_DESTROY_MUTEX|풀에서 개체를 삭제하는 경우 메모리 풀의 내부 동기화 중에 발생합니다.|  
|SOS_PROCESS_AFFINITY_MUTEX|프로세스 선호도 설정에 대한 액세스 동기화 중에 발생합니다.|  
|SOS_RESERVEDMEMBLOCKLIST|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 관리자의 내부 동기화 중에 발생합니다.|  
|SOS_SCHEDULER_YIELD|다른 작업이 실행될 수 있도록 태스크가 자발적으로 스케줄러를 양보하는 경우에 발생합니다. 이 대기 중에 태스크는 해당 퀀텀이 갱신될 때까지 대기합니다.|  
|SOS_SMALL_PAGE_ALLOC|일부 메모리 개체에 의해 관리되는 메모리의 할당 및 해제 중에 발생합니다.|  
|SOS_STACKSTORE_INIT_MUTEX|내부 저장소 초기화 동기화 중에 발생합니다.|  
|SOS_SYNC_TASK_ENQUEUE_EVENT|태스크가 동기 방식으로 시작되는 경우에 발생합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 태스크는 대부분 비동기 방식으로 시작되므로 작업 요청이 작업 큐에 배치된 후 제어가 즉시 시작으로 돌아갑니다.|  
|SOS_VIRTUALMEMORY_LOW|메모리 할당이 리소스 관리자가 가상 메모리를 해제할 때까지 대기하는 경우에 발생합니다.|  
|SOSHOST_EVENT|CLR과 같은 호스팅된 구성 요소가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트 동기화 개체를 대기하는 경우에 발생합니다.|  
|SOSHOST_INTERNAL|CLR과 같은 호스팅된 구성 요소에 사용되는 메모리 관리자 콜백 동기화 중에 발생합니다.|  
|SOSHOST_MUTEX|CLR과 같은 호스팅된 구성 요소가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 뮤텍스 동기화 개체를 대기하는 경우에 발생합니다.|  
|SOSHOST_RWLOCK|CLR과 같은 호스팅된 구성 요소가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 읽기/쓰기 동기화 개체를 대기하는 경우에 발생합니다.|  
|SOSHOST_SEMAPHORE|CLR과 같은 호스팅된 구성 요소가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 세마포 동기화 개체를 대기하는 경우에 발생합니다.|  
|SOSHOST_SLEEP|일반 이벤트가 발생할 때까지 대기하는 동안 호스팅된 태스크가 중지되는 경우에 발생합니다. 호스팅된 태스크는 CLR과 같은 호스팅된 구성 요소에 사용됩니다.|  
|SOSHOST_TRACELOCK|추적 스트림에 대한 액세스 동기화 중에 발생합니다.|  
|SOSHOST_WAITFORDONE|CLR과 같은 호스팅된 구성 요소가 태스크가 완료될 때까지 대기하는 경우에 발생합니다.|  
|SQLCLR_APPDOMAIN|CLR이 응용 프로그램 도메인 시작이 완료될 때까지 대기하는 동안 발생합니다.|  
|SQLCLR_ASSEMBLY|appdomain의 로드된 어셈블리 목록에 대한 액세스를 대기하는 동안 발생합니다.|  
|SQLCLR_DEADLOCK_DETECTION|CLR이 교착 상태 감지가 완료될 때까지 대기하는 동안 발생합니다.|  
|SQLCLR_QUANTUM_PUNISHMENT|CLR 태스크가 실행 퀀텀을 초과하여 조절되는 경우에 발생합니다. 이러한 조절은 리소스를 많이 사용하는 이 태스크가 다른 작업에 미치는 영향을 줄이기 위해 수행됩니다.|  
|SQLSORT_NORMMUTEX|내부 정렬 구조를 초기화하는 동안 내부 동기화 중에 발생합니다.|  
|SQLSORT_SORTMUTEX|내부 정렬 구조를 초기화하는 동안 내부 동기화 중에 발생합니다.|  
|SQLTRACE_BUFFER_FLUSH|태스크가 백그라운드 작업이 4초마다 추적 버퍼를 디스크로 플러시할 때까지 대기하는 경우에 발생합니다.|  
|SQLTRACE_LOCK|파일 추적에서 추적 버퍼 동기화 중에 발생합니다.|  
|SQLTRACE_SHUTDOWN|추적 종료가 처리 중인 추적 이벤트가 완료될 때까지 대기하는 동안 발생합니다.|  
|SQLTRACE_WAIT_ENTRIES|SQL 추적 이벤트 큐가 패킷이 큐에 도착할 때까지 대기하는 동안 발생합니다.|  
|SRVPROC_SHUTDOWN|종료 프로세스가 올바르게 종료하기 위해 내부 리소스가 해제될 때까지 대기하는 동안 발생합니다.|  
|TEMPOBJ|임시 개체 삭제가 동기화되는 경우에 발생합니다. 이 대기는 드물게 발생하며 태스크가 temp 테이블 삭제에 대한 액세스를 과도하게 요청한 경우에만 발생합니다.|  
|THREADPOOL|태스크가 작업자가 실행될 때까지 대기하는 경우에 발생합니다. 이는 최대 작업자 설정이 너무 낮거나 해당 일괄 처리 실행이 비정상적으로 오래 수행되어 다른 일괄 처리에 사용할 수 있는 작업자 수가 감소한 것입니다.|  
|TIMEPRIV_TIMEPERIOD|확장 이벤트 타이머의 내부 동기화 중에 발생합니다.|  
|TRACEWRITE|SQL 추적 행 집합 추적 공급자가 사용 가능한 버퍼나 이벤트를 포함한 버퍼가 처리될 때까지 대기하는 경우에 발생합니다.|  
|TRAN_MARKLATCH_DT|표시된 트랜잭션에 대한 삭제 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.|  
|TRAN_MARKLATCH_EX|표시된 트랜잭션에 대한 배타 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.|  
|TRAN_MARKLATCH_KP|표시된 트랜잭션에 대한 유지 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.|  
|TRAN_MARKLATCH_NL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|TRAN_MARKLATCH_SH|표시된 트랜잭션에 대한 공유 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.|  
|TRAN_MARKLATCH_UP|표시된 트랜잭션에 대한 업데이트 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.|  
|TRANSACTION_MUTEX|트랜잭션에 대한 여러 일괄 처리의 액세스 동기화 중에 발생합니다.|  
|UTIL_PAGE_ALLOC|트랜잭션 로그 검색이 메모리 부족 시 메모리를 사용할 수 있을 때까지 대기하는 경우에 발생합니다.|  
|VIA_ACCEPT|시작하는 동안 VIA(Virtual Interface Adapter) 공급자 연결이 완료된 경우에 발생합니다.|  
|VIEW_DEFINITION_MUTEX|캐시된 뷰 정의에 대한 액세스 동기화 중에 발생합니다.|  
|WAIT_FOR_RESULTS|쿼리 알림이 트리거될 때까지 대기하는 경우에 발생합니다.|  
|WAITFOR|WAITFOR [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 결과로 발생합니다. 대기 시간은 문의 매개 변수에 의해 결정됩니다. 이 대기는 사용자가 시작합니다.|  
|WAITFOR_TASKSHUTDOWN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|WAITSTAT_MUTEX|sys.dm_os_wait_stats를 채우는 데 사용되는 통계 컬렉션에 대한 액세스 동기화 중에 발생합니다.|  
|WCC|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|WORKTBL_DROP|작업 테이블 삭제가 실패한 후 다시 시도하기 전에 일시 중지하는 동안 발생합니다.|  
|WRITE_COMPLETION|쓰기 작업이 진행 중인 경우에 발생합니다.|  
|WRITELOG|로그 플러시가 완료될 때까지 대기하는 동안 발생합니다. 로그 플러시를 발생시키는 일반적인 작업은 검사점과 트랜잭션 커밋입니다.|  
|XACT_OWN_TRANSACTION|트랜잭션 소유권을 획득하기 위해 대기하는 동안 발생합니다.|  
|XACT_RECLAIM_SESSION|세션의 현재 소유자가 세션 소유권을 해제할 때까지 대기하는 동안 발생합니다.|  
|XACTLOCKINFO|트랜잭션 잠금 목록에 대한 액세스 동기화 중에 발생합니다. 트랜잭션 자체 외에도 교착 상태 감지, 페이지 분할 중 잠금 마이그레이션 등의 작업이 이 잠금 목록에 액세스합니다.|  
|XACTWORKSPACE_MUTEX|트랜잭션에서 제거 및 트랜잭션 참여 멤버 간의 데이터베이스 잠금 수 동기화 중에 발생합니다.|  
|XE_BUFFERMGR_ALLPROCESSED_EVENT|확장 이벤트 세션 버퍼를 대상으로 플러시할 때 발생합니다. 이 대기는 백그라운드 스레드에서 발생합니다.|  
|XE_BUFFERMGR_FREEBUF_EVENT|다음 조건 중 하나에 해당하는 경우 발생합니다.<br /><br /> 이벤트 손실이 없도록 확장 이벤트 세션을 구성했고 세션의 모든 버퍼가 현재 가득 차 있는 경우. 이는 확장 이벤트 세션의 버퍼가 너무 작거나 분할이 필요함을 의미할 수 있습니다.<br /><br /> 감사 지연이 발생하는 경우. 이는 감사를 기록하는 드라이브에 디스크 병목 현상이 있음을 의미할 수 있습니다.|  
|XE_DISPATCHER_CONFIG_SESSION_LIST|비동기 대상을 사용하는 확장 이벤트 세션이 시작 또는 중지될 때 발생합니다. 이 대기는 다음 중 하나를 의미할 수 있습니다.<br /><br /> 백그라운드 스레드 풀에 확장 이벤트 세션을 등록하는 중입니다.<br /><br /> 백그라운드 스레드 풀에서 현재 부하를 기준으로 필요한 스레드 수를 계산하는 중입니다.|  
|XE_DISPATCHER_JOIN|확장 이벤트 세션에 사용되는 백그라운드 스레드가 종료되는 경우 발생합니다.|  
|XE_DISPATCHER_WAIT|확장 이벤트 세션에 사용되는 백그라운드 스레드가 이벤트 버퍼 처리를 기다리는 경우 발생합니다.|  
|XE_MODULEMGR_SYNC|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|XE_OLS_LOCK|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|XE_PACKAGE_LOCK_BACKOFF|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|FT_COMPROWSET_RWLOCK|전체 텍스트가 조각 메타데이터 작업에서 대기 중입니다. 정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.|  
|FT_IFTS_RWLOCK|전체 텍스트가 내부 동기화에서 대기 중입니다. 정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.|  
|FT_IFTS_SCHEDULER_IDLE_WAIT|전체 텍스트 스케줄러 중지 대기 유형입니다. 스케줄러가 유휴 상태입니다.|  
|FT_IFTSHC_MUTEX|전체 텍스트가 fdhost 제어 작업에서 대기 중입니다. 정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.|  
|FT_IFTSISM_MUTEX|전체 텍스트가 통신 작업에서 대기 중입니다. 정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.|  
|FT_MASTER_MERGE|전체 텍스트가 마스터 병합 작업에서 대기 중입니다. 정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.|  
  
  
