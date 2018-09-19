---
title: sys.resource_stats (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: ea822937f8bdf6fe0a79c20a391976169d336610
ms.sourcegitcommit: b8e2e3e6e04368aac54100c403cc15fd4e4ec13a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45563989"
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Azure SQL Database의 CPU 사용량 및 저장소 데이터를 반환합니다. 데이터는 5분 간격 이내로 수집 및 집계됩니다. 각 사용자 데이터베이스에 대해 5-분 간격 보고 창은 변경 될 리소스 소비량에서에 대해 한 행씩이 있습니다. 반환 되는 데이터는 CPU 사용량, 저장소 크기 변경 및 데이터베이스 SKU 수정 포함 되어 있습니다. 변경 하지 않고 유휴 데이터베이스 5 분 간격에 대 한 행을 가질 수 없습니다. 기록 데이터는 약 14일 동안 보존됩니다.  
  
 합니다 **sys.resource_stats** 보기에는 데이터베이스와 연결 된 Azure SQL Database 서버 버전에 따라 다른 정의가 포함 됩니다. 이러한 차이점과 새 서버 버전으로 업그레이드할 경우 응용 프로그램에 필요한 모든 수정 사항을 고려하세요.  
  
 다음 표에는 v12 서버에서 사용할 수 있는 열이 설명되어 있습니다.  
  
|열|데이터 형식|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|5 분 보고 간격의 시작을 나타내는 UTC 시간입니다.|  
|end_time|**datetime**|5 분 보고 간격의 끝을 나타내는 UTC 시간입니다.|  
|database_name|**varchar**|사용자 데이터베이스의 이름입니다.|  
|sku|**varchar**|데이터베이스의 서비스 계층입니다. 가능한 값은 다음과 같습니다.<br /><br /> Basic<br /><br /> 표준<br /><br /> Premium<br /><br />범용<br /><br />중요 비즈니스용|  
|storage_in_megabytes|**float**|데이터베이스 데이터, 인덱스, 저장된 프로시저 및 메타 데이터를 포함 하 여 기간에 대 한 메가바이트 최대 저장소 크기입니다.|  
|avg_cpu_percent|**numeric**|서비스 계층 한도의 비율로 계산된 평균 계산 활용률입니다.|  
|avg_data_io_percent|**numeric**|서비스 계층 한도를 기준으로 하는 평균 I/O 활용률입니다.|  
|avg_log_write_percent|**numeric**|서비스 계층 한도의 비율로 계산된 평균 쓰기 리소스 활용률입니다.|  
|max_worker_percent|**decimal(5,2)**|데이터베이스의 서비스 계층 한도에 따른 백분율로 최대 동시 작업자 (요청).<br /><br /> 최대 동시 작업자 수 15 초 샘플을 기반으로 하는 5 분 간격에 대 한 현재 계산 됩니다.|  
|max_session_percent|**decimal(5,2)**|데이터베이스의 서비스 계층 한도에 따른 백분율로 최대 동시 세션<br /><br /> 최대 동시 세션 수의 15 초 샘플을 기반으로 하는 5 분 간격에 대 한 현재 계산 됩니다.|  
|dtu_limit|**int**|현재 최대 데이터베이스 DTU 설정이이 데이터베이스에 대 한 간격입니다. |  
|allocated_storage_in_megabytes|**float**|양을 형식 파일 공간 (mb) 데이터베이스 데이터를 저장 하는 데 사용할 수 있습니다. 서식이 지정 된 파일 공간 데이터 공간 할당 라고도 합니다.  자세한 내용은 참조: [SQL db에서 파일 공간 관리](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|
  
> [!TIP]  
>  이러한 제한 및 서비스 계층에 대 한 더 많은 컨텍스트 항목을 참조 하세요 [서비스 계층](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)합니다.  
    
## <a name="permissions"></a>사용 권한  
 이 보기는 가상으로 연결할 수 있는 권한 가진 모든 사용자 역할에 사용할 수 있습니다 **마스터** 데이터베이스입니다.  
  
## <a name="remarks"></a>Remarks  
 반환한 데이터 **sys.resource_stats** 최대 허용 실행 중인 서비스 계층/성능 수준의 한도의 백분율로 표현 됩니다.  
  
 데이터베이스를 탄력적 풀의 멤버인 경우 백분율 값으로 표시 하는 리소스 통계는 탄력적 풀 구성에 설정 된 대로 데이터베이스에 대 한 최대 한도의 백분율로 표현 됩니다.  
  
 이 데이터의 더욱 세부적인 보기를 사용 하 여 **sys.dm_db_resource_stats** 사용자 데이터베이스에서 동적 관리 뷰. 이 뷰는 15초마다 데이터를 캡처하고 1시간 동안 기록 데이터를 유지합니다.  자세한 내용은 [sys.dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)합니다.  

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
    
## <a name="see-also"></a>관련 항목  
 [서비스 계층](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [서비스 계층 기능 및 제한](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
