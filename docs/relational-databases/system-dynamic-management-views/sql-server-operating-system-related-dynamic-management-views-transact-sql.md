---
title: SQL Server 운영 체제 관련 동적 관리 뷰 (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operating systems [SQL Server], dynamic management objects
- SQL Operating System dynamic management objects [SQL Server]
- SQL OS dynamic management objects [SQL Server]
- dynamic management objects [SQL Server], SQL OS
ms.assetid: 3030c86a-0a74-4fed-ac0f-392e244cb965
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ac714a00dcc4b5a858d12ca0789a44e4c9ebb30e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702811"
---
# <a name="sql-server-operating-system-related-dynamic-management-views-transact-sql"></a>SQL Server 운영 체제 관련 동적 관리 뷰(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 섹션에서는 SQLOS([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 운영 체제)와 관련된 동적 관리 뷰에 대해 다룹니다. SQLOS는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 관련된 운영 체제 리소스를 관리합니다.  
  
|||  
|-|-|  
|[sys.dm_os_buffer_descriptors&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)|[sys.dm_os_memory_pools &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-pools-transact-sql.md)|  
|[sys.dm_os_child_instances &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-child-instances-transact-sql.md)|[sys.dm_os_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql.md)|  
|[sys.dm_os_cluster_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)|[sys.dm_os_performance_counters&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)|  
|[sys.dm_os_dispatcher_pools&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-dispatcher-pools-transact-sql.md)|[sys.dm_os_process_memory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-process-memory-transact-sql.md)|  
|[sys.dm_os_host_info &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)|[sys.dm_os_schedulers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)|  
|[sys.dm_os_hosts &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md)|[sys.dm_os_stacks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-stacks-transact-sql.md)|  
|[sys.dm-os-작업-개체 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-job-object-transact-sql.md)||
|[sys.dm_os_latch_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)|[sys.dm_os_sys_info&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)|  
|[sys.dm_os_loaded_modules &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql.md)|[sys.dm_os_sys_memory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-memory-transact-sql.md)|  
|[sys.dm_os_memory_brokers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-brokers-transact-sql.md)|[sys.dm_os_tasks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)|  
|[sys.dm_os_memory_cache_clock_hands &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-clock-hands-transact-sql.md)|[sys.dm_os_threads &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)|  
|[sys.dm_os_memory_cache_counters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md)|[sys.dm_os_virtual_address_dump &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-virtual-address-dump-transact-sql.md)|  
|[sys.dm_os_memory_cache_entries &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)|[sys.dm_os_volume_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-volume-stats-transact-sql.md)|  
|[sys.dm_os_memory_cache_hash_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-hash-tables-transact-sql.md)|[sys.dm_os_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
|[sys.dm_os_memory_clerks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)|[sys.dm_os_waiting_tasks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md)|  
|[sys.dm_os_memory_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md)|[sys.dm_os_windows_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)|  
|[sys.dm_os_memory_objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)|[sys.dm_os_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)|  
  
 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 운영 체제 관련 동적 관리 뷰는 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]입니다.  
  
|||  
|-|-|  
|**sys.dm_os_function_symbolic_name**|**sys.dm_os_ring_buffers**|  
|**sys.dm_os_memory_allocations**|**sys.dm_os_sublatches**|  
|**sys.dm_os_worker_local_storage**||  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

