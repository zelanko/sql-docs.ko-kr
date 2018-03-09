---
title: sys.dm_os_schedulers (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_schedulers
- sys.dm_os_schedulers_TSQL
- sys.dm_os_schedulers
- dm_os_schedulers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_schedulers dynamic management view
ms.assetid: 3a09d81b-55d5-416f-9cda-1a3a5492abe0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aa32726893d196cc4c2830e79703f5583d661793
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmosschedulers-transact-sql"></a>sys.dm_os_schedulers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  각 스케줄러가 개별 프로세서에 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 스케줄러당 하나의 행을 반환합니다. 이 뷰를 사용하여 스케줄러 상태를 모니터링하거나 런어웨이 태스크를 식별할 수 있습니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_schedulers**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|scheduler_address|**varbinary(8)**|스케줄러의 메모리 주소입니다. Null을 허용하지 않습니다.|  
|parent_node_id|**int**|부모 노드라고도 하는 스케줄러가 속한 노드의 ID입니다. 이것은 NUMA(Non-Uniform Memory Access) 노드를 나타냅니다. Null을 허용하지 않습니다.|  
|scheduler_id|**int**|스케줄러의 ID입니다. 일반 쿼리를 실행하는 데 사용되는 모든 스케줄러에는 1048576 미만의 ID 번호가 있습니다. 관리자 전용 연결 스케줄러와 같이 ID가 1048576보다 크거나 같은 스케줄러는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 내부적으로 사용됩니다. Null을 허용하지 않습니다.|  
|cpu_id|**smallint**|스케줄러에 할당된 CPU ID입니다.<br /><br /> Null을 허용하지 않습니다.<br /><br /> **참고:** 255 확인 하지 못한 선호도 없음에서 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]합니다. 참조 [sys.dm_os_threads&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md) 추가 선호도 정보에 대 한 합니다.|  
|상태|**nvarchar(60)**|스케줄러의 상태를 나타냅니다. 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> 숨김 온라인<br />숨김 오프 라인<br />-표시 온라인<br />-표시 오프 라인<br />-표시 온라인 (DAC)<br />-   HOT_ADDED<br /><br /> Null을 허용하지 않습니다.<br /><br /> HIDDEN 스케줄러는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 내부의 요청을 처리하는 데 사용되고 VISIBLE 스케줄러는 사용자 요청을 처리하는 데 사용됩니다.<br /><br /> OFFLINE 스케줄러는 선호도 마스크에서 오프라인 상태인 프로세서에 매핑되므로 다른 요청을 처리하는 데 사용되지 않습니다. ONLINE 스케줄러는 선호도 마스크에서 온라인 상태인 프로세서에 매핑되므로 스레드 처리에 사용할 수 있습니다.<br /><br /> DAC는 스케줄러가 관리자 전용 연결로 실행되고 있음을 나타냅니다.<br /><br /> HOT ADDED는 hot add CPU 이벤트에 대한 응답으로 스케줄러가 추가되었음을 나타냅니다.|  
|is_online|**bit**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 서버에서 사용할 수 있는 프로세서 중 일부만 사용하도록 구성된 경우 이 구성은 일부 스케줄러가 선호도 마스크에 없는 프로세서에 매핑되어 있음을 의미할 수 있습니다. 이 경우 이 열은 0을 반환합니다. 이 값은 스케줄러가 쿼리나 일괄 처리를 처리하는 데 사용되고 있지 않음을 의미합니다.<br /><br /> Null을 허용하지 않습니다.|  
|is_idle|**bit**|1 = 스케줄러가 유휴 상태입니다. 현재 실행되고 있는 작업자가 없습니다. Null을 허용하지 않습니다.|  
|preemptive_switches_count|**int**|이 스케줄러의 작업자가 선점형 모드로 전환한 횟수입니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 외부의 코드(예: 확장 저장 프로시저 및 분산 쿼리)를 실행하려면 비선점형 스케줄러의 제어를 벗어나서 스레드를 실행해야 합니다. 작업자는 이 작업을 수행하기 위해 선점형 모드로 전환합니다.|  
|context_switches_count|**int**|이 스케줄러에 발생한 컨텍스트 전환 횟수입니다. Null을 허용하지 않습니다.<br /><br /> 다른 작업자가 실행될 수 있도록 하려면 현재 실행 중인 작업자가 스케줄러의 제어를 포기하거나 컨텍스트를 전환해야 합니다.<br /><br /> **참고:** 작업 자가 스케줄러를 생성 및 실행 가능한 큐에 자체 배치한를 찾은 후 다른 작업자를 하는 경우 작업 자가 작업 자가 선택 됩니다. 이 경우 context_switches_count는 업데이트되지 않지만 yield_count는 업데이트됩니다.|  
|idle_switches_count|**int**|스케줄러가 유휴 상태인 동안 이벤트를 기다리고 있는 횟수입니다. 이 열은 context_switches_count와 비슷합니다. Null을 허용하지 않습니다.|  
|current_tasks_count|**int**|이 스케줄러와 연관된 현재 태스크 수입니다. 이 개수에는 다음이 포함됩니다.<br /><br /> -모든 작업 자가 실행할 때까지 기다리고 있습니다.<br />-현재 대기 중이거나 (SUSPENDED 또는 RUNNABLE 상태)에서 실행 하는 작업입니다.<br /><br /> 태스크가 완료되면 이 개수가 감소합니다. Null을 허용하지 않습니다.|  
|runnable_tasks_count|**int**|실행 가능한 큐에 예약 대기 중인 태스크가 할당된 작업자 수입니다. Null을 허용하지 않습니다.|  
|current_workers_count|**int**|이 스케줄러와 연결된 작업자 수입니다. 이 개수에는 태스크가 할당되지 않은 작업자가 포함됩니다. Null을 허용하지 않습니다.|  
|active_workers_count|**int**|활성 상태인 작업자 수입니다. 활성 작업자는 비선점형이며 연결된 태스크가 있어야 하고 실행 중이거나 실행 가능하거나 일시 중지 상태입니다. Null을 허용하지 않습니다.|  
|work_queue_count|**bigint**|보류 큐 내의 태스크 수입니다. 작업자의 선택을 기다리고 있는 태스크입니다. Null을 허용하지 않습니다.|  
|pending_disk_io_count|**int**|완료될 때까지 대기하는 보류 중인 I/O 수입니다. 각 스케줄러에는 컨텍스트 전환이 있을 때마다 완료되었는지 여부를 확인하기 위해 검사되는 보류 중인 I/O 목록이 있습니다. 개수는 요청이 삽입될 때 증가하고 요청이 완료되면 감소합니다. 이 숫자는 I/O 상태를 나타내지 않습니다. Null을 허용하지 않습니다.|  
|load_factor|**int**|이 스케줄러에서 감지된 로드를 나타내는 내부 값입니다. 이 값은 새 태스크를 이 스케줄러에 배치할지 다른 스케줄러에 배치할지 결정하는 데 사용되며 이 값은 스케줄러의 로드가 고르지 않을 때 디버깅 작업에 유용합니다. 스케줄러의 로드에 따라 라우팅이 결정됩니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 노드와 스케줄러의 로드 비율을 사용하여 리소스를 얻을 최적의 위치를 결정할 수 있습니다. 태스크가 큐에 배치되면 로드 비율이 증가하고 태스크가 완료되면 로드 비율이 감소합니다. 로드 비율을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OS에서 작업 로드의 균형을 보다 잘 조정하는 데 도움이 됩니다. Null을 허용하지 않습니다.|  
|yield_count|**int**|이 스케줄러에서 진행률을 나타내는 데 사용되는 내부 값입니다. 이 값은 스케줄러 모니터에서 스케줄러의 작업자가 정해진 시간에 다른 작업자로 전환되지 않는지 여부를 확인하는 데 사용됩니다. 이 값은 작업자나 태스크가 새 작업자로 전환되었음을 나타내지 않습니다. Null을 허용하지 않습니다.|  
|last_timer_activity|**bigint**|CPU 틱에서 스케줄러가 마지막으로 스케줄러 타이머 큐를 확인한 시간입니다. Null을 허용하지 않습니다.|  
|failed_to_create_worker|**bit**|이 스케줄러에 새 작업자를 만들 수 없으면 1로 설정됩니다. 일반적으로 메모리 제약 조건 때문에 이러한 상황이 발생합니다. Null을 허용합니다.|  
|active_worker_address|**varbinary(8)**|현재 활성 상태인 작업자의 메모리 주소입니다. Null을 허용합니다. 자세한 내용은 참조 [sys.dm_os_workers &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|memory_object_address|**varbinary(8)**|스케줄러 메모리 개체의 메모리 주소입니다. NULL을 허용하지 않습니다.|  
|task_memory_object_address|**varbinary(8)**|태스크 메모리 개체의 메모리 주소입니다. Null을 허용하지 않습니다. 자세한 내용은 참조 [sys.dm_os_memory_objects &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).|  
|quantum_length_us|**bigint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] SQLOS에 사용 된 스케줄러 퀀텀을 노출 합니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 프리미엄 계층 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층 필요는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정.   
  
