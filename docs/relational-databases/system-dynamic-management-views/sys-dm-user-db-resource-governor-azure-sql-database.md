---
title: sys. dm _user_db_ggggggggggggggg_l (Transact-sql) Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
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
ms.openlocfilehash: ea07ba28efc4ac50fdeef04bb1b3643c359ead28
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176261"
---
# <a name="sysdm_user_db_resource_governance-transact-sql"></a>sys. dm _user_l (Transact-sql)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Azure SQL Database 데이터베이스에 대 한 리소스 관리 구성 및 용량 설정을 반환 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**database_id**|int|Azure SQL Database 서버 내에서 고유한 데이터베이스의 ID입니다.|
|**logical_database_guid**|uniqueidentifier|사용자 데이터베이스의 논리적 guid 이며 사용자 데이터베이스의 수명 주기 동안 유지 됩니다.  데이터베이스 이름을 바꾸거나 다른 SLO로 설정 해도 GUID는 변경 되지 않습니다. |
|**physical_database_guid**|uniqueidentifier|사용자 데이터베이스의 실제 인스턴스 수명 동안 유지 되는 사용자 데이터베이스의 실제 guid입니다. 를 다른 SLO로 설정 하면이 열이 변경 됩니다.|
|**server_name**|NVARCHAR|논리 서버 이름입니다.|
|**database_name**|NVARCHAR|논리적 데이터베이스 이름입니다.|
|**slo_name**|NVARCHAR|서비스 수준 목표 및 하드웨어 생성.|
|**dtu_limit**|int|데이터베이스의 DTU 한도 (vCore의 경우 NULL)입니다.|
|**cpu_limit**|int|데이터베이스의 vCore 제한 (DTU 데이터베이스의 경우 NULL)입니다.|
|**min_cpu**|tinyint|사용자 작업에서 사용할 수 있는 최소 CPU 비율입니다.|
|**max_cpu**|tinyint|사용자 작업에서 사용할 수 있는 최대 CPU 비율입니다.|
|**cap_cpu**|tinyint|사용자 작업 그룹의 CPU 백분율 (%)입니다.|
|**min_cores**|SMALLINT|SQL에서 사용 하는 Cpu 수입니다.|
|**max_dop**|SMALLINT|사용자 작업에서 사용 하는 최대 병렬 처리 수준입니다.|
|**min_memory**|int|사용자 작업에서 사용할 수 있는 최소 메모리 비율입니다.|
|**max_memory**|int|사용자 작업에서 사용할 수 있는 최대 메모리 비율입니다.|
|**max_sessions**|int|사용자 그룹에 대 한 세션 제한입니다.|
|**max_memory_grant**|int|사용자 작업의 각 쿼리에 대 한 최대 메모리 부여 비율 (%)입니다.|
|**max_db_memory**|int|사용자 DB 작업에 대 한 최대 버퍼 풀 메모리 상한|
|**govern_background_io**|bit|배경 쓰기가 사용자 그룹에 부과 되는지 여부를 나타냅니다.|
|**min_db_max_size_in_mb**|bigint|최소 최대 데이터베이스 파일 크기 (MB)입니다.|
|**max_db_max_size_in_mb**|bigint|최대 최대 데이터베이스 파일 (MB)입니다.|
|**default_db_max_size_in_mb**|bigint|기본 최대 데이터베이스 파일 크기 (MB)입니다.|
|**db_file_growth_in_mb**|bigint|Azure 데이터베이스 파일의 기본 증가 (MB)입니다.|
|**initial_db_file_size_in_mb**|bigint|기본 데이터베이스 파일 크기 (MB)입니다.|
|**log_size_in_mb**|bigint|기본 로그 파일 크기 (MB)입니다.|
|**instance_cap_cpu**|int|인스턴스 수준에서 CPU 상한입니다.|
|**instance_max_log_rate**|bigint|인스턴스 수준에서 로그 생성 속도 상한 (바이트/초)입니다.|
|**instance_max_worker_threads**|int|인스턴스 수준에서 작업자 스레드 제한입니다.|
|**replica_type**|int|복제본 유형 (0은 primary, 1은 보조)입니다.|
|**max_transaction_size**|bigint|모든 트랜잭션에서 사용 되는 최대 로그 공간 (KB)입니다.|
|**checkpoint_rate_mbps**|int|검사점 대역폭 (Mbps)입니다.|
|**checkpoint_rate_io**|int|초당 IOs의 검사점 IO 요금입니다.|
|**last_updated_date_utc**|datetime|마지막 설정 변경 또는 재구성 날짜 및 시간입니다.|
|**primary_group_id**|int|기본 사용자 작업 그룹 ID입니다.|
|**primary_group_max_workers**|int|주 사용자 작업 그룹 수준의 작업자 한도입니다.|
|**primary_min_log_rate**|bigint|기본 사용자 작업 그룹 수준에서 최소 로그 속도 (초당 바이트)입니다.|
|**primary_max_log_rate**|bigint|기본 사용자 작업 그룹 수준에서 최대 로그 속도 (초당 바이트)입니다.|
|**primary_group_min_io**|int|기본 사용자 작업 그룹 수준의 최소 IO입니다.|
|**primary_group_max_io**|int|기본 사용자 작업 그룹 수준의 최대 IO입니다.|
|**primary_group_min_cpu**|FLOAT|기본 사용자 작업 그룹 수준에서 최소 CPU 비율 제한입니다.|
|**primary_group_max_cpu**|FLOAT|기본 사용자 작업 그룹 수준의 최대 CPU 비율 제한입니다.|
|**primary_log_commit_fee**|int|기본 사용자 작업 그룹 수준에서 로그 속도 거 버 넌 스 커밋 요금입니다.|
|**primary_pool_max_workers**|int|주 사용자 풀 수준의 작업자 한도입니다.
|**pool_max_io**|int|기본 사용자 풀 수준의 최대 IO 제한입니다.|
|**govern_db_memory_in_resource_pool**|bit|버퍼 풀의 최대 크기를 리소스 풀 수준에서 제어할 지 여부를 나타냅니다. 일반적으로 탄력적 풀 내의 데이터베이스에 대해 설정 됩니다.|
|**volume_local_iops**|int|로컬 볼륨 (예: C:, D:)에 대 한 초당 Io 수입니다.|
|**volume_managed_xstore_iops**|int|원격 저장소 계정에 대 한 초당 Io 수입니다.|
|**volume_external_xstore_iops**|int|Azure SQL DB 백업 및 원격 분석에서 사용 하는 원격 저장소 계정의 초당 Io 수입니다.|
|**volume_type_local_iops**|int|모든 로컬 볼륨의 초당 Io 수입니다.|
|**volume_type_managed_xstore_iops**|int|인스턴스에서 사용 하는 모든 원격 저장소 계정의 초당 Io 수입니다.|
|**volume_type_external_xstore_iops**|int|Azure SQL DB 백업 및 인스턴스에 대 한 원격 분석에서 사용 하는 모든 원격 저장소 계정의 초당 Io 수입니다.|
|**volume_pfs_iops**|int|프리미엄 파일 저장소에 대 한 초당 Io 수입니다.|
|**volume_type_pfs_iops**|int|인스턴스에서 사용 하는 모든 프리미엄 파일 저장소에 대 한 초당 Io 수입니다.|
|||

## <a name="permissions"></a>사용 권한

이 뷰에는 VIEW DATABASE STATE 권한이 필요합니다.

## <a name="remarks"></a>설명

사용자는 Azure SQL Database 데이터베이스에 대 한 리소스 관리 구성 및 용량 설정에 대해이 동적 관리 뷰에 액세스할 수 있습니다. 

> [!IMPORTANT]
> 이 DMV에 의해 표시 되는 대부분의 데이터는 내부 사용을 위한 것 이며 변경 될 수 있습니다.

## <a name="examples"></a>예

다음 예에서는 데이터베이스 서버 내에서 단일 또는 풀링된 데이터베이스에 대 한 데이터베이스 이름별로 정렬 된 인스턴스 최대 로그 전송률 데이터를 반환 합니다.

```
SELECT database_name,
       primary_max_log_rate
FROM sys.dm_user_db_resource_governance
ORDER BY database_name DESC;  
```

## <a name="see-also"></a>관련 항목

- [트랜잭션 로그 요금 거 버 넌 스](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [단일 데이터베이스 DTU 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [단일 데이터베이스 vCore 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
