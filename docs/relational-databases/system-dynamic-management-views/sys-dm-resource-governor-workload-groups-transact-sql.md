---
description: sys.dm_resource_governor_workload_groups(Transact-SQL)
title: sys. dm_resource_governor_workload_groups (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2020
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dfcbcaceeb4e60a88f1ba00fa7a116629945c7e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454885"
---
# <a name="sysdm_resource_governor_workload_groups-transact-sql"></a>sys.dm_resource_governor_workload_groups(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  작업 그룹 통계 및 작업 그룹의 현재 메모리 내 구성을 반환합니다. 이 뷰는 sys.dm_resource_governor_resource_pools와 조인하여 리소스 풀 이름을 가져올 수 있습니다.  
  
> [!NOTE]  
>  또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_resource_governor_workload_groups**을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|group_id|**int**|작업 그룹의 ID입니다. Null을 허용하지 않습니다.|  
|name|**sysname**|작업 그룹의 이름입니다. Null을 허용하지 않습니다.|  
|pool_id|**int**|리소스 풀의 ID입니다. Null을 허용하지 않습니다.|  
|external_pool_id|**int**|**적용 대상**:부터 시작 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 합니다.<br /><br /> 외부 리소스 풀의 ID입니다. Null을 허용하지 않습니다.|  
|statistics_start_time|**datetime**|작업 그룹에 대해 통계 컬렉션이 다시 설정된 시간입니다. Null을 허용하지 않습니다.|  
|total_request_count|**bigint**|작업 그룹에서 완료된 요청의 누적 수입니다. Null을 허용하지 않습니다.|  
|total_queued_request_count|**bigint**|GROUP_MAX_REQUESTS 제한에 도달한 후에 지연된 요청의 누적 수입니다. Null을 허용하지 않습니다.|  
|active_request_count|**int**|현재 요청 수입니다. Null을 허용하지 않습니다.|  
|queued_request_count|**int**|현재 지연된 요청 수입니다. Null을 허용하지 않습니다.|  
|total_cpu_limit_violation_count|**bigint**|CPU 제한을 초과하는 요청의 누적 수입니다. Null을 허용하지 않습니다.|  
|total_cpu_usage_ms|**bigint**|이 작업 그룹의 누적된 CPU 사용량(밀리초)입니다. Null을 허용하지 않습니다.|  
|max_request_cpu_time_ms|**bigint**|단일 요청에 대한 최대 CPU 사용량(밀리초)입니다. Null을 허용하지 않습니다.<br /><br /> **참고:** 이 값은 구성 가능한 설정인 request_max_cpu_time_sec와 달리 측정 된 값입니다. 자세한 내용은 [CPU Threshold Exceeded 이벤트 클래스](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)를 참조하세요.|  
|blocked_task_count|**int**|현재 차단된 태스크의 수입니다. Null을 허용하지 않습니다.|  
|total_lock_wait_count|**bigint**|발생한 잠금 대기의 누적 횟수입니다. Null을 허용하지 않습니다.|  
|total_lock_wait_time_ms|**bigint**|잠금이 설정된 후 경과된 시간(밀리초)의 누적 합계입니다. Null을 허용하지 않습니다.|  
|total_query_optimization_count|**bigint**|이 작업 그룹의 누적된 쿼리 최적화 횟수입니다. Null을 허용하지 않습니다.|  
|total_suboptimal_plan_generation_count|**bigint**|메모리 부족 때문에 이 작업 그룹에 발생한 만족스럽지 못한 계획 생성의 누적 횟수입니다. Null을 허용하지 않습니다.|  
|total_reduced_memgrant_count|**bigint**|최대 쿼리 크기 제한에 도달한 메모리 부여의 누적 횟수입니다. Null을 허용하지 않습니다.|  
|max_request_grant_memory_kb|**bigint**|통계가 다시 설정된 이후 단일 요청의 최대 메모리 부여 크기(KB)입니다. Null을 허용하지 않습니다.|  
|active_parallel_thread_count|**bigint**|병렬 스레드 사용량의 현재 수입니다. Null을 허용하지 않습니다.|  
|importance|**sysname**|이 작업 그룹에서 요청의 상대적인 중요도에 대한 현재 구성 값입니다. 중요도는 보통 (낮음, 보통 또는 높음)의 다음 중 하나입니다.<br /><br /> Null을 허용하지 않습니다.|  
|request_max_memory_grant_percent|**int**|단일 요청에 대한 최대 메모리 부여의 현재 설정(%)입니다. Null을 허용하지 않습니다.|  
|request_max_cpu_time_sec|**int**|단일 요청에 대한 최대 CPU 사용 제한에 대한 현재 설정(초)입니다. Null을 허용하지 않습니다.|  
|request_memory_grant_timeout_sec|**int**|단일 요청에 대한 메모리 부여 시간 초과에 대한 현재 설정(초)입니다. Null을 허용하지 않습니다.|  
|group_max_requests|**int**|최대 동시 요청 수에 대한 현재 설정입니다. Null을 허용하지 않습니다.|  
|max_dop|**int**|작업 그룹에 대해 구성 된 최대 병렬 처리 수준입니다. 기본값은 0이며 글로벌 설정을 사용합니다. Null을 허용하지 않습니다.| 
|effective_max_dop|**int**|**적용 대상**:부터 시작 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 합니다.<br /><br />작업 그룹에 대 한 효율적인 최대 병렬 처리 수준입니다. Null을 허용하지 않습니다.| 
|total_cpu_usage_preemptive_ms|**bigint**|**적용 대상**:부터 시작 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 합니다.<br /><br />작업 그룹에 대 한 선점형 모드 예약에 사용 된 총 CPU 시간 (밀리초 단위로 측정)입니다. Null을 허용하지 않습니다.<br /><br />[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 외부의 코드(예: 확장 저장 프로시저 및 분산 쿼리)를 실행하려면 비선점형 스케줄러의 제어를 벗어나서 스레드를 실행해야 합니다. 작업자는 이 작업을 수행하기 위해 선점형 모드로 전환합니다.| 
|request_max_memory_grant_percent_numeric|**float**|**적용 대상**:부터 시작 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 합니다.<br /><br />단일 요청에 대한 최대 메모리 부여의 현재 설정(%)입니다. Null을 허용하지 않습니다.| 
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="remarks"></a>설명  
 이 동적 관리 뷰는 인-메모리 구성을 표시합니다. 저장 된 구성 메타 데이터를 보려면 [resource_governor_workload_groups &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md) 카탈로그 뷰를 사용 합니다.  
  
 가 성공적으로 실행 되 면,,,,,,,,,, `ALTER RESOURCE GOVERNOR RESET STATISTICS` `statistics_start_time` `total_request_count` `total_queued_request_count` `total_cpu_limit_violation_count` `total_cpu_usage_ms` `max_request_cpu_time_ms` `total_lock_wait_count` `total_lock_wait_time_ms` `total_query_optimization_count` `total_suboptimal_plan_generation_count` `total_reduced_memgrant_count` 및 `max_request_grant_memory_kb` 카운터가 다시 설정 됩니다. 카운터는 `statistics_start_time` 현재 시스템 날짜 및 시간으로 설정 되 고 다른 카운터는 0으로 설정 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 `VIEW SERVER STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [dm_resource_governor_resource_pools &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)   
 [resource_governor_workload_groups &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
