---
title: sys.elastic_pool_resource_stats
titleSuffix: Azure SQL Database
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
author: CarlRabeler
ms.author: carlrab
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 34f524eb8e6c7a64a53f64eda67a370aace745c3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85648899"
---
# <a name="syselastic_pool_resource_stats-azure-sql-database"></a>sys.elastic_pool_resource_stats (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  SQL Database 서버에서 모든 탄력적 풀에 대한 리소스 사용량 통계를 반환합니다. 각 탄력적 풀에는 15초의 보고 기간마다 행이 하나씩 있습니다(분당 행 4개) 여기에는 풀의 모든 데이터베이스에 의한 CPU, IO, 로그, 스토리지 계산 및 동시 요청/세션 사용률이 포함됩니다. 이 데이터는 14 일 동안 보존 됩니다. 
  
||  
|-|  
|**적용**대상: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|15 초 보고 간격의 시작을 나타내는 UTC 시간입니다.|  
|**end_time**|**datetime2**|15 초 보고 간격의 끝을 나타내는 UTC 시간입니다.|  
|**elastic_pool_name**|**nvarchar(128)**|탄력적 데이터베이스 풀의 이름입니다.|  
|**avg_cpu_percent**|**decimal (5, 2)**|풀 한도의 백분율로 평균 컴퓨팅 사용률.|  
|**avg_data_io_percent**|**decimal (5, 2)**|풀 한도에 따른 백분율로 평균 I/O 사용률|  
|**avg_log_write_percent**|**decimal (5, 2)**|풀 한도의 백분율로 평균 쓰기 리소스 사용률|  
|**avg_storage_percent**|**decimal (5, 2)**|풀의 스토리지 한도의 백분율로 평균 스토리지 사용률|  
|**max_worker_percent**|**decimal (5, 2)**|풀의 한도에 따른 백분율로 최대 동시 작업자(요청)|  
|**max_session_percent**|**decimal (5, 2)**|풀의 한도에 따른 백분율로 최대 동시 세션|  
|**elastic_pool_dtu_limit**|**int**|이 간격 중에 이 탄력적 풀에 대한 현재 최대 탄력적 풀 DTU 설정|  
|**elastic_pool_storage_limit_mb**|**bigint**|이 간격 중에 이 탄력적 풀에 대한 현재 최대 탄력적 풀 스토리지 제한 설정(MB)|
|**avg_allocated_storage_percent**|**decimal (5, 2)**|탄력적 풀의 모든 데이터베이스에서 할당 한 데이터 공간의 비율입니다.  탄력적 풀의 데이터 최대 크기에 할당 된 데이터 공간의 비율입니다.  자세한 내용은 [SQL DB의 파일 공간 관리](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management) 를 참조 하세요.|  
  
## <a name="remarks"></a>설명

 이 보기는 SQL Database 서버의 master 데이터베이스에 있습니다. **Elastic_pool_resource_stats**를 쿼리하려면 master 데이터베이스에 연결 되어 있어야 합니다.  
  
## <a name="permissions"></a>사용 권한

 **Dbmanager** 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예제

 다음 예에서는 현재 SQL Database 서버에 있는 모든 탄력적 데이터베이스 풀에 대해 가장 최근 시간 순으로 정렬 된 리소스 사용률 데이터를 반환 합니다.  
  
```sql
SELECT * FROM sys.elastic_pool_resource_stats
ORDER BY end_time DESC;  
```

 다음 예에서는 지정 된 풀에 대 한 평균 DTU 백분율 소비를 계산 합니다.  

```sql
SELECT start_time, end_time,
  (SELECT Max(v)
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]
FROM sys.elastic_pool_resource_stats
WHERE elastic_pool_name = '<your pool name>'
ORDER BY end_time DESC;  
```

## <a name="see-also"></a>참고 항목

 [탄력적 데이터베이스를 사용 하 여 끝날 때쯤 증가](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [SQL Database 탄력적 데이터베이스 풀 만들기 및 관리 (미리 보기)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
