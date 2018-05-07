---
title: sys.dm_os_tasks (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_tasks
- sys.dm_os_tasks_TSQL
- dm_os_tasks_TSQL
- dm_os_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_tasks dynamic management view
ms.assetid: 180a3c41-e71b-4670-819d-85ea7ef98bac
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b2c142bd8ca0e4efc29b0157d88d8b35e766c534
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmostasks-transact-sql"></a>sys.dm_os_tasks(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 활성 상태인 각 태스크에 대해 하나의 행을 반환합니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_tasks**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|개체의 메모리 주소입니다.|  
|**task_state**|**nvarchar(60)**|태스크의 상태입니다. 다음 중 하나일 수 있습니다.<br /><br /> 보류 중: 작업자 스레드를 기다리고 있습니다.<br /><br /> RUNNABLE: 가능 하지만 퀀텀 수신 대기 합니다.<br /><br /> 실행 중: 현재 스케줄러에서 실행 합니다.<br /><br /> 일시 중단 됨: 작업 자가 있지만 이벤트를 대기 합니다.<br /><br /> 완료: 완료 합니다.<br /><br /> SPINLOOP: spinlock에 걸려 있습니다.|  
|**context_switches_count**|**int**|이 태스크로 완료된 스케줄러 컨텍스트 전환 수입니다.|  
|**pending_io_count**|**int**|이 태스크로 수행된 실제 I/O 수입니다.|  
|**pending_io_byte_count**|**bigint**|이 태스크로 수행된 I/O의 총 바이트 수입니다.|  
|**pending_io_byte_average**|**int**|이 태스크로 수행된 I/O의 평균 바이트 수입니다.|  
|**scheduler_id**|**int**|부모 스케줄러의 ID이며 이 태스크의 스케줄러 정보에 대한 핸들입니다. 자세한 내용은 참조 [sys.dm_os_schedulers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)합니다.|  
|**session_id**|**smallint**|태스크와 연결된 세션의 ID입니다.|  
|**exec_context_id**|**int**|태스크와 연결된 실행 컨텍스트 ID입니다.|  
|**request_id**|**int**|태스크 요청 ID입니다. 자세한 내용은 참조 [sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)합니다.|  
|**worker_address**|**varbinary(8)**|태스크를 실행하고 있는 작업자의 메모리 주소입니다.<br /><br /> NULL = 작업자가 실행할 수 있을 때까지 태스크가 기다리고 있거나 방금 작업 실행이 완료되었습니다.<br /><br /> 자세한 내용은 참조 [sys.dm_os_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)합니다.|  
|**host_address**|**varbinary(8)**|호스트의 메모리 주소입니다.<br /><br /> 0 = 호스팅이 태스크 만들기에 사용되지 않았습니다. 이 값은 이 태스크를 만드는 데 사용된 호스트를 식별하는 데 유용합니다.<br /><br /> 자세한 내용은 참조 [sys.dm_os_hosts &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md)합니다.|  
|**parent_task_address**|**varbinary(8)**|개체의 부모인 태스크의 메모리 주소입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   

## <a name="examples"></a>예  
  
### <a name="a-monitoring-parallel-requests"></a>1. 병렬 요청 모니터링  
 동시에 실행 되는 요청에 대 한 여러 행의 동일한 조합에 대해 표시 됩니다 (\<**session_id**>, \< **request_id**>). 다음 쿼리를 사용 하 여 찾을 수는 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 모든 활성 요청에 대 한 합니다.  
  
> [!NOTE]  
>  A **request_id** 는 세션 내에서 고유 합니다.  
  
```  
SELECT  
    task_address,  
    task_state,  
    context_switches_count,  
    pending_io_count,  
    pending_io_byte_count,  
    pending_io_byte_average,  
    scheduler_id,  
    session_id,  
    exec_context_id,  
    request_id,  
    worker_address,  
    host_address  
  FROM sys.dm_os_tasks  
  ORDER BY session_id, request_id;  
```  
  
### <a name="b-associating-session-ids-with-windows-threads"></a>2. Windows 스레드와 세션 ID 연결  
 다음 쿼리를 사용하여 세션 ID 값을 Windows 스레드 ID와 연결할 수 있습니다. 그런 다음 Windows 성능 모니터에서 스레드의 성능을 모니터링할 수 있습니다. 다음 쿼리는 중지 상태인 세션에 대한 정보를 반환하지 않습니다.  
  
```  
SELECT STasks.session_id, SThreads.os_thread_id  
  FROM sys.dm_os_tasks AS STasks  
  INNER JOIN sys.dm_os_threads AS SThreads  
    ON STasks.worker_address = SThreads.worker_address  
  WHERE STasks.session_id IS NOT NULL  
  ORDER BY STasks.session_id;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
  [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


