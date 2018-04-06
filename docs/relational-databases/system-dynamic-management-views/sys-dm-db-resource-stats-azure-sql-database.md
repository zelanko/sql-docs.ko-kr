---
title: sys.dm_db_resource_stats (Azure SQL 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 116c5875ad7933e1b3d68f0c65ca7d0cb4d2b661
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmdbresourcestats-azure-sql-database"></a>sys.dm_db_resource_stats(Azure SQL 데이터베이스)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  CPU, I/O 및 메모리 사용에 대 한 반환는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 데이터베이스입니다. 데이터베이스에서 활동이 없더라도 15초 간격으로 한 행이 있습니다. 기록 데이터는 한 시간 동안 유지됩니다.  
  
|열|데이터 형식|Description|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|현재 보고 간격의 끝을 나타내는 UTC 시간입니다.|  
|avg_cpu_percent|**10 진수 (5,2)**|서비스 계층 한도의 비율로 계산된 평균 계산 활용률입니다.|  
|avg_data_io_percent|**10 진수 (5,2)**|평균 데이터 서비스 계층 제한의 I/O 활용률입니다.|  
|avg_log_write_percent|**10 진수 (5,2)**|서비스 계층 한도의 비율로 계산된 평균 쓰기 리소스 활용률입니다.|  
|avg_memory_usage_percent|**10 진수 (5,2)**|서비스 계층 한도의 비율로 계산된 평균 메모리 활용률입니다.<br /><br /> 메모리 내 OLTP 개체의 저장에 사용 된 메모리 포함 됩니다.|  
|xtp_storage_percent|**10 진수 (5,2)**|저장소 사용률이 메모리 내 OLTP에 대 한 서비스 계층 한도의 비율로 (보고 간격의 끝). 여기에 다음 메모리 내 OLTP 개체의 저장에 사용 된 메모리: 메모리 액세스에 최적화 된 테이블, 인덱스 및 테이블 변수입니다. ALTER TABLE 작업을 처리 하기 위해 사용 되는 메모리 포함 됩니다.<br /><br /> 데이터베이스에 메모리 내 OLTP를 사용 하지 않는 경우 0을 반환 합니다.|  
|max_worker_percent|**10 진수 (5,2)**|데이터베이스의 서비스 계층 한도의 비율로 최대 동시 작업자 (요청 수)입니다.|  
|max_session_percent|**10 진수 (5,2)**|데이터베이스의 서비스 계층 한도의 비율로 최대 동시 세션|  
|dtu_limit|**int**|현재 최대 데이터베이스 DTU 설정이이 데이터베이스에 대 한이 간격 동안입니다.|  
  
> [!TIP]  
>  이러한 제한 및 서비스 계층에 대 한 더 많은 컨텍스트 항목을 참조 하십시오. [서비스 계층](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) 및 [서비스 계층 기능 및 제한](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)합니다.  
  
## <a name="permissions"></a>Permissions  
 이 뷰에는 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>주의  
 반환한 데이터 **sys.dm_db_resource_stats** 은 Basic, Standard 및 Premium 데이터베이스에 대 한 실행 중인 서비스 계층/성능 수준에 대 한 DTU 제한 허용 되는 최대의 백분율로 표현 됩니다.
 
 데이터베이스가 지난 60분 안에 다른 서버로 장애 조치된 경우 이 뷰는 해당 장애 조치 이후 주 데이터베이스였던 시간에 대해서만 데이터를 반환합니다.  
  
 이 데이터의 덜 세분화 된 뷰를 사용 하 여 **sys.resource_stats** 카탈로그 뷰는 **마스터** 데이터베이스입니다. 이 뷰는 5분마다 데이터를 캡처하고 14일 동안 기록 데이터를 유지합니다.  자세한 내용은 참조 [sys.resource_stats &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)합니다.  
  
 탄력적 풀의 멤버 데이터베이스가 있는 경우 백분율 값으로 표시 되는 리소스 통계 탄력적 풀 구성에 설정 된 대로 데이터베이스에 대 한 최대 DTU 제한의 백분율로 표현 됩니다.  
  
## <a name="example"></a>예제  
  
다음 예에서는 현재 연결된 데이터베이스에 대해 가장 최근 시간 순서로 리소스 사용 데이터를 반환합니다.  
  
```  
SELECT * FROM sys.dm_db_resource_stats ORDER BY end_time DESC;  
  
```  
  
 다음 예에서는 지난 시간 동안 사용자 데이터베이스에 대한 성능 수준에서 허용되는 최대 DTU 한도의 백분율 기준에서 평균 DTU 사용을 식별합니다.  이 비율이 일관되게 100%에 근접한다면 성능 수준 증대를 고려하는 것이 좋습니다.  
  
```  
SELECT end_time,   
  (SELECT Max(v)    
   FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS    
   value(v)) AS [avg_DTU_percent]   
FROM sys.dm_db_resource_stats;  
  
```  
  
 다음 예에서는 지난 시간 동안의 평균 및 최대 CPU %, 데이터 및 로그 I/O, 메모리 사용을 반환합니다.   
  
```  
SELECT    
    AVG(avg_cpu_percent) AS 'Average CPU Utilization In Percent',   
    MAX(avg_cpu_percent) AS 'Maximum CPU Utilization In Percent',   
    AVG(avg_data_io_percent) AS 'Average Data IO In Percent',   
    MAX(avg_data_io_percent) AS 'Maximum Data IO In Percent',   
    AVG(avg_log_write_percent) AS 'Average Log Write Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.resource_stats &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [서비스 계층](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [서비스 계층 기능 및 제한](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
