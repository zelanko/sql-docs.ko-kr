---
title: sys. dm_resource_governor_external_resource_pools (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.technology: machine-learning
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pools_TSQL
- sys.dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_external_resource_pools
- sys.dm_resource_governor_external_resource_pools
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: cf77a073a1432df839bfd13046c66018496e79f1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68468516"
---
# <a name="sysdm_resource_governor_external_resource_pools-transact-sql"></a>sys. dm_resource_governor_external_resource_pools (Transact-sql)
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

현재 외부 리소스 풀 상태, 리소스 풀의 현재 구성 및 리소스 풀 통계에 대 한 정보를 반환 합니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
|열 이름      |데이터 형식      |Description|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|리소스 풀의 ID입니다. Null을 허용하지 않습니다. |
| name|**sysname**|리소스 풀의 이름입니다. Null을 허용하지 않습니다. 
| pool_version|**int**|내부 버전 번호입니다.|
| max_cpu_percent|**int**|CPU 충돌이 있을 때 리소스 풀의 모든 요청에 허용되는 최대 평균 CPU 대역폭에 대한 현재 구성입니다. Null을 허용하지 않습니다. |
| max_processes|**int**|최대 동시 외부 프로세스 수입니다. 기본값은 0이며 제한 없음을 지정합니다. Null을 허용하지 않습니다.|
| max_memory_percent|**int**|이 리소스 풀의 요청에서 사용할 수 있는 총 서버 메모리의 비율에 대한 현재 구성입니다. Null을 허용하지 않습니다. |
| statistics_start_time|**datetime**|이 풀에 대해 통계가 다시 설정된 시간입니다. Null을 허용하지 않습니다. 
| peak_memory_kb|**bigint**|리소스 풀에 사용 되는 최대 메모리 양 (킬로바이트)입니다. Null을 허용하지 않습니다. |
| write_io_count|**int**|리소스 관리자 통계를 다시 설정한 후 발생한 총 쓰기 IO입니다. Null을 허용하지 않습니다. |
| read_io_count|**int**|리소스 관리자 통계를 다시 설정한 후 발생한 총 읽기 IO입니다. Null을 허용하지 않습니다. |
| total_cpu_kernel_ms|**bigint**|리소스 Govenor 통계가 다시 설정 된 후의 누적 CPU 사용자 커널 시간 (밀리초)입니다. Null을 허용하지 않습니다. |
| total_cpu_user_ms|**bigint**|리소스 Govenor 통계가 다시 설정 된 이후의 누적 CPU 사용자 시간 (밀리초)입니다. Null을 허용하지 않습니다. |
| active_processes_count|**int**|요청 순간에 실행되는 외부 프로세스의 수입니다. Null을 허용하지 않습니다. |

 
## <a name="permissions"></a>사용 권한

`VIEW SERVER STATE` 권한이 필요합니다.

## <a name="see-also"></a>참고 항목  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
