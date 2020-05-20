---
title: sys. dm_resource_governor_resource_pool_volumes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_resource_pool_volumes_TSQL
- dm_resource_governor_resource_pool_volumes_TSQL
- dm_resource_governor_resource_pool_volumes
- sys.dm_resource_governor_resource_pool_volumes
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_resource_pool_volumes
- sys.dm_resource_governor_resource_pool_volumes
ms.assetid: fa692e56-c561-4533-97c5-bc12c600553f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f7b77d42eb45831eb6fbb800a5648d4706d738e1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827864"
---
# <a name="sysdm_resource_governor_resource_pool_volumes-transact-sql"></a>sys. dm_resource_governor_resource_pool_volumes (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  각 디스크 볼륨의 현재 리소스 풀 IO 통계에 관한 정보를 반환합니다. 이 정보는 [dm_resource_governor_resource_pools &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)의 리소스 풀 수준 에서도 사용할 수 있습니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|pool_id|**int**|리소스 풀의 ID입니다. Null을 허용하지 않습니다.|  
|volume_name|**sysname**|디스크 volue의 이름입니다. Null을 허용하지 않습니다.|  
|read_io_queued_total|**int**|리소스 관리자를 다시 설정한 후 큐에 놓인 총 읽기 IO입니다. Null을 허용하지 않습니다.|  
|read_io_issued_total|**int**|리소스 관리자 통계를 다시 설정한 후 발생한 총 읽기 IO입니다. Null을 허용하지 않습니다.|  
|read_ios_completed_total|**int**|리소스 관리자 통계를 다시 설정한 후 완료된 총 읽기 IO입니다. Null을 허용하지 않습니다.|  
|read_ios_throttled_total|**int**|리소스 관리자 통계를 다시 설정한 후 정체된 총 읽기 IO입니다. Null을 허용하지 않습니다.|  
|read_bytes_total|**bigint**|리소스 관리자 통계를 다시 설정한 후 읽은 총 바이트 수입니다. Null을 허용하지 않습니다.|  
|read_io_stall_total_ms|**bigint**|읽기 IO 도착과 완료 사이의 총 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|read_io_stall_queued_ms|**bigint**|읽기 IO 도착과 완료 사이의 총 시간(밀리초)입니다. IO 리소스 관리로 인해 발생한 지연 시간입니다. Null을 허용하지 않습니다.|  
|write_io_queued_total|**int**|리소스 관리자 통계를 다시 설정한 후 큐에 놓인 총 쓰기 IO입니다. Null을 허용하지 않습니다.|  
|write_io_issued_total|**int**|리소스 관리자 통계를 다시 설정한 후 발생한 총 쓰기 IO입니다. Null을 허용하지 않습니다.|  
|write_io_completed_total|**int**|리소스 관리자 통계를 다시 설정한 후 완료된 총 쓰기 IO입니다. Null을 허용하지 않습니다.|  
|write_io_throttled_total|**int**|리소스 관리자 통계를 다시 설정한 후 정체된 총 쓰기 IO입니다. Null을 허용하지 않습니다.|  
|write_bytes_total|**bigint**|리소스 관리자 통계를 다시 설정한 후 쓴 총 바이트 수입니다. Null을 허용하지 않습니다.|  
|write_io_stall_total_ms|**bigint**|쓰기 IO 발생과 완료 사이의 총 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|write_io_stall_queued_ms|**bigint**|쓰기 IO 도착과 완료 사이의 총 시간(밀리초)입니다. IO 리소스 관리로 인해 발생한 지연 시간입니다. Null을 허용하지 않습니다.|  
|io_issue_violations_total|**int**|총 IO 실행 위반 수입니다. 즉, IO 실행 속도가 예약된 속도보다 낮았던 횟수입니다. Null을 허용하지 않습니다.|  
|io_issue_delay_total_ms|**bigint**|예약된 IO 실행과 실제 IO 실행 사이의 총 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>권한  
 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참조  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [dm_resource_governor_workload_groups &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [resource_governor_resource_pools &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

