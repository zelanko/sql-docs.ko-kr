---
title: dm_db_resource_stats (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 05/21/2019
ms.service: sql-database
ms.reviewer: ''
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
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1dd66834788896e6952a0352eb2a19fd1a828513
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245959"
---
# <a name="sysdm_db_resource_stats-azure-sql-database"></a>sys.dm_db_resource_stats(Azure SQL 데이터베이스)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 데이터베이스에 대해 CPU, I/O 및 메모리 사용을 반환합니다. 데이터베이스에 작업이 없는 경우에도 한 행은 15초 간격으로 존재합니다. 기록 데이터는 약 1 시간 동안 유지 관리 됩니다.  
  
|열|데이터 형식|Description|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|현재 보고 간격의 끝을 나타내는 UTC 시간입니다.|  
|avg_cpu_percent|**decimal (5, 2)**|서비스 계층 한도의 비율로 계산된 평균 계산 활용률입니다.|  
|avg_data_io_percent|**decimal (5, 2)**|서비스 계층 한도의 백분율로 나타낸 평균 데이터 i/o 사용률입니다. Hyperscale 데이터베이스의 경우 [리소스 사용률 통계의 데이터 IO](https://docs.microsoft.com/azure/sql-database/sql-database-hyperscale-performance-diagnostics#data-io-in-resource-utilization-statistics)를 참조 하세요.|  
|avg_log_write_percent|**decimal (5, 2)**|서비스 계층 한도의 백분율로 나타낸 평균 트랜잭션 로그 쓰기 (MBps)입니다.|  
|avg_memory_usage_percent|**decimal (5, 2)**|서비스 계층 한도의 비율로 계산된 평균 메모리 활용률입니다.<br /><br /> 여기에는 메모리 내 OLTP 개체의 버퍼 풀 페이지 및 저장소에 사용 되는 메모리가 포함 됩니다.|  
|xtp_storage_percent|**decimal (5, 2)**|메모리 내 OLTP에 대 한 저장소 사용률 (보고 간격의 끝에 있는 서비스 계층의 제한 백분율) 여기에는 메모리 내 OLTP 개체를 저장 하는 데 사용 되는 메모리 (메모리 최적화 테이블, 인덱스 및 테이블 변수)가 포함 됩니다. 또한 ALTER TABLE 작업을 처리 하는 데 사용 되는 메모리가 포함 됩니다.<br /><br /> 데이터베이스에서 메모리 내 OLTP를 사용 하지 않는 경우 0을 반환 합니다.|  
|max_worker_percent|**decimal (5, 2)**|데이터베이스의 서비스 계층에 대 한 최대 동시 작업자 (요청) 한도의 백분율입니다.|  
|max_session_percent|**decimal (5, 2)**|데이터베이스 서비스 계층 한도의 비율로 나타낸 최대 동시 세션|  
|dtu_limit|**int**|이 간격 동안이 데이터베이스에 대 한 현재 최대 데이터베이스 DTU 설정입니다. VCore 기반 모델을 사용 하는 데이터베이스의 경우이 열은 NULL입니다.|
|cpu_limit|**decimal (5, 2)**|이 간격 동안의이 데이터베이스에 대 한 vCores 수입니다. DTU 기반 모델을 사용 하는 데이터베이스의 경우이 열은 NULL입니다.|
|avg_instance_cpu_percent|**decimal (5, 2)**|SQL DB 프로세스의 백분율로 나타낸 평균 데이터베이스 CPU 사용량입니다.|
|avg_instance_memory_percent|**decimal (5, 2)**|SQL DB 프로세스의 백분율로 나타낸 평균 데이터베이스 메모리 사용량입니다.|
|avg_login_rate_percent|**decimal (5, 2)**|정보를 제공하기 위해서만 확인됩니다. 지원되지 않습니다. 향후 호환성은 보장되지 않습니다.|
|replica_role|**int**|기본, 1을 보조로, 2를 전달자 (지역 보조의 기본)로 사용 하는 현재 복제본의 역할을 나타냅니다. 읽기 가능한 모든 보조 데이터베이스에 ReadOnly 의도를 사용 하 여 연결 된 경우 "1"이 표시 됩니다. 읽기 전용 의도를 지정 하지 않고 지역 보조 데이터베이스에 연결 하는 경우 "2" (전달자에 연결)가 표시 되어야 합니다.|
|||
  
> [!TIP]  
>  이러한 제한 및 서비스 계층에 대 한 자세한 컨텍스트는 [서비스](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) 계층 및 [서비스 계층 기능 및 제한](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)항목을 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 이 뷰에는 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 Dm_db_resource_stats에서 반환 된 데이터는 실행 중인 서비스 계층/성능 수준에 대해 허용 되는 최대 한도의 백분율로 표시 됩니다 **.**
 
 데이터베이스가 지난 60분 안에 다른 서버로 장애 조치된 경우 이 뷰는 해당 장애 조치 이후 주 데이터베이스였던 시간에 대해서만 데이터를 반환합니다.  
  
 보존 기간이 긴이 데이터에 대 한 보다 세분화 된 보기를 위해 **master** 데이터베이스에서 **resource_stats** 카탈로그 뷰를 사용 합니다. 이 뷰는 5분마다 데이터를 캡처하고 14일 동안 기록 데이터를 유지합니다.  자세한 내용은 [resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)를 참조 하세요.  
  
 데이터베이스가 탄력적 풀의 구성원이 면 백분율 값으로 표시 되는 리소스 통계가 탄력적 풀 구성에 설정 된 데이터베이스에 대 한 최대 한도의 백분율로 표시 됩니다.  
  
## <a name="example"></a>예제  
  
다음 예에서는 현재 연결된 데이터베이스에 대해 가장 최근 시간 순서로 리소스 사용 데이터를 반환합니다.  
  
```  
SELECT * FROM sys.dm_db_resource_stats ORDER BY end_time DESC;  
  
```  
  
 다음 예에서는 지난 시간 동안 사용자 데이터베이스에 대한 성능 수준에서 허용되는 최대 DTU 한도의 백분율 기준에서 평균 DTU 사용을 식별합니다. 이 비율이 일관되게 100%에 근접한다면 성능 수준 증대를 고려하는 것이 좋습니다.  
  
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
    AVG(avg_log_write_percent) AS 'Average Log Write I/O Throughput Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write I/O Throughput Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [서비스 계층](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [서비스 계층 기능 및 한도](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
