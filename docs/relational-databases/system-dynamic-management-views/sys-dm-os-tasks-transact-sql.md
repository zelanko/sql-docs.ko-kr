---
description: sys.dm_os_tasks(Transact-SQL)
title: sys.dm_os_tasks (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: df071060cce4000908ffb8d7ab10e6e6b9e7f9f8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468424"
---
# <a name="sysdm_os_tasks-transact-sql"></a>sys.dm_os_tasks(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 활성 상태인 각 태스크에 대해 하나의 행을 반환합니다. 작업은 SQL Server의 기본 실행 단위입니다. 작업의 예로는 쿼리, 로그인, 로그 아웃 및 삭제할 정리 작업, 검사점 작업, 로그 작성기, 병렬 다시 실행 작업 등의 시스템 태스크가 있습니다. 작업에 대 한 자세한 내용은 [스레드 및 태스크 아키텍처 가이드](../../relational-databases/thread-and-task-architecture-guide.md)를 참조 하세요.
  
> [!NOTE]  
> 또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **sys.dm_pdw_nodes_os_tasks** 이름을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|개체의 메모리 주소입니다.|  
|**task_state**|**nvarchar(60)**|태스크의 상태입니다. 다음 중 하나일 수 있습니다.<br /><br /> 보류 중: 작업자 스레드를 기다리고 있습니다.<br /><br /> 실행 가능: 실행 가능 하지만 퀀텀 수신을 대기 중입니다.<br /><br /> 실행 중: 현재 스케줄러에서 실행 중입니다.<br /><br /> SUSPENDED: 작업자를 포함 하지만 이벤트를 기다리고 있습니다.<br /><br /> 완료 됨: 완료 됨.<br /><br /> SPINLOOP: spinlock에 걸려 있습니다.|  
|**context_switches_count**|**int**|이 태스크로 완료된 스케줄러 컨텍스트 전환 수입니다.|  
|**pending_io_count**|**int**|이 태스크로 수행된 실제 I/O 수입니다.|  
|**pending_io_byte_count**|**bigint**|이 태스크로 수행된 I/O의 총 바이트 수입니다.|  
|**pending_io_byte_average**|**int**|이 태스크로 수행된 I/O의 평균 바이트 수입니다.|  
|**scheduler_id**|**int**|부모 스케줄러의 ID이며 이 태스크의 스케줄러 정보에 대한 핸들입니다. 자세한 내용은 [sys.dm_os_schedulers &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)를 참조 하세요.|  
|**session_id**|**smallint**|태스크와 연결된 세션의 ID입니다.|  
|**exec_context_id**|**int**|태스크와 연결된 실행 컨텍스트 ID입니다.|  
|**request_id**|**int**|태스크 요청 ID입니다. 자세한 내용은 [sys.dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)를 참조 하세요.|  
|**worker_address**|**varbinary(8)**|태스크를 실행하고 있는 작업자의 메모리 주소입니다.<br /><br /> NULL = 작업자가 실행할 수 있을 때까지 태스크가 기다리고 있거나 방금 작업 실행이 완료되었습니다.<br /><br /> 자세한 내용은 [sys.dm_os_workers &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)를 참조 하세요.|  
|**host_address**|**varbinary(8)**|호스트의 메모리 주소입니다.<br /><br /> 0 = 호스팅이 태스크 만들기에 사용되지 않았습니다. 이 값은 이 태스크를 만드는 데 사용된 호스트를 식별하는 데 유용합니다.<br /><br /> 자세한 내용은 [sys.dm_os_hosts &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md)를 참조 하세요.|  
|**parent_task_address**|**varbinary(8)**|개체의 부모인 태스크의 메모리 주소입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한
에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   

## <a name="examples"></a>예  
  
### <a name="a-monitoring-parallel-requests"></a>A. 병렬 요청 모니터링  
 병렬로 실행 되는 요청의 경우 동일한 조합 (,)에 대해 여러 행이 표시 됩니다 \<**session_id**> \<**request_id**> . 다음 쿼리를 사용 하 여 모든 활성 요청에 대 한 [최대 병렬 처리 수준 서버 구성 옵션](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 을 찾을 수 있습니다.  
  
> [!NOTE]  
>  **Request_id** 는 세션 내에서 고유 합니다.  
  
```sql  
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
  
### <a name="b-associating-session-ids-with-windows-threads"></a>B. Windows 스레드와 세션 ID 연결  
 다음 쿼리를 사용하여 세션 ID 값을 Windows 스레드 ID와 연결할 수 있습니다. 그런 다음 Windows 성능 모니터에서 스레드의 성능을 모니터링할 수 있습니다. 다음 쿼리는 중지 상태인 세션에 대한 정보를 반환하지 않습니다.  
  
```sql  
SELECT STasks.session_id, SThreads.os_thread_id  
  FROM sys.dm_os_tasks AS STasks  
  INNER JOIN sys.dm_os_threads AS SThreads  
    ON STasks.worker_address = SThreads.worker_address  
  WHERE STasks.session_id IS NOT NULL  
  ORDER BY STasks.session_id;  
GO  
```  

## <a name="see-also"></a>참고 항목  
[Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)    
[스레드 및 태스크 아키텍처 가이드](../../relational-databases/thread-and-task-architecture-guide.md)     
  


