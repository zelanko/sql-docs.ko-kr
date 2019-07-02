---
title: sys.dm_os_wait_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/16/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_wait_stats_TSQL
- dm_os_wait_stats
- sys.dm_os_wait_stats
- sys.dm_os_wait_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_wait_stats dynamic management view
ms.assetid: 568d89ed-2c96-4795-8a0c-2f3e375081da
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d4fa43746db12f8a1ee2957e3846bf1082ff219
ms.sourcegitcommit: c0e48b643385ce19c65ca6e348ce83b2d22b6514
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492762"
---
# <a name="sysdmoswaitstats-transact-sql"></a>sys.dm_os_wait_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

실행 중인 스레드로 인해 발생한 모든 대기에 대한 정보를 반환합니다. 이 집계 뷰를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 관련된 성능 문제뿐 아니라 특정 쿼리 및 일괄 처리와 관련된 성능 문제도 진단할 수 있습니다. [sys.dm_exec_session_wait_stats &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) 세션에서와 비슷한 정보를 제공 합니다.  
  
> [!NOTE] 
> 이를 호출 하 **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 하거나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** 에 이름을 사용 하 여 **sys.dm_pdw_nodes_os_wait_stats**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar(60)**|대기 유형의 이름입니다. 자세한 내용은 [대기 유형](#WaitTypes)이 항목의 뒷부분에 나오는.|  
|waiting_tasks_count|**bigint**|이 대기 유형의 대기 수입니다. 이 카운터는 각 대기가 시작될 때 증가합니다.|  
|wait_time_ms|**bigint**|이 대기 유형의 총 대기 시간(밀리초)입니다. 이 시간은 signal_wait_time_ms를 포함합니다.|  
|max_wait_time_ms|**bigint**|이 대기 유형의 최대 대기 시간입니다.|  
|signal_wait_time_ms|**bigint**|대기 스레드가 신호를 받은 시간과 실행을 시작한 시간 사이의 차이입니다.|  
|pdw_node_id|**int**|이 배포에 있는 노드에 대 한 식별자입니다. <br/> **적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] |  
  
## <a name="permissions"></a>사용 권한

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   

##  <a name="WaitTypes"></a> 대기 유형  
 **리소스 대기** 리소스 대기를 작업자 리소스를 다른 작업 자가 사용 되는 또는 아직 사용할 수 없습니다 때문에 사용할 수 없는 리소스에 대 한 액세스를 요청 하는 경우에 발생 합니다. 리소스 대기의 예로는 잠금, 래치, 네트워크 및 디스크 I/O 대기가 있습니다. 잠금 및 래치 대기는 동기화 개체에 대한 대기입니다.  
  
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
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대기 시간 카운터 **bigint** 값 및 많지 않기 카운터가 롤오버 되기 쉽습니다 이전 버전의 동등한 카운터와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 쿼리 실행 중에 특정 유형의 대기 시간이 쿼리 내의 병목 또는 대기 지점을 나타낼 수 있습니다. 마찬가지로 높은 대기 시간이나 서버 전체의 대기 횟수가 서버 인스턴스 내의 쿼리 상호 작용에서 병목 또는 핫 스폿을 나타낼 수 있습니다. 예를 들어 잠금 대기는 쿼리의 데이터 경합을, 페이지 IO 래치 대기는 느린 IO 응답 시간을, 페이지 래치 업데이트 대기는 잘못된 파일 레이아웃을 나타냅니다.  
  
 이 동적 관리 뷰의 내용은 다음 명령을 실행하여 다시 설정할 수 있습니다.  
  