## <a name="examples"></a>예  
  
### <a name="a-monitoring-hidden-and-nonhidden-schedulers"></a>1. 숨겨진 스케줄러 및 숨겨지지 않은 스케줄러 모니터링  
 다음 쿼리에서는 모든 스케줄러에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 태스크 및 작업자 상태를 출력합니다. 이 쿼리는 다음 조건을 충족시키는 컴퓨터 시스템에서 실행되었습니다.  
  
-   프로세스(CPU) 두 개  
  
-   NUMA 노드 두 개  
  
-   NUMA 노드당 CPU 한 개  
  
-   `0x03`으로 설정된 선호도 마스크  
  
```  
SELECT  
    scheduler_id,  
    cpu_id,  
    parent_node_id,  
    current_tasks_count,  
    runnable_tasks_count,  
    current_workers_count,  
    active_workers_count,  
    work_queue_count  
  FROM sys.dm_os_schedulers;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
scheduler_id cpu_id parent_node_id current_tasks_count  
------------ ------ -------------- -------------------  
0            1      0              9                    
257          255    0              1                    
1            0      1              10                   
258          255    1              1                    
255          255    32             2                    
  
runnable_tasks_count current_workers_count  
-------------------- ---------------------  
0                    11                     
0                    1                      
0                    18                     
0                    1                      
0                    3                      
  
active_workers_count work_queue_count  
-------------------- --------------------  
6                    0  
1                    0  
8                    0  
1                    0  
1                    0  
```  
  
 이 출력에서는 다음 정보를 제공합니다.  
  
