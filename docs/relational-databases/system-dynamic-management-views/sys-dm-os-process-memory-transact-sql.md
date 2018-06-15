---
title: sys.dm_os_process_memory (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_process_memory_TSQL
- dm_os_process_memory_TSQL
- dm_os_process_memory
- sys.dm_os_process_memory
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_process_memory dynamic management view
ms.assetid: e838130c-95d4-4605-9e3b-eb0ab71cd250
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5732a15fe8fe2d30f6f9c693e66258c0de4b44d3
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34467799"
---
# <a name="sysdmosprocessmemory-transact-sql"></a>sys.dm_os_process_memory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 공간에 소요되는 대부분의 메모리 할당은 이러한 할당을 추적 및 계산하도록 허용된 인터페이스를 통해 제어됩니다. 그러나 메모리 할당은 내부 메모리 관리 루틴을 거치지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 주소 공간에서 수행될 수도 있습니다. 값은 기본 운영 체제 호출을 통해 얻습니다. 내부 메서드에 의해 조작 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 조절 하는 경우 잠금에 대 한 또는 대용량 페이지 할당 제외 하 고 있습니다.  
  
 메모리 크기를 나타내는 모든 반환 값은 킬로바이트(KB) 단위로 표시됩니다. 열 **total_virtual_address_space_reserved_kb** 가 중복 **virtual_memory_in_bytes** 에서 **sys.dm_os_sys_info**합니다.  
  
 다음 표에서는 프로세스 주소 공간의 전체적인 구조를 보여 줍니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_process_memory**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|운영 체제에서 보고한 내용에 대용량 페이지 API를 사용하여 수행된 추적된 할당을 더한 프로세스 작업 집합(KB)을 나타냅니다. Null을 허용하지 않습니다.|  
|**large_page_allocations_kb**|**bigint**|대용량 페이지 API를 사용하여 할당된 물리적 메모리를 지정합니다. Null을 허용하지 않습니다.|  
|**locked_page_allocations_kb**|**bigint**|메모리에서 잠긴 메모리 페이지를 지정합니다. Null을 허용하지 않습니다.|  
|**total_virtual_address_space_kb**|**bigint**|가상 주소 공간의 사용자 모드 부분의 총 크기를 나타냅니다. Null을 허용하지 않습니다.|  
|**virtual_address_space_reserved_kb**|**bigint**|프로세스에 예약된 가상 주소 공간의 총 크기를 나타냅니다. Null을 허용하지 않습니다.|  
|**virtual_address_space_committed_kb**|**bigint**|물리적 페이지에 커밋되거나 매핑된 예약된 가상 주소 공간의 크기를 나타냅니다. Null을 허용하지 않습니다.|  
|**virtual_address_space_available_kb**|**bigint**|현재 사용 가능한 가상 주소 공간의 크기를 나타냅니다. Null을 허용하지 않습니다.<br /><br /> **참고:** 존재할 수는 할당 세분성 보다 작은 영역을 해제 합니다. 이러한 영역은 할당에 사용할 수 없습니다.|  
|**page_fault_count**|**bigint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에서 발생한 페이지 폴트 수를 나타냅니다. Null을 허용하지 않습니다.|  
|**memory_utilization_percentage**|**int**|작업 집합에 있는 커밋된 메모리의 비율을 지정합니다. Null을 허용하지 않습니다.|  
|**available_commit_limit_kb**|**bigint**|프로세스에서 커밋할 수 있는 메모리의 양을 나타냅니다. Null을 허용하지 않습니다.|  
|**process_physical_memory_low**|**bit**|프로세스가 물리적 메모리 부족 알림에 응답함을 나타냅니다. Null을 허용하지 않습니다.|  
|**process_virtual_memory_low**|**bit**|가상 메모리 공간이 부족한 것으로 감지되었음을 나타냅니다. Null을 허용하지 않습니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 대 한 VIEW SERVER STATE 권한이 필요 합니다.  
  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