```sql  
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
|AM_INDBUILD_ALLOCATION |내부적으로만 사용됩니다. <br />**적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|AM_SCHEMAMGR_UNSHARED_CACHE |내부적으로만 사용됩니다. <br />**적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ASSEMBLY_FILTER_HASHTABLE |내부적으로만 사용됩니다. <br />**적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ASSEMBLY_LOAD |어셈블리 로드에 대한 단독 액세스 중에 발생합니다.| 
|ASYNC_DISKPOOL_LOCK |파일 만들기 또는 초기화 같은 태스크를 수행하고 있는 병렬 스레드를 동기화하려고 하는 경우에 발생합니다.| 
|ASYNC_IO_COMPLETION |태스크가 I/O가 완료될 때까지 대기하는 경우에 발생합니다.| 
|ASYNC_NETWORK_IO |태스크가 네트워크 뒤에서 차단되는 경우에 네트워크 쓰기 중에 발생합니다. 클라이언트가 서버의 데이터를 처리하고 있는지 확인합니다.| 
|ASYNC_OP_COMPLETION |내부적으로만 사용됩니다. <br />**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ASYNC_OP_CONTEXT_READ |내부적으로만 사용됩니다. <br />**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ASYNC_OP_CONTEXT_WRITE |내부적으로만 사용됩니다. <br />**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ASYNC_SOCKETDUP_IO |내부적으로만 사용됩니다. <br />**적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|AUDIT_GROUPCACHE_LOCK |특수 캐시에 대한 액세스를 제어하는 잠금을 기다리는 경우에 발생합니다. 캐시에는 각 감사 동작 그룹을 감사하는 데 사용되는 감사에 대한 정보가 포함되어 있습니다.| 
|AUDIT_LOGINCACHE_LOCK |특수 캐시에 대한 액세스를 제어하는 잠금을 기다리는 경우에 발생합니다. 캐시에는 로그인 감사 동작 그룹을 감사하는 데 사용되는 감사에 대한 정보가 포함되어 있습니다.| 
|AUDIT_ON_DEMAND_TARGET_LOCK |감사와 관련된 확장 이벤트 대상의 단일 초기화를 위한 잠금을 기다리는 경우에 발생합니다.| 
|AUDIT_XE_SESSION_MGR |감사와 관련된 확장 이벤트 세션의 시작 및 중지를 동기화하는 데 사용되는 잠금을 기다리는 경우에 발생합니다.| 
|BACKUP |태스크가 백업 처리의 일부로 차단되는 경우에 발생합니다.| 
|BACKUP_OPERATOR |태스크가 테이프 탑재를 대기하는 경우에 발생합니다. 테이프 상태를 확인 하려면 sys.dm_io_backup_tapes를 쿼리 합니다. 탑재 작업이 보류된 상태가 아니라면 이 대기 유형이 테이프 드라이브의 하드웨어 문제를 나타낼 수 있습니다.| 
|BACKUPBUFFER |백업 태스크가 데이터를 기다리거나 데이터를 저장할 버퍼를 기다리는 경우에 발생합니다. 이 유형은 태스크가 테이프 탑재를 기다리는 경우 외에는 일반적이지 않습니다.| 
|BACKUPIO |백업 태스크가 데이터를 기다리거나 데이터를 저장할 버퍼를 기다리는 경우에 발생합니다. 이 유형은 태스크가 테이프 탑재를 기다리는 경우 외에는 일반적이지 않습니다.| 
|BACKUPTHREAD |태스크가 백업 작업이 완료될 때까지 대기하는 경우에 발생합니다. 대기 시간은 몇 분에서 몇 시간까지 걸릴 수 있습니다. 대기 중인 태스크가 I/O 프로세스에 위치하면 문제가 있는 것이 아닙니다.| 
|BAD_PAGE_PROCESS |백그라운드의 주의 대상 페이지 로거가 5초보다 긴 간격으로 실행되는 것을 방지하려는 경우에 발생합니다. 주의 대상 페이지가 너무 많으면 로거가 자주 실행됩니다.| 
|BLOB_METADATA |내부적으로만 사용됩니다. <br />**적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BMPALLOCATION |일괄 처리 모드 연산자 내에서 서로 다른 처리 단계를 입력 하는 스레드 동기화 중에 발생 합니다. <br />**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BMPBUILD |일괄 처리 모드 연산자 내에서 서로 다른 처리 단계를 입력 하는 스레드 동기화 중에 발생 합니다. <br />**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BMPREPARTITION |일괄 처리 모드 연산자 내에서 서로 다른 처리 단계를 입력 하는 스레드 동기화 중에 발생 합니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BMPREPLICATION |일괄 처리 모드 연산자 내에서 서로 다른 처리 단계를 입력 하는 스레드 동기화 중에 발생 합니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BPSORT |일괄 처리 모드 연산자 내에서 서로 다른 처리 단계를 입력 하는 스레드 동기화 중에 발생 합니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_CONNECTION_RECEIVE_TASK |연결 엔드포인트에서 메시지를 받기 위한 액세스를 대기하는 경우에 발생합니다. 엔드포인트에 대한 수신 액세스는 직렬화됩니다.| 
|BROKER_DISPATCHER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_ENDPOINT_STATE_MUTEX |Service Broker 연결 끝점의 상태에 액세스 하려는 경합이 있을 때 발생 합니다. 변경 내용의 상태에 대한 액세스는 직렬화됩니다.| 
|BROKER_EVENTHANDLER |태스크가 대기 하는 Service broker 주 이벤트 처리기에서 때 발생 합니다. 매우 짧게 발생해야 합니다.| 
|BROKER_FORWARDER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_INIT |각 활성 데이터베이스에서 Service Broker를 초기화할 때 발생 합니다. 자주 발생하면 안 됩니다.| 
|BROKER_MASTERSTART |작업을 시작 하려면 Service Broker 주 이벤트 처리기를 대기할 때 발생 합니다. 매우 짧게 발생해야 합니다.| 
|BROKER_RECEIVE_WAITFOR |RECEIVE WAITFOR가 대기 중인 경우에 발생합니다. 이 메시지가 큐에 받을 준비가 또는 잠금 경합이 큐에서 메시지 수신을 방지는 것일 수 있습니다.| 
|BROKER_REGISTERALLENDPOINTS |Service Broker 연결 끝점을 초기화 하는 동안 발생합니다. 매우 짧게 발생해야 합니다.| 
|BROKER_SERVICE |대상 서비스와 연결 된 Service Broker 대상 목록이 업데이트 되거나 우선 순위가 다시 매겨지는 경우 발생 합니다.| 
|BROKER_SHUTDOWN |Service Broker의 계획 된 종료를 때 발생 합니다. 가능하면 매우 짧게 발생해야 합니다.| 
|BROKER_START |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_TASK_SHUTDOWN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_TASK_STOP |Service Broker 큐 태스크 처리기가 태스크를 종료 하려고 할 때 발생 합니다. 상태 검사가 직렬화되고 먼저 실행 상태에 있어야 합니다.| 
|BROKER_TASK_SUBMIT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_TO_FLUSH |Service Broker 지연 flusher 플러시 메모리 내 전송 개체 작업 테이블을 때 발생 합니다.| 
|BROKER_TRANSMISSION_OBJECT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_TRANSMISSION_TABLE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_TRANSMISSION_WORK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|BROKER_TRANSMITTER |Service Broker 전송 기가 작업을 대기할 때 발생 합니다. Service Broker에 하나 이상의 연결 끝점을 통해 네트워크를 통해 전송 될 여러 대화 상자에서 메시지를 예약 하는 전송기 라는 구성 요소가 있습니다. 전송기의이 목적을 위해 2 전용된 스레드가 있습니다. 이 대기 유형은 대화 메시지를 보낼 수 있도록 이러한 전송기 스레드가 대기 하는 경우 청구는 전송 연결을 사용 하 여 합니다. 이 대기 유형의 waiting_tasks_count의 값이 높으면 가리키고 이러한 전송기 스레드가 일시적인 작업 하 고 모든 성능 문제의 징후가 않습니다. Service broker를 전혀 사용 하지 않으면, waiting_tasks_count 2 (2 전송기 스레드) 해야 합니다. 및 wait_time_ms 인스턴스가 시작 된 이후 기간에 두 번 이어야 합니다. 참조 [Service broker 대기 통계](https://blogs.msdn.microsoft.com/sql_service_broker/2008/12/01/service-broker-wait-types)합니다.|
|BUILTIN_HASHKEY_MUTEX |내부 데이터 구조를 초기화하는 동안 인스턴스 시작 후 발생할 수 있습니다. 데이터 구조가 초기화되면 되풀이되지 않습니다.| 
|CHANGE_TRACKING_WAITFORCHANGES |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CHECK_PRINT_RECORD |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|CHECK_SCANNER_MUTEX |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CHECK_TABLES_INITIALIZATION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CHECK_TABLES_SINGLE_SCAN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CHECK_TABLES_THREAD_BARRIER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
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
|CMEMPARTITIONED |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CMEMTHREAD |태스크가 스레드로부터 안전한 메모리 개체를 기다리는 경우에 발생합니다. 여러 태스크가 같은 메모리 개체의 메모리를 할당하려고 하여 경합이 발생할 때 대기 시간이 증가할 수 있습니다.| 
|COLUMNSTORE_BUILD_THROTTLE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|COLUMNSTORE_COLUMNDATASET_SESSION_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|COMMIT_TABLE |내부적으로만 사용됩니다.| 
|CONNECTION_ENDPOINT_LOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|COUNTRECOVERYMGR |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CREATE_DATINISERVICE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|CXCONSUMER |병렬 쿼리 계획을 사용 하 여 행을 보낼 생산자 스레드와 소비자 스레드가 대기 하는 경우 발생 합니다. 이 병렬 쿼리 실행의 정상적인 일부입니다. <br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|
|CXPACKET |병렬 쿼리 계획을 사용 하 여 생성 하 고 행을 사용 하는 경우 및 쿼리 프로세서 교환 반복기를 동기화 할 때 발생 합니다. 대기 시간이 너무 길고 쿼리 튜닝(예: 인덱스 추가)으로 시간을 줄일 수 없는 경우에는 병렬 처리 비용 임계값을 조정하거나 병렬 처리 수준을 낮추세요.<br /> **참고:** 부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], CXPACKET 쿼리 프로세서 교환 반복기를 동기화 및 소비자 스레드는 행을 생성 하는 데만 참조 합니다. 소비자 스레드는 CXCONSUMER 대기 형식에 개별적으로 추적 됩니다.| 
|CXROWSET_SYNC |병렬 범위 검색 중에 발생합니다.| 
|DAC_INIT |관리자 전용 연결이 초기화되는 동안 발생합니다.| 
|DBCC_SCALE_OUT_EXPR_CACHE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DBMIRROR_DBM_EVENT |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|DBMIRROR_DBM_MUTEX |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|DBMIRROR_EVENTS_QUEUE |데이터베이스 미러링이 이벤트가 처리될 때까지 대기하는 경우에 발생합니다.| 
|DBMIRROR_SEND |태스크가 네트워크 계층의 통신 백로그가 지워져서 메시지를 보낼 수 있을 때까지 대기하는 경우에 발생합니다. 통신 계층의 로드가 많아져 데이터베이스 미러링 데이터 처리량에 영향을 미치기 시작했음을 나타냅니다.| 
|DBMIRROR_WORKER_QUEUE |데이터베이스 미러링 작업자 태스크가 추가 작업을 대기하는 경우를 나타냅니다.| 
|DBMIRRORING_CMD |태스크가 로그 레코드가 디스크로 플러시될 때까지 대기하는 경우에 발생합니다. 이 대기 상태는 오랜 시간 동안 유지됩니다.| 
|DBSEEDING_FLOWCONTROL |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DBSEEDING_OPERATION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DEADLOCK_ENUM_MUTEX |교착 상태 모니터와 sys.dm_os_waiting_tasks가 SQL Server가 동시에 여러 개의 교착 상태 검색을 실행 하지 않도록 하려고 하는 경우 발생 합니다.| 
|DEADLOCK_TASK_SEARCH |이 리소스의 대기 시간이 길면 서버가 sys.dm_os_waiting_tasks 위에서 쿼리를 실행하고 있으며 이러한 쿼리가 교착 상태 모니터의 교착 상태 검색을 차단하고 있음을 나타냅니다. 이 대기 유형은 교착 상태 모니터에만 사용됩니다. sys.dm_os_waiting_tasks 위의 쿼리는 DEADLOCK_ENUM_MUTEX를 사용합니다.| 
|DEBUG |TRANSACT-SQL 및 CLR 내부 동기화에 대 한 디버깅 중에 발생 합니다.| 
|DIRECTLOGCONSUMER_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DIRTY_PAGE_POLL |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DIRTY_PAGE_SYNC |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DIRTY_PAGE_TABLE_LOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DISABLE_VERSIONING |SQL Server 버전 트랜잭션 관리자 가장 오래 된 활성 트랜잭션의 타임 스탬프 상태 변경 시작 될 때의 타임 스탬프 보다 이후 인지를 폴링할 때 발생 합니다. 이 경우 ALTER DATABASE 문이 실행되기 전에 시작된 모든 스냅숏 트랜잭션은 완료되었습니다. 이 대기 상태는 ALTER DATABASE 문을 사용 하 여 SQL Server 버전 관리를 해제 하는 경우에 사용 됩니다.| 
|DISKIO_SUSPEND |외부 백업이 활성 상태일 때 태스크가 파일에 액세스하려고 대기하는 경우에 발생합니다. 대기 중인 모든 사용자 프로세스에 대해 보고됩니다. 사용자 프로세스당 값이 5보다 크면 외부 백업을 완료하는 데 걸리는 시간이 너무 긴 것일 수 있습니다.| 
|DISPATCHER_PRIORITY_QUEUE_SEMAPHORE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DISPATCHER_QUEUE_SEMAPHORE |디스패처 풀의 스레드가 처리할 추가 작업을 기다리는 경우에 발생합니다. 이 대기 유형의 대기 시간은 디스패처가 유휴 상태일 때 증가됩니다.| 
|DLL_LOADING_MUTEX |XML 파서 DLL이 로드될 때까지 대기하는 동안 한 번 발생합니다.| 
|DPT_ENTRY_LOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DROP_DATABASE_TIMER_TASK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DROPTEMP |이전 시도가 실패한 경우 임시 개체 삭제를 다시 시도하기 전에 발생합니다. 삭제 시도가 실패할 때마다 대기 시간이 기하급수적으로 증가합니다.| 
|DTC |태스크가 상태 전환 관리에 사용되는 이벤트를 기다리는 경우에 발생합니다. SQL Server MS DTC 서비스를 사용할 수 있는지 알림을 받으면 Microsoft Distributed Transaction Coordinator (MS DTC) 트랜잭션의 복구가 발생할 때이 상태 제어 합니다.| 
|DTC_ABORT_REQUEST |MS DTC 작업자 세션이 MS DTC 트랜잭션의 소유권을 획득하려고 대기하는 경우에 MS DTC 작업자 세션에서 발생합니다. MS DTC가 트랜잭션의 소유권을 획득한 후에는 세션이 트랜잭션을 롤백할 수 있습니다. 일반적으로 세션은 트랜잭션을 사용하고 있는 다른 세션을 기다립니다.| 
|DTC_RESOLVE |복구 태스크가 트랜잭션의 결과물을 쿼리할 수 있도록 데이터베이스 간 트랜잭션에서 master 데이터베이스를 대기하는 경우에 발생합니다.| 
|DTC_STATE |태스크가 내부 MS DTC 전역 상태 개체의 변경을 방지하는 이벤트를 기다리는 경우에 발생합니다. 이 상태는 매우 짧은 시간 동안 유지되어야 합니다.| 
|DTC_TMDOWN_REQUEST |SQL Server에서 MS DTC 서비스를 사용할 수 없는 알림을 수신 하는 경우 MS DTC 작업자 세션에서 발생 합니다. 먼저 작업자는 MS DTC 복구 프로세스가 시작될 때까지 기다렸다가 작업자가 작업하고 있는 분산 트랜잭션의 결과물을 획득하기 위해 대기합니다. 이것은 MS DTC 서비스와의 연결이 다시 설정될 때까지 계속될 수 있습니다.| 
|DTC_WAITFOR_OUTCOME |복구 태스크가 MS DTC가 활성화되어 준비된 트랜잭션을 해결할 수 있을 때까지 대기하는 경우에 발생합니다.| 
|DTCNEW_ENLIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DTCNEW_PREPARE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DTCNEW_RECOVERY |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DTCNEW_TM |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DTCNEW_TRANSACTION_ENLISTMENT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DTCPNTSYNC |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|DUMP_LOG_COORDINATOR |주 태스크가 하위 작업이 데이터를 생성할 때까지 대기하는 경우에 발생합니다. 일반적으로 이 상태는 발생하지 않습니다. 대기 시간이 길면 예상하지 못했던 차단이 발생한 것일 수 있으므로 하위 태스크를 조사해야 합니다.| 
|DUMP_LOG_COORDINATOR_QUEUE |내부적으로만 사용됩니다.| 
|DUMPTRIGGER |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|EC |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|EE_PMOLOCK |문 실행 중 특정 유형의 메모리 할당을 동기화하는 경우에 발생합니다.| 
|EE_SPECPROC_MAP_INIT |내부 프로시저 해시 테이블 생성을 동기화하는 경우에 발생합니다. 이 대기만 SQL Server 인스턴스가 시작 된 후 해시 테이블의 초기 액세스 하는 동안 발생할 수 있습니다.| 
|ENABLE_EMPTY_VERSIONING |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ENABLE_VERSIONING |SQL Server 데이터베이스를 스냅숏 격리 허용 상태로 전환할 준비가 선언 하기 전에 완료 하도록이 데이터베이스의 모든 업데이트 트랜잭션이 대기할 때 발생 합니다. 이 상태는 SQL Server는 ALTER DATABASE 문을 사용 하 여 스냅숏 격리를 활성화 하는 경우에 사용 됩니다.| 
|ERROR_REPORTING_MANAGER |여러 개의 동시 오류 로그 초기화를 동기화하는 경우에 발생합니다.| 
|EXCHANGE |병렬 쿼리 중 쿼리 프로세서 교환 반복기에서 동기화 중에 발생합니다.| 
|EXECSYNC |병렬 쿼리 중 쿼리 프로세서 교환 반복기와 관련되지 않은 영역에서 동기화 중에 발생합니다. 이러한 영역의 예에는 비트맵, LOB(Large Binary Object) 및 스풀 반복기가 있습니다. LOB는 이 대기 상태를 자주 사용할 수 있습니다.| 
|EXECUTION_PIPE_EVENT_INTERNAL |연결 컨텍스트를 통해 전송되는 일괄 처리 실행의 제작자 부분과 소비자 부분 동기화 중에 발생합니다.| 
|EXTERNAL_RG_UPDATE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|EXTERNAL_SCRIPT_NETWORK_IO |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 현재 통해.| 
|EXTERNAL_SCRIPT_PREPARE_SERVICE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|EXTERNAL_SCRIPT_SHUTDOWN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|EXTERNAL_WAIT_ON_LAUNCHER, |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FABRIC_HADR_TRANSPORT_CONNECTION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FABRIC_REPLICA_CONTROLLER_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FABRIC_REPLICA_CONTROLLER_STATE_AND_CONFIG |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FABRIC_REPLICA_PUBLISHER_EVENT_PUBLISH |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FABRIC_REPLICA_PUBLISHER_SUBSCRIBER_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FABRIC_WAIT_FOR_BUILD_REPLICA_EVENT_PROCESSING |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FAILPOINT |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|FCB_REPLICA_READ |스냅숏이나 DBCC에서 만든 임시 스냅숏 스파스 파일의 읽기가 동기화되는 경우에 발생합니다.| 
|FCB_REPLICA_WRITE |스냅숏이나 DBCC에서 만든 임시 스냅숏 스파스 파일에 대한 페이지 밀어넣기 또는 끌어오기가 동기화되는 경우에 발생합니다.| 
|FEATURE_SWITCHES_UPDATE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_DB_KILL_FLAG |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_DB_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_FCB |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_FCB_FIND |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_FCB_PARENT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_FCB_RELEASE_CACHED_ENTRIES |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_FCB_STATE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_FILEOBJECT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NSO_TABLE_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_NTFS_STORE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_RECOVERY |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_RSFX_COMM |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_RSFX_WAIT_FOR_MEMORY |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_STARTUP_SHUTDOWN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_STORE_DB |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_STORE_ROWSET_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FFT_STORE_TABLE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILE_VALIDATION_THREADS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILESTREAM_CACHE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILESTREAM_CHUNKER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILESTREAM_CHUNKER_INIT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILESTREAM_FCB |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILESTREAM_FILE_OBJECT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILESTREAM_WORKITEM_QUEUE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FILETABLE_SHUTDOWN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FOREIGN_REDO |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 현재 통해.| 
|FORWARDER_TRANSITION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
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
|FT_MASTER_MERGE_COORDINATOR |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FT_METADATA_MUTEX |정보를 제공하기 위해서만 문서화됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|FT_PROPERTYLIST_CACHE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|FT_RESTART_CRAWL |임시 오류로부터 복구하기 위해 마지막으로 알려진 양호 지점부터 전체 텍스트 탐색을 다시 시작해야 하는 경우에 발생합니다. 이 대기를 사용하면 해당 채우기에서 현재 작동 중인 작업자 태스크가 현재 단계를 완료하거나 종료할 수 있습니다.| 
|FULLTEXT GATHERER |전체 텍스트 작업을 동기화하는 경우에 발생합니다.| 
|GDMA_GET_RESOURCE_OWNER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GHOSTCLEANUP_UPDATE_STATS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GHOSTCLEANUPSYNCMGR |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GLOBAL_QUERY_CANCEL |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GLOBAL_QUERY_CLOSE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GLOBAL_QUERY_CONSUMER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GLOBAL_QUERY_PRODUCER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GLOBAL_TRAN_CREATE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GLOBAL_TRAN_UCS_SESSION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|GUARDIAN |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|HADR_AG_MUTEX |Always On DDL 문 또는 Windows Server 장애 조치 클러스터링 명령이 가용성 그룹의 구성에 대 한 단독 읽기/쓰기 액세스를 대기할 때 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_AR_CRITICAL_SECTION_ENTRY |Always On DDL 문 또는 Windows Server 장애 조치 클러스터링 명령이 연결된 된 가용성 그룹의 로컬 복제본의 런타임 상태에 대 한 단독 읽기/쓰기 액세스를 대기할 때 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_AR_MANAGER_MUTEX |가용성 복제본 셧다운이 시작될 때까지 기다리고 있거나 가용성 복제본 시작이 종료될 때까지 기다리는 경우에 발생합니다. 내부 에서만 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_AR_UNLOAD_COMPLETED |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_ARCONTROLLER_NOTIFICATIONS_SUBSCRIBER_LIST |상태 변경 또는 구성 변경 등의 가용성 복제본 이벤트에 대한 게시자가 이벤트 구독자 목록에 대한 단독 읽기/쓰기 액세스를 기다리고 있습니다. 내부 에서만 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_BACKUP_BULK_LOCK |Always On 주 데이터베이스는 보조 데이터베이스에서 백업 요청을 수신 하 고 배경에 대 한 대기 스레드를 획득 하거나 BulkOp 잠금 해제에 요청을 처리 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_BACKUP_QUEUE |Always On 주 데이터베이스의 백업 백그라운드 스레드가 보조 데이터베이스에서 새 작업 요청을 기다리고 있습니다. (일반적으로이 경우 주 데이터베이스 BulkOp 로그를 보유 하 고 주 데이터베이스 잠금을 해제할 수 있는지를 나타내기 위해 보조 데이터베이스에 대 한 대기)., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_CLUSAPI_CALL |SQL Server 스레드가 Windows Server 장애 조치 클러스터링 Api를 호출 하기 위해 선점형 모드로 (운영 체제에서 예약 된) (SQL Server에서 예약 된) 비선점형 모드에서 전환 되기를 기다리고 있습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_COMPRESSED_CACHE_SYNC |여러 보조 데이터베이스에 전송 된 로그 블록의 중복 압축을 방지 하는 데 사용 되는 압축 된 로그 블록 캐시에 대 한 액세스를 기다리고 있습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_CONNECTIVITY_INFO |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DATABASE_FLOW_CONTROL |대기 중인 메시지의 최대 수에 도달했을 때 파트너에게 메시지가 전송될 때까지 기다립니다. 로그 검색이 네트워크 전송보다 빠르게 실행 되고 있음을 나타냅니다. 네트워크 전송이 예상 보다 오래 걸릴 경우에이 문제가., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DATABASE_VERSIONING_STATE |Always On 보조 데이터베이스의 버전 관리 상태 변경 시 발생합니다. 이 대기는 내부 데이터 구조 이며 일반적으로 데이터 액세스에 직접적인 영향을 주지를 사용 하 여 매우 짧습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DATABASE_WAIT_FOR_RECOVERY |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DATABASE_WAIT_FOR_RESTART |데이터베이스가 Always On 가용성 그룹 제어에서 다시 시작 될 때까지 기다리고 있습니다. 정상 조건에서는이 아니므로 고객 문제를 여기서 시점에 대기가 예상., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING |읽기 가능한 보조 데이터베이스에서 Always On 가용성 그룹 커밋 또는 롤백 진행 중이 던 읽기 워크 로드에 대 한 보조 복제본이 활성화 될 때 모든 트랜잭션의 대기 하는 동안 행 버전 관리에서 차단 되는 개체에 대 한 쿼리 합니다. 이 대기 유형을 사용 하면 행 버전을 스냅숏 격리에서 쿼리를 실행 하기 전에 사용할 수 있습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DB_COMMAND |대화형 메시지 (Always On 대화 메시지 인프라를 사용 하 여, 다른 쪽의 명시적 응답이 필요 함)에 대 한 응답을 기다리는 중입니다. 다양 한 다른 메시지 유형은이 대기 유형을 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DB_OP_COMPLETION_SYNC |대화형 메시지 (Always On 대화 메시지 인프라를 사용 하 여, 다른 쪽의 명시적 응답이 필요 함)에 대 한 응답을 기다리는 중입니다. 다양 한 다른 메시지 유형은이 대기 유형을 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DB_OP_START_SYNC |Always On DDL 문 또는 Windows Server 장애 조치 클러스터링 명령이 가용성 데이터베이스 및 해당 런타임 상태에 대 한 직렬화 된 액세스에 대 한 기다리고., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DBR_SUBSCRIBER |상태 변경 또는 구성 변경 등의 가용성 복제본 이벤트에 대한 게시자가 가용성 데이터베이스에 해당하는 이벤트 구독자의 런타임 상태에 대한 단독 읽기/쓰기 액세스를 기다리고 있습니다. 내부 에서만 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DBR_SUBSCRIBER_FILTER_LIST |상태 변경 또는 구성 변경 등의 가용성 복제본 이벤트에 대한 게시자가 가용성 데이터베이스에 해당하는 이벤트 구독자 목록에 대한 단독 읽기/쓰기 액세스를 기다리고 있습니다. 내부 에서만 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DBSEEDING |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DBSEEDING_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_DBSTATECHANGE_SYNC |데이터베이스 복제본의 내부 상태를 업데이트 하는 것에 대 한 동시성 제어 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FABRIC_CALLBACK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_BLOCK_FLUSH |항상 FILESTREAM 전송 관리자가 로그 블록의 처리가 완료 될 때까지 기다립니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_FILE_CLOSE |항상 FILESTREAM 전송 관리자가 다음 FILESTREAM 파일이 처리 되 고 해당 핸들이 닫힐 때까지 기다립니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_FILE_REQUEST |Always On 보조 복제본이 주 복제본이 모든 요청 된 FILESTREAM 전송 기다리고 실행 취소 하는 동안 파일., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_IOMGR |항상 FILESTREAM 전송 관리자를 시작 또는 종료 하는 동안 FILESTREAM 항상에서 I/O 관리자를 보호 하는 R/W 잠금을 기다리고., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_IOMGR_IOCOMPLETION |FILESTREAM 항상에서 I/O 관리자가 I/O 완료 될 때까지 기다리고 있습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_MANAGER |항상 FILESTREAM 전송 관리자를 시작 또는 종료 중에 항상 FILESTREAM 전송 관리자를 보호 하는 R/W 잠금을 기다리고., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_FILESTREAM_PREPROC |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_GROUP_COMMIT |트랜잭션 커밋 처리가 단일 로그 블록에 여러 커밋 로그 레코드를 넣을 수 있도록 그룹 커밋이 허용될 때까지 기다리고 있습니다. 이 대기는 로그 I/O를 최적화 하는 필요한 조건, 캡처 및 송신 작업., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_LOGCAPTURE_SYNC |검색을 만들거나 삭제할 때 로그 캡처 또는 적용 개체와 관련된 동시성 제어입니다. 이 경우 예상 되는 대기 상태 또는 연결 상태를 변경 하는 파트너., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_LOGCAPTURE_WAIT |로그 레코드를 사용할 수 있을 때까지 기다립니다. 연결을 통해 새 레코드가 생성될 때까지 또는 캐시에 없는 로그를 읽을 때 I/O가 완료될 때까지 기다리는 경우에 발생할 수 있습니다. 로그 검색을 로그의 끝에 잡힐 이거나 디스크에서 읽는 경우 예상 되는 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_LOGPROGRESS_SYNC |데이터베이스 복제본의 로그 진행률 상태를 업데이트 하는 경우 동시성 제어 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_NOTIFICATION_DEQUEUE |Windows Server 장애 조치(Failover) 클러스터링 알림을 처리하는 백그라운드 태스크가 다음 알림을 기다리고 있습니다. 내부 에서만 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_NOTIFICATION_WORKER_EXCLUSIVE_ACCESS |Always On 가용성 복제본 관리자가 Windows Server 장애 조치 클러스터링 알림을 처리 하는 백그라운드 작업의 런타임 상태에 대 한 직렬화 된 액세스를 기다리고 있습니다. 내부 에서만 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_NOTIFICATION_WORKER_STARTUP_SYNC |백그라운드 태스크가 Windows Server 장애 조치(Failover) 클러스터링 알림을 처리하는 백그라운드 태스크가 시작될 때까지 기다리고 있습니다. 내부 에서만 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_NOTIFICATION_WORKER_TERMINATION_SYNC |백그라운드 태스크가 Windows Server 장애 조치(Failover) 클러스터링 알림을 처리하는 백그라운드 태스크가 종료될 때까지 기다리고 있습니다. 내부 에서만 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_PARTNER_SYNC |파트너 목록에 대 한 동시성 제어 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_READ_ALL_NETWORKS |WSFC 네트워크 목록에 대한 읽기 또는 쓰기 액세스를 얻기 위해 기다립니다. 내부적으로만 사용됩니다. 참고: 동적 관리 뷰 (예: sys.dm_hadr_cluster_networks)에서 사용 되는 WSFC 네트워크 목록을 유지 하는 엔진 또는 항상에서 TRANSACT-SQL 유효성을 검사 하려면 WSFC를 참조 하는 문이 네트워크 정보입니다. 이 목록은 엔진 시작 시 업데이트 되 면 WSFC 관련 알림 및 내부 Alwayson 다시 시작 (예를 들어, 손실 및 WSFC 쿼럼을 다시 얻기). 해당 목록에서 업데이트가 진행 중일 때는 일반적으로 태스크가 차단됩니다. , <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_RECOVERY_WAIT_FOR_CONNECTION |복구를 실행하기 전에 보조 데이터베이스가 주 데이터베이스에 연결될 때까지 기다립니다. 이 주 복제본에 대 한 연결이 느린 경우 길게 할 수는 예상 되는 대기,., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_RECOVERY_WAIT_FOR_UNDO |데이터베이스 복구가 보조 데이터베이스에서 주 데이터베이스와의 공통 로그 지점으로 다시 설정하기 위해 되돌리기 및 초기화 단계를 완료할 때까지 기다립니다. 장애 조치 후 예상 되는 대기입니다. 실행 취소 Windows 시스템 모니터 (perfmon.exe) 및 동적 관리 뷰를 통해 진행률을 추적할 수 있습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_REPLICAINFO_SYNC |현재 복제본 상태를 업데이트 하는 동시성 제어 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SEEDING_CANCELLATION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SEEDING_FILE_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SEEDING_LIMIT_BACKUPS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SEEDING_SYNC_COMPLETION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SEEDING_TIMEOUT_TASK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SEEDING_WAIT_FOR_COMPLETION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SYNC_COMMIT |동기화된 보조 데이터베이스에 대한 트랜잭션 커밋 처리를 통해 로그가 확정될 때까지 기다립니다. 이 대기는 트랜잭션 지연 성능 카운터에 의해서도 반영됩니다. 가용성 그룹 및 전송, 쓰기 및 보조 데이터베이스에 로그를 확인 하려면 시간을 나타냅니다.이 대기 유형은 동기화를 예상 됩니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_SYNCHRONIZING_THROTTLE |트랜잭션 커밋 처리 시 동기화 중인 보조 데이터베이스를 동기화된 상태로 전환하기 위해 주 로그 끝을 따라잡을 수 있도록 허용될 때까지 기다립니다. 보조 데이터베이스는 캐치 업 하는 경우 예상 되는 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_TDS_LISTENER_SYNC |내부 Alwayson 시스템 또는 WSFC 클러스터는 수신기의 시작 또는 중지를 요청 합니다. 이 요청의 처리는 항상 비동기이며 중복 요청을 제거하는 메커니즘이 있습니다. 또한 구성 변경으로 인해 이 프로세스가 일시 중단 되는 순간이 있습니다. 이 수신기 동기화 메커니즘과 관련된 모든 대기는 이 대기 유형을 사용합니다. 내부 에서만 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_TDS_LISTENER_SYNC_PROCESSING |시작 하거나 가용성 그룹 수신기를 중지 해야 하는 항상에서 TRANSACT-SQL 문의 끝에 사용 합니다. 시작/중지 작업이 비동기적으로 완료 된 후 사용자 스레드 수신기의 상황이 알려지지 될 때까지이 대기 유형을 사용 하 여 차단 됩니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_THROTTLE_LOG_RATE_GOVERNOR |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_THROTTLE_LOG_RATE_MISMATCHED_SLO | 지역 복제 보조 lower를 사용 하 여 구성 된 경우 주 데이터베이스 보다 (낮은 SLO) 크기를 계산 합니다. 주 데이터베이스는 보조 복제본에서 지연 된 로그 사용으로 인해 제한 됩니다. 이 주 데이터베이스의 변경 속도를 따라갈 수 부족 하 여 계산 용량을 보유 하면 보조 데이터베이스에서 발생 합니다. <br /> **적용 대상**: Azure SQL 데이터베이스| 
|HADR_THROTTLE_LOG_RATE_LOG_SIZE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_THROTTLE_LOG_RATE_SEEDING |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_THROTTLE_LOG_RATE_SEND_RECV_QUEUE_SIZE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_TIMER_TASK |타이머 태스크 개체에 대한 잠금을 가져올 때까지 기다리며, 작업이 수행되는 시간 사이의 실제 대기에도 사용됩니다. 예를 들어, 하나의 실행 후 10 초 마다 실행 되는 작업에 대 한 Always On 가용성 그룹에 대 한 10 초 동안 기다리면 작업을 다시 예약 하 하 고 여기에 포함 되어 대기 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_TRANSPORT_DBRLIST |전송 계층의 데이터베이스 복제본 목록에 대한 액세스를 기다립니다. 액세스 권한을 부여 하는 spinlock에 사용 되는., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_TRANSPORT_FLOW_CONTROL |처리 중인 승인 되지 않은 Always On 메시지의 수를을 위로 가져갈 때 대기 플로 제어 임계값입니다. (데이터베이스-기준)에 없는 가용성 복제본-기준입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_TRANSPORT_SESSION |Always On 가용성 그룹을 변경 하거나 기본 전송 상태에 액세스 하는 동안 대기 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_WORK_POOL |Always On 가용성 그룹 백그라운드 작업 태스크 개체의 동시성 제어 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_WORK_QUEUE |Always On 가용성 그룹 백그라운드 작업자 스레드 대기 할당할 새 작업입니다. 준비 작업 자가 정상 상태가 새 작업을 대기 하는 경우 예상 되는 대기입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HADR_XRF_STACK_ACCESS |에 액세스 (조회, 추가 및 삭제)는 Always On 가용성 데이터베이스에 대 한 확장 된 복구 분기 지점 스택에., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HCCO_CACHE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HK_RESTORE_FILEMAP |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HKCS_PARALLEL_MIGRATION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HKCS_PARALLEL_RECOVERY |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HTBUILD |일괄 처리 모드 연산자 내에서 서로 다른 처리 단계를 입력 하는 스레드 동기화 중에 발생 합니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HTDELETE |일괄 처리 모드 연산자 내에서 서로 다른 처리 단계를 입력 하는 스레드 동기화 중에 발생 합니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HTMEMO |일괄 처리 모드 연산자 내에서 서로 다른 처리 단계를 입력 하는 스레드 동기화 중에 발생 합니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HTREINIT |일괄 처리 모드 연산자 내에서 서로 다른 처리 단계를 입력 하는 스레드 동기화 중에 발생 합니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HTREPARTITION |일괄 처리 모드 연산자 내에서 서로 다른 처리 단계를 입력 하는 스레드 동기화 중에 발생 합니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|HTTP_ENUMERATION |시스템 시작 시에 HTTP를 시작할 HTTP 엔드포인트를 열거하기 위해 발생합니다.| 
|HTTP_START |연결이 HTTP 초기화가 완료될 때까지 대기하는 경우에 발생합니다.| 
|HTTP_STORAGE_CONNECTION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|IMPPROV_IOWAIT |SQL Server 대량 로드 I/O가 완료를 대기할 때 발생 합니다.| 
|INSTANCE_LOG_RATE_GOVERNOR |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|INTERNAL_TESTING |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|IO_AUDIT_MUTEX |추적 이벤트 버퍼 동기화 중에 발생합니다.| 
|IO_COMPLETION |I/O 작업이 완료될 때까지 대기하는 동안 발생합니다. 이 대기 유형은 일반적으로 비데이터 페이지 I/O를 나타냅니다. 데이터 페이지 I/O 완료 대기 표시 PAGEIOLATCH\_ \* 될 때까지 대기 합니다.| 
|IO_QUEUE_LIMIT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|IO_RETRY |리소스 부족으로 인해 읽기 또는 쓰기와 같은 디스크 I/O 작업이 실패하여 다시 시도되는 경우에 발생합니다.| 
|IOAFF_RANGE_QUEUE |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|KSOURCE_WAKEUP |서비스 제어 관리자의 요청을 대기하는 동안 서비스 제어 태스크에 사용됩니다. 긴 대기가 예상되며 문제가 있는 것은 아닙니다.| 
|KTM_ENLISTMENT |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|KTM_RECOVERY_MANAGER |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|KTM_RECOVERY_RESOLUTION |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|LATCH_DT |DT(삭제) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. 래치 목록을\_ \* 대기 sys.dm_os_latch_stats에서 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.| 
|LATCH_EX |EX(배타) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. 래치 목록을\_ \* 대기 sys.dm_os_latch_stats에서 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.| 
|LATCH_KP |KP(유지) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. 래치 목록을\_ \* 대기 sys.dm_os_latch_stats에서 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.| 
|LATCH_NL |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|LATCH_SH |SH(공유) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. 래치 목록을\_ \* 대기 sys.dm_os_latch_stats에서 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.| 
|LATCH_UP |UP(업데이트) 래치를 대기하는 경우에 발생합니다. 버퍼 래치 또는 트랜잭션 표시 래치를 포함하지 않습니다. 래치 목록을\_ \* 대기 sys.dm_os_latch_stats에서 사용할 수 있습니다. sys.dm_os_latch_stats는 LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX 및 LATCH_DT 대기를 그룹화합니다.| 
|LAZYWRITER_SLEEP |지연 기록기 태스크가 일시 중지 되 면 발생 합니다. 대기 중인 백그라운드 태스크에서 사용한 시간을 측정한 것입니다. 사용자 대기를 찾을 때 이 상태는 고려하지 마세요.| 
|LCK_M_BU |태스크가 대량 업데이트(BU) 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_BU_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 대량 업데이트(BU) 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_BU_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 대량 업데이트(BU) 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_IS |태스크가 내재된 공유(IS) 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_IS_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 내재된 공유(IS) 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_IS_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 내재된 공유(IS) 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_IU |태스크가 의도 업데이트(IU) 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_IU_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 의도 업데이트(IU) 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_IU_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 의도 업데이트(IU) 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_IX |태스크가 의도 배타(IX) 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_IX_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 의도 배타(IX) 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_IX_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 의도 배타(IX) 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_NL |태스크가 현재 키 값의 NULL 잠금 및 현재 키와 이전 키 간의 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 키의 NULL 잠금은 즉시 해제 잠금입니다.| 
|LCK_M_RIn_NL_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 NULL 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 키의 NULL 잠금은 즉시 해제 잠금입니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_NL_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 NULL 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. 키의 NULL 잠금은 즉시 해제 잠금입니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_S |태스크가 현재 키 값의 공유 잠금 및 현재 키와 이전 키 간의 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RIn_S_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 공유 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_S_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 공유 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_U |태스크가 현재 키 값의 업데이트 잠금 및 현재 키와 이전 키 간의 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RIn_U_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 업데이트 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 삽입 범위 잠금을 획득하려고 대기하는 중입니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_U_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 업데이트 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 삽입 범위 잠금을 획득하려고 대기하는 중입니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_X |태스크가 현재 키 값의 배타 잠금 및 현재 키와 이전 키 간의 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RIn_X_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 배타 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RIn_X_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 배타 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 삽입 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RS_S |태스크가 현재 키 값의 공유 잠금 및 현재 키와 이전 키 간의 공유 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RS_S_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 공유 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 공유 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RS_S_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 공유 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 공유 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RS_U |태스크가 현재 키 값의 업데이트 잠금 및 현재 키와 이전 키 간의 업데이트 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RS_U_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 업데이트 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 업데이트 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RS_U_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 업데이트 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 업데이트 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RX_S |태스크가 현재 키 값의 공유 잠금 및 현재 키와 이전 키 간의 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RX_S_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 공유 잠금 및 현재 키와 이전 키 간의 중단 블로커 잠금이 포함된 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RX_S_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 공유 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위 잠금이 포함된 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RX_U |태스크가 현재 키 값의 업데이트 잠금 및 현재 키와 이전 키 간의 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RX_U_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 업데이트 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RX_U_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 업데이트 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RX_X |태스크가 현재 키 값의 배타 잠금 및 현재 키와 이전 키 간의 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_RX_X_ABORT_BLOCKERS |태스크가 현재 키 값의 중단 블로커가 포함된 배타 잠금 및 현재 키와 이전 키 간의 중단 블로커가 포함된 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_RX_X_LOW_PRIORITY |태스크가 현재 키 값의 낮은 우선 순위가 포함된 배타 잠금 및 현재 키와 이전 키 간의 낮은 우선 순위가 포함된 배타 범위 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_S |태스크가 공유 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_S_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_S_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SCH_M |태스크가 스키마 수정 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_SCH_M_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 스키마 수정 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SCH_M_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 스키마 수정 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SCH_S |태스크가 스키마 공유 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_SCH_S_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 스키마 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SCH_S_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 스키마 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SIU |태스크가 의도 업데이트 공유 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_SIU_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 의도 업데이트 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SIU_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 의도 업데이트 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SIX |태스크가 의도 배타 공유 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_SIX_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 의도 배타 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_SIX_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 의도 배타 공유 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_U |태스크가 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_U_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_U_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_UIX |태스크가 의도 배타 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_UIX_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 의도 배타 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_UIX_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 의도 배타 업데이트 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_X |태스크가 배타 잠금을 획득하려고 대기하는 경우에 발생합니다.| 
|LCK_M_X_ABORT_BLOCKERS |태스크가 중단 블로커가 포함된 배타 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LCK_M_X_LOW_PRIORITY |태스크가 낮은 우선 순위가 포함된 배타 잠금을 획득하려고 대기하는 경우에 발생합니다. (관련 된 ALTER TABLE 및 ALTER INDEX의 낮은 우선 순위 대기 옵션을.), <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOG_POOL_SCAN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOG_RATE_GOVERNOR |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGBUFFER |태스크가 로그 버퍼의 공간에 로그 레코드가 저장될 때까지 대기하는 경우에 발생합니다. 값이 계속 높게 나타나면 로그 장치가 서버에서 생성하는 로그의 양을 따라갈 수 없는 것일 수 있습니다.| 
|LOGCAPTURE_LOGPOOLTRUNCPOINT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGGENERATION |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|LOGMGR |데이터베이스를 닫는 동안 태스크가 로그 종료 전에 처리 중인 로그 I/O가 완료될 때까지 대기하는 경우에 발생합니다.| 
|LOGMGR_FLUSH |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|LOGMGR_PMM_LOG |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGMGR_QUEUE |로그 쓰기 태스크가 작업 요청을 대기하는 동안 발생합니다.| 
|LOGMGR_RESERVE_APPEND |태스크가 로그 잘림으로 인해 로그 공간이 확보되어 작업이 새 로그 레코드를 쓸 수 있는지 확인하려고 대기하는 경우에 발생합니다. 이 대기를 줄이려면 영향을 받는 데이터베이스의 로그 파일 크기를 늘리세요.| 
|LOGPOOL_CACHESIZE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGPOOL_CONSUMER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGPOOL_CONSUMERSET |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGPOOL_FREEPOOLS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGPOOL_MGRSET |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGPOOL_REPLACEMENTSET |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOGPOOLREFCOUNTEDOBJECT_REFDONE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|LOWFAIL_MEMMGR_QUEUE |메모리를 사용할 수 있을 때까지 대기하는 동안 발생합니다.| 
|MD_AGENT_YIELD |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|MD_LAZYCACHE_RWLOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|MEMORY_ALLOCATION_EXT |내부 SQL Server 메모리 풀 또는 운영 체제에서 메모리를 할당 하는 동안 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|MEMORY_GRANT_UPDATE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|METADATA_LAZYCACHE_RWLOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|MIGRATIONBUFFER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|MISCELLANEOUS |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|MISCELLANEOUS |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|MSQL_DQ |분산 쿼리 작업이 완료될 때까지 태스크가 대기하는 경우에 발생합니다. 발생 가능한 MARS(Multiple Active Result Set) 응용 프로그램 교착 상태를 감지하는 데 사용됩니다. 대기는 분산 쿼리 호출이 완료될 때 끝납니다.| 
|MSQL_XACT_MGR_MUTEX |태스크가 세션 트랜잭션 관리자의 소유권을 획득하여 세션 수준 트랜잭션 작업을 수행하려고 대기하는 경우에 발생합니다.| 
|MSQL_XACT_MUTEX |트랜잭션 사용 동기화 중에 발생합니다. 요청에서 트랜잭션을 사용하려면 먼저 뮤텍스를 획득해야 합니다.| 
|MSQL_XP |태스크가 확장 저장 프로시저가 끝날 때까지 대기하는 경우에 발생합니다. 이 대기 상태를 사용 하 여 잠재적 MARS 응용 프로그램 교착 상태를 검색할 SQL Server입니다. 대기는 확장 저장 프로시저 호출이 끝날 때 중지됩니다.| 
|MSSEARCH |전체 텍스트 검색 호출 중에 발생합니다. 이 대기는 전체 텍스트 작업이 완료될 때 끝나며 경합이 아니라 전체 텍스트 작업 기간을 나타냅니다.| 
|NET_WAITFOR_PACKET |네트워크 읽기 중 연결이 네트워크 패킷을 대기하는 경우에 발생합니다.| 
|NETWORKSXMLMGRLOAD |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|NODE_CACHE_MUTEX |내부적으로만 사용됩니다.| 
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
|PARALLEL_REDO_DRAIN_WORKER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PARALLEL_REDO_FLOW_CONTROL |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PARALLEL_REDO_LOG_CACHE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PARALLEL_REDO_TRAN_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PARALLEL_REDO_TRAN_TURN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PARALLEL_REDO_WORKER_SYNC |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PARALLEL_REDO_WORKER_WAIT_WORK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PERFORMANCE_COUNTERS_RWLOCK |내부적으로만 사용됩니다.| 
|PHYSICAL_SEEDING_DMV |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|POOL_LOG_RATE_GOVERNOR |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_ABR |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG |Windows 이벤트 로그에 감사 이벤트를 기록하기 위해 SQLOS([!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 운영 체제) 스케줄러가 우선 모드로 전환된 경우에 발생합니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG |Windows 보안 로그에 감사 이벤트를 기록하기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|PREEMPTIVE_CLOSEBACKUPMEDIA |백업 미디어를 닫기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.| 
|PREEMPTIVE_CLOSEBACKUPTAPE |테이프 백업 장치를 닫기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.| 
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE |가상 백업 장치를 닫기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.| 
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL |Windows 장애 조치(Failover) 클러스터 작업을 수행하기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.| 
|PREEMPTIVE_COM_COCREATEINSTANCE |COM 개체를 만들기 위해 SQLOS 스케줄러가 우선 모드로 전환된 경우에 발생합니다.| 
|PREEMPTIVE_COM_COGETCLASSOBJECT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_CREATEACCESSOR |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_DELETEROWS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_GETCOMMANDTEXT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_GETDATA |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_GETNEXTROWS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_GETRESULT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_GETROWSBYBOOKMARK |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_LBFLUSH |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_LBLOCKREGION |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_LBREADAT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_LBSETSIZE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_LBSTAT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_LBUNLOCKREGION |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_LBWRITEAT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_QUERYINTERFACE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_RELEASE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_RELEASEACCESSOR |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_RELEASEROWS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_RELEASESESSION |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_RESTARTPOSITION |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_SEQSTRMREAD |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_SEQSTRMREADANDWRITE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_SETDATAFAILURE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_SETPARAMETERINFO |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_SETPARAMETERPROPERTIES |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_STRMLOCKREGION |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_STRMSEEKANDREAD |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_STRMSEEKANDWRITE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_STRMSETSIZE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_STRMSTAT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_COM_STRMUNLOCKREGION |내부적으로만 사용됩니다.| 
|PREEMPTIVE_CONSOLEWRITE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_CREATEPARAM |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DEBUG |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DFSADDLINK |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DFSLINKEXISTCHECK |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DFSLINKHEALTHCHECK |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DFSREMOVELINK |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DFSREMOVEROOT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DFSROOTFOLDERCHECK |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DFSROOTINIT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DFSROOTSHARECHECK |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DTC_ABORT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DTC_ABORTREQUESTDONE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DTC_BEGINTRANSACTION |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DTC_COMMITREQUESTDONE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DTC_ENLIST |내부적으로만 사용됩니다.| 
|PREEMPTIVE_DTC_PREPAREREQUESTDONE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_FILESIZEGET |내부적으로만 사용됩니다.| 
|PREEMPTIVE_FSAOLEDB_ABORTTRANSACTION |내부적으로만 사용됩니다.| 
|PREEMPTIVE_FSAOLEDB_COMMITTRANSACTION |내부적으로만 사용됩니다.| 
|PREEMPTIVE_FSAOLEDB_STARTTRANSACTION |내부적으로만 사용됩니다.| 
|PREEMPTIVE_FSRECOVER_UNCONDITIONALUNDO |내부적으로만 사용됩니다.| 
|PREEMPTIVE_GETRMINFO |내부적으로만 사용됩니다.| 
|PREEMPTIVE_HADR_LEASE_MECHANISM |Always On 가용성 그룹 임대 관리자는 Microsoft 지원 진단에 대 한 일정입니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_HTTP_EVENT_WAIT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_HTTP_REQUEST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_LOCKMONITOR |내부적으로만 사용됩니다.| 
|PREEMPTIVE_MSS_RELEASE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_ODBCOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OLE_UNINIT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OLEDB_ABORTORCOMMITTRAN |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OLEDB_ABORTTRAN |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OLEDB_GETDATASOURCE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OLEDB_GETLITERALINFO |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OLEDB_GETPROPERTIES |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OLEDB_GETPROPERTYINFO |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OLEDB_GETSCHEMALOCK |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OLEDB_JOINTRANSACTION |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OLEDB_RELEASE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OLEDB_SETPROPERTIES |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OLEDBOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_ACCEPTSECURITYCONTEXT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_ACQUIRECREDENTIALSHANDLE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_AUTHENTICATIONOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_AUTHORIZATIONOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_AUTHZGETINFORMATIONFROMCONTEXT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_AUTHZINITIALIZECONTEXTFROMSID |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_AUTHZINITIALIZERESOURCEMANAGER |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_BACKUPREAD |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_CLOSEHANDLE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_CLUSTEROPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_COMOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_COMPLETEAUTHTOKEN |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_COPYFILE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_CREATEDIRECTORY |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_CREATEFILE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_CRYPTACQUIRECONTEXT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_CRYPTIMPORTKEY |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_CRYPTOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_DECRYPTMESSAGE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_DELETEFILE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_DELETESECURITYCONTEXT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_DEVICEIOCONTROL |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_DEVICEOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_DIRSVC_NETWORKOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_DISCONNECTNAMEDPIPE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_DOMAINSERVICESOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_DSGETDCNAME |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_DTCOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_ENCRYPTMESSAGE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_FILEOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_FINDFILE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_FLUSHFILEBUFFERS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_FORMATMESSAGE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_FREECREDENTIALSHANDLE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_FREELIBRARY |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_GENERICOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_GETADDRINFO |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_GETCOMPRESSEDFILESIZE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_GETDISKFREESPACE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_GETFILEATTRIBUTES |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_GETFILESIZE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_GETFINALFILEPATHBYHANDLE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_OS_GETLONGPATHNAME |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_GETPROCADDRESS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_GETVOLUMENAMEFORVOLUMEMOUNTPOINT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_GETVOLUMEPATHNAME |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_INITIALIZESECURITYCONTEXT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_LIBRARYOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_LOADLIBRARY |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_LOGONUSER |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_LOOKUPACCOUNTSID |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_MESSAGEQUEUEOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_MOVEFILE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_NETGROUPGETUSERS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_NETLOCALGROUPGETMEMBERS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_NETUSERGETGROUPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_NETUSERGETLOCALGROUPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_NETUSERMODALSGET |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICY |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICYFREE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_OPENDIRECTORY |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_PDH_WMI_INIT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_OS_PIPEOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_PROCESSOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_QUERYCONTEXTATTRIBUTES |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_OS_QUERYREGISTRY |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_QUERYSECURITYCONTEXTTOKEN |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_REMOVEDIRECTORY |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_REPORTEVENT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_REVERTTOSELF |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_RSFXDEVICEOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_SECURITYOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_SERVICEOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_SETENDOFFILE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_SETFILEPOINTER |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_SETFILEVALIDDATA |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_SETNAMEDSECURITYINFO |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_SQLCLROPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_SQMLAUNCH |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 부터 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]까지 |  
|PREEMPTIVE_OS_VERIFYSIGNATURE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_VERIFYTRUST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_OS_VSSOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_WAITFORSINGLEOBJECT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_WINSOCKOPS |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_WRITEFILE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_WRITEFILEGATHER |내부적으로만 사용됩니다.| 
|PREEMPTIVE_OS_WSASETLASTERROR |내부적으로만 사용됩니다.| 
|PREEMPTIVE_REENLIST |내부적으로만 사용됩니다.| 
|PREEMPTIVE_RESIZELOG |내부적으로만 사용됩니다.| 
|PREEMPTIVE_ROLLFORWARDREDO |내부적으로만 사용됩니다.| 
|PREEMPTIVE_ROLLFORWARDUNDO |내부적으로만 사용됩니다.| 
|PREEMPTIVE_SB_STOPENDPOINT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_SERVER_STARTUP |내부적으로만 사용됩니다.| 
|PREEMPTIVE_SETRMINFO |내부적으로만 사용됩니다.| 
|PREEMPTIVE_SHAREDMEM_GETDATA |내부적으로만 사용됩니다.| 
|PREEMPTIVE_SNIOPEN |내부적으로만 사용됩니다.| 
|PREEMPTIVE_SOSHOST |내부적으로만 사용됩니다.| 
|PREEMPTIVE_SOSTESTING |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|PREEMPTIVE_SP_SERVER_DIAGNOSTICS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_STARTRM |내부적으로만 사용됩니다.| 
|PREEMPTIVE_STREAMFCB_CHECKPOINT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_STREAMFCB_RECOVER |내부적으로만 사용됩니다.| 
|PREEMPTIVE_STRESSDRIVER |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|PREEMPTIVE_TESTING |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|PREEMPTIVE_TRANSIMPORT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_UNMARSHALPROPAGATIONTOKEN |내부적으로만 사용됩니다.| 
|PREEMPTIVE_VSS_CREATESNAPSHOT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_VSS_CREATEVOLUMESNAPSHOT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_XE_CALLBACKEXECUTE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_XE_CX_FILE_OPEN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_XE_CX_HTTP_CALL |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PREEMPTIVE_XE_DISPATCHER |내부적으로만 사용됩니다.| 
|PREEMPTIVE_XE_ENGINEINIT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_XE_GETTARGETSTATE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_XE_SESSIONCOMMIT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_XE_TARGETFINALIZE |내부적으로만 사용됩니다.| 
|PREEMPTIVE_XE_TARGETINIT |내부적으로만 사용됩니다.| 
|PREEMPTIVE_XE_TIMERRUN |내부적으로만 사용됩니다.| 
|PREEMPTIVE_XETESTING |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|PRINT_ROLLBACK_PROGRESS |ALTER DATABASE termination 절을 사용하여 전환된 데이터베이스에서 사용자 프로세스가 끝나기를 기다리는 데 사용됩니다. 자세한 내용은 ALTER DATABASE (TRANSACT-SQL)을 참조 하세요.| 
|PRU_ROLLBACK_DEFERRED |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_ALL_COMPONENTS_INITIALIZED |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_COOP_SCAN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_DIRECTLOGCONSUMER_GETNEXT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_EVENT_SESSION_INIT_MUTEX |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_FABRIC_REPLICA_CONTROLLER_DATA_LOSS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_ACTION_COMPLETED |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC |백그라운드 태스크가 대기 하는 (폴링)을 통해 받는 백그라운드 태스크가 종료에 대 한 경우 Windows Server 장애 조치 클러스터링 알림을., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_CLUSTER_INTEGRATION |추가, 바꾸기 및/또는 제거는 항상 내부 목록 (예: 네트워크, 네트워크 주소 또는 가용성 그룹 수신기의 목록)에 대 한 쓰기 잠금을 가져올 작업을 기다리고 있습니다. 내부 전용 <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_FAILOVER_COMPLETED |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_JOIN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_OFFLINE_COMPLETED |Windows Server 장애 조치 클러스터링 개체를 제거 하기 전에 오프 라인으로 전환 하는 대상 가용성 그룹 대기 하는 Always On 가용성 그룹 삭제 작업이., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_ONLINE_COMPLETED |Always On을 만들거나가 온라인 대상 가용성 그룹에 대 한 가용성 그룹 장애 조치 작업을 기다리고 있습니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_POST_ONLINE_COMPLETED |Always On 가용성 그룹 삭제 작업이 이전 명령의 일부로 예약 된 백그라운드 태스크가 종료 대기 중입니다. 예를 들어 가용성 데이터베이스를 주 역할로 전환 중인 백그라운드 작업이 있을 수 있습니다. DROP AVAILABILITY GROUP DDL이 백그라운드 태스크가 종료 경합을 방지 하기 위해 대기 해야 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_SERVER_READY_CONNECTIONS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADR_WORKITEM_COMPLETED |비동기 작업 태스크가 완료될 때까지 기다리는 스레드에 의한 내부 대기입니다. 이 예상 되는 대기 이며 CSS를 사용 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_HADRSIM |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_LOG_CONSOLIDATION_IO |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_LOG_CONSOLIDATION_POLL |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_MD_LOGIN_STATS |로그인 상태에서 메타 데이터의 내부 동기화 중에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_MD_RELATION_CACHE |테이블 또는 인덱스에서 메타 데이터의 내부 동기화 중에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_MD_SERVER_CACHE |연결 된 서버에서 메타 데이터의 내부 동기화 중에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_MD_UPGRADE_CONFIG |서버 차원 구성 업그레이드의 내부 동기화 중에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_PREEMPTIVE_APP_USAGE_TIMER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_PREEMPTIVE_AUDIT_ACCESS_WINDOWSLOG |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_QRY_BPMEMORY |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_REPLICA_ONLINE_INIT_MUTEX |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_SBS_FILE_OPERATION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_XTP_FSSTORAGE_MAINTENANCE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|PWAIT_XTP_HOST_STORAGE_WAIT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_ASYNC_CHECK_CONSISTENCY_TASK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_ASYNC_PERSIST_TASK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_ASYNC_PERSIST_TASK_START |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_ASYNC_QUEUE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_BCKG_TASK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_BLOOM_FILTER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_CLEANUP_STALE_QUERIES_TASK_MAIN_LOOP_SLEEP |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_CTXS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_DB_DISK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_DYN_VECTOR |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_EXCLUSIVE_ACCESS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_HOST_INIT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_LOADDB |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_PERSIST_TASK_MAIN_LOOP_SLEEP |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_QDS_CAPTURE_INIT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_SHUTDOWN_QUEUE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_STMT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_STMT_DISK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_TASK_SHUTDOWN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QDS_TASK_START |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QE_WARN_LIST_SYNC |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QPJOB_KILL |업데이트가 실행되기 시작할 때 KILL 호출을 통해 비동기 자동 통계 업데이트가 취소되었음을 나타냅니다. 종료하는 스레드는 일시 중지 상태로, KILL 명령을 수신하기 시작할 때까지 대기합니다. 1초보다 작은 값이 좋습니다.| 
|QPJOB_WAITFOR_ABORT |실행되고 있을 때 KILL 호출을 통해 비동기 자동 통계 업데이트가 취소되었음을 나타냅니다. 업데이트는 이제 완료되었지만 종료하는 스레드 메시지 조정이 완료될 때까지 일시 중지됩니다. 이 상태는 일반적이지만 거의 발생하지 않으며 매우 짧아야 합니다. 1초보다 작은 값이 좋습니다.| 
|QRY_MEM_GRANT_INFO_MUTEX |쿼리 실행 메모리 관리 기능이 정적 권한 부여 정보 목록에 대한 액세스를 제어하려고 하는 경우에 발생합니다. 이 상태는 현재 권한이 부여된 메모리 요청과 대기 중인 메모리 요청에 대한 정보를 나열합니다. 이 상태는 단순 액세스 제어 상태입니다. 이 상태에 대한 긴 대기가 있으면 안 됩니다. 이 뮤텍스가 해제되지 않으면 새로운 메모리 사용 쿼리의 응답이 모두 중지됩니다.| 
|QRY_PARALLEL_THREAD_MUTEX |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QRY_PROFILE_LIST_MUTEX |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QUERY_ERRHDL_SERVICE_DONE |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|QUERY_WAIT_ERRHDL_SERVICE |정보를 제공하기 위해서만 확인됩니다.  지원되지 않습니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다.  |  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN |오프라인 인덱스 빌드 생성이 병렬로 실행되고 정렬되는 여러 작업자 스레드가 정렬 파일에 대한 액세스를 동기화하는 특정 경우에 발생합니다.| 
|QUERY_NOTIFICATION_MGR_MUTEX |쿼리 알림 관리자에서 가비지 수집 큐 동기화 중에 발생합니다.| 
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX |쿼리 알림의 트랜잭션 상태 동기화 중에 발생합니다.| 
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX |쿼리 알림 관리자의 내부 동기화 중에 발생합니다.| 
|QUERY_NOTIFICATION_UNITTEST_MUTEX |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|QUERY_OPTIMIZER_PRINT_MUTEX |쿼리 최적화 프로그램의 진단 출력 생성 동기화 중에 발생합니다. 이 대기 유형은 진단 설정이 Microsoft 제품 지원 담당자의 지시 대로 설정 된 경우에 발생 합니다.| 
|QUERY_TASK_ENQUEUE_MUTEX |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|QUERY_TRACEOUT |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|RBIO_WAIT_VLF |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|RBIO_RG_STORAGE |지연 된 로그 페이지 서버 사용량으로 인해 제한 되 고 대규모 데이터베이스 계산 노드 때 발생 합니다. <br /> **적용 대상**: Azure SQL Database 대규모 합니다.|
|RBIO_RG_DESTAGE |대규모 데이터베이스 계산 노드 장기 로그 저장소에 의해 지연 된 로그 사용으로 인해 제한 되 면 발생 합니다. <br /> **적용 대상**: Azure SQL Database 대규모 합니다.|
|RBIO_RG_REPLICA |읽기 가능한 보조 복제본 노드 로그 소비 지연으로 인해 제한 되 고 데이터베이스 계산 노드는 대규모 때 발생 합니다. <br /> **적용 대상**: Azure SQL Database 대규모 합니다.|
|RBIO_RG_LOCALDESTAGE |대규모 데이터베이스 계산 노드 지연 된 로그 사용으로 인해 로그 서비스에 의해 제한 되 면 발생 합니다. <br /> **적용 대상**: Azure SQL Database 대규모 합니다.|
|RECOVER_CHANGEDB |웜 대기 데이터베이스의 데이터베이스 상태 동기화 중에 발생합니다.| 
|RECOVERY_MGR_LOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REDO_THREAD_PENDING_WORK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REDO_THREAD_SYNC |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REMOTE_BLOCK_IO |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REMOTE_DATA_ARCHIVE_MIGRATION_DMV |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REMOTE_DATA_ARCHIVE_SCHEMA_DMV |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REMOTE_DATA_ARCHIVE_SCHEMA_TASK_QUEUE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REPL_CACHE_ACCESS |복제 아티클 캐시 동기화 중에 발생합니다. 이 대기 중에는 복제 로그 판독기가 정지되고 게시된 테이블에 대한 DDL(데이터 정의 언어) 문이 차단됩니다.| 
|REPL_HISTORYCACHE_ACCESS |내부적으로만 사용됩니다.| 
|REPL_SCHEMA_ACCESS |복제 스키마 버전 정보 동기화 중에 발생합니다. 복제된 개체에 대해 DDL 문을 실행하고 로그 판독기가 DDL 발생을 기반으로 버전이 지정된 스키마를 작성하거나 사용할 때 이 상태가 됩니다. 트랜잭션 복제를 사용 하 여 단일 게시자에서 게시 된 여러 데이터베이스가 있고 게시 된 데이터베이스는 매우 활발 하는 경우이 대기 유형은에서 경합을 볼 수 있습니다.| 
|REPL_TRANFSINFO_ACCESS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REPL_TRANHASHTABLE_ACCESS |내부적으로만 사용됩니다.| 
|REPL_TRANTEXTINFO_ACCESS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|REPLICA_WRITES |태스크가 데이터베이스 스냅숏 또는 DBCC 복제본에 대한 페이지 쓰기가 완료될 때까지 대기하는 동안 발생합니다.| 
|REQUEST_DISPENSER_PAUSE |스냅숏 백업을 위해 파일 I/O를 고정할 수 있도록 태스크가 처리 중인 모든 I/O가 완료될 때까지 대기하는 경우에 발생합니다.| 
|REQUEST_FOR_DEADLOCK_SEARCH |교착 상태 모니터가 다음 교착 상태 검색을 시작하기 위해 대기하는 동안 발생합니다. 이 대기는 교착 상태 감지 사이에 발생하며 이 리소스에 대한 총 대기 시간이 길어도 문제가 있는 것은 아닙니다.| 
|RESERVED_MEMORY_ALLOCATION_EXT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|RESMGR_THROTTLED |새 쿼리가 GROUP_MAX_REQUESTS 설정에 따라 들어오고 정체되는 경우 발생합니다.| 
|RESOURCE_GOVERNOR_IDLE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|RESOURCE_QUEUE |다양한 내부 리소스 큐 동기화 중에 발생합니다.| 
|RESOURCE_SEMAPHORE |다른 동시 쿼리로 인해 쿼리 메모리 요청을 즉시 허용할 수 없는 경우에 발생합니다. 대기 수가 많고 대기 시간이 길면 동시 쿼리 수 또는 메모리 요청 양이 과도하게 많은 것입니다.| 
|RESOURCE_SEMAPHORE_MUTEX |쿼리가 스레드 예약 요청이 수행될 때까지 대기하는 동안 발생합니다. 또한 쿼리 컴파일 및 메모리 부여 요청을 동기화하는 경우에 발생합니다.| 
|RESOURCE_SEMAPHORE_QUERY_COMPILE |동시 쿼리 컴파일 수가 조절 한계에 도달한 경우에 발생합니다. 대기 수가 많고 대기 시간이 길면 컴파일, 다시 컴파일 또는 캐싱할 수 없는 계획 수가 과도하게 많은 것입니다.| 
|RESOURCE_SEMAPHORE_SMALL_QUERY |다른 동시 쿼리로 인해 작은 쿼리의 메모리 요청을 즉시 허용할 수 없는 경우에 발생합니다. 서버는 몇 초 내에 요청된 메모리를 부여하지 못하면 주 쿼리 메모리 풀로 요청을 전송하기 때문에 대기 시간은 몇 초를 넘지 않아야 합니다. 대기 수가 많으면 대기 중인 쿼리가 주 메모리 풀을 차단하는 동안 작은 동시 쿼리 수가 과도하게 많은 것입니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|RESTORE_FILEHANDLECACHE_ENTRYLOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|RESTORE_FILEHANDLECACHE_LOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|RG_RECONFIG |내부적으로만 사용됩니다.| 
|ROWGROUP_OP_STATS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|ROWGROUP_VERSION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|RTDATA_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SATELLITE_CARGO |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SATELLITE_SERVICE_SETUP |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SATELLITE_TASK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SBS_DISPATCH |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SBS_RECEIVE_TRANSPORT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SBS_TRANSPORT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SCAN_CHAR_HASH_ARRAY_INITIALIZATION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SEC_DROP_TEMP_KEY |임시 보안 키 삭제 시도가 실패한 후 다시 시도하기 전에 발생합니다.| 
|SECURITY_CNG_PROVIDER_MUTEX |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SECURITY_CRYPTO_CONTEXT_MUTEX |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SECURITY_DBE_STATE_MUTEX |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SECURITY_KEYRING_RWLOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SECURITY_MUTEX |EKM(확장 가능 키 관리) 암호화 공급자의 전역 목록 및 EKM 세션의 세션 범위 목록에 대한 액세스를 제어하는 뮤텍스를 기다리는 경우에 발생합니다.| 
|SECURITY_RULETABLE_MUTEX |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SEMPLAT_DSI_BUILD |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SEQUENCE_GENERATION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SEQUENTIAL_GUID |새 순차적 GUID를 가져오는 동안 발생합니다.| 
|SERVER_IDLE_CHECK |리소스 모니터는 유휴로 SQL Server 인스턴스를 선언 하는 동안 또는 절전 모드 해제 하려고 하는 경우 SQL Server 인스턴스 유휴 상태 동기화 중에 발생 합니다.| 
|SERVER_RECONFIGURE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SESSION_WAIT_STATS_CHILDREN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SHARED_DELTASTORE_CREATION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SHUTDOWN |종료 문이 활성 연결이 종료될 때까지 대기하는 동안 발생합니다.| 
|SLEEP_BPOOL_FLUSH |검사점이 디스크 하위 시스템의 폭주를 방지하기 위해 새 I/O의 실행을 조절하는 경우에 발생합니다.| 
|SLEEP_BUFFERPOOL_HELPLW |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLEEP_DBSTARTUP |모든 데이터베이스가 복구될 때까지 대기하는 동안 데이터베이스 시작 중에 발생합니다.| 
|SLEEP_DCOMSTARTUP |DCOM 초기화가 완료 될 때까지 기다리는 동안 SQL Server 인스턴스 시작 중에 많아야 한 번 발생 합니다.| 
|SLEEP_MASTERDBREADY |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLEEP_MASTERMDREADY |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLEEP_MASTERUPGRADED |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLEEP_MEMORYPOOL_ALLOCATEPAGES |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLEEP_MSDBSTARTUP |SQL 추적이 msdb 데이터베이스 시작이 완료될 때까지 대기하는 경우에 발생합니다.| 
|SLEEP_RETRY_VIRTUALALLOC |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLEEP_SYSTEMTASK |tempdb 시작이 완료될 때까지 대기하는 동안 백그라운드 태스크 시작 중에 발생합니다.| 
|SLEEP_TASK |일반 이벤트가 발생할 때까지 대기하는 동안 태스크가 중지되는 경우에 발생합니다.| 
|SLEEP_TEMPDBSTARTUP |태스크가 tempdb 시작이 완료될 때까지 대기하는 동안 발생합니다.| 
|SLEEP_WORKSPACE_ALLOCATEPAGE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SLO_UPDATE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SMSYNC |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SNI_CONN_DUP |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SNI_CRITICAL_SECTION |SQL Server 네트워킹 구성 요소 내에서 내부 동기화 중에 발생 합니다.| 
|SNI_HTTP_WAITFOR_0_DISCON |처리 중인 HTTP 연결이 종료 될 때까지 기다리는 동안 SQL Server 종료 하는 동안 발생 합니다.| 
|SNI_LISTENER_ACCESS |NUMA(비균일 메모리 액세스) 노드의 상태 변경 업데이트 작업을 대기하는 동안 발생합니다. 상태 변경에 대한 액세스는 직렬화됩니다.| 
|SNI_TASK_COMPLETION |NUMA 노드 상태 변경 동안 모든 태스크가 완료될 때까지 대기하는 중에 발생합니다.| 
|SNI_WRITE_ASYNC |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SOAP_READ |HTTP 네트워크 읽기가 완료될 때까지 대기하는 동안 발생합니다.| 
|SOAP_WRITE |HTTP 네트워크 쓰기가 완료될 때까지 대기하는 동안 발생합니다.| 
|SOCKETDUPLICATEQUEUE_CLEANUP |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SOS_CALLBACK_REMOVAL |콜백을 제거하기 위해 콜백 목록에 대한 동기화를 수행하는 동안 발생합니다. 서버 초기화가 완료된 후에는 이 카운터가 변경되지 않습니다.| 
|SOS_DISPATCHER_MUTEX |디스패처 풀의 내부 동기화 중에 발생합니다. 풀이 조정되는 경우도 포함됩니다.| 
|SOS_LOCALALLOCATORLIST |[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 메모리 관리자의 내부 동기화 중에 발생합니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|SOS_MEMORY_TOPLEVELBLOCKALLOCATOR |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SOS_MEMORY_USAGE_ADJUSTMENT |메모리 사용량이 풀 사이에서 조절될 경우 발생합니다.| 
|SOS_OBJECT_STORE_DESTROY_MUTEX |풀에서 개체를 삭제하는 경우 메모리 풀의 내부 동기화 중에 발생합니다.| 
|SOS_PHYS_PAGE_CACHE |스레드가 물리적 페이지를 할당하거나 물리적 페이지를 운영 체제에 반환하기 전에 확보해야 하는 뮤텍스를 획득하기 위해 대기하는 시간을 고려합니다. 이 유형의 대기는 SQL Server 인스턴스에서 AWE 메모리를 사용 하는 경우에 나타납니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SOS_PROCESS_AFFINITY_MUTEX |프로세스 선호도 설정에 대한 액세스 동기화 중에 발생합니다.| 
|SOS_RESERVEDMEMBLOCKLIST |SQL Server 메모리 관리자의 내부 동기화 중에 발생 합니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|SOS_SCHEDULER_YIELD |다른 작업이 실행될 수 있도록 태스크가 자발적으로 스케줄러를 양보하는 경우에 발생합니다. 이 대기 중에 태스크는 해당 퀀텀이 갱신될 때까지 대기합니다.| 
|SOS_SMALL_PAGE_ALLOC |일부 메모리 개체에 의해 관리되는 메모리의 할당 및 해제 중에 발생합니다.| 
|SOS_STACKSTORE_INIT_MUTEX |내부 저장소 초기화 동기화 중에 발생합니다.| 
|SOS_SYNC_TASK_ENQUEUE_EVENT |태스크가 동기 방식으로 시작되는 경우에 발생합니다. SQL Server에서 대부분의 작업은 제어 반환 하는 시작으로 작업 요청이 작업 큐에 배치 된 후에 즉시는 비동기 방식으로 시작 됩니다.| 
|SOS_VIRTUALMEMORY_LOW |메모리 할당이 리소스 관리자가 가상 메모리를 해제할 때까지 대기하는 경우에 발생합니다.| 
|SOSHOST_EVENT |CLR과 같은 호스팅된 구성 요소가 SQL Server 이벤트 동기화 개체에서 대기 하는 경우 발생 합니다.| 
|SOSHOST_INTERNAL |CLR과 같은 호스팅된 구성 요소에 사용되는 메모리 관리자 콜백 동기화 중에 발생합니다.| 
|SOSHOST_MUTEX |CLR과 같은 호스팅된 구성 요소가 SQL Server 뮤텍스 동기화 개체에서 대기 하는 경우 발생 합니다.| 
|SOSHOST_RWLOCK |CLR과 같은 호스팅된 구성 요소가 SQL Server 읽기 / 쓰기 동기화 개체에서 대기 하는 경우 발생 합니다.| 
|SOSHOST_SEMAPHORE |CLR과 같은 호스팅된 구성 요소가 SQL Server 세마포 동기화 개체에서 대기 하는 경우 발생 합니다.| 
|SOSHOST_SLEEP |일반 이벤트가 발생할 때까지 대기하는 동안 호스팅된 태스크가 중지되는 경우에 발생합니다. 호스팅된 태스크는 CLR과 같은 호스팅된 구성 요소에 사용됩니다.| 
|SOSHOST_TRACELOCK |추적 스트림에 대한 액세스 동기화 중에 발생합니다.| 
|SOSHOST_WAITFORDONE |CLR과 같은 호스팅된 구성 요소가 태스크가 완료될 때까지 대기하는 경우에 발생합니다.| 
|SP_PREEMPTIVE_SERVER_DIAGNOSTICS_SLEEP |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SP_SERVER_DIAGNOSTICS_BUFFER_ACCESS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SP_SERVER_DIAGNOSTICS_INIT_MUTEX |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SP_SERVER_DIAGNOSTICS_SLEEP |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SQLCLR_APPDOMAIN |CLR이 응용 프로그램 도메인 시작이 완료될 때까지 대기하는 동안 발생합니다.| 
|SQLCLR_ASSEMBLY |appdomain의 로드된 어셈블리 목록에 대한 액세스를 대기하는 동안 발생합니다.| 
|SQLCLR_DEADLOCK_DETECTION |CLR이 교착 상태 감지가 완료될 때까지 대기하는 동안 발생합니다.| 
|SQLCLR_QUANTUM_PUNISHMENT |CLR 태스크가 실행 퀀텀을 초과하여 조절되는 경우에 발생합니다. 이러한 조절은 리소스를 많이 사용하는 이 태스크가 다른 작업에 미치는 영향을 줄이기 위해 수행됩니다.| 
|SQLSORT_NORMMUTEX |내부 정렬 구조를 초기화하는 동안 내부 동기화 중에 발생합니다.| 
|SQLSORT_SORTMUTEX |내부 정렬 구조를 초기화하는 동안 내부 동기화 중에 발생합니다.| 
|SQLTRACE_BUFFER_FLUSH |태스크가 백그라운드 작업이 4초마다 추적 버퍼를 디스크로 플러시할 때까지 대기하는 경우에 발생합니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|SQLTRACE_FILE_BUFFER |파일 추적에서 추적 버퍼 동기화 중에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SQLTRACE_FILE_READ_IO_COMPLETION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SQLTRACE_FILE_WRITE_IO_COMPLETION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SQLTRACE_INCREMENTAL_FLUSH_SLEEP |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SQLTRACE_LOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|SQLTRACE_PENDING_BUFFER_WRITERS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|SQLTRACE_SHUTDOWN |추적 종료가 처리 중인 추적 이벤트가 완료될 때까지 대기하는 동안 발생합니다.| 
|SQLTRACE_WAIT_ENTRIES |SQL 추적 이벤트 큐가 패킷이 큐에 도착할 때까지 대기하는 동안 발생합니다.| 
|SRVPROC_SHUTDOWN |종료 프로세스가 올바르게 종료하기 위해 내부 리소스가 해제될 때까지 대기하는 동안 발생합니다.| 
|STARTUP_DEPENDENCY_MANAGER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|TDS_BANDWIDTH_STATE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|TDS_INIT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|TDS_PROXY_CONTAINER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|TEMPOBJ |임시 개체 삭제가 동기화되는 경우에 발생합니다. 이 대기는 드물게 발생하며 태스크가 temp 테이블 삭제에 대한 액세스를 과도하게 요청한 경우에만 발생합니다.| 
|TEMPORAL_BACKGROUND_PROCEED_CLEANUP |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|TERMINATE_LISTENER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|THREADPOOL |태스크가 작업자가 실행될 때까지 대기하는 경우에 발생합니다. 이는 최대 작업자 설정이 너무 낮거나 해당 일괄 처리 실행이 비정상적으로 오래 수행되어 다른 일괄 처리에 사용할 수 있는 작업자 수가 감소한 것입니다.| 
|TIMEPRIV_TIMEPERIOD |확장 이벤트 타이머의 내부 동기화 중에 발생합니다.| 
|TRACE_EVTNOTIF |내부적으로만 사용됩니다.| 
|TRACEWRITE |SQL 추적 행 집합 추적 공급자가 사용 가능한 버퍼나 이벤트를 포함한 버퍼가 처리될 때까지 대기하는 경우에 발생합니다.| 
|TRAN_MARKLATCH_DT |표시된 트랜잭션에 대한 삭제 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.| 
|TRAN_MARKLATCH_EX |표시된 트랜잭션에 대한 배타 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.| 
|TRAN_MARKLATCH_KP |표시된 트랜잭션에 대한 유지 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.| 
|TRAN_MARKLATCH_NL |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|TRAN_MARKLATCH_SH |표시된 트랜잭션에 대한 공유 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.| 
|TRAN_MARKLATCH_UP |표시된 트랜잭션에 대한 업데이트 모드 래치를 대기하는 경우에 발생합니다. 트랜잭션 표시 래치는 표시된 트랜잭션의 커밋 동기화에 사용됩니다.| 
|TRANSACTION_MUTEX |트랜잭션에 대한 여러 일괄 처리의 액세스 동기화 중에 발생합니다.| 
|UCS_ENDPOINT_CHANGE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|UCS_MANAGER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|UCS_MEMORY_NOTIFICATION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|UCS_SESSION_REGISTRATION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|UCS_TRANSPORT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|UCS_TRANSPORT_STREAM_CHANGE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|UTIL_PAGE_ALLOC |트랜잭션 로그 검색이 메모리 부족 시 메모리를 사용할 수 있을 때까지 대기하는 경우에 발생합니다.| 
|VDI_CLIENT_COMPLETECOMMAND |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|VDI_CLIENT_GETCOMMAND |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|VDI_CLIENT_OPERATION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|VDI_CLIENT_OTHER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|VERSIONING_COMMITTING |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|VIA_ACCEPT |시작하는 동안 VIA(Virtual Interface Adapter) 공급자 연결이 완료된 경우에 발생합니다.| 
|VIEW_DEFINITION_MUTEX |캐시된 뷰 정의에 대한 액세스 동기화 중에 발생합니다.| 
|WAIT_FOR_RESULTS |쿼리 알림이 트리거될 때까지 대기하는 경우에 발생합니다.| 
|WAIT_ON_SYNC_STATISTICS_REFRESH |동기 통계 업데이트 쿼리 컴파일 전에 완료 하 고 실행을 다시 시작할 수에 대 한 대기 하는 경우 발생 합니다.<br /> **적용 대상**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]로 시작|
|WAIT_SCRIPTDEPLOYMENT_REQUEST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_SCRIPTDEPLOYMENT_WORKER |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XLOGREAD_SIGNAL |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_ASYNC_TX_COMPLETION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_CKPT_AGENT_WAKEUP |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_CKPT_CLOSE |검사점이 완료 될 때까지 기다리는 경우 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_CKPT_ENABLED |검사점 사용 안 함, 및에 대 한 대기 중인 검사점을 사용할 때 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_CKPT_STATE_LOCK |검사점 상태 확인을 동기화 할 때 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_COMPILE_WAIT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지.| 
|WAIT_XTP_GUEST |데이터베이스 메모리 할당자는 메모리 부족 알림 수신을 중지할 수 할 때 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_HOST_WAIT |대기 데이터베이스 엔진에 의해 트리거되는 호스트에서 구현 된 경우에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_OFFLINE_CKPT_BEFORE_REDO |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_OFFLINE_CKPT_LOG_IO |오프 라인 검사점 로그 읽기 IO 완료를 기다리는 경우에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_OFFLINE_CKPT_NEW_LOG |새 로그 레코드를 검색에 대 한 오프 라인 검사점 기다리는 경우에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_PROCEDURE_ENTRY |저장 프로시저를 모든 현재 실행 프로시저가 완료를 대기할 때 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_RECOVERY |데이터베이스 복구를 완료 하려면 메모리 최적화 개체의 복구를 위해 기다리는 경우에 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_SERIAL_RECOVERY |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_SWITCH_TO_INACTIVE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_TASK_SHUTDOWN |메모리 내 oltp 네트워크 읽기가 완료 될 때까지 기다리는 경우 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAIT_XTP_TRAN_DEPENDENCY |트랜잭션 종속성을 기다리는 경우 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAITFOR |WAITFOR TRANSACT-SQL 문으로 인해 발생합니다. 대기 시간은 문의 매개 변수에 의해 결정됩니다. 이 대기는 사용자가 시작합니다.| 
|WAITFOR_PER_QUEUE |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WAITFOR_TASKSHUTDOWN |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|WAITSTAT_MUTEX |sys.dm_os_wait_stats를 채우는 데 사용되는 통계 컬렉션에 대한 액세스 동기화 중에 발생합니다.| 
|WCC |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|WINDOW_AGGREGATES_MULTIPASS |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WINFAB_API_CALL |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WINFAB_REPLICA_BUILD_OPERATION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WINFAB_REPORT_FAULT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|WORKTBL_DROP |작업 테이블 삭제가 실패한 후 다시 시도하기 전에 일시 중지하는 동안 발생합니다.| 
|WRITE_COMPLETION |쓰기 작업이 진행 중인 경우에 발생합니다.| 
|WRITELOG |로그 플러시가 완료될 때까지 대기하는 동안 발생합니다. 로그 플러시를 발생시키는 일반적인 작업은 검사점과 트랜잭션 커밋입니다.| 
|XACT_OWN_TRANSACTION |트랜잭션 소유권을 획득하기 위해 대기하는 동안 발생합니다.| 
|XACT_RECLAIM_SESSION |세션의 현재 소유자가 세션 소유권을 해제할 때까지 대기하는 동안 발생합니다.| 
|XACTLOCKINFO |트랜잭션 잠금 목록에 대한 액세스 동기화 중에 발생합니다. 트랜잭션 자체 외에도 교착 상태 감지, 페이지 분할 중 잠금 마이그레이션 등의 작업이 이 잠금 목록에 액세스합니다.| 
|XACTWORKSPACE_MUTEX |트랜잭션에서 제거 및 트랜잭션 참여 멤버 간의 데이터베이스 잠금 수 동기화 중에 발생합니다.| 
|XDB_CONN_DUP_HASH |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XDES_HISTORY |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XDES_OUT_OF_ORDER_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XDES_SNAPSHOT |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XDESTSVERMGR |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XE_BUFFERMGR_ALLPROCESSED_EVENT |확장 이벤트 세션 버퍼를 대상으로 플러시할 때 발생합니다. 이 대기는 백그라운드 스레드에서 발생합니다.| 
|XE_BUFFERMGR_FREEBUF_EVENT |다음 조건 중 하나에 해당하는 경우 발생합니다.| 
|XE_CALLBACK_LIST |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XE_CX_FILE_READ |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XE_DISPATCHER_CONFIG_SESSION_LIST |비동기 대상을 사용하는 확장 이벤트 세션이 시작 또는 중지될 때 발생합니다. 이 대기는 다음 중 하나를 의미할 수 있습니다.| 
|XE_DISPATCHER_JOIN |확장 이벤트 세션에 사용되는 백그라운드 스레드가 종료되는 경우 발생합니다.| 
|XE_DISPATCHER_WAIT |확장 이벤트 세션에 사용되는 백그라운드 스레드가 이벤트 버퍼 처리를 기다리는 경우 발생합니다.| 
|XE_FILE_TARGET_TVF |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XE_LIVE_TARGET_TVF |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XE_MODULEMGR_SYNC |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|XE_OLS_LOCK |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.| 
|XE_PACKAGE_LOCK_BACKOFF |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. <br /> **적용 대상**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 만 합니다. |  
|XE_SERVICES_EVENTMANUAL |내부적으로만 사용됩니다.| 
|XE_SERVICES_MUTEX |내부적으로만 사용됩니다.| 
|XE_SERVICES_RWLOCK |내부적으로만 사용됩니다.| 
|XE_SESSION_CREATE_SYNC |내부적으로만 사용됩니다.| 
|XE_SESSION_FLUSH |내부적으로만 사용됩니다.| 
|XE_SESSION_SYNC |내부적으로만 사용됩니다.| 
|XE_STM_CREATE |내부적으로만 사용됩니다.| 
|XE_TIMER_EVENT |내부적으로만 사용됩니다.| 
|XE_TIMER_MUTEX |내부적으로만 사용됩니다.| 
|XE_TIMER_TASK_DONE |내부적으로만 사용됩니다.| 
|XIO_CREDENTIAL_MGR_RWLOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XIO_CREDENTIAL_RWLOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XIO_EDS_MGR_RWLOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XIO_EDS_RWLOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XIO_IOSTATS_BLOBLIST_RWLOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XIO_IOSTATS_FCBLIST_RWLOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XIO_LEASE_RENEW_MGR_RWLOCK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTP_HOST_DB_COLLECTION |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTP_HOST_LOG_ACTIVITY |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTP_HOST_PARALLEL_RECOVERY |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTP_PREEMPTIVE_TASK |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTP_TRUNCATION_LSN |내부적으로만 사용됩니다. <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTPPROC_CACHE_ACCESS |모든 고유 하 게 컴파일된 저장된 프로시저 캐시 개체에 액세스할 때 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
|XTPPROC_PARTITIONED_STACK_CREATE |지정 된 프로시저에 대 한 저장된 프로시저 캐시 구조 (단일 스레드로 수행 되어야 합니다) 컴파일될-NUMA 노드를 고유 하 게 할당할 때 발생 합니다., <br /> **적용 대상**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|

  
 다음과 같은 Xevent 파티션 관련이 **스위치** 및 온라인 인덱스 다시 작성 합니다. 구문에 대 한 자세한 내용은 [ALTER TABLE &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-table-transact-sql.md) 하 고 [ALTER INDEX &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 잠금 호환성 행렬을 참조 하세요 [sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)합니다.  
  
## <a name="see-also"></a>참고자료  
    
 [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)   
 [sys.dm_db_wait_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-wait-stats-azure-sql-database.md)  
  
  


