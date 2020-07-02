---
title: resource_stats (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a72bb16eddc55f5cf741a7809665b44ada4a7a30
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717578"
---
# <a name="sysresource_stats-azure-sql-database"></a>sys.resource_stats(Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Azure SQL Database의 CPU 사용량 및 스토리지 데이터를 반환합니다. 데이터는 5분 간격 이내로 수집 및 집계됩니다. 각 사용자 데이터베이스에 대해 리소스 소비가 변경 된 5 분 마다 하나의 행이 있습니다. 반환 되는 데이터에는 CPU 사용량, 저장소 크기 변경 및 데이터베이스 SKU 수정이 포함 됩니다. 변경 내용이 없는 유휴 데이터베이스는 5 분 간격으로 행을 가질 수 없습니다. 기록 데이터는 약 14일 동안 보존됩니다.  
  
 **Resource_stats** 뷰는 데이터베이스가 연결 된 Azure SQL Database 서버의 버전에 따라 다른 정의가 있습니다. 이러한 차이점과 새 서버 버전으로 업그레이드할 경우 애플리케이션에 필요한 모든 수정 사항을 고려하세요.  
  
 다음 표에는 v12 서버에서 사용할 수 있는 열이 설명되어 있습니다.  
  
|열|데이터 형식|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|5 분 보고 간격의 시작을 나타내는 UTC 시간입니다.|  
|end_time|**datetime**|5 분 보고 간격의 끝을 나타내는 UTC 시간입니다.|  
|database_name|**nvarchar(128)**|사용자 데이터베이스의 이름입니다.|  
|sku|**nvarchar(128)**|데이터베이스의 서비스 계층입니다. 가능한 값은 다음과 같습니다.<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium<br /><br />범용<br /><br />중요 비즈니스용|  
|storage_in_megabytes|**float**|데이터베이스 데이터, 인덱스, 저장 프로시저 및 메타 데이터를 포함 하 여 기간에 대 한 최대 저장소 크기 (mb)입니다.|  
|avg_cpu_percent|**decimal (5, 2)**|서비스 계층 한도의 비율로 계산된 평균 계산 활용률입니다.|  
|avg_data_io_percent|**decimal (5, 2)**|서비스 계층 한도를 기준으로 하는 평균 I/O 활용률입니다. Hyperscale 데이터베이스의 경우 [리소스 사용률 통계의 데이터 IO](https://docs.microsoft.com/azure/sql-database/sql-database-hyperscale-performance-diagnostics#data-io-in-resource-utilization-statistics)를 참조 하세요.|  
|avg_log_write_percent|**decimal (5, 2)**|서비스 계층 한도의 비율로 계산된 평균 쓰기 리소스 활용률입니다.|  
|max_worker_percent|**decimal (5, 2)**|데이터베이스의 서비스 계층 한도에 따라 최대 동시 작업자 (요청)의 백분율입니다.<br /><br /> 현재 최대 개수는 동시 작업자 수의 15 초 샘플을 기반으로 5 분 간격으로 계산 됩니다.|  
|max_session_percent|**decimal (5, 2)**|데이터베이스의 서비스 계층 한도를 기준으로 하는 최대 동시 세션 (백분율)입니다.<br /><br /> 현재 최대는 동시 세션 수의 15 초 샘플을 기준으로 5 분 간격으로 계산 됩니다.|  
|dtu_limit|**int**|이 간격 동안이 데이터베이스에 대 한 현재 최대 데이터베이스 DTU 설정입니다. |
|xtp_storage_percent|**decimal (5, 2)**|메모리 내 OLTP에 대 한 저장소 사용률 (보고 간격의 끝에 있는 서비스 계층의 제한 백분율) 여기에는 메모리 내 OLTP 개체를 저장 하는 데 사용 되는 메모리 (메모리 최적화 테이블, 인덱스 및 테이블 변수)가 포함 됩니다. 또한 ALTER TABLE 작업을 처리 하는 데 사용 되는 메모리가 포함 됩니다.<br /><br /> 데이터베이스에서 메모리 내 OLTP를 사용 하지 않는 경우 0을 반환 합니다.|
|avg_login_rate_percent|**decimal (5, 2)**|정보를 제공하기 위해서만 확인됩니다. 지원 안 됨 향후 호환성은 보장되지 않습니다.|
|avg_instance_cpu_percent|**decimal (5, 2)**|SQL DB 프로세스의 백분율로 나타낸 평균 데이터베이스 CPU 사용량입니다.|
|avg_instance_memory_percent|**decimal (5, 2)**|SQL DB 프로세스의 백분율로 나타낸 평균 데이터베이스 메모리 사용량입니다.|
|cpu_limit|**decimal (5, 2)**|이 간격 동안의이 데이터베이스에 대 한 vCores 수입니다. DTU 기반 모델을 사용 하는 데이터베이스의 경우이 열은 NULL입니다.|
|allocated_storage_in_megabytes|**float**|데이터베이스 데이터를 저장 하는 데 사용할 수 있는 서식 있는 파일 공간의 크기 (MB)입니다. 형식이 지정 된 파일 공간을 할당 된 데이터 공간이 라고도 합니다.  자세한 내용은 [SQL DB의 파일 공간 관리](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management) 를 참조 하세요.|
  
> [!TIP]  
>  이러한 제한 및 서비스 계층에 대 한 자세한 컨텍스트는 [서비스 계층](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)항목을 참조 하세요.  
    
## <a name="permissions"></a>사용 권한  
 이 보기는 가상 **master** 데이터베이스에 연결할 수 있는 권한이 있는 모든 사용자 역할에 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 Resource_stats에서 반환 된 데이터는 실행 중인 서비스 계층/성능 수준에 대해 허용 되는 최대 한도의 백분율로 표시 됩니다 **.**  
  
 데이터베이스가 탄력적 풀의 구성원이 면 백분율 값으로 표시 되는 리소스 통계가 탄력적 풀 구성에 설정 된 데이터베이스에 대 한 최대 한도의 백분율로 표시 됩니다.  
  
 이 데이터에 대 한 자세한 보기를 보려면 사용자 데이터베이스에서 **dm_db_resource_stats** 동적 관리 뷰를 사용 합니다. 이 뷰는 15초마다 데이터를 캡처하고 1시간 동안 기록 데이터를 유지합니다.  자세한 내용은 [dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)를 참조 하세요.  

## <a name="examples"></a>예제  
 다음 예에서는 지난 1주일 동안 평균적으로 컴퓨팅 활용률의 80% 이상을 사용한 모든 데이터베이스를 반환합니다.  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT database_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY database_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>참고 항목  
 [서비스 계층](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [서비스 계층 기능 및 한도](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
