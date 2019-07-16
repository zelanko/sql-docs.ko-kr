---
title: sys.dm_resource_governor_resource_pools_history_ex (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governor
- sys.resource_governor_TSQL
- resource_governor
- resource_governor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 7b40d9afe54137fb31088aa8aa8b5664c90b715d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053298"
---
# <a name="sysdmresourcegovernorresourcepoolshistoryex-transact-sql"></a>sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Azure SQL Database에 대 한 통계를 풀 하는 리소스의 마지막 30 분 15 초 간격으로 스냅숏을 반환 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**pool_id**|ssNoversion|리소스 풀의 ID입니다. Null을 허용하지 않습니다.
|**name**|sysname|리소스 풀의 이름입니다. Null을 허용하지 않습니다.|
|**snapshot_time**|Datetime2|생성 된 리소스 풀 통계 스냅숏의 날짜/시간|
|**duration_ms**|ssNoversion|현재 및 이전 스냅숏 사이의 기간|
|**statistics_start_time**|Datetime2|이 풀에 대해 통계가 다시 설정된 시간입니다. Null을 허용하지 않습니다.|
|**active_session_count**|ssNoversion|현재 스냅숏의 총 활성 세션|
|**active_worker_count**|ssNoversion|현재 스냅숏의 총 작업자|
|**delta_cpu_usage_ms**|ssNoversion|CPU 사용량 마지막 스냅숏 이후 시간 (밀리초)입니다. Null을 허용하지 않습니다.|
|**delta_cpu_usage_preemptive_ms**|ssNoversion|선점형 win32 호출 관리 하지 않습니다 SQL CPU RG에서 마지막 스냅숏 이후에|
|**used_data_space_kb**|BIGINT|사용자 데이터베이스에 연결 된 사용자 풀에서 사용 된 총 공간|
|**allocated_disk_space_kb**|BIGINT|총 데이터 파일은 연결 된 사용자 데이터베이스의 크기와 사용자 풀|
|**target_memory_kb**|BIGINT|리소스 풀이 사용하려는 대상 메모리 양((KB)입니다. 현재 설정 및 서버 상태를 기반으로 합니다. Null을 허용하지 않습니다.|
|**used_memory_kb**|BIGINT|리소스 풀에 사용되는 최대 메모리 양((KB)입니다. Null을 허용하지 않습니다.|
|**cache_memory_kb**|BIGINT|현재 캐시 메모리의 총 사용량(KB)입니다. Null을 허용하지 않습니다.|
|**compile_memory_kb**|BIGINT|현재 빼앗긴 메모리의 총 사용량(KB)입니다. 이 사용량의 대부분은 컴파일과 최적화에 대한 것이지만 다른 메모리 사용자를 포함할 수도 있습니다. Null을 허용하지 않습니다.|
|**active_memgrant_count**|BIGINT|현재 메모리 부여의 수입니다. Null을 허용하지 않습니다.|
|**active_memgrant_kb**|BIGINT|현재 메모리 부여의 합계(KB)입니다. Null을 허용하지 않습니다.|
|**used_memgrant_kb**|BIGINT|메모리 부여에서 현재 사용된(빼앗긴) 총 메모리(KB)입니다. Null을 허용하지 않습니다.|
|**delta_memgrant_timeout_count**|ssNoversion|메모리 개수는이 기간에이 리소스 풀에 대 한 제한 시간을 부여 합니다. Null을 허용하지 않습니다.|
|**delta_memgrant_waiter_count**|ssNoversion|현재 메모리 부여에서 대기 중인 쿼리 수입니다. Null을 허용하지 않습니다.|
|**delta_out_of_memory_count**|ssNoversion|풀에서 마지막 스냅숏 이후에 실패 한 메모리 할당 수입니다. Null을 허용하지 않습니다.|
|**delta_read_io_queued**|ssNoversion|총 큐에 읽기 Io 마지막 스냅숏 이후에 합니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**delta_read_io_issued**|ssNoversion|총 읽기 Io 마지막 스냅숏 이후에 발급 합니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**delta_read_io_completed**|ssNoversion|총 읽기 Io 마지막 스냅숏 이후에 완료 합니다. Null을 허용하지 않습니다.|
|**delta_read_io_throttled**|ssNoversion|총 읽기 Io 스냅숏 이후에 제한입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**delta_read_bytes**|BIGINT|총 바이트 수가 마지막 스냅숏 이후에 읽습니다. Null을 허용하지 않습니다.|
|**delta_read_io_stall_ms**|ssNoversion|총 시간 (밀리초) 읽기 IO 도착과 완료 사이의 마지막 스냅숏 이후에 완료 합니다. Null을 허용하지 않습니다.|
|**delta_read_io_stall_queued_ms**|ssNoversion|읽기 IO 도착과 완료 사이의 마지막 스냅숏 이후에 밀리초 단위의 총 시간입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 0이 아닌 delta_read_io_stall_queued_ms IO RG에 의해 영향을 받는다는 것을 의미 합니다.|
|**delta_write_io_queued**|ssNoversion|마지막 스냅숏 이후에 총 쓰기 Io 큐에 있습니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**delta_write_io_issued**|ssNoversion|총 쓰기 Io 마지막 스냅숏 이후에 발급 합니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**delta_write_io_completed**|ssNoversion|총 쓰기 Io 마지막 스냅숏 이후에 완료 합니다. Null을 허용하지 않습니다.|
|**delta_write_io_throttled**|ssNoversion|총 쓰기 Io 마지막 스냅숏 이후에 제한 합니다. Null을 허용하지 않습니다.|
|**delta_write_bytes**|BIGINT|마지막 스냅숏 이후에 기록 된 바이트의 총 수입니다. Null을 허용하지 않습니다.|
|**delta_write_io_stall_ms**|ssNoversion|총 시간 (밀리초) 쓰기 IO 도착과 완료 사이의 마지막 스냅숏 이후에 완료 합니다. Null을 허용하지 않습니다.|
|**delta_write_io_stall_queued_ms**|ssNoversion|마지막 스냅숏 이후에 쓰기 IO 도착과 완료 사이의 밀리초 단위의 총 시간입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**delta_io_issue_delay_ms**|ssNoversion|예약 된 문제 및 마지막 스냅숏 이후에 IO의 실제 문제 사이의 (밀리초) 총 시간입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**max_iops_per_volume**|ssNoversion|IOPS (초당)이이 풀에 대 한 디스크 볼륨 설정 당 최대 IO입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**max_memory_kb**|BIGINT|리소스 풀에 있을 수 있는 최대 메모리 양((KB)입니다. 현재 설정 및 서버 상태를 기반으로 합니다. Null을 허용하지 않습니다.
|**max_log_rate_kb**|BIGINT|리소스 풀 수준에서 최대 로그 속도 ((킬로바이트) / 초)입니다.|
|**max_data_space_kb**|BIGINT|최대 탄력적 풀 저장소 용량 한도 (킬로바이트)이 탄력적 풀에 대 한 설정입니다.|
|**max_session**|ssNoversion|풀에 대 한 세션 제한|
|**max_worker**|ssNoversion|작업자 풀에 대 한 한도|
|**min_cpu_percent**|ssNoversion|CPU 충돌이 있을 때 리소스 풀의 모든 요청에 대해 보장되는 평균 CPU 대역폭에 대한 현재 구성입니다. Null을 허용하지 않습니다.|
|**max_cpu_percent**|ssNoversion|CPU 충돌이 있을 때 리소스 풀의 모든 요청에 허용되는 최대 평균 CPU 대역폭에 대한 현재 구성입니다. Null을 허용하지 않습니다.|
|**cap_cpu_percent**|ssNoversion|리소스 풀의 모든 요청에서 받을 CPU 대역폭의 하드 캡입니다. 최대 CPU 대역폭 수준을 지정된 수준으로 제한합니다. 허용되는 값의 범위는 1에서 100까지입니다. Null을 허용하지 않습니다.|
|**min_vcores**|decimal(5,2)|CPU 충돌이 있을 때 리소스 풀의 모든 요청에 대해 보장되는 평균 CPU 대역폭에 대한 현재 구성입니다.  Vcore 단위|
|**max_vcores**|decimal(5,2)|CPU 충돌이 있을 때 리소스 풀의 모든 요청에 허용되는 최대 평균 CPU 대역폭에 대한 현재 구성입니다.  Vcore 단위|
|**cap_vcores**|decimal(5,2)|리소스 풀의 모든 요청에서 받을 CPU 대역폭의 하드 캡입니다.  Vcore 수에는 단위|
|**instance_cpu_count**|ssNoversion|인스턴스에 대해 구성 된 CPU 수|
|**instance_cpu_percent|decimal(5,2)|인스턴스에 대해 구성 하는 CPU 비율|
|**instance_vcores**|decimal(5,2)|인스턴스에 대 한 구성 Vcore 수|
|**delta_log_bytes_used**|decimal(5,2)|총 로그 바이트 단위로 수준의 생성 풀 마지막 스냅숏 이후에|
|**avg_login_rate_percent**|decimal(5,2)|로그인 한도 비교 하는 마지막 스냅숏 이후에 로그인 수|
|**delta_vcores_used**|decimal(5,2)|마지막 스냅숏 이후에 사용률 vcore 수에서를 계산 합니다.|
|**cap_vcores_used_percent**|decimal(5,2)|풀 한도의 백분율로 평균 계산 사용률입니다.|
|**instance_vcores_used_percent**|decimal(5,2)|SQL 인스턴스의 백분율로 평균 계산 사용률입니다.|
|**avg_data_io_percent**|decimal(5,2)|풀 한도에 따른 백분율로 평균 I/O 활용률입니다.|
|**avg_log_write_percent**|decimal(5,2)|평균 쓰기 리소스 사용률 풀 한도의 백분율입니다.|
|**avg_storage_percent**|decimal(5,2)|풀의 저장소 한도의 백분율로 평균 저장소 사용률입니다.|
|**avg_allocated_storage_percent**|decimal(5,2)|탄력적 풀에 있는 모든 데이터베이스에 의해 할당 되는 데이터 공간의 비율입니다. 이 탄력적 풀의 최대 크기 데이터에 할당 하는 데이터 공간의 비율입니다. 자세한 내용은 참조 하십시오. SQL db에서 파일 공간 관리|
|**max_worker_percent**|decimal(5,2)|풀 한도에 따른 백분율로 최대 동시 작업자 (요청).|
|**max_session_percent**|decimal(5,2)|풀 한도에 따른 백분율로 최대 동시 세션|
|||

## <a name="permissions"></a>사용 권한

이 보기에는 VIEW SERVER STATE 권한이 필요합니다.

## <a name="remarks"></a>설명

사용자는 거의 실시간 리소스 사용량 사용자 워크 로드 풀 뿐만 아니라 Azure SQL Database 인스턴스의 시스템 내부 풀에 대 한 모니터링이 동적 관리 뷰를 액세스할 수 있습니다.

> [!IMPORTANT]
> 대부분이이 DMV에서 표시 하는 데이터의 내부 사용을 위한 것 이며 변경 될 수 있습니다.

## <a name="examples"></a>예

다음 예제에서는 사용자 풀에서 최대 로그 속도 데이터 및 각 스냅숏의 사용량 반환  

```sql
select snapshot_time, name, max_log_rate_kb, delta_log_bytes_used from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

다음 예제에서는 논리 마스터에 연결할 필요 없이 sys.elastic_pool_resource_stats로 유사한 정보를 반환

```sql
select snapshot_time, name, cap_vcores_used_percent,
  avg_data_io_percent,  
  avg_log_write_percent,
  avg_storage_percent,
  avg_allocated_storage_percent,
  max_data_space_kb,
  max_worker_percent,
  max_session_percent
    from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

## <a name="see-also"></a>관련 항목

- [변환 로그 속도 거 버 넌 스](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [탄력적 풀 DTU 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [탄력적 풀 vCore 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
