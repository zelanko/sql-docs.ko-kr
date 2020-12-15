---
description: sys.dm_os_job_object(Azure SQL Database)
title: sys.dm_os_job_object (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
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
monikerRange: = azuresqldb-current
ms.openlocfilehash: 456197c4519ca4135cf4a5edbf38d58c6d9246a8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472854"
---
# <a name="sysdm_os_job_object-azure-sql-database"></a>sys.dm_os_job_object(Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

작업 개체 수준에서 특정 리소스 소비 통계 뿐만 아니라 SQL Server 프로세스를 관리 하는 작업 개체의 구성을 설명 하는 단일 행을 반환 합니다. SQL Server 작업 개체에서 실행 되 고 있지 않은 경우 빈 집합을 반환 합니다.

작업 개체는 운영 체제 수준에서 CPU, 메모리 및 IO 리소스 관리를 구현 하는 Windows 구문입니다. 작업 개체에 대 한 자세한 내용은 [작업 개체](/windows/desktop/ProcThread/job-objects)를 참조 하세요.
  
|열|데이터 형식|설명|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|각 일정 간격 중에 SQL Server 스레드가 사용할 수 있는 프로세서 주기 부분을 지정 합니다. 값은 1만-주기 예약 간격 내에서 사용 가능한 주기의 백분율로 보고 되며 논리 Cpu 수를 곱합니다. 예를 들어 논리적 Cpu가 8 인 SQL Server 인스턴스의 값 800은 스레드가 Cpu를 사용할 수 있다는 것을 의미 합니다.|
|cpu_affinity_mask|**bigint**|SQL Server 프로세스가 프로세서 그룹 내에서 사용할 수 있는 논리 프로세서를 설명 하는 비트 마스크입니다. 예를 들어 cpu_affinity_mask 255 (이진의 1111 1111)는 처음 8 개의 논리적 프로세서를 사용할 수 있음을 의미 합니다. <br /><br />이 열은 이전 버전과의 호환성을 위해 제공 됩니다. 프로세서 그룹을 보고 하지 않으며 프로세서 그룹이 64 개 이상의 논리 프로세서를 포함 하는 경우 보고 된 값이 잘못 될 수 있습니다. 대신이 `process_physical_affinity` 열을 사용 하 여 프로세서 선호도를 확인 합니다.|
|cpu_affinity_group|**int**|SQL Server에서 사용 하는 프로세서 그룹의 번호입니다.|
|memory_limit_mb|**bigint**|SQL Server를 포함 하 여 작업 개체의 모든 프로세스가 누적 되 게 사용할 수 있는 커밋된 메모리의 최대 크기 (MB)입니다.| 
|process_memory_limit_mb |**bigint**|작업 개체의 단일 프로세스 (예: SQL Server)에서 사용할 수 있는 커밋된 메모리의 최대 크기 (MB)입니다.|
|workingset_limit_mb |**bigint**|SQL Server 작업 집합에서 사용할 수 있는 최대 메모리 양 (MB)입니다.|
|non_sos_mem_gap_mb|**bigint**|메모리 양 (MB)은 스레드 스택, Dll 및 기타 비 SOS 메모리 할당에 대해 따로 설정 됩니다. SOS 대상 메모리는과 간의 차이 `process_memory_limit_mb` 입니다 `non_sos_mem_gap_mb` .| 
|low_mem_signal_threshold_mb|**bigint**|메모리 임계값 (MB)입니다. 작업 개체에 사용 가능한 메모리 양이이 임계값 미만이 면 메모리 부족 알림 신호가 SQL Server 프로세스로 전송 됩니다. |
|total_user_time|**bigint**|작업 개체를 만든 후에 작업 개체 내 스레드가 사용자 모드에서 소비한 총 100 ns 틱 수입니다. |
|total_kernel_time |**bigint**|작업 개체를 만든 후에 작업 개체 내 스레드가 커널 모드에서 소비한 총 100 ns 틱 수입니다. |
|write_operation_count |**bigint**|작업 개체를 만든 후 SQL Server에서 발급 한 로컬 디스크에 대 한 쓰기 IO 작업의 총 수입니다. |
|read_operation_count |**bigint**|작업 개체를 만든 후 SQL Server에서 발급 한 로컬 디스크의 총 읽기 IO 작업 수입니다. |
|peak_process_memory_used_mb|**bigint**|작업 개체를 만든 후에 SQL Server와 같은 작업 개체의 단일 프로세스가 사용 된 메모리의 최대 크기 (MB)입니다.| 
|peak_job_memory_used_mb|**bigint**|작업 개체를 만든 후 작업 개체의 모든 프로세스가 누적 사용 된 최대 메모리 양 (MB)입니다.|
|process_physical_affinity|**nvarchar (3072)**|SQL Server 프로세스가 각 프로세서 그룹에서 사용할 수 있는 논리 프로세서를 설명 하는 비트 마스크입니다. 이 열의 값은 각각 중괄호로 묶인 하나 이상의 값 쌍으로 구성 됩니다. 각 쌍에서 첫 번째 값은 프로세서 그룹 번호이 고, 두 번째 값은 해당 프로세서 그룹에 대 한 선호도 비트 마스크입니다. 예를 들어 값은 `{{0,a}{1,2}}` 프로세서 그룹의 선호도 마스크가 `0` `a` ( `1010` 이진에서 프로세서 2와 4가 사용 됨을 나타냄)이 고 프로세서 그룹에 대 한 선호도 마스크는 `1` `2` ( `10` 이진에서 프로세서 2가 사용 됨을 나타냄) 임을 의미 합니다.|
  
## <a name="permissions"></a>사용 권한  
SQL Managed Instance에는 `VIEW SERVER STATE` 권한이 필요 합니다. SQL Database에서 데이터베이스의 `VIEW DATABASE STATE` 권한이 필요합니다.  
 
## <a name="see-also"></a>참고 항목  

관리 되는 인스턴스에 대 한 자세한 내용은 [SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)를 참조 하세요.
