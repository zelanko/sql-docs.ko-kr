---
title: sys.elastic_pool_resource_stats (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: reference
f1_keywords:
- sys.elastic_pool_resource_stats catalog view
helpviewer_keywords:
- sys.elastic_pool_resource_stats_TSQL
- sys.elastic_pool_resource_stats
- elastic_pool_resource_stats_TSQL
- elastic_pool_resource_stats
ms.assetid: f242c1bd-3cc8-4c8b-8aaf-c79b6a8a0329
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: ec3fae7d4e2a649ea05c48d400728e229607d92f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079268"
---
# <a name="syselasticpoolresourcestats-azure-sql-database"></a>sys.elastic_pool_resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  SQL Database 서버에서 모든 탄력적 풀에 대 한 리소스 사용 통계를 반환합니다. 각 탄력적 풀에 대 한 각 15 초 보고 창 (분당 4 개 행)에 대 한 하나의 행이 있습니다. 풀의 모든 데이터베이스에서 CPU, IO, 로그, 저장소 사용량 및 동시 요청/세션 사용률이 포함 됩니다. 이 데이터는 14 일 동안 보존 됩니다. 
  
||  
|-|  
|**적용 대상**:  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12입니다.|  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|15 초 보고 간격의 시작을 나타내는 UTC 시간입니다.|  
|**end_time**|**datetime2**|15 초 보고 간격의 끝을 나타내는 UTC 시간입니다.|  
|**elastic_pool_name**|**nvarchar(128)**|탄력적 데이터베이스 풀의 이름입니다.|  
|**avg_cpu_percent**|**decimal(5,2)**|풀 한도의 백분율로 평균 계산 사용률입니다.|  
|**avg_data_io_percent**|**decimal(5,2)**|풀 한도에 따른 백분율로 평균 I/O 활용률입니다.|  
|**avg_log_write_percent**|**decimal(5,2)**|평균 쓰기 리소스 사용률 풀 한도의 백분율입니다.|  
|**avg_storage_percent**|**decimal(5,2)**|풀의 저장소 한도의 백분율로 평균 저장소 사용률입니다.|  
|**max_worker_percent**|**decimal(5,2)**|풀 한도에 따른 백분율로 최대 동시 작업자 (요청).|  
|**max_session_percent**|**decimal(5,2)**|풀 한도에 따른 백분율로 최대 동시 세션|  
|**elastic_pool_dtu_limit**|**int**|현재 최대 탄력적 풀 DTU 설정이 탄력적 풀에 대 한 간격입니다.|  
|**elastic_pool_storage_limit_mb**|**bigint**|현재 최대 탄력적 풀 저장소 용량 한도이 간격 동안 메가바이트에서이 탄력적 풀에 대 한 설정입니다.|
|**avg_allocated_storage_percent**|**decimal(5,2)**|탄력적 풀에 있는 모든 데이터베이스에 의해 할당 되는 데이터 공간의 비율입니다.  이 탄력적 풀의 최대 크기 데이터에 할당 하는 데이터 공간의 비율입니다.  자세한 내용은 참조 하십시오. [SQL db에서 파일 공간 관리](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|  
  
## <a name="remarks"></a>설명

 이 보기는 SQL Database 서버의 마스터 데이터베이스에 있습니다. 쿼리를 master 데이터베이스에 연결 해야 **sys.elastic_pool_resource_stats**합니다.  
  
## <a name="permissions"></a>사용 권한

 멤버 자격이 필요 합니다 **dbmanager** 역할입니다.  
  
## <a name="examples"></a>예

 다음 예에서는 현재 SQL Database 서버에서 모든 elastic database 풀에 대 한 가장 최근 시간을 기준으로 정렬 하는 리소스 사용률 데이터를 반환 합니다.  
  
```sql
SELECT * FROM sys.elastic_pool_resource_stats
ORDER BY end_time DESC;  
```

 다음 예제에서는 지정된 된 풀에 대 한 평균 DTU 소비율을 계산합니다.  

```sql
SELECT start_time, end_time,
  (SELECT Max(v)
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]
FROM sys.elastic_pool_resource_stats
WHERE elastic_pool_name = '<your pool name>'
ORDER BY end_time DESC;  
```

## <a name="see-also"></a>관련 항목

 [탄력적 데이터베이스로 폭발적인 성장 제어](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [SQL Database elastic database 풀 (미리 보기)을 만들고 설정 합니다.](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [sys.resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [sys.dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
