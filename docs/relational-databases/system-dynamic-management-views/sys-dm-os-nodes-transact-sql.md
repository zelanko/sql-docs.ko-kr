---
description: sys.dm_os_nodes(Transact-SQL)
title: sys. dm_os_nodes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 716b3c816bb5246f91c25869de7e2647a10bbc64
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447641"
---
# <a name="sysdm_os_nodes-transact-sql"></a>sys.dm_os_nodes(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

SQLOS라는 내부 구성 요소는 하드웨어 프로세서 위치와 비슷한 노드 구조를 만듭니다. 이러한 구조는 [소프트 NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md) 를 사용 하 여 변경 하 여 사용자 지정 노드 레이아웃을 만들 수 있습니다.  

> [!NOTE]
> 부터 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 특정 하드웨어 구성에 대해 소프트 NUMA를 자동으로 사용 합니다. 자세한 내용은 [자동 소프트 NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa)를 참조 하세요.
  
다음 표에서는 이러한 노드에 대한 정보를 제공합니다.  
  
> [!NOTE]
> 또는에서이 DMV를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_os_nodes**를 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|노드의 ID입니다.|  
|node_state_desc|**nvarchar(256)**|노드 상태에 대한 설명입니다. 함께 사용할 수 없는 값이 먼저 표시되고 함께 사용할 수 있는 값이 그 다음에 표시됩니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.<br /> Online, Thread Resources Low, Lazy Preemptive<br /><br />상호 배타적인 node_state_desc 값은 네 가지가 있습니다. 이러한 설명은 아래에 나와 있습니다.<br /><ul><li>온라인: 노드가 온라인 상태입니다.<li>오프 라인: 노드가 오프 라인 상태임<li>유휴 상태: 노드에 보류 중인 작업 요청이 없으며 유휴 상태를 입력 했습니다.<li>IDLE_READY: 노드에 보류 중인 작업 요청이 없으며 유휴 상태를 시작할 준비가 되었습니다.</li></ul><br />아래에는 결합할 수 있는 세 가지 node_state_desc 값이 설명 되어 있습니다.<br /><ul><li>DAC:이 노드는 [전용 관리 연결](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)에 대해 예약 되어 있습니다.<li>THREAD_RESOURCES_LOW: 메모리가 부족 하 여이 노드에서 새 스레드를 만들 수 없습니다.<li>핫 추가 됨: 핫 add CPU 이벤트에 대 한 응답으로 노드가 추가 되었음을 나타냅니다.</li></ul>|  
|memory_object_address|**varbinary(8)**|이 노드와 연관된 메모리 개체의 주소입니다. [Dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md). memory_object_address에 대 한 일 대 일 관계입니다.|  
|memory_clerk_address|**varbinary(8)**|이 노드와 연관된 메모리 클럭의 주소입니다. [Dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md). memory_clerk_address에 대 한 일 대 일 관계입니다.|  
|io_completion_worker_address|**varbinary(8)**|이 노드에 대한 IO 완료가 할당된 작업자의 주소입니다. [Dm_os_workers](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md). worker_address에 대 한 일 대 일 관계입니다.|  
|memory_node_id|**smallint**|이 노드가 속한 메모리 노드의 ID입니다. [Dm_os_memory_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md). memory_node_id에 대 한 다대일 관계입니다.|  
|cpu_affinity_mask|**bigint**|이 노드와 연관된 CPU를 식별하는 비트맵입니다.|  
|online_scheduler_count|**smallint**|이 노드에서 관리 하는 온라인 스케줄러 수입니다.|  
|idle_scheduler_count|**smallint**|활성 작업자가 없는 온라인 스케줄러 수입니다.|  
|active_worker_count|**int**|이 노드에서 관리하는 모든 스케줄러에서 활성 상태인 작업자의 수입니다.|  
|avg_load_balance|**int**|이 노드의 스케줄러당 평균 태스크 수입니다.|  
|timer_task_affinity_mask|**bigint**|타이머 태스크가 할당될 수 있는 스케줄러를 식별하는 비트맵입니다.|  
|permanent_task_affinity_mask|**bigint**|영구 태스크가 할당될 수 있는 스케줄러를 식별하는 비트맵입니다.|  
|resource_monitor_state|**bit**|각 노드에는 한 개의 할당된 리소스 모니터가 있습니다. 리소스 모니터는 실행 중이거나 유휴 상태일 수 있습니다. 값이 1이면 실행 중이고 0이면 유휴 상태를 나타냅니다.|  
|online_scheduler_mask|**bigint**|이 노드에 대한 프로세스 선호도 마스크를 식별합니다.|  
|processor_group|**smallint**|이 노드에 대한 프로세서 그룹을 식별합니다.|  
|cpu_count |**int** |이 노드에 사용할 수 있는 Cpu 수입니다. |
|pdw_node_id|**int**|이 배포가 설정 된 노드의 식별자입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="see-also"></a>관련 항목    
 [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Soft-NUMA&#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
