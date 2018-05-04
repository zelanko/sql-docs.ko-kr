---
title: sys.elastic_pool_resource_stats (Azure SQL 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- Azure SQL Database
f1_keywords:
- sys.elastic_pool_resource_stats catalog view
helpviewer_keywords:
- sys.elastic_pool_resource_stats_TSQL
- sys.elastic_pool_resource_stats
- elastic_pool_resource_stats_TSQL
- elastic_pool_resource_stats
ms.assetid: f242c1bd-3cc8-4c8b-8aaf-c79b6a8a0329
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 8b89f1719c5fe8b63b101066cd5f159873f2063b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="syselasticpoolresourcestats-azure-sql-database"></a>sys.elastic_pool_resource_stats (Azure SQL 데이터베이스)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  논리 서버에 모든 탄력적 데이터베이스 풀에 대 한 리소스 사용 통계를 반환합니다. 각 탄력적 데이터베이스 풀에 대해 15 초 창 (분당 4 개 행)를 보고에 대 한 하나의 행이 있습니다. 풀의 모든 데이터베이스에서 CPU, IO, 로그, 저장소 사용량 및 동시 요청/세션 사용률을 포함 합니다. 이 데이터는 14 일 동안 보존 됩니다. 
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12 합니다.|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|15 초 보고 간격의 시작을 나타내는 UTC 시간입니다.|  
|**end_time**|**datetime2**|15 초 보고 간격의 끝을 나타내는 UTC 시간입니다.|  
|**elastic_pool_name**|**nvarchar(128)**|탄력적 데이터베이스 풀의 이름입니다.|  
|**avg_cpu_percent**|**decimal(5,2)**|풀의도의 비율로 평균 계산 활용률입니다.|  
|**avg_data_io_percent**|**decimal(5,2)**|풀의 제한을 기준 평균 I/O 활용률입니다.|  
|**avg_log_write_percent**|**decimal(5,2)**|평균 쓰기 리소스 활용률 풀도 비율로 합니다.|  
|**avg_storage_percent**|**decimal(5,2)**|풀의 저장소 용량 한도의 비율로 저장소 사용률을 평균입니다.|  
|**max_worker_percent**|**decimal(5,2)**|풀의 제한을 기준 최대 동시 작업자 (요청 수)입니다.|  
|**max_session_percent**|**decimal(5,2)**|풀의 제한을 기준 최대 동시 세션|  
|**elastic_pool_dtu_limit**|**int**|현재 최대 탄력적인 풀 DTU 설정이 탄력적 풀에 대 한이 간격 동안입니다.|  
|**elastic_pool_storage_limit_mb**|**bigint**|현재 최대 탄력적인 풀 저장소 용량 한도이 간격 동안이 탄력적인 풀이 (메가바이트)에서에 대 한 설정입니다.|  
  
## <a name="remarks"></a>주의  
 이 보기는 논리 서버 master 데이터베이스에 존재합니다. 쿼리를 master 데이터베이스에 연결 해야 **sys.elastic_pool_resource_stats**합니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **dbmanager** 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 모든 탄력적 데이터베이스 풀은 현재 논리 서버에 대 한 가장 최근 시간 순서로 리소스 사용률 데이터를 반환 합니다.  
  
```  
SELECT * FROM sys.elastic_pool_resource_stats   
ORDER BY end_time DESC;  
```  
  
 다음 예제에서는 지정된 된 풀에 대 한 평균 DTU 소비율을 계산 합니다.  
  
```  
SELECT start_time, end_time,      
  (SELECT Max(v)      
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]    
FROM sys.elastic_pool_resource_stats   
WHERE elastic_pool_name = '<your pool name>'   
ORDER BY end_time DESC;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [탄력적 데이터베이스와 함께 해소 폭발적 증가](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [만들기 및 관리 (미리 보기)는 SQL 데이터베이스 탄력적 데이터베이스 풀](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [sys.resource_stats &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [sys.dm_db_resource_stats &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
