---
title: _resource_governor_resource_pools_history_ex (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: f94cc3ccd0278a3ae2f46707f2680f8d198db58a
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70873923"
---
# <a name="sysdm_resource_governor_resource_pools_history_ex-transact-sql"></a>sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Azure SQL Database에 대 한 리소스 풀 통계의 마지막 32 분 (128 개 합계)에 대 한 스냅숏을 20 초 간격으로 반환 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**pool_id**|int|리소스 풀의 ID입니다. Null을 허용하지 않습니다.
|**name**|sysname|리소스 풀의 이름입니다. Null을 허용하지 않습니다.|
|**snapshot_time**|Datetime2|리소스 풀 통계 스냅숏의 날짜/시간|
|**duration_ms**|int|현재 스냅숏과 이전 스냅숏 간의 지속 시간|
|**statistics_start_time**|Datetime2|이 풀에 대해 통계가 다시 설정된 시간입니다. Null을 허용하지 않습니다.|
|**active_session_count**|int|현재 스냅숏의 총 활성 세션|
|**active_worker_count**|int|현재 스냅숏의 총 작업자|
|**delta_cpu_usage_ms**|int|마지막 스냅숏 이후 CPU 사용량 (밀리초)입니다. Null을 허용하지 않습니다.|
|**delta_cpu_usage_preemptive_ms**|int|마지막 스냅숏 이후 SQL CPU RG에 의해 제어 되지 않는 선점형 win32 호출|
|**used_data_space_kb**|bigint|사용자 풀과 연결 된 사용자 데이터베이스에 사용 되는 총 공간|
|**allocated_disk_space_kb**|bigint|사용자 풀과 연결 된의 사용자 데이터베이스에 대 한 총 데이터 파일 크기|
|**target_memory_kb**|bigint|리소스 풀이 사용하려는 대상 메모리 양((KB)입니다. 현재 설정 및 서버 상태를 기반으로 합니다. Null을 허용하지 않습니다.|
|**used_memory_kb**|bigint|리소스 풀에 사용되는 최대 메모리 양((KB)입니다. Null을 허용하지 않습니다.|
|**cache_memory_kb**|bigint|현재 캐시 메모리의 총 사용량(KB)입니다. Null을 허용하지 않습니다.|
|**compile_memory_kb**|bigint|현재 빼앗긴 메모리의 총 사용량(KB)입니다. 이 사용량의 대부분은 컴파일과 최적화에 대한 것이지만 다른 메모리 사용자를 포함할 수도 있습니다. Null을 허용하지 않습니다.|
|**active_memgrant_count**|bigint|현재 메모리 부여의 수입니다. Null을 허용하지 않습니다.|
|**active_memgrant_kb**|bigint|현재 메모리 부여의 합계(KB)입니다. Null을 허용하지 않습니다.|
|**used_memgrant_kb**|bigint|메모리 부여에서 현재 사용된(빼앗긴) 총 메모리(KB)입니다. Null을 허용하지 않습니다.|
|**delta_memgrant_timeout_count**|int|이 기간에이 리소스 풀의 메모리 부여 시간 초과 수입니다. Null을 허용하지 않습니다.|
|**delta_memgrant_waiter_count**|int|현재 메모리 부여에서 대기 중인 쿼리 수입니다. Null을 허용하지 않습니다.|
|**delta_out_of_memory_count**|int|마지막 스냅숏 이후 풀에서 실패 한 메모리 할당의 수입니다. Null을 허용하지 않습니다.|
|**delta_read_io_queued**|int|마지막 스냅숏 이후 큐에 넣은 총 읽기 Io입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**delta_read_io_issued**|int|마지막 스냅숏 이후 발급 된 총 읽기 Io입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**delta_read_io_completed**|int|마지막 스냅숏 이후 완료 된 총 읽기 Io입니다. Null을 허용하지 않습니다.|
|**delta_read_io_throttled**|int|스냅숏 이후 제한 된 총 읽기 Io입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**delta_read_bytes**|bigint|마지막 스냅숏 이후 읽은 총 바이트 수입니다. Null을 허용하지 않습니다.|
|**delta_read_io_stall_ms**|int|마지막 스냅숏 이후 읽기 IO 도착 및 완료 사이의 총 시간 (밀리초)입니다. Null을 허용하지 않습니다.|
|**delta_read_io_stall_queued_ms**|int|마지막 스냅숏 이후 읽기 IO 도착 및 문제 사이의 총 시간 (밀리초)입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다. 0이 아닌 delta_read_io_stall_queued_ms는 IO가 RG의 영향을 받는 것을 의미 합니다.|
|**delta_write_io_queued**|int|마지막 스냅숏 이후 큐에 넣은 총 쓰기 Io입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**delta_write_io_issued**|int|마지막 스냅숏 이후 실행 된 총 쓰기 Io입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**delta_write_io_completed**|int|마지막 스냅숏 이후 완료 된 총 쓰기 Io입니다. Null을 허용하지 않습니다.|
|**delta_write_io_throttled**|int|마지막 스냅숏 이후 제한 된 총 쓰기 Io입니다. Null을 허용하지 않습니다.|
|**delta_write_bytes**|bigint|마지막 스냅숏 이후 작성 된 총 바이트 수입니다. Null을 허용하지 않습니다.|
|**delta_write_io_stall_ms**|int|마지막 스냅숏 이후 쓰기 IO 도착 및 완료 사이의 총 시간 (밀리초)입니다. Null을 허용하지 않습니다.|
|**delta_write_io_stall_queued_ms**|int|마지막 스냅숏 이후 쓰기 IO 도착과 발급 사이의 총 시간 (밀리초)입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**delta_io_issue_delay_ms**|int|마지막 스냅숏 후의 예약 된 문제와 실제 IO 문제 사이의 총 시간 (밀리초)입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**max_iops_per_volume**|int|이 풀에 대 한 디스크 볼륨 설정 당 최대 IOPS (초당 IO) 수입니다. Null을 허용합니다. 리소스 풀에서 IO가 관리되지 않으면 Null입니다.|
|**max_memory_kb**|bigint|리소스 풀에 있을 수 있는 최대 메모리 양((KB)입니다. 현재 설정 및 서버 상태를 기반으로 합니다. Null을 허용하지 않습니다.
|**max_log_rate_kb**|bigint|리소스 풀 수준에서 최대 로그 속도 (초당 킬로바이트 바이트)입니다.|
|**max_data_space_kb**|bigint|이 탄력적 풀에 대 한 최대 탄력적 풀 저장소 제한 설정 (킬로바이트)입니다.|
|**max_session**|int|풀에 대 한 세션 제한|
|**max_worker**|int|풀에 대 한 작업자 제한|
|**min_cpu_percent**|int|CPU 충돌이 있을 때 리소스 풀의 모든 요청에 대해 보장되는 평균 CPU 대역폭에 대한 현재 구성입니다. Null을 허용하지 않습니다.|
|**max_cpu_percent**|int|CPU 충돌이 있을 때 리소스 풀의 모든 요청에 허용되는 최대 평균 CPU 대역폭에 대한 현재 구성입니다. Null을 허용하지 않습니다.|
|**cap_cpu_percent**|int|리소스 풀의 모든 요청에서 받을 CPU 대역폭의 하드 캡입니다. 최대 CPU 대역폭 수준을 지정된 수준으로 제한합니다. 허용되는 값의 범위는 1에서 100까지입니다. Null을 허용하지 않습니다.|
|**min_vcores**|decimal (5, 2)|CPU 충돌이 있을 때 리소스 풀의 모든 요청에 대해 보장되는 평균 CPU 대역폭에 대한 현재 구성입니다.  VCores 단위|
|**max_vcores**|decimal (5, 2)|CPU 충돌이 있을 때 리소스 풀의 모든 요청에 허용되는 최대 평균 CPU 대역폭에 대한 현재 구성입니다.  VCores 단위|
|**cap_vcores**|decimal (5, 2)|리소스 풀의 모든 요청에서 받을 CPU 대역폭의 하드 캡입니다.  VCores의 단위|
|**instance_cpu_count**|int|인스턴스에 대해 구성 된 CPU 수|
|**instance_cpu_percent|decimal (5, 2)|인스턴스에 대해 구성 된 CPU 백분율|
|**instance_vcores**|decimal (5, 2)|인스턴스에 대해 구성 된 vCores 수|
|**delta_log_bytes_used**|decimal (5, 2)|마지막 스냅숏 이후 풀 수준에서 총 로그 생성 (바이트)|
|**avg_login_rate_percent**|decimal (5, 2)|로그인 제한과 비교한 마지막 스냅숏 이후의 로그인 수|
|**delta_vcores_used**|decimal (5, 2)|마지막 스냅숏 이후 vCores 수의 계산 사용률입니다.|
|**cap_vcores_used_percent**|decimal (5, 2)|풀 한도의 백분율로 나타낸 평균 계산 사용률입니다.|
|**instance_vcores_used_percent**|decimal (5, 2)|SQL 인스턴스 제한의 백분율로 나타낸 평균 계산 사용률입니다.|
|**avg_data_io_percent**|decimal (5, 2)|풀의 한도를 기준으로 하는 평균 i/o 사용률 (백분율)입니다.|
|**avg_log_write_percent**|decimal (5, 2)|풀 한도의 백분율로 나타낸 평균 쓰기 리소스 사용률입니다.|
|**avg_storage_percent**|decimal (5, 2)|풀 저장소 한도의 백분율로 나타낸 평균 저장소 사용률입니다.|
|**avg_allocated_storage_percent**|decimal (5, 2)|탄력적 풀의 모든 데이터베이스에서 할당 한 데이터 공간의 비율입니다. 탄력적 풀의 데이터 최대 크기에 할당 된 데이터 공간의 비율입니다. 자세한 내용은 다음을 참조 하세요. SQL DB의 파일 공간 관리|
|**max_worker_percent**|decimal (5, 2)|풀의 한도를 기준으로 하는 최대 동시 작업자 (요청)의 백분율입니다.|
|**max_session_percent**|decimal (5, 2)|풀의 한도를 기준으로 하는 최대 동시 세션 (백분율)입니다.|
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
select snapshot_time, name, max_log_rate_kb, delta_log_bytes_used from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

다음 예에서는 논리 마스터에 연결할 필요 없이 elastic_pool_resource_stats와 유사한 정보를 반환 합니다.

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

- [변환 로그 율 거 버 넌 스](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [탄력적 풀 DTU 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [탄력적 풀 vCore 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
