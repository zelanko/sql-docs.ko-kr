---
title: sys.dm_resource_governor_external_resource_pools (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/02/2018
ms.suite: sql
ms.prod: sql
ms.technology: machine-learning
ms.reviewer: ''
ms.tgt_pltfrm: ''
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
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 80beafc8a281f7f4af71484acfa01ed0016b7de2
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39107665"
---
# <a name="sysdmresourcegovernorexternalresourcepools-transact-sql"></a>sys.dm_resource_governor_external_resource_pools (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

현재 외부 리소스 풀 상태, 리소스 풀 및 리소스 풀 통계의 현재 구성에 대 한 정보를 반환합니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
|열 이름      |데이터 형식      |Description|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|리소스 풀의 ID입니다. Null을 허용하지 않습니다. |
| NAME|**sysname**|리소스 풀의 이름입니다. Null을 허용하지 않습니다. 
| pool_version|**int**|내부 버전 번호입니다.|
| max_cpu_percent|**int**|CPU 충돌이 있을 때 리소스 풀의 모든 요청에 허용되는 최대 평균 CPU 대역폭에 대한 현재 구성입니다. Null을 허용하지 않습니다. |
| max_processes|**int**|동시 외부 프로세스의 최대 수입니다. 기본값은 0이며 제한 없음을 지정합니다. Null을 허용하지 않습니다.|
| max_memory_percent|**int**|이 리소스 풀의 요청에서 사용할 수 있는 총 서버 메모리의 비율에 대한 현재 구성입니다. Null을 허용하지 않습니다. |
| statistics_start_time|**datetime**|이 풀에 대해 통계가 다시 설정된 시간입니다. Null을 허용하지 않습니다. 
| peak_memory_kb|**bigint**|메모리 사용 (킬로바이트)에서 리소스 풀의 최대 양입니다. Null을 허용하지 않습니다. |
| write_io_count|**int**|리소스 관리자 통계를 다시 설정한 후 발생한 총 쓰기 IO입니다. Null을 허용하지 않습니다. |
| read_io_count|**int**|리소스 관리자 통계를 다시 설정한 후 발생한 총 읽기 IO입니다. Null을 허용하지 않습니다. |
| total_cpu_kernel_ms|**bigint**|누적 CPU 사용자 커널 시간 리소스 관리자 통계를 다시 설정한 후 시간 (밀리초)입니다. Null을 허용하지 않습니다. |
| total_cpu_user_ms|**bigint**|리소스 관리자 통계를 다시 설정한 후 시간 (밀리초)의 누적 CPU 사용자 시간이 있습니다. Null을 허용하지 않습니다. |
| active_processes_count|**int**|요청 시 실행 되는 외부 프로세스의 수입니다. Null을 허용하지 않습니다. |

 
## <a name="permissions"></a>사용 권한

`VIEW SERVER STATE` 권한이 필요합니다.

## <a name="see-also"></a>관련 항목  
 [sys.dm_resource_governor_external_resource_pool_affinity&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
