---
title: sys.dm_os_nodes (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7c8cab567bb954ee779fa7efcce032061568cd7a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

SQLOS라는 내부 구성 요소는 하드웨어 프로세서 위치와 비슷한 노드 구조를 만듭니다. 이러한 구조를 사용 하 여 변경할 수 있습니다 [소프트 NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md) 사용자 지정 노드 레이아웃을 만드는 합니다.  

> [!NOTE]
> 부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 특정 하드웨어 구성에 대 한 소프트 NUMA를 자동으로 사용 됩니다. 자세한 내용은 참조 [자동 SOFT-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa)합니다.
  
다음 표에서는 이러한 노드에 대한 정보를 제공합니다.  
  
> [!NOTE]
> 이 DMV를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_nodes**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|노드의 ID입니다.|  
|node_state_desc|**nvarchar(256)**|노드 상태에 대한 설명입니다. 함께 사용할 수 없는 값이 먼저 표시되고 함께 사용할 수 있는 값이 그 다음에 표시됩니다. 예를 들어:<br /> Online, Thread Resources Low, Lazy Preemptive<br /><br />4 개의 상호 배타적인 node_state_desc 값은. 와 해당 설명을 보려면 아래 나열 되어 있습니다.<br /><ul><li>온라인: 노드가 온라인 상태입니다.<li>오프 라인: 노드는 오프 라인<li>유휴: 노드에 보류 중인 작업 요청이 없으면 있으며 유휴 상태가 되었습니다.<li>IDLE_READY: 노드에 보류 중인 작업 요청이 더는 있으며 유휴 상태로 진입할 준비가 되었습니다.</li></ul><br />와 해당 설명을 보려면 아래에 나열 된 3 개의 combinable node_state_desc 값은.<br /><ul><li>DAC:이 노드에서 예약 되어는 [전용 관리 연결](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)합니다.<li>THREAD_RESOURCES_LOW: 없음 새 스레드를 만들 수이 노드에서 메모리 부족 상태로 인해 합니다.<li>HOT ADDED: 대 한 응답으로 노드가 추가 되었음을 나타냅니다는 hot add CPU 이벤트입니다.</li></ul>|  
|memory_object_address|**varbinary(8)**|이 노드와 연관된 메모리 개체의 주소입니다. 한 일 관계를 [sys.dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).memory_object_address 합니다.|  
|memory_clerk_address|**varbinary(8)**|이 노드와 연관된 메모리 클럭의 주소입니다. 한 일 관계를 [sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).memory_clerk_address 합니다.|  
|io_completion_worker_address|**varbinary(8)**|이 노드에 대한 IO 완료가 할당된 작업자의 주소입니다. 한 일 관계를 [sys.dm_os_workers](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).worker_address 합니다.|  
|memory_node_id|**smallint**|이 노드가 속한 메모리 노드의 ID입니다. 다 대 일 관계 [sys.dm_os_memory_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md).memory_node_id 합니다.|  
|cpu_affinity_mask|**bigint**|이 노드와 연관된 CPU를 식별하는 비트맵입니다.|  
|online_scheduler_count|**smallint**|이 노드에서 관리 되는 온라인 스케줄러 수입니다.|  
|idle_scheduler_count|**smallint**|활성 작업자가 없는 온라인 스케줄러 수입니다.|  
|active_worker_count|**int**|이 노드에서 관리하는 모든 스케줄러에서 활성 상태인 작업자의 수입니다.|  
|avg_load_balance|**int**|이 노드의 스케줄러당 평균 태스크 수입니다.|  
|timer_task_affinity_mask|**bigint**|타이머 태스크가 할당될 수 있는 스케줄러를 식별하는 비트맵입니다.|  
|permanent_task_affinity_mask|**bigint**|영구 태스크가 할당될 수 있는 스케줄러를 식별하는 비트맵입니다.|  
|resource_monitor_state|**bit**|각 노드에는 한 개의 할당된 리소스 모니터가 있습니다. 리소스 모니터는 실행 중이거나 유휴 상태일 수 있습니다. 값이 1이면 실행 중이고 0이면 유휴 상태를 나타냅니다.|  
|online_scheduler_mask|**bigint**|이 노드에 대한 프로세스 선호도 마스크를 식별합니다.|  
|processor_group|**smallint**|이 노드에 대한 프로세서 그룹을 식별합니다.|  
|cpu_count |**int** |이 노드에 대 한 사용 가능한 Cpu의 수입니다. |
|pdw_node_id|**int**|이 배포에 있는 노드에 대 한 식별자입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permissions

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   

## <a name="see-also"></a>관련 항목:    
 [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Soft-NUMA&#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