-   5개의 스케줄러가 있습니다. 두 스케줄러의 ID 값은 < 1048576입니다. ID >= 1048576 인 스케줄러를 숨겨진 스케줄러라고 합니다. 스케줄러 `255`는 DAC(관리자 전용 연결)를 나타냅니다. 인스턴스당 하나의 DAC 스케줄러가 있습니다. 메모리 가중을 조정하는 리소스 모니터는 NUMA 노드당 하나씩, 스케줄러 `257`과 스케줄러 `258`을 사용합니다.  
  
-   출력에는 23개의 활성 태스크가 있습니다. 이 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 시작한 리소스 관리 작업과 사용자 요청을 포함합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 태스크의 예로 RESOURCE MONITOR(NUMA 노드당 하나), LAZY WRITER(NUMA 노드당 하나), LOCK MONITOR, CHECKPOINT 및 LOG WRITER가 있습니다.  
  
-   NUMA 노드 `0`은 CPU `1`에 매핑되고 NUMA 노드 `1`은 CPU `0`에 매핑됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 일반적으로 노드 0이 아닌 NUMA 노드에서 시작됩니다.  
  
-   `runnable_tasks_count`가 `0`을 반환하므로 실행 중인 활성 태스크는 없지만 활성 세션은 있을 수 있습니다.  
  
-   DAC를 나타내는 스케줄러 `255`에는 `3`개의 작업자가 연결되어 있습니다. 세 작업자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작 시 할당되며 변경되지 않습니다. 이러한 작업자는 DAC 쿼리를 처리하기 위한 용도로만 사용됩니다. 이 스케줄러의 두 태스크는 연결 관리자와 유휴 작업자를 나타냅니다.  
  
-   `active_workers_count`작업에 연결할 수 있고 비선점형 모드에서 실행 되 고 있는 모든 작업자를 나타냅니다. 네트워크 수신기 같은 일부 태스크는 선점형 일정에서 실행됩니다.  
  
-   숨겨진 스케줄러는 일반적인 사용자 요청을 처리하지 않습니다. 단, DAC 스케줄러는 예외입니다. 이 DAC 스케줄러에는 요청을 처리하는 스레드 하나가 있습니다.  
  
### <a name="b-monitoring-nonhidden-schedulers-in-a-busy-system"></a>2. 사용량이 많은 시스템에서 숨겨지지 않은 스케줄러 모니터링  
 다음 쿼리에서는 사용 가능한 작업자가 처리할 수 없을 만큼 많은 요청이 있는 숨겨지지 않은 과도한 스케줄러의 상태를 보여 줍니다. 이 예에서는 256개의 작업자에 태스크가 할당되어 있습니다. 일부 태스크는 작업자에 할당되기를 기다리고 있습니다. 실행 가능 수가 더 적은 경우 여러 태스크가 하나의 리소스를 기다리고 있음을 의미합니다.  
  
> [!NOTE]  
>  sys.dm_os_workers를 쿼리하여 작업자 상태를 확인할 수 있습니다. 자세한 내용은 참조 [sys.dm_os_workers &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).  
  
 쿼리는 다음과 같습니다.  
  
```  
SELECT  
    scheduler_id,  
    cpu_id,  
    current_tasks_count,  
    runnable_tasks_count,  
    current_workers_count,  
    active_workers_count,  
    work_queue_count  
  FROM sys.dm_os_schedulers  
  WHERE scheduler_id < 255;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
scheduler_id current_tasks_count runnable_tasks_count  
------------ ------------------- --------------------  
0            144                 0                     
1            147                 1                     
  
current_workers_count active_workers_count work_queue_count  
--------------------- -------------------- --------------------  
128                   125                  16  
128                   126                  19  
```  
  
 비교를 위해 다음 결과에서는 작업자를 가져오기 위해 대기하는 작업이 없는 여러 실행 가능 태스크를 보여 줍니다. `work_queue_count`는 두 스케줄러에서 모두 `0`입니다.  
  
```  
scheduler_id current_tasks_count runnable_tasks_count  
------------ ------------------- --------------------  
0            107                 98                    
1            110                 100                   
  
current_workers_count active_workers_count work_queue_count  
--------------------- -------------------- --------------------  
128                   104                  0  
128                   108                  0  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 운영 체제 관련 동적 관리 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


