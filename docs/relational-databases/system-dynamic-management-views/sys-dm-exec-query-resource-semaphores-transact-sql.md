---
description: sys.dm_exec_query_resource_semaphores(Transact-SQL)
title: sys.dm_exec_query_resource_semaphores (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b93ec6457b9dd3b78ed303dbfd819f9bb66dbb65
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484715"
---
# <a name="sysdm_exec_query_resource_semaphores-transact-sql"></a>sys.dm_exec_query_resource_semaphores(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 현재 쿼리 리소스 세마포 상태에 대한 정보를 반환합니다. **sys.dm_exec_query_resource_semaphores** 일반적인 쿼리 실행 메모리 상태를 제공 하며 시스템에서 충분 한 메모리에 액세스할 수 있는지 여부를 확인할 수 있습니다. 이 보기는 [sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md) 에서 얻은 메모리 정보를 보완 하 여 서버 메모리 상태에 대 한 전체 그림을 제공 합니다. **sys.dm_exec_query_resource_semaphores** 는 일반 리소스 세마포에 대해 한 행을 반환 하 고, 작은 쿼리 리소스 세마포의 경우 다른 행을 반환 합니다. 작은 쿼리 세마포에는 다음과 같은 두 가지 요구 사항이 있습니다.  
  
-   요청 된 메모리 부여는 5mb 미만 이어야 합니다.  
  
-   쿼리 비용은 3 개의 비용 단위 미만 이어야 합니다.  
  
> [!NOTE]  
>  또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **sys.dm_pdw_nodes_exec_query_resource_semaphores** 이름을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**resource_semaphore_id**|**smallint**|리소스 세마포의 고유하지 않은 ID입니다. 일반 리소스 세마포의 경우 0을 반환하고 작은 쿼리 리소스 세마포의 경우 1을 반환합니다.|  
|**target_memory_kb**|**bigint**|메모리 사용 대상(KB)을 부여합니다.|  
|**max_target_memory_kb**|**bigint**|가능한 최대 대상(KB)입니다. 작은 쿼리 리소스 세마포의 경우 NULL이 됩니다.|  
|**total_memory_kb**|**bigint**|리소스 세마포가 보유한 메모리(KB)입니다. 시스템의 메모리가 부족 하거나 강제 적용 된 최소 메모리가 자주 부여 되는 경우이 값은 **target_memory_kb** 또는 **max_target_memory_kb** 값 보다 클 수 있습니다. 총 메모리는 사용 가능한 메모리와 부여된 메모리의 합계입니다.|  
|**available_memory_kb**|**bigint**|새 부여에 사용 가능한 메모리(KB)입니다.|  
|**granted_memory_kb**|**bigint**|부여된 총 메모리(KB)입니다.|  
|**used_memory_kb**|**bigint**|부여된 메모리 중에서 실제로 사용된 메모리(KB)입니다.|  
|**grantee_count**|**int**|부여가 만족된 활성 쿼리 수입니다.|  
|**waiter_count**|**int**|부여가 만족될 때까지 대기 중인 쿼리 수입니다.|  
|**timeout_error_count**|**bigint**|서버 시작 후 시간 초과 오류의 총 수입니다. 작은 쿼리 리소스 세마포의 경우 NULL이 됩니다.|  
|**forced_grant_count**|**bigint**|서버 시작 후 강제 적용된 최소 메모리 부여의 총 수입니다. 작은 쿼리 리소스 세마포의 경우 NULL이 됩니다.|  
|**pool_id**|**int**|이 리소스 세마포가 속한 리소스 풀의 ID입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   
  
## <a name="remarks"></a>설명  
 쿼리에서 ORDER BY 또는 집계가 포함된 동적 관리 뷰를 사용하는 경우 메모리 사용이 증가하여 해결하려는 문제가 악화될 수 있습니다.  
  
 문제 해결을 위해 **sys.dm_exec_query_resource_semaphores** 를 사용 하지만 이후 버전의를 사용 하는 응용 프로그램에는이를 포함 하지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 데이터베이스 관리자는 리소스 관리자 기능을 사용하여 서버 리소스를 최대 20개의 리소스 풀에 배치할 수 있습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상에서 각 풀은 독립된 작은 서버 인스턴스와 같이 작동하며 2개의 세마포가 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;관련 동적 관리 뷰 및 함수 실행 ](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
  
  


