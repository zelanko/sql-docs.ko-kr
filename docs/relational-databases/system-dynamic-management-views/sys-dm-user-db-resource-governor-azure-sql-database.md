---
title: sys.dm_user_db_resource_governance (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: d25c4d3cfe8628c01b44a99c6e26a96adf453050
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413069"
---
# <a name="sysdmuserdbresourcegovernance-transact-sql"></a>sys.dm_user_db_resource_governance (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

리소스 거 버 넌 스는 Azure SQL database에 대 한 구성 및 용량 설정을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|ssNoversion|Azure SQL Database 서버 내에서 고유한 데이터베이스의 ID입니다.|
|**logical_database_guid**|uniqueidentifier|사용자 데이터베이스와 사용자 데이터베이스의 수명이 길어질수록 유지에 대 한 논리적 guid입니다.  이름을 변경 하거나 데이터베이스를 다른 설정 SLO 변경 되지 않습니다 GUID. |
|**physical_database_guid**|uniqueidentifier|사용자 데이터베이스의 물리적 인스턴스의 수명 동안 통해 유지 되는 사용자 데이터베이스에 대 한 물리적 guid입니다. 설정 된 다른 SLO 변경할이 열이 하면 합니다.|
|**server_name**|NVARCHAR|논리 서버 이름입니다.|
|**database_name**|NVARCHAR|논리적 데이터베이스 이름입니다.|
|**slo_name**|NVARCHAR|서비스 수준 목표와 하드웨어 세대입니다.|
|**dtu_limit**|ssNoversion|(NULL에 대 한 vCore) 데이터베이스의 DTU 제한 합니다.|
|**cpu_limit**|ssNoversion|vCore 제한인 데이터베이스 (DTU 데이터베이스의 경우 NULL).|
|**min_cpu**|TINYINT|사용자 워크 로드에 따라 사용할 수 있는 최소 CPU 비율입니다.|
|**max_cpu**|TINYINT|사용자 워크 로드에 따라 사용할 수 있는 최대 CPU 비율입니다.|
|**cap_cpu**|TINYINT|사용자 워크 로드 그룹에 대 한 CPU 사용률의 상한입니다.|
|**min_cores**|SMALLINT|SQL에서 사용 된 Cpu의 수입니다.|
|**max_dop**|SMALLINT|최대 사용자 워크 로드를 사용한 병렬 처리 수준입니다.|
|**min_memory**|ssNoversion|사용자 워크 로드에 따라 사용할 수 있는 최소 메모리 비율입니다.|
|**max_memory**|ssNoversion|사용자 워크 로드에 따라 사용할 수 있는 최대 메모리 비율입니다.|
|**max_sessions**|ssNoversion|사용자 그룹에 대 한 세션 제한입니다.|
|**max_memory_grant**|ssNoversion|백분율에서 사용자 워크 로드에서 각 쿼리에 대 한 최대 메모리 부여 합니다.|
|**max_db_memory**|ssNoversion|사용자 DB 워크 로드에 대 한 최대 버퍼 풀 메모리 제한|
|**govern_background_io**|bit|백그라운드 쓰기가 사용자 그룹에는 요금이 부과 됩니다 있는지 여부를 나타냅니다.|
|**min_db_max_size_in_mb**|BIGINT|최소 최대 데이터베이스 파일 크기 (mb)입니다.|
|**max_db_max_size_in_mb**|BIGINT|최대 최대 데이터베이스 파일 (mb)입니다.|
|**default_db_max_size_in_mb**|BIGINT|기본 최대 데이터베이스 파일 크기 (mb)입니다.|
|**db_file_growth_in_mb**|BIGINT|Azure 데이터베이스 파일 (mb)의 기본 증가 합니다.|
|**initial_db_file_size_in_mb**|BIGINT|기본 데이터베이스 파일 크기 (mb)입니다.|
|**log_size_in_mb**|BIGINT|기본 로그 파일 크기 (mb)입니다.|
|**instance_cap_cpu**|ssNoversion|인스턴스 수준에서 CPU 한도입니다.|
|**instance_max_log_rate**|BIGINT|로그 생성 속도 한도 (초당 바이트)에서 인스턴스 수준에서.|
|**instance_max_worker_threads**|ssNoversion|인스턴스 수준에서 작업자 스레드 제한입니다.|
|**replica_type**|ssNoversion|여기서 0은 주, 1은 보조 복제본 형식입니다.|
|**max_transaction_size**|BIGINT|최대 로그 공간 (kb)에서의 모든 트랜잭션을 사용 합니다.|
|**checkpoint_rate_mbps**|ssNoversion|검사점 대역폭 (mbps)입니다.|
|**checkpoint_rate_io**|ssNoversion|검사점 IO IOs의 초당 비율입니다.|
|**last_updated_date_utc**|Datetime|날짜 및 시간 마지막 설정 변경 또는 재구성입니다.|
|**primary_group_id**|ssNoversion|기본 사용자 작업 그룹 id입니다.|
|**primary_group_max_workers**|ssNoversion|기본 사용자 워크 로드 그룹 수준에서 작업자 제한입니다.|
|**primary_min_log_rate**|BIGINT|기본 사용자 워크 로드 그룹 수준에서 최소 로그 속도 (초당 바이트)입니다.|
|**primary_max_log_rate**|BIGINT|기본 사용자 워크 로드 그룹 수준에서 최대 로그 속도 (초당 바이트)입니다.|
|**primary_group_min_io**|ssNoversion|기본 사용자 워크 로드 그룹 수준에서 최소 IO입니다.|
|**primary_group_max_io**|ssNoversion|기본 사용자 워크 로드 그룹 수준에서 최대 IO입니다.|
|**primary_group_min_cpu**|FLOAT|기본 사용자 워크 로드 그룹 수준에서 최소 CPU 비율 제한합니다.|
|**primary_group_max_cpu**|FLOAT|기본 사용자 워크 로드 그룹 수준에서 최대 CPU 비율 제한합니다.|
|**primary_log_commit_fee**|ssNoversion|로그 속도 거 버 넌 스 커밋 요금에 기본 사용자 워크 로드 그룹 수준에서 합니다.|
|**primary_pool_max_workers**|ssNoversion|기본 사용자 풀 수준에서 작업자 제한입니다.
|**pool_max_io**|ssNoversion|기본 사용자 풀 수준에서 최대 IO 제한 합니다.|
|**govern_db_memory_in_resource_pool**|bit|버퍼 풀의 최대 크기는 리소스 풀 수준에서 적용 여부를 표시 합니다. 일반적으로 탄력적 풀 내의 데이터베이스에 대해 설정 합니다.|
|**volume_local_iops**|ssNoversion|로컬 볼륨 (예: c:, d:)에 대 한 두 번째 값 당 IOs입니다.|
|**volume_managed_xstore_iops**|ssNoversion|IOs 원격 저장소 계정에 대 한 두 번째 값 당입니다.|
|**volume_external_xstore_iops**|ssNoversion|Azure SQL DB 백업 및 원격 분석에서 사용 하는 원격 저장소 계정에 대 한 두 번째 값 당 IOs입니다.|
|**volume_type_local_iops**|ssNoversion|모든 로컬 볼륨에 대 한 두 번째 값 당 IOs입니다.|
|**volume_type_managed_xstore_iops**|ssNoversion|인스턴스에서 사용 하는 모든 원격 저장소 계정에 대 한 두 번째 값 당 IOs입니다.|
|**volume_type_external_xstore_iops**|ssNoversion|Azure SQL DB 백업 및 원격 분석 사용 되는 인스턴스에 대 한 모든 원격 저장소 계정에 대 한 두 번째 값 당 IOs입니다.|
|**volume_pfs_iops**|ssNoversion|프리미엄 파일 저장소에 대 한 두 번째 값 당 IOs입니다.|
|**volume_type_pfs_iops**|ssNoversion|인스턴스에서 사용 하는 모든 프리미엄 파일 저장소에 대 한 두 번째 값 당 IOs입니다.|
|||

## <a name="permissions"></a>사용 권한

이 뷰에는 VIEW DATABASE STATE 권한이 필요합니다.

## <a name="remarks"></a>Remarks

사용자가 리소스 거 버 넌 스 구성에 대 한이 동적 관리 뷰 및 Azure SQL database에 대 한 용량 설정에 액세스할 수 있습니다. 

> [!IMPORTANT]
> 대부분이이 DMV에서 표시 하는 데이터의 내부 사용을 위한 것 이며 변경 될 수 있습니다.

## <a name="examples"></a>예

다음 예제에서는 인스턴스 최대 로그 속도 데이터를 단일 또는 풀링된 데이터베이스에 대 한 데이터베이스 서버 내에서 데이터베이스 이름으로 정렬 된를 반환 합니다.

```
SELECT database_name,
       primary_max_log_rate
FROM sys.dm_user_db_resource_governance
ORDER BY database_name DESC;  
```

## <a name="see-also"></a>관련 항목

- [트랜잭션 로그 속도 거 버 넌 스](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [단일 데이터베이스 DTU 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [단일 데이터베이스 vCore 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
