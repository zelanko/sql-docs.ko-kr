---
title: sys. dm_user_db_resource_governance (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governance
- sys.resource_governance_TSQL
- resource_governance
- resource_governance_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governance catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: aa7c7e7a7c510f797377c3cbbceb7c2751418da3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74165924"
---
# <a name="sysdm_user_db_resource_governance-transact-sql"></a>sys. dm_user_db_resource_governance (Transact-sql)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

현재 데이터베이스 또는 탄력적 풀의 리소스 거 버 넌 스 메커니즘에서 사용 되는 실제 구성 및 용량 설정을 반환 합니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|int|Azure SQL Database 서버 내에서 고유한 데이터베이스의 ID입니다.|
|**logical_database_guid**|uniqueidentifier|사용자 데이터베이스의 수명 동안 유지 되는 사용자 데이터베이스의 논리적 GUID입니다.  데이터베이스의 이름을 바꾸거나 서비스 수준 목표를 변경 해도이 값은 변경 되지 않습니다.|
|**physical_database_guid**|uniqueidentifier|사용자 데이터베이스의 실제 인스턴스 수명 동안 유지 되는 사용자 데이터베이스의 실제 GUID입니다. 데이터베이스 서비스 수준 목표를 변경 하면이 값이 변경 됩니다.|
|**server_name**|nvarchar|논리 서버 이름입니다.|
|**database_name**|nvarchar|논리적 데이터베이스 이름입니다.|
|**slo_name**|nvarchar|하드웨어 생성을 포함 한 서비스 수준 목표입니다.|
|**dtu_limit**|int|데이터베이스의 DTU 한도 (vCore의 경우 NULL)입니다.|
|**cpu_limit**|int|데이터베이스의 vCore 제한 (DTU 데이터베이스의 경우 NULL)입니다.|
|**min_cpu**|tinyint|사용자 작업 리소스 풀의 MIN_CPU_PERCENT 값입니다. [리소스 풀 개념](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts)을 참조 하세요.|
|**max_cpu**|tinyint|사용자 작업 리소스 풀의 MAX_CPU_PERCENT 값입니다. [리소스 풀 개념](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts)을 참조 하세요.|
|**cap_cpu**|tinyint|사용자 작업 리소스 풀의 CAP_CPU_PERCENT 값입니다. [리소스 풀 개념](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts)을 참조 하세요.|
|**min_cores**|smallint|내부적으로만 사용됩니다.|
|**max_dop**|smallint|사용자 작업 그룹의 MAX_DOP 값입니다. [작업 그룹 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-workload-group-transact-sql)를 참조 하세요.|
|**min_memory**|int|사용자 작업 리소스 풀의 MIN_MEMORY_PERCENT 값입니다. [리소스 풀 개념](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts)을 참조 하세요.|
|**max_memory**|int|사용자 작업 리소스 풀의 MAX_MEMORY_PERCENT 값입니다. [리소스 풀 개념](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts)을 참조 하세요.|
|**max_sessions**|int|사용자 작업 그룹에 허용 되는 최대 세션 수입니다.|
|**max_memory_grant**|int|사용자 작업 그룹의 REQUEST_MAX_MEMORY_GRANT_PERCENT 값입니다. [작업 그룹 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-workload-group-transact-sql)를 참조 하세요.|
|**max_db_memory**|int|내부적으로만 사용됩니다.|
|**govern_background_io**|bit|내부적으로만 사용됩니다.|
|**min_db_max_size_in_mb**|bigint|데이터 파일의 최소 max_size 값 (MB)입니다. [Database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)를 참조 하세요.|
|**max_db_max_size_in_mb**|bigint|데이터 파일의 최대 max_size 값 (MB)입니다. [Database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)를 참조 하세요.|
|**default_db_max_size_in_mb**|bigint|데이터 파일에 대 한 기본 max_size 값 (MB)입니다. [Database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)를 참조 하세요.|
|**db_file_growth_in_mb**|bigint|데이터 파일의 기본 증가분 (MB)입니다. [Database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)를 참조 하세요.|
|**initial_db_file_size_in_mb**|bigint|새 데이터 파일의 기본 크기 (MB)입니다. [Database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)를 참조 하세요.|
|**log_size_in_mb**|bigint|새 로그 파일의 기본 크기 (MB)입니다. [Database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)를 참조 하세요.|
|**instance_cap_cpu**|int|내부적으로만 사용됩니다.|
|**instance_max_log_rate**|bigint|SQL Server 인스턴스의 로그 생성 률 한도 (바이트/초)입니다. 및 기타 시스템 데이터베이스를 포함 `tempdb` 하 여 인스턴스에 의해 생성 된 모든 로그에 적용 됩니다. 탄력적 풀에서는 풀에 있는 모든 데이터베이스에 의해 생성 된 로그에 적용 됩니다.|
|**instance_max_worker_threads**|int|SQL Server 인스턴스에 대 한 작업자 스레드 제한입니다.|
|**replica_type**|int|복제본 유형 (0은 Primary, 1은 보조)입니다.|
|**max_transaction_size**|bigint|모든 트랜잭션에서 사용 되는 최대 로그 공간 (KB)입니다.|
|**checkpoint_rate_mbps**|int|내부적으로만 사용됩니다.|
|**checkpoint_rate_io**|int|내부적으로만 사용됩니다.|
|**last_updated_date_utc**|Datetime|마지막 설정 변경 또는 재구성 날짜와 시간 (UTC)입니다.|
|**primary_group_id**|int|주 복제본 및 보조 복제본의 사용자 작업에 대 한 작업 그룹 ID입니다.|
|**primary_group_max_workers**|int|사용자 작업 그룹에 대 한 작업자 스레드 제한입니다.|
|**primary_min_log_rate**|bigint|사용자 작업 그룹 수준에서 최소 로그 속도 (바이트/초)입니다. 리소스 관리는이 값 이하로 로그 율을 줄이려고 시도 하지 않습니다.|
|**primary_max_log_rate**|bigint|사용자 작업 그룹 수준에서 초당 최대 로그 속도 (바이트)입니다. 리소스 관리에서는이 값을 초과 하는 로그 전송률을 허용 하지 않습니다.|
|**primary_group_min_io**|int|사용자 작업 그룹의 최소 IOPS입니다. 리소스 관리는이 값 이하로 IOPS를 줄이려고 시도 하지 않습니다.|
|**primary_group_max_io**|int|사용자 작업 그룹에 대 한 최대 IOPS입니다. 리소스 관리에서는이 값을 초과 하는 IOPS를 허용 하지 않습니다.|
|**primary_group_min_cpu**|float|사용자 작업 그룹 수준에 대 한 최소 CPU 비율입니다. 리소스 관리는이 값 아래의 CPU 사용률을 줄이도록 시도 하지 않습니다.|
|**primary_group_max_cpu**|float|사용자 작업 그룹 수준에 대 한 최대 CPU 비율입니다. 리소스 관리에서는이 값을 초과 하는 CPU 사용률을 허용 하지 않습니다.|
|**primary_log_commit_fee**|int|사용자 작업 그룹의 로그 전송률 관리 커밋 요금 (바이트)입니다. 커밋 요금은 로그 율 계정에 대해서만 고정 값을 사용 하 여 각 로그 IO의 크기를 늘립니다. 저장소에 대 한 실제 로그 IO는 증가 되지 않습니다.|
|**primary_pool_max_workers**|int|사용자 작업 리소스 풀에 대 한 작업자 스레드 제한입니다.|
|**pool_max_io**|int|사용자 작업 리소스 풀에 대 한 최대 IOPS 제한입니다.|
|**govern_db_memory_in_resource_pool**|bit|내부적으로만 사용됩니다.|
|**volume_local_iops**|int|내부적으로만 사용됩니다.|
|**volume_managed_xstore_iops**|int|내부적으로만 사용됩니다.|
|**volume_external_xstore_iops**|int|내부적으로만 사용됩니다.|
|**volume_type_local_iops**|int|내부적으로만 사용됩니다.|
|**volume_type_managed_xstore_iops**|int|내부적으로만 사용됩니다.|
|**volume_type_external_xstore_iops**|int|내부적으로만 사용됩니다.|
|**volume_pfs_iops**|int|내부적으로만 사용됩니다.|
|**volume_type_pfs_iops**|int|내부적으로만 사용됩니다.|
|||

## <a name="permissions"></a>사용 권한

이 뷰에는 VIEW DATABASE STATE 권한이 필요합니다.

## <a name="remarks"></a>설명

Azure SQL Database의 리소스 관리에 대 한 설명은 [리소스 제한 SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server)을 참조 하세요.

> [!IMPORTANT]
> 이 DMV에서 반환 하는 대부분의 데이터는 내부 사용을 위한 것 이며 언제 든 지 변경 될 수 있습니다.

## <a name="examples"></a>예

사용자 데이터베이스의 컨텍스트에서 실행 되는 다음 쿼리는 사용자 작업 그룹 및 리소스 풀 수준에서 최대 로그 속도 및 최대 IOPS를 반환 합니다. 단일 데이터베이스의 경우 하나의 행이 반환 됩니다. 탄력적 풀의 데이터베이스에 대해 풀의 각 데이터베이스에 대해 행이 반환 됩니다.

```
SELECT database_name,
       primary_group_id,
       primary_max_log_rate,
       primary_group_max_io,
       pool_max_io
FROM sys.dm_user_db_resource_governance
ORDER BY database_name;  
```

## <a name="see-also"></a>참고 항목

- [리소스 관리자](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)
- [sys.dm_resource_governor_resource_pools(Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql)
- [sys.dm_resource_governor_workload_groups(Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql)
- [sys. dm_resource_governor_resource_pools_history_ex (Transact-sql)](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-history-ex-azure-sql-database)
- [sys.dm_resource_governor_workload_groups_history_ex(Azure SQL Database)](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-history-ex-azure-sql-database)
- [트랜잭션 로그 요금 거 버 넌 스](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [단일 데이터베이스 DTU 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [단일 데이터베이스 vCore 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
