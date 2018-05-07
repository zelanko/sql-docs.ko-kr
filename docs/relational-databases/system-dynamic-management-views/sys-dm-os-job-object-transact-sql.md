---
title: sys.dm_os_job_object (Azure SQL 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology: system-objects
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1924f6c606d2d07d816409278cf9af56ecd868f8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmosjobobject-azure-sql-database"></a>sys.dm_os_job_object (Azure SQL 데이터베이스)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

작업 개체 수준에서 특정 리소스 소모량 통계와 SQL Server 프로세스를 관리 하는 작업 개체의 구성을 설명 하는 단일 행을 반환 합니다. SQL Server 작업 개체에서 실행 되지 않는 경우 빈 집합을 반환 합니다. 

작업 개체는 운영 체제 수준에서 CPU, 메모리 및 IO 리소스 관리를 구현 하는 Windows 생성 개체입니다. 작업 개체에 대 한 자세한 내용은 참조 [작업 개체](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx)합니다. 

> [!NOTE]
> sys.dm_os_job_object DMV 현재 sys.dm_job_object으로 나타날 수 있습니다. 이 임시: `sys.dm_os_job_object` 이 DMV의 영구 이름이 됩니다. 
  
|열|데이터 형식|Description|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|SQL Server 스레드는 각 일정 기간 동안 사용할 수 있는 프로세서 주기의 부분을 지정 합니다. 값은 10000 주기 일정이에서 사용할 수 있는 순환의 백분율로 보고 됩니다. 예를 들어 스레드 CPU 코어를 사용할 수 있는 값 100 의미의 전체 용량 됩니다.|
|cpu_affinity_mask|**bigint**|비트 마스크는 논리 프로세서를 설명 하는 SQL Server 프로세스 프로세서 그룹 내에서 사용할 수 있습니다. 예를 들어 cpu_affinity_mask 255 (이진수에서 1111 1111) 즉, 첫 번째 8 개 논리적 프로세서를 사용할 수 있습니다.|
|cpu_affinity_group|**int**|SQL Server에서 사용 되는 프로세서 그룹의 수입니다.|
|memory_limit_mb|**bigint**|SQL Server를 비롯 한 작업 개체의 모든 프로세스는 누적 되므로 사용할 수 있는 커밋된 메모리의 최대 양입니다.| 
|process_memory_limit_mb |**bigint**|SQL Server 등의 작업 개체에서 단일 프로세스에서 사용할 수 있는 커밋된 메모리의 최대 양입니다.|
|workingset_limit_mb |**bigint**|SQL Server 작업 집합을 사용할 수 있는 메모리의 최대 양입니다.|
|non_sos_mem_gap_mb|**bigint**|스레드 스택, Dll, 및 기타 비 SOS 메모리 할당에 대 한 mb에서 메모리 양의 따로 설정 합니다. SOS 대상 메모리 간의 차이점은 `process_memory_limit_mb` 및 `non_sos_mem_gap_mb`합니다.| 
|low_mem_signal_threshold_mb|**bigint**|메모리 임계값 (MB)입니다. 작업 개체에 대 한 사용 가능한 메모리 양을이 임계값 보다 낮으면 SQL Server 프로세스에 메모리 부족 알림 신호가 전송 됩니다. |
|total_user_time|**bigint**|작업 개체를 만든 후 사용자 모드에서 작업 개체 내에서 스레드 투자 100 ns 틱의 총 수입니다. |
|total_kernel_time |**bigint**|작업 개체 내에서 스레드는 데 소비한 커널 모드에서 작업 개체를 만든 후 해당 하는 100 ns 눈금의 총 수입니다. |
|write_operation_count |**bigint**|총 쓰기 IO 작업 작업 개체를 만든 후 SQL Server에서 발급 하는 로컬 디스크에 있습니다. |
|read_operation_count |**bigint**|작업 개체를 만든 후 SQL Server에서 발급 하는 로컬 디스크에서 읽기 IO 작업의 총 수입니다. |
|peak_process_memory_used_mb|**bigint**|작업 개체가 만들어진 이후에 단일 SQL Server와 같은 작업 개체에서 처리 하는 mb에서 메모리의 최대 양이 사용 됩니다.| 
|peak_job_memory_used_mb|**bigint**|모든 프로세스는 작업 개체에서 작업 개체 이후 누적 사용 mb에서 메모리의 최대 양을 만들었습니다.|
  
## <a name="permissions"></a>Permissions  
SQL 데이터베이스 관리 되는 인스턴스 필요 `VIEW SERVER STATE` 권한. SQL 데이터베이스에서 사용 하려면 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.  
 
## <a name="see-also"></a>관련 항목:  

관리 되는 인스턴스에서 정보를 참조 하십시오. [SQL 데이터베이스 관리 되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)합니다.
  
