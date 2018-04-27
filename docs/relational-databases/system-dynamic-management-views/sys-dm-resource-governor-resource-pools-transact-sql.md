---
title: sys.dm_resource_governor_resource_pools (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_resource_pools_TSQL
- dm_resource_governor_resource_pools_TSQL
- sys.dm_resource_governor_resource_pools
- dm_resource_governor_resource_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_resource_pools dynamic management view
ms.assetid: 9bfc926e-d8bc-40f8-9229-ab1f8a1e69c5
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 95d9af2bc7989f451b1994367c3bf8cb6e2569f3
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="sysdmresourcegovernorresourcepools-transact-sql"></a>sys.dm_resource_governor_resource_pools(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  현재 리소스 풀 상태, 리소스 풀의 현재 구성 및 리소스 풀 통계에 대한 정보를 반환합니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_resource_governor_resource_pools**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|pool_id|**int**|리소스 풀의 ID입니다. Null을 허용하지 않습니다.|  
|name|**sysname**|리소스 풀의 이름입니다. Null을 허용하지 않습니다.|  
|statistics_start_time|**datetime**|이 풀에 대해 통계가 다시 설정된 시간입니다. Null을 허용하지 않습니다.|  
|total_cpu_usage_ms|**bigint**|리소스 관리자 통계를 다시 설정한 후 누적된 CPU 사용량(밀리초)입니다. Null을 허용하지 않습니다.|  
|cache_memory_kb|**bigint**|현재 캐시 메모리의 총 사용량(KB)입니다. Null을 허용하지 않습니다.|  
|compile_memory_kb|**bigint**|현재 빼앗긴 메모리의 총 사용량(KB)입니다. 이 사용량의 대부분은 컴파일과 최적화에 대한 것이지만 다른 메모리 사용자를 포함할 수도 있습니다. Null을 허용하지 않습니다.|  
|used_memgrant_kb|**bigint**|메모리 부여에서 현재 사용된(빼앗긴) 총 메모리(KB)입니다. Null을 허용하지 않습니다.|  
|total_memgrant_count|**bigint**|이 리소스 풀에서 발생하는 메모리 부여의 누적 수입니다. Null을 허용하지 않습니다.|  
|total_memgrant_timeout_count|**bigint**|이 리소스 풀에서 시간을 초과한 메모리 부여의 누적 수입니다. Null을 허용하지 않습니다.|  
|active_memgrant_count|**int**|현재 메모리 부여의 수입니다. Null을 허용하지 않습니다.|  
|active_memgrant_kb|**bigint**|현재 메모리 부여의 합계(KB)입니다. Null을 허용하지 않습니다.|  
|memgrant_waiter_count|**int**|현재 메모리 부여에서 대기 중인 쿼리 수입니다. Null을 허용하지 않습니다.|  
|max_memory_kb|**bigint**|리소스 풀에 있을 수 있는 최대 메모리 양((KB)입니다. 현재 설정 및 서버 상태를 기반으로 합니다. Null을 허용하지 않습니다.|  
|used_memory_kb|**bigint**|리소스 풀에 사용되는 최대 메모리 양((KB)입니다. Null을 허용하지 않습니다.|  
|target_memory_kb|**bigint**|리소스 풀이 사용하려는 대상 메모리 양((KB)입니다. 현재 설정 및 서버 상태를 기반으로 합니다. Null을 허용하지 않습니다.|  
|out_of_memory_count|**bigint**|리소스 관리자 통계를 다시 설정한 후 풀에 있는 실패한 메모리 할당 수입니다. Null을 허용하지 않습니다.|  
|min_cpu_percent|**int**|CPU 충돌이 있을 때 리소스 풀의 모든 요청에 대해 보장되는 평균 CPU 대역폭에 대한 현재 구성입니다. Null을 허용하지 않습니다.|  
|max_cpu_percent|**int**|CPU 충돌이 있을 때 리소스 풀의 모든 요청에 허용되는 최대 평균 CPU 대역폭에 대한 현재 구성입니다. Null을 허용하지 않습니다.|  
|min_memory_percent|**int**|메모리 충돌이 있을 때 리소스 풀의 모든 요청에 대해 보장되는 메모리 양에 대한 현재 구성입니다. 이것은 다른 리소스 풀과 공유되지 않습니다. Null을 허용하지 않습니다.|  
|max_memory_percent|**int**|이 리소스 풀의 요청에서 사용할 수 있는 총 서버 메모리의 비율에 대한 현재 구성입니다. Null을 허용하지 않습니다.|  
|cap_cpu_percent|**int**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 리소스 풀의 모든 요청에서 받을 CPU 대역폭의 하드 캡입니다. 최대 CPU 대역폭 수준을 지정된 수준으로 제한합니다. 허용되는 값의 범위는 1에서 100까지입니다. Null을 허용하지 않습니다.|  
|min_iops_per_volume|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 이 풀에 대한 디스크 볼륨 설정당 최소 IOPS(초당 I/O 작업)입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 즉, 리소스 풀의 MIN_IOPS_PER_VOLUME 및 MAX_IOPS_PER_VOLUME 설정이 0입니다.|  
|max_iops_per_volume|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 이 풀에 대한 디스크 볼륨 설정당 최대 IOPS(초당 I/O 작업)입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 즉, 리소스 풀의 MIN_IOPS_PER_VOLUME 및 MAX_IOPS_PER_VOLUME 설정이 0입니다.|  
|read_io_queued_total|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 리소스 관리자를 다시 설정한 후 큐에 놓인 총 읽기 IO입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 즉, 리소스 풀의 MIN_IOPS_PER_VOLUME 및 MAX_IOPS_PER_VOLUME 설정이 0입니다.|  
|read_io_issued_total|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 리소스 관리자 통계를 다시 설정한 후 발생한 총 읽기 IO입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 즉, 리소스 풀의 MIN_IOPS_PER_VOLUME 및 MAX_IOPS_PER_VOLUME 설정이 0입니다.|  
|read_io_completed_total|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 리소스 관리자 통계를 다시 설정한 후 완료된 총 읽기 IO입니다. Null을 허용하지 않습니다.|  
|read_io_throttled_total|**int**|리소스 관리자 통계를 다시 설정한 후 정체된 총 읽기 IO입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 즉, 리소스 풀의 MIN_IOPS_PER_VOLUME 및 MAX_IOPS_PER_VOLUME 설정이 0입니다.|  
|read_bytes_total|**bigint**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 리소스 관리자 통계를 다시 설정한 후 읽은 총 바이트 수입니다. Null을 허용하지 않습니다.|  
|read_io_stall_total_ms|**bigint**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 읽기 IO 도착과 완료 사이의 총 시간(밀리초)입니다. Null을 허용하지 않습니다. |  
|read_io_stall_queued_ms|**bigint**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 읽기 IO 도착과 완료 사이의 총 시간(밀리초)입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 즉, 리소스 풀의 MIN_IOPS_PER_VOLUME 및 MAX_IOPS_PER_VOLUME 설정이 0입니다.<br /><br /> 확인 하는 경우의 IO 설정 풀 대기 시간, 일으키는지 빼십시오 하려면 **read_io_stall_queued_ms** 에서 **read_io_stall_total_ms**합니다.|  
|write_io_queued_total|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 리소스 관리자 통계를 다시 설정한 후 큐에 놓인 총 쓰기 IO입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 즉, 리소스 풀의 MIN_IOPS_PER_VOLUME 및 MAX_IOPS_PER_VOLUME 설정이 0입니다.|  
|write_io_issued_total|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 리소스 관리자 통계를 다시 설정한 후 발생한 총 쓰기 IO입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 즉, 리소스 풀의 MIN_IOPS_PER_VOLUME 및 MAX_IOPS_PER_VOLUME 설정이 0입니다.|  
|write_io_completed_total|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 리소스 관리자 통계를 다시 설정한 후 완료된 총 쓰기 IO입니다. Null을 허용하지 않습니다.|  
|write_io_throttled_total|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 리소스 관리자 통계를 다시 설정한 후 정체된 총 쓰기 IO입니다. Null을 허용하지 않습니다.|  
|write_bytes_total|**bigint**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 리소스 관리자 통계를 다시 설정한 후 쓴 총 바이트 수입니다. Null을 허용하지 않습니다.|  
|write_io_stall_total_ms|**bigint**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 쓰기 IO 도착과 완료 사이의 총 시간(밀리초)입니다. Null을 허용하지 않습니다. |  
|write_io_stall_queued_ms|**bigint**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 쓰기 IO 도착과 완료 사이의 총 시간(밀리초)입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 즉, 리소스 풀의 MIN_IOPS_PER_VOLUME 및 MAX_IOPS_PER_VOLUME 설정이 0입니다.<br /><br /> IO 리소스 관리로 인해 발생한 지연 시간입니다.|  
|io_issue_violations_total|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 총 IO 실행 위반 수입니다. 즉, IO 실행 속도가 예약된 속도보다 낮았던 횟수입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 즉, 리소스 풀의 MIN_IOPS_PER_VOLUME 및 MAX_IOPS_PER_VOLUME 설정이 0입니다.|  
|io_issue_delay_total_ms|**bigint**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 예약된 IO 실행과 실제 IO 실행 사이의 총 시간(밀리초)입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 즉, 리소스 풀의 MIN_IOPS_PER_VOLUME 및 MAX_IOPS_PER_VOLUME 설정이 0입니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="remarks"></a>주의  
 리소스 관리자 작업 그룹 및 리소스 관리자 리소스 풀에는 다 대 일 매핑이 있습니다. 따라서 리소스 풀 통계의 대부분은 작업 그룹 통계에서 파생됩니다.  
  
 이 동적 관리 뷰는 인-메모리 구성을 표시합니다. 저장된 구성 메타데이터를 보려면 sys.resource_governor_resource_pools 카탈로그 뷰를 사용합니다.  
  
## <a name="permissions"></a>Permissions  
 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_resource_governor_workload_groups&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [sys.resource_governor_resource_pools &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  



