---
title: sys.dm_resource_governor_workload_groups (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_workload_groups
- sys.dm_resource_governor_workload_groups_TSQL
- dm_resource_governor_workload_groups
- dm_resource_governor_workload_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_workload_groups dynamic management view
ms.assetid: f63c4914-1272-43ef-b135-fe1aabd953e0
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: dce7ea713a3be7f97d1156d9598a95d10b16de6e
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmresourcegovernorworkloadgroups-transact-sql"></a>sys.dm_resource_governor_workload_groups(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  작업 그룹 통계 및 작업 그룹의 현재 메모리 내 구성을 반환합니다. 이 뷰는 sys.dm_resource_governor_resource_pools와 조인하여 리소스 풀 이름을 가져올 수 있습니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_resource_governor_workload_groups**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|group_id|**int**|작업 그룹의 ID입니다. Null을 허용하지 않습니다.|  
|name|**sysname**|작업 그룹의 이름입니다. Null을 허용하지 않습니다.|  
|pool_id|**int**|리소스 풀의 ID입니다. Null을 허용하지 않습니다.|  
|external_pool_id|**int**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 외부 리소스 풀의 ID입니다. Null을 허용하지 않습니다.|  
|statistics_start_time|**datetime**|작업 그룹에 대해 통계 컬렉션이 다시 설정된 시간입니다. Null을 허용하지 않습니다.|  
|total_request_count|**bigint**|작업 그룹에서 완료된 요청의 누적 수입니다. Null을 허용하지 않습니다.|  
|total_queued_request_count|**bigint**|GROUP_MAX_REQUESTS 제한에 도달한 후에 지연된 요청의 누적 수입니다. Null을 허용하지 않습니다.|  
|active_request_count|**int**|현재 요청 수입니다. Null을 허용하지 않습니다.|  
|queued_request_count|**int**|현재 지연된 요청 수입니다. Null을 허용하지 않습니다.|  
|total_cpu_limit_violation_count|**bigint**|CPU 제한을 초과하는 요청의 누적 수입니다. Null을 허용하지 않습니다.|  
|total_cpu_usage_ms|**bigint**|이 작업 그룹의 누적된 CPU 사용량(밀리초)입니다. Null을 허용하지 않습니다.|  
|max_request_cpu_time_ms|**bigint**|단일 요청에 대한 최대 CPU 사용량(밀리초)입니다. Null을 허용하지 않습니다.<br /><br /> **참고:** 이것은 request_max_cpu_time_sec, 달리 측정값 구성 가능한 설정 합니다. 자세한 내용은 [CPU Threshold Exceeded 이벤트 클래스](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)를 참조하세요.|  
|blocked_task_count|**int**|현재 차단된 태스크의 수입니다. Null을 허용하지 않습니다.|  
|total_lock_wait_count|**bigint**|발생한 잠금 대기의 누적 횟수입니다. Null을 허용하지 않습니다.|  
|total_lock_wait_time_ms|**bigint**|잠금이 설정된 후 경과된 시간(밀리초)의 누적 합계입니다. Null을 허용하지 않습니다.|  
|total_query_optimization_count|**bigint**|이 작업 그룹의 누적된 쿼리 최적화 횟수입니다. Null을 허용하지 않습니다.|  
|total_suboptimal_plan_generation_count|**bigint**|메모리 부족 때문에 이 작업 그룹에 발생한 만족스럽지 못한 계획 생성의 누적 횟수입니다. Null을 허용하지 않습니다.|  
|total_reduced_memgrant_count|**bigint**|최대 쿼리 크기 제한에 도달한 메모리 부여의 누적 횟수입니다. Null을 허용하지 않습니다.|  
|max_request_grant_memory_kb|**bigint**|통계가 다시 설정된 이후 단일 요청의 최대 메모리 부여 크기(KB)입니다. Null을 허용하지 않습니다.|  
|active_parallel_thread_count|**bigint**|병렬 스레드 사용량의 현재 수입니다. Null을 허용하지 않습니다.|  
|importance|**sysname**|이 작업 그룹에서 요청의 상대적인 중요도에 대한 현재 구성 값입니다. 중요도 다음 중 하나 이며 Medium 기본값 되 고,: 낮음, 보통 또는 높음입니다.<br /><br /> Null을 허용하지 않습니다.|  
|request_max_memory_grant_percent|**int**|단일 요청에 대한 최대 메모리 부여의 현재 설정(%)입니다. Null을 허용하지 않습니다.|  
|request_max_cpu_time_sec|**int**|단일 요청에 대한 최대 CPU 사용 제한에 대한 현재 설정(초)입니다. Null을 허용하지 않습니다.|  
|request_memory_grant_timeout_sec|**int**|단일 요청에 대한 메모리 부여 시간 초과에 대한 현재 설정(초)입니다. Null을 허용하지 않습니다.|  
|group_max_requests|**int**|최대 동시 요청 수에 대한 현재 설정입니다. Null을 허용하지 않습니다.|  
|max_dop|**int**|작업 그룹에 대한 최대 병렬 처리 수준입니다. 기본값은 0이며 글로벌 설정을 사용합니다. Null을 허용하지 않습니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="remarks"></a>주의  
 이 동적 관리 뷰는 인-메모리 구성을 표시합니다. 저장된 구성 메타데이터를 보려면 sys.resource_governor_workload_groups 카탈로그 뷰를 사용합니다.  
  
 ALTER RESOURCE GOVERNOR RESET STATISTICS가 성공적으로 실행 하는 경우 다음과 같은 카운터를 다시 설정 됩니다: statistics_start_time, total_request_count, total_queued_request_count, total_cpu_limit_violation_count, total_cpu_usage_ms max_request_ cpu_time_ms, total_lock_wait_count, total_lock_wait_time_ms, total_query_optimization_count, total_suboptimal_plan_generation_count, total_reduced_memgrant_count 및 max_request_grant_memory_kb 카운터가 다시 합니다. statistics_start_time 현재 시스템 날짜와 시간으로 설정 되어, 다른 카운터는 영 (0)으로 설정 됩니다.  
  
## <a name="permissions"></a>Permissions  
 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_resource_governor_resource_pools &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)   
 [sys.resource_governor_workload_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  



