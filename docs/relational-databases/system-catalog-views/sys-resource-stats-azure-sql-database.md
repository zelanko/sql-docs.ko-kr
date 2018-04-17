---
title: sys.resource_stats (Azure SQL 데이터베이스) | Microsoft Docs
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
caps.latest.revision: 28
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7b8087839e5ea151d69a18cdf46d19fa5c917e66
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Azure SQL Database의 CPU 사용량 및 저장소 데이터를 반환합니다. 데이터는 5분 간격 이내로 수집 및 집계됩니다. 각 사용자 데이터베이스에서 한 행은 리소스 소비 변화에 대한 5분 간격 보고 창입니다. CPU 사용량, 저장소 크기 변경 또는 데이터베이스 SKU 수정 반환 되는 데이터에 포함 되어 있습니다. 변경 없이 유휴 데이터베이스 매 5 분 간격에 대 한 행을 가질 수 없습니다. 기록 데이터는 약 14일 동안 보존됩니다.  
  
 **sys.resource_stats** 뷰에 데이터베이스와 연결 된 Azure SQL 데이터베이스 서버 버전에 따라 서로 다른 정의 합니다. 이러한 차이점과 새 서버 버전으로 업그레이드할 경우 응용 프로그램에 필요한 모든 수정 사항을 고려하세요.  
  
 다음 표에는 v12 서버에서 사용할 수 있는 열이 설명되어 있습니다.  
  
|열|데이터 형식|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|5 분 보고 간격의 시작을 나타내는 UTC 시간입니다.|  
|end_time|**datetime**|5 분 보고 간격의 끝을 나타내는 UTC 시간입니다.|  
|database_name|**varchar**|사용자 데이터베이스의 이름입니다.|  
|sku|**varchar**|데이터베이스의 서비스 계층입니다. 가능한 값은 다음과 같습니다.<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium<br /><br />범용<br /><br />중요 비즈니스용|  
|storage_in_megabytes|**float**|메가바이트 데이터베이스 데이터, 인덱스, 저장된 프로시저 및 메타 데이터를 포함 하 여 시간 간격에 대 한 최대 저장소 크기입니다.|  
|avg_cpu_percent|**numeric**|서비스 계층 한도의 비율로 계산된 평균 계산 활용률입니다.|  
|avg_data_io_percent|**numeric**|서비스 계층 한도를 기준으로 하는 평균 I/O 활용률입니다.|  
|avg_log_write_percent|**numeric**|서비스 계층 한도의 비율로 계산된 평균 쓰기 리소스 활용률입니다.|  
|max_worker_percent|**decimal(5,2)**|데이터베이스의 서비스 계층의 제한을 기준 최대 동시 작업자 (요청 수)입니다.<br /><br /> 최대 동시 작업자 수의 15 초 샘플을 기반으로 하는 5 분 간격에 대 한 현재 계산 됩니다.|  
|max_session_percent|**decimal(5,2)**|데이터베이스의 서비스 계층의 제한을 기준 최대 동시 세션<br /><br /> 최대 동시 세션 수의 15 초 샘플을 기반으로 하는 5 분 간격에 대 한 현재 계산 됩니다.|  
|dtu_limit|**int**|현재 최대 데이터베이스 DTU 설정이이 데이터베이스에 대 한이 간격 동안입니다. |  
  
> [!TIP]  
>  이러한 제한 및 서비스 계층에 대 한 더 많은 컨텍스트 항목을 참조 하십시오. [서비스 계층](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)합니다.  
    
## <a name="permissions"></a>Permissions  
 이 뷰는 가상에 연결할 수 있는 권한 가진 모든 사용자 역할에 사용할 수 있는 **마스터** 데이터베이스입니다.  
  
## <a name="remarks"></a>주의  
 반환한 데이터 **sys.resource_stats** 은 실행 중인 서비스 계층/성능 수준에 대 한 제한은 허용 되는 최대의 백분율로 표현 됩니다.  
  
 탄력적 풀의 멤버 데이터베이스가 있는 경우 백분율 값으로 표시 되는 리소스 통계 탄력적 풀 구성에 설정 된 대로 데이터베이스에 대 한 최대 한계의 %로 표현 됩니다.  
  
 이 데이터의 더욱 세부적인 보기를 사용 하 여 **sys.dm_db_resource_stats** 동적 관리 뷰는 사용자 데이터베이스에 있습니다. 이 뷰의 데이터 15 초 마다 캡처하고 1 시간에 대 한 기록 데이터를 유지 합니다.  자세한 내용은 참조 [sys.dm_db_resource_stats &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)합니다.  

## <a name="examples"></a>예  
 다음 예에서는 지난 1주일 동안 평균적으로 계산 활용률의 80% 이상을 사용한 모든 데이터베이스를 반환합니다.  
  
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
    
## <a name="see-also"></a>관련 항목:  
 [서비스 계층](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [서비스 계층 기능 및 제한](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
