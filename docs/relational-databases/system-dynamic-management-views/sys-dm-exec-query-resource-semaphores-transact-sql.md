---
title: sys.dm_exec_query_resource_semaphores (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
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
- sys.dm_exec_query_resource_semaphores_TSQL
- dm_exec_query_resource_semaphores_TSQL
- sys.dm_exec_query_resource_semaphores
- dm_exec_query_resource_semaphores
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_resource_semaphores dynamic management view
ms.assetid: e43a2aa9-dd52-4c89-911e-1a7d05f7ffbb
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: dca59c6557e951922fa19ebd95526aab5149b9fd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecqueryresourcesemaphores-transact-sql"></a>sys.dm_exec_query_resource_semaphores(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 현재 쿼리 리소스 세마포 상태에 대한 정보를 반환합니다. **sys.dm_exec_query_resource_semaphores** 일반적인 쿼리 실행 메모리 상태를 제공 하며, 시스템 메모리가 부족 하 여 액세스할 수 있는지 여부를 확인할 수 있습니다. 이 보기에서 가져온 메모리 정보를 보완 [sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md) 서버 메모리 상태의 전체 현황을 수 있도록 합니다. **sys.dm_exec_query_resource_semaphores** 작은 쿼리 리소스 세마포에 대 한 다른 행과 일반 리소스 세마포와 대 한 한 행 반환 합니다. 작은 쿼리 세마포에 대 한 두 가지 요구 사항이 있습니다.  
  
-   요청한 메모리 부여 5MB 미만 이어야 합니다.  
  
-   쿼리 비용 보다 작거나 3 비용 단위 있어야 합니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_exec_query_resource_semaphores**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**resource_semaphore_id**|**smallint**|리소스 세마포의 고유하지 않은 ID입니다. 일반 리소스 세마포의 경우 0을 반환하고 작은 쿼리 리소스 세마포의 경우 1을 반환합니다.|  
|**target_memory_kb**|**bigint**|메모리 사용 대상(KB)을 부여합니다.|  
|**max_target_memory_kb**|**bigint**|가능한 최대 대상(KB)입니다. 작은 쿼리 리소스 세마포의 경우 NULL이 됩니다.|  
|**total_memory_kb**|**bigint**|리소스 세마포가 보유한 메모리(KB)입니다. 시스템 메모리가 부족 하거나 강제 적용 된 최소 메모리가 자주 부여 되는 경우이 값 보다 클 수는 **target_memory_kb** 또는 **max_target_memory_kb** 값입니다. 총 메모리는 사용 가능한 메모리와 부여된 메모리의 합계입니다.|  
|**available_memory_kb**|**bigint**|새 부여에 사용 가능한 메모리(KB)입니다.|  
|**granted_memory_kb**|**bigint**|부여된 총 메모리(KB)입니다.|  
|**used_memory_kb**|**bigint**|부여된 메모리 중에서 실제로 사용된 메모리(KB)입니다.|  
|**grantee_count**|**int**|부여가 만족된 활성 쿼리 수입니다.|  
|**waiter_count**|**int**|부여가 만족될 때까지 대기 중인 쿼리 수입니다.|  
|**timeout_error_count**|**bigint**|서버 시작 후 시간 초과 오류의 총 수입니다. 작은 쿼리 리소스 세마포의 경우 NULL이 됩니다.|  
|**forced_grant_count**|**bigint**|서버 시작 후 강제 적용된 최소 메모리 부여의 총 수입니다. 작은 쿼리 리소스 세마포의 경우 NULL이 됩니다.|  
|**pool_id**|**int**|이 리소스 세마포가 속한 리소스 풀의 ID입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   
  
## <a name="remarks"></a>주의  
 쿼리에서 ORDER BY 또는 집계가 포함된 동적 관리 뷰를 사용하는 경우 메모리 사용이 증가하여 해결하려는 문제가 악화될 수 있습니다.  
  
 사용 하 여 **sys.dm_exec_query_resource_semaphores** 문제 해결을 위한 하지만 이후 버전을 사용 하는 응용 프로그램에서 포함 하지 않음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 데이터베이스 관리자는 리소스 관리자 기능을 사용하여 서버 리소스를 최대 20개의 리소스 풀에 배치할 수 있습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상에서 각 풀은 독립된 작은 서버 인스턴스와 같이 작동하며 2개의 세마포가 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [실행 관련 동적 관리 뷰 및 함수 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
  
  


