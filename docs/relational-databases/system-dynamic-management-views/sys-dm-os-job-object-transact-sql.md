---
title: sys.dm_os_job_object (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
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
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: fdc778a34a513c2aca12da0dd0e1245e50dc5d6a
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716280"
---
# <a name="sysdmosjobobject-azure-sql-database"></a>sys.dm_os_job_object (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

특정 리소스 소비 통계 작업 개체 수준에서 뿐만 아니라 SQL Server 프로세스를 관리 하는 작업 개체의 구성을 설명 하는 단일 행을 반환 합니다. 작업 개체에서 SQL Server를 실행 하지 않는 경우 빈 집합을 반환 합니다. 

작업 개체는 운영 체제 수준에서 CPU, 메모리 및 IO 리소스 관리를 구현 하는 Windows 구문. 작업 개체에 대 한 자세한 내용은 참조 하세요. [작업 개체](/windows/desktop/ProcThread/job-objects)합니다. 
  
|열|데이터 형식|설명|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|SQL Server 스레드 예약 간격 동안 사용할 수 있는 프로세서 사이클의 부분을 지정 합니다. 값은 10000 주기 예약 간격 내에서 사용할 수 있는 주기의 백분율로 보고 됩니다. 예를 들어 스레드 CPU 코어를 사용할 수 있는 값의 100 의미는 해당 전체 용량입니다.|
|cpu_affinity_mask|**bigint**|논리적 프로세서를 설명 하는 비트 마스크를 SQL Server 프로세스의 프로세서 그룹 내에서 사용할 수 있습니다. 예를 들어 cpu_affinity_mask 255 (이진에서 1111 1111) 즉, 첫 번째 8 개 논리적 프로세서를 사용할 수 있습니다.|
|cpu_affinity_group|**int**|SQL Server에서 사용 되는 프로세서 그룹의 수입니다.|
|memory_limit_mb|**bigint**|커밋된 메모리 (mb)을 SQL Server를 비롯 한 작업 개체에서 모든 프로세스를 점증적으로 사용할 수 있는 최대 크기입니다.| 
|process_memory_limit_mb |**bigint**|커밋된 메모리 (mb)을 단일 SQL Server와 같은 작업 개체를 처리 하는 최대 크기를 사용할 수 있습니다.|
|workingset_limit_mb |**bigint**|SQL Server 작업 집합을 사용할 수 있는 메모리의 최대 양입니다.|
|non_sos_mem_gap_mb|**bigint**|Mb, 메모리의 양을 스레드 스택, Dll 및 다른 비 SOS 메모리 할당에 대해 따로 설정합니다. SOS 대상 메모리 간의 차이가 `process_memory_limit_mb` 고 `non_sos_mem_gap_mb`입니다.| 
|low_mem_signal_threshold_mb|**bigint**|메모리 임계값 (mb)입니다. 작업 개체에 대 한 사용 가능한 메모리의 양을이 임계값 보다 낮은 경우 SQL Server 프로세스 메모리 알림 신호가 보내집니다. |
|total_user_time|**bigint**|작업 개체 내에서 스레드 사용자 모드에서 소요 작업 개체를 만든 후 100 ns 틱의 총 수입니다. |
|total_kernel_time |**bigint**|작업 개체 내에서 스레드 커널 모드에서 소요 작업 개체를 만든 후 100 ns 틱의 총 수입니다. |
|write_operation_count |**bigint**|총 쓰기 작업 개체를 만든 후 SQL Server에서 발생 한 로컬 디스크 IO 작업입니다. |
|read_operation_count |**bigint**|작업 개체를 만든 후 SQL Server에서 발생 한 로컬 디스크에서 읽기 IO 작업의 총 수입니다. |
|peak_process_memory_used_mb|**bigint**|작업 개체를 만든 후 (mb)을 단일 SQL Server와 같은 작업 개체를 처리 하는 메모리의 최대 양이 사용 됩니다.| 
|peak_job_memory_used_mb|**bigint**|작업 개체 이후 작업 개체의 모든 프로세스를 점증적으로 사용한 MB 메모리의 최대 크기를 만들었습니다.|
  
## <a name="permissions"></a>사용 권한  
SQL Database Managed Instance 필요 `VIEW SERVER STATE` 권한. SQL Database에서 데이터베이스의 `VIEW DATABASE STATE` 권한이 필요합니다.  
 
## <a name="see-also"></a>관련 항목  

관리 되는 인스턴스에 대 한 정보를 참조 하세요 [SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)합니다.
  
