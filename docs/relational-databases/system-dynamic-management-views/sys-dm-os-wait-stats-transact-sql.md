---
title: sys.dm_os_wait_stats (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_wait_stats_TSQL
- dm_os_wait_stats
- sys.dm_os_wait_stats
- sys.dm_os_wait_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_wait_stats dynamic management view
ms.assetid: 568d89ed-2c96-4795-8a0c-2f3e375081da
caps.latest.revision: "111"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 1e6b1129e76717981e08ff35a97abf516c134ac3
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="sysdmoswaitstats-transact-sql"></a>sys.dm_os_wait_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

실행 중인 스레드로 인해 발생한 모든 대기에 대한 정보를 반환합니다. 이 집계 뷰를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 관련된 성능 문제뿐 아니라 특정 쿼리 및 일괄 처리와 관련된 성능 문제도 진단할 수 있습니다. [sys.dm_exec_session_wait_stats&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) 세션에서 비슷한 정보를 제공 합니다.  
  
> [!NOTE] 
> 이 메서드를 호출 하려면  **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** , 이름을 사용 하 여 **sys.dm_pdw_nodes_os_wait_stats**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar (60)**|대기 유형의 이름입니다. 자세한 내용은 참조 [대기 유형](#WaitTypes)이 항목의 뒷부분에 나오는 합니다.|  
|waiting_tasks_count|**bigint**|이 대기 유형의 대기 수입니다. 이 카운터는 각 대기가 시작될 때 증가합니다.|  
|wait_time_ms|**bigint**|이 대기 유형의 총 대기 시간(밀리초)입니다. 이 시간은 signal_wait_time_ms를 포함합니다.|  
|max_wait_time_ms|**bigint**|이 대기 유형의 최대 대기 시간입니다.|  
|signal_wait_time_ms|**bigint**|대기 스레드가 신호를 받은 시간과 실행을 시작한 시간 사이의 차이입니다.|  
|pdw_node_id|**int**|이 배포에 있는 노드에 대 한 식별자입니다. <br/> **적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] |  
  
## <a name="permissions"></a>Permissions  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 프리미엄 계층 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층 필요는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정.  
  
##  <a name="WaitTypes"></a>대기 유형  
 **리소스 대기** 리소스 대기 자가 다른 작업 자가 사용 되 고 있거나 아직 제공 되지 않습니다에 사용할 수 없는 리소스에 대 한 액세스를 요청 하는 경우에 발생 합니다. 리소스 대기의 예로는 잠금, 래치, 네트워크 및 디스크 I/O 대기가 있습니다. 잠금 및 래치 대기는 동기화 개체에 대한 대기입니다.  
  
**큐 대기**  
 큐 대기는 작업자가 유휴 상태로 작업이 할당될 때까지 대기하는 경우에 발생합니다. 큐 대기는 교착 상태 모니터 및 삭제된 레코드 정리 작업 같은 시스템 백그라운드 태스크에서 가장 많이 발생합니다. 이러한 태스크는 작업 큐에 작업 요청이 배치될 때까지 대기합니다. 큐에 새 패킷이 배치되지 않았어도 큐 대기가 정기적으로 활성화될 수 있습니다.  
  
 **외부 대기**  
 외부 대기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업자가 확장 저장 프로시저 호출 또는 연결된 서버 쿼리 같은 외부 이벤트가 완료될 때까지 대기하는 경우에 발생합니다. 차단 문제를 진단할 때는 작업자가 외부 코드를 일부 실행하고 있을 수 있기 때문에 외부 대기가 항상 작업자가 유휴 상태임을 의미하지는 않는다는 점을 유념하세요.  
  
 `sys.dm_os_wait_stats`는 완료된 대기 시간을 보여 줍니다. 현재 대기는 이 동적 관리 뷰에 표시되지 않습니다.  
  
 다음 중 하나라도 해당되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업자 스레드가 대기하는 것으로 간주되지 않습니다.  
  
-   리소스를 사용 가능합니다.  
  
-   큐가 비어 있지 않습니다.  
  
-   외부 프로세스가 완료됩니다.  
  
 스레드가 더 이상 대기하지 않더라도 즉시 스레드 실행을 시작하지는 않습니다. 그와 같은 스레드가 실행 가능한 작업자 큐의 첫 번째 항목이고 퀀텀이 스케줄러에서 실행될 때까지 대기해야 하기 때문입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대기 시간 카운터는 **bigint** 값 및 많지 않기 같이 카운터가 쉽게 롤오버의 이전 버전에서의 해당 카운터 만큼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 쿼리 실행 중에 특정 유형의 대기 시간이 쿼리 내의 병목 또는 대기 지점을 나타낼 수 있습니다. 마찬가지로 높은 대기 시간이나 서버 전체의 대기 횟수가 서버 인스턴스 내의 쿼리 상호 작용에서 병목 또는 핫 스폿을 나타낼 수 있습니다. 예를 들어 잠금 대기는 쿼리의 데이터 경합을, 페이지 IO 래치 대기는 느린 IO 응답 시간을, 페이지 래치 업데이트 대기는 잘못된 파일 레이아웃을 나타냅니다.  
  
 이 동적 관리 뷰의 내용은 다음 명령을 실행하여 다시 설정할 수 있습니다.  
  
``` t-sql  
DBCC SQLPERF ('sys.dm_os_wait_stats', CLEAR);  
GO  
```  
  
이 명령은 모든 카운터를 0으로 다시 설정합니다.  
  
> [!NOTE]
> 이러한 통계는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작할 경우 지속되지 않으며 모든 데이터는 통계가 마지막으로 다시 설정된 이후나 서버가 시작된 이후로 누적됩니다.  
  
 다음 표에서는 태스크에서 발생한 대기 유형을 나열합니다.  

|유형 |Description| 
|-------------------------- |--------------------------| 
|ABR |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| | 
|AM_INDBUILD_ALLOCATION |TBD <br />**적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|AM_SCHEMAMGR_UNSHARED_CACHE |TBD <br />**적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ASSEMBLY_FILTER_HASHTABLE |TBD <br />**적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ASSEMBLY_LOAD |어셈블리 로드에 대한 단독 액세스 중에 발생합니다.| 
|ASYNC_DISKPOOL_LOCK |파일 만들기 또는 초기화 같은 태스크를 수행하고 있는 병렬 스레드를 동기화하려고 하는 경우에 발생합니다.| 
|ASYNC_IO_COMPLETION |태스크가 I/O가 완료될 때까지 대기하는 경우에 발생합니다.| 
|ASYNC_NETWORK_IO |태스크가 네트워크 뒤에서 차단되는 경우에 네트워크 쓰기 중에 발생합니다. 클라이언트가 서버의 데이터를 처리하고 있는지 확인합니다.| 
|ASYNC_OP_COMPLETION |TBD <br />**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ASYNC_OP_CONTEXT_READ |TBD <br />**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ASYNC_OP_CONTEXT_WRITE |TBD <br />**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ASYNC_SOCKETDUP_IO |TBD <br />**적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|AUDIT_GROUPCACHE_LOCK |특수 캐시에 대한 액세스를 제어하는 잠금을 기다리는 경우에 발생합니다. 캐시에는 각 감사 동작 그룹을 감사하는 데 사용되는 감사에 대한 정보가 포함되어 있습니다.| 
|AUDIT_LOGINCACHE_LOCK |특수 캐시에 대한 액세스를 제어하는 잠금을 기다리는 경우에 발생합니다. 캐시에는 로그인 감사 동작 그룹을 감사하는 데 사용되는 감사에 대한 정보가 포함되어 있습니다.| 
|AUDIT_ON_DEMAND_TARGET_LOCK |감사와 관련된 확장 이벤트 대상의 단일 초기화를 위한 잠금을 기다리는 경우에 발생합니다.| 
|AUDIT_XE_SESSION_MGR |감사와 관련된 확장 이벤트 세션의 시작 및 중지를 동기화하는 데 사용되는 잠금을 기다리는 경우에 발생합니다.| 
|BACKUP |태스크가 백업 처리의 일부로 차단되는 경우에 발생합니다.| 
|BACKUP_OPERATOR |태스크가 테이프 탑재를 대기하는 경우에 발생합니다. 테이프 상태를 보려면 sys.dm_io_backup_tapes를 쿼리 합니다. 탑재 작업이 보류된 상태가 아니라면 이 대기 유형이 테이프 드라이브의 하드웨어 문제를 나타낼 수 있습니다.| 
|BACKUPBUFFER |백업 태스크가 데이터를 기다리거나 데이터를 저장할 버퍼를 기다리는 경우에 발생합니다. 이 유형은 태스크가 테이프 탑재를 기다리는 경우 외에는 일반적이지 않습니다.| 
|BACKUPIO |백업 태스크가 데이터를 기다리거나 데이터를 저장할 버퍼를 기다리는 경우에 발생합니다. 이 유형은 태스크가 테이프 탑재를 기다리는 경우 외에는 일반적이지 않습니다.| 
|BACKUPTHREAD |태스크가 백업 작업이 완료될 때까지 대기하는 경우에 발생합니다. 대기 시간은 몇 분에서 몇 시간까지 걸릴 수 있습니다. 대기 중인 태스크가 I/O 프로세스에 위치하면 문제가 있는 것이 아닙니다.| 
|BAD_PAGE_PROCESS |백그라운드의 주의 대상 페이지 로거가 5초보다 긴 간격으로 실행되는 것을 방지하려는 경우에 발생합니다. 주의 대상 페이지가 너무 많으면 로거가 자주 실행됩니다.| 
|BLOB_METADATA |TBD <br />**적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BMPALLOCATION |TBD <br />**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BMPBUILD |TBD <br />**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BMPREPARTITION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BMPREPLICATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BPSORT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_CONNECTION_RECEIVE_TASK |연결 끝점에서 메시지를 받기 위한 액세스를 대기하는 경우에 발생합니다. 끝점에 대한 수신 액세스는 직렬화됩니다.| 
|BROKER_DISPATCHER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_ENDPOINT_STATE_MUTEX |Service Broker 연결 끝점의 상태를 액세스 하는 충돌이 있을 때 발생 합니다. 변경 내용의 상태에 대한 액세스는 직렬화됩니다.| 
|BROKER_EVENTHANDLER |태스크가 대기 하는 Service broker 주 이벤트 처리기에서 때 발생 합니다. 매우 짧게 발생해야 합니다.| 
|BROKER_FORWARDER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_INIT |각 활성 데이터베이스에서 Service Broker를 초기화할 때 발생 합니다. 자주 발생하면 안 됩니다.| 
|BROKER_MASTERSTART |태스크가 대기 하는 시작 하는 Service Broker의 기본 이벤트 처리기에 대 한 경우 발생 합니다. 매우 짧게 발생해야 합니다.| 
|BROKER_RECEIVE_WAITFOR |RECEIVE WAITFOR가 대기 중인 경우에 발생합니다. 받을 준비가 된 메시지가 없는 경우에 주로 발생합니다.| 
|BROKER_REGISTERALLENDPOINTS |Service Broker 연결 끝점을 초기화 하는 동안 발생합니다. 매우 짧게 발생해야 합니다.| 
|BROKER_SERVICE |대상 서비스와 연결 된 Service Broker 대상 목록이 업데이트 되거나 우선 순위가 다시 매겨지는 경우 발생 합니다.| 
|BROKER_SHUTDOWN |Service Broker의 계획된 된 종료 있을 때 발생 합니다. 가능하면 매우 짧게 발생해야 합니다.| 
|BROKER_START |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_TASK_SHUTDOWN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_TASK_STOP |Service Broker 큐 태스크 처리기가 태스크를 종료 하려고 할 때 발생 합니다. 상태 검사가 직렬화되고 먼저 실행 상태에 있어야 합니다.| 
|BROKER_TASK_SUBMIT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_TO_FLUSH |Service Broker 지연 flusher 플러시는 메모리 내 전송 개체 작업 테이블을 때 발생 합니다.| 
|BROKER_TRANSMISSION_OBJECT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_TRANSMISSION_TABLE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_TRANSMISSION_WORK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_TRANSMITTER |Service Broker 전송 기가 작업 기다리고 있을 때 발생 합니다.| 
|BUILTIN_HASHKEY_MUTEX |내부 데이터 구조를 초기화하는 동안 인스턴스 시작 후 발생할 수 있습니다. 데이터 구조가 초기화되면 되풀이되지 않습니다.| 
|CHANGE_TRACKING_WAITFORCHANGES |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CHECK_PRINT_RECORD |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|CHECK_SCANNER_MUTEX |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CHECK_TABLES_INITIALIZATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CHECK_TABLES_SINGLE_SCAN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CHECK_TABLES_THREAD_BARRIER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CHECKPOINT_QUEUE |검사점 태스크가 다음 검사점 요청을 대기하는 동안 발생합니다.| 
|CHKPT |검사점 스레드에 시작할 수 있음을 알리기 위해 서버 시작 시 발생합니다.| 
|CLEAR_DB |데이터베이스를 열거나 닫는 등과 같이 데이터베이스의 상태를 변경하는 작업 중에 발생합니다.| 
|CLR_AUTO_EVENT |태스크가 현재 CLR(공용 언어 런타임) 실행 중이며 특정 자동 이벤트가 시작될 때까지 대기하는 경우에 발생합니다. 긴 대기는 일반적인 것이며 문제가 있는 것은 아닙니다.| 
|CLR_CRST |태스크가 현재 CLR 실행 중이며 현재 다른 작업에서 사용 중인 중요한 섹션을 시작하기 위해 대기하는 경우에 발생합니다.| 
|CLR_JOIN |태스크가 현재 CLR 실행 중이며 다른 작업이 끝날 때까지 대기하는 경우에 발생합니다. 이 대기 상태는 태스크 간에 조인이 있는 경우에 발생합니다.| 
|CLR_MANUAL_EVENT |태스크가 현재 CLR 실행 중이며 특정 수동 이벤트가 시작될 때까지 대기하는 경우에 발생합니다.| 
|CLR_MEMORY_SPY |CLR에서 발생하는 모든 가상 메모리 할당을 기록하는 데 사용되는 데이터 구조에 대한 잠금 획득 대기 중에 발생합니다. 병렬 액세스가 있는 경우 무결성이 유지되도록 데이터 구조가 잠깁니다.| 
|CLR_MONITOR |태스크가 현재 CLR 실행 중이며 모니터 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|CLR_RWLOCK_READER |태스크가 현재 CLR 실행 중이며 판독기 잠금으로 인해 대기하는 경우에 발생합니다.| 
|CLR_RWLOCK_WRITER |태스크가 현재 CLR 실행 중이며 기록기 잠금으로 인해 대기하는 경우에 발생합니다.| 
|CLR_SEMAPHORE |태스크가 현재 CLR 실행 중이며 세마포를 기다리는 경우에 발생합니다.| 
|CLR_TASK_START |CLR 태스크 시작이 완료될 때까지 대기하는 동안 발생합니다.| 
|CLRHOST_STATE_ACCESS |CLR 호스팅 데이터 구조를 단독으로 사용하려고 대기하는 경우에 발생합니다. 이 대기 유형은 CLR 런타임을 설정 또는 중지하는 동안 발생합니다.| 
|CMEMPARTITIONED |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CMEMTHREAD |태스크가 스레드로부터 안전한 메모리 개체를 기다리는 경우에 발생합니다. 여러 태스크가 같은 메모리 개체의 메모리를 할당하려고 하여 경합이 발생할 때 대기 시간이 증가할 수 있습니다.| 
|COLUMNSTORE_BUILD_THROTTLE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|COLUMNSTORE_COLUMNDATASET_SESSION_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|COMMIT_TABLE |TBD| 
|CONNECTION_ENDPOINT_LOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|COUNTRECOVERYMGR |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CREATE_DATINISERVICE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CXCONSUMER |병렬 쿼리 계획에서 소비자 스레드 행 보낼 공급자 스레드를 대기할 때 발생 합니다. 이 병렬 쿼리 실행의 정상적인 일부입니다. <br /> **적용 대상**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 및[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|
|CXPACKET |병렬 쿼리 계획 생성 하 고 행을 사용 하는 경우 및 쿼리 프로세서 교환 반복기를 동기화 할 때 발생 합니다. 대기 시간이 너무 길고 쿼리 튜닝(예: 인덱스 추가)으로 시간을 줄일 수 없는 경우에는 병렬 처리 비용 임계값을 조정하거나 병렬 처리 수준을 낮추세요.<br /> **참고:** 에 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], CXPACKET 쿼리 프로세서 교환 반복기를 동기화 하 고 제작 및 소비자 스레드에 대 한 행만 참조 합니다. 소비자 스레드는 CXCONSUMER 대기 유형의에서 개별적으로 추적 됩니다.| 
|CXROWSET_SYNC |병렬 범위 검색 중에 발생합니다.| 
|DAC_INIT |관리자 전용 연결이 초기화되는 동안 발생합니다.| 
|DBCC_SCALE_OUT_EXPR_CACHE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DBMIRROR_DBM_EVENT |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|DBMIRROR_DBM_MUTEX |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|DBMIRROR_EVENTS_QUEUE |데이터베이스 미러링이 이벤트가 처리될 때까지 대기하는 경우에 발생합니다.| 
|DBMIRROR_SEND |태스크가 네트워크 계층의 통신 백로그가 지워져서 메시지를 보낼 수 있을 때까지 대기하는 경우에 발생합니다. 통신 계층의 로드가 많아져 데이터베이스 미러링 데이터 처리량에 영향을 미치기 시작했음을 나타냅니다.| 
|DBMIRROR_WORKER_QUEUE |데이터베이스 미러링 작업자 태스크가 추가 작업을 대기하는 경우를 나타냅니다.| 
|DBMIRRORING_CMD |태스크가 로그 레코드가 디스크로 플러시될 때까지 대기하는 경우에 발생합니다. 이 대기 상태는 오랜 시간 동안 유지됩니다.| 
|DBSEEDING_FLOWCONTROL |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DBSEEDING_OPERATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DEADLOCK_ENUM_MUTEX |SQL Server가 동시에 여러 개의 교착 상태 검색을 실행 하지 않았는지 확인 하십시오 교착 상태 모니터와 sys.dm_os_waiting_tasks 때 발생 합니다.| 
|DEADLOCK_TASK_SEARCH |이 리소스의 대기 시간이 길면 서버가 sys.dm_os_waiting_tasks 위에서 쿼리를 실행하고 있으며 이러한 쿼리가 교착 상태 모니터의 교착 상태 검색을 차단하고 있음을 나타냅니다. 이 대기 유형은 교착 상태 모니터에만 사용됩니다. sys.dm_os_waiting_tasks 위의 쿼리는 DEADLOCK_ENUM_MUTEX를 사용합니다.| 
|DEBUG |TRANSACT-SQL 및 CLR 내부 동기화에 대 한 디버깅 중에 발생 합니다.| 
|DIRECTLOGCONSUMER_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DIRTY_PAGE_POLL |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DIRTY_PAGE_SYNC |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DIRTY_PAGE_TABLE_LOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DISABLE_VERSIONING |SQL Server의 가장 오래 된 활성 트랜잭션의 타임 스탬프가 상태 변경이 시작 될 때의 타임 스탬프 보다 이후 중인지 확인 하기 위해 버전 트랜잭션 관리자를 폴링할 때 발생 합니다. 이 경우 ALTER DATABASE 문이 실행되기 전에 시작된 모든 스냅숏 트랜잭션은 완료되었습니다. 이 대기 상태는 ALTER DATABASE 문을 사용 하 여 SQL Server 버전 관리를 해제 하는 경우에 사용 됩니다.| 
|DISKIO_SUSPEND |외부 백업이 활성 상태일 때 태스크가 파일에 액세스하려고 대기하는 경우에 발생합니다. 대기 중인 모든 사용자 프로세스에 대해 보고됩니다. 사용자 프로세스당 값이 5보다 크면 외부 백업을 완료하는 데 걸리는 시간이 너무 긴 것일 수 있습니다.| 
|DISPATCHER_PRIORITY_QUEUE_SEMAPHORE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DISPATCHER_QUEUE_SEMAPHORE |디스패처 풀의 스레드가 처리할 추가 작업을 기다리는 경우에 발생합니다. 이 대기 유형의 대기 시간은 디스패처가 유휴 상태일 때 증가됩니다.| 
|DLL_LOADING_MUTEX |XML 파서 DLL이 로드될 때까지 대기하는 동안 한 번 발생합니다.| 
|DPT_ENTRY_LOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DROP_DATABASE_TIMER_TASK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DROPTEMP |이전 시도가 실패한 경우 임시 개체 삭제를 다시 시도하기 전에 발생합니다. 삭제 시도가 실패할 때마다 대기 시간이 기하급수적으로 증가합니다.| 
|DTC |태스크가 상태 전환 관리에 사용되는 이벤트를 기다리는 경우에 발생합니다. SQL Server에서 MS DTC 서비스 수 없게 되었다는 알림을 받은 후에 Microsoft Distributed Transaction Coordinator (MS DTC) 트랜잭션의 복구가 발생할 때이 상태 제어 합니다.| 
|DTC_ABORT_REQUEST |MS DTC 작업자 세션이 MS DTC 트랜잭션의 소유권을 획득하려고 대기하는 경우에 MS DTC 작업자 세션에서 발생합니다. MS DTC가 트랜잭션의 소유권을 획득한 후에는 세션이 트랜잭션을 롤백할 수 있습니다. 일반적으로 세션은 트랜잭션을 사용하고 있는 다른 세션을 기다립니다.| 
|DTC_RESOLVE |복구 태스크가 트랜잭션의 결과물을 쿼리할 수 있도록 데이터베이스 간 트랜잭션에서 master 데이터베이스를 대기하는 경우에 발생합니다.| 
|DTC_STATE |태스크가 내부 MS DTC 전역 상태 개체의 변경을 방지하는 이벤트를 기다리는 경우에 발생합니다. 이 상태는 매우 짧은 시간 동안 유지되어야 합니다.| 
|DTC_TMDOWN_REQUEST |SQL Server MS DTC 서비스가 사용할 수 없다는 알림을 받을 때 MS DTC 작업자 세션에서 발생 합니다. 먼저 작업자는 MS DTC 복구 프로세스가 시작될 때까지 기다렸다가 작업자가 작업하고 있는 분산 트랜잭션의 결과물을 획득하기 위해 대기합니다. 이것은 MS DTC 서비스와의 연결이 다시 설정될 때까지 계속될 수 있습니다.| 
|DTC_WAITFOR_OUTCOME |복구 태스크가 MS DTC가 활성화되어 준비된 트랜잭션을 해결할 수 있을 때까지 대기하는 경우에 발생합니다.| 
|DTCNEW_ENLIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DTCNEW_PREPARE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DTCNEW_RECOVERY |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DTCNEW_TM |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DTCNEW_TRANSACTION_ENLISTMENT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DTCPNTSYNC |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DUMP_LOG_COORDINATOR |주 태스크가 하위 작업이 데이터를 생성할 때까지 대기하는 경우에 발생합니다. 일반적으로 이 상태는 발생하지 않습니다. 대기 시간이 길면 예상하지 못했던 차단이 발생한 것일 수 있으므로 하위 태스크를 조사해야 합니다.| 
|DUMP_LOG_COORDINATOR_QUEUE |TBD| 
|DUMPTRIGGER |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|EC |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|EE_PMOLOCK |문 실행 중 특정 유형의 메모리 할당을 동기화하는 경우에 발생합니다.| 
|EE_SPECPROC_MAP_INIT |내부 프로시저 해시 테이블 생성을 동기화하는 경우에 발생합니다. 이 대기만 SQL Server 인스턴스가 시작 된 후 해시 테이블에 처음 액세스 하는 동안 발생할 수 있습니다.| 
|ENABLE_EMPTY_VERSIONING |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ENABLE_VERSIONING |SQL Server 데이터베이스를 스냅숏 격리 허용 상태로 전환할 준비가 되었다고 선언 하기 전에 완료 하도록이 데이터베이스의 모든 업데이트 트랜잭션이 대기할 때 발생 합니다. 이 상태는 ALTER DATABASE 문을 사용 하 여 스냅숏 격리를 설정 하는 SQL Server 때 사용 됩니다.| 
|ERROR_REPORTING_MANAGER |여러 개의 동시 오류 로그 초기화를 동기화하는 경우에 발생합니다.| 
|EXCHANGE |병렬 쿼리 중 쿼리 프로세서 교환 반복기에서 동기화 중에 발생합니다.| 
|EXECSYNC |병렬 쿼리 중 쿼리 프로세서 교환 반복기와 관련되지 않은 영역에서 동기화 중에 발생합니다. 이러한 영역의 예에는 비트맵, LOB(Large Binary Object) 및 스풀 반복기가 있습니다. LOB는 이 대기 상태를 자주 사용할 수 있습니다.| 
|EXECUTION_PIPE_EVENT_INTERNAL |연결 컨텍스트를 통해 전송되는 일괄 처리 실행의 제작자 부분과 소비자 부분 동기화 중에 발생합니다.| 
|EXTERNAL_RG_UPDATE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|EXTERNAL_SCRIPT_NETWORK_IO |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 현재 통해 합니다.| 
|EXTERNAL_SCRIPT_PREPARE_SERVICE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|EXTERNAL_SCRIPT_SHUTDOWN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|EXTERNAL_WAIT_ON_LAUNCHER, |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FABRIC_HADR_TRANSPORT_CONNECTION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FABRIC_REPLICA_CONTROLLER_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FABRIC_REPLICA_CONTROLLER_STATE_AND_CONFIG |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FABRIC_REPLICA_PUBLISHER_EVENT_PUBLISH |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FABRIC_REPLICA_PUBLISHER_SUBSCRIBER_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FABRIC_WAIT_FOR_BUILD_REPLICA_EVENT_PROCESSING |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FAILPOINT |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|FCB_REPLICA_READ |스냅숏이나 DBCC에서 만든 임시 스냅숏 스파스 파일의 읽기가 동기화되는 경우에 발생합니다.| 
|FCB_REPLICA_WRITE |스냅숏이나 DBCC에서 만든 임시 스냅숏 스파스 파일에 대한 페이지 밀어넣기 또는 끌어오기가 동기화되는 경우에 발생합니다.| 
|FEATURE_SWITCHES_UPDATE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_DB_KILL_FLAG |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_DB_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_FCB |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_FCB_FIND |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_FCB_PARENT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_FCB_RELEASE_CACHED_ENTRIES |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_FCB_STATE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_FILEOBJECT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_TABLE_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NTFS_STORE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_RECOVERY |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_RSFX_COMM |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_RSFX_WAIT_FOR_MEMORY |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_STARTUP_SHUTDOWN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_STORE_DB |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_STORE_ROWSET_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_STORE_TABLE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILE_VALIDATION_THREADS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILESTREAM_CACHE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILESTREAM_CHUNKER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILESTREAM_CHUNKER_INIT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILESTREAM_FCB |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILESTREAM_FILE_OBJECT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILESTREAM_WORKITEM_QUEUE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILETABLE_SHUTDOWN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FOREIGN_REDO |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 현재 통해 합니다.| 
|FORWARDER_TRANSITION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FS_FC_RWLOCK |다음 중 하나를 수행하기 위해 FILESTREAM 가비지 수집기가 대기하는 경우에 발생합니다.| 
|FS_GARBAGE_COLLECTOR_SHUTDOWN |FILESTREAM 가비지 수집기가 정리 태스크 완료를 기다리는 경우에 발생합니다.| 
|FS_HEADER_RWLOCK |FILESTREAM 헤더 파일(Filestream.hdr)에서 내용을 읽거나 업데이트하기 위해 FILESTREAM 데이터 컨테이너의 FILESTREAM 헤더에 대한 액세스를 얻으려고 대기하는 경우에 발생합니다.| 
|FS_LOGTRUNC_RWLOCK |다음 중 하나를 수행하기 위해 FILESTREAM 로그 잘림에 대한 액세스를 얻으려고 대기하는 경우에 발생합니다.| 
|FSA_FORCE_OWN_XACT |FILESTREAM 파일 I/O 작업을 관련 트랜잭션에 바인딩해야 하지만 현재 다른 세션에서 해당 트랜잭션을 소유하고 있는 경우에 발생합니다.| 
|FSAGENT |FILESTREAM 파일 I/O 작업이 다른 파일 I/O 작업에 사용되는 FILESTREAM 에이전트 리소스를 기다리는 경우에 발생합니다.| 
|FSTR_CONFIG_MUTEX |다른 FILESTREAM 기능 다시 구성 작업이 완료될 때까지 대기하는 경우에 발생합니다.| 
|FSTR_CONFIG_RWLOCK |FILESTREAM 구성 매개 변수에 대한 액세스 직렬화를 대기하는 경우에 발생합니다.| 
|FT_COMPROWSET_RWLOCK |전체 텍스트가 조각 메타데이터 작업에서 대기 중입니다. 정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|FT_IFTS_RWLOCK |전체 텍스트가 내부 동기화에서 대기 중입니다. 정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|FT_IFTS_SCHEDULER_IDLE_WAIT |전체 텍스트 스케줄러 중지 대기 유형입니다. 스케줄러가 유휴 상태입니다.| 
|FT_IFTSHC_MUTEX |전체 텍스트가 fdhost 제어 작업에서 대기 중입니다. 정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|FT_IFTSISM_MUTEX |전체 텍스트가 통신 작업에서 대기 중입니다. 정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|FT_MASTER_MERGE |전체 텍스트가 마스터 병합 작업에서 대기 중입니다. 정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|FT_MASTER_MERGE_COORDINATOR |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FT_METADATA_MUTEX |정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|FT_PROPERTYLIST_CACHE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FT_RESTART_CRAWL |임시 오류로부터 복구하기 위해 마지막으로 알려진 양호 지점부터 전체 텍스트 탐색을 다시 시작해야 하는 경우에 발생합니다. 이 대기를 사용하면 해당 채우기에서 현재 작동 중인 작업자 태스크가 현재 단계를 완료하거나 종료할 수 있습니다.| 
|FULLTEXT GATHERER |전체 텍스트 작업을 동기화하는 경우에 발생합니다.| 
|GDMA_GET_RESOURCE_OWNER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GHOSTCLEANUP_UPDATE_STATS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GHOSTCLEANUPSYNCMGR |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GLOBAL_QUERY_CANCEL |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GLOBAL_QUERY_CLOSE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GLOBAL_QUERY_CONSUMER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GLOBAL_QUERY_PRODUCER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GLOBAL_TRAN_CREATE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GLOBAL_TRAN_UCS_SESSION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GUARDIAN |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|HADR_AG_MUTEX |Always On DDL 문 또는 Windows Server 장애 조치 클러스터링 명령이 가용성 그룹의 구성에 대 한 단독 읽기/쓰기 액세스를 기다리는 경우 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_AR_CRITICAL_SECTION_ENTRY |Always On DDL 문 또는 Windows Server 장애 조치 클러스터링 명령이 연결된 된 가용성 그룹의 로컬 복제본의 런타임 상태에 대 한 단독 읽기/쓰기 액세스를 기다리는 경우 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_AR_MANAGER_MUTEX |가용성 복제본 셧다운이 시작될 때까지 기다리고 있거나 가용성 복제본 시작이 종료될 때까지 기다리는 경우에 발생합니다. 내부 전용입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_AR_UNLOAD_COMPLETED |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_ARCONTROLLER_NOTIFICATIONS_SUBSCRIBER_LIST |상태 변경 또는 구성 변경 등의 가용성 복제본 이벤트에 대한 게시자가 이벤트 구독자 목록에 대한 단독 읽기/쓰기 액세스를 기다리고 있습니다. 내부 전용입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_BACKUP_BULK_LOCK |Always On 주 데이터베이스는 보조 데이터베이스에서 백업 요청을 수신 하 고 배경에 대 한 대기 스레드를 획득 하거나 BulkOp 잠금 해제에 대 한 요청을 처리 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_BACKUP_QUEUE |Always On 주 데이터베이스의 백업 백그라운드 스레드가 보조 데이터베이스에서 새 작업 요청에 대 한 대기 중입니다. (일반적으로 발생 주 데이터베이스 BulkOp 로그의 상태를 유지 하 고 주 데이터베이스에 잠금을 해제할 수 있는지를 나타내기 위해 보조 데이터베이스에 대 한 대기)., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_CLUSAPI_CALL |SQL Server 스레드가 Windows Server 장애 조치 클러스터링 Api를 호출 하려면 (SQL Server에서 예약 된) 비선점형 모드에서 (운영 체제에서 예약 된) 선점형 모드로 전환 되기를 기다리고 있습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_COMPRESSED_CACHE_SYNC |여러 보조 데이터베이스에 전송 된 로그 블록의 중복 압축을 방지 하는 데 사용 되는 압축 된 로그 블록의 캐시에 대 한 액세스를 기다리는 중입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_CONNECTIVITY_INFO |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DATABASE_FLOW_CONTROL |대기 중인 메시지의 최대 수에 도달했을 때 파트너에게 메시지가 전송될 때까지 기다립니다. 로그 검색이 네트워크 전송보다 빠르게 실행 되고 있음을 나타냅니다. 네트워크 전송이 예상 보다 느린 경우에 이런 동기화 문제가 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DATABASE_VERSIONING_STATE |Always On 보조 데이터베이스의 버전 관리 상태 변경 시 발생합니다. 이 대기는 내부 데이터 구조 이며 일반적으로 데이터 액세스에 직접적인 영향을 주지와 정도로 매우 짧습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DATABASE_WAIT_FOR_RECOVERY |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DATABASE_WAIT_FOR_RESTART |데이터베이스를 Always On 가용성 그룹 제어에서 다시 시작 될 때까지 기다리고 있습니다. 정상 조건에서 하지 고객 문제 때문에 이것이 시점에 대기가 예상 여기., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING |Always on 가용성 그룹 커밋 또는 롤백 진행 중이 던 읽기 작업에 대 한 보조 복제본이 활성화 될 때 모든 트랜잭션의 기다리는 동안 행 버전 관리에서 차단 된 읽기 가능한 보조 데이터베이스에 있는 개체에 대 한 쿼리 합니다. 이 대기 유형을 스냅숏 격리에서 쿼리를 실행 하기 전에 사용할 수 있는 행 버전을 사용 하면., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DB_COMMAND |대화 메시지 (여기에 항상 대화 메시지 인프라를 사용 하는 다른 쪽의 명시적 응답이 필요)에 대 한 응답을 기다리는 중입니다. 다양 한 메시지 유형 수가이 대기 유형을 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DB_OP_COMPLETION_SYNC |대화 메시지 (여기에 항상 대화 메시지 인프라를 사용 하는 다른 쪽의 명시적 응답이 필요)에 대 한 응답을 기다리는 중입니다. 다양 한 메시지 유형 수가이 대기 유형을 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DB_OP_START_SYNC |Always On DDL 문 또는 Windows Server 장애 조치 클러스터링 명령이 가용성 데이터베이스 및 해당 런타임 상태에 대 한 직렬화 된 액세스에 대 한 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DBR_SUBSCRIBER |상태 변경 또는 구성 변경 등의 가용성 복제본 이벤트에 대한 게시자가 가용성 데이터베이스에 해당하는 이벤트 구독자의 런타임 상태에 대한 단독 읽기/쓰기 액세스를 기다리고 있습니다. 내부 전용입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DBR_SUBSCRIBER_FILTER_LIST |상태 변경 또는 구성 변경 등의 가용성 복제본 이벤트에 대한 게시자가 가용성 데이터베이스에 해당하는 이벤트 구독자 목록에 대한 단독 읽기/쓰기 액세스를 기다리고 있습니다. 내부 전용입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DBSEEDING |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DBSEEDING_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DBSTATECHANGE_SYNC |데이터베이스 복제본의 내부 상태를 업데이트 하기 위한 동시성 제어 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FABRIC_CALLBACK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_BLOCK_FLUSH |항상 FILESTREAM 전송 관리자가 로그 블록의 처리가 완료 될 때까지 기다립니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_FILE_CLOSE |항상 FILESTREAM 전송 관리자가 다음 FILESTREAM 파일이 처리 되 고 해당 핸들이 닫힐 때까지 기다립니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_FILE_REQUEST |Always On 보조 복제본이 주 복제본이 모든 요청 된 FILESTREAM 전송 기다리고 실행 취소 하는 동안 파일., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_IOMGR |항상 FILESTREAM 전송 관리자를 시작 또는 종료 하는 동안 FILESTREAM 항상에 I/O 관리자를 보호 하는 R/W 잠금을 기다리고 있습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_IOMGR_IOCOMPLETION |FILESTREAM 항상에 I/O 관리자가 I/O 완료 될 때까지 기다립니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_MANAGER |항상 FILESTREAM 전송 관리자를 시작 또는 종료 하는 동안에 항상 FILESTREAM 전송 관리자를 보호 하는 R/W 잠금을 기다리고 있습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_PREPROC |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_GROUP_COMMIT |트랜잭션 커밋 처리가 단일 로그 블록에 여러 커밋 로그 레코드를 넣을 수 있도록 그룹 커밋이 허용될 때까지 기다리고 있습니다. 이 대기는 로그 I/O를 최적화 하는 필요한 조건, 캡처 및 송신 작업., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_LOGCAPTURE_SYNC |검색을 만들거나 삭제할 때 로그 캡처 또는 적용 개체와 관련된 동시성 제어입니다. 이 예상 되는 대기 상태 또는 연결 상태를 변경 하는 파트너입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_LOGCAPTURE_WAIT |로그 레코드를 사용할 수 있을 때까지 기다립니다. 연결을 통해 새 레코드가 생성될 때까지 또는 캐시에 없는 로그를 읽을 때 I/O가 완료될 때까지 기다리는 경우에 발생할 수 있습니다. 로그 검색을 로그의 끝을 따라 잡으면 또는 디스크에서 읽는 경우 예상 되는 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_LOGPROGRESS_SYNC |데이터베이스 복제본의 로그 진행률 상태를 업데이트할 때의 동시성 제어 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_NOTIFICATION_DEQUEUE |Windows Server 장애 조치(Failover) 클러스터링 알림을 처리하는 백그라운드 태스크가 다음 알림을 기다리고 있습니다. 내부 전용입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_NOTIFICATION_WORKER_EXCLUSIVE_ACCESS |Windows Server 장애 조치 클러스터링 알림을 처리 하는 백그라운드 작업의 런타임 상태에 대 한 직렬화 된 액세스에 대 한 Always On 가용성 복제본 관리자 대기 중입니다. 내부 전용입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_NOTIFICATION_WORKER_STARTUP_SYNC |백그라운드 태스크가 Windows Server 장애 조치(Failover) 클러스터링 알림을 처리하는 백그라운드 태스크가 시작될 때까지 기다리고 있습니다. 내부 전용입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_NOTIFICATION_WORKER_TERMINATION_SYNC |백그라운드 태스크가 Windows Server 장애 조치(Failover) 클러스터링 알림을 처리하는 백그라운드 태스크가 종료될 때까지 기다리고 있습니다. 내부 전용입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_PARTNER_SYNC |파트너 목록에서 동시성 제어 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_READ_ALL_NETWORKS |WSFC 네트워크 목록에 대한 읽기 또는 쓰기 액세스를 얻기 위해 기다립니다. 내부적으로만 사용됩니다. 참고: 동적 관리 뷰 (예: sys.dm_hadr_cluster_networks)에 사용 되는 WSFC 네트워크 목록을 저장 하는 엔진 또는 네트워크 정보를 WSFC를 참조 하는 문은 항상에 TRANSACT-SQL 유효성을 검사 하 합니다. 이 목록은 엔진 시작 시 업데이트 됩니다, WSFC 관련 알림 및 내부에 항상 다시 시작 (예를 들어 손실 및 WSFC 쿼럼의 다시 얻은). 해당 목록에서 업데이트가 진행 중일 때는 일반적으로 태스크가 차단됩니다. , <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_RECOVERY_WAIT_FOR_CONNECTION |복구를 실행하기 전에 보조 데이터베이스가 주 데이터베이스에 연결될 때까지 기다립니다. 이 예상된 대기 주에 대 한 연결이 느린 경우을 늘릴 수 있습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_RECOVERY_WAIT_FOR_UNDO |데이터베이스 복구가 보조 데이터베이스에서 주 데이터베이스와의 공통 로그 지점으로 다시 설정하기 위해 되돌리기 및 초기화 단계를 완료할 때까지 기다립니다. 장애 조치 후 예상 되는 대기입니다. 실행 취소 하면 Windows 시스템 모니터 (perfmon.exe) 및 동적 관리 뷰를 통해 진행률을 추적할 수 있습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_REPLICAINFO_SYNC |현재 복제본 상태를 업데이트 하는 동시성 제어 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SEEDING_CANCELLATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SEEDING_FILE_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SEEDING_LIMIT_BACKUPS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SEEDING_SYNC_COMPLETION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SEEDING_TIMEOUT_TASK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SEEDING_WAIT_FOR_COMPLETION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SYNC_COMMIT |동기화된 보조 데이터베이스에 대한 트랜잭션 커밋 처리를 통해 로그가 확정될 때까지 기다립니다. 이 대기는 트랜잭션 지연 성능 카운터에 의해서도 반영됩니다. 이 대기 유형은 사용할 동기화에 대 한 가용성 그룹 및 보내기, 쓰기 및 보조 데이터베이스에 대 한 로그 인정 하는 시간을 나타냅니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SYNCHRONIZING_THROTTLE |트랜잭션 커밋 처리 시 동기화 중인 보조 데이터베이스를 동기화된 상태로 전환하기 위해 주 로그 끝을 따라잡을 수 있도록 허용될 때까지 기다립니다. 이 예상 되는 대기 보조 데이터베이스는 빠른 경우., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_TDS_LISTENER_SYNC |내부 Alwayson 시스템 또는 WSFC 클러스터가 수신기 시작 되거나 중지를 요청 합니다. 이 요청의 처리는 항상 비동기이며 중복 요청을 제거하는 메커니즘이 있습니다. 또한 구성 변경으로 인해 이 프로세스가 일시 중단 되는 순간이 있습니다. 이 수신기 동기화 메커니즘과 관련된 모든 대기는 이 대기 유형을 사용합니다. 내부 전용입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_TDS_LISTENER_SYNC_PROCESSING |시작 하거나 anavailability 그룹 수신기를 중지 해야 하는 항상에 TRANSACT-SQL 문의 끝에 사용 됩니다. 시작/중지 작업은 비동기적으로 수행 하 고, 이후 사용자 스레드 알려져 있는 수신기의 상황이 될 때까지이 대기 유형을 사용 하 여 차단 됩니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_THROTTLE_LOG_RATE_GOVERNOR |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_THROTTLE_LOG_RATE_LOG_SIZE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_THROTTLE_LOG_RATE_SEEDING |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_THROTTLE_LOG_RATE_SEND_RECV_QUEUE_SIZE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_TIMER_TASK |타이머 태스크 개체에 대한 잠금을 가져올 때까지 기다리며, 작업이 수행되는 시간 사이의 실제 대기에도 사용됩니다. 예를 들어 10 초 마다 하나의 실행 후 실행 되는 작업에 대 한 Always On 가용성 그룹 약 10 초는 작업 일정을 변경 하려면 잠시 기다린 후 대기가 여기 포함 됩니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_TRANSPORT_DBRLIST |전송 계층의 데이터베이스 복제본 목록에 대한 액세스를 기다립니다. 에 대 한 액세스 권한을 부여 하는 spinlock에 사용 되는., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_TRANSPORT_FLOW_CONTROL |처리 중인 승인 되지 않은 Always On 메시지의 수를 out 위로 가져갈 때 대기 플로 제어 임계값입니다. (데이터베이스에 데이터베이스에 기반)에 없는 가용성 복제본-기준입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_TRANSPORT_SESSION |Always On 가용성 그룹을 변경 하거나 기본 전송 상태에 액세스 하는 동안 대기 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_WORK_POOL |Always On 가용성 그룹 백그라운드 작업 (task) 개체의 동시성 제어 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_WORK_QUEUE |Always On 가용성 그룹 백그라운드 작업자 스레드 새 작업이 할당 될 때까지 대기 합니다. 이 예상 되는 대기 자가 있는지 준비는 정상 상태인 새 작업을 대기 하는 경우., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_XRF_STACK_ACCESS |에 액세스 (조회, 추가 및 삭제)는 Always On 가용성 데이터베이스에 대 한 확장 된 복구 분기 지점 스택에., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HCCO_CACHE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HK_RESTORE_FILEMAP |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HKCS_PARALLEL_MIGRATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HKCS_PARALLEL_RECOVERY |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HTBUILD |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HTDELETE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HTMEMO |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HTREINIT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HTREPARTITION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HTTP_ENUMERATION |시스템 시작 시에 HTTP를 시작할 HTTP 끝점을 열거하기 위해 발생합니다.| 
|HTTP_START |연결이 HTTP 초기화가 완료될 때까지 대기하는 경우에 발생합니다.| 
|HTTP_STORAGE_CONNECTION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|IMPPROV_IOWAIT |SQL Server 대량 로드 I/O가 완료를 대기할 때 발생 합니다.| 
|INSTANCE_LOG_RATE_GOVERNOR |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|INTERNAL_TESTING |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|IO_AUDIT_MUTEX |추적 이벤트 버퍼 동기화 중에 발생합니다.| 
|IO_COMPLETION |I/O 작업이 완료될 때까지 대기하는 동안 발생합니다. 이 대기 유형은 일반적으로 비데이터 페이지 I/O를 나타냅니다. 데이터 페이지 I/O 완료 대기 PAGEIOLATCH로 표시\_ \* 될 때까지 대기 합니다.| 
|IO_QUEUE_LIMIT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|IO_RETRY |리소스 부족으로 인해 읽기 또는 쓰기와 같은 디스크 I/O 작업이 실패하여 다시 시도되는 경우에 발생합니다.| 
|IOAFF_RANGE_QUEUE |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|KSOURCE_WAKEUP |서비스 제어 관리자의 요청을 대기하는 동안 서비스 제어 태스크에 사용됩니다. 긴 대기가 예상되며 문제가 있는 것은 아닙니다.| 
|KTM_ENLISTMENT |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|KTM_RECOVERY_MANAGER |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|KTM_RECOVERY_RESOLUTION |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|LATCH_DT |DT(삭제) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. 래치 목록이\_ \* 대기는 sys.dm_os_latch_stats에서 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.| 
|LATCH_EX |EX(배타) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. 래치 목록이\_ \* 대기는 sys.dm_os_latch_stats에서 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.| 
|LATCH_KP |KP(유지) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. 래치 목록이\_ \* 대기는 sys.dm_os_latch_stats에서 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.| 
|LATCH_NL |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|LATCH_SH |SH(공유) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. 래치 목록이\_ \* 대기는 sys.dm_os_latch_stats에서 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.| 
|LATCH_UP |UP(업데이트) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. 래치 목록이\_ \* 대기는 sys.dm_os_latch_stats에서 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.| 
|LAZYWRITER_SLEEP |지연 기록기 태스크가 일시 중지되는 경우에 발생합니다. 대기 중인 백그라운드 태스크에서 사용한 시간을 측정한 것입니다. 사용자 대기를 찾을 때 이 상태는 고려하지 마세요.| 
|LCK_M_BU |태스크가 대량 업데이트(BU) 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_BU_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 대량 업데이트(BU) 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_BU_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 대량 업데이트(BU) 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_IS |태스크가 내재된 공유(IS) 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_IS_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 내재된 공유(IS) 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_IS_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 내재된 공유(IS) 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_IU |태스크가 의도 업데이트(IU) 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_IU_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 의도 업데이트(IU) 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_IU_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 의도 업데이트(IU) 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_IX |태스크가 의도 배타(IX) 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_IX_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 의도 배타(IX) 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_IX_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 의도 배타(IX) 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_NL |태스크가 현재 키 값의 NULL 잠금 및 현재 키와 이전 키 간의 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 키의 NULL 잠금은 즉시 해제 잠금입니다.| 
|LCK_M_RIn_NL_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 NULL 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 키의 NULL 잠금은 즉시 해제 잠금입니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_NL_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 NULL 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 키의 NULL 잠금은 즉시 해제 잠금입니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_S |태스크가 현재 키 값의 공유 잠금 및 현재 키와 이전 키 간의 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RIn_S_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 공유 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_S_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 공유 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_U |태스크가 현재 키 값의 업데이트 잠금 및 현재 키와 이전 키 간의 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RIn_U_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 업데이트 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 삽입 범위 잠금을 획득하려고 대기하는 중입니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_U_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 업데이트 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 삽입 범위 잠금을 획득하려고 대기하는 중입니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_X |태스크가 현재 키 값의 배타 잠금 및 현재 키와 이전 키 간의 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RIn_X_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 배타 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_X_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 배타 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RS_S |태스크가 현재 키 값의 공유 잠금 및 현재 키와 이전 키 간의 공유 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RS_S_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 공유 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 공유 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RS_S_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 공유 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 공유 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RS_U |태스크가 현재 키 값의 업데이트 잠금 및 현재 키와 이전 키 간의 업데이트 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RS_U_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 업데이트 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 업데이트 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RS_U_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 업데이트 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 업데이트 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RX_S |태스크가 현재 키 값의 공유 잠금 및 현재 키와 이전 키 간의 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RX_S_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 공유 잠금 및 현재 키와 이전 키 간의 중단 블로커 잠금이 포함된 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RX_S_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 공유 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위 잠금이 포함된 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RX_U |태스크가 현재 키 값의 업데이트 잠금 및 현재 키와 이전 키 간의 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RX_U_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 업데이트 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RX_U_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 업데이트 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RX_X |태스크가 현재 키 값의 배타 잠금 및 현재 키와 이전 키 간의 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RX_X_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 배타 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RX_X_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 배타 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_S |태스크가 공유 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_S_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_S_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SCH_M |태스크가 스키마 수정 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_SCH_M_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 스키마 수정 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SCH_M_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 스키마 수정 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SCH_S |태스크가 스키마 공유 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_SCH_S_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 스키마 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SCH_S_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 스키마 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SIU |태스크가 의도 업데이트 공유 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_SIU_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 의도 업데이트 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SIU_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 의도 업데이트 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SIX |태스크가 의도 배타 공유 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_SIX_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 의도 배타 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SIX_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 의도 배타 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_U |태스크가 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_U_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_U_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_UIX |태스크가 의도 배타 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_UIX_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 의도 배타 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_UIX_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 의도 배타 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_X |태스크가 배타 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_X_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 배타 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_X_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 배타 잠금을 획득하려고 대기하는 경우에 발생합니다. (에 관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션입니다.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOG_POOL_SCAN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOG_RATE_GOVERNOR |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGBUFFER |태스크가 로그 버퍼의 공간에 로그 레코드가 저장될 때까지 대기하는 경우에 발생합니다. 값이 계속 높게 나타나면 로그 장치가 서버에서 생성하는 로그의 양을 따라갈 수 없는 것일 수 있습니다.| 
|LOGCAPTURE_LOGPOOLTRUNCPOINT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGGENERATION |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|LOGMGR |데이터베이스를 닫는 동안 태스크가 로그 종료 전에 처리 중인 로그 I/O가 완료될 때까지 대기하는 경우에 발생합니다.| 
|LOGMGR_FLUSH |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|LOGMGR_PMM_LOG |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGMGR_QUEUE |로그 쓰기 태스크가 작업 요청을 대기하는 동안 발생합니다.| 
|LOGMGR_RESERVE_APPEND |태스크가 로그 잘림으로 인해 로그 공간이 확보되어 작업이 새 로그 레코드를 쓸 수 있는지 확인하려고 대기하는 경우에 발생합니다. 이 대기를 줄이려면 영향을 받는 데이터베이스의 로그 파일 크기를 늘리세요.| 
|LOGPOOL_CACHESIZE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGPOOL_CONSUMER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGPOOL_CONSUMERSET |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGPOOL_FREEPOOLS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGPOOL_MGRSET |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGPOOL_REPLACEMENTSET |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGPOOLREFCOUNTEDOBJECT_REFDONE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOWFAIL_MEMMGR_QUEUE |메모리를 사용할 수 있을 때까지 대기하는 동안 발생합니다.| 
|MD_AGENT_YIELD |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|MD_LAZYCACHE_RWLOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|MEMORY_ALLOCATION_EXT |내부 SQL Server 메모리 풀 또는 운영 체제에서 메모리를 할당 하는 동안 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|MEMORY_GRANT_UPDATE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|METADATA_LAZYCACHE_RWLOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|MIGRATIONBUFFER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|MISCELLANEOUS |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|MISCELLANEOUS |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|MSQL_DQ |분산 쿼리 작업이 완료될 때까지 태스크가 대기하는 경우에 발생합니다. 발생 가능한 MARS(Multiple Active Result Set) 응용 프로그램 교착 상태를 감지하는 데 사용됩니다. 대기는 분산 쿼리 호출이 완료될 때 끝납니다.| 
|MSQL_XACT_MGR_MUTEX |태스크가 세션 트랜잭션 관리자의 소유권을 획득하여 세션 수준 트랜잭션 작업을 수행하려고 대기하는 경우에 발생합니다.| 
|MSQL_XACT_MUTEX |트랜잭션 사용 동기화 중에 발생합니다. 요청에서 트랜잭션을 사용하려면 먼저 뮤텍스를 획득해야 합니다.| 
|MSQL_XP |태스크가 확장 저장 프로시저가 끝날 때까지 대기하는 경우에 발생합니다. SQL Server는이 대기 상태를 사용 하 여 잠재적 MARS 응용 프로그램 교착 상태를 검색 합니다. 대기는 확장 저장 프로시저 호출이 끝날 때 중지됩니다.| 
|MSSEARCH |전체 텍스트 검색 호출 중에 발생합니다. 이 대기는 전체 텍스트 작업이 완료될 때 끝나며 경합이 아니라 전체 텍스트 작업 기간을 나타냅니다.| 
|NET_WAITFOR_PACKET |네트워크 읽기 중 연결이 네트워크 패킷을 대기하는 경우에 발생합니다.| 
|NETWORKSXMLMGRLOAD |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|NODE_CACHE_MUTEX |TBD| 
|OLEDB |SQL Server는 SQL Server Native Client OLE DB 공급자를 호출할 때 발생 합니다. 이 대기 유형은 동기화에 사용되지 않습니다. 대신 OLE DB Provider에 대한 호출 기간을 나타냅니다.| 
|ONDEMAND_TASK_QUEUE |백그라운드 태스크가 우선 순위가 높은 시스템 작업 요청을 대기하는 동안 발생합니다. 대기 시간이 길면 우선 순위가 높은 처리할 요청이 없는 것이므로 염려할 필요가 없습니다.| 
|PAGEIOLATCH_DT |태스크가 I/O 요청에 있는 버퍼를 래치에서 기다리는 경우에 발생합니다. 래치 요청이 삭제 모드에 있습니다. 대기 수가 많으면 디스크 하위 시스템에 문제가 있을 수 있습니다.| 
|PAGEIOLATCH_EX |태스크가 I/O 요청에 있는 버퍼를 래치에서 기다리는 경우에 발생합니다. 래치 요청이 배타 모드에 있습니다. 대기 수가 많으면 디스크 하위 시스템에 문제가 있을 수 있습니다.| 
|PAGEIOLATCH_KP |태스크가 I/O 요청에 있는 버퍼를 래치에서 기다리는 경우에 발생합니다. 래치 요청이 유지 모드에 있습니다. 대기 수가 많으면 디스크 하위 시스템에 문제가 있을 수 있습니다.| 
|PAGEIOLATCH_NL |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|PAGEIOLATCH_SH |태스크가 I/O 요청에 있는 버퍼를 래치에서 기다리는 경우에 발생합니다. 래치 요청이 공유 모드에 있습니다. 대기 수가 많으면 디스크 하위 시스템에 문제가 있을 수 있습니다.| 
|PAGEIOLATCH_UP |태스크가 I/O 요청에 있는 버퍼를 래치에서 기다리는 경우에 발생합니다. 래치 요청이 업데이트 모드에 있습니다. 대기 수가 많으면 디스크 하위 시스템에 문제가 있을 수 있습니다.| 
|PAGELATCH_DT |태스크가 I/O 요청에 없는 버퍼를 래치에서 대기하는 경우에 발생합니다. 래치 요청이 삭제 모드에 있습니다.| 
|PAGELATCH_EX |태스크가 I/O 요청에 없는 버퍼를 래치에서 대기하는 경우에 발생합니다. 래치 요청이 배타 모드에 있습니다.| 
|PAGELATCH_KP |태스크가 I/O 요청에 없는 버퍼를 래치에서 대기하는 경우에 발생합니다. 래치 요청이 유지 모드에 있습니다.| 
|PAGELATCH_NL |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|PAGELATCH_SH |태스크가 I/O 요청에 없는 버퍼를 래치에서 대기하는 경우에 발생합니다. 래치 요청이 공유 모드에 있습니다.| 
|PAGELATCH_UP |태스크가 I/O 요청에 없는 버퍼를 래치에서 대기하는 경우에 발생합니다. 래치 요청이 업데이트 모드에 있습니다.| 
|PARALLEL_BACKUP_QUEUE |RESTORE HEADERONLY, RESTORE FILELISTONLY 또는 RESTORE LABELONLY에서 직렬화 출력이 생성되는 경우에 발생합니다.| 
|PARALLEL_REDO_DRAIN_WORKER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PARALLEL_REDO_FLOW_CONTROL |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PARALLEL_REDO_LOG_CACHE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PARALLEL_REDO_TRAN_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PARALLEL_REDO_TRAN_TURN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PARALLEL_REDO_WORKER_SYNC |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PARALLEL_REDO_WORKER_WAIT_WORK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PERFORMANCE_COUNTERS_RWLOCK |TBD| 
|PHYSICAL_SEEDING_DMV |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|POOL_LOG_RATE_GOVERNOR |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_ABR |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG |Windows 이벤트 로그에 감사 이벤트를 기록하기 위해 SQLOS([!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 운영 체제) 스케줄러가 우선 모드로 전환된 경우에 발생합니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG |Windows 보안 로그에 감사 이벤트를 기록하기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|PREEMPTIVE_CLOSEBACKUPMEDIA |백업 미디어를 닫기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.| 
|PREEMPTIVE_CLOSEBACKUPTAPE |테이프 백업 장치를 닫기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.| 
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE |가상 백업 장치를 닫기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.| 
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL |Windows 장애 조치(Failover) 클러스터 작업을 수행하기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.| 
|PREEMPTIVE_COM_COCREATEINSTANCE |COM 개체를 만들기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.| 
|PREEMPTIVE_COM_COGETCLASSOBJECT |TBD| 
|PREEMPTIVE_COM_CREATEACCESSOR |TBD| 
|PREEMPTIVE_COM_DELETEROWS |TBD| 
|PREEMPTIVE_COM_GETCOMMANDTEXT |TBD| 
|PREEMPTIVE_COM_GETDATA |TBD| 
|PREEMPTIVE_COM_GETNEXTROWS |TBD| 
|PREEMPTIVE_COM_GETRESULT |TBD| 
|PREEMPTIVE_COM_GETROWSBYBOOKMARK |TBD| 
|PREEMPTIVE_COM_LBFLUSH |TBD| 
|PREEMPTIVE_COM_LBLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBREADAT |TBD| 
|PREEMPTIVE_COM_LBSETSIZE |TBD| 
|PREEMPTIVE_COM_LBSTAT |TBD| 
|PREEMPTIVE_COM_LBUNLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBWRITEAT |TBD| 
|PREEMPTIVE_COM_QUERYINTERFACE |TBD| 
|PREEMPTIVE_COM_RELEASE |TBD| 
|PREEMPTIVE_COM_RELEASEACCESSOR |TBD| 
|PREEMPTIVE_COM_RELEASEROWS |TBD| 
|PREEMPTIVE_COM_RELEASESESSION |TBD| 
|PREEMPTIVE_COM_RESTARTPOSITION |TBD| 
|PREEMPTIVE_COM_SEQSTRMREAD |TBD| 
|PREEMPTIVE_COM_SEQSTRMREADANDWRITE |TBD| 
|PREEMPTIVE_COM_SETDATAFAILURE |TBD| 
|PREEMPTIVE_COM_SETPARAMETERINFO |TBD| 
|PREEMPTIVE_COM_SETPARAMETERPROPERTIES |TBD| 
|PREEMPTIVE_COM_STRMLOCKREGION |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDREAD |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDWRITE |TBD| 
|PREEMPTIVE_COM_STRMSETSIZE |TBD| 
|PREEMPTIVE_COM_STRMSTAT |TBD| 
|PREEMPTIVE_COM_STRMUNLOCKREGION |TBD| 
|PREEMPTIVE_CONSOLEWRITE |TBD| 
|PREEMPTIVE_CREATEPARAM |TBD| 
|PREEMPTIVE_DEBUG |TBD| 
|PREEMPTIVE_DFSADDLINK |TBD| 
|PREEMPTIVE_DFSLINKEXISTCHECK |TBD| 
|PREEMPTIVE_DFSLINKHEALTHCHECK |TBD| 
|PREEMPTIVE_DFSREMOVELINK |TBD| 
|PREEMPTIVE_DFSREMOVEROOT |TBD| 
|PREEMPTIVE_DFSROOTFOLDERCHECK |TBD| 
|PREEMPTIVE_DFSROOTINIT |TBD| 
|PREEMPTIVE_DFSROOTSHARECHECK |TBD| 
|PREEMPTIVE_DTC_ABORT |TBD| 
|PREEMPTIVE_DTC_ABORTREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_BEGINTRANSACTION |TBD| 
|PREEMPTIVE_DTC_COMMITREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_ENLIST |TBD| 
|PREEMPTIVE_DTC_PREPAREREQUESTDONE |TBD| 
|PREEMPTIVE_FILESIZEGET |TBD| 
|PREEMPTIVE_FSAOLEDB_ABORTTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_COMMITTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_STARTTRANSACTION |TBD| 
|PREEMPTIVE_FSRECOVER_UNCONDITIONALUNDO |TBD| 
|PREEMPTIVE_GETRMINFO |TBD| 
|PREEMPTIVE_HADR_LEASE_MECHANISM |CSS 진단에 대 한 일정 always On 가용성 그룹 임대 관리자., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_HTTP_EVENT_WAIT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_HTTP_REQUEST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_LOCKMONITOR |TBD| 
|PREEMPTIVE_MSS_RELEASE |TBD| 
|PREEMPTIVE_ODBCOPS |TBD| 
|PREEMPTIVE_OLE_UNINIT |TBD| 
|PREEMPTIVE_OLEDB_ABORTORCOMMITTRAN |TBD| 
|PREEMPTIVE_OLEDB_ABORTTRAN |TBD| 
|PREEMPTIVE_OLEDB_GETDATASOURCE |TBD| 
|PREEMPTIVE_OLEDB_GETLITERALINFO |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTYINFO |TBD| 
|PREEMPTIVE_OLEDB_GETSCHEMALOCK |TBD| 
|PREEMPTIVE_OLEDB_JOINTRANSACTION |TBD| 
|PREEMPTIVE_OLEDB_RELEASE |TBD| 
|PREEMPTIVE_OLEDB_SETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDBOPS |TBD| 
|PREEMPTIVE_OS_ACCEPTSECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_ACQUIRECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_AUTHENTICATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHORIZATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHZGETINFORMATIONFROMCONTEXT |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZECONTEXTFROMSID |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZERESOURCEMANAGER |TBD| 
|PREEMPTIVE_OS_BACKUPREAD |TBD| 
|PREEMPTIVE_OS_CLOSEHANDLE |TBD| 
|PREEMPTIVE_OS_CLUSTEROPS |TBD| 
|PREEMPTIVE_OS_COMOPS |TBD| 
|PREEMPTIVE_OS_COMPLETEAUTHTOKEN |TBD| 
|PREEMPTIVE_OS_COPYFILE |TBD| 
|PREEMPTIVE_OS_CREATEDIRECTORY |TBD| 
|PREEMPTIVE_OS_CREATEFILE |TBD| 
|PREEMPTIVE_OS_CRYPTACQUIRECONTEXT |TBD| 
|PREEMPTIVE_OS_CRYPTIMPORTKEY |TBD| 
|PREEMPTIVE_OS_CRYPTOPS |TBD| 
|PREEMPTIVE_OS_DECRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_DELETEFILE |TBD| 
|PREEMPTIVE_OS_DELETESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_DEVICEIOCONTROL |TBD| 
|PREEMPTIVE_OS_DEVICEOPS |TBD| 
|PREEMPTIVE_OS_DIRSVC_NETWORKOPS |TBD| 
|PREEMPTIVE_OS_DISCONNECTNAMEDPIPE |TBD| 
|PREEMPTIVE_OS_DOMAINSERVICESOPS |TBD| 
|PREEMPTIVE_OS_DSGETDCNAME |TBD| 
|PREEMPTIVE_OS_DTCOPS |TBD| 
|PREEMPTIVE_OS_ENCRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_FILEOPS |TBD| 
|PREEMPTIVE_OS_FINDFILE |TBD| 
|PREEMPTIVE_OS_FLUSHFILEBUFFERS |TBD| 
|PREEMPTIVE_OS_FORMATMESSAGE |TBD| 
|PREEMPTIVE_OS_FREECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_FREELIBRARY |TBD| 
|PREEMPTIVE_OS_GENERICOPS |TBD| 
|PREEMPTIVE_OS_GETADDRINFO |TBD| 
|PREEMPTIVE_OS_GETCOMPRESSEDFILESIZE |TBD| 
|PREEMPTIVE_OS_GETDISKFREESPACE |TBD| 
|PREEMPTIVE_OS_GETFILEATTRIBUTES |TBD| 
|PREEMPTIVE_OS_GETFILESIZE |TBD| 
|PREEMPTIVE_OS_GETFINALFILEPATHBYHANDLE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_OS_GETLONGPATHNAME |TBD| 
|PREEMPTIVE_OS_GETPROCADDRESS |TBD| 
|PREEMPTIVE_OS_GETVOLUMENAMEFORVOLUMEMOUNTPOINT |TBD| 
|PREEMPTIVE_OS_GETVOLUMEPATHNAME |TBD| 
|PREEMPTIVE_OS_INITIALIZESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_LIBRARYOPS |TBD| 
|PREEMPTIVE_OS_LOADLIBRARY |TBD| 
|PREEMPTIVE_OS_LOGONUSER |TBD| 
|PREEMPTIVE_OS_LOOKUPACCOUNTSID |TBD| 
|PREEMPTIVE_OS_MESSAGEQUEUEOPS |TBD| 
|PREEMPTIVE_OS_MOVEFILE |TBD| 
|PREEMPTIVE_OS_NETGROUPGETUSERS |TBD| 
|PREEMPTIVE_OS_NETLOCALGROUPGETMEMBERS |TBD| 
|PREEMPTIVE_OS_NETUSERGETGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERGETLOCALGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERMODALSGET |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICY |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICYFREE |TBD| 
|PREEMPTIVE_OS_OPENDIRECTORY |TBD| 
|PREEMPTIVE_OS_PDH_WMI_INIT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_OS_PIPEOPS |TBD| 
|PREEMPTIVE_OS_PROCESSOPS |TBD| 
|PREEMPTIVE_OS_QUERYCONTEXTATTRIBUTES |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_OS_QUERYREGISTRY |TBD| 
|PREEMPTIVE_OS_QUERYSECURITYCONTEXTTOKEN |TBD| 
|PREEMPTIVE_OS_REMOVEDIRECTORY |TBD| 
|PREEMPTIVE_OS_REPORTEVENT |TBD| 
|PREEMPTIVE_OS_REVERTTOSELF |TBD| 
|PREEMPTIVE_OS_RSFXDEVICEOPS |TBD| 
|PREEMPTIVE_OS_SECURITYOPS |TBD| 
|PREEMPTIVE_OS_SERVICEOPS |TBD| 
|PREEMPTIVE_OS_SETENDOFFILE |TBD| 
|PREEMPTIVE_OS_SETFILEPOINTER |TBD| 
|PREEMPTIVE_OS_SETFILEVALIDDATA |TBD| 
|PREEMPTIVE_OS_SETNAMEDSECURITYINFO |TBD| 
|PREEMPTIVE_OS_SQLCLROPS |TBD| 
|PREEMPTIVE_OS_SQMLAUNCH |TBD <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 부터 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]까지 |  
|PREEMPTIVE_OS_VERIFYSIGNATURE |TBD| 
|PREEMPTIVE_OS_VERIFYTRUST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_OS_VSSOPS |TBD| 
|PREEMPTIVE_OS_WAITFORSINGLEOBJECT |TBD| 
|PREEMPTIVE_OS_WINSOCKOPS |TBD| 
|PREEMPTIVE_OS_WRITEFILE |TBD| 
|PREEMPTIVE_OS_WRITEFILEGATHER |TBD| 
|PREEMPTIVE_OS_WSASETLASTERROR |TBD| 
|PREEMPTIVE_REENLIST |TBD| 
|PREEMPTIVE_RESIZELOG |TBD| 
|PREEMPTIVE_ROLLFORWARDREDO |TBD| 
|PREEMPTIVE_ROLLFORWARDUNDO |TBD| 
|PREEMPTIVE_SB_STOPENDPOINT |TBD| 
|PREEMPTIVE_SERVER_STARTUP |TBD| 
|PREEMPTIVE_SETRMINFO |TBD| 
|PREEMPTIVE_SHAREDMEM_GETDATA |TBD| 
|PREEMPTIVE_SNIOPEN |TBD| 
|PREEMPTIVE_SOSHOST |TBD| 
|PREEMPTIVE_SOSTESTING |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|PREEMPTIVE_SP_SERVER_DIAGNOSTICS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_STARTRM |TBD| 
|PREEMPTIVE_STREAMFCB_CHECKPOINT |TBD| 
|PREEMPTIVE_STREAMFCB_RECOVER |TBD| 
|PREEMPTIVE_STRESSDRIVER |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|PREEMPTIVE_TESTING |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|PREEMPTIVE_TRANSIMPORT |TBD| 
|PREEMPTIVE_UNMARSHALPROPAGATIONTOKEN |TBD| 
|PREEMPTIVE_VSS_CREATESNAPSHOT |TBD| 
|PREEMPTIVE_VSS_CREATEVOLUMESNAPSHOT |TBD| 
|PREEMPTIVE_XE_CALLBACKEXECUTE |TBD| 
|PREEMPTIVE_XE_CX_FILE_OPEN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_XE_CX_HTTP_CALL |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_XE_DISPATCHER |TBD| 
|PREEMPTIVE_XE_ENGINEINIT |TBD| 
|PREEMPTIVE_XE_GETTARGETSTATE |TBD| 
|PREEMPTIVE_XE_SESSIONCOMMIT |TBD| 
|PREEMPTIVE_XE_TARGETFINALIZE |TBD| 
|PREEMPTIVE_XE_TARGETINIT |TBD| 
|PREEMPTIVE_XE_TIMERRUN |TBD| 
|PREEMPTIVE_XETESTING |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|PRINT_ROLLBACK_PROGRESS |ALTER DATABASE termination 절을 사용하여 전환된 데이터베이스에서 사용자 프로세스가 끝나기를 기다리는 데 사용됩니다. 자세한 내용은 ALTER DATABASE (TRANSACT-SQL)을 참조 하세요.| 
|PRU_ROLLBACK_DEFERRED |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_ALL_COMPONENTS_INITIALIZED |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_COOP_SCAN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_DIRECTLOGCONSUMER_GETNEXT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_EVENT_SESSION_INIT_MUTEX |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_FABRIC_REPLICA_CONTROLLER_DATA_LOSS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_ACTION_COMPLETED |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC |백그라운드 작업 (폴링)를 통해 수신 하는 백그라운드 태스크의 종료 부분이 끝났으면 기다리고 있을 때 발생 합니다. Windows Server 장애 조치 클러스터링 알림을., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_CLUSTER_INTEGRATION |추가, 바꾸기 및/또는 제거 작업이 Alwayson 내부 목록 (예: 네트워크, 네트워크 주소 또는 가용성 그룹 수신기의 목록)에 대 한 쓰기 잠금을 가져올 기다리고 있습니다. 내부 전용 <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_FAILOVER_COMPLETED |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_JOIN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_OFFLINE_COMPLETED |오프 라인으로 Windows Server 장애 조치 클러스터링 개체를 삭제 하기 전에 대상 가용성 그룹에 대 한 Always On 가용성 그룹 삭제 작업이 대기 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_ONLINE_COMPLETED |Always On 만들기 또는 가용성 그룹 장애 조치 작업이 대상 가용성 그룹이 온라인 상태가 될 때까지 기다리고 있습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_POST_ONLINE_COMPLETED |Always On 가용성 그룹 삭제 작업이 이전 명령의 일부로 예약 된 백그라운드 태스크가 종료 될 때까지 기다리고 있습니다. 예를 들어 가용성 데이터베이스를 주 역할로 전환 중인 백그라운드 작업이 있을 수 있습니다. DROP AVAILABILITY GROUP DDL이 백그라운드 태스크가 종료 경합 상태를 방지 하기 위해 대기 해야 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_SERVER_READY_CONNECTIONS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_WORKITEM_COMPLETED |비동기 작업 태스크가 완료될 때까지 기다리는 스레드에 의한 내부 대기입니다. 이 예상 되는 대기 이며 CSS를 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADRSIM |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_LOG_CONSOLIDATION_IO |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_LOG_CONSOLIDATION_POLL |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_MD_LOGIN_STATS |로그인 통계에 대 한 메타 데이터의 내부 동기화 중에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_MD_RELATION_CACHE |테이블 또는 인덱스에서 메타 데이터의 내부 동기화 중에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_MD_SERVER_CACHE |연결 된 서버에서 메타 데이터의 내부 동기화 중에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_MD_UPGRADE_CONFIG |업그레이드 서버 수준 구성의 내부 동기화 중에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_PREEMPTIVE_APP_USAGE_TIMER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_PREEMPTIVE_AUDIT_ACCESS_WINDOWSLOG |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_QRY_BPMEMORY |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_REPLICA_ONLINE_INIT_MUTEX |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_SBS_FILE_OPERATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_XTP_FSSTORAGE_MAINTENANCE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_XTP_HOST_STORAGE_WAIT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_ASYNC_CHECK_CONSISTENCY_TASK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_ASYNC_PERSIST_TASK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_ASYNC_PERSIST_TASK_START |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_ASYNC_QUEUE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_BCKG_TASK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_BLOOM_FILTER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_CLEANUP_STALE_QUERIES_TASK_MAIN_LOOP_SLEEP |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_CTXS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_DB_DISK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_DYN_VECTOR |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_EXCLUSIVE_ACCESS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_HOST_INIT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_LOADDB |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_PERSIST_TASK_MAIN_LOOP_SLEEP |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_QDS_CAPTURE_INIT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_SHUTDOWN_QUEUE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_STMT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_STMT_DISK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_TASK_SHUTDOWN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_TASK_START |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QE_WARN_LIST_SYNC |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QPJOB_KILL |업데이트가 실행되기 시작할 때 KILL 호출을 통해 비동기 자동 통계 업데이트가 취소되었음을 나타냅니다. 종료하는 스레드는 일시 중지 상태로, KILL 명령을 수신하기 시작할 때까지 대기합니다. 1초보다 작은 값이 좋습니다.| 
|QPJOB_WAITFOR_ABORT |실행되고 있을 때 KILL 호출을 통해 비동기 자동 통계 업데이트가 취소되었음을 나타냅니다. 업데이트는 이제 완료되었지만 종료하는 스레드 메시지 조정이 완료될 때까지 일시 중지됩니다. 이 상태는 일반적이지만 거의 발생하지 않으며 매우 짧아야 합니다. 1초보다 작은 값이 좋습니다.| 
|QRY_MEM_GRANT_INFO_MUTEX |쿼리 실행 메모리 관리 기능이 정적 권한 부여 정보 목록에 대한 액세스를 제어하려고 하는 경우에 발생합니다. 이 상태는 현재 권한이 부여된 메모리 요청과 대기 중인 메모리 요청에 대한 정보를 나열합니다. 이 상태는 단순 액세스 제어 상태입니다. 이 상태에 대한 긴 대기가 있으면 안 됩니다. 이 뮤텍스가 해제되지 않으면 새로운 메모리 사용 쿼리의 응답이 모두 중지됩니다.| 
|QRY_PARALLEL_THREAD_MUTEX |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QRY_PROFILE_LIST_MUTEX |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QUERY_ERRHDL_SERVICE_DONE |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|QUERY_WAIT_ERRHDL_SERVICE |정보를 제공하기 위해서만 확인됩니다.  지원되지 않습니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다.  |  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN |오프라인 인덱스 빌드 생성이 병렬로 실행되고 정렬되는 여러 작업자 스레드가 정렬 파일에 대한 액세스를 동기화하는 특정 경우에 발생합니다.| 
|QUERY_NOTIFICATION_MGR_MUTEX |쿼리 알림 관리자에서 가비지 수집 큐 동기화 중에 발생합니다.| 
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX |쿼리 알림의 트랜잭션 상태 동기화 중에 발생합니다.| 
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX |쿼리 알림 관리자의 내부 동기화 중에 발생합니다.| 
|QUERY_NOTIFICATION_UNITTEST_MUTEX |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|QUERY_OPTIMIZER_PRINT_MUTEX |쿼리 최적화 프로그램의 진단 출력 생성 동기화 중에 발생합니다. 이 대기 유형은 진단 설정이 Microsoft 기술 지원 서비스의 지시 대로 설정 된 경우에 발생 합니다.| 
|QUERY_TASK_ENQUEUE_MUTEX |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QUERY_TRACEOUT |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|RBIO_WAIT_VLF |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|RECOVER_CHANGEDB |웜 대기 데이터베이스의 데이터베이스 상태 동기화 중에 발생합니다.| 
|RECOVERY_MGR_LOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REDO_THREAD_PENDING_WORK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REDO_THREAD_SYNC |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REMOTE_BLOCK_IO |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REMOTE_DATA_ARCHIVE_MIGRATION_DMV |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REMOTE_DATA_ARCHIVE_SCHEMA_DMV |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REMOTE_DATA_ARCHIVE_SCHEMA_TASK_QUEUE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REPL_CACHE_ACCESS |복제 아티클 캐시 동기화 중에 발생합니다. 이 대기 중에는 복제 로그 판독기가 정지되고 게시된 테이블에 대한 DDL(데이터 정의 언어) 문이 차단됩니다.| 
|REPL_HISTORYCACHE_ACCESS |TBD| 
|REPL_SCHEMA_ACCESS |복제 스키마 버전 정보 동기화 중에 발생합니다. 복제된 개체에 대해 DDL 문을 실행하고 로그 판독기가 DDL 발생을 기반으로 버전이 지정된 스키마를 작성하거나 사용할 때 이 상태가 됩니다.| 
|REPL_TRANFSINFO_ACCESS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REPL_TRANHASHTABLE_ACCESS |TBD| 
|REPL_TRANTEXTINFO_ACCESS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REPLICA_WRITES |태스크가 데이터베이스 스냅숏 또는 DBCC 복제본에 대한 페이지 쓰기가 완료될 때까지 대기하는 동안 발생합니다.| 
|REQUEST_DISPENSER_PAUSE |스냅숏 백업을 위해 파일 I/O를 고정할 수 있도록 태스크가 처리 중인 모든 I/O가 완료될 때까지 대기하는 경우에 발생합니다.| 
|REQUEST_FOR_DEADLOCK_SEARCH |교착 상태 모니터가 다음 교착 상태 검색을 시작하기 위해 대기하는 동안 발생합니다. 이 대기는 교착 상태 감지 사이에 발생하며 이 리소스에 대한 총 대기 시간이 길어도 문제가 있는 것은 아닙니다.| 
|RESERVED_MEMORY_ALLOCATION_EXT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|RESMGR_THROTTLED |새 쿼리가 GROUP_MAX_REQUESTS 설정에 따라 들어오고 정체되는 경우 발생합니다.| 
|RESOURCE_GOVERNOR_IDLE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|RESOURCE_QUEUE |다양한 내부 리소스 큐 동기화 중에 발생합니다.| 
|RESOURCE_SEMAPHORE |다른 동시 쿼리로 인해 쿼리 메모리 요청을 즉시 허용할 수 없는 경우에 발생합니다. 대기 수가 많고 대기 시간이 길면 동시 쿼리 수 또는 메모리 요청 양이 과도하게 많은 것입니다.| 
|RESOURCE_SEMAPHORE_MUTEX |쿼리가 스레드 예약 요청이 수행될 때까지 대기하는 동안 발생합니다. 또한 쿼리 컴파일 및 메모리 부여 요청을 동기화하는 경우에 발생합니다.| 
|RESOURCE_SEMAPHORE_QUERY_COMPILE |동시 쿼리 컴파일 수가 조절 한계에 도달한 경우에 발생합니다. 대기 수가 많고 대기 시간이 길면 컴파일, 다시 컴파일 또는 캐싱할 수 없는 계획 수가 과도하게 많은 것입니다.| 
|RESOURCE_SEMAPHORE_SMALL_QUERY |다른 동시 쿼리로 인해 작은 쿼리의 메모리 요청을 즉시 허용할 수 없는 경우에 발생합니다. 서버는 몇 초 내에 요청된 메모리를 부여하지 못하면 주 쿼리 메모리 풀로 요청을 전송하기 때문에 대기 시간은 몇 초를 넘지 않아야 합니다. 대기 수가 많으면 대기 중인 쿼리가 주 메모리 풀을 차단하는 동안 작은 동시 쿼리 수가 과도하게 많은 것입니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|RESTORE_FILEHANDLECACHE_ENTRYLOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|RESTORE_FILEHANDLECACHE_LOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|RG_RECONFIG |TBD| 
|ROWGROUP_OP_STATS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ROWGROUP_VERSION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|RTDATA_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SATELLITE_CARGO |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SATELLITE_SERVICE_SETUP |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SATELLITE_TASK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SBS_DISPATCH |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SBS_RECEIVE_TRANSPORT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SBS_TRANSPORT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SCAN_CHAR_HASH_ARRAY_INITIALIZATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SEC_DROP_TEMP_KEY |임시 보안 키 삭제 시도가 실패한 후 다시 시도하기 전에 발생합니다.| 
|SECURITY_CNG_PROVIDER_MUTEX |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SECURITY_CRYPTO_CONTEXT_MUTEX |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SECURITY_DBE_STATE_MUTEX |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SECURITY_KEYRING_RWLOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SECURITY_MUTEX |EKM(확장 가능 키 관리) 암호화 공급자의 전역 목록 및 EKM 세션의 세션 범위 목록에 대한 액세스를 제어하는 뮤텍스를 기다리는 경우에 발생합니다.| 
|SECURITY_RULETABLE_MUTEX |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SEMPLAT_DSI_BUILD |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SEQUENCE_GENERATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SEQUENTIAL_GUID |새 순차적 GUID를 가져오는 동안 발생합니다.| 
|SERVER_IDLE_CHECK |리소스 모니터를 켜는 또는 유휴로 SQL Server 인스턴스를 선언 하려고 하는 경우 SQL Server 인스턴스 유휴 상태 동기화 중에 발생 합니다.| 
|SERVER_RECONFIGURE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SESSION_WAIT_STATS_CHILDREN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SHARED_DELTASTORE_CREATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SHUTDOWN |종료 문이 활성 연결이 종료될 때까지 대기하는 동안 발생합니다.| 
|SLEEP_BPOOL_FLUSH |검사점이 디스크 하위 시스템의 폭주를 방지하기 위해 새 I/O의 실행을 조절하는 경우에 발생합니다.| 
|SLEEP_BUFFERPOOL_HELPLW |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLEEP_DBSTARTUP |모든 데이터베이스가 복구될 때까지 대기하는 동안 데이터베이스 시작 중에 발생합니다.| 
|SLEEP_DCOMSTARTUP |DCOM 초기화가 완료 될 때까지 기다리는 동안 SQL Server 인스턴스 시작 중에 많아야 한 번 발생 합니다.| 
|SLEEP_MASTERDBREADY |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLEEP_MASTERMDREADY |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLEEP_MASTERUPGRADED |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLEEP_MEMORYPOOL_ALLOCATEPAGES |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLEEP_MSDBSTARTUP |SQL 추적이 msdb 데이터베이스 시작이 완료될 때까지 대기하는 경우에 발생합니다.| 
|SLEEP_RETRY_VIRTUALALLOC |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLEEP_SYSTEMTASK |tempdb 시작이 완료될 때까지 대기하는 동안 백그라운드 태스크 시작 중에 발생합니다.| 
|SLEEP_TASK |일반 이벤트가 발생할 때까지 대기하는 동안 태스크가 중지되는 경우에 발생합니다.| 
|SLEEP_TEMPDBSTARTUP |태스크가 tempdb 시작이 완료될 때까지 대기하는 동안 발생합니다.| 
|SLEEP_WORKSPACE_ALLOCATEPAGE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLO_UPDATE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SMSYNC |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SNI_CONN_DUP |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SNI_CRITICAL_SECTION |SQL Server 네트워킹 구성 요소의 내부 동기화 중에 발생 합니다.| 
|SNI_HTTP_WAITFOR_0_DISCON |처리 중인 HTTP 연결이 종료 될 때까지 기다리는 동안 SQL Server 종료 하는 동안 발생 합니다.| 
|SNI_LISTENER_ACCESS |NUMA(비균일 메모리 액세스) 노드의 상태 변경 업데이트 작업을 대기하는 동안 발생합니다. 상태 변경에 대한 액세스는 직렬화됩니다.| 
|SNI_TASK_COMPLETION |NUMA 노드 상태 변경 동안 모든 태스크가 완료될 때까지 대기하는 중에 발생합니다.| 
|SNI_WRITE_ASYNC |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SOAP_READ |HTTP 네트워크 읽기가 완료될 때까지 대기하는 동안 발생합니다.| 
|SOAP_WRITE |HTTP 네트워크 쓰기가 완료될 때까지 대기하는 동안 발생합니다.| 
|SOCKETDUPLICATEQUEUE_CLEANUP |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SOS_CALLBACK_REMOVAL |콜백을 제거하기 위해 콜백 목록에 대한 동기화를 수행하는 동안 발생합니다. 서버 초기화가 완료된 후에는 이 카운터가 변경되지 않습니다.| 
|SOS_DISPATCHER_MUTEX |디스패처 풀의 내부 동기화 중에 발생합니다. 풀이 조정되는 경우도 포함됩니다.| 
|SOS_LOCALALLOCATORLIST |[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 메모리 관리자의 내부 동기화 중에 발생합니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|SOS_MEMORY_TOPLEVELBLOCKALLOCATOR |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SOS_MEMORY_USAGE_ADJUSTMENT |메모리 사용량이 풀 사이에서 조절될 경우 발생합니다.| 
|SOS_OBJECT_STORE_DESTROY_MUTEX |풀에서 개체를 삭제하는 경우 메모리 풀의 내부 동기화 중에 발생합니다.| 
|SOS_PHYS_PAGE_CACHE |스레드가 물리적 페이지를 할당하거나 물리적 페이지를 운영 체제에 반환하기 전에 확보해야 하는 뮤텍스를 획득하기 위해 대기하는 시간을 고려합니다. 이 형식에 대 한 대기는 SQL Server 인스턴스에서 AWE 메모리를 사용 하는 경우에 나타납니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SOS_PROCESS_AFFINITY_MUTEX |프로세스 선호도 설정에 대한 액세스 동기화 중에 발생합니다.| 
|SOS_RESERVEDMEMBLOCKLIST |SQL Server 메모리 관리자의 내부 동기화 중에 발생 합니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|SOS_SCHEDULER_YIELD |다른 작업이 실행될 수 있도록 태스크가 자발적으로 스케줄러를 양보하는 경우에 발생합니다. 이 대기 중에 태스크는 해당 퀀텀이 갱신될 때까지 대기합니다.| 
|SOS_SMALL_PAGE_ALLOC |일부 메모리 개체에 의해 관리되는 메모리의 할당 및 해제 중에 발생합니다.| 
|SOS_STACKSTORE_INIT_MUTEX |내부 저장소 초기화 동기화 중에 발생합니다.| 
|SOS_SYNC_TASK_ENQUEUE_EVENT |태스크가 동기 방식으로 시작되는 경우에 발생합니다. SQL Server에서 대부분의 작업은 비동기 방식 제어를 반환 하는 시작에 작업 요청이 작업 큐에 배치 된 후에 즉시 시작 됩니다.| 
|SOS_VIRTUALMEMORY_LOW |메모리 할당이 리소스 관리자가 가상 메모리를 해제할 때까지 대기하는 경우에 발생합니다.| 
|SOSHOST_EVENT |CLR과 같은 호스팅된 구성 요소가 SQL Server 이벤트 동기화 개체를 대기 하는 경우 발생 합니다.| 
|SOSHOST_INTERNAL |CLR과 같은 호스팅된 구성 요소에 사용되는 메모리 관리자 콜백 동기화 중에 발생합니다.| 
|SOSHOST_MUTEX |CLR과 같은 호스팅된 구성 요소가 SQL Server 뮤텍스 동기화 개체를 대기 하는 경우 발생 합니다.| 
|SOSHOST_RWLOCK |CLR과 같은 호스팅된 구성 요소가 SQL Server 읽기 / 쓰기 동기화 개체를 대기 하는 경우 발생 합니다.| 
|SOSHOST_SEMAPHORE |CLR과 같은 호스팅된 구성 요소가 SQL Server 세마포 동기화 개체를 대기 하는 경우 발생 합니다.| 
|SOSHOST_SLEEP |일반 이벤트가 발생할 때까지 대기하는 동안 호스팅된 태스크가 중지되는 경우에 발생합니다. 호스팅된 태스크는 CLR과 같은 호스팅된 구성 요소에 사용됩니다.| 
|SOSHOST_TRACELOCK |추적 스트림에 대한 액세스 동기화 중에 발생합니다.| 
|SOSHOST_WAITFORDONE |CLR과 같은 호스팅된 구성 요소가 태스크가 완료될 때까지 대기하는 경우에 발생합니다.| 
|SP_PREEMPTIVE_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SP_SERVER_DIAGNOSTICS_BUFFER_ACCESS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SP_SERVER_DIAGNOSTICS_INIT_MUTEX |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SP_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SQLCLR_APPDOMAIN |CLR이 응용 프로그램 도메인 시작이 완료될 때까지 대기하는 동안 발생합니다.| 
|SQLCLR_ASSEMBLY |appdomain의 로드된 어셈블리 목록에 대한 액세스를 대기하는 동안 발생합니다.| 
|SQLCLR_DEADLOCK_DETECTION |CLR이 교착 상태 감지가 완료될 때까지 대기하는 동안 발생합니다.| 
|SQLCLR_QUANTUM_PUNISHMENT |CLR 태스크가 실행 퀀텀을 초과하여 조절되는 경우에 발생합니다. 이러한 조절은 리소스를 많이 사용하는 이 태스크가 다른 작업에 미치는 영향을 줄이기 위해 수행됩니다.| 
|SQLSORT_NORMMUTEX |내부 정렬 구조를 초기화하는 동안 내부 동기화 중에 발생합니다.| 
|SQLSORT_SORTMUTEX |내부 정렬 구조를 초기화하는 동안 내부 동기화 중에 발생합니다.| 
|SQLTRACE_BUFFER_FLUSH |태스크가 백그라운드 작업이 4초마다 추적 버퍼를 디스크로 플러시할 때까지 대기하는 경우에 발생합니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|SQLTRACE_FILE_BUFFER |파일 추적에서 추적 버퍼 동기화 중에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SQLTRACE_FILE_READ_IO_COMPLETION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SQLTRACE_FILE_WRITE_IO_COMPLETION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SQLTRACE_INCREMENTAL_FLUSH_SLEEP |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SQLTRACE_LOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|SQLTRACE_PENDING_BUFFER_WRITERS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SQLTRACE_SHUTDOWN |추적 종료가 처리 중인 추적 이벤트가 완료될 때까지 대기하는 동안 발생합니다.| 
|SQLTRACE_WAIT_ENTRIES |SQL 추적 이벤트 큐가 패킷이 큐에 도착할 때까지 대기하는 동안 발생합니다.| 
|SRVPROC_SHUTDOWN |종료 프로세스가 올바르게 종료하기 위해 내부 리소스가 해제될 때까지 대기하는 동안 발생합니다.| 
|STARTUP_DEPENDENCY_MANAGER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|TDS_BANDWIDTH_STATE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|TDS_INIT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|TDS_PROXY_CONTAINER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|TEMPOBJ |임시 개체 삭제가 동기화되는 경우에 발생합니다. 이 대기는 드물게 발생하며 태스크가 temp 테이블 삭제에 대한 액세스를 과도하게 요청한 경우에만 발생합니다.| 
|TEMPORAL_BACKGROUND_PROCEED_CLEANUP |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|TERMINATE_LISTENER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|THREADPOOL |태스크가 작업자가 실행될 때까지 대기하는 경우에 발생합니다. 이는 최대 작업자 설정이 너무 낮거나 해당 일괄 처리 실행이 비정상적으로 오래 수행되어 다른 일괄 처리에 사용할 수 있는 작업자 수가 감소한 것입니다.| 
|TIMEPRIV_TIMEPERIOD |확장 이벤트 타이머의 내부 동기화 중에 발생합니다.| 
|TRACE_EVTNOTIF |TBD| 
|TRACEWRITE |SQL 추적 행 집합 추적 공급자가 사용 가능한 버퍼나 이벤트를 포함한 버퍼가 처리될 때까지 대기하는 경우에 발생합니다.| 
|TRAN_MARKLATCH_DT |표시된 트랜잭션에 대한 삭제 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.| 
|TRAN_MARKLATCH_EX |표시된 트랜잭션에 대한 배타 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.| 
|TRAN_MARKLATCH_KP |표시된 트랜잭션에 대한 유지 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.| 
|TRAN_MARKLATCH_NL |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|TRAN_MARKLATCH_SH |표시된 트랜잭션에 대한 공유 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.| 
|TRAN_MARKLATCH_UP |표시된 트랜잭션에 대한 업데이트 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.| 
|TRANSACTION_MUTEX |트랜잭션에 대한 여러 일괄 처리의 액세스 동기화 중에 발생합니다.| 
|UCS_ENDPOINT_CHANGE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|UCS_MANAGER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|UCS_MEMORY_NOTIFICATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|UCS_SESSION_REGISTRATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|UCS_TRANSPORT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|UCS_TRANSPORT_STREAM_CHANGE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|UTIL_PAGE_ALLOC |트랜잭션 로그 검색이 메모리 부족 시 메모리를 사용할 수 있을 때까지 대기하는 경우에 발생합니다.| 
|VDI_CLIENT_COMPLETECOMMAND |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|VDI_CLIENT_GETCOMMAND |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|VDI_CLIENT_OPERATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|VDI_CLIENT_OTHER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|VERSIONING_COMMITTING |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|VIA_ACCEPT |시작하는 동안 VIA(Virtual Interface Adapter) 공급자 연결이 완료된 경우에 발생합니다.| 
|VIEW_DEFINITION_MUTEX |캐시된 뷰 정의에 대한 액세스 동기화 중에 발생합니다.| 
|WAIT_FOR_RESULTS |쿼리 알림이 트리거될 때까지 대기하는 경우에 발생합니다.| 
|WAIT_SCRIPTDEPLOYMENT_REQUEST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_SCRIPTDEPLOYMENT_WORKER |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XLOGREAD_SIGNAL |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_ASYNC_TX_COMPLETION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_CKPT_AGENT_WAKEUP |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_CKPT_CLOSE |검사점이 완료 될 때까지 기다리는 경우 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_CKPT_ENABLED |검사점 작성은 대기 하는 사용 되지 않는 검사점을 사용 하도록 설정 하는 경우에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_CKPT_STATE_LOCK |검사점 상태 확인을 동기화 할 때 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_COMPILE_WAIT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다.| 
|WAIT_XTP_GUEST |데이터베이스의 메모리 할당자에서 메모리 부족 알림 수신을 중지할 할 때 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_HOST_WAIT |대기 데이터베이스 엔진에 의해 트리거되는 및 호스트에서 구현 하는 경우에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_OFFLINE_CKPT_BEFORE_REDO |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_OFFLINE_CKPT_LOG_IO |오프 라인 검사점 대기는 로그 IO 완료를 읽을 경우에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_OFFLINE_CKPT_NEW_LOG |새 로그 레코드를 검색에 대 한 오프 라인 검사점 대기 경우에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_PROCEDURE_ENTRY |삭제 프로시저 대기에 대 한 모든 현재 실행 프로시저가 완료 될 경우에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_RECOVERY |데이터베이스 복구 완료 하는 메모리 액세스에 최적화 된 개체의 복구를 위해 대기 하는 경우에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_SERIAL_RECOVERY |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_SWITCH_TO_INACTIVE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_TASK_SHUTDOWN |메모리 내 oltp 네트워크 읽기가 완료 될 때까지 기다리는 경우 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_TRAN_DEPENDENCY |트랜잭션 종속성을 기다리는 경우 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAITFOR |WAITFOR TRANSACT-SQL 문으로 인해 발생합니다. 대기 시간은 문의 매개 변수에 의해 결정됩니다. 이 대기는 사용자가 시작합니다.| 
|WAITFOR_PER_QUEUE |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAITFOR_TASKSHUTDOWN |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|WAITSTAT_MUTEX |sys.dm_os_wait_stats를 채우는 데 사용되는 통계 컬렉션에 대한 액세스 동기화 중에 발생합니다.| 
|WCC |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|WINDOW_AGGREGATES_MULTIPASS |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WINFAB_API_CALL |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WINFAB_REPLICA_BUILD_OPERATION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WINFAB_REPORT_FAULT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WORKTBL_DROP |작업 테이블 삭제가 실패한 후 다시 시도하기 전에 일시 중지하는 동안 발생합니다.| 
|WRITE_COMPLETION |쓰기 작업이 진행 중인 경우에 발생합니다.| 
|WRITELOG |로그 플러시가 완료될 때까지 대기하는 동안 발생합니다. 로그 플러시를 발생시키는 일반적인 작업은 검사점과 트랜잭션 커밋입니다.| 
|XACT_OWN_TRANSACTION |트랜잭션 소유권을 획득하기 위해 대기하는 동안 발생합니다.| 
|XACT_RECLAIM_SESSION |세션의 현재 소유자가 세션 소유권을 해제할 때까지 대기하는 동안 발생합니다.| 
|XACTLOCKINFO |트랜잭션 잠금 목록에 대한 액세스 동기화 중에 발생합니다. 트랜잭션 자체 외에도 교착 상태 감지, 페이지 분할 중 잠금 마이그레이션 등의 작업이 이 잠금 목록에 액세스합니다.| 
|XACTWORKSPACE_MUTEX |트랜잭션에서 제거 및 트랜잭션 참여 멤버 간의 데이터베이스 잠금 수 동기화 중에 발생합니다.| 
|XDB_CONN_DUP_HASH |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XDES_HISTORY |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XDES_OUT_OF_ORDER_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XDES_SNAPSHOT |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XDESTSVERMGR |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XE_BUFFERMGR_ALLPROCESSED_EVENT |확장 이벤트 세션 버퍼를 대상으로 플러시할 때 발생합니다. 이 대기는 백그라운드 스레드에서 발생합니다.| 
|XE_BUFFERMGR_FREEBUF_EVENT |다음 조건 중 하나에 해당하는 경우 발생합니다.| 
|XE_CALLBACK_LIST |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XE_CX_FILE_READ |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XE_DISPATCHER_CONFIG_SESSION_LIST |비동기 대상을 사용하는 확장 이벤트 세션이 시작 또는 중지될 때 발생합니다. 이 대기는 다음 중 하나를 의미할 수 있습니다.| 
|XE_DISPATCHER_JOIN |확장 이벤트 세션에 사용되는 백그라운드 스레드가 종료되는 경우 발생합니다.| 
|XE_DISPATCHER_WAIT |확장 이벤트 세션에 사용되는 백그라운드 스레드가 이벤트 버퍼 처리를 기다리는 경우 발생합니다.| 
|XE_FILE_TARGET_TVF |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XE_LIVE_TARGET_TVF |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XE_MODULEMGR_SYNC |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|XE_OLS_LOCK |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|XE_PACKAGE_LOCK_BACKOFF |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|XE_SERVICES_EVENTMANUAL |TBD| 
|XE_SERVICES_MUTEX |TBD| 
|XE_SERVICES_RWLOCK |TBD| 
|XE_SESSION_CREATE_SYNC |TBD| 
|XE_SESSION_FLUSH |TBD| 
|XE_SESSION_SYNC |TBD| 
|XE_STM_CREATE |TBD| 
|XE_TIMER_EVENT |TBD| 
|XE_TIMER_MUTEX |TBD| 
|XE_TIMER_TASK_DONE |TBD| 
|XIO_CREDENTIAL_MGR_RWLOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XIO_CREDENTIAL_RWLOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XIO_EDS_MGR_RWLOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XIO_EDS_RWLOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XIO_IOSTATS_BLOBLIST_RWLOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XIO_IOSTATS_FCBLIST_RWLOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XIO_LEASE_RENEW_MGR_RWLOCK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTP_HOST_DB_COLLECTION |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTP_HOST_LOG_ACTIVITY |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTP_HOST_PARALLEL_RECOVERY |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTP_PREEMPTIVE_TASK |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTP_TRUNCATION_LSN |TBD <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTPPROC_CACHE_ACCESS |모든 고유 하 게 컴파일된 저장된 프로시저 캐시 개체에 액세스할 때 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTPPROC_PARTITIONED_STACK_CREATE |지정된 된 프로시저에 대 한 저장된 프로시저 캐시 구조 (단일 스레드로 수행 되어야 합니다) 컴파일된-NUMA 노드를 고유 하 게 할당 하는 경우에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|

  
 다음과 같은 Xevent를 파티션에 관련 된 **스위치** 및 온라인 인덱스 다시 작성 합니다. 구문에 대 한 정보를 참조 하세요. [ALTER table&#40; Transact SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md) 및 [ALTER index&#40; Transact SQL &#41; ](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 잠금 호환성 표를 참조 하십시오. [sys.dm_tran_locks&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).  
  
## <a name="see-also"></a>관련 항목:  
    
 [SQL Server 운영 체제 관련 동적 관리 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_session_wait_stats&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)   
 [sys.dm_db_wait_stats &#40; Azure SQL 데이터베이스 &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-wait-stats-azure-sql-database.md)  
  
  


