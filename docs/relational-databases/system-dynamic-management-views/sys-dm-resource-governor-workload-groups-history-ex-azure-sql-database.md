---
title: dm_resource_governor_workload_groups_history_ex (Azure SQL Database) | Microsoft Docs
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
ms.openlocfilehash: 0b112762df3ca05411594b1e1c03a04817c094d9
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823322"
---
# <a name="sysdm_resource_governor_workload_groups_history_ex-azure-sql-database"></a>sys.dm_resource_governor_workload_groups_history_ex(Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

Azure SQL Database에 대 한 리소스 풀 통계의 마지막 32 분 (총 128 초)에 대 한 스냅숏을 20 초 간격으로 반환 합니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**pool_id**| Int |리소스 풀의 ID입니다. Null을 허용하지 않습니다.|
|**group_id**| Int |작업 그룹의 ID입니다. Null을 허용하지 않습니다.|
|**name**| nvarchar(256) |작업 그룹의 이름입니다. Null을 허용하지 않습니다.|
|**snapshot_time**| Datetime |만든 리소스 그룹 통계 스냅숏의 날짜/시간입니다.|
|**duration_ms**| Int |현재 스냅숏과 이전 스냅숏 간의 기간입니다.|
|**active_worker_count**| Int |현재 스냅숏의 총 작업자|
|**active_request_count**| Int |현재 요청 수입니다. Null을 허용하지 않습니다.|
|**active_session_count**| Int |현재 스냅숏의 총 활성 세션.|
|**total_request_count**| bigint |작업 그룹에서 완료된 요청의 누적 수입니다. Null을 허용하지 않습니다.|
|**delta_request_count**| Int |마지막 스냅숏 이후 작업 그룹에서 완료 된 요청 수입니다. Null을 허용하지 않습니다.|
|**total_cpu_usage_ms**| bigint |이 작업 그룹의 누적된 CPU 사용량(밀리초)입니다. Null을 허용하지 않습니다.|
|**delta_cpu_usage_ms**| Int |마지막 스냅숏 이후 CPU 사용량 (밀리초)입니다. Null을 허용하지 않습니다.|
|**delta_cpu_usage_preemptive_ms**| Int |선점형 win32 호출은 마지막 스냅숏 이후 SQL CPU RG에 의해 제어 되지 않습니다.|
|**delta_reads_reduced_memgrant_count**| Int |마지막 스냅숏 이후 최대 쿼리 크기 제한에 도달한 메모리 부여의 수입니다. Null을 허용하지 않습니다.|
|**reads_throttled**| Int |제한 된 총 읽기 수입니다.|
|**delta_reads_queued**| Int |마지막 스냅숏 이후 큐에 넣은 총 읽기 Io입니다. Null을 허용합니다. 리소스 그룹이 IO에 대해 관리 되지 않는 경우 Null입니다.|
|**delta_reads_issued**| Int |마지막 스냅숏 이후 발급 된 총 읽기 Io입니다. Null을 허용합니다. 리소스 그룹이 IO에 대해 관리 되지 않는 경우 Null입니다.|
|**delta_reads_completed**| Int |마지막 스냅숏 이후 완료 된 총 읽기 Io입니다. Null을 허용하지 않습니다.|
|**delta_read_bytes**| bigint |마지막 스냅숏 이후 읽은 총 바이트 수입니다. Null을 허용하지 않습니다.|
|**delta_read_stall_ms**| Int |마지막 스냅숏 이후 읽기 IO 도착 및 완료 사이의 총 시간 (밀리초)입니다. Null을 허용하지 않습니다.|
|**delta_read_stall_queued_ms**| Int |마지막 스냅숏 이후 읽기 IO 도착 및 문제 사이의 총 시간 (밀리초)입니다. Null을 허용합니다. 리소스 그룹이 IO에 대해 관리 되지 않는 경우 Null입니다. 0이 아닌 delta_read_stall_queued_ms는 IO가 RG의 영향을 받는 것을 의미 합니다.|
|**delta_writes_queued**| Int |마지막 스냅숏 이후 큐에 넣은 총 쓰기 Io입니다. Null을 허용합니다. 리소스 그룹이 IO에 대해 관리 되지 않는 경우 Null입니다.|
|**delta_writes_issued**| Int |마지막 스냅숏 이후 실행 된 총 쓰기 Io입니다. Null을 허용합니다. 리소스 그룹이 IO에 대해 관리 되지 않는 경우 Null입니다.|
|**delta_writes_completed**| Int |마지막 스냅숏 이후 완료 된 총 쓰기 Io입니다. Null을 허용하지 않습니다.|
|**delta_writes_bytes**| bigint |마지막 스냅숏 이후 작성 된 총 바이트 수입니다. Null을 허용하지 않습니다.|
|**delta_write_stall_ms**| Int |마지막 스냅숏 이후 쓰기 IO 도착 및 완료 사이의 총 시간 (밀리초)입니다. Null을 허용하지 않습니다.|
|**delta_background_writes**| Int |마지막 스냅숏 이후 백그라운드 작업에서 수행 된 총 쓰기입니다.|
|**delta_background_write_bytes**| bigint |마지막 스냅숏 이후 백그라운드 작업에서 수행 하는 총 쓰기 크기 (바이트)입니다.|
|**delta_log_bytes_used**| bigint |마지막 스냅숏 이후 사용 된 로그 (바이트)입니다.|
|**delta_log_temp_db_bytes_used**| bigint |마지막 스냅숏 이후 사용 된 Tempdb 로그 (바이트)입니다.|
|**delta_query_optimizations**| bigint |마지막 스냅숏 이후이 작업 그룹의 쿼리 최적화 수입니다. Null을 허용하지 않습니다.|
|**delta_suboptimal_plan_generations**| bigint |마지막 스냅숏 이후 메모리 압력으로 인해이 작업 그룹에서 발생 한 최적이 아닌 계획 생성의 수입니다. Null을 허용하지 않습니다.
|**max_memory_grant_kb**| bigint |그룹에 대 한 최대 메모리 부여 (KB)입니다.|
|**max_request_cpu_msec**| bigint |단일 요청에 대한 최대 CPU 사용량(밀리초)입니다. Null을 허용하지 않습니다.|
|**max_concurrent_request**| Int |최대 동시 요청 수에 대한 현재 설정입니다. Null을 허용하지 않습니다.|
|**max_io**| Int |그룹에 대 한 최대 IO 제한입니다.|
|**max_global_io**| Int |정보를 제공하기 위해서만 확인됩니다. 지원 안 됨 향후 호환성은 보장되지 않습니다.
|**max_queued_io**| Int |정보를 제공하기 위해서만 확인됩니다. 지원 안 됨 향후 호환성은 보장되지 않습니다.|
|**max_log_rate_kb**| bigint |리소스 그룹 수준에서 최대 로그 속도 (초당 킬로바이트 바이트)입니다.|
|**max_session**| Int |그룹에 대 한 세션 제한입니다.|
|**max_worker**| Int |그룹에 대 한 작업자 한도입니다.|
|||

## <a name="permissions"></a>사용 권한

이 보기에는 VIEW SERVER STATE 권한이 필요 합니다.

## <a name="remarks"></a>설명

사용자는이 동적 관리 보기에 액세스 하 여 사용자 작업 풀 및 Azure SQL Database 인스턴스의 시스템 내부 풀에 대 한 거의 실시간 리소스 사용량을 모니터링할 수 있습니다.

> [!IMPORTANT]
> 이 DMV에 의해 표시 되는 대부분의 데이터는 내부 사용을 위한 것 이며 변경 될 수 있습니다.

## <a name="examples"></a>예

다음 예에서는 사용자 풀의 각 스냅숏에서 최대 로그 속도 데이터 및 사용량을 반환 합니다.

```sql
SELECT snapshot_time,
       name,
       max_log_rate_kb,
       delta_log_bytes_used
FROM sys.dm_resource_governor_workload_groups_history_ex
WHERE name LIKE 'User%'
ORDER BY snapshot_time DESC;
```

## <a name="see-also"></a>참고 항목

- [변환 로그 율 거 버 넌 스](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [탄력적 풀 DTU 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [탄력적 풀 vCore 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
