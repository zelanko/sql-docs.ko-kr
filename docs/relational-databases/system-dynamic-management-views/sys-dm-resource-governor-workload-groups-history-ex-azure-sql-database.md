---
title: sys.dm_resource_governor_workload_groups_history_ex (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_workload_groups_history_ex_TSQL
- sys.dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_resource_governor_workload_groups_history_ex dynamic management view
author: joesackmsft
ms.author: josack
manager: craigg
ms.openlocfilehash: a177d3bcb81e17bb3a3accf6e1fade02132a58fa
ms.sourcegitcommit: 209fa6dafe324f606c60dda3bb8df93bcf7af167
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66213764"
---
# <a name="sysdmresourcegovernorworkloadgroupshistoryex-azure-sql-database"></a>sys.dm_resource_governor_workload_groups_history_ex (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Azure SQL Database에 대 한 통계를 풀 하는 리소스의 마지막 30 분 15 초 간격으로 스냅숏을 반환 합니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**pool_id**| ssNoversion |리소스 풀의 ID입니다. Null을 허용하지 않습니다.|
|**group_id**| ssNoversion |작업 그룹의 ID입니다. Null을 허용하지 않습니다.|
|**name**| nvarchar(256) |작업 그룹의 이름입니다. Null을 허용하지 않습니다.|
|**snapshot_time**| Datetime |생성 된 리소스 그룹 통계 스냅숏의 날짜/시간입니다.|
|**duration_ms**| ssNoversion |현재 및 이전 스냅숏 간에 기간입니다.|
|**active_worker_count**| ssNoversion |현재 스냅숏의 총 작업자입니다.|
|**active_request_count**| ssNoversion |현재 요청 수입니다. Null을 허용하지 않습니다.|
|**active_session_count**| ssNoversion |현재 스냅숏의 총 활성 세션입니다.|
|**total_request_count**| BIGINT |작업 그룹에서 완료된 요청의 누적 수입니다. Null을 허용하지 않습니다.|
|**delta_request_count**| ssNoversion |마지막 스냅숏 이후에 작업 그룹에서 완료 된 요청의 수입니다. Null을 허용하지 않습니다.|
|**total_cpu_usage_ms**| BIGINT |이 작업 그룹의 누적된 CPU 사용량(밀리초)입니다. Null을 허용하지 않습니다.|
|**delta_cpu_usage_ms**| ssNoversion |CPU 사용량 마지막 스냅숏 이후 시간 (밀리초)입니다. Null을 허용하지 않습니다.|
|**delta_cpu_usage_preemptive_ms**| ssNoversion |선점형 win32 호출을 하지 마지막 스냅숏 이후에 SQL CPU RG 하 여 제어합니다.|
|**delta_reads_reduced_memgrant_count**| ssNoversion |마지막 스냅숏 이후에 최대 쿼리 크기 제한에 도달한 메모리 부여의 수입니다. Null을 허용하지 않습니다.|
|**reads_throttled**| ssNoversion |제한 된 읽기의 총 수입니다.|
|**delta_reads_queued**| ssNoversion |총 큐에 읽기 Io 마지막 스냅숏 이후에 합니다. Null을 허용합니다. 리소스 그룹은 IO에 대 한 관리 되지 경우 null입니다.|
|**delta_reads_issued**| ssNoversion |총 읽기 Io 마지막 스냅숏 이후에 발급 합니다. Null을 허용합니다. 리소스 그룹은 IO에 대 한 관리 되지 경우 null입니다.|
|**delta_reads_completed**| ssNoversion |총 읽기 Io 마지막 스냅숏 이후에 완료 합니다. Null을 허용하지 않습니다.|
|**delta_read_bytes**| BIGINT |총 바이트 수가 마지막 스냅숏 이후에 읽습니다. Null을 허용하지 않습니다.|
|**delta_read_stall_ms**| ssNoversion |총 시간 (밀리초) 읽기 IO 도착과 완료 사이의 마지막 스냅숏 이후에 완료 합니다. Null을 허용하지 않습니다.|
|**delta_read_stall_queued_ms**| ssNoversion |읽기 IO 도착과 완료 사이의 마지막 스냅숏 이후에 밀리초 단위의 총 시간입니다. Null을 허용합니다. 리소스 그룹은 IO에 대 한 관리 되지 경우 null입니다. 0이 아닌 delta_read_stall_queued_ms IO RG에 의해 영향을 받는다는 것을 의미 합니다.|
|**delta_writes_queued**| ssNoversion |마지막 스냅숏 이후에 총 쓰기 Io 큐에 있습니다. Null을 허용합니다. 리소스 그룹은 IO에 대 한 관리 되지 경우 null입니다.|
|**delta_writes_issued**| ssNoversion |총 쓰기 Io 마지막 스냅숏 이후에 발급 합니다. Null을 허용합니다. 리소스 그룹은 IO에 대 한 관리 되지 경우 null입니다.|
|**delta_writes_completed**| ssNoversion |총 쓰기 Io 마지막 스냅숏 이후에 완료 합니다. Null을 허용하지 않습니다.|
|**delta_writes_bytes**| BIGINT |마지막 스냅숏 이후에 기록 된 바이트의 총 수입니다. Null을 허용하지 않습니다.|
|**delta_write_stall_ms**| ssNoversion |총 시간 (밀리초) 쓰기 IO 도착과 완료 사이의 마지막 스냅숏 이후에 완료 합니다. Null을 허용하지 않습니다.|
|**delta_background_writes**| ssNoversion |총 쓰기 마지막 스냅숏 이후에 백그라운드 태스크에 의해 수행 됩니다.|
|**delta_background_write_bytes**| BIGINT |총 쓰기 크기 (바이트)에서 마지막 스냅숏 이후에 백그라운드 태스크에 의해 수행 됩니다.|
|**delta_log_bytes_used**| BIGINT |바이트에서 마지막 스냅숏 이후에 사용 된 로그입니다.|
|**delta_log_temp_db_bytes_used**| BIGINT |Tempdb 로그 바이트의 마지막 스냅숏 이후에 사용 합니다.|
|**delta_query_optimizations**| BIGINT |이 작업 그룹에서 마지막 스냅숏 이후에 쿼리 최적화 횟수입니다. Null을 허용하지 않습니다.|
|**delta_suboptimal_plan_generations**| BIGINT |메모리 부족으로 인해 작업 그룹에서 마지막 스냅숏 이후에 발생 한 최적이 아닌 계획이 세대의 수입니다. Null을 허용하지 않습니다.
|**max_memory_grant_kb**| BIGINT |최대 메모리 (kb)에서 그룹에 대 한 권한을 부여 합니다.|
|**max_request_cpu_msec**| BIGINT |단일 요청에 대한 최대 CPU 사용량(밀리초)입니다. Null을 허용하지 않습니다.|
|**max_concurrent_request**| ssNoversion |최대 동시 요청 수에 대한 현재 설정입니다. Null을 허용하지 않습니다.|
|**max_io**| ssNoversion |그룹에 대 한 최대 IO 제한 합니다.|
|**max_global_io**| ssNoversion |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.
|**max_queued_io**| ssNoversion |정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.|
|**max_log_rate_kb**| BIGINT |리소스 그룹 수준에서 최대 로그 속도 ((킬로바이트) / 초)입니다.|
|**max_session**| ssNoversion |그룹에 대 한 세션 제한입니다.|
|**max_worker**| ssNoversion |그룹의 작업자 제한 됩니다.|
|||

## <a name="permissions"></a>사용 권한

이 뷰에는 VIEW DATABASE STATE 권한이 필요합니다.

## <a name="remarks"></a>Remarks

사용자는 거의 실시간 리소스 사용량 사용자 워크 로드 풀 뿐만 아니라 Azure SQL Database 인스턴스의 시스템 내부 풀에 대 한 모니터링이 동적 관리 뷰를 액세스할 수 있습니다.

> [!IMPORTANT]
> 대부분이이 DMV에서 표시 하는 데이터의 내부 사용을 위한 것 이며 변경 될 수 있습니다.

## <a name="examples"></a>예

다음 예제에서는 사용자 풀에서 최대 로그 속도 데이터 및 각 스냅숏의 사용량을 반환합니다.

```sql
SELECT snapshot_time,
       name,
       max_log_rate_kb,
       delta_log_bytes_used
FROM sys.dm_resource_governor_workload_groups_history_ex
WHERE name LIKE 'User%'
ORDER BY snapshot_time DESC;
```

## <a name="see-also"></a>관련 항목

- [변환 로그 속도 거 버 넌 스](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [탄력적 풀 DTU 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [탄력적 풀 vCore 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)