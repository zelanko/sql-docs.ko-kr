---
title: sys.dm_exec_query_memory_grants (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_memory_grants_TSQL
- sys.dm_exec_query_memory_grants
- sys.dm_exec_query_memory_grants_TSQL
- dm_exec_query_memory_grants
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_memory_grants dynamic management view
ms.assetid: 2c417747-2edd-4e0d-8a9c-e5f445985c1a
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7a72c642fe09f754d2c201a50bb00baa346e6a43
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43069319"
---
# <a name="sysdmexecquerymemorygrants-transact-sql"></a>sys.dm_exec_query_memory_grants(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  요청한 메모리 부여를 대기 및 메모리 부여 받은 모든 쿼리에 대 한 정보를 반환 합니다. 쿼리 메모리 부여 하지 않아도 되는이 뷰에 나타나지 않습니다. 예를 들어, 정렬 및 해시 조인 작업이 없이 쿼리 하는 동안 쿼리 실행 메모리 부여를가지고 **ORDER BY** 절 메모리 부여 수는 없습니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이러한 정보 노출을 방지하기 위해 연결된 테넌트에 속하지 않는 데이터가 포함된 행은 모두 필터링됩니다. 또한 열에 값 **scheduler_id**, **wait_order**, **pool_id**, **group_id** 필터링 되 열 값 설정 NULL입니다.  
  
> [!NOTE]  
> 이를 호출 하 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_exec_query_memory_grants**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|이 쿼리가 실행되고 있는 세션의 ID(SPID)입니다.|  
|**request_id**|**int**|요청의 ID입니다. 세션의 컨텍스트에서 고유합니다.|  
|**scheduler_id**|**int**|이 쿼리를 예약하고 있는 스케줄러의 ID입니다.|  
|**dop**|**smallint**|이 쿼리의 병렬 처리 수준입니다.|  
|**request_time**|**datetime**|이 쿼리가 메모리 부여를 요청한 날짜와 시간입니다.|  
|**grant_time**|**datetime**|이 쿼리에 메모리가 부여된 날짜와 시간입니다. 아직 메모리가 부여되지 않은 경우 NULL이 됩니다.|  
|**requested_memory_kb**|**bigint**|요청된 총 메모리 양(KB)입니다.|  
|**granted_memory_kb**|**bigint**|실제로 부여된 총 메모리 양(KB)입니다. 아직 메모리가 부여되지 않은 경우 NULL이 될 수 있습니다. 일반적인 상황에서이 값은 여야 동일 **requested_memory_kb**합니다. 인덱스 생성 시에는 서버가 처음 부여된 메모리 외에 요청 시 메모리를 추가로 허용할 수 있습니다.|  
|**required_memory_kb**|**bigint**|이 쿼리를 실행하는 데 필요한 최소 메모리(KB)입니다. **requested_memory_kb** 동일이 양보다 크거나 합니다.|  
|**used_memory_kb**|**bigint**|현재 사용된 실제 메모리(KB)입니다.|  
|**max_used_memory_kb**|**bigint**|현재까지 사용된 최대 실제 메모리(KB)입니다.|  
|**query_cost**|**float**|예상 쿼리 비용입니다.|  
|**timeout_sec**|**int**|이 쿼리가 메모리 부여 요청을 포기하기까지의 제한 시간(초)입니다.|  
|**resource_semaphore_id**|**smallint**|이 쿼리가 대기 중인 리소스 세마포의 고유하지 않은 ID입니다.<br /><br /> **참고:** 이 ID는 고유 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 이전의 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. 이러한 변경 내용은 쿼리 실행 문제를 해결하는 데 영향을 줄 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "주의" 섹션을 참조하세요.|  
|**queue_id**|**smallint**|이 쿼리가 메모리 부여를 기다리는 대기 큐의 ID입니다. 메모리가 이미 부여된 경우 NULL이 됩니다.|  
|**wait_order**|**int**|지정 된 대기 쿼리의 순서 대로 **queue_id**합니다. 다른 쿼리가 메모리 부여를 얻거나 시간 초과될 경우 지정된 쿼리에 대해 이 값이 변경될 수 있습니다. 메모리가 이미 부여된 경우 NULL이 됩니다.|  
|**is_next_candidate**|**bit**|다음 메모리 부여 후보입니다.<br /><br /> 1 = 예<br /><br /> 0 = 아니요<br /><br /> NULL = 메모리가 이미 부여된 경우|  
|**wait_time_ms**|**bigint**|대기 시간(밀리초)입니다. 메모리가 이미 부여된 경우 NULL이 됩니다.|  
|**plan_handle**|**varbinary(64)**|이 쿼리 계획의 식별자입니다. 사용 하 여 **sys.dm_exec_query_plan** 실제 XML 계획을 추출 합니다.|  
|**sql_handle**|**varbinary(64)**|이 쿼리에 대한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 텍스트의 식별자입니다. 사용 하 여 **sys.dm_exec_sql_text** 가져오려면 실제 [!INCLUDE[tsql](../../includes/tsql-md.md)] 텍스트입니다.|  
|**group_id**|**int**|이 쿼리가 실행하고 있는 작업 그룹의 ID입니다.|  
|**pool_id**|**int**|이 작업 그룹이 속한 리소스 풀의 ID입니다.|  
|**is_small**|**tinyint**|1로 설정되면 이 부여에서 작은 리소스 세마포를 사용합니다. 0으로 설정되면 일반 세마포가 사용됩니다.|  
|**ideal_memory_kb**|**bigint**|실제 메모리에 적합하도록 부여된 메모리 크기(KB)입니다. 이 크기는 카디널리티 예측에 기반합니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한  

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   
   
## <a name="remarks"></a>Remarks  
 쿼리 제한 시간에 대한 일반적인 디버깅 시나리오는 다음과 같습니다.  
  
-   전체 시스템 메모리 사용 하 여 상태를 확인 [sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)를 [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md), 및 다양 한 성능 카운터입니다.  
  
-   쿼리 실행 메모리 예약에 대 한 확인 **sys.dm_os_memory_clerks** 여기서 `type = 'MEMORYCLERK_SQLQERESERVATIONS'`합니다.  
  
-   대기 중인 쿼리를 확인<sup>1</sup> 사용 하 여 부여 **sys.dm_exec_query_memory_grants**합니다.  
  
    ```sql  
    --Find all queries waiting in the memory queue  
    SELECT * FROM sys.dm_exec_query_memory_grants where grant_time is null  
    ```  
    
    <sup>1</sup> 이 시나리오에서 대기 형식은 일반적으로 RESOURCE_SEMAPHORE입니다. 자세한 내용은 [sys.dm_os_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)를 참조하세요. 
  
-   사용 하 여 메모리 부여를 사용 하 여 쿼리에 대 한 캐시를 검색할 [sys.dm_exec_cached_plans &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md) 하 고 [sys.dm_exec_query_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
  
    ```sql  
    -- retrieve every query plan from the plan cache  
    USE master;  
    GO  
    SELECT * FROM sys.dm_exec_cached_plans cp CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
    GO  
    ```  
  
-   사용 하 여 메모리 사용량이 많은 쿼리를 세부적으로 검토할 [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)합니다.  
  
    ```sql  
    --Find top 5 queries by average CPU time  
    SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
      plan_handle, query_plan   
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
    ORDER BY total_worker_time/execution_count DESC;  
    GO  
    ```  
  
-   런어웨이 쿼리가 의심 되 면 검사에서 Showplan [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) 일괄 처리에서 텍스트 및 [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)합니다.  
  
 쿼리를 포함 하는 동적 관리 뷰를 사용 하는 `ORDER BY` 또는 집계 메모리 소비가 증가 하 고 따라서 해결 하는 문제에 기여 수 있습니다.  
  
 데이터베이스 관리자는 리소스 관리자 기능을 사용하여 서버 리소스를 최대 20개의 리소스 풀에 배치할 수 있습니다. 부터는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], 각 풀 처럼 작은 독립 서버 인스턴스를 동작 하 고 2 세마포를 필요로 합니다. 반환 되는 행 수가 **sys.dm_exec_query_resource_semaphores** 될 수 있습니다 최대 20 배가에 반환 되는 행 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.dm_exec_query_resource_semaphores &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)     
 [sys.dm_os_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
 [실행 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
