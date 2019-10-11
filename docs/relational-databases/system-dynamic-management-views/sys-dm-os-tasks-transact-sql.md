---
title: _os_tasks (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 69fb7b1e0d9f98ec7d00441613a8887a81c4567c
ms.sourcegitcommit: aece9f7db367098fcc0c508209ba243e05547fe1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72260429"
---
# <a name="sysdm_os_tasks-transact-sql"></a>sys.dm_os_tasks(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 활성 상태인 각 태스크에 대해 하나의 행을 반환합니다. 작업에 대 한 자세한 내용은 [스레드 및 태스크 아키텍처 가이드](../../relational-databases/thread-and-task-architecture-guide.md)를 참조 하세요.
  
> [!NOTE]  
> @No__t-0 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서이를 호출 하려면 **_pdw_nodes_os_tasks**이름을 사용 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|개체의 메모리 주소입니다.|  
|**task_state**|**nvarchar(60)**|태스크의 상태입니다. 다음 중 하나일 수 있습니다.<br /><br /> 작업이 작업자 스레드 대기 중입니다.<br /><br /> 실행할 실행 가능 하지만 퀀텀 수신을 대기 중입니다.<br /><br /> 이상을 현재 스케줄러에서 실행 중입니다.<br /><br /> 일시 에는 작업자가 있지만 이벤트를 기다리고 있습니다.<br /><br /> 끝났습니다 작업이.<br /><br /> SPINLOOP: Spinlock에 걸려 있습니다.|  
|**context_switches_count**|**int**|이 태스크로 완료된 스케줄러 컨텍스트 전환 수입니다.|  
|**pending_io_count**|**int**|이 태스크로 수행된 실제 I/O 수입니다.|  
|**pending_io_byte_count**|**bigint**|이 태스크로 수행된 I/O의 총 바이트 수입니다.|  
|**pending_io_byte_average**|**int**|이 태스크로 수행된 I/O의 평균 바이트 수입니다.|  
|**scheduler_id**|**int**|부모 스케줄러의 ID이며 이 태스크의 스케줄러 정보에 대한 핸들입니다. 자세한 내용은 [_os_schedulers &#40;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)를 참조 하세요.|  
|**session_id**|**smallint**|태스크와 연결된 세션의 ID입니다.|  
|**exec_context_id**|**int**|태스크와 연결된 실행 컨텍스트 ID입니다.|  
|**request_id**|**int**|태스크 요청 ID입니다. 자세한 내용은 [_exec_requests &#40;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)를 참조 하세요.|  
|**worker_address**|**varbinary(8)**|태스크를 실행하고 있는 작업자의 메모리 주소입니다.<br /><br /> NULL = 작업자가 실행할 수 있을 때까지 태스크가 기다리고 있거나 방금 작업 실행이 완료되었습니다.<br /><br /> 자세한 내용은 [_os_workers &#40;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)를 참조 하세요.|  
|**host_address**|**varbinary(8)**|호스트의 메모리 주소입니다.<br /><br /> 0 = 호스팅이 태스크 만들기에 사용되지 않았습니다. 이 값은 이 태스크를 만드는 데 사용된 호스트를 식별하는 데 유용합니다.<br /><br /> 자세한 내용은 [_os_hosts &#40;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md)를 참조 하세요.|  
|**parent_task_address**|**varbinary(8)**|개체의 부모인 태스크의 메모리 주소입니다.|  
|**pdw_node_id**|**int**|**적용**대상: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], @no__t<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한
@No__t-0에서 `VIEW SERVER STATE` 권한이 필요 합니다.   
@No__t-0 Premium 계층에서는 데이터베이스에 대 한 `VIEW DATABASE STATE` 권한이 필요 합니다. @No__t-0 표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="examples"></a>예  
  
### <a name="a-monitoring-parallel-requests"></a>A. 병렬 요청 모니터링  
 병렬로 실행 되는 요청의 경우 동일한 조합 (\<**session_id**>, \<**request_id**>)에 대해 여러 개의 행이 표시 됩니다. 다음 쿼리를 사용 하 여 모든 활성 요청에 대 한 [최대 병렬 처리 수준 서버 구성 옵션](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 을 찾을 수 있습니다.  
  
> [!NOTE]  
>  **Request_id** 는 세션 내에서 고유 합니다.  
  
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
  
### <a name="b-associating-session-ids-with-windows-threads"></a>2\. Windows 스레드와 세션 ID 연결  
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
  
## <a name="see-also"></a>관련 항목  
[SQL Server 운영 체제 관련 동적 관리 뷰 &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)    
[스레드 및 태스크 아키텍처 가이드](../../relational-databases/thread-and-task-architecture-guide.md)     
  


